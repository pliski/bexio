# Bexio
[![Dependencies](https://david-dm.org/mathewmeconry/bexio/status.svg)](https://david-dm.org/mathewmeconry/bexio)
[![Known Vulnerabilities](https://snyk.io/test/npm/bexio/badge.svg)](https://snyk.io/test/npm/bexio)
[![codecov](https://codecov.io/gh/mathewmeconry/bexio/branch/master/graph/badge.svg)](https://codecov.io/gh/mathewmeconry/bexio)
[![Tests](https://github.com/mathewmeconry/bexio/workflows/Test/badge.svg)](https://github.com/mathewmeconry/bexio/actions)
[![Publish](https://github.com/mathewmeconry/bexio/workflows/Publish/badge.svg)](https://github.com/mathewmeconry/bexio/actions)
![npm](https://img.shields.io/npm/v/bexio)

This library provides a comprehensive set of functions to interact with the Bexio API. It includes methods for all available endpoints, including authentication, error handling, and type safety.

## Installation

```sh
# Using pnpm (recommended)
pnpm add bexio

# Using npm
npm install bexio

# Using yarn
yarn add bexio
```

## Features

- Full TypeScript support with included type definitions
- Comprehensive coverage of Bexio API endpoints
- Promise-based API
- Error handling with detailed responses
- Support for all CRUD operations where applicable

## Functions

### Implemented

You can find a list of all implements functions in the [wiki](https://github.com/mathewmeconry/bexio/wiki)

### Missing

You can find a list of all missing functions here: [Missing Functions](https://github.com/mathewmeconry/bexio/wiki#missing-functions).  
If you need a function implemented, please fill out an issue.


## Basic Usage

```typescript
import Bexio from "bexio";

// Initialize with your API token
const bexio = new Bexio("YOUR_API_TOKEN");

// Example: Fetch a contact
bexio.contacts.show(1)
.then(contact => console.log(contact))
.catch(error => console.error(error));

// Example: Create a new invoice
const invoice = await bexio.invoices.create({
// invoice details
});
```
## Available Resources

The library provides access to the following Bexio resources:

### Contacts
- List contacts
- Create contact
- Show contact details
- Update contact
- Delete contact

### Projects
- List projects
- Create project
- Show project details
- Update project
- Delete project

### Invoices
- List invoices
- Create invoice
- Show invoice details
- Update invoice
- Delete invoice
- Generate PDF

### Items
- List items
- Create item
- Show item details
- Update item
- Delete item

### And more...
- Business Activities
- Contact Relations
- Contact Groups
- Project Statuses
- Project Types
- Bills
- Payments
- Timetracking
- Users

## Authentication

The library requires an API token from Bexio. To obtain an API token:

1. Log in to your Bexio account
2. Navigate to Settings > Developer
3. Create a new API token


## Error Handling

The library provides comprehensive error handling for all API requests. If an error occurs, it will be thrown as a JavaScript Error object with the following properties:

- `code`: The HTTP status code
- `message`: The error message
- `data`: The response data

Example:
```typescript
try {
    await bexio.contacts.show(999);
} catch (error) {
    console.error(`Status: ${error.code}`);
    console.error(`Message: ${error.message}`);
}
```

## TypeScript Support

All interfaces and types are exported and can be imported directly:

```typescript
import { ContactsStatic } from "bexio";
const contact: ContactsStatic.ContactCreate = {
    // TypeScript will provide type hints here
};
```
## Development

To contribute to this library:

1. Fork the repository
2. Install dependencies:
```bash
   pnpm install
```
3. Make your changes
4. Run tests:
```bash
   pnpm test
```
5. Build:
```bash
   pnpm build
 ```

## Testing

The library uses Jest for testing. Run tests with:
```bash
   pnpm test
```
Coverage reports are automatically generated and can be found in the `coverage` directory.

## Support

- Supports Node.js >= 10.0
- TypeScript support included
- Full API documentation available at [docs.bexio.com](https://docs.bexio.com/)


## Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin feature/my-new-feature`
5. Submit a pull request

## Issues

If you find a bug or would like to request a new feature, please [open an issue](https://github.com/mathewmeconry/bexio/issues).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

