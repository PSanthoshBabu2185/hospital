# MedVault Frontend - Component Documentation

## Overview

This document provides detailed information about all React components in the MedVault frontend application.

## Core Components

### CustomNavbar.jsx
**Location**: `src/components/Navbar.jsx`

**Purpose**: Main navigation component with role-based menu items

**Features**:
- Dynamic menu based on user role (Patient/Doctor/Admin)
- JWT authentication status display
- User dropdown with profile and logout options
- Responsive Bootstrap navigation

**Props**: None (uses localStorage for user data)

**Key Functions**:
- `handleLogout()`: Clears tokens and redirects to home
- `getRoleBasedMenuItems()`: Returns menu items based on user role

### Footer.jsx
**Location**: `src/components/Footer.jsx`

**Purpose**: Application footer with links and branding

**Features**:
- Quick links navigation
- Support information
- Copyright and branding
- Responsive layout

### ProtectedRoute.jsx
**Location**: `src/components/ProtectedRoute.jsx`

**Purpose**: Route protection component for authenticated users

**Props**:
- `children`: React components to render
- `allowedRoles`: Array of roles that can access the route

**Features**:
- JWT token validation
- Role-based access control
- Automatic redirect to login for unauthenticated users
- Redirect to dashboard for unauthorized roles

## Page Components

### Home.jsx
**Location**: `src/pages/Home.jsx`

**Purpose**: Landing page with platform overview

**Features**:
- Hero section with call-to-action
- Feature highlights
- Role-based content
- Responsive design
- Demo credentials display

### Login.jsx
**Location**: `src/pages/Login.jsx`

**Purpose**: User authentication form

**State**:
- `formData`: Email and password
- `loading`: Loading state for form submission
- `error`: Error message display

**Features**:
- Form validation
- JWT token storage
- Role-based redirect after login
- Demo credentials for testing

**API Integration**:
- `POST /auth/login`

### Register.jsx
**Location**: `src/pages/Register.jsx`

**Purpose**: User registration form

**State**:
- `formData`: User registration data
- `loading`: Loading state
- `error`: Error message

**Features**:
- Role selection (Patient/Doctor/Admin)
- Doctor-specific fields (specialization, license)
- Form validation
- Password confirmation

**API Integration**:
- `POST /auth/register`

### Dashboard.jsx
**Location**: `src/pages/Dashboard.jsx`

**Purpose**: User dashboard with statistics and recent activity

**State**:
- `stats`: User statistics (appointments, records, etc.)
- `recentAppointments`: Recent appointment data
- `loading`: Loading state

**Features**:
- Role-based dashboard content
- Statistics cards
- Recent appointments table
- Quick action buttons

**API Integration**:
- `GET /appointments`
- `GET /records/{patientId}`

### Appointments.jsx
**Location**: `src/pages/Appointments.jsx`

**Purpose**: Appointment management interface

**State**:
- `appointments`: List of appointments
- `doctors`: Available doctors (for patients)
- `showModal`: Modal visibility
- `editingAppointment`: Currently editing appointment
- `formData`: Appointment form data

**Features**:
- Create new appointments
- Edit existing appointments
- Status management (for doctors)
- Role-based functionality
- Responsive table layout

**API Integration**:
- `GET /appointments`
- `POST /appointments`
- `PUT /appointments/{id}`
- `DELETE /appointments/{id}`

### Records.jsx
**Location**: `src/pages/Records.jsx`

**Purpose**: Medical records management

**State**:
- `records`: List of medical records
- `patients`: Available patients (for doctors/admins)
- `showUploadModal`: Upload modal visibility
- `showViewModal`: View modal visibility
- `selectedRecord`: Currently selected record
- `uploadData`: File upload form data

**Features**:
- File upload with validation
- Patient selection (for doctors/admins)
- Record viewing and downloading
- File type and size validation
- Responsive table layout

**API Integration**:
- `POST /records/upload`
- `GET /records/{patientId}`
- `GET /records/download/{id}`
- `DELETE /records/{id}`

### Profile.jsx
**Location**: `src/pages/Profile.jsx`

**Purpose**: User profile management

**State**:
- `formData`: Profile form data
- `loading`: Loading state
- `saving`: Saving state
- `error`: Error message

**Features**:
- Profile information editing
- Doctor-specific fields
- Profile summary display
- Quick action buttons
- Form validation

**API Integration**:
- `GET /profile`
- `PUT /profile`

## Admin Components

### AdminUsers.jsx
**Location**: `src/pages/admin/AdminUsers.jsx`

**Purpose**: User management interface for administrators

**State**:
- `users`: List of all users
- `loading`: Loading state
- `showModal`: Add user modal visibility

**Features**:
- View all system users
- Delete users
- Verify doctors
- User statistics
- Role-based filtering

**API Integration**:
- `GET /admin/users`
- `PUT /admin/doctors/{id}/verify`
- `DELETE /admin/users/{id}`

### AdminDoctors.jsx
**Location**: `src/pages/admin/AdminDoctors.jsx`

**Purpose**: Doctor verification interface

**State**:
- `doctors`: List of doctors
- `loading`: Loading state

**Features**:
- Doctor verification workflow
- Statistics dashboard
- Verification guidelines
- Bulk operations

**API Integration**:
- `GET /admin/users` (filtered for doctors)
- `PUT /admin/doctors/{id}/verify`
- `DELETE /admin/users/{id}`

## API Configuration

### axios.js
**Location**: `src/api/axios.js`

**Purpose**: Axios configuration and API endpoint definitions

**Features**:
- Base URL configuration
- Request/response interceptors
- JWT token handling
- Error handling
- API endpoint organization

**Exports**:
- `authAPI`: Authentication endpoints
- `appointmentsAPI`: Appointment management
- `recordsAPI`: Medical records
- `profileAPI`: Profile management
- `adminAPI`: Admin functions

## Styling

### index.css
**Location**: `src/index.css`

**Purpose**: Global styles and CSS variables

**Features**:
- CSS custom properties for theming
- Bootstrap customization
- Responsive utilities
- Animation keyframes
- Toast notification styling

## Routing

### App.js
**Location**: `src/App.js`

**Purpose**: Main application component with routing

**Routes**:
- `/` - Home page
- `/login` - Login form
- `/register` - Registration form
- `/dashboard` - User dashboard (protected)
- `/appointments` - Appointment management (protected)
- `/records` - Medical records (protected)
- `/profile` - User profile (protected)
- `/admin/users` - User management (admin only)
- `/admin/doctors` - Doctor verification (admin only)

**Features**:
- React Router DOM v6
- Protected routes with role-based access
- Toast notification container
- Layout structure (Navbar + Main + Footer)

## State Management

The application uses React hooks for state management:

- `useState`: Local component state
- `useEffect`: Side effects and API calls
- `localStorage`: Persistent user data and tokens
- Context API: Not used (kept simple as requested)

## Error Handling

- Try-catch blocks for API calls
- Toast notifications for user feedback
- Form validation
- Network error handling
- Token expiration handling

## Performance Considerations

- Lazy loading not implemented (can be added if needed)
- Component memoization not used (can be added for optimization)
- Image optimization not implemented
- Bundle splitting not configured

## Testing

- No test files included (can be added with Jest/React Testing Library)
- Manual testing with demo accounts
- API testing with Postman
- Browser compatibility testing

## Accessibility

- Semantic HTML elements
- ARIA labels where needed
- Keyboard navigation support
- Screen reader compatibility
- Color contrast compliance

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers

## Future Enhancements

- Unit and integration tests
- Performance optimization
- Accessibility improvements
- Progressive Web App features
- Real-time notifications
- Advanced search and filtering
- Data visualization charts
- Export functionality
