# Node-Excel-Export: Streamlined Excel Generation for Node.js Applications

## Project Overview

Node-Excel-Export is a lightweight and efficient Node.js library designed to simplify the process of generating Excel (.xlsx) files programmatically. The library provides a straightforward way to convert data sets into Excel spreadsheets with minimal configuration and overhead.

### Key Features

- **Simple Data Export**: Easily convert JSON or array-based data into Excel spreadsheet format
- **Flexible Column Configuration**: Supports custom column definitions, including captions, types, and widths
- **Multiple Sheet Generation**: Ability to create multiple sheets in a single Excel workbook
- **Data Type Support**: Handles various data types including strings, numbers, dates, and boolean values
- **Custom Styling**: Optional support for custom XML style configurations

### Use Cases

This library is ideal for developers who need to:
- Generate reports dynamically
- Export data from databases or APIs to Excel
- Create spreadsheets with complex data structures
- Automate Excel file generation in Node.js applications

### Performance and Efficiency

- Lightweight implementation with minimal dependencies
- Uses streaming and efficient XML generation techniques
- Supports large datasets with optimized memory usage

## Getting Started, Installation, and Setup

## Quick Start

### Installation

Install the package using npm:

```bash
npm install excel-export
```

### Basic Usage

#### Creating a Simple Excel File

```javascript
const nodeExcel = require('excel-export');

// Configure columns
const conf = {
  cols: [{
    caption: 'Name',
    type: 'string'
  }, {
    caption: 'Date',
    type: 'date'
  }, {
    caption: 'Number',
    type: 'number'
  }],
  
  // Add data rows
  rows: [
    ['John Doe', new Date(), 42],
    ['Jane Smith', new Date(), 99]
  ]
};

// Generate Excel file
const excelBuffer = nodeExcel.execute(conf);
```

### Advanced Configuration

#### Column Configuration Options

- `caption`: Column header text
- `type`: Data type (`'string'`, `'date'`, `'bool'`, `'number'`)
- `width`: Column width
- `beforeCellWrite`: Custom cell preprocessing function
- `captionStyleIndex`: Styling index for column header

#### Supported Features

- Multiple sheet generation
- Custom data transformations
- Date and number formatting
- Flexible column definitions

### Synchronous and Asynchronous Methods

```javascript
// Synchronous execution
const result = nodeExcel.execute(config);

// Asynchronous execution
nodeExcel.executeAsync(config, (result) => {
  // Handle result
});
```

### Notes

- Requires Node.js
- Works best with Express.js for web applications
- Generates `.xlsx` files compatible with Microsoft Excel

## API Reference

### Exports and Main Functions

#### `execute(config)`
- **Description**: Generates an Excel spreadsheet based on configuration parameters
- **Parameters**:
  - `config` (Object | Array): Configuration for generating Excel sheets
    - Single sheet configuration:
      - `name` (string, optional): Name of the sheet (defaults to "sheet1", "sheet2", etc.)
      - `cols` (Array): Column definitions for the sheet
        - `caption` (string): Column header text
        - `type` (string): Data type of column ('string', 'number', 'date', 'bool')
        - `width` (number, optional): Column width
        - `captionStyleIndex` (number, optional): Style index for column header
        - `beforeCellWrite` (function, optional): Callback for cell data transformation
      - `rows` (Array): Data rows for the sheet
  - **Returns**: Raw Excel file buffer
- **Example**:
  ```javascript
  const result = execute({
    name: 'Sales Report',
    cols: [
      { caption: 'Name', type: 'string' },
      { caption: 'Amount', type: 'number' }
    ],
    rows: [
      ['John Doe', 1000],
      ['Jane Smith', 1500]
    ]
  });
  ```

#### `executeAsync(config, callback)`
- **Description**: Async version of `execute()` that uses `process.nextTick()`
- **Parameters**:
  - `config`: Same as `execute()`
  - `callback`: Function to handle the generated Excel file
- **Example**:
  ```javascript
  executeAsync(config, (result) => {
    // Handle generated Excel file
  });
  ```

### Utility Prototypes and Functions

#### Date Prototypes
- `Date.prototype.getJulian()`
  - **Description**: Converts a date to its Julian calendar representation
  - **Returns**: Julian date number

- `Date.prototype.oaDate()`
  - **Description**: Converts a date to Excel's serial date format
  - **Returns**: Excel date serial number

#### Utility Functions

- `getColumnLetter(col)`
  - **Description**: Converts a numeric column index to Excel column letter(s)
  - **Parameters**:
    - `col` (number): Column index (1-based)
  - **Returns**: Column letter(s) like 'A', 'B', 'AA'
  - **Throws**: Error if column index is 0 or negative

### Supported Cell Types
- `string`: Text values
- `number`: Numeric values
- `date`: Date values
- `bool`: Boolean values

## Project Structure

The project follows a straightforward directory structure designed to support Excel export functionality:

```
.
├── example/              # Contains example usage and demonstration files
│   ├── app.js            # Sample application showcasing library usage
│   ├── package.json      # Example project dependencies
│   └── styles.xml        # XML stylesheet for Excel export configuration
├── test/                 # Unit testing directory
│   └── main.js           # Main test suite for the library
├── index.js              # Primary entry point of the library
├── sheet.js              # Core implementation for sheet-related operations
├── package.json          # Project metadata and dependency management
└── .gitignore            # Specifies intentionally untracked files to ignore
```

#### Key Directories
- `example/`: Provides sample code and demonstrates how to use the library
- `test/`: Contains unit tests to ensure library functionality and reliability

#### Core Files
- `index.js`: Main entry point for the Excel export library
- `sheet.js`: Implements core sheet-related functionality
- `package.json`: Defines project metadata, dependencies, and scripts

## Technologies Used

### Languages
- JavaScript (Node.js)

### Core Libraries and Dependencies
- `collections`: Data structure library for advanced collection handling
- `node-zip`: Library for creating ZIP archives (used for Excel file generation)

### Development and Testing
- Mocha: Testing framework for running unit tests
- Should.js: Assertion library for test cases

### File Formats
- XML (for styles configuration)
- XLSX (Excel spreadsheet export)

### Runtime Environment
- Node.js

### Project Management
- npm (package management)

## Contributing

We welcome and appreciate contributions to the Node Excel Export project! Before contributing, please follow these guidelines:

### How to Contribute

1. Fork the repository and create your branch from `main`.
2. If you've added code that should be tested, add tests using Mocha.
3. Ensure the test suite passes by running `npm test`.
4. Make sure your code follows the existing code style of the project.

### Contribution Process

- Open an issue to discuss proposed changes before making significant modifications.
- Create clear and descriptive pull requests.
- Be respectful and constructive in all interactions.

### Development Setup

- Ensure you have Node.js installed
- Install dependencies: `npm install`
- Run tests: `npm test`

### Testing

The project uses Mocha for testing. When contributing:
- Write tests for new functionality
- Ensure all existing tests pass
- Test both single and multi-sheet Excel export scenarios

### Code Style

- Follow the existing JavaScript coding conventions in the project
- Use clear, descriptive variable and function names
- Include comments for complex logic

### Reporting Issues

- Use the GitHub Issues section
- Provide a clear description of the issue
- Include steps to reproduce, expected behavior, and actual behavior
- If possible, include a minimal reproducible example

### License

By contributing, you agree that your contributions will be licensed under the project's BSD license.

## License

This project is licensed under the BSD License. 

For the full license text, please refer to the license details specified in the `package.json` file. 

#### Key Provisions
- The BSD License is a permissive free software license
- Allows for reuse within both open source and proprietary software
- Requires preservation of copyright and license notices

### Permissions
- Commercial use
- Modification
- Distribution
- Private use

### Conditions
- License and copyright notice must be included
- Source code may be required if distributed

#### Additional Information
For specific details about the BSD License, visit the [Open Source Initiative BSD License page](https://opensource.org/licenses/BSD-3-Clause).