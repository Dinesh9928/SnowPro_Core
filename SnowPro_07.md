
### 1. **File Formats in Snowflake:**
   - Snowflake supports several file formats for loading and unloading data, including CSV, JSON, Parquet, ORC, AVRO, and XML.
   - **Supported for loading and unloading**: CSV, JSON, Parquet.
   - **Supported for loading only**: AVRO, ORC, XML.
   - File formats can be created using the Snowflake web UI or SQL commands, with various options like compression and handling of blank lines or headers.
   - When creating external tables, the schema of the file format must match the schema of the Snowflake table.
   - **Partitioning**: Supported for ORC, Parquet, and JSON formats.
   - Example SQL commands show how to create file formats and stages, followed by loading data into tables.

### 2. **Sequences in Snowflake:**
   - Sequences generate unique, incrementing numbers across sessions and statements, useful for primary keys.
   - Sequences in Snowflake may have gaps; they do not guarantee contiguous values.
   - Example: Creating and using a sequence to generate unique values. The sequence values can be customized (e.g., incrementing by 5).
   - Important: Sequence numbers may have gaps or non-contiguous values.

### 3. **Tasks in Snowflake:**
   - Tasks automate the execution of SQL statements at scheduled intervals (e.g., every 60 minutes).
   - **Serverless tasks**: Compute resources are managed by Snowflake.
   - **User-managed tasks**: Compute resources (like virtual warehouses) are specified by the user.
   - Tasks can be combined with streams for continuous data processing (e.g., change data capture).
   - Example SQL commands demonstrate how to create and schedule tasks with Snowflake's task management system.
   - Tasks can be grouped into **task graphs**, which define dependencies between tasks.

### 4. **Streams in Snowflake:**
   - Streams are used for change data capture (CDC), tracking changes to tables (e.g., inserts, updates, deletes).
   - A stream records changes made to a source table and provides metadata about the changes (e.g., action type, update status).
   - Snowflake supports different types of streams, including standard streams, which track all DML changes (inserts, updates, deletes).
   - Streams help with tracking changes in data over time, making them useful for data pipelines.

# SnowPro Core Certification Series: File Formats, Sequences, Streams, and Tasks in Snowflake

## Overview

This video covers:

*   File Formats
*   Sequences
*   Streams
*   Tasks

## File Formats

### Supported Formats

*   **Loading and Unloading**: CSV, JSON, Parquet
*   **Loading Only**: Avro, ORC, XML

### Creation Methods

*   **Snowflake Web UI (SnowSite)**
*   **SQL Commands**

### Options

*   Compression
*   Skip Header
*   Skip Blank Lines
*   Trim Spaces
*   Field Enclosure
*   Error on Column Count Mismatch

### Example

`CREATE FILE FORMAT my_csv_format TYPE = 'CSV' FIELD_DELIMITER = '|' SKIP_HEADER = 1;CREATE STAGE my_csv_stage FILE_FORMAT = my_csv_format;COPY INTO my_table FROM @my_csv_stage;`

## `Sequences`

### `Purpose`

*   `Generate unique, continuous values for primary keys.`

### `Characteristics`

*   `No guarantee of gapless sequence numbers.`
*   `Values can be generated across sessions and statements.`

### `Example`

``CREATE OR REPLACE SEQUENCE seq1 START = 1 INCREMENT = 1;SELECT seq1.nextval; -- Returns 1SELECT seq1.nextval; -- Returns 2INSERT INTO seq_test_table VALUES (seq1.nextval); -- Inserts 3``

## ``Tasks``

### ``Purpose``

*   ``Schedule SQL statements or stored procedures.``

### ``Types``

*   ``**Serverless Task**: Compute managed by Snowflake.``
*   ``**User-Managed Task**: User specifies the compute.``

### ``Example``

#### ``Serverless Task``

```CREATE TASK t1 SCHEDULE = '60 MINUTE' AS INSERT INTO my_table VALUES (CURRENT_TIMESTAMP);```

#### ```User-Managed Task```

````CREATE TASK t2 WAREHOUSE = mywh SCHEDULE = '5 MINUTE' AS INSERT INTO my_table VALUES (CURRENT_TIMESTAMP);````

### ```Workflow```

1.  ```**Create Task Admin Role**```
2.  ```**Create Task**```
3.  ```**Resume Task**```

### ```Task Graphs```

*   ```**DAG (Directed Acyclic Graph)**: Chain of dependent tasks.```
*   ```**Limitations**: Max 1,000 tasks, 100 predecessors, and 100 child tasks.```

### ```Example```

````CREATE TASK task5 AFTER task2, task3, task4 AS INSERT INTO my_table VALUES (CURRENT_TIMESTAMP);````

## ```Streams```

### ```Purpose```

*   ```Track changes (inserts, updates, deletes) in tables for change data capture (CDC).```

### ```Types```

*   ```**Standard Stream**: Tracks all DML changes.```
*   ```**Append-Only Stream**: Tracks only inserts.```
*   ```**Insert-Only Stream**: Tracks inserts, not deletes.```

### ```Example```

````CREATE STREAM my_stream ON TABLE my_table;SELECT * FROM my_stream;````

### ```Combining Tasks and Streams```

````CREATE TASK my_task WAREHOUSE = mywh SCHEDULE = '5 MINUTE' WHEN SYSTEM$STREAM_HAS_DATA('my_stream') AS INSERT INTO my_table1 SELECT * FROM my_stream WHERE metadata$action = 'INSERT';````

## ```Documentation Links```

*   ```**File Formats**: [Snowflake Documentation](https://docs.snowflake.com/en/user-guide/data-load-file-formats.html)```
*   ```**Sequences**: [Snowflake Documentation](https://docs.snowflake.com/en/sql-reference/sql/create-sequence.html)```
*   ```**Tasks**: [Snowflake Documentation](https://docs.snowflake.com/en/user-guide/tasks-intro.html)```
*   ```**Streams**: [Snowflake Documentation](https://docs.snowflake.com/en/user-guide/streams.html)```

## ```Summary Table```

<table>

<thead>

<tr>

<th>Feature</th>

<th>Purpose</th>

<th>Key Points</th>

<th>Example</th>

</tr>

</thead>

<tbody>

<tr>

<td>File Formats</td>

<td>Load/Unload data</td>

<td>Supported formats: CSV, JSON, Parquet, Avro, ORC, XML</td>

<td><span>CREATE FILE FORMAT my_csv_format TYPE = 'CSV';</span></td>

</tr>

<tr>

<td>Sequences</td>

<td>Generate unique values</td>

<td>No gapless guarantee, used for primary keys</td>

<td><span>CREATE SEQUENCE seq1 START = 1 INCREMENT = 1;</span></td>

</tr>

<tr>

<td>Tasks</td>

<td>Schedule SQL statements</td>

<td>Types: Serverless, User-Managed; Can create task graphs (DAG)</td>

<td><span>CREATE TASK t1 SCHEDULE = '60 MINUTE' AS INSERT INTO my_table;</span></td>

</tr>

<tr>

<td>Streams</td>

<td>Track table changes (CDC)</td>

<td>Types: Standard, Append-Only, Insert-Only</td>

<td><span>CREATE STREAM my_stream ON TABLE my_table;</span></td>

</tr>

</tbody>

</table>
