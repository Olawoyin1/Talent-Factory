# API Documentation

Base URL: `http://localhost:3000`

All responses follow a consistent shape:
- Success: `{ "success": true, "message": "...", "data": { ... } }`
- Error: `{ "success": false, "message": "...", "errors": [ ... ] }`

---

## Public Form Endpoints

---

### POST /api/learners
Submit a learner application.

**Request**
```http
POST /api/learners
Content-Type: application/json
```

```json
{
  "firstName": "Amina",
  "lastName": "Fawaz",
  "email": "amina@example.com",
  "phone": "+234 810 000 0000",
  "state": "Lagos",
  "gender": "Female",
  "ageRange": "18–24",
  "referral": "LinkedIn",
  "education": "Bachelor's Degree (B.Sc / B.A / B.Ed)",
  "fieldOfStudy": "Human Resource Management",
  "employment": "Student (full-time)",
  "jobTitle": "",
  "industry": "",
  "hrExp": "No HR experience at all",
  "linkedin": "https://linkedin.com/in/aminafawaz",
  "applyReason": "I'm a student wanting practical HR experience",
  "whyJoin": "I want to build a career in HR...",
  "twoYears": "I plan to become a certified HR professional...",
  "biggestChallenge": "The gap between university theory and workplace reality",
  "schedule": "Saturday mornings (9AM–12PM)",
  "modules": ["Recruitment & Talent Acquisition", "People Analytics"],
  "internIndustry": "Fintech / Financial Services",
  "hrKnowledge": "3",
  "referredBy": "Saw a post by Elizabeth Odetokun",
  "payment": "Instalment plan (₦50,000 × 3)",
  "techAccess": "Yes — reliable laptop and internet",
  "additionalInfo": "",
  "type": "Learner Application"
}
```

**Success Response — 201**
```json
{
  "success": true,
  "message": "Learner application submitted successfully",
  "data": {
    "_id": "665f1a2b3c4d5e6f7a8b9c0d",
    "firstName": "Amina",
    "lastName": "Fawaz",
    "email": "amina@example.com",
    "phone": "+234 810 000 0000",
    "state": "Lagos",
    "modules": ["Recruitment & Talent Acquisition", "People Analytics"],
    "createdAt": "2025-01-15T10:30:00.000Z",
    "updatedAt": "2025-01-15T10:30:00.000Z"
  }
}
```

**Validation Error — 400**
```json
{
  "success": false,
  "message": "Validation error",
  "errors": [
    { "field": "email", "message": "Invalid email address" },
    { "field": "firstName", "message": "First name is required" }
  ]
}
```

---

### POST /api/instructors
Submit an instructor application.

**Request**
```http
POST /api/instructors
Content-Type: application/json
```

```json
{
  "firstName": "Chidi",
  "lastName": "Nwosu",
  "email": "chidi@company.com",
  "phone": "+234 810 000 0000",
  "proTitle": "Head of People, Flutterwave",
  "employer": "Flutterwave",
  "industry": "Fintech",
  "linkedin": "https://linkedin.com/in/chidinwosu",
  "state": "Lagos",
  "referral": "LinkedIn",
  "totalYears": "8–10 years",
  "hrYears": "6–8 years HR",
  "seniority": "Head of Department",
  "notableOrgs": "1. Flutterwave (2021-Present)\n2. PWC (2018-2021)",
  "certs": ["PHRi", "CIPM"],
  "achievement": "Implemented automated performance review system",
  "teachModules": ["Recruitment", "Performance Management"],
  "topModule": "Recruitment & Talent Acquisition",
  "taughtBefore": "Yes — frequently",
  "teachingApproach": "Hands-on workshop style with live templates",
  "confidence": "9",
  "timeSlots": ["Weekday evenings (7PM–9PM)"],
  "sessionCount": "1–2 sessions",
  "bankName": "GTBank",
  "accountName": "Chidi Nwosu",
  "accountNumber": "0123456789",
  "whyTeach": "To help bridge the gap in the local HR industry",
  "wishKnown": "The importance of data-driven decision making",
  "bio": "Chidi is a senior HR leader with a decade of experience",
  "additionalInfo": ""
}
```

**Success Response — 201**
```json
{
  "success": true,
  "message": "Instructor application submitted successfully",
  "data": {
    "_id": "665f1a2b3c4d5e6f7a8b9c0e",
    "firstName": "Chidi",
    "lastName": "Nwosu",
    "email": "chidi@company.com",
    "proTitle": "Head of People, Flutterwave",
    "employer": "Flutterwave",
    "certs": ["PHRi", "CIPM"],
    "teachModules": ["Recruitment", "Performance Management"],
    "timeSlots": ["Weekday evenings (7PM–9PM)"],
    "createdAt": "2025-01-15T10:35:00.000Z",
    "updatedAt": "2025-01-15T10:35:00.000Z"
  }
}
```

**Validation Error — 400**
```json
{
  "success": false,
  "message": "Validation error",
  "errors": [
    { "field": "email", "message": "Invalid email address" }
  ]
}
```

---

### POST /api/waitlist
Join the waitlist.

**Request**
```http
POST /api/waitlist
Content-Type: application/json
```

```json
{
  "email": "interested@example.com",
  "source": "Talent Factory Waitlist"
}
```

**Success Response — 201**
```json
{
  "success": true,
  "message": "You've been added to the waitlist",
  "data": {
    "_id": "665f1a2b3c4d5e6f7a8b9c0f",
    "email": "interested@example.com",
    "source": "Talent Factory Waitlist",
    "createdAt": "2025-01-15T10:40:00.000Z",
    "updatedAt": "2025-01-15T10:40:00.000Z"
  }
}
```

**Duplicate Email — 409**
```json
{
  "success": false,
  "message": "A record with this email already exists"
}
```

---

## Admin Endpoints

---

### POST /api/admin/login
Authenticate as admin and receive a JWT token.

**Request**
```http
POST /api/admin/login
Content-Type: application/json
```

```json
{
  "email": "admin@yourapp.com",
  "password": "changeme123"
}
```

**Success Response — 200**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY2NWYxYTJiM2M0ZDVlNmY3YThiOWMxMCIsImVtYWlsIjoiYWRtaW5AeW91cmFwcC5jb20iLCJuYW1lIjoiQWRtaW4gVXNlciIsInJvbGUiOiJhZG1pbiIsImlhdCI6MTcwNTMxMjAwMCwiZXhwIjoxNzA1OTE2ODAwfQ.signature",
  "admin": {
    "name": "Admin User",
    "email": "admin@yourapp.com",
    "role": "admin"
  }
}
```

**Invalid Credentials — 401**
```json
{
  "success": false,
  "message": "Invalid credentials"
}
```

**Validation Error — 400**
```json
{
  "success": false,
  "message": "Validation error",
  "errors": [
    { "field": "email", "message": "Invalid email address" }
  ]
}
```

---

### GET /api/admin/dashboard
Get a summary of all submissions. Requires JWT.

**Request**
```http
GET /api/admin/dashboard
Authorization: Bearer <token>
```

**Success Response — 200**
```json
{
  "success": true,
  "message": "Dashboard data",
  "data": {
    "totalLearners": 42,
    "totalInstructors": 8,
    "totalWaitlist": 130,
    "recentLearners": [
      {
        "_id": "665f1a2b3c4d5e6f7a8b9c0d",
        "firstName": "Amina",
        "lastName": "Fawaz",
        "email": "amina@example.com",
        "createdAt": "2025-01-15T10:30:00.000Z"
      }
    ],
    "recentInstructors": [
      {
        "_id": "665f1a2b3c4d5e6f7a8b9c0e",
        "firstName": "Chidi",
        "lastName": "Nwosu",
        "email": "chidi@company.com",
        "createdAt": "2025-01-15T10:35:00.000Z"
      }
    ],
    "recentWaitlist": [
      {
        "_id": "665f1a2b3c4d5e6f7a8b9c0f",
        "email": "interested@example.com",
        "createdAt": "2025-01-15T10:40:00.000Z"
      }
    ]
  }
}
```

**Unauthorized — 401**
```json
{
  "success": false,
  "message": "Unauthorized"
}
```

---

### GET /api/admin/learners
Fetch all learner applications. Supports pagination and search.

**Request**
```http
GET /api/admin/learners?page=1&limit=10&email=amina&name=fawaz
Authorization: Bearer <token>
```

**Query Parameters**

| Param | Type | Required | Description |
|-------|------|----------|-------------|
| page | number | No | Page number (default: 1) |
| limit | number | No | Records per page (default: 20) |
| email | string | No | Filter by email (case-insensitive) |
| name | string | No | Filter by first or last name (case-insensitive) |

**Success Response — 200**
```json
{
  "success": true,
  "message": "Learner records",
  "data": {
    "records": [
      {
        "_id": "665f1a2b3c4d5e6f7a8b9c0d",
        "firstName": "Amina",
        "lastName": "Fawaz",
        "email": "amina@example.com",
        "phone": "+234 810 000 0000",
        "state": "Lagos",
        "gender": "Female",
        "education": "Bachelor's Degree (B.Sc / B.A / B.Ed)",
        "modules": ["Recruitment & Talent Acquisition", "People Analytics"],
        "payment": "Instalment plan (₦50,000 × 3)",
        "createdAt": "2025-01-15T10:30:00.000Z",
        "updatedAt": "2025-01-15T10:30:00.000Z"
      }
    ],
    "total": 42,
    "page": 1,
    "limit": 10
  }
}
```

---

### GET /api/admin/instructors
Fetch all instructor applications. Supports pagination and search.

**Request**
```http
GET /api/admin/instructors?page=1&limit=10&name=chidi
Authorization: Bearer <token>
```

**Query Parameters** — same as `/api/admin/learners`

**Success Response — 200**
```json
{
  "success": true,
  "message": "Instructor records",
  "data": {
    "records": [
      {
        "_id": "665f1a2b3c4d5e6f7a8b9c0e",
        "firstName": "Chidi",
        "lastName": "Nwosu",
        "email": "chidi@company.com",
        "proTitle": "Head of People, Flutterwave",
        "employer": "Flutterwave",
        "industry": "Fintech",
        "seniority": "Head of Department",
        "certs": ["PHRi", "CIPM"],
        "teachModules": ["Recruitment", "Performance Management"],
        "timeSlots": ["Weekday evenings (7PM–9PM)"],
        "createdAt": "2025-01-15T10:35:00.000Z",
        "updatedAt": "2025-01-15T10:35:00.000Z"
      }
    ],
    "total": 8,
    "page": 1,
    "limit": 10
  }
}
```

---

### GET /api/admin/waitlist
Fetch all waitlist entries. Supports pagination and email search.

**Request**
```http
GET /api/admin/waitlist?page=1&limit=20&email=interested
Authorization: Bearer <token>
```

**Query Parameters**

| Param | Type | Required | Description |
|-------|------|----------|-------------|
| page | number | No | Page number (default: 1) |
| limit | number | No | Records per page (default: 20) |
| email | string | No | Filter by email (case-insensitive) |

**Success Response — 200**
```json
{
  "success": true,
  "message": "Waitlist records",
  "data": {
    "records": [
      {
        "_id": "665f1a2b3c4d5e6f7a8b9c0f",
        "email": "interested@example.com",
        "source": "Talent Factory Waitlist",
        "createdAt": "2025-01-15T10:40:00.000Z",
        "updatedAt": "2025-01-15T10:40:00.000Z"
      }
    ],
    "total": 130,
    "page": 1,
    "limit": 20
  }
}
```

---

## Common Error Responses

### 404 — Route Not Found
```json
{
  "success": false,
  "message": "Route not found"
}
```

### 429 — Rate Limit Exceeded
```json
{
  "success": false,
  "message": "Too many requests, please try again later."
}
```

### 500 — Server Error (production)
```json
{
  "success": false,
  "message": "Something went wrong"
}
```
