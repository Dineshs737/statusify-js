# @uthayakumar-dinesh/statusify-js

[![npm version](https://badge.fury.io/js/@uthayakumar-dinesh%2Fstatusify.svg)](https://badge.fury.io/js/@uthayakumar-dinesh%2Fstatusify)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

A lightweight JavaScript package that provides HTTP status codes as constants with utility functions for reverse lookup operations.

## Installation

```bash
npm install @uthayakumar-dinesh/statusify-js
```

## Usage

### CommonJS

```javascript
const {
  HTTP_STATUS,
  getStatusName,
} = require("@uthayakumar-dinesh/statusify-js");

// Using status constants
console.log(HTTP_STATUS.OK); // 200
console.log(HTTP_STATUS.NOT_FOUND); // 404
console.log(HTTP_STATUS.INTERNAL_SERVER_ERROR); // 500

// Get status name from code
console.log(getStatusName(200)); // "OK"
console.log(getStatusName(404)); // "NOT_FOUND"
console.log(getStatusName(999)); // "UNKNOWN_STATUS"
```

### ES6 Modules

```javascript
import { HTTP_STATUS, getStatusName } from "@uthayakumar-dinesh/statusify-js";

// Same usage as above
console.log(HTTP_STATUS.CREATED); // 201
console.log(getStatusName(201)); // "CREATED"
```

### Express.js Example

```javascript
const express = require("express");
const {
  HTTP_STATUS,
  getStatusName,
} = require("@uthayakumar-dinesh/statusify-js");

const app = express();

app.get("/users/:id", (req, res) => {
  const user = findUser(req.params.id);

  if (!user) {
    return res.status(HTTP_STATUS.NOT_FOUND).json({
      error: "User not found",
      statusCode: HTTP_STATUS.NOT_FOUND,
      statusName: getStatusName(HTTP_STATUS.NOT_FOUND),
    });
  }

  res.status(HTTP_STATUS.OK).json(user);
});
```

### API Response Helper

```javascript
function createApiResponse(statusCode, data = null, message = "") {
  return {
    statusCode,
    statusName: getStatusName(statusCode),
    success: statusCode >= 200 && statusCode < 300,
    message,
    data,
  };
}

// Usage
const successResponse = createApiResponse(HTTP_STATUS.CREATED, {
  id: 1,
  name: "John",
});
const errorResponse = createApiResponse(
  HTTP_STATUS.BAD_REQUEST,
  null,
  "Invalid input",
);
```

## API Reference

### HTTP_STATUS Object

Contains all HTTP status codes as constants:

```javascript
const HTTP_STATUS = {
  // 1xx Informational
  CONTINUE: 100,
  SWITCHING_PROTOCOLS: 101,

  // 2xx Success
  OK: 200,
  CREATED: 201,
  ACCEPTED: 202,
  NON_AUTHORITATIVE_INFORMATION: 203,
  NO_CONTENT: 204,
  RESET_CONTENT: 205,
  PARTIAL_CONTENT: 206,

  // 3xx Redirection
  MULTIPLE_CHOICES: 300,
  MOVED_PERMANENTLY: 301,
  FOUND: 302,
  SEE_OTHER: 303,
  NOT_MODIFIED: 304,
  TEMPORARY_REDIRECT: 307,
  PERMANENT_REDIRECT: 308,

  // 4xx Client Errors
  BAD_REQUEST: 400,
  UNAUTHORIZED: 401,
  PAYMENT_REQUIRED: 402,
  FORBIDDEN: 403,
  NOT_FOUND: 404,
  METHOD_NOT_ALLOWED: 405,
  NOT_ACCEPTABLE: 406,
  REQUEST_TIMEOUT: 408,
  CONFLICT: 409,
  GONE: 410,
  LENGTH_REQUIRED: 411,
  PRECONDITION_FAILED: 412,
  PAYLOAD_TOO_LARGE: 413,
  URI_TOO_LONG: 414,
  UNSUPPORTED_MEDIA_TYPE: 415,
  TOO_MANY_REQUESTS: 429,

  // 5xx Server Errors
  INTERNAL_SERVER_ERROR: 500,
  NOT_IMPLEMENTED: 501,
  BAD_GATEWAY: 502,
  SERVICE_UNAVAILABLE: 503,
  GATEWAY_TIMEOUT: 504,
};
```

### getStatusName(code)

Returns the constant name for a given HTTP status code.

**Parameters:**

- `code` (number): The HTTP status code

**Returns:**

- `string`: The constant name or `"UNKNOWN_STATUS"` if not found

## Available Status Codes

### 1xx Informational

| Code | Constant              | Description         |
| ---- | --------------------- | ------------------- |
| 100  | `CONTINUE`            | Continue            |
| 101  | `SWITCHING_PROTOCOLS` | Switching Protocols |

### 2xx Success

| Code | Constant                        | Description                   |
| ---- | ------------------------------- | ----------------------------- |
| 200  | `OK`                            | OK                            |
| 201  | `CREATED`                       | Created                       |
| 202  | `ACCEPTED`                      | Accepted                      |
| 203  | `NON_AUTHORITATIVE_INFORMATION` | Non-Authoritative Information |
| 204  | `NO_CONTENT`                    | No Content                    |
| 205  | `RESET_CONTENT`                 | Reset Content                 |
| 206  | `PARTIAL_CONTENT`               | Partial Content               |

### 3xx Redirection

| Code | Constant             | Description        |
| ---- | -------------------- | ------------------ |
| 300  | `MULTIPLE_CHOICES`   | Multiple Choices   |
| 301  | `MOVED_PERMANENTLY`  | Moved Permanently  |
| 302  | `FOUND`              | Found              |
| 303  | `SEE_OTHER`          | See Other          |
| 304  | `NOT_MODIFIED`       | Not Modified       |
| 307  | `TEMPORARY_REDIRECT` | Temporary Redirect |
| 308  | `PERMANENT_REDIRECT` | Permanent Redirect |

### 4xx Client Errors

| Code | Constant                 | Description            |
| ---- | ------------------------ | ---------------------- |
| 400  | `BAD_REQUEST`            | Bad Request            |
| 401  | `UNAUTHORIZED`           | Unauthorized           |
| 402  | `PAYMENT_REQUIRED`       | Payment Required       |
| 403  | `FORBIDDEN`              | Forbidden              |
| 404  | `NOT_FOUND`              | Not Found              |
| 405  | `METHOD_NOT_ALLOWED`     | Method Not Allowed     |
| 406  | `NOT_ACCEPTABLE`         | Not Acceptable         |
| 408  | `REQUEST_TIMEOUT`        | Request Timeout        |
| 409  | `CONFLICT`               | Conflict               |
| 410  | `GONE`                   | Gone                   |
| 411  | `LENGTH_REQUIRED`        | Length Required        |
| 412  | `PRECONDITION_FAILED`    | Precondition Failed    |
| 413  | `PAYLOAD_TOO_LARGE`      | Payload Too Large      |
| 414  | `URI_TOO_LONG`           | URI Too Long           |
| 415  | `UNSUPPORTED_MEDIA_TYPE` | Unsupported Media Type |
| 429  | `TOO_MANY_REQUESTS`      | Too Many Requests      |

### 5xx Server Errors

| Code | Constant                | Description           |
| ---- | ----------------------- | --------------------- |
| 500  | `INTERNAL_SERVER_ERROR` | Internal Server Error |
| 501  | `NOT_IMPLEMENTED`       | Not Implemented       |
| 502  | `BAD_GATEWAY`           | Bad Gateway           |
| 503  | `SERVICE_UNAVAILABLE`   | Service Unavailable   |
| 504  | `GATEWAY_TIMEOUT`       | Gateway Timeout       |

## Browser Support

This package works in:

- Node.js 12+
- All modern browsers (ES6+ support)
- Can be bundled with webpack, rollup, etc.

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Links

- **GitHub**: [https://github.com/uthayakumar-dinesh/statusify](https://github.com/Dineshs737/statusify-js)
- **npm**: [@uthayakumar-dinesh/statusify](https://www.npmjs.com/package/@uthayakumar-dinesh/statusify-js)
