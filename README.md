# Backend Project

## Overview

The purpose of this project is to show how you develop. Do not focus on being feature complete, but on well structured and robust code execution and data manipulation.

### Setting

A client has come to you requesting a backend server that they can use to authenicate users, and run arbitrary, long running tasks based off of user permission levels.
Task requests return a task id, which identifies the task on the server. The user can use that id to check the status of the task (which, if the task is done will return the result of the task),
or they can cancel the task.

You are to develop a server application that accepts https requests according to the specifications listed below.

## Specifications

Task Types

- Arbitrary JS
  - Only Admins may run this task
  - JS code is passed as a string
  - The result of running the JS is returned as the result when the task completes
- Delay

  - A time in seconds is passed as a number
  - All authenticated users may run this task
  - Zero is returned as the result when the task completes

- Minimum Viable Product
  - Endpoint to Authenticate users based off of a username and password
    - If the user exists, a token should be returned to identify the user
      - Token identifies the user
      - Token expires after a specific duration
    - If the user does not exist, then the endpoint should reject the user login
  - Endpoint(s) to manage users
    - Create users
      - Only Admin users may use
      - Must provide username, password, and Authorization level (Admin, User)
    - Edit users
      - Only Admin users may use unless the user is editing themselves
      - If a user tries to change their own Authorization level, then the request is rejected
    - Delete users
      - Only Admin may use
      - If a user is deleted, then any active tokens are invalidated
  - Endpoint to start task
    - Users may only start tasks that their authorization level permits
    - The task id is returned on successful start of the task
  - Endpoint to stop task
    - Users may only stop tasks that are owned by them, or if the task is owned by a User and the token used belongs to an admin
  - Endpoint to check status of task
    - Users may only check tasks that are owned by them, or if the task is owned by a User and the token used belongs to an admin
    - If the task does not exist, then a 404 is returned
    - If the user does not have permission, then their request is rejected appropriately
