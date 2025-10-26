# MedVault Frontend

A modern, responsive React.js frontend for the MedVault medical management system.

## Features

- **User Authentication**: JWT-based login/registration with role-based access
- **Role Management**: Support for Patient, Doctor, and Admin roles
- **Appointment Booking**: Patients can book appointments with doctors
- **Medical Records**: Secure file upload and management system
- **Admin Panel**: User management and doctor verification
- **Responsive Design**: Mobile-first design with Bootstrap 5
- **Real-time Notifications**: Toast notifications for user feedback

## Tech Stack

- **React.js 18**: Latest React with hooks
- **React Router DOM v6**: Client-side routing
- **Bootstrap 5**: Responsive UI components
- **Axios**: HTTP client for API calls
- **React Toastify**: Toast notifications
- **JWT**: Authentication tokens

## Installation

1. Install dependencies:
```bash
npm install
```

2. Start the development server:
```bash
npm start
```

3. Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

## API Integration

The frontend is configured to work with a Spring Boot backend running on `http://localhost:8080/api`.

### API Endpoints

- **Authentication**: `/auth/login`, `/auth/register`
- **Appointments**: `/appointments` (GET, POST, PUT, DELETE)
- **Records**: `/records/upload`, `/records/{patientId}`
- **Profile**: `/profile` (GET, PUT)
- **Admin**: `/admin/users`, `/admin/doctors/{id}/verify`

### Authentication

JWT tokens are automatically included in API requests via Axios interceptors. Tokens are stored in localStorage and refreshed as needed.

## User Roles

### Patient
- Book appointments with doctors
- Upload and manage medical records
- View appointment history
- Update profile information

### Doctor
- View and manage appointment schedule
- Approve/reject appointment requests
- Access authorized patient records
- Update professional information

### Admin
- Manage all system users
- Verify doctor credentials
- View system-wide data
- Delete users and appointments

## Project Structure

```
src/
├── api/
│   └── axios.js          # Axios configuration and API endpoints
├── components/
│   ├── Navbar.jsx        # Navigation component
│   ├── Footer.jsx        # Footer component
│   └── ProtectedRoute.jsx # Route protection component
├── pages/
│   ├── Home.jsx          # Landing page
│   ├── Login.jsx         # Login form
│   ├── Register.jsx      # Registration form
│   ├── Dashboard.jsx     # User dashboard
│   ├── Appointments.jsx  # Appointment management
│   ├── Records.jsx       # Medical records management
│   ├── Profile.jsx       # User profile
│   └── admin/
│       ├── AdminUsers.jsx    # User management
│       └── AdminDoctors.jsx  # Doctor verification
├── App.js                # Main app component with routing
├── index.js              # App entry point
└── index.css             # Global styles
```

## Demo Credentials

For testing purposes, use these demo accounts:

- **Patient**: patient@demo.com / password123
- **Doctor**: doctor@demo.com / password123
- **Admin**: admin@demo.com / password123

## Development

### Available Scripts

- `npm start`: Runs the app in development mode
- `npm build`: Builds the app for production
- `npm test`: Launches the test runner
- `npm eject`: Ejects from Create React App (one-way operation)

### Environment Variables

Create a `.env` file in the root directory:

```
REACT_APP_API_BASE_URL=http://localhost:8080/api
```

## Security Features

- JWT token authentication
- Role-based route protection
- Automatic token refresh
- Secure file upload validation
- Input sanitization and validation

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License.
