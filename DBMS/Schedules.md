### **🔹 Schedules in DBMS (With Detailed Examples)**

A **schedule** in DBMS is the **sequence of execution of transactions**, ensuring consistency in multi-user databases.

## **🔹 1. Serial Schedule**

- Transactions execute **one after another**, without overlapping.
- **Ensures consistency but is slow** due to lack of concurrency.

### **Example**

#### Transactions T1 & T2 (Updating Account Balance)

| **Step** | **T1: Withdraw ₹1000**            | **T2: Deposit ₹500** |
| -------- | --------------------------------- | -------------------- |
| 1        | `Read(balance)` = 5000            | -                    |
| 2        | `balance = balance - 1000` (4000) | -                    |
| 3        | `Write(balance = 4000)`           | -                    |
| 4        | `Read(balance)` = 4000            | -                    |
| 5        | `balance = balance + 500` (4500)  | -                    |
| 6        | `Write(balance = 4500)`           | -                    |

✅ **Result:** Final balance = ₹4500, no inconsistency.

---

## **🔹 2. Non-Serial Schedule**

- Transactions **overlap**, increasing concurrency but **may cause inconsistencies**.

### **Example**

| **Step** | **T1**                            | **T2**                             |
| -------- | --------------------------------- | ---------------------------------- |
| 1        | `Read(balance)` = 5000            | -                                  |
| 2        | -                                 | `Read(balance)` = 5000             |
| 3        | `balance = balance - 1000` (4000) | -                                  |
| 4        | -                                 | `balance = balance - 500` (4500 ❌) |
| 5        | `Write(balance = 4000)` ✅         | -                                  |
| 6        | -                                 | `Write(balance = 4500 ❌)`          |

🚨 **Issue:** Lost Update Problem – **T2 overwrites T1’s update**, causing **data inconsistency**.

✅ **Solution:** Use **Serializable Schedule or Two-Phase Locking (2PL)**.

---

## **🔹 3. Serializable Schedule**

A **non-serial** schedule that produces the **same result as a serial schedule**.

✅ **Ensures consistency while allowing concurrency.**

### **Example**

| **Step** | **T1**                            | **T2**                           |
| -------- | --------------------------------- | -------------------------------- |
| 1        | `Read(balance)` = 5000            | -                                |
| 2        | `balance = balance - 1000` (4000) | -                                |
| 3        | `Write(balance = 4000)`           | -                                |
| 4        | -                                 | `Read(balance)` = 4000           |
| 5        | -                                 | `balance = balance - 500` (3500) |
| 6        | -                                 | `Write(balance = 3500)`          |

✅ **Result:** Equivalent to **T1 → T2 execution**, so it is **serializable**.

---

## **🔹 4. Conflict-Serializable Schedule**

A **schedule is conflict-serializable** if transactions can be **rearranged into a serial order** by swapping **non-conflicting operations**.

#### **Conflicting Operations**

1️⃣ **Read-Write (RW Conflict)** – One transaction reads while another writes the same data.  
2️⃣ **Write-Read (WR Conflict)** – One transaction writes before another reads the same data.  
3️⃣ **Write-Write (WW Conflict)** – Two transactions write to the same data.

### **Example**

| **Step** | **T1**       | **T2**       |
| -------- | ------------ | ------------ |
| 1        | `Read(X)`    | -            |
| 2        | -            | `Write(X)` ❌ |
| 3        | `Write(X)` ❌ | -            |

🚨 **Issue:** T1 and T2 both write X → **Conflict detected**.

✅ **Fix:** Rearrange transactions to avoid conflicts.

---

## **🔹 5. View-Serializable Schedule**

A schedule is **view-serializable** if **initial reads and final writes match a serial schedule**.

✅ **Less strict than conflict-serializable but ensures consistency.**

### **Example**

| **Step** | **T1**    | **T2**     |
| -------- | --------- | ---------- |
| 1        | `Read(A)` | -          |
| 2        | -         | `Write(A)` |
| 3        | `Read(A)` | -          |
| 4        | -         | `Write(A)` |

🚨 **Conflict exists but produces the same final value as a serial schedule.**

---

## **🔹 6. Cascadeless Schedule**

✅ **Prevents cascading rollbacks** by **not allowing a transaction to read uncommitted data**.

🚨 **Fix for Dirty Read problem**.

### **Example**

| **Step** | **T1**                   | **T2**                    |
| -------- | ------------------------ | ------------------------- |
| 1        | `Read(A)`                | -                         |
| 2        | `Write(A) (Uncommitted)` | -                         |
| 3        | -                        | `Read(A)` ❌ (Not allowed) |

✅ **Fix:** T2 must wait until T1 commits.

---

## **🔹 Final Summary**

| **Schedule Type**         | **Concurrency** | **Consistency** | **Used in Databases?**      |
| ------------------------- | --------------- | --------------- | --------------------------- |
| **Serial**                | ❌ No            | ✅ Yes           | ❌ No (Too slow)             |
| **Non-Serial**            | ✅ Yes           | ❌ No            | ❌ No (Causes inconsistency) |
| **Serializable**          | ✅ Yes           | ✅ Yes           | ✅ Yes (Ideal case)          |
| **Conflict-Serializable** | ✅ Yes           | ✅ Yes           | ✅ Yes                       |
| **View-Serializable**     | ✅ Yes           | ✅ Yes           | ✅ Yes                       |
| **Cascadeless**           | ✅ Yes           | ✅ Yes           | ✅ Yes (Prevents Dirty Read) |
### **🔹 Recoverable & Non-Recoverable Schedules in DBMS**

A **schedule** is a sequence of executed transactions. In case of system failure, the database must be able to recover to a **consistent state**.

---
## **🔹 1. Recoverable Schedule** ✅

A schedule is **recoverable** if a transaction **commits only after all transactions it depends on have committed**.

### **Example (Recoverable Schedule)**

| **Step** | **T1**              | **T2**              |
| -------- | ------------------- | ------------------- |
| 1        | `Read(A = 1000)`    | -                   |
| 2        | `A = A - 500 (500)` | -                   |
| 3        | `Write(A = 500)`    | -                   |
| 4        | -                   | `Read(A = 500)`     |
| 5        | `Commit T1 ✅`       | -                   |
| 6        | -                   | `A = A + 200 (700)` |
| 7        | -                   | `Write(A = 700)`    |
| 8        | -                   | `Commit T2 ✅`       |

✅ **Why Recoverable?**

- **T2 reads A from T1**.
- **T1 commits before T2 commits**, ensuring consistency.

🚀 **Advantage:** No data inconsistency after rollback.

---

## **🔹 2. Non-Recoverable Schedule** ❌

A schedule is **non-recoverable** if a transaction **commits before a dependent transaction has committed**.

### **Example (Non-Recoverable Schedule)**

| **Step** | **T1**                   | **T2**          |
| -------- | ------------------------ | --------------- |
| 1        | `Read(A = 1000)`         | -               |
| 2        | `A = A - 500 (500)`      | -               |
| 3        | `Write(A = 500)`         | -               |
| 4        | -                        | `Read(A = 500)` |
| 5        | -                        | `Commit T2 ❌`   |
| 6        | **System crash occurs**  | -               |
| 7        | **T1 is rolled back!** ❌ | -               |

🚨 **Problem:**

- **T2 committed data read from uncommitted T1** (Dirty Read).
- **If T1 rolls back, T2’s committed data becomes invalid**, leading to inconsistency.

❌ **Such schedules should be avoided!**

---

## **🔹 3. Cascading Rollback Schedule** 🔄

A schedule causes **cascading rollback** if a transaction rollback **forces other transactions to roll back**.

### **Example (Cascading Rollback)**

| **Step** | **T1**              | **T2**                   | **T3**                   |
| -------- | ------------------- | ------------------------ | ------------------------ |
| 1        | `Read(A = 1000)`    | -                        | -                        |
| 2        | `A = A - 500 (500)` | -                        | -                        |
| 3        | `Write(A = 500)`    | -                        | -                        |
| 4        | -                   | `Read(A = 500)`          | -                        |
| 5        | -                   | `Write(A = 500)`         | -                        |
| 6        | -                   | -                        | `Read(A = 500)`          |
| 7        | **T1 rolls back** ❌ | -                        | -                        |
| 8        | -                   | **T2 also rolls back** ❌ | -                        |
| 9        | -                   | -                        | **T3 also rolls back** ❌ |

🚨 **Problem:**

- **T2 depends on T1** → When T1 rolls back, **T2 must also roll back**.
- **T3 depends on T2** → When T2 rolls back, **T3 must also roll back**.

**⏩ Solution:** **Use Cascadeless Schedule (Only Read Committed Data).**

---

## **🔹 4. Cascadeless Schedule** ✅

A schedule is **cascadeless** if **a transaction only reads committed data**.

### **Example (Cascadeless Schedule)**

| **Step** | **T1**              | **T2**           |
| -------- | ------------------- | ---------------- |
| 1        | `Read(A = 1000)`    | -                |
| 2        | `A = A - 500 (500)` | -                |
| 3        | `Write(A = 500)`    | -                |
| 4        | `Commit T1 ✅`       | -                |
| 5        | -                   | `Read(A = 500)`  |
| 6        | -                   | `Write(A = 700)` |
| 7        | -                   | `Commit T2 ✅`    |

✅ **T2 reads only after T1 commits**, avoiding cascading rollbacks.

---

## **🔹 Summary Table**

| **Type**                  | **Commit Order**                                   | **Issue?**                          | **Solution**        |
| ------------------------- | -------------------------------------------------- | ----------------------------------- | ------------------- |
| **Recoverable** ✅         | **T1 commits before T2 commits**                   | No inconsistency                    | **Preferred**       |
| **Non-Recoverable** ❌     | **T2 commits before T1**                           | Data inconsistency if T1 rolls back | **Avoid**           |
| **Cascading Rollback** 🔄 | **Rollback of T1 forces rollback of T2, T3, etc.** | Performance issue                   | **Use Cascadeless** |
| **Cascadeless** ✅         | **T2 reads only committed data from T1**           | No cascading rollback               | **Best Approach**   |
