# Restful Booker API Testing Portfolio

API test collection for [Restful Booker](https://restful-booker.herokuapp.com) built with Postman.  
Created as part of a QA portfolio to demonstrate manual API testing skills.

## Tools

- Postman — API testing & collections
- JavaScript — pm.test assertions
- Git & GitHub — version control & repository management

## Collection Structure

| Folder          | Requests                                                                                                                             |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Auth            | Health Check, Get Token                                                                                                              |
| Booking - Read  | Get All Bookings, Get Booking by ID                                                                                                  |
| Booking - Write | Create Booking, Update Booking, Delete Booking                                                                                       |
| Edge Cases      | Invalid ID, Missing Fields, No Token, String ID, Invalid Date, Negative Price, SQL Injection, Checkout Before Checkin, XSS Injection |

## How to Run

1. Import `restful-booker-collection.json` into Postman
2. Create an Environment with variable `base_url` = `https://restful-booker.herokuapp.com`
3. Run **Get Token** first to authenticate
4. Run other requests in order

## Bugs Found

| #   | Request                                  | Expected         | Actual                                 | Severity |
| --- | ---------------------------------------- | ---------------- | -------------------------------------- | -------- |
| 1   | Create Booking - Missing Fields          | 400 Bad Request  | 500 Internal Server Error              | High     |
| 2   | Create Booking - Invalid Date            | 400 Bad Request  | 200 OK — corrupted date `0NaN-aN-aN`   | High     |
| 3   | Create Booking - Negative Price          | 400 Bad Request  | 200 OK — accepts `-999`                | Critical |
| 4   | Create Booking - Checkout Before Checkin | 400 Bad Request  | 200 OK — accepts impossible date range | High     |
| 5   | Create Booking - XSS Injection           | 400 or sanitized | 200 OK — stores raw `<script>` tag     | Critical |
