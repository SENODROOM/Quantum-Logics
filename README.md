# Quantum Logics

A comprehensive software house platform featuring modern web technologies, showcasing products, services, and career opportunities with a focus on clean design and accessibility.

## Overview

Quantum Logics is a full-stack web application that serves as a modern software company website. It features product showcases, job application systems, admin dashboard with real-time statistics, and demonstrates best practices in web development including accessibility compliance and clean build processes.

## Project Structure

```
Quantum-Logics/
├── backend/              # Backend API service (submodule)
├── frontend/             # React frontend application (submodule)
├── docs/                 # Comprehensive documentation
├── .gitmodules           # Git submodules configuration
├── .gitignore            # Git ignore rules
└── LICENSE               # MIT License
```

## Components

### Backend

The backend provides RESTful API services with Express.js and MongoDB integration.

**Key features:**
- RESTful API endpoints
- JWT authentication system
- MongoDB database with Mongoose ODM
- Email notifications with Nodemailer
- Admin dashboard data endpoints
- Job application management

To work with the backend:

```bash
cd backend
# Follow backend-specific setup instructions
```

### Frontend

The frontend is a modern React application with emphasis on accessibility and user experience.

**Key features:**
- React 19.2.4 with modern hooks
- Responsive design with pure CSS
- Accessibility compliance (WCAG 2.1)
- Product showcase and company information
- Job application system
- Real-time statistics dashboard
- Clean build with no warnings

To work with the frontend:

```bash
cd frontend
# Follow frontend-specific setup instructions
```

## Getting Started

### Prerequisites

- Git (with submodule support)
- Node.js (recommended version TBD based on backend/frontend requirements)
- npm or yarn package manager
- Any additional language/runtime requirements specific to backend and frontend

### Installation

1. Clone the repository with submodules:

```bash
git clone --recurse-submodules https://github.com/SENODROOM/Quantum-Logics.git
cd Quantum-Logics
```

If you've already cloned without submodules, initialize them:

```bash
git submodule update --init --recursive
```

2. Install backend dependencies:

```bash
cd backend
npm install  # or yarn install
```

3. Install frontend dependencies:

```bash
cd ../frontend
npm install  # or yarn install
```

### Development Setup

Each component has its own setup requirements. Refer to the respective README files in the `backend/` and `frontend/` directories for specific configuration steps.

**Typical workflow:**

```bash
# Terminal 1: Start the backend
cd backend
npm run dev

# Terminal 2: Start the frontend
cd frontend
npm run dev
```

## Usage

Once both services are running, you can access:

- **Frontend:** http://localhost:3000 (typically)
- **Backend API:** http://localhost:5000 (typically, adjust based on your configuration)

## Development Workflow

### Updating Submodules

To fetch the latest changes from both submodules:

```bash
git submodule update --recursive --remote
```

### Committing Changes

When making changes to submodules:

```bash
# From root directory
cd backend
git add .
git commit -m "Your message"
git push

cd ../frontend
git add .
git commit -m "Your message"
git push

# Update parent repo references
cd ..
git add .
git commit -m "Update submodules"
git push
```

## Building for Production

### Backend Build

```bash
cd backend
npm run build
```

### Frontend Build

```bash
cd frontend
npm run build
```

Refer to each component's README for deployment instructions.

## Environment Variables

Each component may require its own `.env` file. Check the backend and frontend directories for example configuration files (typically `.env.example`).

**Common variables:**
- `API_URL` - Backend API endpoint
- `PORT` - Service port
- `NODE_ENV` - Environment (development, staging, production)

## Recent Updates (March 2025)

### ✅ Build Quality Improvements
- **Clean Build**: Eliminated all ESLint warnings and build errors
- **Accessibility**: Fixed jsx-a11y compliance issues
- **Code Quality**: Removed unused imports and optimized components
- **UI Enhancement**: Improved hero section alignment and responsiveness

### 📚 Documentation Updates
- **Architecture**: Comprehensive system architecture documentation
- **Contributing**: Updated guidelines with build requirements
- **FAQ**: Added troubleshooting section for common build issues
- **Changelog**: Detailed release notes and version history

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

**Build Requirements**: All contributions must pass:
- Clean frontend build (`npm run build` with no warnings)
- Accessibility compliance checks
- Code quality standards

When contributing to submodules, ensure changes are well-tested and documented.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Copyright (c) 2026 Muhammad Saad Amin - Canvas Market

## Support & Documentation

For detailed information about specific components:

- **Comprehensive Documentation:** See `docs/` directory
- **Backend Documentation:** See `backend/README.md`
- **Frontend Documentation:** See `frontend/README.md`

For issues, questions, or suggestions, please open an issue on the GitHub repository.

## Acknowledgments

Special thanks to all contributors and the open-source community for making this project possible.

---

**Happy coding! 🚀**
