API
===

Introduction
--------------



The software we developed has a client-server architecture with 3 parts:

- Frontend
- Backend
- PostgreSQL Database

How does our application work:
--------------------------

In order for a client to request a resource for example the client is requesting subjects, a http request would be made to the server to a specific endpoint. A function in the backend is called based on the specific endpoint which fetches data from the PostgreSQL database. Due to the way our project is implemented, there has to be a bridge between the PostgreSQL database and the Python backend. We decided to use Pyscopg2 which is a PostgreSQL adapter for Python which provides developers with detailed control over SQL queries and database interactions. Psycopg2 is required to establish database connections, execute SQL queries, handle transactions and fetch and process data. Without it, the server would be unable to respond to http requests sent via the frontend. There would be no database connection between the backend and the database. 

A custom API has been implemented in the learning application using http.server module in Python, it provides provides endpoints for managing and retrieving data for a quiz application. It interacts with a PostgreSQL database using psycopg2 and supports functionalities such as fetching subjects (/subjects), topics (/topics), quizzes (/quiz), and quiz questions with answers (/quiz_questions). It also includes endpoints for user management, such as creating accounts (/create_account), account authentication (/login), and submitting quiz attempts (/submit_attempts). The API returns JSON responses, handles errors gracefully, and includes CORS support for seamless integration with frontend applications like Flutter.

.. code-block:: python

   class S(BaseHTTPRequestHandler):
       def do_GET(self):
           parsed_path = urlparse(self.path)
           if self.path == '/subjects':
               subjects = fetchSubjects()
               self.send_response(200)
               self.send_header('Access-Control-Allow-Origin', '*')  # Allow all origins
               self.send_header('Content-type','application/json')
               self.end_headers()
               self.wfile.write(json.dumps(subjects, indent = 2).encode('utf-8'))




Upon the client sending a http request to the server, the class S is triggered in the backend due to the http request being a GET request. The http request is sent to a specific endpoint exposed by the server, the urlparse function is called to parse the request path `urlparse(self.path)`. A check is done on the request to see if it specifically for the specific endpoint. If this condition passes: `if self.path == '/subjects'` then the server process to handle with the request, in this case the backend function is called for example for /subjects, the fetchSubjects() function would be called.


fetchSubjects:
^^^^^^^^^^^^^^^

.. code-block:: python

   def fetchSubjects():
    conn = None
    cur = None
    subjects = []
    try:
        conn = connection_pool.getconn()
        cur = conn.cursor()
        
        cur.execute('SELECT subject_id, subject_name FROM subjects')
        
        rows = cur.fetchall()
        conn.commit()
        conn.close()
        
        return [{"subject_id": row[0], "subject_name": row[1]} for row in rows] # array of the subjects fetched from the database
    except Exception as error:
        print(error)
    finally: 
        if cur is not None:
            cur.close()
        if conn is not None:
            connection_pool.putconn(conn)
    
    return subjects


The fetchSubjects gets a connection from the connection pool (group of pre-established connections), creates a cursor to execute the SQL query, fetches the results via cur.fetchall(). a list comprehension is used where the rows are processed in a list of dictionaries and finally after the results have been fetched and placed in an array, the connection borrowed from the connection pool is returned for efficient database connection handling and to save resources etc. The fetchSubjects function returns a list of dictionaries. 

After the fetchSubjects is called, the server prepares a http response. The server sends a header of http status 200 via `self.send_response(200)` to show the request was successful. To prevent cross-origin-access-sharing error, a header is added to allow cross-origin requests from any domain. The `self.send_header('Content-type','application/json')` specifies that the response content type is JSON. The subjects array that was fetched from the database is serialised into JSON string via `self.wfile.write(json.dumps(subjects, indent = 2).encode('utf-8'))`. JSON is used which is sent to the frontend, for it easier to display the JSON (this can be done via localhost:8000/subjects) and it is easy to extract data from JSON and handle the data in the frontend etc. The response is sent to the client with the payload of the data being in JSON format which can display the subjects to the user on the frontend user interface.


