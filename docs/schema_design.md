erDiagram
    USERS {
        String user_id PK
        varchar username
        varchar email
        varchar password
        timestamp created_at
        timestamp updated_at
    }

    TASKS {
        String task_id PK
        int user_id FK
        varchar title
        text description
        enum status
        timestamp created_at
        timestamp updated_at
    }

    USERS ||--o{ TASKS : "owns"