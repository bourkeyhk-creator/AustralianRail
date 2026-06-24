# Australian Rail News Aggregation Website

An AI-powered news aggregation platform focused exclusively on Australian train and railroad news.

## Overview

This project builds a modern news website (similar to RenewEconomy.com.au) that aggregates Australian railway news from multiple AI search platforms:
- Google News API
- Perplexity API
- NewsAPI

## Features

- **Multi-platform Search Aggregation**: Searches across Google, Perplexity, and NewsAPI
- **Content Filtering**: Automatically filters for Australian-only railway content
- **Intelligent Deduplication**: Removes duplicate articles across platforms
- **Caching Layer**: Reduces API calls and improves response times
- **Content Categories**: News, Analysis, Infrastructure, Policy, Freight, Passenger Services
- **Source Attribution**: Proper credit to original news sources
- **RESTful API**: Clean API endpoints for frontend consumption

## Project Structure

```
├── server.js                 # Express server entry point
├── src/
│   ├── config/              # Configuration files
│   ├── services/            # Business logic (search, filtering, deduplication)
│   ├── routes/              # API routes
│   ├── middleware/          # Express middleware
│   ├── models/              # Database models
│   ├── utils/               # Helper functions
│   └── logger/              # Logging configuration
├── database/
│   ├── migrations/          # Database migration scripts
│   └── seeds/               # Seed data
├── tests/                   # Unit and integration tests
└── docs/                    # API documentation
```

## Quick Start

### Prerequisites
- Node.js v16+
- PostgreSQL v12+
- API keys from: Google News, Perplexity, NewsAPI

### Installation

```bash
npm install
cp .env.example .env
# Edit .env with your configuration
npm run migrate
npm run dev
```

### Server runs on
```
http://localhost:3001
```

## API Endpoints

### Search for Australian Rail News
```
GET /api/articles/search
Query Parameters:
  - q: search query (optional)
  - category: rail|freight|passenger|infrastructure|policy|all (default: all)
  - limit: number of results (default: 20)
  - offset: pagination offset (default: 0)
  - sort: latest|relevant|trending (default: latest)
```

### Get Featured Articles
```
GET /api/articles/featured
Query Parameters:
  - limit: number of featured articles (default: 5)
```

### Get Articles by Category
```
GET /api/articles/category/:category
Query Parameters:
  - limit: number of results (default: 20)
  - offset: pagination offset (default: 0)
```

### Get Article Details
```
GET /api/articles/:id
```

## Content Filtering Rules

The system filters articles to ensure **Australian railway focus only**:

1. **Geographical Filter**: Must mention Australian locations/organizations
2. **Topic Filter**: Must be rail/train/railway related
3. **Content Filter**: Excludes non-train topics (aviation, shipping, general news, etc.)
4. **Keyword Matching**: Uses comprehensive Australian rail keywords

## Database Schema

See `database/migrations/` for schema details.

Key tables:
- `articles` - Cached articles from search APIs
- `sources` - Metadata about news sources
- `search_logs` - Track search queries for analytics
- `article_duplicates` - Track deduplicated content

## Environment Variables

See `.env.example` for all available configuration options.

## Development

```bash
# Run in development mode with auto-reload
npm run dev

# Run tests
npm test

# Run database migrations
npm run migrate
```

## API Key Setup

### Google News API
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a project
3. Enable News API
4. Create API key credentials

### Perplexity API
1. Visit [Perplexity API](https://www.perplexity.ai/)
2. Sign up and generate API key
3. Add to `.env`

### NewsAPI
1. Visit [NewsAPI.org](https://newsapi.org/)
2. Sign up for free tier
3. Generate API key

## Content Attribution

All articles include:
- Source URL (links to original article)
- Publication name
- Author (when available)
- Publish date
- Excerpt (not full reproduction - fair use)

## License

MIT
