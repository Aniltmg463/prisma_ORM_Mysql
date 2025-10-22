# 1. CREATE a new todo
curl -X POST http://localhost:3000/todos ^
  -H "Content-Type: application/json" ^
  -d "
{
  "title": "My First Todo",
  "description": "Testing SQLite connection"
}"

# 2. GET all todos
curl -X GET http://localhost:3000/todos

# 3. GET a specific todo (replace 1 with actual ID)
curl -X GET http://localhost:3000/todos/1

# 4. UPDATE a todo (replace 1 with actual ID)
curl -X PUT http://localhost:3000/todos/1 ^
  -H "Content-Type: application/json" ^
  -d "{\"title\":\"Learn NestJS - Updated\",\"description\":\"Build a todo app with SQLite\",\"completed\":true}"

# 5. DELETE a todo (replace 1 with actual ID)
curl -X DELETE http://localhost:3000/todos/1

# NestJS Todo App with SQLite & Prisma

A simple Todo application built with NestJS, Prisma ORM, and SQLite database.

## 📋 Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [CRUD Operations with Postman](#crud-operations-with-postman)
- [Database Schema](#database-schema)
- [Project Structure](#project-structure)

## ✨ Features

- RESTful API for Todo management
- SQLite database with Prisma ORM
- Full CRUD operations (Create, Read, Update, Delete)
- Input validation
- Automatic timestamps (createdAt, updatedAt)

## 📋 Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- Postman (for API testing)

## 🚀 Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd todo-app-mysql-prisma
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up environment variables:**
   Create a `.env` file in the root directory:
   ```env
   DATABASE_URL="file:./prisma/db/dev.sqlite"
   ```

4. **Generate Prisma client:**
   ```bash
   npx prisma generate
   ```

5. **Create the database:**
   ```bash
   npx prisma db push
   ```

## 🏃‍♂️ Running the Application

1. **Start the development server:**
   ```bash
   npm run start:dev
   ```

2. **The application will be running at:**
   ```
   http://localhost:3000
   ```

## 🛠 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/todos` | Get all todos |
| GET | `/todos/:id` | Get a specific todo by ID |
| POST | `/todos` | Create a new todo |
| PUT | `/todos/:id` | Update a todo |
| DELETE | `/todos/:id` | Delete a todo |

## 🔄 CRUD Operations with Postman

### Base URL
```
http://localhost:3000
```

### 1. 📝 **CREATE a New Todo**

**Method:** `POST`  
**URL:** `http://localhost:3000/todos`  
**Headers:**
```
Content-Type: application/json
```
**Body (raw JSON):**
```json
{
  "title": "Complete NestJS project",
  "description": "Finish building the todo app with SQLite database"
}
```

**Expected Response (201 Created):**
```json
{
  "id": 1,
  "title": "Complete NestJS project",
  "description": "Finish building the todo app with SQLite database",
  "completed": false,
  "createdAt": "2025-10-22T14:30:00.000Z",
  "updatedAt": "2025-10-22T14:30:00.000Z"
}
```

### 2. 📖 **READ All Todos**

**Method:** `GET`  
**URL:** `http://localhost:3000/todos`  
**Headers:** None required

**Expected Response (200 OK):**
```json
[
  {
    "id": 1,
    "title": "Complete NestJS project",
    "description": "Finish building the todo app with SQLite database",
    "completed": false,
    "createdAt": "2025-10-22T14:30:00.000Z",
    "updatedAt": "2025-10-22T14:30:00.000Z"
  }
]
```

### 3. 📖 **READ a Specific Todo**

**Method:** `GET`  
**URL:** `http://localhost:3000/todos/1`  
**Headers:** None required

**Expected Response (200 OK):**
```json
{
  "id": 1,
  "title": "Complete NestJS project",
  "description": "Finish building the todo app with SQLite database",
  "completed": false,
  "createdAt": "2025-10-22T14:30:00.000Z",
  "updatedAt": "2025-10-22T14:30:00.000Z"
}
```

### 4. ✏️ **UPDATE a Todo**

**Method:** `PUT`  
**URL:** `http://localhost:3000/todos/1`  
**Headers:**
```
Content-Type: application/json
```
**Body (raw JSON):**
```json
{
  "title": "Complete NestJS project - Updated",
  "description": "Finish building the todo app with SQLite database and add tests",
  "completed": true
}
```

**Expected Response (200 OK):**
```json
{
  "id": 1,
  "title": "Complete NestJS project - Updated",
  "description": "Finish building the todo app with SQLite database and add tests",
  "completed": true,
  "createdAt": "2025-10-22T14:30:00.000Z",
  "updatedAt": "2025-10-22T14:35:00.000Z"
}
```

### 5. 🗑️ **DELETE a Todo**

**Method:** `DELETE`  
**URL:** `http://localhost:3000/todos/1`  
**Headers:** None required

**Expected Response (200 OK):**
```json
{
  "message": "Todo deleted successfully",
  "id": 1
}
```

## 🧪 Testing Sequence with Postman

Follow this sequence to test all CRUD operations:

1. **Create multiple todos** (POST) - Create 3-4 different todos
2. **Get all todos** (GET) - Verify all todos are created
3. **Get specific todo** (GET) - Test fetching by ID
4. **Update a todo** (PUT) - Mark one as completed
5. **Get all todos again** (GET) - Verify the update
6. **Delete a todo** (DELETE) - Remove one todo
7. **Get all todos final** (GET) - Verify deletion

## 🗄️ Database Schema

```prisma
model Todo {
  id          Int      @id @default(autoincrement())
  title       String
  description String?
  completed   Boolean  @default(false)
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}
```

## 📁 Project Structure

```
├── prisma/
│   ├── db/
│   │   └── dev.sqlite          # SQLite database file
│   ├── migrations/             # Database migrations
│   └── schema.prisma          # Prisma schema
├── src/
│   ├── prisma/
│   │   ├── prisma.module.ts   # Prisma module
│   │   └── prisma.service.ts  # Prisma service
│   ├── todo/
│   │   ├── todo.controller.ts # Todo routes
│   │   ├── todo.module.ts     # Todo module
│   │   └── todo.service.ts    # Todo business logic
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   └── main.ts
├── .env                       # Environment variables
├── package.json
└── README.md
```

## 🚨 Error Handling

The API returns appropriate HTTP status codes:

- `200` - Success
- `201` - Created successfully
- `400` - Bad Request (validation error)
- `404` - Todo not found
- `500` - Internal server error

## 💡 Tips for Postman Testing

1. **Create a Postman Collection** for all Todo endpoints
2. **Use Environment Variables** in Postman for the base URL
3. **Save example responses** for documentation
4. **Use Tests tab** in Postman to add automated assertions
5. **Chain requests** using the todo ID from previous responses

## 🔧 Troubleshooting

### Common Issues:

1. **500 Internal Server Error**
   - Check if the database file exists in `prisma/db/dev.sqlite`
   - Run `npx prisma db push` to create/sync the database

2. **Environment variable not found**
   - Ensure `.env` file exists with correct `DATABASE_URL`
   - Restart the application after changing `.env`

3. **Prisma Client Error**
   - Run `npx prisma generate` to regenerate the client
   - Check if the schema.prisma file is valid

### Commands for Reset:

```bash
# Reset database
rm prisma/db/dev.sqlite
npx prisma db push

# Regenerate Prisma client
npx prisma generate

# Restart application
npm run start:dev
```

## 📝 License

This project is licensed under the MIT License.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

---
for .env setup
# DATABASE_URL="file:./prisma/db/dev.sqlite"
DATABASE_URL="file:./db/dev.sqlite"

# Environment variables declared in this file are automatically made available to Prisma.
# See the documentation for more detail: https://pris.ly/d/prisma-schema#accessing-environment-variables-from-the-schema

# Prisma supports the native connection string format for PostgreSQL, MySQL, SQLite, SQL Server, MongoDB and CockroachDB.
# See the documentation for all the connection string options: https://pris.ly/d/connection-strings

# MySQL connection strings (commented out)
# DATABASE_URL="mysql://root:@localhost:3306/bidding_app"
# DATABASE_URL="mysql://root:password@localhost:3308/bidding_app" 


**Happy Coding! 🚀**
