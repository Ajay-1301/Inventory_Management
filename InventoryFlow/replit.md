# Inventory Management System

## Overview

A complete web-based Inventory Management System for tracking products, storage locations, and product movements across different warehouses. The system helps manage inventory by recording when products are moved between locations and provides reporting capabilities to view current stock levels.

**Current Status**: Fully functional client-side application built with HTML, CSS, and JavaScript, using localStorage for data persistence. Flask and MySQL reference implementations provided as text files for hiring test submission.

**Created**: October 6, 2025

## User Preferences

- Preferred communication style: Simple, everyday language
- Implementation approach: HTML, CSS, and JavaScript with localStorage
- Flask and MySQL provided as reference text files only

## Recent Changes

**October 6, 2025**:
- Created complete inventory management web application
- Implemented product management (add, edit, delete, view)
- Implemented location management (add, edit, delete, view)
- Implemented product movement tracking with inward, outward, and transfer capabilities
- Created stock balance report with real-time calculation
- Added Bootstrap 5 styling with custom CSS
- Created Flask+MySQL reference implementation files:
  - reference_flask_app.txt - Complete Flask application code
  - reference_mysql_schema.txt - MySQL database schema with sample data
  - reference_requirements.txt - Python dependencies
- Set up Python HTTP server to serve static files on port 5000

## Project Architecture

### Frontend Architecture

**Technology Stack**: Vanilla HTML, CSS, and JavaScript
- Pure client-side application with no backend dependencies
- Multi-page architecture with separate HTML files for each feature area:
  - `index.html` - Dashboard/home page with navigation cards
  - `products.html` - Product management interface
  - `locations.html` - Location management interface  
  - `movements.html` - Product movement tracking
  - `report.html` - Stock balance reporting

**Design Pattern**: Page-based navigation with shared Bootstrap navbar
- Bootstrap 5.3.0 framework for responsive UI components
- Custom CSS (`styles.css`) for consistent branding and styling
- Form-based CRUD operations for all entities
- Real-time updates using JavaScript event listeners

### Data Storage Solution

**Current Implementation**: Browser localStorage
- All data persisted in browser's localStorage as JSON strings
- Three primary data collections:
  - `products` - Product catalog with product_id, name, description
  - `locations` - Storage location registry with location_id, name, address
  - `movements` - Movement transaction log with timestamps

**Data Access Layer** (`app.js`):
- Centralized functions for CRUD operations:
  - `getProducts()`, `addProduct()`, `updateProduct()` for products
  - `getLocations()`, `addLocation()`, `updateLocation()` for locations
  - `getMovements()`, `addMovement()` for movement tracking
- Delete operations available in product and location pages
- Data persists across browser sessions until manually cleared

### Data Model

**Product Entity**:
- `product_id` (string, primary key, auto-generated)
- `name` (string, required)
- `description` (text, optional)

**Location Entity**:
- `location_id` (string, primary key, auto-generated)
- `name` (string, required)
- `address` (text, optional)

**ProductMovement Entity**:
- `movement_id` (integer, auto-generated timestamp-based)
- `timestamp` (ISO datetime string)
- `from_location` (foreign key to Location, nullable for new inventory)
- `to_location` (foreign key to Location, nullable for outbound/sold items)
- `product_id` (foreign key to Product, required)
- `qty` (integer, required, positive)

**Movement Logic**:
- NULL `from_location` = new inventory entering the system
- NULL `to_location` = product leaving the system (sold/disposed)
- Both locations set = transfer between warehouses
- Quantity tracking allows for partial movements

### Reporting Architecture

**Stock Balance Calculation**:
- Aggregate movements by product and location
- Inbound movements (to_location) add to location stock
- Outbound movements (from_location) subtract from location stock
- Real-time calculation from complete movement transaction log
- Sorted alphabetically by product name, then location name

## Files Structure

```
/
├── index.html                    # Home page with dashboard
├── products.html                 # Product management page
├── locations.html                # Location management page
├── movements.html                # Product movement tracking page
├── report.html                   # Stock balance report page
├── app.js                        # Shared JavaScript data management
├── styles.css                    # Custom CSS styling
├── reference_flask_app.txt       # Flask backend reference implementation
├── reference_mysql_schema.txt    # MySQL database schema with sample data
└── reference_requirements.txt    # Python dependencies for Flask app
```

## External Dependencies

### Frontend Libraries

**Bootstrap 5.3.0** (CDN):
- CSS: `https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css`
- JS: `https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js`
- Purpose: Responsive UI framework, grid system, form components, navigation, tables, cards

### Browser APIs

**localStorage API**:
- Primary data persistence mechanism
- Stores JSON-serialized data collections
- Limited to ~5-10MB depending on browser
- Data persists until explicitly cleared

## Reference Implementation (Flask + MySQL)

**Purpose**: Provided as text files for hiring test submission

**Files**:
- `reference_flask_app.txt` - Complete Flask application with:
  - SQLAlchemy ORM models for Product, Location, ProductMovement
  - Full CRUD routes for all entities
  - RESTful API endpoints
  - Stock balance report calculation
  - Database relationship handling

- `reference_mysql_schema.txt` - MySQL database schema with:
  - Table definitions with proper foreign keys
  - Indexes for query optimization
  - Sample data (20+ movements as per requirement)
  - Stock balance query example

- `reference_requirements.txt` - Python dependencies:
  - Flask 3.0.0
  - Flask-SQLAlchemy 3.1.1
  - PyMySQL 1.1.0
  - SQLAlchemy 2.0.23
  - Installation instructions

## Development Server

**Current Setup**:
- Python 3.11 HTTP server
- Command: `python -m http.server 5000`
- Serves static HTML files
- Accessible on port 5000

## Features

### Working Features (HTML/CSS/JS)

1. **Product Management**
   - Add new products with name and description
   - Edit existing products
   - Delete products
   - View all products in table format
   - Auto-generated product IDs

2. **Location Management**
   - Add new locations/warehouses with name and address
   - Edit existing locations
   - Delete locations
   - View all locations in table format
   - Auto-generated location IDs

3. **Product Movement Tracking**
   - Record inward movements (new stock arrival)
   - Record outward movements (sales, disposals)
   - Record transfers between locations
   - Dropdown selection for products and locations
   - Quantity input with validation
   - Timestamp recording
   - Complete movement history view

4. **Stock Balance Report**
   - Real-time calculation of current stock levels
   - Shows product name, location name, and quantity
   - Filters out zero or negative balances
   - Sorted by product and location
   - Clean table format with badges

### Reference Implementation Features (Flask/MySQL)

- Complete database-backed implementation
- All frontend features with persistent storage
- RESTful API endpoints for all operations
- Database relationships with foreign keys
- Transaction logging with timestamps
- Production-ready code structure

## Future Enhancements

Potential features for next phase:
- Backend API integration to replace localStorage
- User authentication and authorization
- Product search and filtering
- Stock alert notifications for low inventory
- Data export functionality (CSV/PDF)
- Barcode scanning integration
- Multi-user support with role-based access
- Audit trail for all changes
- Dashboard with charts and statistics
