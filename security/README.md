# 🔐 Security Interview Cheat Sheet

## 🧱 Core Security Concepts

### Validation

Ensures input matches expected format and type. - Example: email must be
a valid string - Tools: Joi, Zod - Goal: Reject invalid data early

### Sanitization

Removes dangerous content from input. - Example: remove
```{=html}
<script>
```
tags - Tools: xss, express-mongo-sanitize - Goal: Remove malicious
payloads

### Escaping

Prevents browsers from interpreting input as executable code. - Example:
\< becomes \< - Goal: Safe output rendering

### Encoding

Transforms data into safe transport format. - Example:
encodeURIComponent - Goal: Safe transmission or embedding

------------------------------------------------------------------------

## 🛢 NoSQL Injection (MongoDB)

### What is it?

Injection of MongoDB operators like `$ne`, `$gt` to manipulate queries.

### Prevention

-   Validate input (Joi/Zod)
-   Use express-mongo-sanitize
-   Never pass req.body directly to queries
-   Enable Mongoose strict mode

------------------------------------------------------------------------

## 💥 XSS (Cross-Site Scripting)

### Types

-   Stored XSS
-   Reflected XSS

### Prevention

-   Output escaping
-   Input sanitization
-   Helmet + CSP
-   Avoid innerHTML
-   httpOnly cookies for tokens

------------------------------------------------------------------------

## 🍪 Cookies vs localStorage

  Feature              httpOnly Cookie   localStorage
  -------------------- ----------------- --------------
  Protected from JS    Yes               No
  Vulnerable to CSRF   Yes               No
  XSS Token Theft      No                Yes

Best practice (Fintech): Use httpOnly + Secure + SameSite cookies with
CSRF protection.

------------------------------------------------------------------------

## 🔁 CSRF

### Why it happens?

Browsers automatically attach cookies to cross-site requests.

### Prevention

-   CSRF token
-   SameSite=strict or lax
-   Double submit cookie strategy

------------------------------------------------------------------------

## 🛡 Defense in Depth Strategy

1.  Input Validation
2.  Sanitization
3.  Secure Authentication (bcrypt + JWT)
4.  Authorization (RBAC)
5.  Secure Headers (Helmet, CSP)
6.  Rate Limiting
7.  HTTPS + HSTS
8.  Logging & Monitoring

Security = Risk Reduction Strategy, not 100% prevention.

------------------------------------------------------------------------

# 🎯 Interview Questions & Answers

## 🟢 Junior Level

**Q: What is XSS?**\
A: XSS allows attackers to inject malicious JavaScript into web pages.

**Q: What is NoSQL Injection?**\
A: It occurs when attackers inject MongoDB operators to manipulate
database queries.

**Q: How do you store passwords securely?**\
A: Using bcrypt hashing with salt. Never store plain text passwords.

------------------------------------------------------------------------

## 🟡 Mid Level

**Q: Authentication vs Authorization?**\
A: Authentication verifies identity; Authorization verifies permissions.

**Q: Why is localStorage risky for JWT?**\
A: Because XSS can access and steal tokens stored in localStorage.

**Q: When is CSRF protection required?**\
A: When using cookie-based authentication.

------------------------------------------------------------------------

## 🔴 Senior Level

**Q: How would you design a secure production API?**\
A: - Strict validation & sanitization - httpOnly secure cookies - CSRF
protection - Role-based access control - Rate limiting - Logging &
monitoring - HTTPS only - Secret management - Defense in depth approach

**Q: What would you do if XSS is found in production?**\
A: 1. Patch immediately 2. Invalidate active sessions 3. Review logs 4.
Strengthen CSP & sanitization 5. Conduct post-mortem analysis

------------------------------------------------------------------------

# 🚀 Production API Security Checklist

-   express.json({ limit: '10kb' })
-   Joi/Zod validation
-   express-mongo-sanitize
-   xss sanitization
-   bcrypt hashing
-   Short-lived JWT access token
-   Refresh token rotation
-   httpOnly + secure cookies
-   CSRF protection
-   Helmet + CSP
-   Rate limiting (Redis)
-   HTTPS only
-   HSTS header
-   Centralized logging

------------------------------------------------------------------------

Stay secure. Think in layers. Defense in depth always wins.
