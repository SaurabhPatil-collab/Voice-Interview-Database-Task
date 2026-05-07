# Run Steps From Scratch

## Step 1: Install DB Browser for SQLite

Download DB Browser for SQLite from:
https://sqlitebrowser.org/dl/

Install it normally.

## Step 2: Create a New Database

1. Open DB Browser for SQLite.
2. Click New Database.
3. Save it as voice_interview.db inside this folder:
   E:\Voice-Interview-Database-Task
4. If a Create Table window opens, close it.

## Step 3: Paste SQL Code

1. Click Execute SQL.
2. Open voice_interview_schema.sql.
3. Copy all SQL code.
4. Paste it into Execute SQL.
5. Click the Run button.

## Step 4: Check Tables

Click Database Structure. You should see:

- candidates
- interviews
- transcripts
- evaluations
- interview_states
- interview_session_logs

## Step 5: Insert Test Data

Paste and run this in Execute SQL:

```sql
INSERT INTO candidates (candidate_id, full_name, email)
VALUES ('C001', 'Saurabh Patil', 'saurabh@example.com');

INSERT INTO interviews (interview_id, candidate_id, domain)
VALUES ('I001', 'C001', 'Python Developer');

INSERT INTO transcripts (interview_id, question_number, question, answer)
VALUES ('I001', 1, 'What is Python?', 'Python is a high-level programming language.');

INSERT INTO evaluations (transcript_id, score, feedback)
VALUES (1, 85, 'Good answer with clear explanation.');

INSERT INTO interview_states (interview_id, current_state, question_count)
VALUES ('I001', 'COMPLETED', 1);

INSERT INTO interview_session_logs (interview_id, event_type, details)
VALUES ('I001', 'INTERVIEW_COMPLETED', 'Candidate completed one question.');
```

## Step 6: View Data

Run:

```sql
SELECT * FROM candidates;
SELECT * FROM interviews;
SELECT * FROM transcripts;
SELECT * FROM evaluations;
```

## Step 7: View Combined Data

Run:

```sql
SELECT
    c.full_name,
    i.domain,
    t.question,
    t.answer,
    e.score,
    e.feedback
FROM candidates c
JOIN interviews i ON c.candidate_id = i.candidate_id
JOIN transcripts t ON i.interview_id = t.interview_id
JOIN evaluations e ON t.transcript_id = e.transcript_id;
```
