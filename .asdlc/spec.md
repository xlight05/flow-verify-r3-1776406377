# Overview

This project is a simple RESTful API service for managing a personal todo list. The system provides a minimal set of endpoints that allow clients to retrieve all existing todos, create new todos, and delete todos by identifier. It is intended as a lightweight backend service that can be consumed by web, mobile, or command-line clients.

The target users are developers who need a straightforward task-tracking backend, or end users interacting through a client application that consumes the API. The high-level approach is to expose a small, predictable HTTP interface backed by persistent storage, with clear request/response contracts and standard error handling.

The system prioritizes simplicity, reliability, and ease of integration over advanced features. It should be easy to run, test, and extend in the future with additional capabilities such as updates, filtering, or user accounts.

# Capabilities

## Todo Data Model
- Each todo must have a unique identifier assigned by the system upon creation.
- Each todo must include a title as a required text field.
- Each todo may optionally include a description as a free-text field.
- Each todo must include a completion status, defaulting to "not completed" upon creation.
- Each todo must record a creation timestamp set automatically by the system.

## List Todos Endpoint
- The system must expose an endpoint to retrieve all existing todos.
- The response must return todos as a JSON array.
- Each item in the response must include the identifier, title, description, completion status, and creation timestamp.
- When no todos exist, the endpoint must return an empty array with a success status code.
- The endpoint must respond with HTTP 200 on success.

## Create Todo Endpoint
- The system must expose an endpoint to create a new todo from a JSON request body.
- The request must require a non-empty title field.
- The request may include an optional description field.
- The system must reject requests with missing or empty titles and return an HTTP 400 response with a descriptive error message.
- On success, the endpoint must return HTTP 201 with the newly created todo, including its assigned identifier.
- The system must persist the created todo so it appears in subsequent list requests.

## Delete Todo Endpoint
- The system must expose an endpoint to delete a todo by its identifier.
- On successful deletion, the endpoint must return HTTP 204 with no response body.
- If the specified identifier does not exist, the endpoint must return HTTP 404 with a descriptive error message.
- Once deleted, a todo must no longer appear in list responses.

## Request and Response Standards
- All request and response bodies must use JSON format.
- All responses must include appropriate HTTP status codes reflecting the outcome.
- Error responses must include a consistent structure containing an error message.
- The API must use clear, predictable URL paths for each resource operation.

## Data Persistence
- Todos must be stored in persistent storage so data survives service restarts.
- The system must ensure identifiers remain unique across the lifetime of the service.

## Validation and Error Handling
- The system must validate incoming request payloads and reject malformed JSON with HTTP 400.
- The system must return HTTP 405 or equivalent for unsupported methods on valid paths.
- The system must return HTTP 404 for requests to unknown paths.
- Unexpected server errors must return HTTP 500 without leaking internal details.

## Non-Functional Requirements
- The API must respond to standard requests within 500 milliseconds under normal load.
- The API must handle concurrent requests without data corruption.
- The service must provide a health check endpoint indicating operational status.
- The API must log each request with method, path, and response status for observability.
- The service must be runnable locally with minimal configuration for development and testing.
