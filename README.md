# Departmental Store Database Application

## Overview
This project is a high-performance, multi-threaded departmental store database application developed as part of the CS315 course. Built using Python and Oracle Database, it leverages the `oracledb` module with a configurable connection pool (50–100 connections) to simulate realistic workloads. The application supports customer creation, order placement with randomized item generation, updates, deletions, and summary queries, while ensuring ACID compliance. It includes detailed logging, tracing, and monitoring for operational metrics, deadlock detection, and performance profiling.

For a comprehensive understanding, refer to the [project report]([link-to-report-placeholder](https://python-oracledb.readthedocs.io/en/latest/index.html)).

## Features
- **Concurrent Transaction Handling**: Scales to 50–100 pooled connections with multiple worker threads.
- **ACID Compliance**: Ensures transactional integrity with commit/rollback mechanisms.
- **Layered Architecture**:
  - Database Layer (`db.py`): Manages Oracle connectivity and monitoring.
  - Business Logic Layer (`action.py`): Implements CRUD operations for `CUSTOMERS`, `ORDERS`, and `ITEMS`.
  - Logging/Tracing Layer (`logger_tracer.py`): Dual logging for summary and detailed SQL traces.
  - Workload Management Layer (`main.py`): Dispatches weighted transactions with periodic snapshots.
- **Error Handling**: Robust handling of database errors (e.g., deadlocks, duplicates).
- **Monitoring**: Real-time visibility into pool utilization, session activity, and lock contention.

## Prerequisites
- **Python 3.8+**
- **Oracle Database**: Access to an Oracle Database instance (local or remote).
- **Python Libraries**:
  - `oracledb`: For Oracle Database connectivity.
  - `tabulate`: For formatting trace logs.
  - Install dependencies using:
    ```bash
    pip install oracledb tabulate
    ```
- **Oracle Client Libraries**: Required for `oracledb`. Follow the [oracledb installation guide](https://python-oracledb.readthedocs.io/en/latest/user_guide/installation.html).

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/JainSajal23/CS315.git
   cd CS315/main
   ```
2. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```
   If `requirements.txt` is not present, manually install the prerequisites listed above.

## Configuration
The application uses a `db.config` file to manage settings. Edit `db.config` with your Oracle Database credentials and desired parameters:
- **Database Connection Pool Settings** (`[pool]`):
  - `ISPool=True`
  - `user`, `password`, `dsn`: Your Oracle Database credentials.
  - `min=50`, `max=100`, `increment=10`, `timeout=15`
- **Transaction Execution Settings** (`[transactions]`):
  - `doThreading=True`
  - `num_threads=10`
  - `iterations=100` or `duration_mins=0`
- **Test Case Weight Settings** (`[test_cases]`): Assign weights to prioritize test cases (e.g., `orders_ofcust_customdate=1`).
- **Logging and Tracing Settings** (`[address]`, `[log_file_handle]`, `[trace_file_handle]`):
  - `log_file_direc`: Directory for log files.
  - `log_level=10`, `trace_format`

Example `db.config` snippet:
```
[pool]
ISPool=True
user=scott
password=tiger
dsn=localhost:1521/orcl
min=50
max=100
increment=10
timeout=15

[transactions]
doThreading=True
num_threads=10
iterations=100
duration_mins=0
```

## Usage
1. Ensure your Oracle Database instance is running and accessible.
2. Configure `db.config` with your settings.
3. Run the application:
   ```bash
   python main.py
   ```
4. Monitor logs and traces in the specified directories for operational metrics and debugging.

## Project Structure
- `db.py`: Database connectivity and monitoring.
- `action.py`: Business logic for CRUD operations.
- `logger_tracer.py`: Logging and tracing functionality.
- `main.py`: Workload orchestration and threading.
- `db.config`: Configuration file for database and runtime settings.

## Results
The system successfully handles concurrent transactions for a 1-minute duration, with logs capturing successes, errors, session activity, and lock conditions. Detailed results are available in the project report.

## Contributors
- **Sajal Jain**
- **Siddhant Singhai**
- **Akshat Mehta**
- **Abhishek Choudhary**
- **Aryan Thada**
## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
