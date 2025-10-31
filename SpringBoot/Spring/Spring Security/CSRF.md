# CSRF, Sessions & Cookies — Notes

## 1. Overview

This note explains sessions, cookies, and CSRF in simple terms with examples and defenses.

---

## 2. What is a Session?

- A **session** is a temporary relationship between a user (browser) and a website after login.
    
- When you log in, the server creates a **session** and gives your browser a **session ID** (usually via a cookie).
    
- The browser sends this session cookie automatically with requests to the site so the server knows who you are.
    

**Analogy:** session = library visitor card. The server recognizes you because of that card.

---

## 3. What is a Cookie?

- A **cookie** is a small piece of data stored by the browser for a specific origin (domain+protocol+port).
    
- The browser automatically includes relevant cookies when making requests to that origin.
    

**Common uses:** session ID (login), preferences (theme), tracking, cart items.

**Important:** Cookies for `siteA.com` cannot be read by `siteB.com` (same-origin policy), but they _are sent automatically_ when the browser makes a request to `siteA.com`.

---

## 4. What is CSRF (Cross-Site Request Forgery)?

- CSRF is an attack that tricks a logged-in user’s browser into **performing unintended actions** on another site where the user is authenticated.
    
- It exploits that browsers **automatically send cookies** for the target site when a request is made.
    

**Goal of attacker:** cause an action (transfer money, change settings) using the user’s valid session cookie.

---

## 5. How a CSRF attack works (step-by-step)

1. You log into `bank.com` → browser stores `sessionId=XYZ` for `bank.com`.
    
2. You visit `evil.com`.
    
3. `evil.com` contains a hidden form or auto-submitted request pointing to `https://bank.com/transfer`.
    
4. Browser sends the request to `bank.com` and **automatically attaches** `sessionId=XYZ` because the request targets `bank.com`.
    
5. `bank.com` sees a valid session and performs the action — even though you didn’t intend it.
    

**Key:** `evil.com` cannot read `bank.com` cookies or responses, but it can cause the browser to make the request that includes `bank.com`’s cookies.

---

## 6. Where the CSRF token is stored

- **Default (Spring):** token stored on the **server side in the user session** and exposed to the client (hidden form field or endpoint like `/getCsrfToken`).
    
- **Alternate (double-submit cookie):** token stored in a readable cookie (set by server); client reads cookie and sends token in header. Server compares header vs cookie.
    

**Important:** tokens are _not automatically included_ by the browser as headers — client code must add them to POST/PUT/DELETE requests.

---

## 7. Why the CSRF token prevents attacks

- The attacker can cause a browser to _send the session cookie_, but **cannot read** the CSRF token (same-origin policy).
    
- The server requires the correct token in addition to the session cookie. Without it, the forged request is rejected.
    

---

## 8. Example (simple)

**Malicious HTML on `evil.com`:**

```html
<form action="https://bank.com/transfer" method="POST">
  <input type="hidden" name="amount" value="1000">
  <input type="hidden" name="to" value="attacker">
</form>
<script>document.forms[0].submit();</script>
```

- Browser sends the POST to `bank.com` with `Cookie: sessionId=XYZ`.
    
- Without CSRF protection, `bank.com` performs the transfer.
    
- With CSRF protection, `bank.com` expects `X-CSRF-TOKEN: <token>` and rejects the request if token is missing/invalid.
    

---

## 9. Other defenses & notes

- **SameSite cookie attribute** (`Lax` or `Strict`) reduces CSRF by preventing the browser from sending cookies on certain cross-site requests.
    
- **Referer/Origin checks:** server validates `Origin` or `Referer` header for sensitive actions.
    
- **CORS** protects cross-origin XHR/fetch reading but does not prevent form-based CSRF alone.
    
- **Fix XSS vulnerabilities.** If an attacker can run JS on your site (XSS), they can read CSRF tokens and defeat CSRF protections.
    

---

## 10. TL;DR

- Cookies are automatically sent for requests to the cookie’s origin — that enables CSRF.
    
- CSRF token is a secret sent with state-changing requests to prove the request came from your site.
    
- Use CSRF tokens, SameSite cookies, and prevent XSS to stay safe.
    

---

_Edited: concise notes for quick reference._
![[Pasted image 20251005122040.png]]
# Spring Security Controller & Endpoints

## 📂 Package

`com.testing.SpringSecurity.controller`

- `@RestController` exposes REST endpoints
    
- Handles **Student data** and **CSRF token retrieval**
    
- Uses `HttpServletRequest` to access request attributes
    

---

## 1👑 Sample Data

```java
private List<Student> students = new ArrayList<>(
    List.of(
        new Student(1, "user1", 1),
        new Student(2, "user2", 2)
    )
);
```

- Initialized with 2 sample students
    
- `Student` bean has fields: `id`, `name`, `grade`
    




---

## 2👑 Endpoints

### 2.1 `/greet`

```java
@GetMapping("/greet")
public String greet() {
    return "Hello everyone";
}
```

- **Request Type:** GET
    
- **Description:** Simple greeting message
    
- **Authentication:** Requires **Basic Auth**
    
- **Example cURL:**
    

```bash
curl -u jack:pass1234 http://localhost:8080/greet
```

---

### 2.2 `/getStudents`

```java
@GetMapping("/getStudents")
public List<Student> getStudents() {
    return students;
}
```

- **Request Type:** GET
    
- **Description:** Returns all students
    
- **Authentication:** Requires **Basic Auth**
    
- **Example cURL:**
    

```bash
curl -u jack:pass1234 http://localhost:8080/getStudents
```

---

### 2.3 `/addStudent`

```java
@PostMapping("/addStudent")
public Student addStudent(@RequestBody Student student) {
    students.add(student);
    return student;
}
```

- **Request Type:** POST
    
- **Description:** Adds a new student to the list
    
- **Authentication:** Requires **Basic Auth**
    
- **CSRF Protection:** Must send **X-CSRF-TOKEN** header with token
    
- **Example cURL:**
    

```bash
# 1️⃣ Get CSRF token
curl -u jack:pass1234 http://localhost:8080/getCsrfToken

# 2️⃣ Add student using token
curl -u jack:pass1234 -X POST http://localhost:8080/addStudent \
-H "Content-Type: application/json" \
-H "X-CSRF-TOKEN: <csrf-token-here>" \
-d '{"id":3,"name":"user3","grade":3}'
```

---

### 2.4 `/getCsrfToken`

```java
@GetMapping("/getCsrfToken")
public CsrfToken getCsrfToken(HttpServletRequest request) {
    return (CsrfToken) request.getAttribute("_csrf");
}
```

- **Request Type:** GET
    
- **Description:** Returns CSRF token for current session
    
- **Authentication:** Requires **Basic Auth**
    
- **Purpose:** Needed for **POST/PUT/DELETE** requests
    
- **Example cURL:**
    

```bash
curl -u jack:pass1234 http://localhost:8080/getCsrfToken
```

---

## 3👑 Notes

- All endpoints are secured with **Basic Auth** using credentials in `application.properties`:
    

```properties
spring.security.user.name=jack
spring.security.user.password=pass1234
```

- **CSRF token** is required for state-changing requests (POST/PUT/DELETE)
    
- `HttpServletRequest.getAttribute("_csrf")` retrieves CSRF token programmatically
    
- `@RestController` = `@Controller` + `@ResponseBody` (automatically converts responses to JSON)