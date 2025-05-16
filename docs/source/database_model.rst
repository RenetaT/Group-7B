Database Model
==============

This learning application's database schema is designed to organize and handle data related to users, subjects, topics, quizzes, questions, results, and rewards.

Entity-Relationship Diagram (ERD)
---------------------------------
link :
https://app.diagrams.net/#G1xh_K94tQJBBiNvQwiQV4ebWRCBj-GVoO#%7B%22pageId%22%3A%22eB-IHovhO6KBxCCwhGGL%22%7D


Table Descriptions
------------------

Users
~~~~~

- **user_id** (SERIAL, PRIMARY KEY): Unique identifier for each user. Auto-incrementing and primary key.
- **user_name** (VARCHAR(20)): User's first name, limited to 20 characters.
- **user_last_name** (VARCHAR(20)): User's last name, limited to 20 characters.
- **user_email** (VARCHAR(50), UNIQUE): Email address used for login and communication. Must be unique.
- **password** (VARCHAR(250)): Hashed password for authentication, stored securely with a salt.
- **join_date** (TIMESTAMP): The date and time when the user registered.

Subjects
~~~~~~~~

- **subject_id** (SERIAL, PRIMARY KEY): Unique identifier for each subject.
- **subject_name** (VARCHAR(20)): Name of the subject (e.g., "Mathematics", "English").
- **sub_description** (TEXT): A more detailed description of the subject.

Topics
~~~~~~

- **topic_id** (SERIAL, PRIMARY KEY): Unique identifier for each topic.
- **subject_id** (INT, NOT NULL, FOREIGN KEY): Links to the subject in the Subjects table.
- **topic_name** (VARCHAR(20), UNIQUE): Unique topic name, limited to 20 characters.
- **description** (TEXT): A more detailed description of the topic.

Quizzes
~~~~~~~

- **quiz_id** (SERIAL, PRIMARY KEY): Unique identifier for each quiz.
- **quiz_name** (VARCHAR(15), NOT NULL): Name of the quiz, cannot be null.
- **subject_id** (INT, NOT NULL, FOREIGN KEY): Links to a subject.
- **topic_id** (INT, NULL, FOREIGN KEY): Optional link to a topic.
- **quiz_title** (VARCHAR(20), NOT NULL, UNIQUE): Title of the quiz.
- **quiz_level** (ENUM ['Easy', 'Medium', 'Hard'], NOT NULL): Difficulty level.
- **quiz_type** (ENUM ['mock exam', 'quiz'], NOT NULL): Type of quiz.

Questions
~~~~~~~~~

- **question_id** (SERIAL, PRIMARY KEY): Unique identifier for each question.
- **question_text** (TEXT, NOT NULL): The content of the question.
- **points** (INT, NOT NULL): Points awarded for a correct answer.
- **question_level** (ENUM ['Easy', 'Medium', 'Hard'], NOT NULL): Difficulty level.

Answers
~~~~~~~

- **answer_id** (SERIAL, PRIMARY KEY): Unique identifier for each answer.
- **question_id** (INT, NOT NULL, FOREIGN KEY): Links to the related question.
- **answer_text** (TEXT): Answer option text.
- **is_correct** (BOOLEAN): Indicates whether the answer is correct.

User Attempts
~~~~~~~~~~~~~

- **attempt_id** (SERIAL, PRIMARY KEY): Unique identifier for each attempt.
- **user_id** (INT, NOT NULL): Links to the user who made the attempt.
- **question_id** (INT, NOT NULL): Links to the question being answered.
- **answer_id** (TEXT): Links to the selected answer.
- **is_correct** (BOOLEAN, NOT NULL): Indicates if the answer was correct.

Student Progress
~~~~~~~~~~~~~~~~

- **progress_id** (SERIAL, PRIMARY KEY): Unique identifier for each progress record.
- **user_id** (INT, NOT NULL): Links to the user.
- **total_points** (INT, DEFAULT 0): Total accumulated points.
- **user_level** (INT, DEFAULT 0): User's current level based on performance.

