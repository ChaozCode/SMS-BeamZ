# 📱 BeamZ - SMS API Platform

> Fast, cheap, reliable SMS messaging for developers.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue)](https://www.typescriptlang.org/)

## 🚀 Why BeamZ?

| Feature | BeamZ | Twilio |
|---------|-------|--------|
| Price/SMS (US) | **$0.003** | $0.0079 |
| Bulk Rate | **$0.002** | $0.0075 |
| Setup Fee | **$0** | $0 |
| Monthly Minimum | **$0** | $0 |

**60% cheaper than Twilio** with the same reliability.

## ⚡ Quick Start

### Install SDK

```bash
npm install @beamz/sdk
# or
yarn add @beamz/sdk
# or
pnpm add @beamz/sdk
```

### Send Your First SMS

```typescript
import { BeamZ } from '@beamz/sdk';

const beamz = new BeamZ('your_api_key');

const message = await beamz.messages.send({
  to: '+14155551234',
  from: '+14155559876',
  body: 'Hello from BeamZ! 🚀'
});

console.log(`Message sent: ${message.id}`);
```

### Python

```python
from beamz import BeamZ

client = BeamZ('your_api_key')

message = client.messages.send(
    to='+14155551234',
    from_='+14155559876',
    body='Hello from BeamZ! 🚀'
)

print(f'Message sent: {message.id}')
```

### cURL

```bash
curl -X POST https://api.beamz.io/v1/messages \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "+14155551234",
    "from": "+14155559876",
    "body": "Hello from BeamZ!"
  }'
```

## 📦 Features

- ✅ **Simple REST API** - Send SMS in one API call
- ✅ **Global Coverage** - 200+ countries supported
- ✅ **Delivery Reports** - Real-time webhook callbacks
- ✅ **Phone Numbers** - Buy and manage numbers via API
- ✅ **Two-Way SMS** - Receive incoming messages
- ✅ **MMS Support** - Send images and media (coming soon)
- ✅ **SDKs** - Node.js, Python, and more
- ✅ **Dashboard** - Web UI for management

## 📊 Pricing

| Tier | Price/SMS | Volume |
|------|-----------|--------|
| Pay-as-you-go | $0.003 | Any |
| Starter | $0.0025 | 10K+/mo |
| Growth | $0.002 | 100K+/mo |
| Enterprise | Custom | 1M+/mo |

No monthly fees. No contracts. Cancel anytime.

## 🛠️ Development

### Prerequisites

- Node.js 20+
- PostgreSQL 16+
- Redis 7+
- pnpm 8+

### Setup

```bash
# Clone the repo
git clone https://github.com/ChaozCode/SMS-BeamZ.git
cd SMS-BeamZ

# Install dependencies
pnpm install

# Setup environment
cp .env.example .env

# Run database migrations
pnpm db:migrate

# Start development server
pnpm dev
```

### Project Structure

```
SMS-BeamZ/
├── apps/
│   ├── api/           # REST API server
│   ├── dashboard/     # Next.js web app
│   └── docs/          # Documentation site
├── packages/
│   ├── core/          # Shared business logic
│   ├── sdk-node/      # Node.js SDK
│   └── sdk-python/    # Python SDK
├── services/
│   ├── message-processor/
│   └── webhook-dispatcher/
└── infrastructure/
    ├── docker/
    └── terraform/
```

## 📚 Documentation

- [API Reference](https://docs.beamz.io/api)
- [Quickstart Guide](https://docs.beamz.io/quickstart)
- [SDKs](https://docs.beamz.io/sdks)
- [Webhooks](https://docs.beamz.io/webhooks)
- [Pricing](https://beamz.io/pricing)

## 🔗 Links

- **Website**: https://beamz.io
- **Dashboard**: https://app.beamz.io
- **API**: https://api.beamz.io
- **Status**: https://status.beamz.io

## 📄 License

MIT © [ChaozCode](https://chaozcode.com)

---

**BeamZ** - *SMS that doesn't break the bank* 💸
