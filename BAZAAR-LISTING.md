# Getting Listed on x402 Bazaar

## Overview

Your Weather Data MCP will automatically appear on **https://x402bazaar.app** after your first paid call settles through the CDP Facilitator. No registration form needed!

## Current Status

✅ **Implementation Complete**: Weather API with x402 payment middleware
✅ **x402 Discovery**: `/.well-known/x402` endpoint ready
✅ **MCP Compatible**: `/mcp/tools` endpoint configured
⏳ **Deployment**: Ready to deploy to Vercel

## How to Get Listed

### Step 1: Deploy to Vercel ✅ IN PROGRESS

Once deployed, validate your endpoint:

```bash
curl -i https://weather-data-mcp.vercel.app/api/current?location=London
```

Should return:
```
HTTP/1.1 402 Payment Required
```

### Step 2: Wait for First Paid Call

Once a user or AI agent completes a paid call through the CDP Facilitator:
1. Payment settles on Base Mainnet
2. CDP automatically catalogs your endpoint
3. Your service appears on x402bazaar.app within minutes

### Step 3: Optional - Manual Testing

You can test with CDP's x402 tooling or wait for organic discovery.

## Discovery Confirmation

After a paid call, check the `EXTENSION-RESPONSES` header in the settle response (base64-encoded JSON):

- `"success"` - Metadata cataloged ✅
- `"processing"` - Being cataloged asynchronously ⏳
- `"rejected"` - Check `rejectedReason` for validation errors ❌

## Requirements for Listing

### Required:
- ✅ Public HTTPS URL
- ✅ Returns `402 Payment Required`
- ✅ Valid x402 discovery endpoint
- ✅ Accepts payments through CDP Facilitator
- ✅ Base/USDC only

### For Featured/Curated Tier:
- Live mainnet payments
- ≥99% availability (30-day window)
- Complete input schemas and examples
- Clear agent-focused description
- Passes platform health probes

## Your Endpoint Details

**Base URL**: `https://weather-data-mcp.vercel.app` (to be deployed)
**Method**: `GET`  
**Price**: $0.002 USDC  
**Network**: Base Mainnet (eip155:8453)  
**Payment Address**: `0xf081ee84c0d85278a6242bc265f0b312021ebeb1`

**Primary Endpoints**:
1. `/api/current?location=London` - Get current weather
2. `/api/forecast?location=Paris&days=5` - Get forecast
3. `/api/coordinates?lat=40.7128&lon=-74.0060` - Get weather by coordinates

**Example Request**:
```bash
GET /api/current?location=London
```

**Example Response**:
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
  }
}
```

## Maintenance

To stay listed:
- Complete at least 1 paid call every 30 days
- Maintain ≥99% uptime
- Continue returning 402 for unpaid requests
- Respond to health probes

**Auto-removal happens when**:
- No settlements for 30+ days
- Health probes fail consistently
- Endpoint stops returning 402

## Tracking Your Listing

Once listed, find your endpoint on:
- **Browse**: https://x402bazaar.app
- **Search by tags**: weather, climate, forecast, location, travel, planning, mcp
- **Your payment address**: Search by `0xf081ee84c0d85278a6242bc265f0b312021ebeb1`

## Use Cases for AI Agents

Your Weather Data MCP is perfect for:
- **Travel Planning** - Check weather before booking trips
- **Event Planning** - Schedule outdoor activities optimally
- **Market Analysis** - Weather impacts retail, commodities, energy markets
- **Location Recommendations** - Suggest activities based on current conditions
- **Climate Research** - Analyze weather patterns and trends
- **Smart Automation** - Integrate with smart home and IoT systems
- **Agriculture** - Monitor conditions for farming decisions
- **Logistics** - Plan shipments and routes around weather

## Metadata Quality

**Description**: 
"Real-time weather and climate data for AI agents. Current conditions, 5-day forecasts, and global coverage for 200,000+ cities. Get temperature, humidity, wind, and conditions by location name or coordinates. Perfect for travel planning, event scheduling, market analysis, and location-based recommendations."

**Tags**:
- weather
- climate
- forecast
- temperature
- location
- travel
- planning
- mcp
- real-time
- global

## Support

- **x402 Docs**: https://docs.cdp.coinbase.com/x402
- **GitHub**: https://github.com/coinbase/x402
- **Bazaar**: https://x402bazaar.app
- **Live API**: https://weather-data-mcp.vercel.app (to be deployed)

## Next Steps

⏳ Deploying to Vercel
⏳ Creating GitHub repository
⏳ Validating all endpoints
⏳ Waiting for first paid call to auto-list on Bazaar

Your MCP is ready for deployment!

---

**Coming soon!** After deployment, your first paid call will automatically list you on x402bazaar.app! 🚀
