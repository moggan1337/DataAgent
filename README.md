# DataAgent 📊

<!-- Badges -->
[![npm version](https://img.shields.io/npm/v/dataagent.svg)](https://www.npmjs.com/package/dataagent)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![Node.js Version](https://img.shields.io/node/v/dataagent.svg)](https://nodejs.org/)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](#)
[![Downloads](https://img.shields.io/npm/dm/dataagent.svg)](https://npmjs.com/package/dataagent)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

---

A powerful, lightweight data analysis library for Node.js and the browser. DataAgent provides seamless handling of CSV and JSON datasets with built-in statistical analysis, data visualization, and transformation capabilities.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage Examples](#usage-examples)
- [API Reference](#api-reference)
- [Configuration](#configuration)
- [Advanced Usage](#advanced-usage)
- [Error Handling](#error-handling)
- [Performance Tips](#performance-tips)
- [Contributing](#contributing)
- [License](#license)

---

## Features

### Core Capabilities

- **📄 Multi-Format Support** - Load and parse CSV, JSON, and JSON Lines formats with automatic type inference
- **📈 Statistical Analysis** - Comprehensive statistical computations including mean, median, mode, standard deviation, percentiles, and correlations
- **📊 Data Visualization** - Generate beautiful charts and graphs including bar charts, line charts, scatter plots, and histograms
- **🔄 Data Transformation** - Filter, sort, group, pivot, and reshape your data with a fluent API
- **🧹 Data Cleaning** - Handle missing values, detect outliers, normalize data, and fix type inconsistencies
- **📤 Export Capabilities** - Export results to CSV, JSON, or generate shareable visualization URLs

### Additional Features

- **TypeScript Support** - Full TypeScript definitions included for enhanced IDE support
- **Tree-Shakeable** - Import only what you need to minimize bundle size
- **Zero Dependencies** - No external runtime dependencies for core functionality
- **Stream Processing** - Handle large files efficiently with streaming support
- **Validation** - Built-in data validation and schema enforcement

---

## Installation

### Prerequisites

- Node.js 18.0 or higher
- npm, yarn, or pnpm package manager

### Install via npm

```bash
npm install dataagent
```

### Install via yarn

```bash
yarn add dataagent
```

### Install via pnpm

```bash
pnpm add dataagent
```

### Install from source

```bash
git clone https://github.com/yourusername/dataagent.git
cd dataagent
npm install
npm run build
```

### Browser Installation

You can also use DataAgent directly in the browser via CDN:

```html
<script type="module">
  import { DataAnalyzer } from 'https://cdn.jsdelivr.net/npm/dataagent/dist/index.js';
</script>
```

---

## Quick Start

```typescript
import { DataAnalyzer } from 'dataagent';

// Create a new analyzer instance
const analyzer = new DataAnalyzer();

// Analyze a CSV dataset
const result = analyzer.analyze('path/to/data.csv');

// View basic information
console.log(`Rows: ${result.rows}`);
console.log(`Columns: ${result.columns}`);
console.log(`Insights: ${result.insights}`);

// Generate a visualization
const chart = analyzer.visualize(result);
console.log(`Chart URL: ${chart}`);
```

---

## Usage Examples

### Example 1: Basic CSV Analysis

```typescript
import { DataAnalyzer } from 'dataagent';

const analyzer = new DataAnalyzer();

// Load and analyze a CSV file
const csvData = `
name,age,salary,department
Alice,28,75000,Engineering
Bob,35,85000,Marketing
Carol,42,95000,Engineering
David,31,70000,Sales
Eve,29,72000,Marketing
`;

const result = analyzer.analyze(csvData);

console.log('=== Analysis Results ===');
console.log(`Total Rows: ${result.rows}`);
console.log(`Total Columns: ${result.columns}`);
console.log(`Columns Found: ${result.columnsList.join(', ')}`);
console.log('Statistical Insights:', result.insights);
```

**Output:**
```
=== Analysis Results ===
Total Rows: 5
Total Columns: 4
Columns Found: name, age, salary, department
Statistical Insights: [
  { column: 'age', mean: 33, median: 31, stdDev: 5.1 },
  { column: 'salary', mean: 79400, median: 75000, stdDev: 9871 }
]
```

### Example 2: JSON Data Analysis

```typescript
import { DataAnalyzer } from 'dataagent';

const analyzer = new DataAnalyzer();

// Analyze JSON data
const jsonData = [
  { product: 'Laptop', price: 999, rating: 4.5, reviews: 1500 },
  { product: 'Smartphone', price: 699, rating: 4.3, reviews: 2300 },
  { product: 'Tablet', price: 449, rating: 4.1, reviews: 890 },
  { product: 'Watch', price: 299, rating: 4.7, reviews: 3200 },
  { product: 'Headphones', price: 149, rating: 4.2, reviews: 4100 },
];

const result = analyzer.analyze(JSON.stringify(jsonData));

console.log('=== Product Analysis ===');
console.log(`Products Analyzed: ${result.rows}`);
console.log(`Average Price: $${result.statistics.price.mean}`);
console.log(`Average Rating: ${result.statistics.rating.mean.toFixed(2)}`);
console.log(`Price Range: $${result.statistics.price.min} - $${result.statistics.price.max}`);
```

### Example 3: Generating Visualizations

```typescript
import { DataAnalyzer } from 'dataagent';

const analyzer = new DataAnalyzer();

// Analyze data and generate charts
const salesData = `
month,sales,expenses
January,15000,12000
February,18000,13000
March,22000,15000
April,19000,14000
May,25000,16000
June,28000,17000
`;

const result = analyzer.analyze(salesData);

// Generate different chart types
const barChart = analyzer.visualize(result, { type: 'bar', column: 'sales' });
const lineChart = analyzer.visualize(result, { type: 'line', columns: ['sales', 'expenses'] });
const histogram = analyzer.visualize(result, { type: 'histogram', column: 'sales' });

console.log('Bar Chart URL:', barChart);
console.log('Line Chart URL:', lineChart);
console.log('Histogram URL:', histogram);
```

### Example 4: Statistical Analysis

```typescript
import { DataAnalyzer, Statistics } from 'dataagent';

const data = `
value
10
15
20
25
30
35
40
45
50
`;

const analyzer = new DataAnalyzer();
const result = analyzer.analyze(data);

// Access detailed statistics
const stats = result.statistics.value;

console.log('=== Statistical Summary ===');
console.log(`Count: ${stats.count}`);
console.log(`Sum: ${stats.sum}`);
console.log(`Mean: ${stats.mean}`);
console.log(`Median: ${stats.median}`);
console.log(`Mode: ${stats.mode}`);
console.log(`Standard Deviation: ${stats.stdDev}`);
console.log(`Variance: ${stats.variance}`);
console.log(`Min: ${stats.min}`);
console.log(`Max: ${stats.max}`);
console.log(`Range: ${stats.range}`);
console.log(`25th Percentile: ${stats.percentiles.p25}`);
console.log(`50th Percentile: ${stats.percentiles.p50}`);
console.log(`75th Percentile: ${stats.percentiles.p75}`);
console.log(`95th Percentile: ${stats.percentiles.p95}`);
```

### Example 5: Data Transformation

```typescript
import { DataAnalyzer, DataTransformer } from 'dataagent';

const employeeData = `
id,name,department,salary,years
1,Alice,Engineering,85000,5
2,Bob,Marketing,72000,3
3,Carol,Engineering,92000,8
4,David,Sales,68000,2
5,Eve,Engineering,78000,4
`;

const transformer = new DataTransformer(employeeData);

// Filter employees with salary > 70000
const highEarners = transformer.filter(row => row.salary > 70000);
console.log('High Earners:', highEarners.length);

// Group by department
const byDepartment = transformer.groupBy('department');
console.log('Departments:', Object.keys(byDepartment));

// Sort by salary descending
const sorted = transformer.sortBy('salary', 'desc');
console.log('Top Paid:', sorted[0].name);

// Select specific columns
const namesOnly = transformer.select(['name', 'department']);
console.log('Names:', namesOnly);
```

### Example 6: Command Line Usage

```bash
# Analyze a CSV file
dataagent analyze data.csv

# Generate a chart
dataagent visualize data.csv --type bar --output chart.png

# Get statistics summary
dataagent stats data.csv --columns salary,age

# Transform data
dataagent transform data.csv --filter "salary > 50000" --sort salary --output filtered.csv
```

---

## API Reference

### DataAnalyzer Class

#### Constructor

```typescript
new DataAnalyzer(options?: AnalyzerOptions)
```

**Parameters:**
| Parameter | Type | Description | Default |
|-----------|------|-------------|---------|
| `options.delimiter` | `string` | CSV delimiter character | `,` |
| `options.hasHeader` | `boolean` | Whether CSV has header row | `true` |
| `options.skipEmpty` | `boolean` | Skip empty rows | `true` |
| `options.inferTypes` | `boolean` | Auto-detect column types | `true` |
| `options.decimalSeparator` | `string` | Decimal separator | `.` |

#### Methods

##### `analyze(data: string): AnalysisResult`

Analyzes the provided CSV or JSON data and returns comprehensive results.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `data` | `string` | CSV or JSON string to analyze |

**Returns:** `AnalysisResult`

```typescript
interface AnalysisResult {
  rows: number;           // Number of data rows
  columns: number;       // Number of columns
  columnsList: string[]; // List of column names
  data: Record<string, any>[]; // Parsed data as objects
  statistics: {          // Per-column statistics
    [columnName: string]: ColumnStatistics;
  };
  insights: Insight[];   // Generated insights
  types: {               // Inferred column types
    [columnName: string]: 'string' | 'number' | 'boolean' | 'date';
  };
}
```

##### `visualize(data: AnalysisResult, options?: VisualizationOptions): string`

Generates a visualization URL for the analyzed data.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `data` | `AnalysisResult` | Result from `analyze()` |
| `options.type` | `'bar' \| 'line' \| 'scatter' \| 'histogram' \| 'pie'` | Chart type |
| `options.column` | `string` | Column to visualize |
| `options.columns` | `string[]` | Multiple columns |
| `options.title` | `string` | Chart title |

**Returns:** `string` - Chart URL

##### `export(data: AnalysisResult, format: 'csv' | 'json', options?: ExportOptions): string`

Exports analyzed data to specified format.

**Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `data` | `AnalysisResult` | Data to export |
| `format` | `'csv' \| 'json'` | Export format |
| `options.includeStats` | `boolean` | Include statistics | `false` |
| `options.pretty` | `boolean` | Pretty print JSON | `false` |

### DataTransformer Class

#### Constructor

```typescript
new DataTransformer(data: string | Record<string, any>[])
```

#### Methods

##### `filter(predicate: (row: Row) => boolean): Row[]`

Filters rows based on a predicate function.

##### `sortBy(column: string, direction: 'asc' | 'desc'): Row[]`

Sorts data by specified column.

##### `groupBy(column: string): Record<string, Row[]>`

Groups data by column value.

##### `select(columns: string[]): Row[]`

Selects only specified columns.

##### `limit(count: number): Row[]`

Limits results to specified count.

##### `aggregate(column: string, operation: 'sum' | 'avg' | 'min' | 'max' | 'count'): number`

Computes aggregate value for a column.

##### `pivot(rowKey: string, columnKey: string, valueKey: string): PivotResult`

Creates a pivot table.

### Statistics Module

```typescript
import { Statistics } from 'dataagent';

// Compute statistics for an array of numbers
const numbers = [10, 20, 30, 40, 50];
const stats = Statistics.compute(numbers);

// Individual statistical functions
Statistics.mean(numbers);      // 30
Statistics.median(numbers);    // 30
Statistics.mode(numbers);      // [10, 20, 30, 40, 50] (no mode)
Statistics.stdDev(numbers);    // 14.142...
Statistics.variance(numbers);  // 200
Statistics.percentile(numbers, 75); // 40
Statistics.correlation(x, y);  // correlation coefficient
```

### ColumnStatistics Interface

```typescript
interface ColumnStatistics {
  count: number;           // Non-null value count
  nullCount: number;       // Null/missing value count
  uniqueCount: number;     // Unique values count
  sum: number;             // Sum (numbers only)
  mean: number;            // Arithmetic mean
  median: number;          // Median value
  mode: number | string;   // Most frequent value
  stdDev: number;           // Standard deviation
  variance: number;        // Variance
  min: number | string;    // Minimum value
  max: number | string;    // Maximum value
  range: number;           // Max - Min
  percentiles: {
    p5: number;
    p25: number;
    p50: number;
    p75: number;
    p95: number;
  };
}
```

---

## Configuration

### Analyzer Configuration

```typescript
const analyzer = new DataAnalyzer({
  delimiter: ';',           // Use semicolon as CSV delimiter
  hasHeader: true,          // First row is header
  skipEmpty: true,          // Skip empty rows
  inferTypes: true,         // Auto-detect column types
  decimalSeparator: '.',    // Use dot for decimals
  dateFormat: 'YYYY-MM-DD', // Expected date format
  nullValues: ['NA', 'N/A', ''], // Values to treat as null
});
```

### Visualization Configuration

```typescript
const chart = analyzer.visualize(result, {
  type: 'bar',
  column: 'sales',
  title: 'Monthly Sales Report',
  width: 800,
  height: 600,
  colors: ['#3498db', '#2ecc71', '#e74c3c'],
  showLegend: true,
  showGrid: true,
  animation: true,
});
```

---

## Advanced Usage

### Handling Large Files with Streaming

```typescript
import { DataAnalyzer, DataStream } from 'dataagent';

const stream = new DataStream('large_file.csv');

stream.on('chunk', (rows) => {
  // Process each chunk
  console.log(`Processing ${rows.length} rows`);
});

stream.on('complete', (result) => {
  console.log('Analysis complete:', result.rows);
});

stream.start();
```

### Custom Data Validation

```typescript
import { DataAnalyzer, Validator } from 'dataagent';

const schema = {
  email: { type: 'string', pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/ },
  age: { type: 'number', min: 0, max: 150 },
  name: { type: 'string', required: true },
};

const validator = new Validator(schema);
const result = validator.validate(data);

if (!result.valid) {
  console.log('Validation errors:', result.errors);
}
```

### Correlation Analysis

```typescript
import { DataAnalyzer, Correlation } from 'dataagent';

const analyzer = new DataAnalyzer();
const result = analyzer.analyze(data);

// Compute correlation matrix
const correlationMatrix = Correlation.matrix(result.data, [
  'age', 'salary', 'experience', 'satisfaction'
]);

console.log('Correlation between age and salary:', correlationMatrix.age.salary);
```

### Data Cleaning Pipeline

```typescript
import { DataAnalyzer, DataCleaner } from 'dataagent';

const cleaner = new DataCleaner(data);

// Chain cleaning operations
const cleaned = cleaner
  .removeDuplicates()
  .fillMissing('age', { strategy: 'median' })
  .removeOutliers('salary', { method: 'iqr', threshold: 1.5 })
  .normalize('price', { method: 'minmax' })
  .trimStrings()
  .dedupe()
  .getResult();
```

---

## Error Handling

### Try-Catch Pattern

```typescript
import { DataAnalyzer } from 'dataagent';

const analyzer = new DataAnalyzer();

try {
  const result = analyzer.analyze(data);
  console.log('Success:', result);
} catch (error) {
  if (error instanceof ParseError) {
    console.error('Parse error:', error.message);
    console.error('Line:', error.line);
    console.error('Column:', error.column);
  } else if (error instanceof ValidationError) {
    console.error('Validation error:', error.details);
  } else {
    console.error('Unexpected error:', error);
  }
}
```

### Error Types

| Error Type | Description |
|------------|-------------|
| `ParseError` | CSV/JSON parsing failed |
| `ValidationError` | Data validation failed |
| `TypeError` | Invalid data types |
| `RangeError` | Value out of expected range |
| `EmptyDataError` | No data to analyze |

---

## Performance Tips

### Optimizing Large Dataset Processing

```typescript
// 1. Use streaming for large files
const stream = new DataStream('large.csv');
stream.pipe(process.stdout);

// 2. Limit columns if not all are needed
const result = analyzer.analyze(data, { columns: ['id', 'name', 'value'] });

// 3. Disable statistics if not needed
const result = analyzer.analyze(data, { computeStats: false });

// 4. Use sampling for quick insights
const sample = DataSampler.random(data, { size: 1000 });
const result = analyzer.analyze(sample);
```

### Memory Management

```typescript
// Process in chunks to manage memory
const processor = new ChunkProcessor({
  chunkSize: 10000,
  onChunk: (chunk) => {
    // Process chunk immediately
    saveToDatabase(chunk);
    // Chunk is then garbage collected
  }
});

processor.process(largeDataset);
```

---

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting a pull request.

### Development Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/dataagent.git
cd dataagent

# Install dependencies
npm install

# Run tests
npm test

# Build for production
npm run build

# Lint code
npm run lint
```

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm test -- --grep "analyze"
```

### Submitting Changes

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 DataAgent Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Support

- 📖 Documentation: [docs.dataagent.io](https://docs.dataagent.io)
- 💬 Discord: [Join our community](https://discord.gg/dataagent)
- 🐛 Issues: [GitHub Issues](https://github.com/yourusername/dataagent/issues)
- 📧 Email: support@dataagent.io

---

<p align="center">
  Made with ❤️ by the DataAgent Team
</p>
