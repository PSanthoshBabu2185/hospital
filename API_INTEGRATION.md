# MedVault Frontend - API Integration Guide

This document provides detailed information about API integration for the MedVault frontend application.

## Base Configuration

The frontend is configured to communicate with a Spring Boot backend running on:
- **Base URL**: `http://localhost:8080/api`
- **Authentication**: JWT Bearer tokens
- **Content Type**: `application/json` (except file uploads)

## API Endpoints

### Authentication

#### POST /auth/login
**Purpose**: User login
**Request Body**:
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```
**Response**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 1,
    "firstName": "John",
    "lastName": "Doe",
    "email": "user@example.com",
    "role": "PATIENT",
    "phoneNumber": "+1234567890",
    "specialization": null,
    "licenseNumber": null,
    "isVerified": true,
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

#### POST /auth/register
**Purpose**: User registration
**Request Body**:
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "user@example.com",
  "password": "password123",
  "role": "PATIENT",
  "phoneNumber": "+1234567890",
  "specialization": "Cardiology", // For doctors only
  "licenseNumber": "MD123456" // For doctors only
}
```

### Appointments

#### GET /appointments
**Purpose**: Fetch all appointments (filtered by user role)
**Headers**: `Authorization: Bearer <token>`
**Response**:
```json
[
  {
    "id": 1,
    "appointmentDate": "2024-01-15T10:00:00Z",
    "appointmentTime": "10:00",
    "reason": "Regular checkup",
    "status": "CONFIRMED",
    "patientId": 1,
    "doctorId": 2,
    "patient": {
      "id": 1,
      "firstName": "John",
      "lastName": "Doe"
    },
    "doctor": {
      "id": 2,
      "firstName": "Dr. Jane",
      "lastName": "Smith",
      "specialization": "Cardiology"
    }
  }
]
```

#### POST /appointments
**Purpose**: Create new appointment
**Request Body**:
```json
{
  "appointmentDate": "2024-01-15T10:00:00Z",
  "appointmentTime": "10:00",
  "reason": "Regular checkup",
  "patientId": 1,
  "doctorId": 2
}
```

#### PUT /appointments/{id}
**Purpose**: Update appointment
**Request Body**:
```json
{
  "status": "CONFIRMED",
  "appointmentDate": "2024-01-15T10:00:00Z",
  "appointmentTime": "10:00",
  "reason": "Updated reason"
}
```

#### DELETE /appointments/{id}
**Purpose**: Delete appointment

### Medical Records

#### POST /records/upload
**Purpose**: Upload medical record file
**Content-Type**: `multipart/form-data`
**Form Data**:
- `file`: File object
- `title`: String
- `description`: String
- `patientId`: Number

#### GET /records/{patientId}
**Purpose**: Get records for specific patient
**Response**:
```json
[
  {
    "id": 1,
    "title": "Blood Test Results",
    "description": "Complete blood count",
    "fileName": "blood_test.pdf",
    "fileSize": 1024000,
    "uploadDate": "2024-01-01T00:00:00Z",
    "patientId": 1
  }
]
```

#### GET /records/download/{id}
**Purpose**: Download medical record file
**Response**: File download

#### DELETE /records/{id}
**Purpose**: Delete medical record

### Profile Management

#### GET /profile
**Purpose**: Get current user profile
**Headers**: `Authorization: Bearer <token>`

#### PUT /profile
**Purpose**: Update user profile
**Request Body**:
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "phoneNumber": "+1234567890",
  "specialization": "Cardiology", // For doctors
  "licenseNumber": "MD123456" // For doctors
}
```

### Admin Endpoints

#### GET /admin/users
**Purpose**: Get all users (Admin only)
**Headers**: `Authorization: Bearer <admin_token>`

#### PUT /admin/doctors/{doctorId}/verify
**Purpose**: Verify doctor credentials (Admin only)
**Headers**: `Authorization: Bearer <admin_token>`

#### DELETE /admin/users/{userId}
**Purpose**: Delete user (Admin only)
**Headers**: `Authorization: Bearer <admin_token>`

## Error Handling

### Common Error Responses

#### 401 Unauthorized
```json
{
  "message": "Invalid or expired token",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

#### 403 Forbidden
```json
{
  "message": "Access denied. Insufficient permissions.",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

#### 400 Bad Request
```json
{
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "Email is required"
    }
  ],
  "timestamp": "2024-01-01T00:00:00Z"
}
```

#### 500 Internal Server Error
```json
{
  "message": "Internal server error",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## Frontend Implementation

### Axios Configuration

```javascript
// src/api/axios.js
import axios from 'axios';

const api = axios.create({
  baseURL: 'http://localhost:8080/api',
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Request interceptor to add JWT token
api.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Response interceptor to handle token expiration
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      localStorage.removeItem('user');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);
```

### API Service Functions

```javascript
// Authentication
export const authAPI = {
  login: (credentials) => api.post('/auth/login', credentials),
  register: (userData) => api.post('/auth/register', userData),
};

// Appointments
export const appointmentsAPI = {
  getAll: () => api.get('/appointments'),
  create: (appointmentData) => api.post('/appointments', appointmentData),
  update: (id, appointmentData) => api.put(`/appointments/${id}`, appointmentData),
  delete: (id) => api.delete(`/appointments/${id}`),
};

// Records
export const recordsAPI = {
  upload: (formData) => api.post('/records/upload', formData, {
    headers: { 'Content-Type': 'multipart/form-data' }
  }),
  getByPatient: (patientId) => api.get(`/records/${patientId}`),
  delete: (id) => api.delete(`/records/${id}`),
};
```

## Testing with Postman

### Collection Setup

1. Create a new Postman collection named "MedVault API"
2. Set collection variables:
   - `base_url`: `http://localhost:8080/api`
   - `token`: (will be set after login)

### Authentication Flow

1. **Register User**:
   ```
   POST {{base_url}}/auth/register
   Body: {
     "firstName": "Test",
     "lastName": "User",
     "email": "test@example.com",
     "password": "password123",
     "role": "PATIENT"
   }
   ```

2. **Login**:
   ```
   POST {{base_url}}/auth/login
   Body: {
     "email": "test@example.com",
     "password": "password123"
   }
   ```

3. **Set Token**:
   - Copy token from login response
   - Set collection variable `token`
   - Add Authorization header: `Bearer {{token}}`

### Testing Protected Endpoints

All subsequent requests should include:
```
Authorization: Bearer {{token}}
```

## CORS Configuration

Ensure your Spring Boot backend has CORS configured to allow requests from `http://localhost:3000`:

```java
@CrossOrigin(origins = "http://localhost:3000")
@RestController
@RequestMapping("/api")
public class AuthController {
    // Controller methods
}
```

## File Upload Testing

For testing file uploads in Postman:

1. Set method to POST
2. Go to Body tab
3. Select "form-data"
4. Add fields:
   - `file`: Select file (type: File)
   - `title`: Text value
   - `description`: Text value
   - `patientId`: Number value

## Environment Variables

Create `.env` file in React project root:

```
REACT_APP_API_BASE_URL=http://localhost:8080/api
REACT_APP_ENVIRONMENT=development
```

Update axios configuration to use environment variable:

```javascript
const api = axios.create({
  baseURL: process.env.REACT_APP_API_BASE_URL || 'http://localhost:8080/api',
  // ... other config
});
```

## Troubleshooting

### Common Issues

1. **CORS Errors**: Ensure backend CORS is configured for frontend origin
2. **Token Expiration**: Implement token refresh logic
3. **File Upload Issues**: Check file size limits and allowed file types
4. **Network Errors**: Verify backend is running on correct port

### Debug Tips

1. Check browser Network tab for API calls
2. Verify request headers include Authorization token
3. Check console for JavaScript errors
4. Use Postman to test API endpoints independently
5. Verify backend logs for server-side errors
