# Voice Interview System - Database Schema Design

## Overview

This repository contains the database schema design for a **Voice Interview System**. The schema is designed to store interview sessions, candidate information, transcripts, evaluations, interview state, and session logs in a structured and normalized format.

The goal of this design is to avoid messy data storage, reduce redundancy, and maintain clear relationships between different parts of the interview workflow.

## Objective

The objective of this task is to design a normalized relational database schema for a voice-based interview system that stores:

- Interview session details
- Candidate information
- Interview questions and candidate answers
- Evaluation scores and feedback
- Current interview state
- Session-level logs

## Deliverables

This repository includes:

| Deliverable | File |
| --- | --- |
| SQL Schema | `voice_interview_schema.sql` |
| ER Diagram | `er_diagram.md` |
| Documentation | `README.md` |

## Database Tables

The schema consists of the following tables:

| Table Name | Description |
| --- | --- |
| `candidates` | Stores candidate profile information |
| `interviews` | Stores interview session details such as domain, start time, and end time |
| `transcripts` | Stores interview questions, answers, and timestamps |
| `evaluations` | Stores score and feedback for each transcript response |
| `interview_states` | Stores the current state and question count of an interview |
| `interview_session_logs` | Stores session activity logs and system events |

## Entity Relationships

The database follows these relationships:

- A candidate can attend multiple interviews.
- An interview belongs to one candidate.
- An interview can contain multiple transcript records.
- Each transcript response can have one evaluation.
- Each interview has one current state record.
- Each interview can have multiple session log records.

## ER Diagram

The ER diagram is available in the following file:

```text
er_diagram.md
It represents the relationship between candidates, interviews, transcripts, evaluations, interview states, and session logs.

SQL Schema
The SQL schema is available in the following file:

voice_interview_schema.sql
This file contains all CREATE TABLE statements, primary keys, foreign keys, constraints, and table relationships.

How To Run The Schema
Prerequisites
Install DB Browser for SQLite:

https://sqlitebrowser.org/dl/
Steps
Open DB Browser for SQLite.
Create a new database file named:
voice_interview.db
Open the Execute SQL tab.
Copy the SQL code from:
voice_interview_schema.sql
Paste the code into the SQL editor.
Click the Run button.
Open the Database Structure tab.
Verify that all tables are created successfully.
Sample Test Data
You can use the following SQL statements to test the schema:

INSERT INTO candidates (candidate_id, full_name, email)
VALUES ('C001', 'Saurabh Patil', 'saurabh@example.com');

INSERT INTO interviews (interview_id, candidate_id, domain)
VALUES ('I001', 'C001', 'Python Developer');

INSERT INTO transcripts (interview_id, question_number, question, answer)
VALUES (
    'I001',
    1,
    'What is Python?',
    'Python is a high-level programming language.'
);

INSERT INTO evaluations (transcript_id, score, feedback)
VALUES (
    1,
    85,
    'Good answer with clear explanation.'
);

INSERT INTO interview_states (interview_id, current_state, question_count)
VALUES (
    'I001',
    'COMPLETED',
    1
);

INSERT INTO interview_session_logs (interview_id, event_type, details)
VALUES (
    'I001',
    'INTERVIEW_COMPLETED',
    'Candidate completed one interview question.'
);
Sample Query
The following query fetches candidate, interview, transcript, and evaluation details together:

SELECT
    c.full_name,
    i.domain,
    t.question,
    t.answer,
    e.score,
    e.feedback
FROM candidates c
JOIN interviews i
    ON c.candidate_id = i.candidate_id
JOIN transcripts t
    ON i.interview_id = t.interview_id
JOIN evaluations e
    ON t.transcript_id = e.transcript_id;
Normalization Approach
The schema is normalized to reduce redundancy and improve maintainability.

Candidate details are stored separately in the candidates table.
Interview metadata is stored in the interviews table.
Questions and answers are stored as individual transcript records.
Evaluation data is linked to transcript records instead of repeating answer details.
Interview state is separated from interview metadata because it changes during the interview.
Session logs are stored independently as append-only records.
Benefits
Reduces duplicate data
Improves data consistency
Supports multiple interviews per candidate
Stores multiple questions and answers per interview
Allows individual answer evaluation
Tracks current interview progress
Maintains session-level logs
Conclusion
This database schema provides a clean and scalable foundation for a Voice Interview System. It organizes interview-related data into normalized relational tables and supports transcript storage, evaluation tracking, state management, and session logging.
