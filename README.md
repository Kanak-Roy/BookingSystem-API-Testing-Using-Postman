# Booking System API Testing Using Postman

## 📌 Project Overview

This project demonstrates **API testing and test automation using Postman** for a Booking System API. It includes CRUD operations, authentication, dynamic test data generation, environment variables, response validation, and automated assertions using Postman's JavaScript-based test scripts.

The project is designed to practice API testing concepts and demonstrate practical QA skills through a reusable Postman collection.

## 🎯 Project Objectives

- Understand REST API testing using Postman.
- Validate HTTP status codes and response bodies.
- Test CRUD operations: Create, Read, Update, and Delete.
- Implement automated assertions using Postman test scripts.
- Generate dynamic test data using Postman variables.
- Manage environment variables for reusable test data.
- Extract and reuse booking IDs and authentication tokens.
- Validate response time, response size, and JSON response format.
- Verify booking data before and after update and deletion.

## 🛠️ Tools and Technologies

- **Postman** — API request execution and test automation
- **REST API** — HTTP methods and endpoint testing
- **JavaScript** — Automated test scripts
- **JSON** — Request and response data format
- **Postman Environment Variables** — Dynamic data management
- **Moment.js** — Date generation and formatting in pre-request scripts
- **Git and GitHub** — Version control and project documentation

## 📂 Project Structure

```text
BookingSystem-API-Testing/
│
├── BookingSystem.postman_collection.json
├── BookingSystemEnv.postman_environment.json
└── README.md
```

## 🔗 API Under Test

This collection is designed around the Booking System API, using the following endpoints:

| HTTP Method | Endpoint | Purpose |
|---|---|---|
| GET | `/booking` | Retrieve booking IDs |
| POST | `/booking` | Create a new booking |
| GET | `/booking/{id}` | Retrieve a specific booking |
| POST | `/auth` | Generate an authentication token |
| PUT | `/booking/{id}` | Update an existing booking |
| PATCH | `/booking/{id}` | Partially update booking details |
| DELETE | `/booking/{id}` | Delete a booking |
| GET | `/booking/{id}` | Verify booking deletion |

**Base URL:** Configure the `base_url` environment variable before executing the requests.

## 🧪 Test Scenarios Covered

### 1. Get Booking IDs
- Verify that the response status code is `200`.
- Validate response time and response size.
- Verify that the response body is in JSON format.
- Check whether a specific booking ID exists.
- Validate the expected booking ID in the response.

### 2. Create Booking
- Verify that the response status code is `201`.
- Validate response time and response size.
- Verify the generated booking details against the expected values.
- Validate the response JSON structure.
- Extract the generated `bookingid` and save it as the `id` environment variable.

### 3. Verify Created Booking
- Retrieve the newly created booking using its ID.
- Verify the status code and response format.
- Validate the booking details against the stored environment variables.

### 4. Authentication
- Send a POST request to `/auth`.
- Submit the username and password in JSON format.
- Verify successful token generation.
- Validate that the token exists, is a non-empty string, and is saved in the environment variable `token`.

### 5. Update Booking — PUT
- Update the booking using its ID.
- Send updated booking information in the request body.
- Include the authentication token in the Cookie header.
- Validate the response status code and booking fields.

### 6. Verify Booking After Update
- Retrieve the booking after the update.
- Validate that the updated values match the expected environment variables.

### 7. Partial Update Booking — PATCH
- Update only the booking dates.
- Generate new check-in and check-out dates dynamically.
- Verify that the updated booking dates match the expected values.

### 8. Delete Booking
- Delete the booking using its ID.
- Include the authentication token in the request headers.
- Verify the response status code and the expected success message.

### 9. Verify Booking After Deletion
- Send a GET request for the deleted booking.
- Verify that the response status code is `404`.
- Check the response for the expected not-found result.

## ⚙️ Automated Test Validations

The collection contains Postman test scripts using `pm.test()` and `pm.expect()`.

| Validation | Purpose |
|---|---|
| Status Code Validation | Verify expected HTTP status codes |
| Response Time Validation | Check whether response time is below 1000 ms |
| Response Size Validation | Check whether response size is below 300 bytes |
| JSON Validation | Verify that the response body is JSON |
| Response Data Validation | Compare actual and expected booking details |
| Booking ID Validation | Verify booking ID existence and correctness |
| Authentication Validation | Verify token existence and data type |
| CRUD Validation | Verify booking creation, retrieval, modification, and deletion |

*Note: Response-time and response-size thresholds are the assertions configured in this collection, not guaranteed performance requirements of the API.*

## 🔄 Dynamic Data and Environment Variables

The project uses environment variables to manage reusable test data.

| Variable | Purpose |
|---|---|
| `base_url` | Base URL of the API |
| `id` | ID of the created booking |
| `token` | Authentication token |
| `fName` | Dynamic first name |
| `lName` | Dynamic last name |
| `totalPrice` | Dynamic booking price |
| `dpaid` | Dynamic deposit-paid Boolean |
| `checkIn` | Check-in date |
| `checkOut` | Check-out date |
| `additionalneed` | Dynamic additional booking requirement |

### Dynamic Test Data

Pre-request scripts use Postman's dynamic variables to generate values such as:

- Random first and last names
- Random integer values
- Random Boolean values
- Random additional-needs text
- Dynamically generated check-in and check-out dates

The collection also uses Moment.js to format and calculate booking dates.

## 🔗 Request Chaining

The project demonstrates request chaining by extracting values from API responses and storing them in environment variables.

Examples:

- After creating a booking, the generated booking ID is stored in `id`.
- After authentication, the generated token is stored in `token`.
- Subsequent GET, PUT, PATCH, and DELETE requests reuse the booking ID.
- Update requests reuse the authentication token and generated booking data.

This approach reduces hardcoded values and makes the test collection more reusable.

## 🚀 How to Run the Project

### Prerequisites

- Install [Postman](https://www.postman.com/downloads/).
- Have access to a compatible Booking System API.
- Download or clone this GitHub repository.

### Step 1: Clone the Repository

```bash
git clone <https://github.com/Kanak-Roy/BookingSystem-API-Testing-Using-Postman>
cd BookingSystem-API-Testing
```

### Step 2: Import the Collection

1. Open Postman.
2. Click **Import**.
3. Select `BookingSystem.postman_collection.json`.
4. Confirm that the collection is imported successfully.

### Step 3: Import the Environment

1. Click **Import** in Postman.
2. Select `BookingSystemEnv.postman_environment.json`.
3. Open the imported environment.
4. Set `base_url` to the base URL of your API.
5. Save the environment.

### Step 4: Select the Environment

Select `BookingSystemEnv` from the environment selector in Postman.

### Step 5: Execute the Requests

Run the requests individually in the appropriate workflow:

1. Get Booking IDs
2. Create Booking
3. Get Booking Created ID Check
4. Create Token
5. Update Booking
6. Get Booking Created ID Check After Update
7. Partial Update Booking
8. Delete Booking
9. Get Booking Created ID Check After Delete

Run the authentication request before protected operations, and ensure that a valid booking ID exists before updating or deleting a booking.

**Important:** The collection uses a token cookie and an `Authorization: Basic` header on protected requests. Verify that the API accepts this configuration before running the tests.

### Step 6: Review Test Results

Open the **Test Results** section in Postman to review passed and failed assertions.

If an assertion fails, inspect the response status code, response body, environment variables, and Postman Console for troubleshooting.

## 📊 Expected Results

When the API is available, the environment is configured correctly, and the API behaves as expected, the collection is designed to validate:

- Successful retrieval of booking IDs.
- Successful booking creation and retrieval.
- Successful authentication and token extraction.
- Successful full and partial booking updates.
- Successful booking deletion.
- A not-found response when retrieving a deleted booking.
- Expected booking field values, response formats, and configured performance thresholds.

Actual results depend on the API implementation, test data, and execution environment.

## 📚 Skills Demonstrated

- Manual API Testing
- API Test Automation with Postman
- REST API Fundamentals
- HTTP Methods and Status Codes
- JSON Request and Response Validation
- Positive API Testing
- CRUD Operations Testing
- Authentication and Token Handling
- Pre-request Scripts
- Post-response Test Scripts
- Environment Variables
- Dynamic Test Data Generation
- Request Chaining
- JavaScript Assertions
- Git and GitHub

## 🔮 Future Improvements

- Add negative test cases for invalid inputs and missing fields.
- Add authentication failure and invalid-token scenarios.
- Improve response schema and data-type validation.
- Add boundary-value and input-validation tests.
- Add reusable collection-level test scripts.
- Execute the collection using Newman for command-line automation.
- Integrate automated execution into a CI/CD pipeline.
- Generate and publish HTML test reports.
- Improve cleanup and isolation of test data between runs.

## 👤 Author

**Kanak Roy Shanda**

- 🐙 GitHub: [Visit my GitHub](https://github.com/Kanak-Roy)
- 💼 LinkedIn: [Connect with me on LinkedIn](https://www.linkedin.com/in/kanak-roy-shanda-601961238/)
- 📧 Email: [kanakroyshanda@gmail.com](mailto:kanakroyshanda@gmail.com)
---

⭐ If you find this project useful, feel free to star the repository.
