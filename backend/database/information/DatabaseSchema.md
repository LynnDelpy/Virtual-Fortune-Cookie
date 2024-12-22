# Database Schema

## Users Table
Stores information about registered users.

| Column Name   | Data Type   | Constraints                  |
|---------------|-------------|------------------------------|
| `UserID`      | INT         | PRIMARY KEY, AUTO_INCREMENT  |
| `Username`    | VARCHAR(100)| UNIQUE, NOT NULL             |
| `Email`       | VARCHAR(100)| UNIQUE, NOT NULL             |
| `Password`    | BINARY(64)  | NOT NULL                     |
| `CreatedAt`   | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP    |


---

## Fortunes Table
Stores user-submitted fortunes.

| Column Name   | Data Type   | Constraints                  |
|---------------|-------------|------------------------------|
| `FortuneID`   | INT         | PRIMARY KEY, AUTO_INCREMENT  |
| `UserID`      | INT         | FOREIGN KEY REFERENCES Users(UserID) ON DELETE CASCADE |
| `Text`        | TEXT        | NOT NULL                     |
| `CreatedAt`   | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP    |

---

## MoodEntries Table
Tracks user mood entries.

| Column Name   | Data Type   | Constraints                  |
|---------------|-------------|------------------------------|
| `MoodID`      | INT         | PRIMARY KEY, AUTO_INCREMENT  |
| `UserID`      | INT         | FOREIGN KEY REFERENCES Users(UserID) ON DELETE CASCADE |
| `Mood`        | VARCHAR(50) | NOT NULL                     |
| `Notes`       | TEXT        | NULLABLE                     |
| `CreatedAt`   | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP    |

---

## UserLogs Table
Tracks user activity.

| Column Name   | Data Type   | Constraints                  |
|---------------|-------------|------------------------------|
| `LogID`       | INT         | PRIMARY KEY, AUTO_INCREMENT  |
| `UserID`      | INT         | FOREIGN KEY REFERENCES Users(UserID) ON DELETE CASCADE |
| `Action`      | VARCHAR(255)| NOT NULL                     |
| `Timestamp`   | TIMESTAMP   | DEFAULT CURRENT_TIMESTAMP    |

---

## Relationships
- **Users to Fortunes**: One-to-Many (one user can submit many fortunes).
- **Users to MoodEntries**: One-to-Many (one user can have many mood entries).
- **Users to UserLogs**: One-to-Many (one user can generate many activity logs).
