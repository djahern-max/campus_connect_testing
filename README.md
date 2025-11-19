# 🎓 CampusConnect Backend

**A modern FastAPI backend for connecting students with colleges and scholarship opportunities**

[![Tests](https://img.shields.io/badge/tests-94%20passing-brightgreen)](tests/)
[![Python](https://img.shields.io/badge/python-3.11-blue)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109+-00a393)](https://fastapi.tiangolo.com/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

---

## 📊 Project Status

- **Total Tests:** 96 (94 passing, 2 skipped)
- **Test Coverage:** Comprehensive integration and unit testing
- **Backend Status:** Production-ready
- **Frontend:** In development

---

## 🏗️ Architecture

CampusConnect is built with a modern, scalable architecture:

- **Backend Framework:** FastAPI (async Python web framework)
- **Database:** PostgreSQL with SQLAlchemy ORM
- **Authentication:** Custom JWT-based auth with invitation code system
- **Cloud Storage:** DigitalOcean Spaces for image/media management
- **Payments:** Stripe integration for subscription management
- **Testing:** Pytest with comprehensive integration and unit tests

---

## 🚀 Key Features

### Authentication & Authorization
- ✅ Super Admin system for platform management
- ✅ Institution and Scholarship admin accounts
- ✅ Invitation code-based registration
- ✅ JWT token authentication
- ✅ Role-based access control

### Institution Management
- ✅ Institution profiles with IPEDS integration
- ✅ Admissions data management and verification
- ✅ Tuition and financial information
- ✅ Gallery and media management
- ✅ Extended information (campus life, services, etc.)

### Scholarship Management
- ✅ Scholarship listings and search
- ✅ Eligibility criteria management
- ✅ Application deadline tracking
- ✅ Award amount ranges

### Media & Content
- ✅ Image upload to DigitalOcean Spaces
- ✅ Gallery management with featured images
- ✅ Video URL management (YouTube, Vimeo)
- ✅ Automatic image optimization

### Business Features
- ✅ Stripe subscription management
- ✅ Contact form and inquiry system
- ✅ Outreach campaign management
- ✅ Display settings customization

---

## 🧪 Testing Suite

Our comprehensive testing suite ensures reliability and maintainability:

### Test Structure
```
tests/
├── integration/           # API endpoint integration tests (75 tests)
│   ├── test_custom_auth_flow.py
│   ├── test_admissions_tuition.py
│   ├── test_contact.py
│   ├── test_gallery.py
│   ├── test_institutions.py
│   ├── test_scholarships.py
│   ├── test_subscriptions.py
│   ├── test_videos.py
│   ├── test_outreach.py
│   └── ...
├── unit/                  # Unit tests for core functionality (19 tests)
│   ├── test_auth_service.py
│   └── test_models.py
└── conftest.py           # Shared fixtures and configuration
```

### Running Tests

#### Run All Tests
```bash
# Activate virtual environment
source venv/bin/activate

# Run all tests with verbose output
pytest tests/ -v

# Run with coverage report
pytest tests/ --cov=app --cov-report=html
```

#### Run Specific Test Categories
```bash
# Run only integration tests
pytest tests/integration/ -v

# Run only unit tests
pytest tests/unit/ -v

# Run tests by marker
pytest tests/ -m auth -v          # Authentication tests
pytest tests/ -m gallery -v       # Gallery management tests
pytest tests/ -m integration -v   # All integration tests
```

#### Run Specific Test Files
```bash
# Test authentication flow
pytest tests/integration/test_custom_auth_flow.py -v

# Test gallery management
pytest tests/integration/test_gallery.py -v

# Test institutions endpoints
pytest tests/integration/test_institutions.py -v

# Test scholarships endpoints
pytest tests/integration/test_scholarships.py -v
```

#### Advanced Test Options
```bash
# Run last failed tests only
pytest tests/ --lf

# Stop on first failure
pytest tests/ -x

# Run tests in parallel (faster)
pytest tests/ -n auto

# Show test durations
pytest tests/ --durations=10

# Verbose output with traceback
pytest tests/ -vv --tb=short
```

### Test Coverage by Category

| Category | Tests | Status |
|----------|-------|--------|
| Authentication & Authorization | 13 | ✅ 100% |
| Institution Management | 19 | ✅ 100% |
| Scholarship Management | 3 | ✅ 100% |
| Gallery & Media | 16 | ✅ 100% |
| Data Management | 12 | ✅ 100% |
| Contact & Inquiries | 6 | ✅ 100% |
| Subscriptions | 5 | ✅ 100% |
| Videos | 5 | ✅ 100% |
| Outreach | 6 | ✅ 100% |
| Unit Tests | 9 | ✅ 100% |

---

## 🛠️ Setup & Installation

### Prerequisites
- Python 3.11+
- PostgreSQL 14+
- Virtual environment tool (venv, conda, etc.)

### Installation Steps

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/campusconnect-backend.git
cd campusconnect-backend
```

2. **Create and activate virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
```bash
# Copy example environment file
cp .env.example .env

# Edit .env with your configuration
nano .env
```

Required environment variables:
- `DATABASE_URL` - PostgreSQL connection string
- `SECRET_KEY` - JWT secret key
- `SPACES_KEY` - DigitalOcean Spaces access key
- `SPACES_SECRET` - DigitalOcean Spaces secret key
- `STRIPE_SECRET_KEY` - Stripe API secret key
- `SENDGRID_API_KEY` - SendGrid API key (for emails)

5. **Set up test database**
```bash
# Create test database
createdb campusconnect_test

# Copy test environment
cp .env.test.example .env.test

# Edit .env.test with test database configuration
nano .env.test
```

6. **Run database migrations**
```bash
alembic upgrade head
```

7. **Start the development server**
```bash
uvicorn app.main:app --reload
```

The API will be available at `http://localhost:8000`

8. **Verify installation**
```bash
# Check API health
curl http://localhost:8000/health

# Run tests
pytest tests/ -v
```

---

## 📚 API Documentation

### Interactive API Docs

Once the server is running, visit:
- **Swagger UI:** `http://localhost:8000/docs`
- **ReDoc:** `http://localhost:8000/redoc`
- **Simple Routes List:** `http://localhost:8000/routes-simple`

### Key Endpoints

#### Public Endpoints (No Auth Required)

**Health & System**
```
GET  /                    # Root endpoint
GET  /health              # Health check
GET  /routes-simple       # List all routes
```

**Institutions**
```
GET  /api/v1/institutions                    # List institutions
GET  /api/v1/institutions/{ipeds_id}         # Get institution details
GET  /api/v1/institutions/{ipeds_id}/admissions   # Get admissions data
GET  /api/v1/institutions/{ipeds_id}/tuition      # Get tuition data
GET  /api/v1/institutions/by-id/{id}         # Get by database ID
```

**Scholarships**
```
GET  /api/v1/scholarships                    # List scholarships
GET  /api/v1/scholarships/{id}               # Get scholarship details
```

**Public Gallery**
```
GET  /api/v1/public/gallery/institutions/{id}/gallery        # Institution gallery
GET  /api/v1/public/gallery/institutions/{id}/featured-image # Featured image
GET  /api/v1/public/gallery/scholarships/{id}/gallery        # Scholarship gallery
```

**Contact**
```
POST /api/v1/contact/submit                  # Submit contact form
```

#### Admin Endpoints (Authentication Required)

**Authentication**
```
POST /api/v1/admin/auth/register             # Register with invitation code
POST /api/v1/admin/auth/login                # Login (returns JWT)
GET  /api/v1/admin/auth/me                   # Get current user info
POST /api/v1/admin/auth/validate-invitation  # Validate invitation code
```

**Super Admin Only**
```
POST   /api/v1/admin/auth/invitations        # Create invitation code
GET    /api/v1/admin/auth/invitations        # List invitation codes
DELETE /api/v1/admin/auth/invitations/{id}   # Delete invitation code
GET    /api/v1/contact/inquiries             # List all inquiries
```

**Profile & Settings**
```
GET /api/v1/admin/profile/entity             # Get admin's institution/scholarship
GET /api/v1/admin/profile/display-settings   # Get display settings
PUT /api/v1/admin/profile/display-settings   # Update display settings
```

**Data Management**
```
GET /api/v1/admin/data/admissions            # Get admissions data
PUT /api/v1/admin/data/admissions/{id}       # Update admissions data
POST /api/v1/admin/data/admissions/{id}/verify  # Verify admissions data

GET /api/v1/admin/data/tuition               # Get tuition data
PUT /api/v1/admin/data/tuition/{id}          # Update tuition data
POST /api/v1/admin/data/tuition/{id}/verify  # Verify tuition data
```

**Gallery Management**
```
GET    /api/v1/admin/gallery                 # List gallery images
POST   /api/v1/admin/gallery                 # Add image to gallery
PUT    /api/v1/admin/gallery/{id}            # Update gallery image
DELETE /api/v1/admin/gallery/{id}            # Delete gallery image
PUT    /api/v1/admin/gallery/reorder         # Reorder gallery images
POST   /api/v1/admin/gallery/set-featured    # Set featured image
GET    /api/v1/admin/gallery/featured        # Get featured image
```

**Image Upload**
```
POST   /api/v1/admin/images/upload           # Upload image to Spaces
GET    /api/v1/admin/images/list             # List uploaded images
DELETE /api/v1/admin/images/{filename}       # Delete uploaded image
```

**Extended Info**
```
GET    /api/v1/admin/extended-info           # Get extended information
PUT    /api/v1/admin/extended-info           # Update extended information
DELETE /api/v1/admin/extended-info           # Delete extended information
```

**Videos**
```
GET    /api/v1/admin/videos                  # List videos
POST   /api/v1/admin/videos                  # Add video
PUT    /api/v1/admin/videos/{id}             # Update video
DELETE /api/v1/admin/videos/{id}             # Delete video
PUT    /api/v1/admin/videos/reorder          # Reorder videos
```

**Subscriptions**
```
GET  /api/v1/admin/subscriptions/pricing     # Get pricing information
GET  /api/v1/admin/subscriptions/current     # Get current subscription
POST /api/v1/admin/subscriptions/create-checkout  # Create Stripe checkout
POST /api/v1/admin/subscriptions/cancel      # Cancel subscription
GET  /api/v1/admin/subscriptions/portal      # Get customer portal link
```

**Outreach**
```
GET  /api/v1/admin/outreach/stats            # Get outreach statistics
GET  /api/v1/admin/outreach                  # List outreach campaigns
POST /api/v1/admin/outreach                  # Create outreach campaign
PUT  /api/v1/admin/outreach/{id}             # Update campaign
GET  /api/v1/admin/outreach/templates        # List email templates
POST /api/v1/admin/outreach/templates        # Create email template
```

### Authentication Flow

1. **Super Admin creates invitation code**
   ```bash
   POST /api/v1/admin/auth/invitations
   Authorization: Bearer {super_admin_token}
   {
     "entity_type": "institution",
     "entity_id": 123,
     "assigned_email": "admin@university.edu",
     "expires_in_days": 30
   }
   ```

2. **New admin validates invitation code**
   ```bash
   POST /api/v1/admin/auth/validate-invitation
   {
     "code": "INVITATION-CODE-HERE"
   }
   ```

3. **New admin registers**
   ```bash
   POST /api/v1/admin/auth/register
   {
     "email": "admin@university.edu",
     "password": "SecurePassword123!",
     "invitation_code": "INVITATION-CODE-HERE"
   }
   ```

4. **Admin logs in**
   ```bash
   POST /api/v1/admin/auth/login
   {
     "username": "admin@university.edu",
     "password": "SecurePassword123!"
   }
   ```

5. **Use JWT token for authenticated requests**
   ```bash
   GET /api/v1/admin/profile/entity
   Authorization: Bearer {jwt_token}
   ```

---

## 🗄️ Database Schema

### Core Models

**AdminUser**
- Custom authentication system
- Roles: `super_admin`, `admin`
- Entity linking (institution or scholarship)

**Institution**
- IPEDS ID integration
- Geographic information
- Control type classification
- Student/faculty metrics

**Scholarship**
- Award amount ranges
- Eligibility criteria
- Deadline tracking
- Difficulty levels

**InvitationCode**
- Secure invitation system
- Entity-specific codes
- Expiration handling
- Status tracking

**GalleryImage**
- Multi-entity support
- Display ordering
- Featured image designation
- Image type categorization

**AdmissionsData & TuitionData**
- Institution-specific data
- Verification system
- Year tracking
- Comprehensive financial metrics

---

## 🔐 Security Features

- **Password Hashing:** PBKDF2 with secure salts
- **JWT Tokens:** Industry-standard authentication
- **Role-Based Access:** Granular permission system
- **Invitation System:** Secure account creation
- **CORS Protection:** Configurable cross-origin policies
- **SQL Injection Protection:** SQLAlchemy ORM
- **Environment Variables:** Sensitive data protection

---

## 🧩 Testing Guide

### Test Configuration

The test suite uses a separate test database and environment configuration:

**Test Database:** `campusconnect_test`
**Test Config:** `.env.test`

### Test Isolation

Each test runs in its own transaction that is rolled back after completion:
- ✅ Clean database state per test
- ✅ No test pollution
- ✅ Parallel execution safe
- ✅ Fast test runs

### Writing New Tests

#### Integration Test Example
```python
import pytest
from httpx import AsyncClient

@pytest.mark.integration
class TestMyFeature:
    
    @pytest.mark.asyncio
    async def test_my_endpoint(
        self,
        client: AsyncClient,
        admin_headers: dict
    ):
        """Test my new endpoint"""
        response = await client.get(
            "/api/v1/my-endpoint",
            headers=admin_headers
        )
        
        assert response.status_code == 200
        data = response.json()
        assert "expected_field" in data
```

#### Unit Test Example
```python
import pytest
from app.core.security import get_password_hash, verify_password

@pytest.mark.unit
class TestPasswordSecurity:
    
    def test_password_hashing(self):
        """Test password hashing works correctly"""
        password = "TestPassword123!"
        hashed = get_password_hash(password)
        
        assert verify_password(password, hashed)
        assert not verify_password("WrongPassword", hashed)
```

### Available Fixtures

The test suite provides comprehensive fixtures in `conftest.py`:

- `client` - Async HTTP client
- `db_session` - Database session with rollback
- `super_admin_user` - Super admin user instance
- `super_admin_token` - Super admin JWT token
- `super_admin_headers` - Auth headers for super admin
- `test_institution` - Test institution instance
- `test_scholarship` - Test scholarship instance
- `invitation_code_institution` - Institution invitation code
- `registered_admin_user` - Registered admin account
- `admin_token` - Regular admin JWT token
- `admin_headers` - Auth headers for regular admin
- `sample_image_bytes` - Test image data

### Test Markers

Use markers to organize and run specific test categories:

```python
@pytest.mark.unit           # Unit tests
@pytest.mark.integration    # Integration tests
@pytest.mark.auth           # Authentication tests
@pytest.mark.gallery        # Gallery management tests
@pytest.mark.slow           # Slow-running tests
@pytest.mark.invitation     # Invitation code tests
```

---

## 📈 Performance & Optimization

- **Async/Await:** Non-blocking I/O operations
- **Connection Pooling:** Efficient database connections
- **Lazy Loading:** Optimized SQLAlchemy queries
- **CDN Integration:** DigitalOcean Spaces for static assets
- **Caching Strategy:** Prepared for Redis integration
- **Database Indexing:** Optimized query performance

---

## 🚀 Deployment

### Production Checklist

- [ ] Set `TESTING=false` in production environment
- [ ] Use strong `SECRET_KEY` (32+ characters)
- [ ] Configure production database URL
- [ ] Set up DigitalOcean Spaces
- [ ] Configure Stripe production keys
- [ ] Set up SendGrid for emails
- [ ] Configure CORS for frontend domain
- [ ] Enable HTTPS
- [ ] Set up monitoring and logging
- [ ] Configure backup strategy

### Environment Variables

**Required:**
```env
# Database
DATABASE_URL=postgresql+asyncpg://user:pass@host:5432/campusconnect_db

# Security
SECRET_KEY=your-secret-key-here-32-chars-minimum
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# DigitalOcean Spaces
SPACES_KEY=your-spaces-key
SPACES_SECRET=your-spaces-secret
SPACES_BUCKET=campusconnect
SPACES_REGION=nyc3

# Stripe
STRIPE_SECRET_KEY=sk_live_...
STRIPE_PUBLISHABLE_KEY=pk_live_...
STRIPE_WEBHOOK_SECRET=whsec_...

# SendGrid
SENDGRID_API_KEY=SG...
FROM_EMAIL=noreply@campusconnect.com

# Frontend URL
FRONTEND_URL=https://campusconnect.com
```

**Optional:**
```env
# Testing
TESTING=false
TEST_DATABASE_URL=postgresql+asyncpg://user:pass@host:5432/campusconnect_test

# Logging
LOG_LEVEL=INFO
```

---

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Write tests** for your changes
4. **Ensure all tests pass** (`pytest tests/ -v`)
5. **Commit your changes** (`git commit -m 'Add amazing feature'`)
6. **Push to the branch** (`git push origin feature/amazing-feature`)
7. **Open a Pull Request**

### Code Style

- Follow PEP 8 style guidelines
- Use type hints
- Write docstrings for public functions
- Keep functions focused and small
- Add tests for new features

---

## 📝 Project Structure

```
campusconnect-backend/
├── app/
│   ├── api/
│   │   └── v1/              # API endpoints
│   │       ├── admin_auth.py
│   │       ├── admin_gallery.py
│   │       ├── admin_images.py
│   │       ├── institutions.py
│   │       ├── scholarships.py
│   │       └── ...
│   ├── core/                # Core functionality
│   │   ├── config.py
│   │   ├── database.py
│   │   ├── security.py
│   │   └── ...
│   ├── models/              # SQLAlchemy models
│   │   ├── admin_user.py
│   │   ├── institution.py
│   │   ├── scholarship.py
│   │   └── ...
│   ├── schemas/             # Pydantic schemas
│   ├── services/            # Business logic
│   │   ├── auth_service.py
│   │   ├── image_service.py
│   │   └── ...
│   ├── middleware/          # Custom middleware
│   └── main.py             # FastAPI application
├── tests/
│   ├── integration/         # Integration tests
│   ├── unit/               # Unit tests
│   ├── conftest.py         # Test fixtures
│   └── docs/               # Test documentation
├── alembic/                # Database migrations
├── .env                    # Environment variables
├── .env.test              # Test environment
├── requirements.txt       # Python dependencies
├── pytest.ini            # Pytest configuration
└── README.md            # This file
```

---

## 🐛 Known Issues & Limitations

- Outreach features return 403 for regular admins (Super Admin only)
- Some display settings endpoints return 404 when no settings exist
- Image upload requires DigitalOcean Spaces configuration
- Contact form submissions may fail if SendGrid is not configured

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Authors

- **Your Name** - *Initial work* - [YourGitHub](https://github.com/yourusername)

---

## 🙏 Acknowledgments

- FastAPI for the excellent web framework
- SQLAlchemy for powerful ORM capabilities
- Pytest for comprehensive testing tools
- The Python async community

---

## 📞 Support & Contact

- **Email:** support@campusconnect.com
- **Issues:** [GitHub Issues](https://github.com/yourusername/campusconnect-backend/issues)
- **Documentation:** [API Docs](http://localhost:8000/docs)

---

## 🗺️ Roadmap

### Current Status ✅
- [x] Complete authentication system
- [x] Institution management
- [x] Scholarship management
- [x] Gallery & media management
- [x] Subscription system
- [x] Comprehensive test suite (94 tests passing)

### In Progress 🚧
- [ ] Frontend development
- [ ] Advanced search & filtering
- [ ] Email notification system
- [ ] Analytics dashboard

### Planned Features 📋
- [ ] Student application tracking
- [ ] Advanced matching algorithm
- [ ] Mobile app support
- [ ] Multi-language support
- [ ] AI-powered recommendations
- [ ] Integration with common app

---

**Built with ❤️ using FastAPI and Python**