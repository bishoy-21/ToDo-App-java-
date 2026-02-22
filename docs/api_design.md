# 📌 To-Do List API Documentation

This API powers a collaborative to-do list application.  
It supports user authentication, list management, and task management.

---
## 🔐 Authentication

### POST `/auth/signup`
- **Request**
  ```json
  {
    "username": "bishoy",
    "email": "bishoy@example.com",
    "password": "securePassword123"
  }
  ```
- **Success Response (201 Created)**
  ```json
  {
    "data": {
      "message": "User created successfully",
      "user_id": "uuid"
    }
  }
  ```
- **Error Response (400 Bad Request)**
  ```json
  {
    "data": {
      "message": "Email already exists"
    }
  }
  ```

### POST `/auth/login`
- **Request**
  ```json
  {
    "email": "bishoy@example.com",
    "password": "securePassword123"
  }
  ```
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Login successful",
      "token": "jwt-token-here"
    }
  }
  ```
- **Error Response (401 Unauthorized)**
  ```json
  {
    "data": {
      "message": "Invalid credentials"
    }
  }
  ```

---

## 📂 List Management

### POST `/lists`
- **Request**
  ```json
  {
    "name": "Work Tasks"
  }
  ```
- **Success Response (201 Created)**
  ```json
  {
    "data": {
      "message": "List created successfully",
      "list_id": "uuid"
    }
  }
  ```

### GET `/lists`
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Lists retrieved successfully",
      "lists": [
        { "list_id": "uuid", "name": "Work Tasks" },
        { "list_id": "uuid", "name": "Personal" }
      ]
    }
  }
  ```

### PUT `/lists/{id}`
- **Request**
  ```json
  {
    "name": "Updated List Name"
  }
  ```
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "List updated successfully",
      "list_id": "uuid"
    }
  }
  ```
- **Error Response (404 Not Found)**
  ```json
  {
    "data": {
      "message": "List not found"
    }
  }
  ```

### DELETE `/lists/{id}`
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "List deleted successfully",
      "list_id": "uuid"
    }
  }
  ```
- **Error Response (404 Not Found)**
  ```json
  {
    "data": {
      "message": "List not found"
    }
  }
  ```

---

## ✅ Task Management (inside a list)

### POST `/lists/{list_id}/tasks`
- **Request**
  ```json
  {
    "title": "Finish API design",
    "description": "Write docs",
    "status": "pending"
  }
  ```
- **Success Response (201 Created)**
  ```json
  {
    "data": {
      "message": "Task created successfully",
      "task_id": "uuid"
    }
  }
  ```

### GET `/lists/{list_id}/tasks`
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Tasks retrieved successfully",
      "tasks": [
        { "task_id": "uuid", "title": "Finish API design", "status": "pending" },
        { "task_id": "uuid", "title": "Prepare project report", "status": "done" }
      ]
    }
  }
  ```

### GET `/lists/{list_id}/tasks/{task_id}`
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Task retrieved successfully",
      "task": {
        "task_id": "uuid",
        "title": "Finish API design",
        "description": "Write docs",
        "status": "pending"
      }
    }
  }
  ```
- **Error Response (404 Not Found)**
  ```json
  {
    "data": {
      "message": "Task not found"
    }
  }
  ```

### PUT `/lists/{list_id}/tasks/{task_id}`
- **Request**
  ```json
  {
    "title": "Update API design",
    "status": "done"
  }
  ```
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Task updated successfully",
      "task_id": "uuid"
    }
  }
  ```
- **Error Response (404 Not Found)**
  ```json
  {
    "data": {
      "message": "Task not found"
    }
  }
  ```

### DELETE `/lists/{list_id}/tasks/{task_id}`
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Task deleted successfully",
      "task_id": "uuid"
    }
  }
  ```
- **Error Response (404 Not Found)**
  ```json
  {
    "data": {
      "message": "Task not found"
    }
  }
  ```

### PATCH `/lists/{list_id}/tasks/{task_id}/finish`
- **Success Response (200 OK)**
  ```json
  {
    "data": {
      "message": "Task marked as done",
      "task_id": "uuid",
      "status": "done"
    }
  }
  ```
- **Error Response (404 Not Found)**
  ```json
  {
    "data": {
      "message": "Task not found"
    }
  }
  ```

