# Architecture

This document provides a comprehensive overview of the Quantum Logics system architecture, including design decisions, technology stack, and implementation details.

## Table of Contents

- [System Overview](#system-overview)
- [Technology Stack](#technology-stack)
- [Frontend Architecture](#frontend-architecture)
- [Backend Architecture](#backend-architecture)
- [Database Design](#database-design)
- [Security Architecture](#security-architecture)
- [Deployment Architecture](#deployment-architecture)
- [Development Workflow](#development-workflow)
- [Performance Considerations](#performance-considerations)
- [Scalability Planning](#scalability-planning)

## System Overview

Quantum Logics is a full-stack web application designed as a modern software house platform. The system follows a monorepo structure with separate frontend and backend components, each maintained as Git submodules.

### Core Components

1. **Frontend**: React-based single-page application
2. **Backend**: Express.js REST API with MongoDB
3. **Database**: MongoDB with Atlas for production
4. **Authentication**: JWT-based authentication system
5. **File Storage**: Local file system with cloud migration path

### Key Features

- Company website with product showcase
- Job application system
- Admin dashboard with real-time statistics
- Email notification system
- Mobile-responsive design
- Accessibility compliance (WCAG 2.1)

## Technology Stack

### Frontend

- **Framework**: React 19.2.4
- **Routing**: React Router DOM
- **Styling**: Pure CSS with CSS variables
- **Build Tool**: Create React App (react-scripts)
- **HTTP Client**: Axios
- **State Management**: React Hooks (useState, useEffect, useRef)
- **Custom Hooks**: useCounter, useInView for animations

### Backend

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: bcryptjs + JWT
- **Validation**: express-validator
- **Email**: Nodemailer
- **Development**: nodemon

### Development Tools

- **Version Control**: Git with submodules
- **Package Manager**: npm
- **Code Quality**: ESLint with accessibility rules
- **Build System**: React Scripts for frontend, npm scripts for backend

## Frontend Architecture

### Component Structure

The frontend follows a component-based architecture with clear separation of concerns:

```
src/
├── components/
│   ├── HomePage.jsx      # Main landing page component
│   ├── Navbar.jsx        # Navigation component
│   ├── Footer.jsx        # Footer component
│   └── Icon.jsx          # Icon utilities
├── App.jsx               # Root application component
└── index.js              # Application entry point
```

### Key Components

#### HomePage.jsx
- **Purpose**: Main landing page with company information
- **Features**: Hero section, product showcase, testimonials, team profiles
- **Custom Hooks**: 
  - `useCounter`: Animated number counters
  - `useInView`: Scroll-triggered animations
- **Accessibility**: Fully compliant with jsx-a11y rules

#### Navbar.jsx
- **Purpose**: Navigation and user authentication
- **Features**: Product dropdown, user menu, mobile responsiveness
- **State Management**: Local state for menu toggles and user data

#### Footer.jsx
- **Purpose**: Site footer with links and information
- **Features**: Social links, legal pages, company information

### Styling Architecture

The styling system uses pure CSS with a design token approach:

```css
/* Design Tokens */
:root {
  --primary-color: #2563eb;
  --secondary-color: #1e40af;
  --accent-color: #60a5fa;
  --text-primary: #1f2937;
  --text-secondary: #6b7280;
  --bg-primary: #ffffff;
  --bg-secondary: #f9fafb;
}
```

### Build Process

The frontend uses Create React App's build system:

1. **Development**: `npm start` - Hot reload development server
2. **Build**: `npm run build` - Production optimization
3. **Test**: `npm test` - Unit testing with Jest
4. **Eject**: `npm run eject` - Custom configuration (if needed)

### Accessibility Features

- Semantic HTML5 elements
- ARIA labels and roles
- Keyboard navigation support
- Screen reader compatibility
- Color contrast compliance
- Focus management

## Backend Architecture

### API Structure

The backend follows RESTful API principles:

```
api/
├── auth/              # Authentication endpoints
├── users/             # User management
├── jobs/              # Job postings and applications
├── admin/             # Admin dashboard data
└── notifications/    # Email and system notifications
```

### Key Endpoints

#### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `POST /api/auth/logout` - User logout
- `GET /api/auth/verify` - Token verification

#### Jobs
- `GET /api/jobs` - List all job postings
- `POST /api/jobs` - Create new job posting
- `POST /api/jobs/:id/apply` - Submit job application
- `GET /api/jobs/:id/applications` - View job applications

#### Admin
- `GET /api/admin/stats` - Dashboard statistics
- `GET /api/admin/users` - User management
- `PUT /api/admin/users/:id` - Update user status

### Data Models

#### User Model
```javascript
{
  _id: ObjectId,
  email: String,
  password: String, // bcrypt hashed
  role: String, // 'admin', 'user'
  profile: {
    firstName: String,
    lastName: String,
    phone: String,
    address: String
  },
  createdAt: Date,
  updatedAt: Date
}
```

#### Job Model
```javascript
{
  _id: ObjectId,
  title: String,
  description: String,
  requirements: [String],
  location: String,
  type: String, // 'full-time', 'part-time', 'contract'
  salary: String,
  postedBy: ObjectId,
  applications: [ObjectId],
  status: String, // 'active', 'closed'
  createdAt: Date,
  updatedAt: Date
}
```

### Security Implementation

#### Authentication
- JWT tokens for session management
- bcryptjs for password hashing
- Rate limiting on auth endpoints
- Input validation and sanitization

#### Authorization
- Role-based access control (RBAC)
- Middleware for route protection
- Admin-only endpoints

## Database Design

### MongoDB Schema

The database uses MongoDB with the following collections:

- **users**: User accounts and profiles
- **jobs**: Job postings and descriptions
- **applications**: Job applications and status
- **notifications**: System and email notifications
- **sessions**: Active user sessions

### Indexing Strategy

```javascript
// Users collection
db.users.createIndex({ email: 1 }, { unique: true })
db.users.createIndex({ role: 1 })

// Jobs collection
db.jobs.createIndex({ status: 1 })
db.jobs.createIndex({ postedBy: 1 })
db.jobs.createIndex({ createdAt: -1 })

// Applications collection
db.applications.createIndex({ jobId: 1 })
db.applications.createIndex({ userId: 1 })
db.applications.createIndex({ status: 1 })
```

### Data Relationships

- Users → Jobs (one-to-many via postedBy)
- Users → Applications (one-to-many)
- Jobs → Applications (one-to-many)
- Applications → Status tracking

## Security Architecture

### Authentication Flow

1. User submits credentials
2. Server validates and hashes password
3. JWT token generated and returned
4. Client stores token in localStorage
5. Token sent with subsequent requests
6. Server validates token on protected routes

### Security Measures

- **Password Security**: bcryptjs with salt rounds
- **Token Security**: JWT with expiration and refresh
- **Input Validation**: express-validator for all inputs
- **Rate Limiting**: Prevent brute force attacks
- **CORS**: Proper cross-origin resource sharing
- **HTTPS**: SSL/TLS encryption in production

### Data Protection

- Sensitive data encryption at rest
- PII (Personally Identifiable Information) protection
- GDPR compliance considerations
- Regular security audits

## Deployment Architecture

### Development Environment

- **Local Development**: Docker containers for consistency
- **Database**: Local MongoDB instance
- **Frontend**: React development server (port 3000)
- **Backend**: Node.js server (port 5000)

### Production Environment

- **Frontend**: Static hosting (Vercel/Netlify)
- **Backend**: Cloud hosting (AWS/Heroku)
- **Database**: MongoDB Atlas
- **Email**: SendGrid or similar service
- **CDN**: CloudFlare for static assets

### CI/CD Pipeline

1. **Code Commit**: Git push to repository
2. **Automated Testing**: Unit and integration tests
3. **Build Process**: Production build optimization
4. **Deployment**: Automated deployment to staging
5. **Production**: Manual approval for production deploy

## Development Workflow

### Git Workflow

```
main (production)
├── develop (staging)
└── feature/* (feature branches)
```

### Code Quality

- **ESLint**: JavaScript code linting
- **Prettier**: Code formatting
- **Accessibility**: jsx-a11y rules enforcement
- **Testing**: Jest for unit tests

### Development Commands

```bash
# Frontend
npm start          # Development server
npm run build      # Production build
npm test           # Run tests

# Backend
npm run dev        # Development with nodemon
npm start          # Production server
npm test           # Run tests
```

## Performance Considerations

### Frontend Optimization

- **Code Splitting**: Lazy loading of components
- **Bundle Optimization**: Tree shaking and minification
- **Image Optimization**: WebP format and lazy loading
- **Caching**: Service worker implementation
- **Performance Monitoring**: Web Vitals tracking

### Backend Optimization

- **Database Indexing**: Optimized query performance
- **Caching**: Redis for frequently accessed data
- **Compression**: Gzip compression for responses
- **Connection Pooling**: Efficient database connections
- **Load Balancing**: Multiple server instances

### Monitoring and Analytics

- **Error Tracking**: Sentry or similar service
- **Performance Monitoring**: New Relic or DataDog
- **User Analytics**: Google Analytics or privacy-focused alternative
- **Uptime Monitoring**: Pingdom or similar service

## Scalability Planning

### Horizontal Scaling

- **Frontend**: CDN distribution and edge computing
- **Backend**: Load balancer with multiple instances
- **Database**: Read replicas and sharding strategy

### Vertical Scaling

- **Resource Allocation**: CPU and memory optimization
- **Database Optimization**: Query performance tuning
- **Caching Strategy**: Multi-level caching implementation

### Future Considerations

- **Microservices**: Potential migration to microservices architecture
- **GraphQL**: API layer optimization
- **Serverless**: Function-based architecture exploration
- **Progressive Web App**: Enhanced mobile experience

## Recent Updates (March 2025)

### Frontend Improvements

- **Build Optimization**: Resolved all ESLint warnings and build errors
- **Accessibility**: Fixed jsx-a11y/anchor-is-valid warnings
- **UI Enhancement**: Centered hero actions for better alignment
- **Code Cleanup**: Removed unused imports and CSS classes

### Technical Debt Resolution

- **Clean Build**: Eliminated all production build warnings
- **Accessibility Compliance**: Full WCAG 2.1 adherence
- **Performance**: Optimized bundle size and loading times
- **Maintainability**: Improved code organization and documentation

This architecture document serves as a comprehensive guide for developers, system administrators, and stakeholders involved in the Quantum Logics project.
