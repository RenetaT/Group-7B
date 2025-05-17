Introduction:
==============

The learning app has a client-server architecture. The client sends a http request to the server where a backend function (representing a component which serves a particular purpose) fetches data from the backend. The server prepares a JSON response to send to the client. 


The components have been slightly changed during implementation. Particular components have been broken down into subcomponents while other components have been replaced or removed entirely due to feasability of implementing such components (for a feature) due to time constraints and difficulty of implementation. 


Client-Server system architecture:
-----------------------------------





Components In Use:
-------------

- Subject Manager: Uses the fetchSubjects() backend function to fetch subject_id and subject_name from the subjects table in the database in order to fetch subjects

- Topic Manager: Uses the fetchTopics() backend function to fetch topic_id and topic_name for matching subject_id from the topics table in the database in order to fetch topics for each subject

- Quiz Manager: Uses the generateQuizzes() backend function to fetch quiz_id and quiz_name  from the database in order to fetch quizzes for each topic.

- Question Manager: Uses the fetchQuestionAndAnswers() backendfunction to fetch questions and answers from the database for every quiz.

- Leaderboard: Uses fetchLeaderboard() backend function which fetches the total points a user has accumulated based on the amount of questions they have got correct. 

- Progress Tracker: Updates the total points and the level of a user in the database after every quiz completed. 

- Register Account: The register account component is responsible for inserting a new account the user has made into the database provided that user_name, user_last_name, user_email and user_password fields are all filled in. The createAccount() backend function is used which inserts a new record into the users table in the database which holds all the existing user accounts.

- Account Authenticator: The account authenticator verifies whether the user's credentials are correct or not and whether an account exists under a certain email address; it uses the loginUser() backend function
