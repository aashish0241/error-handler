


# Custom Error Handler Middleware

An easy-to-use custom error handler middleware for Express.js. This package provides a structured way to handle errors in your backend application, with support for custom error classes and environment-specific stack traces.

## Features

- **Custom Error Class**: Standardize error responses with a custom error class.
- **Environment-Specific Stack Traces**: Includes stack traces in development mode only.
- **Easy Integration**: Plug-and-play error handling for Express.js.

## Installation

Install the package via npm:

```sh
npm install error-handler-cli
```

## Usage

### 1. Import the Middleware

```javascript
const { CustomError, errorHandler } = require('error-handler-cli');
```

### 2. Create an Express Application

Here's an example of how to use the custom error handler in an Express.js app:

```javascript
const express = require('express');
const { CustomError, errorHandler } = require('error-handler-cli');

const app = express();

// Route that throws a custom error
app.get('/error', (req, res, next) => {
    throw new CustomError('Invalid request data', 400);
});

// Route that throws a generic error
app.get('/generic-error', (req, res, next) => {
    next(new Error('Something went wrong!'));
});

// Use the custom error handler middleware
app.use(errorHandler);

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

### 3. Environment-Specific Stack Traces

- **Development Mode**: Displays detailed error messages and stack traces.
- **Production Mode**: Hides stack traces for security. Set `NODE_ENV=production` to enable this.

## API

### CustomError Class

The `CustomError` class is used to create standardized error objects.

#### Constructor:
```javascript
new CustomError(message, statusCode)
```

- `message` (string): The error message.
- `statusCode` (number): The HTTP status code (default: `500`).

### errorHandler Middleware

The `errorHandler` middleware is used to catch and process errors.

#### Signature:
```javascript
errorHandler(err, req, res, next)
```

- Automatically formats and sends error responses.
- Includes stack traces in development mode.

## Example Response

### Development Mode
```json
{
    "success": false,
    "message": "Invalid request data",
    "stack": "Error: Invalid request data\n    at /path/to/file.js:10:10"
}
```

### Production Mode
```json
{
    "success": false,
    "message": "Invalid request data"
}
```

## Contributing

Feel free to contribute by submitting issues or pull requests. We welcome all contributions!

## License

This project is licensed under the ISC License. See the LICENSE file for more details.

## Author

Developed by **Aashish Timsina**.
```
https://github.com/aashish0241
```