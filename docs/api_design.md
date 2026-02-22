# To-Do App API

A simple yet powerful RESTful API for a multi-user To-Do list application.

## Features
- User registration & JWT-based authentication
- Create, read, update (complete), and delete personal tasks
- Discover the most common tasks shared across all users

## Tech Stack (example)
- Backend: SpringBoot.
- Database: PostgreSQL / MongoDB
- Authentication: JWT (access tokens)

## Base URL
https://api.todoapp.example.com/v1
textor locally:
http://localhost:3000/api
text## Authentication
Protected endpoints require a JWT token in the header:
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
text## Endpoints

### 1. Register a new user  
**POST** `/users/register`

**Body**
```json
{
  "username": "bishoy123",
  "email": "bishoy@example.com",
  "password": "Cairo2026$strong"
}
```

Success (201)
```json
{
  "message": "User created successfully",
  "user": {
    "id": 7,
    "username": "bishoy123",
    "email": "bishoy@example.com",
    "created_at": "2026-02-22T18:45:12.000Z"
  }
}
```
### 2. Login
**POST** /auth/login
Body
```json
{
  "username": "bishoy123",
  "password": "Cairo2026$strong"
}
```
Success (200)
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 7,
    "username": "bishoy123",
    "email": "bishoy@example.com"
  }
}
```
### 3. Logout (client-side)
**POST** /auth/logout
Recommended: discard token on frontend.
Optional server-side: add token to blacklist.
Success (200)
```json
{ "message": "Logged out successfully" }
```
### 4. Create a task
**POST** /tasks
Auth: required
Body
```json
{
  "title": "Finish API documentation",
  "description": "Include all endpoints with examples"
}
```
Success (201)
```json
{
  "message": "Task created",
  "task": {
    "id": 56,
    "title": "Finish API documentation",
    "description": "Include all endpoints with examples",
    "completed": false,
    "created_at": "2026-02-22T19:12:45.000Z"
  }
}
```
### 5. List my tasks
**GET** /tasks
Auth: required
Query params (optional)
?completed=true
?page=1&limit=15
Success (200)
```json
{
  "tasks": [
    {
      "id": 56,
      "title": "Finish API documentation",
      "completed": false,
      ...
    },
    ...
  ],
  "pagination": {
    "page": 1,
    "limit": 15,
    "total": 23
  }
}
```
### 6. Delete a task
**DELETE** /tasks/:id
Auth: required (only owner)
Example: /tasks/56
Success (200)
```json
{ "message": "Task deleted successfully" }
```
### 7. Mark task as completed (or toggle)
**PUT** /tasks/:id/complete
Auth: required
Body (optional)
```json
{
  "completed": true     // or false
}
```
Omit body → sets to true
Success (200)
```json
{
  "message": "Task updated",
  "task": {
    "id": 56,
    "completed": true,
    "updated_at": "2026-02-22T19:20:10.000Z"
  }
}
```
### 8. Get most common tasks across all users
**GET** /tasks/common
Auth: required (can be made public if desired)
Query params (optional)
?min_users=3 (default: 2)
?limit=10 (default: 10)
Success (200)
```json
{
  "common_tasks": [
    {
      "title": "Drink water",
      "user_count": 47
    },
    {
      "title": "Morning walk",
      "user_count": 32
    },
    {
      "title": "Call family",
      "user_count": 19
    }
  ]
}
```
