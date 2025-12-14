# MongoDB Basics & Use Case

This repository contains the practical tasks for **Week 12**, focusing on learning MongoDB fundamentals and applying them to a real-world scenario.

## 📌 Project Overview

The objective of this task was to understand MongoDB commands, perform CRUD operations, and build a small logic for a **Library Management System**.

### 📂 Contents

*   **`MongoDB_Basics_and_UseCase.md`**: A comprehensive guide and log of the specific commands (Insert, Read, Update, Delete) and queries used.
*   **`MongoDB-Submission.pdf`**: A compiled PDF containing screenshots of the terminal output for all executed tasks.

## 🚀 Tasks Covered

### 1. Database & Collection Setup
*   Created `studentDB` and `students` collection.
*   Learned to switch databases and manage data structures.

### 2. CRUD Operations
*   **Create**: Inserted single and multiple documents (Students with name, age, course).
*   **Read**: Fetched all data and filtered by specific criteria (e.g., "MERN Stack").
*   **Update**: Modified student status and added new fields (`isEnrolled`) to multiple documents.
*   **Delete**: Removed records based on conditions.

### 3. Advanced Query Operators
*   Practiced using operators for precise data retrieval:
    *   `$gt` (Greater Than) & `$lt` (Less Than)
    *   `$in` (Matches any in array)
    *   `$exists` (Checks for field existence)
    *   `$and` / `$or` (Logical operators)

### 4. Real-World Use Case: Library System
*   **Scenario**: Managing a library's book inventory (`libraryDB`).
*   **Features Implemented**:
    *   Stocking new books.
    *   Searching for available books in specific genres.
    *   Simulating a **Borrowing System** by decrementing `copiesAvailable` using `$inc`.

## 🛠️ Tech Stack
*   **Database**: MongoDB
*   **Shell**: Mongosh
*   **Environment**: PowerShell / Windows Terminal

## 📝 Submission
The detailed execution proofs are available in the **[MongoDB-Submission.pdf](./MongoDB-Submission.pdf)** file.
