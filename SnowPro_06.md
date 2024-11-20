 1. **User-Defined Functions (UDFs)**:
   - **Definition**: UDFs allow you to define custom functions to enhance SQL functionality. They encapsulate logic that can be reused within SQL queries.
   - **Types**:
     - **Scalar UDF**: Returns a single value per input row. Example: A Python function that adds 1 to an input integer.
     - **Table UDF (UDTF)**: Returns a table, and each row in the input produces multiple rows in the output.
   - **Supported Languages**: Java, JavaScript, Python, Scala, and Snowflake scripting for UDFs.

2. **External Functions**:
   - **Definition**: External functions are executed outside of Snowflake, typically using cloud services like AWS Lambda, Azure Functions, or GCP Functions.
   - **Architecture**: Snowflake communicates with the remote service through an **HTTPS Proxy Service** and integrates security via an **API Integration**.
   - **Limitations**: 
     - Must be scalar functions (return a single value).
     - Response size is limited to 10MB.
     - Cannot be shared through Snowflake’s data-sharing mechanism.
   - **Languages Supported**: In addition to typical UDF languages, external functions also support Go and Shell scripting.
   
3. **Stored Procedures**:
   - **Definition**: Stored procedures encapsulate SQL logic to perform operations like DML (insert, update, delete) or administrative tasks. They can execute multiple SQL statements dynamically.
   - **Languages Supported**: Java, Python, Scala (via Snowpark API), JavaScript, and SQL using Snowflake scripting.
   - **Usage**: Stored procedures are used for tasks requiring multiple SQL statements or DDL/DML operations. They do not necessarily return a value, unlike UDFs, which always return a value.
   - **Example**: A stored procedure that reads data from one table and inserts it into another.
   
4. **Difference Between Stored Procedures and UDFs**:
   - **UDFs**: Return a value and can be part of a SQL statement. They cannot perform DDL/DML operations.
   - **Stored Procedures**: Do not always return a value and are used for administrative tasks or complex operations involving multiple SQL statements.

5. **Documentation**:
   - The Snowflake documentation provides details on UDFs, external functions, and stored procedures, including supported languages, creation guidelines, and differences between UDFs and stored procedures.
