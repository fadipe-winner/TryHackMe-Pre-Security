# Module 4: Data and Programming Fundamentals

## Overview

This module introduced me to how computers represent data and the basics of
programming and databases.

I learned about data encoding, Python, JavaScript, databases, and SQL.
Programming was one of the more challenging parts of the Pre Security path
for me, but working through simple examples helped me understand the basic
logic behind code.

---

## 1. Data Representation and Encoding

Computers represent information using binary (0s and 1s).

A single binary digit is called a **bit**, while 8 bits make a **byte**.

Computers also need a way to represent characters such as letters, numbers,
and symbols. Character encoding provides a standard way of mapping these
characters to values that computers can process.

Some important encoding concepts include:

- **ASCII** - represents letters, numbers, punctuation, and other characters
  using numerical values.
- **Unicode** - supports a much larger range of characters and languages.
- **UTF-8** - a widely used encoding for Unicode text.

I also learned that **encoding is not encryption**. Encoding changes how data
is represented, while encryption is designed to protect information from
unauthorized access.

---

## 2. Programming Fundamentals

Although programming languages can look different, they share many common
concepts.

Some of the basic concepts I learned were:

- Variables - store values that a program can use.
- Data types - describe the type of information being stored.
- Input - information provided to a program.
- Output - information produced by a program.
- Conditions - allow programs to make decisions.
- Loops - allow instructions to be repeated.
- Functions - reusable blocks of code.

Common data types include strings, integers, floats, and Boolean values.

---

## 3. Python Basics

Python was one of the programming languages introduced in this module.

A simple example of variables is:

```python
username = "Alex"
failed_logins = 3
```

Python uses `print()` to display information:

```python
print("Hello")
```

It can also receive input from the user:

```python
name = input("Enter your name: ")
```

One important thing I learned is that `input()` returns text. If I need a
number, I can convert it:

```python
guess = int(input("Take a guess: "))
```

---

## 4. Conditions and Loops

Conditional statements allow a program to make decisions.

Python uses `if`, `elif`, and `else`.

For example:

```python
secret = 10
guess = 15

if guess < secret:
    print("Too low")
elif guess > secret:
    print("Too high")
else:
    print("Correct")
```

Since `15` is greater than `10`, the program displays:

```text
Too high
```

This helped me understand programming as:

**Input → Process → Check Condition → Make Decision → Output**

I also learned that loops such as `for` and `while` allow code to run
repeatedly without writing the same instructions over and over.

---

## 5. JavaScript Basics

JavaScript is widely used to add behaviour and interactivity to websites.

One thing I noticed was that Python and JavaScript can express the same
programming logic using different syntax.

Python:

```python
if guess > secret:
    print("Too high")
```

JavaScript:

```javascript
if (guess > secret) {
    console.log("Too high");
}
```

Some basic differences I learned are:

| Python | JavaScript | Meaning |
|---|---|---|
| `print()` | `console.log()` | Display output |
| `x = 10` | `let x = 10;` | Store a value |
| `elif` | `else if` | Check another condition |
| `or` | `\|\|` | OR |
| `and` | `&&` | AND |

The syntax is different, but the underlying logic can be very similar.

---

## 6. Databases

A database is an organized collection of information that can be stored,
managed, and retrieved.

Relational databases organize information into **tables** containing rows
and columns.

For example:

| id | username | department |
|---:|---|---|
| 1 | Alex | IT |
| 2 | Sam | Finance |
| 3 | Jordan | IT |

A **row** represents a record, while a **column** represents a particular
type of information about that record.

---

## 7. SQL Basics

SQL stands for **Structured Query Language** and is used to interact with
relational databases.

Some of the SQL keywords I learned include:

- `SELECT` - chooses what data to return.
- `FROM` - specifies which table the data comes from.
- `WHERE` - filters records using a condition.
- `ORDER BY` - sorts the results.
- `AND` / `OR` - combine conditions.

For example:

```sql
SELECT username
FROM users
WHERE department = 'IT';
```

I can read this as:

> Show me the usernames from the users table where the department is IT.

---

## 8. Connection to Cybersecurity

These programming and database concepts provide useful foundations for
cybersecurity.

Python can be used for automation and processing data, JavaScript is
important for understanding web applications, and SQL helps me understand
how structured information can be queried.

For example, the basic idea of filtering records can also apply when
investigating security data:

```sql
SELECT username, source_ip
FROM login_events
WHERE status = 'failed';
```

This can be read as:

> Show me the username and source IP for failed login events.

I do not need to become a software developer for my current SOC/Blue Team
goal, but being able to understand simple code and programming logic will be
useful as I progress.

---

## Key Takeaway

This was one of the more challenging modules for me because programming was
still new to me.

My biggest takeaway was that I do not need to memorize every line of code.
Understanding the logic behind the code is more important at this stage.

I developed a foundational understanding of data representation, encoding,
Python, JavaScript, databases, and SQL. I plan to keep improving these skills
through practice as I move into more hands-on cybersecurity and SOC-focused
learning.
