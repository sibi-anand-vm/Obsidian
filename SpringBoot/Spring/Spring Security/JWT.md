# ☕ REST, Statelessness & JWT (Notes)

---

## 🌐 1️⃣ REST is Stateless

### 🧠 Meaning

- Each client request must contain **all information needed** to process it.
    
- The server **does not store** any user session or state between requests.
    
- Every request is **independent**.
    

> REST APIs are **stateless** — the server doesn’t remember you between requests.

---

### ☕ Coffee Shop Analogy

|Scenario|Description|
|---|---|
|**Stateful System**|You say “Same as yesterday,” and the barista remembers your last order. (Server stores state)|
|**Stateless System (REST)**|You say “One cappuccino with extra sugar” every time — the barista doesn’t remember you. (All info is in the request)|

✅ **REST = Stateless Communication**

---

## 🔐 2️⃣ Why JWT is Needed

- REST servers are **stateless** — they don’t store session info.
    
- When a user logs in, the server issues a **token (JWT)** instead of storing session data.
    
- The client sends this token with every request for authentication.
    

> JWT allows authentication **without maintaining sessions** on the server.

---

### ☕ Coffee Shop Example with JWT

1. You log in → barista checks your credentials.
    
2. Barista gives you a **token (membership card)** with your info:
    
    ```json
    { "name": "Captain", "role": "USER", "exp": "10:00 AM" }
    ```
    
3. You show the token each time you order.
    
4. The barista **verifies** the token — he doesn’t remember you from before.
    

That’s **JWT-based stateless authentication**.

---

## 🧬 3️⃣ JWT Structure

A JWT = **Header.Payload.Signature**

Example:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiJjYXB0YWluIiwicm9sZSI6IlVTRVIifQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

|Part|Description|Example|
|---|---|---|
|**Header**|Algorithm & Token Type|`{ "alg": "HS256", "typ": "JWT" }`|
|**Payload**|Data (claims)|`{ "username": "Captain", "role": "USER" }`|
|**Signature**|Verifies token integrity|Generated using secret key|

---

## 🔒 4️⃣ Symmetric Cryptography in JWT

- JWT uses **HMAC-SHA256** (or similar) with a **shared secret key**.
    
- Both **server for signing** and **verification** use the **same key**.
    
- This is called **symmetric encryption**.
    

### Example:

```java
Signature = HMACSHA256(
    base64UrlEncode(header) + "." + base64UrlEncode(payload),
    secretKey
)
```

> Only the server knows the secret key, so tokens can’t be forged.

---

## 🔎 5️⃣ Summary

| Concept              | Explanation                                                         |
| -------------------- | ------------------------------------------------------------------- |
| **REST**             | Architectural style for stateless communication                     |
| **Stateless**        | Server doesn’t store session info; client sends all data every time |
| **JWT**              | Token-based authentication mechanism for stateless APIs             |
| **Symmetric Crypto** | Same key used to sign                                               |