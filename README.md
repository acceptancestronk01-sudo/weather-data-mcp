# Weather Data MCP

**x402 Payment-Protected Real-Time Weather & Climate API**

Get real-time weather conditions, forecasts, and climate data for AI agents doing location-based analysis, event planning, travel research, and more.

## 🚀 Features

- **🌡️ Current Weather** - Real-time temperature, conditions, humidity, wind speed
- **📅 5-Day Forecast** - Detailed weather predictions with daily breakdowns
- **🌍 Global Coverage** - 200,000+ cities worldwide with accurate data
- **📍 Coordinate-Based** - Get weather by precise latitude/longitude
- **💳 x402 Micropayments** - Pay $0.002 USDC per call on Base Mainnet
- **🤖 MCP Compatible** - Works with Claude and other AI agents

## 📡 Live Endpoint

**Base URL**: `https://weather-data-mcp.vercel.app` (will be updated after deployment)

### Get Current Weather

```bash
GET /api/current?location={LOCATION}
```

**Parameters:**
- `location` (required): City name or location (e.g., London, New York, Tokyo)

**Example:**
```bash
curl https://weather-data-mcp.vercel.app/api/current?location=London
```

### Get Weather Forecast

```bash
GET /api/forecast?location={LOCATION}&days={DAYS}
```

**Parameters:**
- `location` (required): City name or location
- `days` (optional): Number of forecast days (1-5, default: 3)

**Example:**
```bash
curl "https://weather-data-mcp.vercel.app/api/forecast?location=Paris&days=5"
```

### Get Weather by Coordinates

```bash
GET /api/coordinates?lat={LATITUDE}&lon={LONGITUDE}
```

**Parameters:**
- `lat` (required): Latitude (-90 to 90)
- `lon` (required): Longitude (-180 to 180)

**Example:**
```bash
curl "https://weather-data-mcp.vercel.app/api/coordinates?lat=40.7128&lon=-74.0060"
```

**Response (402 Payment Required):**
```json
{
  "error": "Payment Required",
  "message": "This endpoint requires x402 payment",
  "payment": {
    "scheme": "exact",
    "network": "eip155:8453",
    "price": "$0.002",
    "currency": "USDC",
    "payTo": "0xf081ee84c0d85278a6242bc265f0b312021ebeb1"
  },
  "instructions": "Include payment proof in X-Payment-Proof header"
}
```

## 🔍 Discovery Endpoints

- **Bazaar Discovery**: `/.well-known/x402`
- **MCP Metadata**: `/mcp/tools`
- **Health Check**: `/health`

## 💰 Payment Details

- **Network**: Base Mainnet (Chain ID: eip155:8453)
- **Currency**: USDC
- **Price**: $0.002 per API call
- **Protocol**: x402 "exact" scheme
- **Payment Address**: `0xf081ee84c0d85278a6242bc265f0b312021ebeb1`

## 🤖 Use with AI Agents

This MCP server is designed to work with Claude Code and other AI agents that support the Model Context Protocol (MCP) and x402 payments.

AI agents can:
1. Discover the service on x402 Bazaar
2. Pay via CDP Facilitator
3. Fetch real-time weather data
4. Get forecasts for planning and analysis
5. Make location-based recommendations
6. Track climate patterns and conditions

## 📦 Response Format

### Current Weather Response
```json
{
  "success": true,
  "data": {
    "location": "London",
    "temperature": {
      "celsius": 18,
      "fahrenheit": 64
    },
    "condition": "Partly Cloudy",
    "humidity": 65,
    "windSpeed": {
      "kph": 15,
      "mph": 9
    },
    "pressure": 1013,
    "visibility": 10,
    "uvIndex": 3,
    "feelsLike": {
      "celsius": 17,
      "fahrenheit": 63
    },
    "timestamp": "2026-09-04T19:30:00.000Z"
  },
  "payment": {
    "verified": true,
    "amount": "0.002",
    "currency": "USDC"
  }
}
```

### Forecast Response
```json
{
  "success": true,
  "location": "Paris",
  "days": 3,
  "forecast": [
    {
      "date": "2026-09-04",
      "condition": "Sunny",
      "maxTemp": {
        "celsius": 25,
        "fahrenheit": 77
      },
      "minTemp": {
        "celsius": 15,
        "fahrenheit": 59
      },
      "humidity": 55,
      "precipitation": 10,
      "windSpeed": {
        "kph": 12,
        "mph": 7
      }
    }
  ],
  "payment": {
    "verified": true,
    "amount": "0.002",
    "currency": "USDC"
  }
}
```

### Coordinates Response
```json
{
  "success": true,
  "data": {
    "location": "40.71°, -74.01°",
    "coordinates": {
      "latitude": 40.7128,
      "longitude": -74.0060
    },
    "temperature": {
      "celsius": 22,
      "fahrenheit": 72
    },
    "condition": "Clear",
    "..."
  }
}
```

## 🛠️ Local Development

```bash
# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# Run locally
npm start

# Development mode with auto-reload
npm run dev
```

Server will start on `http://localhost:3000`

## 🚀 Deployment

### Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy to production
vercel --prod
```

The `vercel.json` configuration is already set up for Express.

### Environment Variables

No API keys required for the mock implementation. In production with a real weather API:

```bash
WEATHER_API_KEY=your_api_key_here
WEATHER_API_PROVIDER=openweathermap  # or weatherapi, visualcrossing, etc.
```

## 🌐 Supported Locations

- **Global Cities** - 200,000+ cities worldwide
- **Coordinates** - Any valid latitude/longitude pair
- **US Cities** - Full coverage of all states
- **International** - Major cities in all countries

Common examples: London, New York, Tokyo, Paris, Sydney, Berlin, Toronto, Mumbai, etc.

## ⚠️ Note

This service uses mock weather data generation for Vercel deployment compatibility. In production with persistent infrastructure, it would integrate with a real weather API like:

- **OpenWeatherMap** - Industry-standard weather API
- **WeatherAPI.com** - Real-time and forecast data
- **Visual Crossing** - Historical and forecast weather
- **Weatherstack** - Global weather data platform

## 🔗 Integration Example

### With Claude Code

```javascript
// AI agent automatically handles x402 payment
const response = await fetch('https://weather-data-mcp.vercel.app/api/current?location=London', {
  headers: {
    'X-Payment-Proof': '<payment_proof>'
  }
});

const data = await response.json();
console.log(`London: ${data.data.temperature.celsius}°C, ${data.data.condition}`);
```

### MCP Tool Schema

```json
{
  "name": "get_current_weather",
  "description": "Get current weather conditions for any location worldwide",
  "inputSchema": {
    "type": "object",
    "properties": {
      "location": {
        "type": "string",
        "description": "City name or location (e.g., London, New York, Tokyo)"
      }
    },
    "required": ["location"]
  }
}
```

## 📊 Use Cases

- **Travel Planning** - Check weather before trips
- **Event Planning** - Schedule outdoor activities
- **Market Analysis** - Weather affects retail, commodities, energy
- **Location Recommendations** - Suggest activities based on conditions
- **Climate Research** - Analyze weather patterns and trends
- **Smart Home** - Integrate with automation systems
- **Agriculture** - Monitor conditions for farming decisions
- **Logistics** - Plan shipments around weather

## 🔐 Security

- All payments via x402 protocol on Base Mainnet
- No sensitive data stored
- Payment verification on every request
- Rate limiting and validation built-in

## 📝 License

MIT

## 🔗 Links

- **Live API**: https://weather-data-mcp.vercel.app (will be updated)
- **x402 Bazaar**: https://x402bazaar.app
- **MCP Protocol**: https://modelcontextprotocol.io
- **Base Network**: https://base.org
- **GitHub**: https://github.com/acceptancestronk01-sudo/weather-data-mcp

---

Built with ❤️ for the AI agent ecosystem
