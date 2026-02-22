classDiagram
    class USERS {
        +UUID user_id PK
        +VARCHAR username UNIQUE
        +VARCHAR email UNIQUE
        +VARCHAR password (hashed)
    }

    class LISTS {
        +UUID list_id PK
        +VARCHAR name
        +UUID user_id FK -> USERS(user_id)
    }

    class TASKS {
        +UUID task_id PK
        +VARCHAR title
        +TEXT description
        +ENUM status ('pending','done')
        timestamp created_at
        timestamp updated_at
        +UUID list_id FK -> LISTS(list_id)
    }

    USERS "1" --> "many" LISTS : owns
    LISTS "1" --> "many" TASKS : contains