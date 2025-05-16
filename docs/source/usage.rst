Usage
=====

This section explains how to set up your development environment and run the Learning App locally.

Setting Up the Development Environment
--------------------------------------

Follow these steps to prepare your machine:

1. **Install Flutter**  
   Follow the instructions on flutter.dev <https://flutter.dev/docs/get-started/install>_ to install the Flutter SDK.

2. **Install Python**  
   Make sure you have Python 3.x installed. You can download it from python.org <https://www.python.org/downloads/>_.

3. **Install PostgreSQL**  
   Download and install PostgreSQL from postgresql.org <https://www.postgresql.org/download/>_.  
   After installation, create a new database for the project and verify that your config.py contains the correct connection settings.

Running the Backend
-------------------

1. **Navigate to the backend directory**  
   
bash
   cd backend

2.**Install dependencies
pip install psycopg2-binary schedule

3.Configure the database connection
 Edit config.py and set your database host, name, user, and password.

4.Start the backend server

 python backend.py


Running the Flutter Application
--------------------------------
1. **Navigate to your Flutter project directory**  
   
   cd flutter_app   # or whatever your Flutter folder is named

2. **Get Flutter packages
   flutter pub get
3. **Run on an emulator or connected device
 flutter run


Code Structure
--------------
Below is a brief overview of the key source files and their roles:

backend.py
Handles HTTP requests, database interaction, and defines the REST API.

config.py
Contains the db_config object with your PostgreSQL connection settings.

home_page.dart
The main Flutter screen displaying the list of subjects.

leaderboard.dart
Implements the leaderboard view and logic.

main.dart
Application entry point; handles routing to login, registration, quiz, and mock-exam screens.

subject_page.dart
Screen for selecting a subject and browsing its topics.
