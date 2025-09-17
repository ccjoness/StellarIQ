# StellarIQ

A proof of concept financial analysis platform providing real-time market data, technical indicators, and intelligent trading signals for both cryptocurrency and equity markets.

## Features

- **Unified Search**: Search across crypto and equity markets with unified results
- **Real-time Data**: Live price feeds from CoinGecko and Finnhub APIs
- **Technical Analysis**: Advanced indicators including RSI, Stochastic, Bollinger Bands, and MACD
- **Smart Signals**: Intelligent signal generation with confidence scoring
- **Watchlist**: Personal watchlist with push notifications - Not implemented yet
- **Cross-platform**: React Native mobile app with responsive design

## Architecture

### Backend (FastAPI)
- **API**: FastAPI with Python 3.12
- **Database**: PostgreSQL with SQLAlchemy 2.0
- **Cache**: Redis for performance optimization
- **Tasks**: APScheduler for background data updates
- **Testing**: pytest with comprehensive coverage

### Mobile App (React Native)
- **Framework**: Expo with TypeScript
- **State Management**: TanStack Query
- **Charts**: Victory Native for technical analysis visualization
- **Navigation**: React Navigation v6
- **Notifications**: Expo Notifications for alerts

### Data Sources
- **All Market Data**: Alpha Vantage API (stocks + crypto)
- **Stock Data**: Real-time quotes, company overviews, historical OHLCV data
- **Crypto Data**: Real-time exchange rates, historical OHLCV data
- **Coverage**: Real-time quotes, historical data, technical indicators, market metadata

### Premium Features (Alpha Vantage Premium)
- **🚀 75 API calls/minute** (vs 5 for free tier)
- **⚡ 0.8 second intervals** (vs 12 seconds for free tier)
- **📊 15-minute delayed intraday data** (vs end-of-day for free tier)
- **📈 Intraday data access** (1min, 5min, 15min, 30min, 60min intervals)
- **🎯 Higher data quality** and more frequent updates
- **💪 Better performance** for near real-time applications
- **⚠️ Note**: Data is delayed by 15 minutes, not real-time

## Tech Stack

| Component | Technology |
|-----------|------------|
| Mobile App | React Native (Expo) + TypeScript |
| Backend API | FastAPI + Python 3.12 |
| Database | PostgreSQL + SQLAlchemy 2.0 |
| Cache | Redis |
| State Management | TanStack Query |
| Charts | Victory Native |
| Background Tasks | APScheduler |
| Testing | pytest + Jest |
| Linting | ESLint + Prettier + mypy + Ruff |
| DevOps | Docker + GitHub Actions |

## Project Structure

```
StellarIQ/
├── backend/                 # FastAPI backend
│   ├── app/
│   │   ├── api/            # API routes
│   │   ├── core/           # Core configuration
│   │   ├── models/         # SQLAlchemy models
│   │   ├── services/       # Business logic
│   │   ├── tasks/          # Background tasks
│   │   └── utils/          # Utilities
│   ├── tests/              # Backend tests
│   ├── alembic/            # Database migrations
│   ├── Dockerfile
│   ├── pyproject.toml
│   └── requirements.txt
├── mobile/                 # React Native app
│   ├── src/
│   │   ├── components/     # Reusable components
│   │   ├── screens/        # App screens
│   │   ├── services/       # API services
│   │   ├── hooks/          # Custom hooks
│   │   ├── types/          # TypeScript types
│   │   └── utils/          # Utilities
│   ├── __tests__/          # Mobile tests
│   ├── package.json
│   └── app.json
├── docker-compose.yml      # Development environment
├── .github/                # CI/CD workflows
└── docs/                   # Documentation
```

## Quick Start

### Prerequisites
- Node.js 18+ and Yarn
- Python 3.12+ and Poetry
- Docker and Docker Compose
- Expo CLI

### Backend Setup

1. **Clone and setup backend**:
```bash
cd backend
poetry install
cp .env .env
# Edit .env with your API keys
```

2. **Start services**:
```bash
docker-compose up -d postgres redis
poetry run alembic upgrade head
poetry run uvicorn app.main:app --reload
```

### Mobile App Setup

1. **Setup mobile app**:
```bash
cd mobile
yarn install
```

2. **Start development**:
```bash
yarn start
# Scan QR code with Expo Go app
```

## Configuration

### Environment Variables

#### Backend (.env)
```env
# Database
DATABASE_URL=postgresql://stellariq:stellariq_password@localhost:5432/stellariq

# Redis
REDIS_URL=redis://localhost:6379

# API Keys (Alpha Vantage required)
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_api_key_here

# Alpha Vantage Premium Configuration (optional)
ALPHA_VANTAGE_CALLS_PER_MINUTE=75  # 5 for free, 75 for premium

# Security
SECRET_KEY=your-super-secret-key-change-this-in-production

# Environment
ENVIRONMENT=development
LOG_LEVEL=INFO
```

#### Mobile (app.json)
```json
{
  "expo": {
    "extra": {
      "apiUrl": "http://localhost:8000"
    }
  }
}
```

**Note for Android/Physical Devices**: Replace `localhost` with your computer's IP address:
```json
{
  "expo": {
    "extra": {
      "apiUrl": "http://192.168.1.100:8000"
    }
  }
}
```

## Technical Indicators

### Implemented Signals
- **RSI (14)**: Oversold < 30, Overbought > 70
- **Stochastic %K (14,3)**: Oversold < 20, Overbought > 80
- **Bollinger Bands (20, 2σ)**: Price breakouts
- **MACD (12,26,9)**: Trend confirmation

### Signal Logic
- **Consensus**: ≥2 indicators agree → show signal state
- **Confidence**: Fraction of agreeing indicators (0-1)
- **Consistency**: Last 3 bars trend analysis

## Testing

### Backend Tests
```bash
cd backend
# Run all tests
poetry run pytest --cov=app tests/

# Test API integrations
poetry run python test_alpha_vantage.py    # Test Alpha Vantage integration
poetry run python test_env.py              # Test environment variables
```

### Mobile Tests
```bash
cd mobile
yarn test                                   # Jest tests
yarn lint                                   # ESLint
yarn type-check                             # TypeScript check
```

### API Endpoints Testing
Once backend is running, test these endpoints:
- **Health**: http://localhost:8000/health
- **Stock with signals**: http://localhost:8000/api/v1/tickers/AAPL?market_type=stock
- **Historical data**: http://localhost:8000/api/v1/tickers/AAPL/historical?market_type=stock&days=30
- **Signal analysis**: http://localhost:8000/api/v1/signals/analyze/AAPL?market_type=stock

## Deployment

### Backend (Docker)
```bash
docker build -t stellariq-backend ./backend
docker run -p 8000:8000 stellariq-backend
```

### Mobile (Expo)
```bash
cd mobile
expo build:android
expo build:ios
```

## API Documentation

Once the backend is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Performance Tips
- **Caching**: Redis cache reduces API calls significantly
- **Rate limiting**: Built-in rate limiting respects API limits
- **Background tasks**: Data updates happen automatically every 5 minutes

## Links

### Documentation
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [React Native Documentation](https://reactnative.dev/)
- [Expo Documentation](https://docs.expo.dev/)

### APIs & Data Sources
- [Alpha Vantage API](https://www.alphavantage.co/documentation/) - All market data (stocks + crypto)

### Tools & Libraries
- [Poetry](https://python-poetry.org/) - Python dependency management
- [TanStack Query](https://tanstack.com/query) - Data fetching for React
- [Victory Native](https://formidable.com/open-source/victory/) - Data visualization
