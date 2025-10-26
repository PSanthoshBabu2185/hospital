# MedVault Frontend - Installation and Setup

## Prerequisites

Before installing the MedVault frontend, ensure you have:

- **Node.js** (v16 or higher) - [Download here](https://nodejs.org/)
- **npm** (comes with Node.js) or **yarn**
- **Spring Boot backend** running on `http://localhost:8080`

## Installation Steps

### 1. Clone or Download the Project

If you have the project files, navigate to the project directory:

```bash
cd medvault-frontend
```

### 2. Install Dependencies

Install all required packages:

```bash
npm install
```

This will install:
- React.js (v18.2.0)
- React Router DOM (v6.8.0)
- Axios (v1.3.0)
- Bootstrap (v5.2.0)
- React Bootstrap (v2.7.0)
- React Toastify (v9.1.0)

### 3. Environment Configuration

Create a `.env` file in the root directory:

```bash
# .env
REACT_APP_API_BASE_URL=http://localhost:8080/api
REACT_APP_ENVIRONMENT=development
```

### 4. Start the Development Server

```bash
npm start
```

The application will open in your browser at `http://localhost:3000`.

## Verification

### 1. Check Application Loads

- Open `http://localhost:3000`
- You should see the MedVault home page
- Navigation should be visible

### 2. Test Authentication

- Click "Login" in the navigation
- Use demo credentials:
  - **Patient**: patient@demo.com / password123
  - **Doctor**: doctor@demo.com / password123
  - **Admin**: admin@demo.com / password123

### 3. Verify API Connection

- Ensure your Spring Boot backend is running on port 8080
- Check browser console for any CORS or connection errors
- Test API calls by logging in and navigating to different pages

## Troubleshooting

### Common Issues

#### 1. Port Already in Use

If port 3000 is already in use:

```bash
# Kill process using port 3000
npx kill-port 3000

# Or use a different port
PORT=3001 npm start
```

#### 2. Backend Connection Issues

- Verify Spring Boot is running on `http://localhost:8080`
- Check CORS configuration in backend
- Ensure API endpoints are accessible

#### 3. Dependency Issues

```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### 4. Build Issues

```bash
# Clear build cache
npm run build

# Check for TypeScript errors (if any)
npm run test
```

## Development Commands

### Available Scripts

```bash
# Start development server
npm start

# Build for production
npm run build

# Run tests
npm test

# Eject from Create React App (one-way operation)
npm run eject
```

### Development Tips

1. **Hot Reload**: Changes are automatically reflected in the browser
2. **Console Logs**: Check browser console for errors and API calls
3. **Network Tab**: Monitor API requests in browser dev tools
4. **Component Inspection**: Use React Developer Tools extension

## Production Build

### Build the Application

```bash
npm run build
```

This creates a `build` folder with optimized production files.

### Serve Production Build

```bash
# Install serve globally
npm install -g serve

# Serve the build folder
serve -s build
```

## Docker Setup (Optional)

### Create Dockerfile

```dockerfile
# Dockerfile
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
```

### Build and Run Docker Container

```bash
# Build image
docker build -t medvault-frontend .

# Run container
docker run -p 3000:3000 medvault-frontend
```

## Environment Variables

### Development

```bash
# .env.development
REACT_APP_API_BASE_URL=http://localhost:8080/api
REACT_APP_ENVIRONMENT=development
REACT_APP_DEBUG=true
```

### Production

```bash
# .env.production
REACT_APP_API_BASE_URL=https://your-api-domain.com/api
REACT_APP_ENVIRONMENT=production
REACT_APP_DEBUG=false
```

## Browser Support

Tested on:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Performance Optimization

### Bundle Analysis

```bash
# Install bundle analyzer
npm install --save-dev webpack-bundle-analyzer

# Analyze bundle size
npm run build
npx webpack-bundle-analyzer build/static/js/*.js
```

### Code Splitting

The application can be enhanced with:
- React.lazy() for component lazy loading
- Dynamic imports for route-based splitting
- Suspense boundaries for loading states

## Security Considerations

### Environment Variables

- Never commit `.env` files with sensitive data
- Use `REACT_APP_` prefix for client-side variables
- Server-side secrets should remain on the backend

### API Security

- JWT tokens are stored in localStorage
- Tokens are automatically included in API requests
- Token expiration is handled by interceptors

## Monitoring and Analytics

### Error Tracking

Consider integrating:
- Sentry for error tracking
- Google Analytics for usage analytics
- LogRocket for session replay

### Performance Monitoring

- Core Web Vitals tracking
- Bundle size monitoring
- API response time tracking

## Next Steps

1. **Customize Branding**: Update colors, logos, and content
2. **Add Features**: Implement additional functionality
3. **Testing**: Add unit and integration tests
4. **Deployment**: Set up CI/CD pipeline
5. **Monitoring**: Add error tracking and analytics

## Support

For issues or questions:
1. Check browser console for errors
2. Verify backend API is running
3. Test with demo accounts
4. Review documentation files
5. Check network connectivity
