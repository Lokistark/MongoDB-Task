# MongoDB Basics, Key Concepts, and Real-World Use Case

## 1. Database & Collection Setup

In MongoDB, databases hold collections of documents. You don't always need to explicitly create them; they are created when you first store data.

**Commands:**

```javascript
// Switch to a new database (or create it if it doesn't exist)
use studentDB

// Explicitly create a collection (optional, usually created on insert)
db.createCollection("students")
```

---

## 2. Insert Operations

Adding data to your collection.

**Insert One Document:**

```javascript
db.students.insertOne({
    name: "John Doe",
    age: 20,
    course: "Web Development",
    status: "active"
})
```

**Insert Multiple Documents:**

```javascript
db.students.insertMany([
    { name: "Alice Smith", age: 22, course: "MERN Stack", status: "active" },
    { name: "Bob Johnson", age: 19, course: "Data Science", status: "inactive" },
    { name: "Charlie Brown", age: 23, course: "MERN Stack", status: "completed" },
    { name: "David Lee", age: 21, course: "Cyber Security", status: "active" }
])
```

---

## 3. Read Operations

Retrieving data from the collection.

**Fetch All Documents:**

```javascript
db.students.find()
```

**Fetch with Filters (e.g., MERN Stack students):**

```javascript
db.students.find({ course: "MERN Stack" })
```

---

## 4. Update Operations

Modifying existing documents.

**Update Single Document via Condition:**
*Change the status of the student named 'John Doe' to 'completed'.*

```javascript
db.students.updateOne(
    { name: "John Doe" },
    { $set: { status: "completed" } }
)
```

**Update Multiple Documents:**
*Update all 'active' students to have a new field 'isEnrolled' set to true.*

```javascript
db.students.updateMany(
    { status: "active" },
    { $set: { isEnrolled: true } }
)
```

---

## 5. Delete Operations

Removing documents.

**Delete One Document:**
*Delete a student named 'Bob Johnson'.*

```javascript
db.students.deleteOne({ name: "Bob Johnson" })
```

**Delete All Documents:**

```javascript
db.students.deleteMany({}) // CAUTION: Deletes everything in the collection
```

---

## 6. Query Operators

Refining searches with operators.

*   **$gt / $lt** (Greater Than / Less Than): Find students older than 20.
    ```javascript
    db.students.find({ age: { $gt: 20 } })
    ```

*   **$in** (In Array): Find students in either "MERN Stack" or "Data Science".
    ```javascript
    db.students.find({ course: { $in: ["MERN Stack", "Data Science"] } })
    ```

*   **$and** (Logical AND): Find active students aged 21. (Implicit in default query, but explicit here).
    ```javascript
    db.students.find({ $and: [{ status: "active" }, { age: 21 }] })
    ```

*   **$or** (Logical OR): Find students who are either completed OR under 20.
    ```javascript
    db.students.find({ $or: [{ status: "completed" }, { age: { $lt: 20 } }] })
    ```

*   **$exists** (Field Existence): Find students who have the 'isEnrolled' field.
    ```javascript
    db.students.find({ isEnrolled: { $exists: true } })
    ```

---

## 7. Real-World Use Case: Library Management System

**Scenario:** A library wants to manage its book inventory.
**Database:** `libraryDB`
**Collection:** `books`

### Key Fields:
*   `title` (String)
*   `author` (String)
*   `genre` (Array of Strings)
*   `publishedYear` (Number)
*   `copiesAvailable` (Number)

### Operations Implementation:

**1. Insert Books (Initial Inventory):**
```javascript
use libraryDB

db.books.insertMany([
    { title: "The Great Gatsby", author: "F. Scott Fitzgerald", genre: ["Classic", "Fiction"], publishedYear: 1925, copiesAvailable: 5 },
    { title: "To Kill a Mockingbird", author: "Harper Lee", genre: ["Classic", "Drama"], publishedYear: 1960, copiesAvailable: 2 },
    { title: "1984", author: "George Orwell", genre: ["Dystopian", "Sci-Fi"], publishedYear: 1949, copiesAvailable: 0 },
    { title: "Clean Code", author: "Robert C. Martin", genre: ["Tech", "Education"], publishedYear: 2008, copiesAvailable: 10 }
])
```

**2. Search (Find 'Available' Classics):**
*Find books that are in the "Classic" genre AND have copies available (> 0).*
```javascript
db.books.find({
    genre: "Classic",
    copiesAvailable: { $gt: 0 }
})
```

**3. Update (Book Return & Restock):**
*A user returned "1984", so we increase the available copies by 1.*
```javascript
db.books.updateOne(
    { title: "1984" },
    { $inc: { copiesAvailable: 1 } }
)
```

**4. Update (Book Borrowing):**
*Borrow "Clean Code", decrease copies by 1.*
```javascript
db.books.updateOne(
    { title: "Clean Code", copiesAvailable: { $gt: 0 } }, // Ensure copies exist before borrowing
    { $inc: { copiesAvailable: -1 } }
)
```

**5. Delete (Outdated Edition):**
*Remove books published before 1900.*
```javascript
db.books.deleteMany({ publishedYear: { $lt: 1900 } })
```
