# Node-Excel-Export: Elegant and Lightweight Excel Generation for Node.js

## Project Overview

Node-Excel-Export is a lightweight Node.js library designed to simplify the process of generating Excel (xlsx) files programmatically. It provides an intuitive interface for converting data sets into Excel spreadsheets with fine-grained control over formatting and content.

### Key Features
- Simple and straightforward Excel file generation
- Support for multiple sheet creation
- Flexible data type handling (strings, numbers, dates, booleans)
- Customizable column configurations
- Efficient shared string management for optimized file size
- Style customization options

### Problem Solved
Many developers struggle with complex Excel export libraries or manual spreadsheet generation. Node-Excel-Export addresses these challenges by:
- Providing a clean, JavaScript-based approach to Excel file creation
- Abstracting away the complexities of the Office Open XML (OOXML) file format
- Offering a lightweight solution with minimal dependencies
- Enabling dynamic data export with minimal overhead

### Benefits
- Cross-platform compatibility
- Low memory footprint
- Easy integration with Node.js applications
- Supports various data transformation scenarios
- Minimal external library requirements

## Getting Started, Installation, and Setup

### Prerequisites

- Node.js (Recommended: Latest LTS version)
- npm (Node Package Manager)

### Installation

Install the package using npm:

```bash
npm install excel-export
```

### Quick Start

#### Basic Usage

```javascript
const nodeExcel = require('excel-export');

// Configure columns and data
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
  
  rows: [
    ['John Doe', new Date(), 42],
    ['Jane Smith', new Date(), 99]
  ]
};

// Generate Excel file
const excelBuffer = nodeExcel.execute(conf);
```

### Development Setup

1. Clone the repository:
```bash
git clone https://github.com/functionscope/Node-Excel-Export.git
cd Node-Excel-Export
```

2. Install dependencies:
```bash
npm install
```

3. Run tests:
```bash
npm test
```

### Platform Considerations

- Works on all platforms supporting Node.js
- Tested on Windows, macOS, and Linux
- No additional platform-specific setup required

### Additional Configuration

#### Asynchronous File Generation

```javascript
nodeExcel.executeAsync(config, (result) => {
  // Handle generated Excel file
});
```

### Performance Notes

- Supports generating Excel files with multiple sheets
- Efficient memory usage for large datasets
- Minimal external dependencies

## Features / Capabilities

#### Core Features

- **Excel XLSX File Generation**: Easily convert data sets into Excel spreadsheets
- **Multiple Data Type Support**: Handles various data types including:
  - Strings
  - Numbers
  - Dates
  - Boolean values

#### Advanced Configuration Capabilities

- **Custom Column Definitions**: Define column properties like:
  - Caption
  - Type
  - Width
  - Custom cell preprocessing

- **Styling Support**: 
  - Apply custom Excel styles via XML configuration
  - Dynamic cell styling through `beforeCellWrite` callback

#### Flexible Sheet Generation

- **Single and Multi-Sheet Support**: 
  - Generate single worksheet Excel files
  - Create multiple worksheets in a single Excel file
  - Customize worksheet names

#### Advanced Data Transformation

- **Cell Preprocessing**: 
  - Transform cell data before writing
  - Modify cell types dynamically
  - Apply conditional styling

#### Performance and Compatibility

- **Node.js Integration**: Designed for seamless use in Node.js applications
- **Express.js Compatibility**: Easy integration with web frameworks
- **Lightweight Implementation**: Minimal dependencies

#### Export Features

- **Binary Export**: Generate Excel files ready for download
- **Flexible Configuration**: Highly customizable export process

## Usage Examples

## Basic Excel Export

### Creating a Simple Spreadsheet

```javascript
const nodeExcel = require('excel-export');

// Configure columns
const conf = {
  cols: [
    { 
      caption: 'String Column', 
      type: 'string' 
    },
    { 
      caption: 'Date Column', 
      type: 'date' 
    },
    { 
      caption: 'Boolean Column', 
      type: 'bool' 
    },
    { 
      caption: 'Number Column', 
      type: 'number' 
    }
  ],
  rows: [
    ['Hello', new Date(), true, 3.14159],
    ['World', new Date(), false, 2.7182]
  ]
};

// Generate Excel file
const result = nodeExcel.execute(conf);
```

### Advanced Column Configuration

```javascript
const conf = {
  cols: [
    {
      caption: 'String Column',
      type: 'string',
      width: 15,  // Column width
      captionStyleIndex: 1,  // Optional style for column header
      beforeCellWrite: function(row, cellData) {
        // Optional transformation of cell data
        return cellData.toUpperCase();
      }
    }
  ],
  rows: [
    ['sample text'],
    ['another text']
  ]
};
```

### Handling Different Data Types

```javascript
const conf = {
  cols: [
    { caption: 'String', type: 'string' },
    { caption: 'Date', type: 'date' },
    { caption: 'Boolean', type: 'bool' },
    { caption: 'Number', type: 'number' }
  ],
  rows: [
    ['Text', new Date(), true, 42],
    [null, null, false, null]  // Handling null values
  ]
};
```

### Generating Large Spreadsheets

```javascript
const uuid = require('node-uuid');

const conf = {
  cols: Array.from({length: 10}, (_, i) => ({
    caption: `Column ${i}`,
    type: 'string'
  })),
  rows: Array.from({length: 1000}, () => 
    Array.from({length: 10}, () => uuid.v4())
  )
};

const result = nodeExcel.execute(conf);
```

### Async Export

```javascript
nodeExcel.executeAsync(conf, function(result) {
  // Process result asynchronously
  fs.writeFileSync('output.xlsx', result, 'binary');
});
```

### Handling Dates and Timestamps

```javascript
const originDate = new Date(Date.UTC(1899, 11, 30));

const conf = {
  cols: [{
    caption: 'Date',
    type: 'date',
    beforeCellWrite: function(row, cellData, eOpt) {
      if (cellData === null) {
        eOpt.cellType = 'string';
        return 'N/A';
      }
      // Convert date to Excel timestamp
      return (cellData - originDate) / (24 * 60 * 60 * 1000);
    }
  }]
};
```

### External Styles

```javascript
const conf = {
  stylesXmlFile: 'custom_styles.xml',  // Path to custom styles XML
  // Other configuration
};
```

### Notes
- Input dates should typically be UTC dates to ensure accurate representation
- Null values are supported and will be rendered appropriately
- Custom cell transformations can be applied using `beforeCellWrite`
- Column widths and styles can be customized

## Project Structure

The project is organized with the following key directories and files:

### Root Directory
- `index.js`: The main entry point of the library
- `package.json`: Defines project metadata, dependencies, and scripts
- `sheet.js`: Likely contains core functionality for Excel sheet manipulation

### Subdirectories
#### `example/`
Contains example implementation files:
- `app.js`: Sample application demonstrating library usage
- `package.json`: Project dependencies for the example
- `styles.xml`: Potentially defines styling for Excel exports

#### `test/`
Contains test-related files:
- `main.js`: Test suite for the library

### Key Files
- `.gitignore`: Specifies intentionally untracked files to ignore
- `Readme.md`: Main project documentation
- `README_Prometheus.md`: Additional documentation (possibly related to Prometheus integration)

The project follows a typical Node.js library structure with clear separation between core library code, examples, and tests.

## Technologies Used

#### Runtime
- Node.js

#### Core Libraries
- `collections`: Data structure library
- `node-zip`: ZIP file creation and manipulation

#### Development and Testing
- Mocha: Testing framework
- Should.js: Assertion library

#### File Formats
- Excel XLSX export support

#### Programming Languages
- JavaScript (ECMAScript)

## Additional Notes

### Performance Considerations

When working with large datasets, be mindful of memory usage. The library uses streaming techniques to optimize Excel file generation, but extremely large datasets may require careful memory management.

### Compatibility and Limitations

- Fully compatible with Microsoft Excel and most modern spreadsheet applications
- Best suited for Node.js applications with moderate to large data export requirements
- XML-based styling offers flexibility but may have some limitations compared to full Excel formatting

### Version Compatibility

- Supports Node.js LTS versions
- Tested with Excel 2010 and newer versions
- May require additional configuration for specialized Excel features

### Security Notes

- Always sanitize and validate input data before generating Excel files
- Be cautious when using `beforeCellWrite` callback to prevent potential data manipulation

### Troubleshooting

#### Common Issues

- Ensure all required dependencies are correctly installed
- Check data types match the specified column configurations
- Verify XML style configurations for custom styling

#### Debugging Tips

- Use `executeAsync()` for better error handling in complex scenarios
- Log configuration objects to verify column and data settings
- Validate input data before Excel generation

### Future Development

The library is actively maintained with potential future enhancements including:
- Improved date and number formatting options
- Enhanced styling capabilities
- Performance optimizations for larger datasets

### Community and Support

- Report issues on the [GitHub repository](https://github.com/functionscope/Node-Excel-Export)
- Community support available through GitHub issues
- Contributions are welcome and appreciated

## Contributing

We welcome contributions to this Excel export library! To ensure a smooth contribution process, please follow these guidelines:

### Contribution Process

1. Fork the repository and create your branch from `main`.
2. Ensure your code follows the existing project structure and coding style.
3. Write or update tests for any changes you make, using the existing test framework (Mocha).

### Development Setup

- The project uses Node.js for development
- Install dependencies with `npm install`
- Run tests using `npm test`

### Testing

- All contributions must include appropriate test coverage
- Tests are written using Mocha and Should.js
- Run existing tests before submitting a pull request to ensure compatibility

### Code Guidelines

- Follow the existing code style in the project
- Use clear, descriptive variable and function names
- Add comments to explain complex logic
- Ensure code is clean and well-formatted

### Reporting Issues

- Use the GitHub Issues section to report bugs or suggest enhancements
- Provide a clear and detailed description of the issue
- Include steps to reproduce the problem, if applicable

### Pull Request Process

1. Update the README with details of changes if necessary
2. Ensure all tests pass
3. Make sure your code does not introduce new warnings or errors
4. Provide a clear description of your changes in the pull request

### Dependencies

- Project dependencies are managed via npm
- When adding new dependencies, provide a clear reason and update `package.json`

**Note:** By contributing, you agree that your contributions will be licensed under the project's BSD license.

## License

This project is licensed under the BSD License. 

For the full license text, please refer to the license details specified in the `package.json` file. The BSD License is a permissive free software license that allows for reuse within both free and proprietary software.

#### Key Permissions
- Commercial use is permitted
- Modification and distribution are allowed
- Provides an express grant of patent rights from contributors
- Requires preservation of the original copyright notice and disclaimer

##### Disclaimer
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.