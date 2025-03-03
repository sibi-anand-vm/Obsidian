### **Transactions in DBMS: A Deep Dive**

A **transaction** is a sequence of operations performed as a single logical unit of work in a database. Transactions ensure data integrity and consistency, especially in multi-user environments. Let’s dive into the details of transactions, including their properties, states, and management.

---

### **1. What is a Transaction?**

A transaction is a set of operations (e.g., **INSERT**, **UPDATE**, **DELETE**) that are executed as a single unit. It ensures that either all operations are completed successfully, or none are.

#### **Example: Bank Transfer**

- Transfer $100 from Account A to Account B.
    
- Operations:
    
    1. **Deduct $100 from Account A.**
        
    2. **Add $100 to Account B.**
        

Both operations must succeed or fail together. If one operation fails, the entire transaction is rolled back.

---

### **2. ACID Properties of Transactions**

Transactions in DBMS follow the **ACID** properties to ensure reliability and consistency:

#### **A. Atomicity**

- A transaction is treated as a single unit.
    
- Either all operations in the transaction are completed, or none are.
    
- If any operation fails, the entire transaction is rolled back.
    

#### **B. Consistency**

- A transaction brings the database from one valid state to another.
    
- All constraints (e.g., primary keys, foreign keys) must be satisfied before and after the transaction.
    

#### **C. Isolation**

- Concurrent transactions do not interfere with each other.
    
- Each transaction is executed in isolation, as if it were the only one running.
    

#### **D. Durability**

- Once a transaction is committed, its changes are permanent, even in the event of a system failure.
    

---

### **3. States of a Transaction**

A transaction goes through several states during its lifecycle:

1. **Active**:
    
    - The transaction is being executed.
        
    - Operations like **INSERT**, **UPDATE**, or **DELETE** are performed.
        
2. **Partially Committed**:
    
    - All operations are executed, but changes are not yet saved to the database.
        
3. **Committed**:
    
    - Changes are permanently saved to the database.
        
    - The transaction is successfully completed.
        
4. **Failed**:
    
    - The transaction cannot proceed due to an error (e.g., constraint violation, system crash).
        
5. **Aborted**:
    
    - The transaction is rolled back, and the database is restored to its state before the transaction started.
        
6. **Terminated**:
    
    - The transaction is either committed or aborted and is no longer active.
### **Concurrency Control**

In a multi-user environment, multiple transactions may execute simultaneously. Concurrency control ensures that transactions do not interfere with each other.

#### **A. Problems Due to Concurrency**

1. **Dirty Read**:
    
    - A transaction reads uncommitted data from another transaction.
        
2. **Non-Repeatable Read**:
    
    - A transaction reads the same data twice, but the values differ due to another transaction’s update.
        
3. **Phantom Read**:
    
    - A transaction reads a set of rows twice, but the number of rows differs due to another transaction’s insert or delete.
        

#### **B. Isolation Levels**

To control concurrency, DBMS provides different isolation levels:

1. **Read Uncommitted**:
    
    - Allows dirty reads, non-repeatable reads, and phantom reads.
        
    - Lowest isolation level.
        
2. **Read Committed**:
    
    - Prevents dirty reads but allows non-repeatable reads and phantom reads.
        
3. **Repeatable Read**:
    
    - Prevents dirty reads and non-repeatable reads but allows phantom reads.
        
4. **Serializable**:
    
    - Prevents dirty reads, non-repeatable reads, and phantom reads.
        
    - Highest isolation level.