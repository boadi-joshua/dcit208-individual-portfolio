UNIVERSITY OF GHANA DEPARTMENT OF 
COMPUTER SCIENCE  
DCIT 208 — SOFTWARE ENGINEERING  
INDIVIDUAL PORTFOLIO — IA03 
USE-CASE-TO-STORY TRACEABILITY CARD 
Overview & Student Details 
Item Details 
Student Name Joshua Boadi 
GitHub Username boadi-joshua 
Team / Sakai Group DE-SEGP 19 / Group 19 
Project Title Brainy Bites - East Legon 
Client/Domain Restaurant food-menu and customer-account 
management system 
Date 23 October 2026 
Selected Use Case Customer Logs In 
 
1. Source Evidence and Use-Case Importance 
Item Details 
Source Type Existing team GitHub issue 
Repository AbdiWaris/DE-DCIT208-GROUP-19 
Issue Number #1 
Issue Title Implement and Verify Customer Login 
Functionality 
Issue URL https://github.com/AbdiWaris/DE-DCIT208-GR
OUP-19/issues/1 
Issue Status Open 
 
Source Requirement 
The application needs to authenticate customers before they access account-related features. 
Guests should be able to browse the menu without an account, while logged-in customers may 
access functions that require authentication. 
Why This Use Case Matters 
Customer login distinguishes guests from authenticated customers. Guests may browse menu 
items, categories, descriptions, and prices, while protected account-related functions should 
only be available after the system verifies a customer's identity. 
2. Use-Case Card 
Field Description 
Use-case Name Customer Logs In 
Primary Actor Registered customer 
Goal Sign in successfully to access account-related 
features and activities that require 
authentication. 
Trigger The customer selects "Customer sign in" in the 
Brainy Bites application. 
Preconditions 1. The customer has an existing account. 2. 
The customer has an email address and 
password. 3. The login interface is available. 4. 
The authentication service and required data 
store are available. 5. The customer is not 
already logged in. 
 
Main Success Flow 
1. The customer opens the Brainy Bites application. 
2. The customer selects "Customer sign in". 
3. The system displays the login form. 
4. The customer enters an email address and password. 
5. The customer submits the login form. 
6. The frontend checks that the required fields are not empty. 
7. The frontend sends the login request to the authentication endpoint (POST 
/api/auth/login). 
8. The backend validates the submitted login details. 
9. The authentication service looks up the customer record using the submitted email 
address. 
10. The service verifies the submitted password against the stored password hash. 
11. If authentication succeeds, the system creates a session or token. 
12. The customer is redirected to the appropriate page (main menu page). 
13. The customer can access the features permitted to an authenticated customer. 
Alternate Flow: Guest Browses Without Logging In 
1. A visitor opens the application. 
2. The visitor does not select "Customer sign in". 
3. The system allows the visitor to browse menu items, categories, descriptions, and prices. 
4. The system restricts account-related features that require authentication. 
Exception Flow: Incorrect Credentials 
1. The customer enters an incorrect email address or password and submits the form. 
2. The system rejects the login attempt. 
3. No authenticated session or token is created. 
4. The application displays a safe error message without revealing whether the email exists. 
5. The customer remains unauthenticated and can try again. 
Postconditions 
● On Success: The customer is authenticated, a valid session/token is created, and 
permitted protected features become available. 
● On Failure: The customer remains unauthenticated, no valid session/token is created, 
and sensitive information is not exposed. 
3. User Story 
As a registered customer, I want to log in to my Brainy Bites account, So that I can access 
account-related features and activities that require authentication. 
4. Acceptance Criteria 
● AC1: Successful customer login 
○ Given a registered customer has a valid email address and password, 
○ When the customer enters the correct credentials and submits the form, 
○ Then the system authenticates the customer, 
○ And a valid session or authentication token is created, 
○ And the customer is redirected to the correct post-login page. 
● AC2: Incorrect login credentials 
○ Given a customer is on the login page, 
○ When the customer enters an incorrect email address or password, 
○ Then the system rejects the login attempt, 
○ And an appropriate error message is displayed, 
○ And no authenticated session or token is created, 
○ And the message does not reveal whether the email address exists. 
● AC3: Missing required login field 
○ Given a customer is on the login page, 
○ When the customer submits the form without an email address or password, 
○ Then validation feedback is displayed, 
○ And the customer remains unauthenticated. 
5. Non-Functional Requirement (NFR) 
Field Description 
Category Security and privacy
Requirement Passwords must be stored using an appropriate 
password-hashing method, not as readable 
plaintext. Authentication must only succeed 
after credentials are verified. Login errors 
should not disclose whether a particular email 
address is registered. 
Status Planned verification. 
Why This NFR Matters 
A login form alone does not guarantee secure authentication. Passwords should be protected 
before storage, protected features should not be accessible to unauthenticated users, and error 
messages should avoid exposing account information. 
How to Verify 
1. Review the authentication code to identify the password-hashing method. 
2. Check that stored password values are hashes rather than readable passwords. 
3. Test valid synthetic credentials and confirm the expected successful flow. 
4. Test an incorrect password and confirm no authenticated session is created. 
5. Test an unknown email address and check whether the error response avoids account 
enumeration. 
6. Check that passwords are not written to logs, API responses, or screenshots. 
6. Traceability Table 
Traceability Item Evidence / Description Status 
Requirement Authenticate customers for Under development 
account-related features while 
allowing public menu browsing. 
Source Evidence GitHub Issue #1: Implement Available 
and Verify Customer Login 
Functionality. 
Use Case Customer Logs In. Draft 
User Story Registered customer logs in to Draft 
access authenticated features. 
NFR Password hashing, safe Planned 
authentication, and generic 
error messages. 
Acceptance Criteria AC1 successful login; AC2 Planned 
incorrect credentials; AC3 
missing required field. 
Test Idea Reject an incorrect-password Planned 
login safely. 
Request-Flow Details Endpoint POST /api/auth/login, Pending code check 
data model users table.
7. GitHub Issue Evidence 
● Issue Title: Implement and Verify Customer Login Functionality 
● Issue Number: #1 
● Issue URL: https://github.com/AbdiWaris/DE-DCIT208-GROUP-19/issues/1 
● Status: Open 
8. Test Idea 
Field Details 
Test Name Reject customer login attempt with an incorrect 
password 
Test Type Planned manual end-to-end or integration test 
Starting Condition A synthetic test account exists in a 
development environment, and customer is 
logged out. 
Test Data Email: test.customer@example.test | 
Password: WrongPassword123! 
Action Open login page, enter synthetic email and 
incorrect password, select login button. 
Expected Result Attempt is rejected; safe error message shown; 
no session/token created; customer remains 
unauthenticated. 
Status PLANNED 
9. Request-Flow Reasoning 
Item Explanation / Verification Needed 
Actor Device Customer's smartphone, tablet, or computer 
with a web browser. 
Interface Brainy Bites web application and customer 
sign-in page. 
Route/Endpoint POST /api/auth/login 
Data Sent Email address and password in the login 
request body. 
Validation Frontend checks required fields; backend 
verifies credentials before authentication. 
Database/Service users table for account record and password 
verification. 
Validation Failure Missing fields trigger validation feedback and 
prevent authentication. 
Incorrect Credentials Attempt rejected with generic error message 
and no session created. 
Service Outage Fails safely, avoids partial sessions, and avoids 
logging raw passwords. 
Protected Data Email addresses, password hashes, session
Item 
10. Declarations & AI Disclosure 
Personal Understanding Declaration 
I understand the use case, user story, acceptance criteria, and traceability links submitted here, 
and I can explain them orally if called upon. 
● Signed: Joshua Boadi 
● Date: 23 October 2026 
AI Disclosure 
● AI Used: Yes (ChatGPT) 
● Date Used: 23 October 2026 
● Purpose: To review and structure the IA03 use-case-to-story traceability card, improve 
clarity, and format in 
Explanation / Verification Needed 
tokens, and account features. 
