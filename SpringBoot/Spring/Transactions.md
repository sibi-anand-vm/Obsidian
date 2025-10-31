![[Pasted image 20251003102627.png]]
![[Pasted image 20251003102659.png]]
![[Pasted image 20251003102829.png]]

Transaction helps us avoid boilerplate code by using AOP.
@Enable transaction management is not necessary.

Can be applied at class level and method level.
![[Pasted image 20251003103118.png]]

### 1. Transaction Managers

This section refers to the two primary ways a developer can control a transaction's lifecycle (start, commit, rollback):

- **Programmatic
    
- **Declarative:**

### 2. Transaction Propagations

Propagation rules define how a transactional method should behave when it is called from another method, especially one that is already running inside a transaction. They control how the transactional context flows across method boundaries.

# Transaction Propagations in Spring

---

## 1️⃣ REQUIRED (default)

**Meaning:** Join the existing transaction, or create a new one if none exists.  
**Use case:** Normal operations.

```java
@Transactional(propagation = Propagation.REQUIRED) public void saveUser() {     // joins outer transaction if exists }
```

✅ Behavior: If outer transaction rolls back → this also rolls back.

---

## 2️⃣ REQUIRES_NEW

**Meaning:** Always create a new transaction, suspend any existing one.  
**Use case:** Logging, auditing, or critical operations that must commit even if outer fails.

```java
@Transactional(propagation = Propagation.REQUIRES_NEW) public void saveLog() {     // independent transaction }
```

✅ Behavior: Inner transaction commits or rolls back independently. Outer transaction pause does not affect it.

---

## 3️⃣ NESTED

**Meaning:** Run a nested transaction inside the outer transaction.  
**Use case:** Partial rollback possible.

```java
@Transactional(propagation = Propagation.NESTED) public void saveItem() {     // can rollback this nested part without affecting outer }
```

✅ Behavior: If nested fails → only nested rolls back; outer can continue.  
_Requires DataSource that supports savepoints._

---

## 4️⃣ SUPPORTS

**Meaning:** Join transaction if exists, else run without transaction.  
**Use case:** Optional transactional behavior.

```java
@Transactional(propagation = Propagation.SUPPORTS) public void optionalTx() {      }
```

✅ Behavior: Runs in outer transaction if present, else executes without a transaction.

---

## 5️⃣ NOT_SUPPORTED

**Meaning:** Always run outside a transaction. Suspends existing transaction.  
**Use case:** Reading logs or sending emails where rollback is not desired.

```java
@Transactional(propagation = Propagation.NOT_SUPPORTED) public void sendEmail() {     // no transaction }
```

✅ Behavior: Suspends outer transaction, runs without a transaction. Changes are immediate, no rollback.

---

## 6️⃣ MANDATORY

**Meaning:** Must run inside an existing transaction, else throw error.  
**Use case:** Called only from transactional methods.

```java
@Transactional(propagation = Propagation.MANDATORY) public void updateData() {     // fails if no transaction exists }
```

✅ Behavior: Fails if no transaction exists. Always part of outer transaction.

---

## 7️⃣ NEVER

**Meaning:** Must run without a transaction, throw error if there’s one.  
**Use case:** Read-only operations or external calls that shouldn’t be transactional.

```java
@Transactional(propagation = Propagation.NEVER) public void readExternal() {     // fails if inside transaction }
```

✅ Behavior: Throws error if called inside a transaction. Must run outside.


![[Pasted image 20251003105154.png]]
![[Pasted image 20251003105257.png]]
![[Pasted image 20251003105745.png]]
![[Pasted image 20251003110042.png]]
This makes spring to pick up DataSourceTransactionManager instead of defaultly picking JPATransactionManager.
First Approach:
![[Pasted image 20251003111252.png]]
![[Pasted image 20251003112642.png]]

### So, when do you need **programmatic**?

- When you can’t just put `@Transactional` because:
    
    1. **Transaction depends on runtime conditions**  
        (Example: rollback only if a certain validation fails).
        
    2. **Multiple small transactions inside one method**  
        (Example: commit after every batch in a loop).
        
    3. **Mixing multiple data sources / message queues**  
        (DB + Kafka/JMS + another DB).
        
    4. **Utility/library code** that Spring doesn’t manage → `@Transactional` won’t work there.