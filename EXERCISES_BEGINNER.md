# PostgreSQL Command-Line Exercise File

## 🟢 Easy Level

**Scenario:**
You are managing a small database of books in a library.

**Objectives:**

1. **Create a table** named `book` with the following columns:
   - `id` (integer, primary key, auto-increment)
   - `title` (text)
   - `author` (text)
   - `published_year` (integer)
2. **Insert** the following data into `book`:
   - ("The Hobbit", "J.R.R. Tolkien", 1937)
   - ("1984", "George Orwell", 1949)
   - ("The Catcher in the Rye", "J.D. Salinger", 1951)
3. **Display all books** in the table.
4. **Select** only the titles of books published before 1950.

## 🟠 Intermediate Level

**Scenario:**

You now want to track library members and their borrowed books.

**Objectives:**

1. **Create a table** called members with:
   - `id` (integer, primary key, auto-increment)
   - `name` (text)
   - `join_date` (date)
2. **Insert** the following members:
   - ("Alice", "2023-01-10")
   - ("Bob", "2023-02-15")
3. **Create a table** called `borrow` with:
   - `id` (integer, primary key, auto-increment)
   - `member_id` (integer, references members(id))
   - `book_id` (integer, references books(id))
   - `borrowed_on` (date)
4. **Insert** the following borrow records:
   - Alice borrowed "The Hobbit" on 2023-03-01
   - Bob borrowed "1984" on 2023-03-05
5. **List all borrows** with the member’s name, book title, and borrowed date.

## 🔴 Advanced Level

**Scenario:**

You want to analyze and update library data for reporting.

**Objectives:**

1. **Add a column** to the `books` table called `available` (boolean, default true).
2. **Update** the `available` column to `false` for any book that is currently borrowed (i.e., appears in the `borrow` table).
3. **Display** all books with their availability status.
4. **Delete** the borrow record for Alice, and set the book she borrowed as available again.
5. **Write a query** to find all members who have never borrowed a book.
6. _(Bonus)_ **Display** the total number of books borrowed by each member, including those with zero.
