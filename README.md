# DLT StreamForge

A Python-based data generation tool for creating realistic streaming data pipelines with Databricks Delta Live Tables (DLT). This tool generates dimension, fact, and change feed tables with configurable schemas and data quality rules.

## Features

- **Multiple Table Types**:
  - Dimension tables with configurable key ranges
  - Fact tables with foreign key relationships
  - Change feed tables with SCD Type 2 support
  - Support for multiple industries (Retail, Energy, etc.)

- **Data Quality Rules**:
  - Configurable min/max values for numeric columns
  - Anomaly percentage to generate out-of-range values
  - Automatic data quality rule application during generation
  - Support for both normal and anomalous data patterns

- **DLT Pipeline Generation**:
  - Automatic DLT code generation in SQL and Python
  - Support for streaming tables and views
  - SCD Type 2 implementation for change feeds
  - Exportable as Jupyter notebooks

## Prerequisites

- Python 3.8+
- Databricks CLI configured (for Databricks deployment)
- Required Python packages (see requirements.txt)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/dlt-streamforge.git
cd dlt-streamforge
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

1. **Configure Schema**:
   - Place your schema YAML files in the `schema/{industry}` directory
   - Define tables, columns, and data quality rules
   - Example schema structure:
   ```yaml
   table: energy_consumption
   type: fact
   num_rows: 1000
   columns:
     plant_id:
       type: int
     consumption_value:
       type: float
   data_quality_rules:
     consumption_value:
       min_value: 0
       max_value: 1000
       anomaly_percentage: 0.05  # 5% of values will be outside range
   ```

2. **Run the Application**:
   ```bash
   python app.py
   ```

3. **Generate Data**:
   - Select your industry
   - Choose output language (SQL/Python)
   - Enter an empty output path (directory must be empty)
   - Click "Start" to begin generation

## Schema Configuration

### Table Types

1. **Dimension Tables**:
   ```yaml
   table: equipment
   type: dimension
   num_rows: 500
   columns:
     equipment_id:
       type: int
     equipment_name:
       type: string
   ```

2. **Fact Tables**:
   ```yaml
   table: energy_consumption
   type: fact
   num_rows: 1000
   columns:
     plant_id:
       type: int
     consumption_value:
       type: float
   data_quality_rules:
     consumption_value:
       min_value: 0
       max_value: 1000
       anomaly_percentage: 0.05
   ```

3. **Change Feed Tables**:
   ```yaml
   table: customer_changes
   type: change_feed
   num_rows: 100
   columns:
     key:
       type: string
     change_timestamp:
       type: datetime
   change_feed_rules:
     dlt_config:
       keys: ["key"]
       sequence_by: "change_timestamp"
   ```

### Data Quality Rules

Data quality rules can be defined for any column in your schema:

```yaml
data_quality_rules:
  column_name:
    min_value: 0        # Minimum allowed value
    max_value: 1000     # Maximum allowed value
    anomaly_percentage: 0.05  # Percentage of values that will be outside range
```

## Output

The tool generates:
1. CSV files for each table
2. DLT pipeline code in SQL and Python
3. Jupyter notebook with complete pipeline code

## Deployment

### Local Development
- Run `python app.py`
- Access the UI at `http://localhost:8050`

### Databricks Deployment
1. Configure Databricks CLI
2. Deploy to Databricks workspace
3. Access through Databricks URL

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
