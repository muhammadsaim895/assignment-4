# JSONPlaceholder API Testing

## 👨‍💻 Author

**Muhammad Saim Ovais**

### 10Pearls Shine Internship

This project was completed as part of my **10Pearls Shine Internship** to practice **API Testing, Postman, Automated API Tests, and Load Testing**.

---

# 📌 Project Overview

This project tests the **JSONPlaceholder REST API** using **Postman**.

The purpose of this project is to check whether the API works correctly when we:

* Get data
* Create new data
* Update existing data
* Delete data
* Send invalid or incomplete data
* Check response status codes
* Check response time
* Check response data
* Check response structure

The Postman collection contains automated tests for **GET, POST, PUT, and DELETE** requests.

---

# 🛠️ Tools Used

* **Postman** – API testing
* **JSONPlaceholder** – Test API
* **Postman Collection** – Contains API requests and automated tests
* **Postman Environment** – Stores the API base URL
* **Apache JMeter** – Load testing
* **GitHub** – Project documentation and version control

---

# 📂 Project Files

The project contains the following important files:

```text
JSONPlaceholder_API_Testing.postman_collection.json
JSONPlaceholder.postman_environment.json
JSONPlaceholder_LoadTest.jmx
screenshots.docx
README.md
```

### 1. Postman Collection

`JSONPlaceholder_API_Testing.postman_collection.json`

This file contains all the API requests and automated tests.

### 2. Postman Environment

`JSONPlaceholder.postman_environment.json`

This file contains the `baseUrl` variable.

The value of `baseUrl` is:

```text
https://jsonplaceholder.typicode.com
```

The collection uses this variable when sending requests.

### 3. JMeter File

`JSONPlaceholder_LoadTest.jmx`

This file is intended for load testing using Apache JMeter.

### 4. Screenshots

`screenshots.docx`

This contains screenshots related to the testing work.

---

# 🚀 How to Run the API Tests

## Step 1 – Install Postman

First, install **Postman** on your computer.

Open Postman after installation.

---

# Step 2 – Import the Collection

Open Postman.

On the left side, click:

**Import**

Then select:

```text
JSONPlaceholder_API_Testing.postman_collection.json
```

After importing, you should see:

```text
JSONPlaceholder API Testing - Assignment 4
```

The collection contains different folders for different HTTP methods.

---

# Step 3 – Import the Environment

Again, click:

**Import**

Select:

```text
JSONPlaceholder.postman_environment.json
```

The environment contains:

```text
baseUrl = https://jsonplaceholder.typicode.com
```

This means we do not need to write the complete website address in every request.

---

# Step 4 – Select the Environment

In Postman, look at the environment selector near the top-right area.

Select:

```text
JSONPlaceholder Environment
```

Make sure the environment is active.

The requests use:

```text
{{baseUrl}}
```

For example:

```text
{{baseUrl}}/posts
```

Postman will automatically replace `{{baseUrl}}` with:

```text
https://jsonplaceholder.typicode.com
```

---

# Step 5 – Open the Collection

Go to the **Collections** section in Postman.

Open:

```text
JSONPlaceholder API Testing - Assignment 4
```

You will see four main sections:

```text
1. GET Requests
2. POST Requests
3. PUT Requests
4. DELETE Requests
```

---

# 🟢 Step 6 – Run GET Tests

GET is used to **retrieve/read data**.

The collection contains three GET tests:

```text
GET All Posts
GET Single Post (id=1)
GET Non-Existent Post (id=99999)
```

The collection checks things such as status code, response time, response structure, and required fields.

---

## Test 1 – GET All Posts

Open:

```text
GET Requests
    ↓
GET All Posts
```

Click:

**Send**

The request is:

```text
GET {{baseUrl}}/posts
```

The automated tests check:

* Status code is `200`
* Response time is less than `1000ms`
* Response is an array
* Array contains `100` posts
* Posts contain required fields
* Content-Type is JSON

These checks are already included in the Postman collection.

### Expected Result

You should receive a successful response containing posts.

In the **Test Results** section, the tests should show:

```text
PASS
```

---

# Test 2 – GET Single Post

Open:

```text
GET Requests
    ↓
GET Single Post (id=1)
```

Click:

**Send**

The request is:

```text
GET {{baseUrl}}/posts/1
```

The automated tests check:

* Status code is `200`
* Response time is less than `800ms`
* Response has the correct structure
* ID equals `1`
* Title is not empty
* Body is not empty
* User ID is a number

These checks are defined in the collection.

### Expected Result

The request should successfully return post number `1`.

---

# Test 3 – GET Non-Existent Post

Open:

```text
GET Requests
    ↓
GET Non-Existent Post (id=99999)
```

Click:

**Send**

The request is:

```text
GET {{baseUrl}}/posts/99999
```

This is a **negative test**.

We are intentionally requesting a post that does not exist.

The expected status code is:

```text
404
```

The test also checks that the response time is below `800ms`.

### Expected Result

```text
Status: 404 Not Found
```

The test should still show **PASS** because `404` is the expected result for this negative test.

---

# 🟡 Step 7 – Run POST Tests

POST is used to **create new data**.

The collection contains:

```text
POST Create New Post
POST Create Post - Missing Body (Negative)
```

The POST request uses JSON data and the `Content-Type` header is set to `application/json`.

---

# Test 4 – Create New Post

Open:

```text
POST Requests
    ↓
POST Create New Post
```

Click:

**Send**

The request is:

```text
POST {{baseUrl}}/posts
```

The body contains:

```json
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
```

The automated tests check:

* Status code is `201 Created`
* Response time is less than `1000ms`
* Submitted fields are returned correctly
* A new ID is generated

The collection also saves the generated ID as:

```text
createdPostId
```

for possible later use.

### Expected Result

You should receive:

```text
201 Created
```

and the response should contain an ID.

---

# Test 5 – POST Missing Body

Open:

```text
POST Requests
    ↓
POST Create Post - Missing Body (Negative)
```

Click:

**Send**

The request intentionally sends incomplete data:

```json
{
    "title": "foo"
}
```

This is a **negative test**.

The collection expects:

```text
201 Created
```

and checks that the response still contains an ID.

### Important

A negative test does not always mean that the API must return an error.

It means that we are testing an unusual or invalid situation to see how the API behaves.

---

# 🔵 Step 8 – Run PUT Test

PUT is used to **update existing data**.

The collection contains:

```text
PUT Update Post (id=1)
```

Open:

```text
PUT Requests
    ↓
PUT Update Post (id=1)
```

Click:

**Send**

The request is:

```text
PUT {{baseUrl}}/posts/1
```

The body is:

```json
{
    "id": 1,
    "title": "updated title",
    "body": "updated body content",
    "userId": 1
}
```

The automated tests check:

* Status code is `200`
* Response time is less than `1000ms`
* Updated values are returned
* ID remains `1`

These tests are already included in the collection.

### Expected Result

The API should return:

```text
200 OK
```

and show the updated title and body.

---

# 🔴 Step 9 – Run DELETE Test

DELETE is used to **delete data**.

Open:

```text
DELETE Requests
    ↓
DELETE Post (id=1)
```

Click:

**Send**

The request is:

```text
DELETE {{baseUrl}}/posts/1
```

The automated tests check:

* Status code is `200`
* Response time is less than `800ms`
* Response body is an empty object

These checks are included in the collection.

### Expected Result

The request should return:

```text
200 OK
```

---

# 🧪 How to Run All Tests at Once

Instead of opening every request and clicking **Send** one by one, you can run the complete collection.

## Step 1

Open the **Collections** section.

Find:

```text
JSONPlaceholder API Testing - Assignment 4
```

## Step 2

Click the **three dots (...)** next to the collection.

## Step 3

Select:

```text
Run collection
```

This opens the **Collection Runner**.

## Step 4

Select the environment:

```text
JSONPlaceholder Environment
```

## Step 5

Make sure all required requests are selected.

## Step 6

Click:

```text
Run JSONPlaceholder API Testing - Assignment 4
```

Postman will automatically execute the requests.

---

# 📊 Understanding the Test Results

After the collection finishes, Postman shows the test results.

You will normally see:

```text
PASS
FAIL
```

### PASS

**PASS** means the actual result matched the expected result.

Example:

```text
Expected Status Code: 200
Actual Status Code: 200
Result: PASS
```

### FAIL

**FAIL** means the actual result did not match what the automated test expected.

Example:

```text
Expected Status Code: 200
Actual Status Code: 500
Result: FAIL
```

---

# 🔍 What Does the Automated Testing Check?

The Postman collection does more than simply check whether a request gets a response.

It checks several things.

## 1. Status Code

Example:

```text
200
201
404
```

This tells us whether the API request produced the expected HTTP result.

---

## 2. Response Time

The tests check that the API responds within a specific time.

For example:

```text
Response time < 1000ms
```

or:

```text
Response time < 800ms
```

## The exact limit depends on the individual test.

## 3. Response Structure

The tests check whether the response has the expected format.

For example, the GET All Posts test checks that the response is an array and contains 100 posts.

---

## 4. Required Fields

For a post, the tests check fields such as:

```text
userId
id
title
body
```

This helps make sure that the API is returning the expected information.

---

# 📋 Test Summary

| Test                       | Method | Purpose          | Expected Result |
| -------------------------- | ------ | ---------------- | --------------- |
| GET All Posts              | GET    | Get all posts    | 200             |
| GET Single Post            | GET    | Get post ID 1    | 200             |
| GET Non-Existent Post      | GET    | Negative test    | 404             |
| Create New Post            | POST   | Create a post    | 201             |
| Create Post - Missing Body | POST   | Negative test    | 201             |
| Update Post                | PUT    | Update post ID 1 | 200             |
| Delete Post                | DELETE | Delete post ID 1 | 200             |

---

# 🧑‍💻 Simple Testing Flow

The complete testing process is:

```text
Open Postman
      ↓
Import Collection
      ↓
Import Environment
      ↓
Select JSONPlaceholder Environment
      ↓
Open Collection
      ↓
Run Requests
      ↓
Automated Tests Execute
      ↓
Check PASS / FAIL
      ↓
Review Test Results
      ↓
Take Screenshots
      ↓
Document Results
```

---

# ⚡ Load Testing with JMeter

The project also includes a JMeter file:

```text
JSONPlaceholder_LoadTest.jmx
```

The purpose of JMeter is different from Postman.

### Postman

Postman is mainly used to check whether individual API requests work correctly.

### JMeter

JMeter is used to test how an API behaves when many requests are sent.

For example:

```text
Postman:
1 request → Check API

JMeter:
Many requests → Check API performance
```

---

# 📝 Important Note About the JMeter File

The provided `.jmx` file currently contains a **503 Backend.max_conn reached** response rather than a normal JMeter test plan. Therefore, it should be checked/re-created in JMeter before treating it as a runnable load-test plan.

Do not claim that the JMeter load test successfully ran unless the JMeter test plan opens correctly and produces actual results.

---

# 📸 Screenshots

Screenshots can be used as evidence that the tests were executed.

Useful screenshots include:

1. Postman collection
2. Selected environment
3. GET test result
4. POST test result
5. PUT test result
6. DELETE test result
7. Collection Runner results
8. PASS/FAIL summary
9. JMeter results, if successfully executed

The submitted screenshots document includes Postman workspace and JMeter-related result sections.

---

# 🐛 If a Test Fails

If a test shows **FAIL**, do not immediately assume the API is broken.

Check:

### 1. Is the environment selected?

Make sure:

```text
JSONPlaceholder Environment
```

is selected.

### 2. Is `baseUrl` correct?

It should be:

```text
https://jsonplaceholder.typicode.com
```

### 3. Check the request URL

For example:

```text
{{baseUrl}}/posts
```

### 4. Check the HTTP method

Make sure the method is correct:

```text
GET
POST
PUT
DELETE
```

### 5. Check the response

Look at:

```text
Status
Body
Headers
Response Time
Test Results
```

---

# 📚 What I Learned

Through this project, I practiced:

* API testing
* REST API concepts
* HTTP methods
* GET requests
* POST requests
* PUT requests
* DELETE requests
* Positive testing
* Negative testing
* Status code validation
* Response time validation
* Response structure validation
* Automated testing in Postman
* Environment variables
* Collection Runner
* Basic load testing concepts

---

# 🎯 Conclusion

This project demonstrates API testing of the **JSONPlaceholder REST API** using Postman.

The automated tests verify different parts of the API, including:

```text
Status Codes
Response Time
Response Structure
Response Fields
Content Type
Positive Scenarios
Negative Scenarios
```

The project was completed as part of the **10Pearls Shine Internship**.

---

## 👨‍💻 Student / Intern

**Name:** Muhammad Saim Ovais

**Program:** 10Pearls Shine Internship

**Project:** JSONPlaceholder API Testing

**Testing Tool:** Postman

**Load Testing Tool:** Apache JMeter
