# Task Manager

A professional full-stack task management and performance tracking platform with Node.js/PostgreSQL backend and React/Tailwind frontend. Features real-time collaboration, automated workflows, and comprehensive analytics for team productivity monitoring.

## Key Features

###  Authentication & Authorization
- **Secure JWT Authentication**: Robust login/register system with role-based access control
- **Three-Tier Role System**: Admin, Team Lead, and Developer roles with distinct permissions

###  Role-Based Functionality

**Developer Features:**
- Update task progress with percentage tracking
- Submit verifiable proofs (images/links)
- Track work hours via Punch In/Punch Out system
- Claim and work on assigned tasks
- Submit work for team lead review

**Team Lead Features:**
- Create and assign tasks to developers
- Verify completed work (Approve/Rework functionality)
- Set deadlines and provide feedback
- Monitor team performance and task status
- Manage task distribution among present developers

**Admin Features:**
- Comprehensive performance analytics dashboard
- Real-time completion rate tracking
- Delay analysis and productivity metrics
- Team lead verification efficiency monitoring
- Detailed drill-down views for individual developer performance

###  Attendance & Time Tracking
- Real-time Punch In/Punch Out system
- Automatic daily hour calculation
- Present/Completed status tracking
- 24-hour automatic reset mechanism

###  Automated Workflows
- Intelligent status transitions (todo → in-progress → awaiting-review → done)
- Automatic field updates during approval/rework processes
- Submission limit enforcement (3 submissions max)
- Delay calculation based on due dates

###  Analytics & Reporting
- Visual completion rate indicators with progress bars
- On-time vs delayed task tracking
- Average delay calculations
- Team lead verification time metrics
- Individual developer performance breakdown

###  Data Management
- PostgreSQL database with relational integrity
- Automated cleanup of old tasks (30-day retention)
- Real-time synchronization using Socket.io
- Proper error handling and data validation

##  Tech Stack

### Backend
- **Runtime**: Node.js with Express.js framework
- **Database**: PostgreSQL with raw connection pooling
- **Authentication**: JWT (JSON Web Tokens)
- **Real-time**: Socket.io for live updates
- **Architecture**: RESTful API with role-based middleware

### Frontend
- **Framework**: React with Vite build tool
- **Styling**: Tailwind CSS for responsive design
- **State Management**: React hooks and context
- **Real-time**: Socket.io-client for WebSocket connections
- **Routing**: React Router for SPA navigation

### Database
- **Primary**: PostgreSQL with relational schema
- **Features**: Foreign keys, indexes, and data integrity
- **Maintenance**: Automated cleanup jobs and triggers

##  Role Hierarchy & Permissions

### 1. Admin (Highest Level)
- **Permissions**: Full analytics access, user management oversight
- **Restrictions**: Cannot create/assign tasks or verify work
- **Focus**: Performance monitoring, delay analysis, system metrics

### 2. Team Lead (Operational Level)
- **Permissions**: Task creation, assignment, verification, and rework requests
- **Capabilities**: Manage developer workload, set deadlines, approve/reject submissions
- **Tools**: Task distribution to present developers, performance tracking

### 3. Developer (Execution Level)
- **Permissions**: Claim tasks, update progress, submit work for review
- **Capabilities**: Progress tracking, proof submission, attendance logging
- **Limitations**: Submission cap of 3 attempts per task, requires approval for completion

##  Project Structure
```
├── backend/                 # Node.js API server
│   ├── database/           # Database configuration and schema
│   │   ├── db.js          # PostgreSQL connection pool
│   │   ├── schema.sql     # Database schema definition
│   │   └── migrate.js     # Migration utilities
│   ├── middleware/         # Authentication and authorization
│   │   ├── auth.js        # JWT verification and role checks
│   │   └── cors.js        # CORS configuration
│   ├── models/             # Database abstraction layer
│   │   ├── Task.js        # Task CRUD operations and business logic
│   │   └── User.js        # User management and authentication
│   ├── routes/             # API endpoints
│   │   ├── analytics.js   # Performance metrics and reporting
│   │   ├── attendance.js  # Punch system and time tracking
│   │   ├── auth.js        # Login/register endpoints
│   │   └── tasks.js       # Task management APIs
│   ├── sockets/            # Real-time communication
│   │   └── socket.js      # Socket.io event handlers
│   ├── utils/              # Helper functions
│   │   └── cleanup.js     # Automated maintenance tasks
│   ├── index.js            # Server entry point
│   ├── package.json        # Backend dependencies
│   └── package-lock.json   # Dependency lock file
│
├── frontend/               # React + Vite application
│   ├── scripts/            # Utility scripts
│   │   └── check_url.js   # URL validation helper
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   │   ├── AdminAnalytics.jsx     # Performance dashboard
│   │   │   ├── AdminSection.jsx       # Admin task management
│   │   │   ├── AttendanceCard.jsx     # Punch system UI
│   │   │   ├── DeveloperSearch.jsx    # Task discovery
│   │   │   ├── DeveloperSection.jsx   # Developer task view
│   │   │   ├── DeveloperUpdateModal.jsx # Progress submission
│   │   │   ├── EditModal.jsx          # Task editing
│   │   │   ├── TaskCard.jsx           # Individual task display
│   │   │   ├── TasksGrid.jsx          # Task listing layout
│   │   │   ├── Toast.jsx              # Notification system
│   │   │   ├── TopBar.jsx             # Navigation header
│   │   │   └── ViewModal.jsx          # Task details view
│   │   ├── pages/          # Main application pages
│   │   │   ├── Dashboard.jsx          # Main dashboard
│   │   │   ├── Forgot.jsx             # Password recovery
│   │   │   ├── Login.jsx              # Authentication
│   │   │   ├── Register.jsx           # User registration
│   │   │   └── Show.jsx               # Public task view
│   │   ├── services/       # API communication
│   │   │   ├── authService.js         # Authentication APIs
│   │   │   └── taskService.js         # Task management APIs
│   │   ├── utils/          # Helper functions
│   │   │   ├── auth.js                # Auth state management
│   │   │   └── protectedRoute.jsx     # Route protection
│   │   ├── App.jsx         # Main application component
│   │   ├── index.css       # Global styles
│   │   └── main.jsx        # Application entry point
│   ├── index.html          # HTML template
│   ├── package.json        # Frontend dependencies
│   ├── postcss.config.js   # PostCSS configuration
│   ├── tailwind.config.js  # Tailwind CSS configuration
│   └── vite.config.js      # Vite build configuration
│
├── .gitignore              # Git ignore rules
└── README.md               # Project documentation
```

## Prerequisites
- Node.js (v14+)
- PostgreSQL (v12+)
- npm or yarn

## Installation & Setup

### 1. Install PostgreSQL
- **Windows**: https://www.postgresql.org/download/windows/
- **Mac**: `brew install postgresql`
- **Linux**: `sudo apt-get install postgresql`

### 2. Create Database
```bash
psql -U postgres
CREATE DATABASE taskmanager;
```

### 3. Setup Backend
```bash
cd backend
npm install
```

Configure database connection in `database/db.js` or set environment variables:
```bash
export DB_HOST=localhost
export DB_PORT=5432
export DB_NAME=taskmanager
export DB_USER=postgres
export DB_PASSWORD=your_password
```

### 4. Run Database Schema
```bash
psql -U postgres -d taskmanager -f database/schema.sql
```

### 5. Start Backend Server
```bash
cd backend
npm start
```
Server runs on `http://localhost:5000`

### 6. Start Frontend Development
```bash
cd frontend
npm install
npm run dev
```
Frontend runs on `http://localhost:5173`

##  Database Schema Overview

### Core Tables

**users table**:
- Role-based access control (admin/teamlead/developer)
- Attendance tracking (punch_status, present/completed)
- Work hour accumulation and reset mechanisms
- User profile and authentication data

**tasks table**:
- Comprehensive task metadata (title, details, priority, due dates)
- Progress tracking (percentage, developer updates)
- Verification workflow fields (developer_status, teamlead_status, final_status)
- Proof storage (image URLs, external links)
- Rework feedback and submission counting
- Delay calculation and completion timestamps

### Task Status Workflow
1. **todo**: Initial state - task created but not started
2. **in-progress**: Developer has claimed and started work
3. **awaiting-review**: Developer submitted work for verification
4. **rework-required**: Team Lead requested changes/fixes
5. **done**: Final approval - task completed successfully

### Key Relationships
- Users can own multiple tasks (owner_email)
- Users can be assigned to tasks (assignee_email)
- Tasks track submission history and verification timestamps
- Attendance data linked to user productivity metrics

##  Automated Maintenance

### Data Cleanup
- **Task Archival**: Automatically removes tasks older than 30 days
- **Schedule**: Hourly background job processing
- **Purpose**: Maintain database performance and storage efficiency

### Attendance Reset
- **Daily Reset**: Punch status automatically resets every 24 hours
- **Timing**: Consistent daily cycle for accurate time tracking
- **Scope**: Resets present/completed status for all users

### Performance Optimization
- **Connection Pooling**: Efficient database connection management
- **Index Usage**: Optimized queries with proper indexing
- **Memory Management**: Automatic cleanup of expired sessions

##  Troubleshooting Guide

### Database Connection Issues
**Symptoms**: Connection refused, authentication failed

**Solutions**:
1. Verify PostgreSQL service is running: `pg_isready`
2. Check database credentials in `backend/database/db.js`
3. Confirm database exists: `psql -l`
4. Test connection manually: `psql -U postgres -d taskmanager`
5. Review PostgreSQL error logs for detailed diagnostics

### Port Conflicts
**Common Issues**:
- Backend port 5000 already in use
- Frontend port 5173 unavailable

**Resolutions**:
- Backend: Modify PORT environment variable
- Frontend: Vite automatically selects alternative ports
- Check for conflicting processes: `netstat -an | grep 5000`

### Authentication Problems
**JWT Issues**:
- Token expiration errors
- Invalid signature warnings
- Role permission denied

**Debug Steps**:
1. Verify JWT_SECRET environment variable
2. Check token expiration settings
3. Confirm user role assignments in database
4. Review browser console for auth errors

### Real-time Updates Not Working
**Socket.io Troubleshooting**:
1. Verify both frontend and backend servers are running
2. Check browser console for WebSocket connection errors
3. Confirm CORS settings allow WebSocket connections
4. Test network connectivity between client and server

### Performance Issues
**Slow Loading**:
1. Check database query performance
2. Verify connection pooling settings
3. Monitor server resource usage
4. Review network latency between components

### Guidelines
- Follow existing code structure and naming conventions
- Maintain consistent commit message format
- Write clear, descriptive pull request descriptions
- Ensure all tests pass before submitting
- Update documentation for new features

### Development Process
1. Fork the repository
2. Create feature branch from main
3. Implement changes with proper error handling
4. Test thoroughly across different scenarios
5. Submit pull request with detailed description

### Code Standards
- Use ESLint/Prettier for code formatting
- Follow React best practices and hooks guidelines
- Implement proper error boundaries
- Write meaningful variable and function names
- Include JSDoc comments for complex functions

## License
ISC
