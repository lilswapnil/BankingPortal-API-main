API Documentation - Banking Portal
Introduction: The Banking Portal API allows users to perform various banking operations, including managing accounts, fund transfers, and transactions. This document provides details on each API endpoint, its request parameters, response structure, and authentication requirements. It also includes information on error handling and status codes.

Authentication: The API endpoints require bearer token authentication. Users must obtain a valid access token and include it in the "Authorization" header with the "Bearer" scheme to access protected endpoints.

Base URL: http://localhost:8180

1. Account Endpoints
1.1. Check PIN Created
Endpoint: /api/account/pin/check
Method: GET
Authorization: Bearer Token
Request Body: None
Description: Checks if a PIN has been created for the user's account.
Response:
Status Code: 200 OK
Body:
{
    "hasPIN": true,
    "msg": "PIN Created"
}
or
{
    "hasPIN": false,
    "msg": "Pin Not Created"
}
Possible Status Codes:

200 OK: The PIN status was successfully retrieved.
401 Unauthorized: The user is not authenticated. Please ensure you include a valid bearer token in the request header.
1.2. Create PIN
Endpoint: /api/account/pin/create
Method: POST
Authorization: Bearer Token
Request Body:
{
    "pin": "1234",
    "password": "secretpassword1"
}
Description: Creates a new PIN for the user's account.
Response:
Status Code: 200 OK
Body:
{
    "msg": "PIN created successfully"
}
Possible Status Codes:

200 OK: The PIN was successfully created.
400 Bad Request: The request body is missing or invalid.
401 Unauthorized: The user is not authenticated or the provided password is incorrect. Please ensure you include a valid bearer token in the request header.
404 Not Found: The user's account was not found.
1.3. Update PIN
Endpoint: /api/account/pin/update
Method: POST
Authorization: Bearer Token
Request Body:
{
    "oldPin": "4321",
    "newPin": "1234",
    "password": "secretpassword1"
}
Description: Updates the existing PIN for the user's account.
Response:
Status Code: 200 OK
Body:
{
    "msg": "PIN updated successfully"
}
Possible Status Codes:

200 OK: The PIN was successfully updated.
400 Bad Request: The request body is missing or invalid.
401 Unauthorized: The user is not authenticated, the provided password is incorrect, or the old PIN is incorrect. Please ensure you include a valid bearer token in the request header.
404 Not Found: The user's account was not found.
1.4. Withdraw
Endpoint: /api/account/withdraw
Method: POST
Authorization: Bearer Token
Request Body:
{
    "amount": 10.0,
    "pin": "4321"
}
Description: Withdraws the specified amount from the user's account.
Response:
Status Code: 200 OK
Body:
{
    "msg": "Cash withdrawn successfully"
}
Possible Status Codes:

200 OK: The cash withdrawal was successful.
400 Bad Request: The request body is missing or invalid, or the account does not have sufficient balance.
401 Unauthorized: The user is not authenticated or the provided PIN is incorrect. Please ensure you include a valid bearer token in the request header.
404 Not Found: The user's account was not found.
1.5. Deposit
Endpoint: /api/account/deposit
Method: POST
Authorization: Bearer Token
Request Body:
{
    "amount": 100.0,
    "pin": "4321"
}
Description: Deposits the specified amount into the user's account.
Response:
Status Code: 200 OK
Body:
{
    "msg": "Cash deposited successfully"
}
Possible Status Codes:

200 OK: The cash deposit was successful.
400 Bad Request: The request body is missing or invalid.
401 Unauthorized: The user is not authenticated or the provided PIN is incorrect. Please ensure you include a valid bearer token in the request header.
404 Not Found: The user's account was not found.
1.6. Fund Transfer
Endpoint: /api/account/fund-transfer
Method: POST
Authorization: Bearer Token
Request Body:
{
    "amount": 10.0,
    "pin": "4321",
    "targetAccountNumber": "556704"
}
Description: Transfers the specified amount to another user's account.
Response:
Status Code: 200 OK
Body:
{
    "msg": "Fund transferred successfully"
}
Possible Status Codes:

200 OK: The fund transfer was successful.
400 Bad Request: The request body is missing or invalid, or the account does not have sufficient balance.
401 Unauthorized: The user is not authenticated or the provided PIN is incorrect. Please ensure you include a valid bearer token in the request header.
404 Not Found: The user's source or target account was not found.
1.7. Transactions
Endpoint: /api/account/transactions
Method: GET
Authorization: Bearer Token
Description: Retrieves the list of transactions for the user's account.
Response:
Status Code: 200 OK
Body: List of transaction objects.
Possible Status Codes:

200 OK: The list of transactions was successfully retrieved.
401 Unauthorized: The user is not authenticated. Please ensure you include a valid bearer token in the request header.
1.8. Account Details
Endpoint: /api/dashboard/account
Method: GET
Authorization: Bearer Token
Description: Retrieves details of the user's account.
Response:
Status Code: 200 OK
Body: Account details object.
Possible Status Codes:

200 OK: The account details were successfully retrieved.
401 Unauthorized: The user is not authenticated. Please
ensure you include a valid bearer token in the request header.

404 Not Found: The user's account was not found.
2. User Endpoints
2.1. Register User
Endpoint: /api/users/register
Method: POST
Request Body:
{
    "name": "Abhishek a",
    "password": "secretpassword2",
    "email": "jonoe@gmail.com",
    "address": "123 Main Street",
    "phone_number": "134566690"
}
Description: Registers a new user with the provided details.
Response:
Status Code: 200 OK
Body:
{
    "name": "Abhishek a",
    "email": "jonoe@gmail.com",
    "accountNumber": "236480",
    "IFSC_code": "[IFSC_CODE]",
    "branch": "[BRANCH]",
    "account_type": "[ACCOUNT_TYPE]"
}
Possible Status Codes:

200 OK: The user was successfully registered.
400 Bad Request: The request body is missing or invalid.
404 Not Found: The user's account was not found.
2.2. Get User Details
Endpoint: /api/dashboard/user
Method: GET
Authorization: Bearer Token
Description: Retrieves details of the authenticated user.
Response:
Status Code: 200 OK
Body: User details object.
Possible Status Codes:

200 OK: The user details were successfully retrieved.
401 Unauthorized: The user is not authenticated. Please ensure you include a valid bearer token in the request header.
404 Not Found: The user's account was not found.
2.3. Login
Endpoint: /api/users/login
Method: POST
Request Body:
{
    "accountNumber": "236480",
    "password": "secretpassword2"
}
Description: Logs in the user with the provided account number and password.
Response:
Status Code: 200 OK
Body:
{
    "token": "[JWT_TOKEN]"
}
Possible Status Codes:

200 OK: The login was successful, and a JWT token is provided in the response body.
400 Bad Request: The request body is missing or invalid.
401 Unauthorized: The provided account number or password is incorrect.
404 Not Found: The user's account was not found.
Error Handling: The API implements global exception handling for the following scenarios:

NotFoundException: Returns 404 Not Found with an error message.
UnauthorizedException: Returns 401 Unauthorized with an error message.
InsufficientBalanceException: Returns 400 Bad Request with an error message.
Please note that this API documentation provides an overview of the available endpoints, request parameters, and response structures, along with additional details on error handling and status codes. For a comprehensive understanding of the API, further details such as possible response data and detailed error messages should be included in the final API documentation.
