# Database Setup Guide

## 🎯 Overview

This guide explains how to set up the Mother India Stock Management database from scratch. The system automatically creates all tables, indexes, and default data when you start the server.

## ✨ Automatic Initialization

**The database initializes automatically when you start the server!**

Just run:
```bash
cd server
npm start
```

The server will automatically:
1. ✅ Create all database tables
2. ✅ Run all migrations
3. ✅ Add all performance indexes
4. ✅ Create default warehouses
5. ✅ Create default users (admin, manager, staff)

## 🆕 Fresh Database Setup

### Option 1: Automatic (Recommended)

1. **Create an empty PostgreSQL database:**
   ```sql
   CREATE DATABASE mother_india;
   ```

2. **Configure environment variables:**
   
   Create or update `server/.env`:
   ```env
   DB_NAME=mother_india
   DB_USER=postgres
   DB_PASSWORD=your_password
   DB_HOST=localhost
   DB_PORT=5432
   ```

3. **Start the server:**
   ```bash
   cd server
   npm start
   ```

That's it! The server will automatically initialize everything.

### Option 2: Manual Initialization Script

If you want to initialize without starting the server:

```bash
cd server
npm run init-fresh
```

This runs the `init_fresh_database.js` script which:
- Creates all tables
- Runs all migrations
- Adds all indexes
- Creates default data

## 📊 What Gets Created Automatically

### Tables Created:
1. **users** - User accounts (admin, manager, staff)
2. **warehouses** - Storage facilities
3. **varieties** - Rice varieties
4. **kunchinittus** - Storage locations within warehouses
5. **arrivals** - Stock movements (purchase, shifting, production)
6. **outturns** - Production batches
7. **rice_productions** - Rice production records
8. **packagings** - Packaging types
9. **purchase_rates** - Purchase rate calculations
10. **hamali_rates** - Labor rates
11. **hamali_entries** - Labor entries
12. **opening_balances** - Opening stock balances
13. **balance_audit_trails** - Stock audit trails

### Indexes Created:
- **10 comprehensive performance indexes** for optimal query speed
- Composite indexes for multi-column queries
- Partial indexes for filtered queries
- Covering indexes for pagination

### Default Data Created:

**Default Warehouses:**
- Warehouse 1 (W1)
- Warehouse 2 (W2)
- Warehouse 3 (W3)

**Default Users:**
- **Admin**: username: `admin`, password: `admin123`
- **Manager**: username: `manager`, password: `manager123`
- **Staff**: username: `staff`, password: `staff123`

⚠️ **Important**: Change these default passwords after first login!

## 🔄 Recreating the Database

If you need to recreate the database from scratch:

### Step 1: Drop and Recreate Database

```sql
-- Connect to PostgreSQL
psql -U postgres

-- Drop existing database
DROP DATABASE IF EXISTS mother_india;

-- Create fresh database
CREATE DATABASE mother_india;

-- Exit psql
\q
```

### Step 2: Start Server (Automatic Initialization)

```bash
cd server
npm start
```

The server will detect the empty database and automatically:
1. Create all tables
2. Run all migrations
3. Add all indexes
4. Create default data

### Step 3: Verify

Check the server logs for:
```
✅ Database connection established successfully.
✅ Initial database schema created.
✅ Migrations completed.
✅ Default warehouses created
✅ Default users created
🚀 Mother India Stock Management Server running on port 5000
```

## 🛠️ Manual Migration Commands

If you need to run specific operations:

### Initialize Fresh Database:
```bash
npm run init-fresh
```

### Run Migrations Only:
```bash
npm run migrate
```

### Reset Database (Dangerous!):
```bash
npm run reset-db
```
⚠️ This will delete all data!

## 📋 Verification Checklist

After initialization, verify:

- [ ] Server starts without errors
- [ ] Can login with default admin credentials
- [ ] Dashboard loads successfully
- [ ] Can view warehouses list
- [ ] Can view users list
- [ ] No errors in server logs

## 🔍 Troubleshooting

### Issue: "Database connection failed"

**Solution:**
1. Check PostgreSQL is running
2. Verify database exists: `psql -U postgres -l`
3. Check credentials in `.env` file
4. Test connection: `psql -U postgres -d mother_india`

### Issue: "Table already exists"

**Solution:**
This is normal! The system checks if tables exist before creating them. You'll see warnings but the server will continue.

### Issue: "Migration failed"

**Solution:**
1. Check server logs for specific error
2. Migrations are idempotent (safe to run multiple times)
3. If needed, drop and recreate database

### Issue: "Default users not created"

**Solution:**
1. Check if users table exists
2. Manually run: `npm run init-db`
3. Check server logs for errors

## 🎯 Database Schema

### Core Tables:

```
users
├── id (PK)
├── username (unique)
├── password (hashed)
├── role (admin/manager/staff)
└── isActive

warehouses
├── id (PK)
├── code (unique)
├── name
└── isActive

kunchinittus
├── id (PK)
├── code (unique)
├── name
├── warehouseId (FK)
└── varietyId (FK)

arrivals
├── id (PK)
├── slNo (unique)
├── date
├── movementType
├── variety
├── bags
├── netWeight
├── status
└── [many more fields...]

outturns
├── id (PK)
├── code (unique)
├── allottedVariety
├── type (Raw/Steam)
└── createdBy (FK)
```

## 📈 Performance Features

The database includes:

- **10 comprehensive indexes** for fast queries
- **Optimized connection pool** (5-20 connections)
- **Query timeouts** (30s statement, 60s idle)
- **Automatic query logging** for slow queries (>100ms)

## 🔐 Security Notes

1. **Change default passwords** immediately after setup
2. **Use strong passwords** in production
3. **Restrict database access** to application server only
4. **Enable SSL** for database connections in production
5. **Regular backups** are essential

## 📚 Additional Resources

- **Performance Optimization**: See `PERFORMANCE_OPTIMIZATION.md`
- **Quick Start**: See `QUICK_START_PERFORMANCE.md`
- **API Documentation**: See `README.md`

## 🆘 Support

If you encounter issues:

1. Check server logs for errors
2. Verify PostgreSQL is running
3. Check database credentials
4. Review this guide
5. Check migration files in `server/migrations/`

---

**Last Updated**: November 17, 2025  
**Database Version**: 1.0.0 with Performance Optimizations
