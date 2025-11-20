# Mother India Stock Management System

Complete stock management system for industrial rice mill operations with advanced inventory tracking, approval workflows, and comprehensive reporting.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Node](https://img.shields.io/badge/node-16.x+-green)
![PostgreSQL](https://img.shields.io/badge/postgresql-12.x+-blue)
![React](https://img.shields.io/badge/react-18.x-61dafb)

---

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Installation](#installation)
- [Default Credentials](#default-credentials)
- [System Architecture](#system-architecture)
- [Documentation](#documentation)
- [Support](#support)

---

## ✨ Features

### Core Functionality
- **📦 Arrivals Management** - Record purchase and shifting transactions
- **🏭 Production Tracking** - Outturn and by-product management
- **📊 Real-time Dashboard** - Live statistics and quick actions
- **📍 Location Management** - Warehouses, Kunchinittus, and Varieties
- **📈 Kunchinittu Ledger** - Comprehensive stock tracking with inward/outward movements
- **📑 Paddy Stock Reports** - Daily ledger with running balances

### Advanced Features
- ✅ **Role-Based Access Control** - Staff, Manager, and Admin roles
- 🔄 **Approval Workflow** - Multi-level approval system
- 📤 **Export Capabilities** - CSV and PDF export for all reports
- 🔐 **Secure Authentication** - JWT-based authentication
- ⚡ **Performance Optimized** - Handles 200,000+ records efficiently
- 🌐 **LAN Support** - Multi-user network access

### Business Intelligence
- Real-time stock calculations
- Bifurcation by variety and location
- Cutting and moisture percentage tracking
- Broker and lorry tracking
- Opening balance management
- Audit trail for all transactions

---

## 🛠️ Tech Stack

### Backend
- **Runtime**: Node.js 16+
- **Framework**: Express.js
- **Database**: PostgreSQL 12+
- **ORM**: Sequelize
- **Authentication**: JWT with bcrypt
- **Export**: CSV (@json2csv/plainjs), PDF (pdfkit)

### Frontend
- **Framework**: React 18.x with TypeScript
- **Styling**: Styled Components
- **HTTP Client**: Axios
- **State Management**: Context API
- **Routing**: React Router v6

---

## 🚀 Quick Start

### Prerequisites
- Node.js 16.x or higher
- PostgreSQL 12.x or higher
- 4GB RAM minimum

### Installation in 3 Steps

```bash
# 1. Install dependencies
npm run install-deps

# 2. Create database
psql -U postgres
CREATE DATABASE mother_india;
\q

# 3. Run the application
npm run dev
```

The application will be available at:
- **Frontend**: http://localhost:3000
- **Backend**: http://localhost:5000

---

## 📖 Installation

For detailed installation instructions, see:

- **[INSTALLATION_GUIDE.md](./INSTALLATION_GUIDE.md)** - Complete installation guide for single computer
- **[LAN_INSTALLATION_GUIDE.md](./LAN_INSTALLATION_GUIDE.md)** - Network setup for multiple computers

### Basic Setup

1. **Install Node.js**
   - Download from https://nodejs.org/
   - Version 16.x or higher required

2. **Install PostgreSQL**
   - Download from https://www.postgresql.org/
   - Remember your password (default in config: `12345`)

3. **Install Application**
   ```bash
   npm run install-deps
   ```

4. **Create Database**
   ```sql
   CREATE DATABASE mother_india;
   ```

5. **Start Application**
   ```bash
   npm run dev
   ```

---

## 🔑 Default Credentials

After installation, login with these accounts:

| Role | Username | Password | Permissions |
|------|----------|----------|-------------|
| **Admin** | `ashish` | `ashish789` | Full system access |
| **Manager** | `rohit` | `rohit456` | View and approve records |
| **Staff** | `staff` | `staff123` | Create and edit records |

**⚠️ Important**: Change these passwords immediately after first login!

---

## 🏗️ System Architecture

### Database Schema
- **users** - User accounts and roles
- **warehouses** - Storage locations
- **kunchinittus** - Sub-locations within warehouses
- **varieties** - Rice varieties
- **arrivals** - All stock transactions
- **outturns** - Production records
- **byproducts** - By-product tracking
- **opening_balances** - Initial stock balances

### Application Structure
```
ashishmill/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/    # Reusable components
│   │   ├── contexts/      # React contexts
│   │   ├── pages/         # Page components
│   │   └── index.tsx      # Entry point
│   └── package.json
│
├── server/                # Node.js backend
│   ├── config/           # Database configuration
│   ├── middleware/       # Auth middleware
│   ├── models/           # Sequelize models
│   ├── routes/           # API routes
│   ├── services/         # Business logic
│   └── index.js          # Server entry point
│
└── package.json          # Root package
```

---

## 📚 Documentation

### Installation Guides
- **[INSTALLATION_GUIDE.md](./INSTALLATION_GUIDE.md)** - Single computer setup
- **[LAN_INSTALLATION_GUIDE.md](./LAN_INSTALLATION_GUIDE.md)** - Network/LAN setup

### Available Commands

#### Root Directory
```bash
npm run install-deps    # Install all dependencies
npm run dev            # Run both frontend and backend
```

#### Backend (server/)
```bash
npm start              # Start backend server
npm run init-db        # Initialize database
```

#### Frontend (client/)
```bash
npm start              # Start development server
npm run build          # Build for production
```

---

## 🎯 Usage

### 1. Dashboard
- View today's arrivals count
- Check pending approvals
- Monitor total stock in kg
- See active warehouses count

### 2. Arrivals
- **Purchase Entry** - Record new stock purchases
- **Shifting Entry** - Move stock between locations
- **Production Shifting** - Record production output

### 3. Records
- View all arrivals by date
- Filter by movement type
- Approve/reject pending records
- Edit or delete entries

### 4. Kunchinittu Ledger
- View stock movement for each Kunchinittu
- See inward and outward transactions
- Calculate remaining stock
- Export to PDF

### 5. Locations
- Manage warehouses
- Create and edit Kunchinittus
- Define varieties
- Link locations in chain

---

## 🔧 Configuration

### Database Configuration
Edit `server/config/database.js`:
```javascript
{
  username: 'postgres',
  password: '12345',      // Change this
  database: 'mother_india',
  host: 'localhost',
  port: 5432
}
```

### Environment Variables
Create `.env` in server directory:
```env
NODE_ENV=development
PORT=5000
CLIENT_URL=http://localhost:3000
JWT_SECRET=your_secret_key_here
```

---

## 🌐 LAN Setup

For multi-computer access:

1. Set static IP on server computer (e.g., `192.168.1.100`)
2. Update `client/.env`:
   ```env
   REACT_APP_API_URL=http://192.168.1.100:5000
   ```
3. Configure firewall to allow ports 3000, 5000, 5432
4. Access from client computers: `http://192.168.1.100:3000`

See **[LAN_INSTALLATION_GUIDE.md](./LAN_INSTALLATION_GUIDE.md)** for complete instructions.

---

## 🐛 Troubleshooting

### Common Issues

**Port already in use**
```bash
# Windows
Get-Process -Name node | Stop-Process -Force

# Linux/macOS
killall node
```

**Database connection failed**
- Verify PostgreSQL is running
- Check credentials in `server/config/database.js`
- Ensure database `mother_india` exists

**Frontend blank page**
- Check browser console (F12)
- Verify backend is running
- Clear browser cache

**Can't access from network**
- Check firewall settings
- Verify server IP address
- Ensure on same network

---

## 📊 Performance

System is optimized for:
- ✅ 200,000+ records
- ✅ Multiple concurrent users
- ✅ Fast search and filtering
- ✅ Efficient PDF generation
- ✅ Real-time data updates

### Database Indexes
Automatic indexes on:
- Dates (for fast date-range queries)
- Kunchinittu IDs (for ledger calculations)
- Status fields (for approval workflows)
- Foreign keys (for joins)

---

## 🔒 Security

- JWT-based authentication
- Role-based access control
- Password hashing with bcrypt
- SQL injection prevention (Sequelize ORM)
- Rate limiting on API endpoints
- Input validation and sanitization

---

## 📝 License

Proprietary - Mother India Mill
All rights reserved.

---

## 👥 Support

For technical support or questions:
- Check the installation guides
- Review troubleshooting sections
- Contact system administrator

---

## 🎉 Getting Started

1. Follow the [INSTALLATION_GUIDE.md](./INSTALLATION_GUIDE.md)
2. Login with default credentials
3. Change passwords for security
4. Create locations (Warehouses → Varieties → Kunchinittus)
5. Start entering arrivals data
6. Generate reports from Kunchinittu Ledger

---

**Made with ❤️ for Mother India Mill**

*Version 1.0.0 - October 2025*
