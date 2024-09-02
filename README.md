# **ForesightFin Member Reports API Documentation**

Welcome to the **ForesightFin Member Reports API** documentation. This API provides endpoints for retrieving member-related financial data such as active loans, investments, loan details, and member profiles. This document will help you integrate and utilize these endpoints effectively.

---

## **Table of Contents**

1. **Base URL**
2. **Authentication**
3. **Endpoints**
    - 3.1 **Get Active Loans**
    - 3.2 **Get Investments**
    - 3.3 **Get Loan Details**
    - 3.4 **Get Member Profile**
4. **Error Handling**
5. **Testing**
6. **Examples**
7. **Contact & Support**

---

## **1. Base URL**

All API endpoints are accessible under the following base URL:

```
https://api.foresightfin.app/
```

---

## **2. Authentication**

*Note: The provided code snippets do not include authentication mechanisms. It is recommended to implement secure authentication (e.g., OAuth 2.0, API keys) to protect your endpoints.*

---

## **3. Endpoints**

### **3.1 Get Active Loans**

- **Description:** Retrieve a list of active loan IDs for a specific member and station.
- **URL:** `/active-loans`
- **Method:** `GET`
- **URL Parameters:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:** 
      ```json
      [
          12345,
          67890,
          23456
      ]
      ```
- **Error Responses:**
    - **Code:** `500 Internal Server Error`
    - **Content:** No content.
- **Example Request:**

```
GET https://api.foresightfin.app/active-loans?memberNumber=MEM123&stationId=STN456
```

- **Example Response:**

```json
[
    101,
    102,
    103
]
```

---

### **3.2 Get Investments**

- **Description:** Retrieve a list of investments for a specific member, station, and investment code.
- **URL:** `/investments`
- **Method:** `GET`
- **URL Parameters:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
    - `investmentCode` (integer, required): The code representing the type of investment.
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      [
          {
              "receiptDate": "2023-01-15",
              "debit": 1000.0,
              "credit": 500.0,
              "runningBalance": 500.0
          },
          {
              "receiptDate": "2023-02-15",
              "debit": 1000.0,
              "credit": 600.0,
              "runningBalance": 900.0
          }
      ]
      ```
- **Error Responses:**
    - **Code:** `500 Internal Server Error`
    - **Content:** No content.
- **Example Request:**

```
GET https://api.foresightfin.app/investments?memberNumber=MEM123&stationId=STN456&investmentCode=789
```

- **Example Response:**

```json
[
    {
        "receiptDate": "2023-03-10",
        "debit": 1500.0,
        "credit": 700.0,
        "runningBalance": 800.0
    }
]
```

---

### **3.3 Get Loan Details**

- **Description:** Retrieve detailed information about a specific loan for a member at a station.
- **URL:** `/loan-details`
- **Method:** `GET`
- **URL Parameters:**
    - `memberNumber` (string, required): The unique identifier for the member.
    - `stationId` (string, required): The identifier for the station.
    - `loanId` (integer, required): The unique identifier for the loan.
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      [
          {
              "loanId": 101,
              "receiptDate": "2023-01-15",
              "transIndicator": "P",
              "disbursedAmount": 5000.0,
              "requestedAmount": 4500.0,
              "paidAmount": 500.0,
              "principalPaid": 300.0,
              "interestPaid": 200.0,
              "principalAmount": 4500.0,
              "cumulativePrincipalPaid": 300.0,
              "cumulativeInterestPaid": 200.0,
              "outstandingPrincipal": 4200.0,
              "outstandingInterest": 1800.0,
              "interestAmount": 500.0
          }
      ]
      ```
- **Error Responses:**
    - **Code:** `404 Not Found`
    - **Content:** No content.
    - **Code:** `500 Internal Server Error`
    - **Content:** No content.
- **Example Request:**

```
GET https://api.foresightfin.app/loan-details?memberNumber=MEM123&stationId=STN456&loanId=101
```

- **Example Response:**

```json
[
    {
        "loanId": 101,
        "receiptDate": "2023-01-15",
        "transIndicator": "P",
        "disbursedAmount": 5000.0,
        "requestedAmount": 4500.0,
        "paidAmount": 500.0,
        "principalPaid": 300.0,
        "interestPaid": 200.0,
        "principalAmount": 4500.0,
        "cumulativePrincipalPaid": 300.0,
        "cumulativeInterestPaid": 200.0,
        "outstandingPrincipal": 4200.0,
        "outstandingInterest": 1800.0,
        "interestAmount": 500.0
    }
]
```

---

### **3.4 Get Member Profile**

- **Description:** Retrieve the profile information of a member based on their phone number.
- **URL:** `/member-profile`
- **Method:** `GET`
- **URL Parameters:**
    - `phoneNumber` (string, required): The phone number of the member in E.164 format (e.g., `+255657822049`).
- **Success Response:**
    - **Code:** `200 OK`
    - **Content:**
      ```json
      {
          "surname": "Doe",
          "otherName": "John",
          "memberNo": "MEM123",
          "stationId": "STN456",
          "saccoName": "Foresight SACCO"
      }
      ```
- **Error Responses:**
    - **Code:** `400 Bad Request`
    - **Content:** `null` (e.g., invalid phone number format)
    - **Code:** `404 Not Found`
    - **Content:** No content.
    - **Code:** `500 Internal Server Error`
    - **Content:** `null`.
- **Example Request:**

```
GET https://api.foresightfin.app/member-profile?phoneNumber=+255657822049
```

- **Example Response:**

```json
{
    "surname": "Smith",
    "otherName": "Anna",
    "memberNo": "MEM456",
    "stationId": "STN789",
    "saccoName": "Foresight SACCO"
}
```

---

## **4. Error Handling**

The API uses standard HTTP status codes to indicate the success or failure of an API request:

- **200 OK:** The request was successful, and the server returned the requested data.
- **400 Bad Request:** The request was invalid or cannot be otherwise served. This is often due to missing required parameters or invalid parameter formats.
- **404 Not Found:** The requested resource could not be found.
- **500 Internal Server Error:** An unexpected error occurred on the server.

*Note: The API currently does not provide detailed error messages in the response body. It is recommended to enhance error responses with meaningful messages for better debugging and user experience.*

---

## **5. Testing**

For testing purposes, you can use the following phone numbers to retrieve member profiles:

- **Phone Number 1:** `+255657822049`
- **Phone Number 2:** `+255762415356`

*Ensure that these phone numbers exist in the database to receive successful responses.*

### **Example Test Cases**

1. **Retrieve Active Loans**
    - **Request:**
        ```
        GET https://api.foresightfin.app/active-loans?memberNumber=MEM123&stationId=STN456
        ```
    - **Expected Response:**
        ```json
        [101, 102, 103]
        ```

2. **Retrieve Investments**
    - **Request:**
        ```
        GET https://api.foresightfin.app/investments?memberNumber=MEM123&stationId=STN456&investmentCode=789
        ```
    - **Expected Response:**
        ```json
       

 [
            {
                "receiptDate": "2023-03-10",
                "debit": 1500.0,
                "credit": 700.0,
                "runningBalance": 800.0
            }
        ]
        ```

3. **Retrieve Loan Details**
    - **Request:**
        ```
        GET https://api.foresightfin.app/loan-details?memberNumber=MEM123&stationId=STN456&loanId=101
        ```
    - **Expected Response:**
        ```json
        [
            {
                "loanId": 101,
                "receiptDate": "2023-01-15",
                "transIndicator": "P",
                "disbursedAmount": 5000.0,
                "requestedAmount": 4500.0,
                "paidAmount": 500.0,
                "principalPaid": 300.0,
                "interestPaid": 200.0,
                "principalAmount": 4500.0,
                "cumulativePrincipalPaid": 300.0,
                "cumulativeInterestPaid": 200.0,
                "outstandingPrincipal": 4200.0,
                "outstandingInterest": 1800.0,
                "interestAmount": 500.0
            }
        ]
        ```

4. **Retrieve Member Profile**
    - **Request:**
        ```
        GET https://api.foresightfin.app/member-profile?phoneNumber=+255657822049
        ```
    - **Expected Response:**
        ```json
        {
            "surname": "Smith",
            "otherName": "Anna",
            "memberNo": "MEM456",
            "stationId": "STN789",
            "saccoName": "Foresight SACCO"
        }
        ```

