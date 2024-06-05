---
Title: DBS101 Flipped Class 12
categories: [DBS101, Flipped_Class12]
tags: [DBS101]
---

# Topic :  Recovery System
----

In DBMS, Database recovery is a critical component of any robust database management system (DBMS), ensuring that data remains consistent and reliable even in the face of system failures or crashes. One of the most widely adopted algorithms for database recovery is the Algorithm for Recovery and Isolation Exploiting Semantics (ARIES), which is based on the Write-Ahead Logging (WAL) protocol

## Algorithm for Recovery and Isolation Exploiting Semantics (ARIES)

ARIES is designed to provide efficient and reliable recovery, leveraging the information stored in the log records. Let's dive into the key aspects of the ARIES algorithm:

1. Log Records:

- ARIES utilizes three types of log records: undo-only, redo-only, and undo-redo.
- Undo-only log records store the before-image of the data, allowing for undo operations to retrieve the old data.
- Redo-only log records store the after-image of the data, enabling redo operations to reapply the changes.
- Undo-redo log records contain both the before-image and the after-image, providing the necessary information for both undo and redo operations.

2. Log Sequence Number (LSN):

- Each log record is assigned a unique and monotonically increasing Log Sequence Number (LSN).
- Every data page in the DBMS has a page LSN field that stores the LSN of the last update made to that page.
- The WAL protocol ensures that the log record corresponding to an update is written to stable storage before the updated data page is written to disk.

3. Checkpointing:

- ARIES periodically writes a checkpoint record to the log, containing the transaction table and the dirty page table.
- A master log record is maintained separately in stable storage, storing the LSN of the latest checkpoint record.
- On restart, the recovery subsystem reads the master log record to find the checkpoint's LSN, reads the checkpoint record, and starts the recovery process from there.

4. Recovery Process:
The ARIES recovery process consists of three phases:

1. **Analysis Phase:**

- The recovery subsystem determines the earliest log record from which the next pass must start.
- It scans the log forward from the checkpoint record to construct a snapshot of the system's state at the time of the crash.

2. **Redo Phase:**
- Starting from the earliest LSN, the log is read forward, and each update is reapplied (redone).

3. **Undo Phase:**
- The log is scanned backward, and updates corresponding to "loser" transactions (those that did not commit) are undone.

### Advantages
The ARIES algorithm's strength lies in its efficient and robust approach to database recovery:
- It leverages the information stored in the log records to effectively restore the database to a consistent state, even in the face of system failures or crashes.
- The checkpoint mechanism and the master log record provide a reliable way to minimize the time and resources required for the recovery process.

## Shadow Paging
Shadow Paging is a recovery technique used in database management systems to recover the database after a system failure or crash. It is based on the concept of "Cut-off-Place" updating, where updates are made to a separate, shadowed copy of the database pages instead of the actual database.

![alt text](<../shadow paging 12.png>)

### Key Aspects of Shadow Paging
1. Page-based Database Structure:

- The database is considered to be composed of fixed-size logical units of storage called pages.
- These pages are mapped to physical blocks of storage using a page table.

2. Dual Page Tables:

- The system maintains two page tables: the Current Page Table and the Shadow Page Table.
- The Current Page Table is used to point to the most recent versions of the database pages on disk.
- The Shadow Page Table is a copy of the Current Page Table, made at the start of a transaction.

3. Transaction Execution:

- When a transaction starts, the system creates a copy of the Current Page Table, called the Shadow Page Table.
- During the transaction, updates are made to the database pages, and the Current Page Table is modified accordingly.
- The Shadow Page Table remains unchanged throughout the transaction.
Commit Operation:

4. To commit a transaction, the system:
- Writes all modified pages from the buffers to the actual database.
- Writes the Current Page Table to disk, overwriting the address of the old Shadow Page Table.
- At this point, the Current Page Table and the Shadow Page Table become identical.

5. Recovery:

- In the event of a system failure or crash, the recovery process is straightforward:
- If the crash occurs before the commit operation, the system can simply discard the Current Page Table and restore the database using the Shadow Page Table.
- If the crash occurs after the commit operation, the system can simply restore the database using the Current Page Table.

### Advantages of Shadow Paging
- Fewer disk accesses required for operations
- Faster and less expensive recovery process
- No need for undo or redo operations
Improved fault tolerance and concurrency

### Disadvantages of Shadow Paging
- Difficulty in maintaining locality of related pages on disk
- Overhead in managing the free space and garbage collection
- Performance overhead due to copying changes back to the actual database
- Limited concurrency control and potential for data fragmentation
- Complexity in implementing for some systems with complex data structures

The Shadow Paging recovery technique provides a simple and efficient way to maintain data consistency and recover the database in the event of a system failure or crash. However, it also has some limitations, and the decision to use it should be based on the specific requirements and characteristics of the database system.

## Database Logging
Database logging is a critical component of a highly available database solution. Logs keep records of database changes, allowing the database to be recovered and restored in the event of a failure.

### Types of Database Logging
There are two main types of database logging:

1. Circular Logging:

- Circular logging is the default behavior when a new database is created.
- In circular logging, the log files are reused, overwriting old log records.
- This means that you can only recover the database to the point of the last backup, as changes after the backup are lost.

2. Archive Logging:

- Archive logging is used specifically for rollforward recovery.
- Archived log files are copied from the current log path or mirror log path to another location.
- This allows the database to be restored to a specific point in time, using the archived logs in addition to the active logs.

The key advantage of archive logging is the ability to perform more granular, point-in-time recovery, as the archived logs can be used to recover changes made after the last backup.

### Advanced Log Space Management (ALSM)
When running Db2 11.5.4 and later, you can use Advanced Log Space Management (ALSM) to reduce the likelihood of encountering transaction log full conditions.

ALSM is enabled by setting the DB2_ADVANCED_LOG_SPACE_MGMT registry variable to ON.

### Log Control Files
When a database restarts after a failure, the database manager uses information recorded in log control files to determine which records from the log files need to be applied to the database to return it to a consistent state.

The log control files contain metadata about the log files, such as the Log Sequence Numbers (LSNs) and other information required for the recovery process.

### Key Considerations
- Choose archive logging over circular logging to enable more granular, point-in-time recovery.
- Implement Advanced Log Space Management (ALSM) to proactively manage the log space and reduce the risk of transaction log full conditions.
- Ensure the log control files are properly maintained and accessible to the database manager during the recovery process.

Proper management and configuration of database logging is crucial for ensuring the availability and recoverability of your database system, especially in the face of failures or unexpected events.