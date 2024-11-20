**SnowPro Core Certification Exam**. 

---

### **Introduction to Snowflake and Exam Overview**
- Introduction to Snowflake and its relevance for **SnowPro Core Certification**.
- Overview of Snowflake’s **hybrid architecture** combining shared-disk and shared-nothing approaches.

---

### **Snowflake Architecture Overview**
1. **Three Main Layers**:
   - **Data Storage Layer**:
     - Data is stored in optimized, compressed formats in cloud object storage (AWS S3, Azure Blob, GCP storage).
     - Separation of storage and compute, enabling independent scalability.
   - **Compute Layer (Virtual Warehouses)**:
     - Provides compute power for tasks like data loading, query execution, ML model training, etc.
     - Offers T-shirt sizes (e.g., X-Small, Small, Medium, Large, 6X-Large).
     - Supports **vertical scaling** (e.g., Medium → Large) and **horizontal scaling** (multi-cluster warehouses for concurrency).
     - Key features: Auto-suspend, Auto-resume, and per-second billing after an initial 60-second charge.
   - **Cloud Services Layer**:
     - The "brain" of Snowflake.
     - Handles metadata management, query optimization, security, and infrastructure management.
     - Includes caching mechanisms like **metadata cache** (for query optimization) and **result cache** (for reusing query results within 24 hours).

---

### **Caching in Snowflake**
- **Result Cache**:
  - Stores query results for 24 hours.
  - Avoids compute layer costs for identical queries within the caching window.
- **Metadata Cache**:
  - Stores data statistics for query optimization.
- **Warehouse Cache**:
  - Associated with active virtual warehouses but clears once the warehouse is suspended.

---

### **Virtual Warehouse Billing**
- **Per-second billing**:
  - Based on the size and runtime of the warehouse.
  - Minimum charge of 60 seconds even for short-lived queries.
- **Cost factors**:
  - Number of virtual warehouses.
  - Runtime duration.
  - Warehouse size.

---

### **Connection Methods to Snowflake**
1. **Web UI**:
   - Default user interface for managing Snowflake resources.
   - Includes **SnowSite** for advanced features like data visualization and monitoring.
2. **Programmatic Interfaces**:
   - **SnowSQL** (CLI for query execution and scripting).
   - **ODBC/JDBC** (for integration with tools like Tableau, Power BI).
   - **Native Connectors** for Python and Spark.
3. **Third-party Tools**:
   - Integration with platforms like Informatica, ThoughtSpot, and others.

---

### **Exam Preparation and Future Content**
- Upcoming videos in the series will cover:
  - Detailed architecture insights.
  - Query optimization techniques.
  - Hands-on guidance for the SnowPro Core Certification.

---
