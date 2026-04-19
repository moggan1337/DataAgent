# DataAgent 📊

**Data Analysis** - CSV/JSON, statistics, charts.

## Features

- **📄 CSV/JSON** - Load and parse
- **📈 Stats** - Statistical analysis
- **📊 Charts** - Generate charts

## Installation

```bash
npm install dataagent
```

## Usage

```typescript
import { DataAnalyzer } from 'dataagent';

const analyzer = new DataAnalyzer();

const result = analyzer.analyze('data.csv');
console.log(result.rows);    // Number of rows
console.log(result.columns); // Number of columns
console.log(result.insights); // Statistical insights

const chart = analyzer.visualize(result);
console.log(chart); // 'chart://...'
```

## License

MIT
