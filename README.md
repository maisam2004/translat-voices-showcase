# 🎙️ VoiceAir - Universal Voice Translator

> A comprehensive FastAPI-based real-time voice translation platform with advanced speech-to-text, text translation, text-to-speech capabilities, PDF tools, and e-commerce marketplace integration.

[![Python Version](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.119.0-009688.svg?logo=fastapi)](https://fastapi.tiangolo.com)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Live Demo](https://img.shields.io/badge/live-voisair.com-blue.svg)](https://voisair.com)

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Quick Start](#-quick-start-local-development)
- [API Documentation](#-api-documentation)
- [Deployment](#-deployment-to-heroku)
- [Environment Variables](#-environment-variables-reference)
- [Contributing](#-contributing)

---

## ✨ Features

### 🎤 Core Translation Features
- **Real-time Voice Translation**: Duplex mode with simultaneous mic & speaker translation
- **Audio File Transcription**: Upload audio/video files (supports 50+ formats)
- **Text Translation**: 50+ languages with auto-detection and regional accents
- **Text-to-Speech (TTS)**: Azure Neural Voices with accent-aware synthesis
- **SRT Subtitle Translation**: Batch translate video subtitle files
- **Translation History**: Save and manage up to 50 translation sessions with audio playback

### 📄 PDF Tools Suite
- **PDF Merge**: Combine multiple PDFs into one
- **PDF Compress**: Reduce file size while maintaining quality
- **PDF to Images**: Export pages as high-resolution images (72-250 DPI)
- **Images to PDF**: Convert multiple images to a single PDF
- **PDF Split**: Extract specific pages or ranges
- **Trip Pack**: Organize travel documents into a single PDF
- **Visa Fix**: Optimize photos for visa applications (size & format requirements)
- **PDF to Word**: Extract text to editable DOCX format
- **Word to PDF**: Convert DOCX files to PDF

### 💳 Subscription & Monetization
- **Stripe Integration**: Free, Creator ($9.99/mo), Business ($29.99/mo) plans
- **Credit System**: Usage-based limits for text, audio, and API calls
- **API Access**: RESTful API with key-based authentication (Business plan)
- **Webhooks**: Event-driven integrations for automation
- **Payment Receipts**: Automatic email receipts with detailed breakdowns

### 🛒 E-Commerce Marketplace
- **18 Categories**: Travel (8) + E-commerce (10) including electronics, fashion, beauty
- **Deal Management**: Featured deals, discount codes, multi-image carousels
- **Click Tracking**: Analytics for affiliate conversions
- **Copy-to-Clipboard**: Quick discount code copying with visual feedback
- **Responsive Design**: Tailwind CSS with Material Icons

### 🔐 Authentication & Security
- **Google OAuth 2.0**: One-click login with profile sync
- **JWT Authentication**: Secure session management with token refresh
- **API Key Management**: Generate, list, and revoke API keys
- **Role-Based Access**: Admin, user, and API-level permissions
- **Rate Limiting**: SlowAPI-based protection (10-20 req/min per endpoint)

### 📊 Admin Features
- **SQLAdmin Dashboard**: Manage users, subscriptions, payments, offers, and support tickets
- **AI Content Agent**: Automated blog post and travel offer creation
- **Email Notifications**: Support request alerts and payment confirmations
- **Usage Analytics**: Track user activity, credits, and API consumption
- **Database Migrations**: Alembic-powered schema versioning

---

## 🛠️ Tech Stack

### Backend
| Technology | Version | Purpose |
|------------|---------|---------|
| **FastAPI** | 0.119.0 | Modern async web framework |
| **SQLAlchemy** | 2.0.44 | ORM for database interactions |
| **PostgreSQL** | 16+ | Production database (Heroku) |
| **SQLite** | 3+ | Local development database |
| **Alembic** | 1.18.1 | Database migration management |
| **Pydantic** | 2.12.0 | Data validation and serialization |
| **Uvicorn** | 0.37.0 | ASGI server |
| **Gunicorn** | 21.2.0 | Production process manager |

### Authentication & Security
| Technology | Version | Purpose |
|------------|---------|---------|
| **python-jose** | 3.5.0 | JWT token handling |
| **PyJWT** | 2.10.1 | JSON Web Tokens |
| **passlib** | 1.7.4 | Password hashing (bcrypt) |
| **cryptography** | 46.0.2 | Encryption utilities |
| **SlowAPI** | 0.1.9 | Rate limiting middleware |

### Payment & Subscriptions
| Technology | Version | Purpose |
|------------|---------|---------|
| **Stripe** | 13.0.1 | Payment processing & webhooks |

### AI & Translation Services
| Technology | Version | Purpose |
|------------|---------|---------|
| **AssemblyAI** | Latest | Speech-to-text transcription |
| **Google Cloud Translate** | 3.15.3 | Text translation (50+ languages) |
| **Azure Speech Services** | - | Neural text-to-speech (TTS) |
| **gTTS** | 2.5.4 | Fallback TTS engine |

### PDF Processing
| Technology | Version | Purpose |
|------------|---------|---------|
| **PyMuPDF (fitz)** | 1.24.0+ | PDF parsing, rendering, manipulation |
| **img2pdf** | 0.5.0+ | Image-to-PDF conversion |
| **Pillow** | 10.0.0+ | Image processing |
| **python-docx** | 1.1.2 | DOCX creation |
| **mammoth** | 1.4.19 | DOCX to HTML conversion |
| **playwright** | 1.44.0 | HTML to PDF (headless browser) |

### Storage & Media
| Technology | Version | Purpose |
|------------|---------|---------|
| **boto3** | 1.35.71 | AWS S3 integration for file storage |
| **aiohttp** | 3.13.0 | Async HTTP client |

### Frontend
| Technology | Version | Purpose |
|------------|---------|---------|
| **Jinja2** | 3.1.6 | Server-side templating |
| **Bootstrap** | 5.3.8 | Responsive UI framework |
| **Tailwind CSS** | 3.4+ | Utility-first CSS (deals page) |
| **Font Awesome** | 6.5+ | Icon library |
| **Material Icons** | - | Google Material Design icons |
| **Vanilla JavaScript** | ES6+ | Client-side interactivity |

### Admin & Monitoring
| Technology | Version | Purpose |
|------------|---------|---------|
| **SQLAdmin** | 0.16.1 | Database admin interface |
| **WTForms** | 3.1.2 | Form validation in admin |

---

## 🏗️ Project Architecture

### Directory Structure

```
translat-voices/
│
├── 📁 auth/                      # Authentication & authorization
│   ├── __init__.py               # Package initialization
│   ├── api_keys.py               # API key generation & validation
│   ├── credit_manager.py         # Usage credits & plan limits
│   ├── jwt_auth.py               # JWT token handling
│   ├── models.py                 # Auth-related SQLAlchemy models
│   ├── oauth.py                  # Google OAuth 2.0 flow
│   ├── pdf_processor.py          # PDF manipulation logic
│   ├── pdf_routes.py             # PDF API endpoints
│   ├── transcription_manager.py  # Background transcription jobs
│   ├── usage_tracker.py          # PDF usage quota tracking
│   └── webhooks.py               # Webhook delivery system
│
├── 📁 static/                    # Frontend assets
│   ├── css/                      # Custom stylesheets
│   ├── js/                       # JavaScript modules
│   │   └── realtime-whole.js     # Real-time translation UI
│   ├── images/                   # Logos, icons, placeholders
│   └── google-login-logo.png     # OAuth button asset
│
├── 📁 templates/                 # Jinja2 HTML templates
│   ├── base.html                 # Master layout (navbar, footer)
│   ├── realtime.html             # Main translation interface
│   ├── travel_deals_v2.html      # E-commerce marketplace
│   ├── pdf_tools.html            # PDF tools landing page
│   ├── profile.html              # User dashboard & API keys
│   ├── pricing.html              # Subscription plans
│   ├── transcriptions.html       # Audio file transcription page
│   ├── login.html                # Email/password login form
│   ├── register.html             # User registration
│   ├── about.html                # About page
│   └── contact.html              # Support contact form
│
├── 📁 alembic/                   # Database migrations
│   ├── versions/                 # Migration scripts
│   └── env.py                    # Alembic configuration
│
├── 📁 content_agent/             # AI content generation system
│   ├── config.json               # Agent configuration
│   ├── agent.py                  # Blog & deal creation logic
│   └── README.md                 # Agent setup guide
│
├── 📁 tools/                     # Utility scripts
│
├── 📁 temp_audio/                # Temporary audio processing
├── 📁 permanent_audio/           # Persistent audio storage
├── 📁 storage/                   # Local file storage
│
├── 📄 main.py                    # FastAPI application (2,933 lines)
├── 📄 models.py                  # SQLAlchemy database models
├── 📄 database.py                # Database engine & session
├── 📄 admin.py                   # SQLAdmin configuration
├── 📄 payments.py                # Stripe webhook handlers
├── 📄 agent_api_endpoints.py    # Admin API for AI agents
├── 📄 admin_upload_routes.py    # S3 file upload endpoints
├── 📄 support_notifications.py  # Email alert system
├── 📄 storage.py                 # S3 upload utilities
├── 📄 media_optimizer.py         # Audio/video optimization
│
├── 📄 requirements.txt           # Python dependencies (112 packages)
├── 📄 Procfile                   # Heroku process definition
├── 📄 runtime.txt                # Python 3.11 specification
├── 📄 app.json                   # Heroku app manifest
│
├── 📄 .env.template              # Environment variables template
├── 📄 .gitignore                 # Git exclusions
└── 📄 README.md                  # This file
```

### Database Models

```python
# Core Models (models.py)
- User                      # User accounts & profiles
- Subscription              # Stripe subscription data
- Payment                   # Payment transaction history
- TranslationHistory        # Saved translations
- TranscriptionJob          # Background transcription tasks
- SupportRequest            # Customer support tickets

# Content Models
- BlogPost                  # Blog articles
- TravelOffer               # Marketplace deals
- TravelOfferImage          # Deal image gallery
- TravelOfferClick          # Click tracking analytics
- Partner                   # Affiliate partners
- NewsletterSubscriber      # Email list
- NewsletterCampaign        # Email campaigns
```

### Key API Endpoints

#### Translation Services
```
POST   /transcribe            # Upload audio file for transcription
POST   /translate             # Translate text between languages
POST   /tts                   # Convert text to speech audio
POST   /translate-srt         # Translate SRT subtitle file
GET    /get-realtime-token    # Get AssemblyAI token for live transcription
```

#### PDF Tools
```
GET    /api/pdf/usage-stats   # Get user's PDF quota
POST   /api/pdf/merge         # Merge multiple PDFs
POST   /api/pdf/compress      # Reduce PDF file size
POST   /api/pdf/to-images     # Export PDF pages as images
POST   /api/pdf/to-pdf        # Convert images to PDF
POST   /api/pdf/split         # Split PDF by page ranges
POST   /api/pdf/to-word       # Convert PDF to DOCX
POST   /api/pdf/from-word     # Convert DOCX to PDF
POST   /api/pdf/trip-pack     # Create travel document pack
POST   /api/pdf/visa-fix      # Optimize photo for visa requirements
```

#### User & Subscription
```
GET    /profile               # User dashboard
POST   /profile/cancel-subscription  # Cancel Stripe subscription
GET    /profile/portal        # Stripe billing portal
POST   /api/keys              # Create API key
GET    /api/keys              # List user's API keys
POST   /api/webhooks          # Create webhook endpoint
GET    /api/webhooks          # List webhooks
```

#### Transcription Jobs (Async)
```
POST   /api/transcribe/start  # Start background transcription job
GET    /api/transcribe/jobs   # List user's transcription jobs
GET    /api/transcribe/jobs/{id}  # Get job status & result
```

#### Admin API (Requires Admin JWT)
```
POST   /api/admin/blog-posts  # Create blog post via AI agent
GET    /api/admin/blog-posts  # List blog posts
POST   /api/admin/travel-offers  # Create travel offer
GET    /api/admin/travel-offers  # List travel offers
```

#### Public Pages
```
GET    /                      # Redirect to /realtime
GET    /realtime              # Main translation interface
GET    /pdf-tools             # PDF tools landing page
GET    /transcriptions        # Audio transcription page
GET    /travel-deals          # E-commerce marketplace
GET    /pricing               # Subscription plans
GET    /profile               # User dashboard
GET    /blog                  # Blog listing
GET    /blog/{slug}           # Individual blog post
GET    /contact               # Support contact form
GET    /about                 # About page
```

---

---

## 🚀 Quick Start (Local Development)

### Prerequisites

- **Python 3.11+** (specified in `runtime.txt`)
- **pip** (latest version recommended)
- **Git** for version control
- **PostgreSQL** (optional, uses SQLite by default locally)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/maisam2004/translat-voices.git
   cd translat-voices
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv_new
   
   # Windows
   venv_new\Scripts\activate
   
   # macOS/Linux
   source venv_new/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   
   # Install Playwright browsers for PDF conversion
   playwright install chromium
   ```

4. **Set up environment variables**
   
   Create a `.env` file in the project root:
   ```bash
   # Copy template
   cp .env.template .env
   ```
   
   **Edit `.env` and configure:**
   
   ```ini
   # Environment
   ENVIRONMENT=development
   PRODUCTION_DOMAIN=http://localhost:8000
   
   # Security
   JWT_SECRET_KEY=your_generated_secret_key_here  # Generate: python -c "import secrets; print(secrets.token_urlsafe(32))"
   
   # Database (auto-created SQLite locally)
   # DATABASE_URL is auto-set by Heroku in production
   
   # Stripe (get from https://dashboard.stripe.com/apikeys)
   STRIPE_SECRET_KEY=sk_test_your_test_key
   STRIPE_PUBLISHABLE_KEY=pk_test_your_test_key
   STRIPE_WEBHOOK_SECRET=whsec_your_webhook_secret
   
   # Google OAuth (https://console.cloud.google.com/)
   GOOGLE_CLIENT_ID=your_client_id.apps.googleusercontent.com
   GOOGLE_CLIENT_SECRET=GOCSPX-your_secret
   GOOGLE_REDIRECT_URI=http://localhost:8000/auth/callback
   
   # API Keys for Services
   ASSEMBLYAI_API_KEY=your_assemblyai_key          # https://app.assemblyai.com/
   GOOGLE_API_KEY=your_google_translate_key        # Google Cloud Translation API
   AZURE_API_KEY=your_azure_speech_key             # Azure Speech Services
   AZURE_REGION=eastus                             # Azure region
   
   # AWS S3 (optional, for file storage)
   AWS_ACCESS_KEY_ID=your_aws_key
   AWS_SECRET_ACCESS_KEY=your_aws_secret
   AWS_S3_BUCKET_NAME=your_bucket_name
   AWS_REGION=us-east-1
   ```

5. **Initialize database**
   ```bash
   # Create tables from models
   python -c "from database import engine; from models import Base; Base.metadata.create_all(bind=engine)"
   ```

6. **Run development server**
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```

7. **Access the application**
   - **Main App**: http://localhost:8000
   - **Translator**: http://localhost:8000/realtime
   - **PDF Tools**: http://localhost:8000/pdf-tools
   - **Admin Panel**: http://localhost:8000/admin
   - **API Docs (Swagger)**: http://localhost:8000/docs
   - **ReDoc**: http://localhost:8000/redoc

---

## 📚 API Documentation

### Authentication

All API endpoints require authentication via one of:

1. **Session Cookie** (browser-based, after Google OAuth login)
2. **JWT Token** (header: `Authorization: Bearer <token>`)
3. **API Key** (header: `X-API-Key: <key>`, Business plan only)

### Example: Translation API

**Request:**
```bash
curl -X POST http://localhost:8000/translate \
  -H "X-API-Key: your_api_key_here" \
  -F "text=Hello, world!" \
  -F "source_language=en" \
  -F "target_language=es"
```

**Response:**
```json
{
  "translated_text": "¡Hola, mundo!",
  "source_language": "en",
  "target_language": "es",
  "credits_used": 13
}
```

### Example: Text-to-Speech

**Request:**
```bash
curl -X POST http://localhost:8000/tts \
  -H "X-API-Key: your_api_key_here" \
  -F "text=¡Hola, mundo!" \
  -F "language=es" \
  --output audio.mp3
```

**Response:** Binary audio file (MP3, 24kHz, 96kbps)

### Example: Transcription Job (Async)

**Start Job:**
```bash
curl -X POST http://localhost:8000/api/transcribe/start \
  -H "X-API-Key: your_api_key_here" \
  -F "file=@meeting_recording.mp4"
```

**Response:**
```json
{
  "job_id": "uuid-here",
  "status": "processing",
  "message": "Transcription started"
}
```

**Check Status:**
```bash
curl -X GET "http://localhost:8000/api/transcribe/jobs/uuid-here" \
  -H "X-API-Key: your_api_key_here"
```

**Response:**
```json
{
  "id": "uuid-here",
  "status": "completed",
  "original_filename": "meeting_recording.mp4",
  "file_size": 52428800,
  "transcription_text": "Full transcription here...",
  "created_at": "2026-02-04T10:30:00Z",
  "updated_at": "2026-02-04T10:35:22Z"
}
```

### Rate Limits (per endpoint)

| Endpoint | Free Plan | Creator Plan | Business Plan |
|----------|-----------|--------------|---------------|
| `/translate` | 20/min | 20/min | 20/min |
| `/tts` | 15/min | 15/min | 15/min |
| `/transcribe` | 10/min | 10/min | 10/min |
| `/api/pdf/*` | 5/min | 10/min | 20/min |

### Monthly Quotas

| Resource | Free | Creator | Business |
|----------|------|---------|----------|
| Text translation | 10,000 chars | 2M chars | Unlimited |
| Audio transcription | 5 min | 30 min | 150 min |
| TTS generation | 1,000 chars | 100K chars | Unlimited |
| PDF processing | 10 MB/day | 100 MB/day | Unlimited |
| API requests | ❌ | ❌ | 10,000/mo |
| Translation history | 20 items | 50 items | 50 items |

---

---

## 🚢 Deployment to Heroku

### Prerequisites

- [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) installed
- Heroku account with billing enabled (for PostgreSQL addon)
- Git repository initialized in your project

### Deployment Steps

1. **Login to Heroku**
   ```bash
   heroku login
   ```

2. **Create a new Heroku app**
   ```bash
   heroku create your-app-name
   # Example: heroku create voiceair-translator
   ```

3. **Add PostgreSQL addon**
   ```bash
   # Essential plan (~$5/month, required for production)
   heroku addons:create heroku-postgresql:essential-0 -a your-app-name
   ```

4. **Set environment variables**
   ```bash
   # Generate and set JWT secret
   heroku config:set JWT_SECRET_KEY=$(python -c "import secrets; print(secrets.token_urlsafe(32))")
   
   # Set environment to production
   heroku config:set ENVIRONMENT=production
   
   # Set your production domain (example: voisair.com)
   heroku config:set PRODUCTION_DOMAIN=https://your-app-name.herokuapp.com
   
   # Stripe keys (use LIVE keys for production)
   heroku config:set STRIPE_SECRET_KEY=sk_live_your_key_here
   heroku config:set STRIPE_PUBLISHABLE_KEY=pk_live_your_key_here
   heroku config:set STRIPE_WEBHOOK_SECRET=whsec_your_secret_here
   
   # Google OAuth
   heroku config:set GOOGLE_CLIENT_ID=your_client_id.apps.googleusercontent.com
   heroku config:set GOOGLE_CLIENT_SECRET=your_client_secret
   heroku config:set GOOGLE_REDIRECT_URI=https://your-app-name.herokuapp.com/auth/callback
   
   # API Keys for Translation Services
   heroku config:set ASSEMBLYAI_API_KEY=your_key_here
   heroku config:set GOOGLE_API_KEY=your_key_here
   heroku config:set AZURE_API_KEY=your_key_here
   heroku config:set AZURE_REGION=eastus
   
   # AWS S3 (for file storage)
   heroku config:set AWS_ACCESS_KEY_ID=your_aws_key
   heroku config:set AWS_SECRET_ACCESS_KEY=your_aws_secret
   heroku config:set AWS_S3_BUCKET_NAME=your_bucket_name
   heroku config:set AWS_REGION=us-east-1
   ```

5. **Update Google OAuth redirect URI**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Navigate to **APIs & Services > Credentials**
   - Edit your OAuth 2.0 Client ID
   - Add to **Authorized redirect URIs**:
     ```
     https://your-app-name.herokuapp.com/auth/callback
     ```
   - Save changes

6. **Update Stripe webhook endpoint**
   - Go to [Stripe Dashboard Webhooks](https://dashboard.stripe.com/webhooks)
   - Click **Add endpoint**
   - URL: `https://your-app-name.herokuapp.com/stripe/webhook`
   - Select events:
     - `checkout.session.completed`
     - `customer.subscription.created`
     - `customer.subscription.updated`
     - `customer.subscription.deleted`
     - `invoice.payment_succeeded`
     - `invoice.payment_failed`
   - Copy the **Signing secret** and set it:
     ```bash
     heroku config:set STRIPE_WEBHOOK_SECRET=whsec_your_secret
     ```

7. **Deploy to Heroku**
   ```bash
   # Add Heroku remote (if not already added)
   git remote add heroku https://git.heroku.com/your-app-name.git
   
   # Commit any pending changes
   git add .
   git commit -m "Prepare for Heroku deployment"
   
   # Push to Heroku
   git push heroku main
   ```

8. **Initialize database tables**
   ```bash
   heroku run python -c "from database import engine; from models import Base; Base.metadata.create_all(bind=engine)"
   ```

9. **Install Playwright browsers (for PDF conversion)**
   ```bash
   heroku run playwright install chromium
   ```

10. **Set up an admin user (optional)**
    ```bash
    heroku run python set_admin.py your_email@example.com
    ```

11. **Open your app**
    ```bash
    heroku open
    ```

### Post-Deployment Checklist

- [ ] Test Google OAuth login flow
- [ ] Test Stripe payment integration (use test cards)
- [ ] Verify API endpoints work with API keys
- [ ] Check admin panel access at `/admin`
- [ ] Test file upload functionality (audio, PDF)
- [ ] Test PDF tools (merge, compress, etc.)
- [ ] Monitor logs: `heroku logs --tail`
- [ ] Set up uptime monitoring (e.g., UptimeRobot)
- [ ] Configure custom domain (optional): `heroku domains:add yourdomain.com`
- [ ] Set up SSL certificate: `heroku certs:auto:enable`

### Monitoring & Maintenance

**View logs:**
```bash
heroku logs --tail -a your-app-name
```

**Check database status:**
```bash
heroku pg:info
```

**Run database migrations:**
```bash
heroku run alembic upgrade head
```

**Restart dynos:**
```bash
heroku restart
```

**Scale dynos (if needed):**
```bash
# Upgrade to Standard dyno for better performance
heroku ps:scale web=1:standard-1x
```

---

---

## 🔧 Environment Variables Reference

| Variable | Required | Description | Example | Where to Get |
|----------|----------|-------------|---------|--------------|
| `DATABASE_URL` | Auto | PostgreSQL connection string | `postgresql://user:pass@host/db` | Auto-set by Heroku PostgreSQL addon |
| `JWT_SECRET_KEY` | ✅ | Secret for JWT token signing | `random_32_char_string` | Generate: `python -c "import secrets; print(secrets.token_urlsafe(32))"` |
| `ENVIRONMENT` | ✅ | Deployment environment | `development` or `production` | Set manually |
| `PRODUCTION_DOMAIN` | ✅ | Your app's public URL | `https://voisair.com` | Your production domain |
| **Stripe** |
| `STRIPE_SECRET_KEY` | ✅ | Stripe API secret key | `sk_live_...` or `sk_test_...` | [Stripe Dashboard > API Keys](https://dashboard.stripe.com/apikeys) |
| `STRIPE_PUBLISHABLE_KEY` | ✅ | Stripe public key | `pk_live_...` or `pk_test_...` | [Stripe Dashboard > API Keys](https://dashboard.stripe.com/apikeys) |
| `STRIPE_WEBHOOK_SECRET` | ✅ | Stripe webhook signing secret | `whsec_...` | [Stripe Dashboard > Webhooks](https://dashboard.stripe.com/webhooks) |
| **Google OAuth** |
| `GOOGLE_CLIENT_ID` | ✅ | OAuth 2.0 client ID | `123.apps.googleusercontent.com` | [Google Cloud Console > Credentials](https://console.cloud.google.com/apis/credentials) |
| `GOOGLE_CLIENT_SECRET` | ✅ | OAuth 2.0 client secret | `GOCSPX-...` | [Google Cloud Console > Credentials](https://console.cloud.google.com/apis/credentials) |
| `GOOGLE_REDIRECT_URI` | ✅ | OAuth callback URL | `https://app.com/auth/callback` | Your domain + `/auth/callback` |
| **Translation APIs** |
| `ASSEMBLYAI_API_KEY` | ✅ | Speech-to-text API key | `abc123...` | [AssemblyAI Dashboard](https://app.assemblyai.com/) |
| `GOOGLE_API_KEY` | ⚠️ | Google Translate API key | `AIza...` | [Google Cloud Console > APIs](https://console.cloud.google.com/) |
| `AZURE_API_KEY` | ⚠️ | Azure Speech Services key | `abc123...` | [Azure Portal > Speech Services](https://portal.azure.com/) |
| `AZURE_REGION` | ⚠️ | Azure service region | `eastus` or `westeurope` | Same as your Azure Speech resource |
| **AWS S3 (File Storage)** |
| `AWS_ACCESS_KEY_ID` | ⚠️ | AWS IAM access key | `AKIA...` | [AWS IAM Console](https://console.aws.amazon.com/iam/) |
| `AWS_SECRET_ACCESS_KEY` | ⚠️ | AWS IAM secret key | `abc123...` | [AWS IAM Console](https://console.aws.amazon.com/iam/) |
| `AWS_S3_BUCKET_NAME` | ⚠️ | S3 bucket name | `my-app-storage` | Your S3 bucket name |
| `AWS_REGION` | ⚠️ | AWS region | `us-east-1` | Your S3 bucket region |

**Legend:**
- ✅ = **Required** for basic functionality
- ⚠️ = **Optional** but highly recommended for full feature set

### API Service Setup Links

1. **AssemblyAI** (Speech-to-Text)
   - Sign up: https://www.assemblyai.com/
   - Get API key from dashboard
   - Free tier: 100 min/month

2. **Google Cloud Translation API**
   - Enable: https://console.cloud.google.com/apis/library/translate.googleapis.com
   - Create credentials: API Key
   - Pricing: $20 per 1M chars

3. **Azure Speech Services**
   - Create resource: https://portal.azure.com/#create/Microsoft.CognitiveServicesSpeechServices
   - Copy key and region from resource overview
   - Free tier: 5 audio hours/month

4. **AWS S3** (File Storage)
   - Create bucket: https://s3.console.aws.amazon.com/s3/
   - Create IAM user with `AmazonS3FullAccess` policy
   - Generate access keys

---

## 🔐 Security Best Practices

### Environment Security
- ✅ **NEVER** commit `.env` to Git (included in `.gitignore`)
- ✅ Use different API keys for development vs production
- ✅ Rotate secrets regularly (every 90 days)
- ✅ Use Stripe test keys (`sk_test_`) in development
- ✅ Enable 2FA on all service accounts (Stripe, Google, AWS)

### Application Security
- ✅ HTTPS enforced in production (`ENVIRONMENT=production`)
- ✅ Secure cookies: `HttpOnly`, `SameSite=Lax`
- ✅ Rate limiting on all endpoints (SlowAPI)
- ✅ JWT tokens with expiration (24h default)
- ✅ Stripe webhook signature verification
- ✅ SQL injection protection (SQLAlchemy ORM)
- ✅ XSS protection (Jinja2 auto-escaping)

### User Data
- ✅ Passwords hashed with bcrypt (if email/password auth used)
- ✅ API keys stored as hashed values in database
- ✅ User files stored on S3 with unique UUIDs
- ✅ Translation history limited to last 50 items
- ✅ Temporary audio files cleaned up after 1 hour

### Monitoring
```bash
# View security-related logs
heroku logs --tail | grep -i "error\|failed\|unauthorized"

# Check for failed login attempts
heroku logs --tail | grep "401\|403"
```

---

## 🐛 Troubleshooting

### Database Issues

**Error: `could not connect to server`**
```bash
# Check DATABASE_URL is set
heroku config:get DATABASE_URL

# Verify database is accessible
heroku pg:info

# Reset connection pool
heroku restart
```

**Error: `relation "users" does not exist`**
```bash
# Run migrations
heroku run alembic upgrade head

# Or recreate tables (⚠️ destroys data)
heroku run python -c "from database import engine; from models import Base; Base.metadata.create_all(bind=engine)"
```

### Application Crashes

**Error: `R10 - Boot timeout`**
- Check `Procfile` is correct: `web: gunicorn main:app -k uvicorn.workers.UvicornWorker`
- Increase timeout: `heroku config:set BOOT_TIMEOUT=120`
- Check logs: `heroku logs --tail`

**Error: `H12 - Request timeout`**
- Large file uploads: Increase Gunicorn timeout in `Procfile`
- Use async transcription endpoints (`/api/transcribe/start`) instead

### Static Files Not Loading

```bash
# Verify static directory exists
ls -la static/

# Check FastAPI static mount in main.py
grep "app.mount" main.py

# Ensure paths use /static/ prefix
# ✅ /static/css/style.css
# ❌ css/style.css
```

### OAuth Redirect Errors

**Error: `redirect_uri_mismatch`**
1. Check `GOOGLE_REDIRECT_URI` matches production domain:
   ```bash
   heroku config:get GOOGLE_REDIRECT_URI
   ```
2. Update Google Cloud Console:
   - Go to Credentials > Edit OAuth 2.0 Client
   - Add exact redirect URI (with https://)
   - Save and wait 5 minutes for propagation

### Stripe Webhook Failures

**Error: `No signatures found matching the expected signature`**
```bash
# Verify webhook secret
heroku config:get STRIPE_WEBHOOK_SECRET

# Test webhook locally with Stripe CLI
stripe listen --forward-to localhost:8000/stripe/webhook
```

### PDF Processing Errors

**Error: `Playwright not installed`**
```bash
heroku run playwright install chromium
```

**Error: `PDF file too large`**
- Check user quota: `/api/pdf/usage-stats`
- Increase limits in `auth/pdf_processor.py` (constants)

### API Rate Limit Exceeded

```json
{
  "error": "Rate limit exceeded",
  "retry_after": 60
}
```

**Solution:** Wait 60 seconds or upgrade to a higher plan with increased limits

---

## 🤝 Contributing

### Development Workflow

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**
4. **Test locally**
   ```bash
   uvicorn main:app --reload
   ```
5. **Commit with clear messages**
   ```bash
   git commit -m "Add: New translation language support for Arabic"
   ```
6. **Push to your fork**
   ```bash
   git push origin feature/amazing-feature
   ```
7. **Open a Pull Request**

### Code Style

- **Python**: Follow PEP 8, use `black` formatter
- **JavaScript**: ES6+, use `prettier` for formatting
- **HTML/CSS**: Semantic HTML5, Bootstrap conventions
- **Comments**: Clear docstrings for all functions

### Testing

```bash
# Run tests (if test suite exists)
pytest

# Check code formatting
black --check .

# Lint Python code
flake8 main.py auth/ --max-line-length=120
```

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 📧 Support & Contact

### Get Help

- 📖 **Documentation**: Check this README and inline code comments
- 🐛 **Bug Reports**: [Create an issue](https://github.com/maisam2004/translat-voices/issues)
- 💡 **Feature Requests**: [Open a discussion](https://github.com/maisam2004/translat-voices/discussions)
- 📧 **Email**: support@voisair.com (if configured)

### Useful Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Stripe API Reference](https://stripe.com/docs/api)
- [AssemblyAI Docs](https://www.assemblyai.com/docs)
- [Heroku Dev Center](https://devcenter.heroku.com/)
- [Bootstrap 5 Docs](https://getbootstrap.com/docs/5.3/)

---

## 🙏 Acknowledgments

- **FastAPI** - Modern Python web framework
- **AssemblyAI** - Accurate speech-to-text transcription
- **Azure Speech Services** - High-quality neural TTS
- **Stripe** - Seamless payment processing
- **Heroku** - Easy deployment and scaling
- **Bootstrap** - Responsive UI components

---

## 📊 Project Stats

- **Total Lines of Code**: ~8,500+ (Python, JavaScript, HTML)
- **Dependencies**: 112 Python packages
- **API Endpoints**: 50+
- **Supported Languages**: 50+
- **Live Demo**: [voisair.com](https://voisair.com)

---

**Built with ❤️ using FastAPI, Bootstrap, and modern web technologies**

*Last Updated: February 2026*
