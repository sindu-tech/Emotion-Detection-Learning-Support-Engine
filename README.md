
## Step 1: Read the problem statement

Identify:

* What objects need to store data? → These are **Entities**.
* What information belongs to each object? → These are **Attributes**.
* How are the objects connected? → These are **Relationships**.
* Which attributes uniquely identify a record? → **Primary Keys (PK)**.
* Which attributes connect two entities? → **Foreign Keys (FK)**.

---

## Step 2: Identify the Entities

From the description:

### Entity 1: Users

Stores user account information.

### Entity 2: Emotion_Records

Stores emotion prediction sessions.

You now have:

```
Users
Emotion_Records
```

---

## Step 3: Identify the Attributes

### Users

```
email
name
password
role
login_count
created_at
```

### Emotion_Records

```
record_id
email
field
input_text
predicted_emotion
secondary_emotion
confidence_score
model_used
ai_response
response_type
emotion_scores
timestamp
csv_logged
```

---

## Step 4: Find the Primary Keys

Look for words like

* uniquely identifies
* unique identifier
* primary key

From your description:

```
Users
------
email (PK)

Emotion_Records
---------------
record_id (PK)
```

---

## Step 5: Find the Foreign Key

Look for words like

* references
* belongs to
* linked with

Here

```
Emotion_Records.email

references

Users.email
```

So

```
email (FK)
```

---

## Step 6: Identify the Relationship

The description says

> One user can generate multiple emotion analysis sessions.

Therefore

```
Users
   1
   |
   |
   |----<
        Many

Emotion_Records
```

This is called

```
One-to-Many (1:M)
```

---

## Step 7: Draw the ER Diagram

```
+---------------------------+
|          USERS            |
+---------------------------+
| PK email                  |
| name                      |
| password                  |
| role                      |
| login_count               |
| created_at                |
+---------------------------+
             |
             | 1
             |
             |
             | M
+---------------------------+
|     EMOTION_RECORDS       |
+---------------------------+
| PK record_id              |
| FK email                  |
| field                     |
| input_text                |
| predicted_emotion         |
| secondary_emotion         |
| confidence_score          |
| model_used                |
| ai_response               |
| response_type             |
| emotion_scores            |
| timestamp                 |
| csv_logged                |
+---------------------------+
```

---

# Step 8: Explain the Diagram

If asked in viva or exam:

> The ER diagram consists of two entities: Users and Emotion_Records. The Users entity stores account details such as email, password, role, and login information. The Emotion_Records entity stores emotion analysis results, AI responses, confidence scores, timestamps, and session details. The email attribute acts as the primary key in Users and as a foreign key in Emotion_Records, creating a one-to-many relationship. One user can have multiple emotion analysis records, while each record belongs to only one user.

---

# Step 9: Convert ER Diagram into Tables

```
USERS
------
email (PK)
name
password
role
login_count
created_at
```

```
EMOTION_RECORDS
---------------
record_id (PK)
email (FK)
field
input_text
predicted_emotion
secondary_emotion
confidence_score
model_used
ai_response
response_type
emotion_scores
timestamp
csv_logged
```

---

# Step 10: SQL Code (if asked)

```sql
CREATE TABLE Users (
    email VARCHAR(100) PRIMARY KEY,
    name VARCHAR(100),
    password VARCHAR(255),
    role VARCHAR(20),
    login_count INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE Emotion_Records (
    record_id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(100),
    field VARCHAR(100),
    input_text TEXT,
    predicted_emotion VARCHAR(50),
    secondary_emotion VARCHAR(50),
    confidence_score DECIMAL(5,2),
    model_used VARCHAR(20),
    ai_response TEXT,
    response_type VARCHAR(50),
    emotion_scores TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    csv_logged BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (email) REFERENCES Users(email)
);
```

---

# Step 11: If asked to write the database description

You can write:

> The database consists of two entities: Users and Emotion_Records. The Users entity stores user information including email, name, password, role, login count, and account creation date. The Emotion_Records entity stores details of each emotion analysis session, including predicted emotion, confidence score, AI-generated response, model used, emotion scores, and timestamp. The email attribute serves as the primary key in Users and as a foreign key in Emotion_Records, establishing a one-to-many relationship where one user can have multiple emotion analysis records. This design minimizes redundancy, maintains data integrity, and supports efficient storage, retrieval, analytics, and reporting.

### A simple checklist for similar tasks

1. Read the description.
2. Identify the **entities**.
3. List the **attributes** of each entity.
4. Mark the **primary key (PK)**.
5. Identify the **foreign key (FK)**.
6. Determine the **relationship** (1:1, 1:M, or M:N).
7. Draw the ER diagram.
8. Convert the ER diagram into relational tables.
9. Write the SQL `CREATE TABLE` statements if required.
10. Write a brief explanation of the database design and how it supports the application's functionality.
