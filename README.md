# API Testing – Assignment 4

**10Pearls Shine Internship**
**Submitted by:** Muhammad Saim Ovais

---

## What This Assignment Is About

Two tools were used:

- **Postman** – to test the API requests (GET, POST, PUT, DELETE) and check if the responses are correct.
- **Apache JMeter** – to test how the API performs when many users send requests at the same time.

---

## Files in This Repository

| File | What It Is |
|---|---|
| `SaimOvais_Assignment4_APICollection.json` | Postman collection with all the API requests and tests |
| `SaimOvais_Assignment4_Environment.json` | Postman environment with the base URL |
| `SaimOvais_Assignment4_LoadTest.jmx` | JMeter test plan for the load test |
| `.png` screenshot files | Screenshots showing the tests were run and passed |
| `README.md` | This file |

---

## Part 1: Postman Testing

### What Was Tested

**GET Requests**
- Get all posts
- Get a single post (id = 1)
- Get a post that does not exist (id = 99999) — to check the error response

**POST Request**
- Create a new post

**PUT Request**
- Update an existing post

**DELETE Request**
- Delete a post

### What Each Test Checks

Every request has automated tests written in Postman that check:
1. **Status Code** – Is the response code correct (200, 201, 404, etc.)?
2. **Response Time** – Did the API respond fast enough?
3. **Response Structure** – Is the response in the correct format (object or array)?
4. **Field Values** – Do the fields like `id`, `title`, `body`, and `userId` have the correct values?

### How to Run It Yourself

1. Install [Postman](https://www.postman.com/downloads/).
2. Open Postman and press `Ctrl + O` to open the Import window.
3. Import both files:
   - `SaimOvais_Assignment4_APICollection.json`
   - `SaimOvais_Assignment4_Environment.json`
4. In the top-right corner, select **Assignment 4 Environment** from the dropdown (it must not say "No environment").
5. Open any request and click **Send**.
6. Click on the **Test Results** tab to see which tests passed.

---

## Part 2: JMeter Load Testing

### Test Setup

| Setting | Value |
|---|---|
| Number of Users (Threads) | 10 |
| Ramp-Up Period | 5 seconds |
| Loop Count | 5 |
| Endpoints Tested | `GET /posts/1` and `GET /posts` |

This means the test sent **100 total requests** (10 users × 5 loops × 2 endpoints) to the API.

### Results

| Metric | GET /posts/1 | GET /posts |
|---|---|---|
| Requests Sent | 50 | 50 |
| Average Response Time | 253 ms | 240 ms |
| Error Rate | 0.00% | 0.00% |
| Throughput | 5.9 requests/sec | 6.3 requests/sec |

**Summary:** All 100 requests were successful with a 0% error rate. The average response time stayed under 300 milliseconds, which is good for a public API under this level of load.

### How to Run It Yourself

1. Install Java (JDK 8 or higher) from [adoptium.net](https://adoptium.net/) if not already installed.
2. Download [Apache JMeter](https://jmeter.apache.org/download_jmeter.cgi) (the `.zip` binary file).
3. Extract the zip file.
4. Open the `bin` folder and double-click **`jmeter.bat`** (the Windows Batch File, not the shell script or config file).
5. In JMeter, go to **File → Open** and select `SaimOvais_Assignment4_LoadTest.jmx`.
6. Click the green **Start** button (▶) at the top to run the test.
7. Click on **View Results Tree** in the left panel to see individual results.
8. Click on **Summary Report** in the left panel to see the overall performance numbers.

---

## What I Learned

- How to send different types of API requests (GET, POST, PUT, DELETE) using Postman.
- How to write simple automated tests in Postman using JavaScript (`pm.test`).
- How HTTP status codes work (200 OK, 201 Created, 404 Not Found).
- How to organize API requests into folders inside a Postman Collection.
- How to set up a basic load test in JMeter using a Thread Group and HTTP Request Sampler.
- How to read performance results like response time, throughput, and error rate.
