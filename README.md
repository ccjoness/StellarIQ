# StellarIQ

A comprehensive financial analysis platform providing real-time market data, technical indicators, and intelligent trading signals for both cryptocurrency and equity markets. Built with FastAPI backend and React Native (Expo) mobile app.

## ✨ Features

### Core Functionality
- **🔍 Unified Search**: Search across crypto and equity markets with unified results
- **📊 Real-time Data**: Live price feeds and market data via Alpha Vantage API
- **📈 Technical Analysis**: Advanced indicators including RSI, Stochastic, Bollinger Bands, and MACD
- **🎯 Smart Signals**: Intelligent signal generation with confidence scoring and trend analysis
- **⭐ Favorites/Watchlist**: Personal watchlist with real-time price tracking
- **🔔 Push Notifications**: Firebase Cloud Messaging for price alerts and market updates
- **🔐 Authentication**: Secure user authentication with JWT tokens and Google Sign-In
- **📱 Cross-platform**: React Native mobile app with responsive design

### Advanced Features
- **📉 Candlestick Charts**: Interactive OHLCV charts with Victory Native
- **🔄 Background Updates**: Automated market data refresh with APScheduler
- **💾 Smart Caching**: Valkey (Redis) caching for optimal performance
- **🎨 Theme Support**: Light/Dark mode with system preference detection
- **📊 Portfolio Tracking**: Crypto portfolio management (in development)
- **🔔 Alert Management**: Customizable price alerts and notification preferences

## 🏗️ Architecture

### Backend (FastAPI)
- **Framework**: FastAPI with Python 3.12
- **Database**: PostgreSQL with SQLAlchemy 2.0 ORM
- **Cache**: Valkey (Redis-compatible) for performance optimization
- **Background Tasks**: APScheduler for scheduled market data updates
- **Authentication**: JWT tokens with bcrypt password hashing
- **API Documentation**: Auto-generated Swagger UI and ReDoc
- **Logging**: Structured logging with custom log configuration

### Mobile App (React Native/Expo)
- **Framework**: Expo SDK 54 with TypeScript
- **State Management**: TanStack Query (React Query) for server state
- **Local State**: Zustand for client-side state management
- **Charts**: Victory Native for technical analysis visualization
- **Navigation**: React Navigation v7 with bottom tabs and stack navigation
- **Notifications**: Expo Notifications + Firebase Cloud Messaging
- **Authentication**: Google Sign-In integration
- **Storage**: AsyncStorage for local data persistence

### Data Sources
- **Primary API**: Alpha Vantage API (stocks + crypto)
- **Stock Data**: Real-time quotes, company overviews, historical OHLCV data
- **Crypto Data**: Real-time exchange rates, historical OHLCV data
- **Coverage**: Intraday data, daily/weekly/monthly historical data, technical indicators

### Alpha Vantage API Tiers
- **Free Tier**: 5 API calls/minute, 500 calls/day, end-of-day data
- **Premium Tier**: 75 API calls/minute, 15-minute delayed intraday data
- **⚠️ Note**: All data is delayed by 15 minutes (not real-time)

## 🛠️ Tech Stack

| Component | Technology | Version |
|-----------|------------|---------|
| **Mobile App** | React Native (Expo) | 0.81.4 / SDK 54 |
| **Language** | TypeScript | 5.9.2 |
| **Backend API** | FastAPI | 0.116.2 |
| **Runtime** | Python | 3.12 |
| **Database** | PostgreSQL | Latest |
| **ORM** | SQLAlchemy | 2.0.43 |
| **Cache** | Valkey (Redis) | 6.1.1 |
| **State Management** | TanStack Query + Zustand | 5.8.4 + 4.4.7 |
| **Charts** | Victory Native | 36.6.12 |
| **Navigation** | React Navigation | 7.x |
| **Notifications** | Expo Notifications + Firebase | 0.32.11 |
| **Authentication** | JWT + Google Sign-In | - |
| **Background Tasks** | APScheduler | 3.11.0 |
| **Migrations** | Alembic | 1.16.5 |
| **HTTP Client** | httpx | 0.28.1 |
| **Testing** | pytest + Jest | Latest |
| **Linting** | ESLint + Prettier | Latest |

## 📁 Project Structure

```
StellarIQ_App/
├── StellarIQ_API/           # FastAPI backend
│   ├── app/
│   │   ├── core/            # Core configuration (database, auth, security, valkey)
│   │   ├── models/          # SQLAlchemy models (user, favorites, notifications, etc.)
│   │   ├── routers/         # API route handlers (auth, stocks, crypto, favorites, etc.)
│   │   ├── schemas/         # Pydantic schemas for request/response validation
│   │   ├── services/        # Business logic (market data, analysis, notifications)
│   │   ├── templates/       # HTML templates (account deletion, privacy policy)
│   │   └── utils/           # Utilities (technical analysis, chart formatting)
│   ├── alembic/             # Database migrations
│   ├── tests/               # Backend tests
│   ├── main.py              # Application entry point
│   ├── config.py            # Configuration settings
│   ├── requirements.txt     # Python dependencies
│   ├── docker-compose.yml   # Docker services (PostgreSQL, Valkey)
│   └── log_conf.yaml        # Logging configuration
│
├── StellarIQ_Mobile/        # React Native (Expo) app
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   │   ├── AlertButton.tsx
│   │   │   ├── CandlestickChart.tsx
│   │   │   ├── FavoriteButton.tsx
│   │   │   ├── TechnicalIndicatorCharts.tsx
│   │   │   └── NotificationSettings.tsx
│   │   ├── screens/         # App screens
│   │   │   ├── HomeScreen.tsx
│   │   │   ├── SearchScreen.tsx
│   │   │   ├── WatchlistScreen.tsx
│   │   │   ├── TickerDetailScreen.tsx
│   │   │   ├── auth/        # Authentication screens
│   │   │   └── ...
│   │   ├── navigation/      # Navigation configuration
│   │   ├── services/        # API client and services
│   │   ├── contexts/        # React contexts (Auth, Watchlist)
│   │   ├── providers/       # React providers (Theme, Notifications)
│   │   ├── hooks/           # Custom React hooks
│   │   ├── types/           # TypeScript type definitions
│   │   └── constants/       # App constants and configuration
│   ├── assets/              # Images, icons, fonts
│   ├── App.tsx              # Root component
│   ├── app.config.js        # Expo configuration
│   ├── package.json         # Node dependencies
│   └── tsconfig.json        # TypeScript configuration
│
├── logo/                    # App logos (Android/iOS)
└── README.md                # This file
```

## 🚀 Quick Start

### Prerequisites
- **Node.js** 18+ and **Yarn** (for mobile app)
- **Python** 3.12+ (for backend)
- **Docker** and **Docker Compose** (for PostgreSQL and Valkey)
- **Expo CLI** (install with `npm install -g expo-cli`)
- **Alpha Vantage API Key** (get free key at [alphavantage.co](https://www.alphavantage.co/support/#api-key))

### Backend Setup

1. **Navigate to API directory**:
```bash
cd StellarIQ_API
```

2. **Install Python dependencies**:
```bash
pip install -r requirements.txt
```

3. **Create environment file**:
```bash
# Create .env file with the following content:
DATABASE_URL=postgresql://stellariq:password@localhost:5432/stellariq_db
VALKEY_URL=redis://localhost:6379/0
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_api_key_here
ALPHA_VANTAGE_RATE_LIMIT_PER_MINUTE=5
SECRET_KEY=your-super-secret-jwt-key-change-this-in-production
ACCESS_TOKEN_EXPIRE_MINUTES=30
CACHE_TTL_SECONDS=900
```

4. **Start database and cache services**:
```bash
docker-compose up -d
```

5. **Run database migrations**:
```bash
alembic upgrade head
```

6. **Start the API server**:
```bash
python -m uvicorn main:app --host 0.0.0.0 --port 8000 --reload --log-config=log_conf.yaml
```

The API will be available at `http://localhost:8000`

### Mobile App Setup

1. **Navigate to mobile directory**:
```bash
cd StellarIQ_Mobile
```

2. **Install dependencies**:
```bash
yarn install
```

3. **Configure API URL**:
Edit `app.config.js` and update the `apiUrl`:
```javascript
extra: {
  apiUrl: "http://192.168.1.100:8000",  // Replace with your computer's IP
  // ...
}
```

**Note**: For Android devices/emulators, use your computer's local IP address instead of `localhost`.

4. **Start Expo development server**:
```bash
yarn start
# or
expo start
```

5. **Run on device**:
- Scan the QR code with **Expo Go** app (iOS/Android)
- Or press `a` for Android emulator
- Or press `i` for iOS simulator (macOS only)

## ⚙️ Configuration

### Backend Environment Variables

Create a `.env` file in the `StellarIQ_API` directory:

```env
# Database Configuration
DATABASE_URL=postgresql://stellariq:password@localhost:5432/stellariq_db

# Valkey (Redis-compatible) Cache
VALKEY_URL=redis://localhost:6379/0

# Alpha Vantage API Configuration
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_api_key_here
ALPHA_VANTAGE_RATE_LIMIT_PER_MINUTE=5  # 5 for free tier, 75 for premium

# JWT Authentication
SECRET_KEY=your-super-secret-jwt-key-change-this-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Application Settings
APP_NAME=StellarIQ Backend
APP_VERSION=1.0.0
DEBUG=True

# Cache Settings
CACHE_TTL_SECONDS=900  # 15 minutes

# Email/SMTP Configuration (optional, for account deletion emails)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASSWORD=your-app-password
SMTP_FROM_EMAIL=noreply@stellariq.com
SMTP_FROM_NAME=StellarIQ
```

### Mobile App Configuration

The mobile app uses `app.config.js` for configuration. Key settings:

```javascript
export default {
  expo: {
    extra: {
      apiUrl: process.env.EXPO_PUBLIC_API_URL || "http://192.168.1.100:8000",
      eas: {
        projectId: "2f38aa9b-5f7a-497e-bfad-3bd8e3ecdaaa"
      }
    }
  }
}
```

**Finding your local IP address**:
- **Windows**: Run `ipconfig` and look for IPv4 Address
- **macOS/Linux**: Run `ifconfig` or `ip addr` and look for inet address
- **Example**: `192.168.1.100`

### Firebase Configuration (for Push Notifications)

1. Place `google-services.json` in `StellarIQ_Mobile/` directory
2. Place Firebase admin SDK JSON in `StellarIQ_Mobile/` directory
3. Configure in `app.config.js`:
```javascript
android: {
  googleServicesFile: "./google-services.json",
  // ...
}
```

## 📊 Technical Indicators & Signals

### Implemented Indicators

| Indicator | Parameters | Buy Signal | Sell Signal |
|-----------|------------|------------|-------------|
| **RSI** | Period: 14 | < 30 (Oversold) | > 70 (Overbought) |
| **Stochastic** | %K: 14, %D: 3 | < 20 (Oversold) | > 80 (Overbought) |
| **Bollinger Bands** | Period: 20, StdDev: 2 | Price < Lower Band | Price > Upper Band |
| **MACD** | Fast: 12, Slow: 26, Signal: 9 | MACD crosses above Signal | MACD crosses below Signal |

### Signal Generation Logic

The platform uses a **consensus-based approach** for generating trading signals:

1. **Individual Indicator Analysis**: Each indicator is evaluated independently
2. **Consensus Requirement**: At least 2 indicators must agree for a signal
3. **Confidence Scoring**: Calculated as the fraction of agreeing indicators (0.0 to 1.0)
4. **Trend Consistency**: Analyzes the last 3 bars to confirm trend direction
5. **Signal States**:
   - **BUY**: Bullish consensus detected
   - **SELL**: Bearish consensus detected
   - **NEUTRAL**: No clear consensus or mixed signals

### Example Signal Response

```json
{
  "symbol": "AAPL",
  "signal": "BUY",
  "confidence": 0.75,
  "indicators": {
    "rsi": {"value": 28.5, "signal": "BUY"},
    "stochastic": {"value": 18.2, "signal": "BUY"},
    "bollinger": {"signal": "BUY"},
    "macd": {"signal": "NEUTRAL"}
  },
  "trend": "BULLISH",
  "timestamp": "2025-09-29T12:00:00Z"
}
```

## 🧪 Testing


### Manual API Testing

Once the backend is running, you can test these endpoints:

#### Health Check
```bash
curl http://localhost:8000/health
```

#### Authentication
```bash
# Register user
curl -X POST http://localhost:8000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123","full_name":"Test User"}'

# Login
curl -X POST http://localhost:8000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123"}'
```

#### Stock Data
```bash
# Get stock quote
curl http://localhost:8000/api/stocks/AAPL

# Get historical data
curl http://localhost:8000/api/stocks/AAPL/historical?interval=daily&days=30

# Get technical indicators
curl http://localhost:8000/api/indicators/AAPL?interval=daily
```

#### Crypto Data
```bash
# Get crypto quote
curl http://localhost:8000/api/crypto/BTC

# Get historical data
curl http://localhost:8000/api/crypto/BTC/historical?interval=daily&days=30
```

#### Analysis & Signals
```bash
# Get signal analysis
curl http://localhost:8000/api/analysis/AAPL?market_type=stock
```

## 📱 Building & Deployment

### Building Android APK

```bash
cd StellarIQ_Mobile

# Build development APK
eas build --platform android --profile preview

# Build production APK
eas build --platform android --profile production

# Local build (requires Android Studio)
expo prebuild
yarn android
```

Built APKs are stored in the `apkBuilds/` directory.

### Building iOS App

```bash
cd StellarIQ_Mobile

# Build for iOS (requires macOS)
eas build --platform ios --profile preview

# Local build (requires Xcode)
expo prebuild
yarn ios
```

### Backend Deployment

#### Using Docker
```bash
cd StellarIQ_API

# Build Docker image
docker build -t stellariq-backend .

# Run container
docker run -p 8000:8000 \
  -e DATABASE_URL=your_db_url \
  -e VALKEY_URL=your_redis_url \
  -e ALPHA_VANTAGE_API_KEY=your_api_key \
  stellariq-backend
```

#### Using Docker Compose
```bash
cd StellarIQ_API
docker-compose up -d
```

#### Manual Deployment
```bash
cd StellarIQ_API

# Install dependencies
pip install -r requirements.txt

# Run migrations
alembic upgrade head

# Start with Uvicorn
uvicorn main:app --host 0.0.0.0 --port 8000
```

## 📚 API Documentation

Once the backend is running, interactive API documentation is available:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Key API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/api/auth/register` | POST | User registration |
| `/api/auth/login` | POST | User login |
| `/api/stocks/{symbol}` | GET | Get stock quote |
| `/api/crypto/{symbol}` | GET | Get crypto quote |
| `/api/stocks/{symbol}/historical` | GET | Historical stock data |
| `/api/crypto/{symbol}/historical` | GET | Historical crypto data |
| `/api/indicators/{symbol}` | GET | Technical indicators |
| `/api/analysis/{symbol}` | GET | Signal analysis |
| `/api/favorites` | GET/POST/DELETE | Manage favorites |
| `/api/notifications` | GET/POST | Manage notifications |

## ⚡ Performance Optimization

### Caching Strategy
- **Valkey (Redis)**: Caches API responses for 15 minutes (configurable)
- **Quote Cache**: Real-time quotes cached for quick access
- **Historical Data Cache**: Daily/weekly/monthly data cached longer
- **Indicator Cache**: Technical indicators cached to reduce computation

### Rate Limiting
- **Alpha Vantage**: Respects API rate limits (5 calls/min for free tier)
- **Request Queuing**: Automatic queuing when rate limit is reached
- **Smart Batching**: Combines multiple requests when possible

### Background Tasks
- **Market Monitor**: Updates watchlist prices every 5 minutes
- **Data Refresh**: Refreshes cached data periodically
- **Notification Dispatch**: Sends price alerts based on user preferences

### Best Practices
- Use caching to minimize API calls
- Implement pagination for large datasets
- Use WebSockets for real-time updates (future enhancement)
- Optimize database queries with proper indexing

## 🔧 Development Tools & Scripts

### Backend Scripts

```bash
cd StellarIQ_API

# Run database migrations
alembic upgrade head

# Create new migration
alembic revision --autogenerate -m "description"

# Downgrade migration
alembic downgrade -1
```

### Mobile Scripts

```bash
cd StellarIQ_Mobile

# Start with cache cleared
yarn start:clear

# Start with tunnel (for testing on external devices)
yarn start:tunnel

# Clean project
yarn clean

# Check project health
yarn doctor

# Prebuild native code
yarn prebuild
```

## 🐛 Troubleshooting

### Backend Issues

**Database connection errors**:
```bash
# Check if PostgreSQL is running
docker ps

# Restart database
docker-compose restart postgres

# Check database logs
docker-compose logs postgres
```

**Valkey/Redis connection errors**:
```bash
# Check if Valkey is running
docker ps

# Restart Valkey
docker-compose restart valkey

# Test connection
redis-cli ping
```

**API rate limit errors**:
- Check your Alpha Vantage API key
- Verify rate limit settings in `.env`
- Wait for rate limit window to reset (1 minute)

### Mobile App Issues

**Metro bundler errors**:
```bash
# Clear cache and restart
yarn start:clear

# Or manually clear
expo start -c
```

**Module not found errors**:
```bash
# Reinstall dependencies
rm -rf node_modules
yarn install
```

**Android build errors**:
```bash
# Clean Android build
cd android
./gradlew clean
cd ..
yarn android
```

**Expo Go connection issues**:
- Ensure phone and computer are on the same network
- Use tunnel mode: `yarn start:tunnel`
- Check firewall settings

## 📖 Additional Resources

### Documentation
- [FastAPI Documentation](https://fastapi.tiangolo.com/) - Backend framework
- [React Native Documentation](https://reactnative.dev/) - Mobile framework
- [Expo Documentation](https://docs.expo.dev/) - Expo platform
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/) - ORM
- [TanStack Query Documentation](https://tanstack.com/query) - Data fetching
- [Victory Native Documentation](https://formidable.com/open-source/victory/) - Charts

### APIs & Data Sources
- [Alpha Vantage API](https://www.alphavantage.co/documentation/) - Market data provider
- [Alpha Vantage Support](https://www.alphavantage.co/support/) - API support

### Tools & Libraries
- [Alembic](https://alembic.sqlalchemy.org/) - Database migrations
- [Valkey](https://valkey.io/) - Redis-compatible cache
- [APScheduler](https://apscheduler.readthedocs.io/) - Background tasks
- [Pydantic](https://docs.pydantic.dev/) - Data validation
- [React Navigation](https://reactnavigation.org/) - Navigation
- [Zustand](https://github.com/pmndrs/zustand) - State management

## 📄 License

This project is a proof of concept and is provided as-is for educational purposes.

## 🙏 Acknowledgments

- **Jason Scherrer at [Renew Inbound](https://portal.renewinboundhq.com/i/partners?ref=DMG)** for giving me the permission to use his idea for this app. If you need bookkeeping, they are the best.
- **Alpha Vantage** for providing comprehensive market data API
- **FastAPI** team for the excellent Python framework
- **Expo** team for simplifying React Native development
- **Open source community** for the amazing tools and libraries

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Check existing documentation
- Review API documentation at `/docs` endpoint

---

**Note**: This is a proof of concept application. Market data is delayed by 15 minutes and should not be used for actual trading decisions. Always consult with financial professionals before making investment decisions.
