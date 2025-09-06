# Joy Aviation Supplies (JAS) Web Application

[![Version](https://img.shields.io/badge/version-2.0-blue.svg)](https://github.com/Joy-Aviation/jas_project)
[![Django](https://img.shields.io/badge/Django-5.2-green.svg)](https://djangoproject.com/)
[![React](https://img.shields.io/badge/React-19.1.0-blue.svg)](https://reactjs.org/)
[![Python](https://img.shields.io/badge/Python-3.13+-yellow.svg)](https://python.org/)
[![License](https://img.shields.io/badge/license-MIT-orange.svg)](LICENSE)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
- [Maintenance & Troubleshooting](#maintenance--troubleshooting)
- [Development](#development)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

The Joy Aviation Supplies (JAS) Web Application is a comprehensive solution designed for aviation parts sourcing, inventory management, and RFQ (Request for Quote) processing. The system integrates with multiple supplier platforms through automated scrapers and provides a modern web interface for efficient parts management and sourcing operations.

### Key Capabilities

- **Parts Catalog Management**: Comprehensive database of aviation parts with detailed specifications
- **Advanced Search & Filtering**: Multi-criteria search with real-time filtering capabilities
- **Data Import/Export**: CSV/Excel support for bulk operations
- **Supplier Data Integration**: Automated data collection from multiple aviation suppliers
- **Real-time Monitoring**: Live status tracking of scrapers and data processing

## ✨ Features

### 🔍 Parts Management
- **Advanced Search Tool**: Search parts by multiple criteria with flexible input methods
- **Bulk Operations**: CSV upload/download for efficient data management
- **Part Details**: Comprehensive part information including pricing, availability, and specifications
- **Alternative Parts**: Cross-reference and suggest alternative part numbers
- **Price Tracking**: Historical pricing data and price break analysis

### 🤖 Automated Scraping
- **Multi-Supplier Support**: Integration with KLX, Aviall, Proponent, Monroe, and Aero Performance
- **Scheduled Operations**: Automated catalog updates and on-demand scraping
- **Real-time Monitoring**: Live status tracking and progress updates
- **Data Quality**: Automated data cleaning and normalization
- **Error Handling**: Robust error management and recovery

### 📈 Analytics & Reporting
- **Dashboard Views**: Real-time analytics and key performance indicators
- **Export Capabilities**: CSV/Excel export for all data views
- **Search Analytics**: Track search patterns and popular parts
- **Supplier Performance**: Monitor supplier response times and data quality

## 🏗️ Architecture

### System Components

```
┌─────────────────────────────────────────────────────────────┐
│                    JAS Web Application                      │
├─────────────────────────────────────────────────────────────┤
│  Frontend (React)          │  Backend (Django)             │
│  ├── Part Search           │  ├── API Layer                │
│  ├── RFQ Manager           │  ├── Data Models              │
│  ├── Scrapers Dashboard    │  ├── Business Logic           │
│  ├── Inventory Management  │  └── Database Layer           │
│  └── Analytics             │                               │
├─────────────────────────────────────────────────────────────┤
│                    JA-Scrapers (FastAPI)                   │
│  ├── KLX Scraper           │  ├── Monroe Scraper           │
│  ├── Aviall Scraper        │  ├── Proponent Scraper        │
│  └── Aero Performance      │  └── Celery Workers           │
├─────────────────────────────────────────────────────────────┤
│                    Database Layer                          │
│  ├── MySQL (Primary)       │  ├── AWS S3 Storage           │
│  └── Redis (Caching)       │                               │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **Data Collection**: Scrapers collect data from supplier websites
2. **Data Processing**: Raw data is cleaned, normalized, and validated
3. **Storage**: Processed data is stored in MySQL database
4. **API Layer**: Django REST API provides data access
5. **Frontend**: React application consumes APIs for user interface
6. **User Operations**: Search, filter, export, and manage parts data

## 🛠️ Technology Stack

### Backend
- **Framework**: Django 5.2 with Django REST Framework
- **Database**: MySQL (Production), SQLite (Development)
- **Authentication**: JWT-based authentication
- **API**: RESTful API with comprehensive documentation
- **Caching**: Redis for performance optimization
- **Task Queue**: Celery for background processing

### Frontend
- **Framework**: React 19.1.0 with Vite
- **UI Library**: Tailwind CSS for styling
- **State Management**: React Hooks and Context
- **Data Tables**: TanStack Table for advanced table functionality
- **File Processing**: Papa Parse for CSV handling
- **Routing**: React Router for navigation

### Scraping Infrastructure
- **Framework**: FastAPI for high-performance scraping
- **Scraping**: Scrapy with Playwright for dynamic content
- **Scheduling**: Celery Beat for automated tasks
- **Data Processing**: Pandas for data manipulation
- **Authentication**: JWT for secure API access

### DevOps & Deployment
- **Containerization**: Docker support (Coming Soon)
- **Environment Management**: Pyenv environments
- **Version Control**: Git with structured branching
- **CI/CD**: Not Conifgured Yet

## 🚀 Installation & Setup

### Prerequisites

- **Python**: 3.13+ (recommended)
- **Node.js**: 18+ (for frontend development)
- **MySQL**: 8.0+ (for production database)
- **Redis**: 6.0+ (for caching and task queue)
- **Git**: Latest version

### Quick Start

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Joy-Aviation/jas_project.git
   cd jas_project
   ```

2. **Backend Setup**
   ```bash
   # Create and activate virtual environment
   python -m venv jas-env

   #For Windows
   jas-env/Scripts/activate

   #For Linux
   source jas-env/bin/activate
   
   # Install dependencies
   cd jas_backend
   pip install -r requirements.txt
   
   # Configure environment variables
   nano .env
   # Add database credentials to .env file
   
   # Run migrations
   python manage.py migrate
   
   # Start development server
   python manage.py runserver
   ```

3. **Frontend Setup**
   ```bash
   cd jas_frontend
   npm install
   
   # Configure environment
   nano .env
   # Edit API URL to .env
   
   # Start development server
   npm run dev
   ```

4. **JA-Scrapers Setup**
   ```bash
   cd ../JA-Scrapers
   pip install -r requirements.txt
   
   # Start FastAPI server
   uvicorn main:app --reload --port 8001
   ```

### Environment Configuration

Create a `.env` file in the `jas_backend` directory:

```env
# Database Configuration
DB_NAME=jas_database
DB_USER=your_username
DB_PASSWORD=your_password
DB_HOST=localhost
DB_PORT=3306

# Django Settings
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# API Configuration
ROTOBULL_AUTH=Bearer your-auth-token

# Redis Configuration
REDIS_URL=redis://localhost:6379/0
```

Create a `.env` file in the `jas_frontend` directory:

```env
VITE_API_URL=http://localhost:8000/api/
VITE_SCRAPERS_URL=http://localhost:8001/
```

## 📖 Usage Guide

### Parts Search

1. **Navigate to Search Tool**
   - Access the "Part Search Tool" from the main navigation
   - Choose between text input or CSV upload methods

2. **Text Input Method**
   - Enter part numbers separated by commas, spaces, or newlines
   - Click "Search Parts" to execute the search
   - View results in the interactive table

3. **CSV Upload Method**
   - Upload a CSV file with part numbers in the first column
   - The system automatically validates and processes the file
   - Download results as CSV for further analysis

### RFQ Management

1. **Access RFQ Manager**
   - Navigate to the "RFQ Manager" tab
   - Download templates for consistent data entry

2. **Upload RFQ Data**
   - Use the provided template format
   - Upload CSV files with required columns
   - Process and validate data automatically

3. **Export Results**
   - Generate comprehensive reports
   - Export data in multiple formats
   - Track RFQ status and progress

### Scrapers Management

1. **Monitor Scrapers**
   - View real-time status of all scrapers
   - Monitor scheduled and on-demand operations
   - Track data collection progress

2. **Run Scrapers**
   - Execute on-demand scraping operations
   - Configure scraper parameters
   - Monitor output and results

3. **Data Quality**
   - Review scraped data quality
   - Validate data completeness
   - Export processed data

## 🔌 API Documentation

### Core Endpoints

#### Parts Management
- `GET /api/catalogue/` - List all parts with pagination
- `GET /api/catalogue/{id}/` - Get detailed part information
- `POST /api/search-parts/` - Search parts by criteria
- `POST /api/import/parts-prices/csv/` - Import parts data from CSV
- `POST /api/import/parts/json/` - Import parts data from JSON

#### RFQ Management
- `GET /api/rfq/` - List RFQ records
- `POST /api/rfq/` - Create new RFQ
- `PUT /api/rfq/{id}/` - Update RFQ status
- `GET /api/rfq/{id}/items/` - Get RFQ line items

#### Scrapers Integration
- `GET /scrapers/status/` - Get scraper status
- `POST /scrapers/run/` - Execute scraper
- `GET /scrapers/output/{id}/` - Get scraper output

### Authentication

The API uses JWT-based authentication. Include the token in the Authorization header:

```bash
curl -H "Authorization: Bearer jwt-token" \
     http://localhost:8000/api/catalogue/
```

### Rate Limiting

- **Search Operations**: 100 requests per minute
- **Import Operations**: 10 requests per minute
- **Scraper Operations**: 5 requests per minute

## 👨‍💻 Development

### Development Environment Setup

1. **Fork and Clone**
   ```bash
   git clone https://github.com/your-username/jas_project.git
   cd jas_project
   ```

2. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Install Development Dependencies**
   ```bash
   # Backend
   pip install -r requirements-dev.txt
   
   # Frontend
   npm install --dev
   ```

### Code Standards

1. **Python/Django**
   - Follow PEP 8 style guidelines
   - Use type hints where appropriate
   - Write comprehensive docstrings
   - Maintain 80%+ test coverage

2. **JavaScript/React**
   - Use ESLint and Prettier for code formatting
   - Follow React best practices
   - Write unit tests with Jest
   - Use TypeScript for new components

3. **Git Workflow**
   - Use conventional commit messages
   - Create pull requests for all changes
   - Require code reviews for merges
   - Keep commits atomic and focused

## 🚀 Deployment

### Production Deployment

1. **Server Requirements**
   - Ubuntu 20.04+ or CentOS 8+
   - 4GB+ RAM, 2+ CPU cores
   - 50GB+ storage space
   - MySQL 8.0+ and Redis 6.0+

2. **Django Backend**
   
    Coming Soon

3. **React Frontend**

    Coming Soon

4. **JA-Scrapers**
   ```bash
   # Install production dependencies
   pip install uvicorn[standard]
   
   # Start with Uvicorn
   uvicorn main:app --host 0.0.0.0 --port 8001 --workers 4
   ```

### Docker Deployment

   Coming Soon

### Environment-Specific Configuration

- **Development**: Use SQLite and local file storage
- **Staging**: Use MySQL with limited resources
- **Production**: Use MySQL with Redis caching and CDN

## 🔧 Maintenance & Troubleshooting

### Common Issues

#### Database Connection Errors
```bash
# Check MySQL service
sudo systemctl status mysql

# Verify connection
mysql -u username -p -h localhost

# Check Django database configuration
python manage.py dbshell
```

#### Frontend Build Issues
```bash
# Clear node modules and reinstall
rm -rf node_modules package-lock.json
npm install

# Check Node.js version
node --version  # Should be 18+

# Clear Vite cache
rm -rf .vite
npm run dev
```

#### Scraper Failures
```bash
# Check scraper logs
tail -f klx.log

# Verify network connectivity
curl -I https://supplier-website.com

# Check Celery workers
celery -A celery_worker worker --loglevel=info
```

### Performance Optimization

1. **Database Optimization**
   - Add appropriate indexes for frequently queried fields
   - Use database connection pooling
   - Implement query optimization

2. **Caching Strategy**
   - Enable Redis caching for API responses
   - Implement browser caching for static assets
   - Use CDN for global content delivery

3. **Frontend Optimization**
   - Implement code splitting and lazy loading
   - Optimize bundle size with tree shaking
   - Use service workers for offline functionality

### Monitoring & Logging

1. **Application Logs**
   ```bash
   # Django logs
   tail -f logs/django.log
   
   # Scraper logs
   tail -f logs/scrapers.log
   
   # Nginx logs
   tail -f /var/log/nginx/access.log
   ```

2. **Health Checks**
   - API health endpoint: `GET /api/health/`
   - Database connectivity: `GET /api/health/db/`
   - Scraper status: `GET /scrapers/health/`

3. **Performance Monitoring**
   - Monitor response times and error rates
   - Track database query performance
   - Monitor memory and CPU usage


### Testing

1. **Backend Tests**
   ```bash
   # Run all tests
   python manage.py test
   
   # Run specific test
   python manage.py test jas_app.tests.test_models
   
   # Run with coverage
   coverage run --source='.' manage.py test
   coverage report
   ```

2. **Frontend Tests**
   ```bash
   # Run unit tests
   npm test
   
   # Run with coverage
   npm run test:coverage
   
   # Run E2E tests
   npm run test:e2e
   ```

3. **Integration Tests**
   ```bash
   # Test API endpoints
   python manage.py test api.tests.test_integration
   
   # Test scraper functionality
   python -m pytest scrapers/tests/
   ```

### Contributing Guidelines

1. **Feature Requests**
   - Describe the use case and benefits (On Notion)
   - Provide mockups or examples
   - Consider backward compatibility

2. **Pull Requests**
   - Reference related issues
   - Include tests for new functionality
   - Update documentation as needed
   - Ensure all checks pass

## 📚 Additional Resources

### Documentation
- [Django Documentation](https://docs.djangoproject.com/)
- [React Documentation](https://reactjs.org/docs/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Scrapy Documentation](https://docs.scrapy.org/)

### Related Projects
- [JA-Scrapers](https://github.com/Joy-Aviation/JA-Scrapers) - Automated data collection system

### Support
- **Email**: hammadt451@gmail.com

## 🙏 Acknowledgments

- **Development Team**: Nascon
- **Open Source Libraries**: Django, React, FastAPI, Scrapy, and all contributing developers

---

**Joy Aviation Supplies Web Application** - Streamlining aviation parts sourcing and management since 2024.