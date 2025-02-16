# Unhandled Promise Rejection in Node.js Express Application

This repository demonstrates a common but subtle error in Node.js applications using Express.js: unhandled promise rejections.  The example code includes an Express route handler that performs an asynchronous operation. If the operation fails and rejects the promise, the error is logged to the console, but the server continues running without proper error handling.  This can lead to unexpected behavior and instability.

The `bug.js` file contains the buggy code.  The `bugSolution.js` file shows how to fix the issue using `process.on('unhandledRejection', ...)` for global error handling and `try...catch` blocks for more specific handling within the route handler.

## How to Reproduce

1. Clone this repository.
2. Navigate to the repository directory.
3. Run `npm install express`.
4. Run `node bug.js`.
5. Observe the console output.  Refresh the page multiple times to see the error occur randomly.
6. Run `node bugSolution.js` to see the improved error handling.

## Solution

The solution involves two key improvements:

* **Global Unhandled Rejection Handling:**  Using `process.on('unhandledRejection', ...)` to handle promise rejections that are not caught anywhere else. This prevents the application from crashing silently. 
* **Improved Route Handler:** Wrapping the asynchronous operation in a `try...catch` block to gracefully handle exceptions that might occur within the `someAsyncOperation` function.