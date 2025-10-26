# Getting Started with MedVault Frontend

## Quick Start

1. **Install Dependencies**:
   ```bash
   npm install
   ```

2. **Start Development Server**:
   ```bash
   npm start
   ```

3. **Open Browser**: Navigate to `http://localhost:3000`

## Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- Spring Boot backend running on `http://localhost:8080`

## Demo Accounts

Use these accounts for testing:

| Role | Email | Password |
|------|-------|----------|
| Patient | patient@demo.com | password123 |
| Doctor | doctor@demo.com | password123 |
| Admin | admin@demo.com | password123 |

## Features Overview

### For Patients
- ✅ Register and login
- ✅ Book appointments with doctors
- ✅ Upload medical records (PDF, images, documents)
- ✅ View appointment history
- ✅ Update profile information

### For Doctors
- ✅ Register with specialization and license
- ✅ View appointment schedule
- ✅ Approve/reject appointment requests
- ✅ Access authorized patient records
- ✅ Update professional information

### For Administrators
- ✅ Manage all system users
- ✅ Verify doctor credentials
- ✅ View system-wide statistics
- ✅ Delete users and appointments

## Project Structure

```
src/
├── api/                 # API configuration and endpoints
├── components/          # Reusable UI components
├── pages/              # Page components
│   ├── admin/          # Admin-specific pages
│   ├── Home.jsx        # Landing page
│   ├── Login.jsx       # Authentication
│   ├── Dashboard.jsx   # User dashboard
│   ├── Appointments.jsx # Appointment management
│   ├── Records.jsx     # Medical records
│   └── Profile.jsx     # User profile
├── App.js              # Main app with routing
└── index.js            # Entry point
```

## API Integration

The frontend communicates with a Spring Boot backend via REST APIs:

- **Base URL**: `http://localhost:8080/api`
- **Authentication**: JWT Bearer tokens
- **File Uploads**: Multipart form data

### Key Endpoints

- `POST /auth/login` - User authentication
- `POST /auth/register` - User registration
- `GET /appointments` - Fetch appointments
- `POST /appointments` - Create appointment
- `POST /records/upload` - Upload medical record
- `GET /records/{patientId}` - Get patient records

## Development

### Available Scripts

- `npm start` - Start development server
- `npm build` - Build for production
- `npm test` - Run tests
- `npm eject` - Eject from Create React App

### Environment Variables

Create `.env` file:

```
REACT_APP_API_BASE_URL=http://localhost:8080/api
```

## Styling

- **Bootstrap 5**: Responsive UI components
- **Custom CSS**: Healthcare-themed colors and animations
- **Mobile-first**: Responsive design for all devices

## Security Features

- JWT token authentication
- Role-based route protection
- Automatic token refresh
- Secure file upload validation
- Input sanitization

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Troubleshooting

### Common Issues

1. **Backend Connection**: Ensure Spring Boot is running on port 8080
2. **CORS Errors**: Check backend CORS configuration
3. **Token Issues**: Clear localStorage and login again
4. **File Upload**: Check file size and format restrictions

### Debug Tips

1. Check browser console for errors
2. Use Network tab to monitor API calls
3. Verify request headers include Authorization token
4. Test API endpoints with Postman first

## Support

For issues or questions:
1. Check the API Integration guide
2. Review browser console errors
3. Verify backend logs
4. Test with demo accounts

## Next Steps

1. **Customize**: Modify colors, logos, and branding
2. **Extend**: Add new features and pages
3. **Deploy**: Build and deploy to production
4. **Monitor**: Set up error tracking and analytics
