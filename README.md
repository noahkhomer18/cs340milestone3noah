Author: Noah Khomer
Course: CS 340 – Client Server Development
Date: November 22, 2024
Project Overview
This project is part of Milestone 3 for the CS 340 course. The objective was to work with a MongoDB instance to perform the following tasks:

Import a dataset into a MongoDB database.
Create single-field and compound indices to optimize query performance.
Set up user authentication to secure access to the database.
Steps and Highlights
1. Loading the Database
The Austin Animal Center (AAC) Outcomes dataset was loaded into MongoDB using the mongoimport tool.
Challenges Faced:
Initially, the import commands found online didn’t work due to missing the correct host and port values.
After researching, the issue was resolved by including the --host and --port options in the mongoimport command.
2. Query Verification
After the database was loaded, the following commands were executed to verify the data:
javascript
Copy code
use AAC
db.animals.countDocuments()
Confirmed that the database contained 10,000 records.
3. Indexing for Performance
Single Field Index:
Created an index on the breed field to optimize queries filtering by breed.
Verified the index usage with the explain function using:
javascript
Copy code
db.animals.find({ breed: "Labrador Retriever Mix" }).explain("executionStats")
Compound Index:
Created a compound index on breed and outcome_type fields to optimize queries filtering by multiple criteria.
Tested the compound index with:
javascript
Copy code
db.animals.find({ breed: "Labrador Retriever Mix", outcome_type: "Transfer" }).explain("executionStats")
4. Authentication Setup
Creating a New User:
Added a user (aacuser) with a readWrite role restricted to the AAC database using:
javascript
Copy code
db.createUser({
  user: "aacuser",
  pwd: "noah123",
  roles: [
    { role: "readWrite", db: "AAC" }
  ]
})
Faced an issue where the user already existed. Researched and updated the password with:
javascript
Copy code
db.updateUser("aacuser", { pwd: "noah123" })
Verification:
Tested the aacuser login in a second terminal session.
Verified the connection with:
javascript
Copy code
db.runCommand({ connectionStatus: 1 })
Confirmed limited access by listing accessible databases (AAC) and testing queries.
Deliverables
The following deliverables are included:

Screenshots of the MongoDB import process.
Commands and outputs for single-field and compound index creation and testing.
User authentication setup, including aacuser creation and connection verification.
Queries showing accessible databases and successful access to the AAC database.
Acknowledgments
Special thanks to the course announcements and MongoDB documentation for helping resolve common issues, such as ensuring the correct host/port and updating existing user passwords.

Next Steps
Tomorrow, I will:

Begin working on Week 4 Project 4-1: Create and Read in Python for MongoDB, integrating Python to perform CRUD operations on the database.
Update my progress for the Software Security course.
Contact
Feel free to reach out if you’d like to discuss MongoDB, Python integration, or database optimization techniques!
