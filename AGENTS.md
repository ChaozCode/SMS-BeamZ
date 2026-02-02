# AGENTS.md - BeamZ SMS Platform
# AI Agent Instructions for SMS-BeamZ Development
# Version: 1.0.0 | Created: 2026-02-02

---

## 🚀 PROJECT OVERVIEW

**Package Name**: SMS-BeamZ  
**App Name**: BeamZ  
**Purpose**: High-performance SMS messaging platform with competitive pricing  
**Repository**: https://github.com/ChaozCode/SMS-BeamZ

### Mission
Build a cost-effective, developer-friendly SMS API that beats Twilio pricing while maintaining enterprise-grade reliability.

---

## 📊 SMS MARKET RESEARCH (2025-2026)

### Competitive Pricing Analysis

| Provider | Price/SMS (US) | Bulk Rate | Notes |
|----------|---------------|-----------|-------|
| **Twilio** | $0.0079 | $0.0075 | Industry standard, expensive |
| **Sinch** | $0.0078 | Custom | Good omnichannel |
| **Telnyx** | $0.004 | $0.003 | Developer favorite |
| **Plivo** | $0.005 | $0.004 | Good API docs |
| **Vonage** | $0.0068 | Custom | Enterprise focused |
| **MessageBird** | $0.006 | $0.005 | EU-focused |
| **Textla** | $0.01 | $0.08 | Small business |
| **ClickSend** | $0.006 | $0.005 | Competitive |

### BeamZ Target Pricing
- **Standard**: $0.003/SMS (60% cheaper than Twilio)
- **Bulk (10K+)**: $0.002/SMS
- **Enterprise**: Custom pricing from $0.001/SMS

### Key Differentiators
1. **Price Leadership**: Cheapest reliable SMS API
2. **Developer Experience**: Simple REST API, great SDKs
3. **Transparency**: No hidden fees, pay-as-you-go
4. **Speed**: Sub-100ms delivery latency
5. **Global Reach**: 200+ countries supported

---

## 🏗️ ARCHITECTURE

```
┌─────────────────────────────────────────────────────────────┐
│                      BeamZ Platform                          │
├─────────────────────────────────────────────────────────────┤
│  API Gateway (Kong/Express)                                  │
│  ├─ Rate Limiting                                           │
│  ├─ Authentication (API Keys + JWT)                         │
│  └─ Request Routing                                         │
├─────────────────────────────────────────────────────────────┤
│  Core Services                                               │
│  ├─ Message Service (send, receive, status)                 │
│  ├─ Number Service (buy, manage phone numbers)              │
│  ├─ Webhook Service (delivery reports, inbound)             │
│  ├─ Analytics Service (usage, costs, reports)               │
│  └─ Billing Service (credits, invoices)                     │
├─────────────────────────────────────────────────────────────┤
│  Carrier Aggregation Layer                                   │
│  ├─ Telnyx (primary US)                                     │
│  ├─ Plivo (backup US)                                       │
│  ├─ Sinch (international)                                   │
│  └─ Direct carrier connections (future)                     │
├─────────────────────────────────────────────────────────────┤
│  Infrastructure                                              │
│  ├─ PostgreSQL (messages, users, billing)                   │
│  ├─ Redis (rate limiting, caching, queues)                  │
│  ├─ Kafka (message queuing, event streaming)                │
│  └─ S3 (message logs, attachments)                          │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 PROJECT STRUCTURE

```
SMS-BeamZ/
├── .github/
│   ├── copilot-instructions.md   # Copilot-specific instructions
│   └── workflows/                 # CI/CD pipelines
├── apps/
│   ├── api/                       # Main API server
│   ├── dashboard/                 # Web dashboard (Next.js)
│   └── docs/                      # Documentation site
├── packages/
│   ├── core/                      # Shared business logic
│   ├── sdk-node/                  # Node.js SDK
│   ├── sdk-python/                # Python SDK
│   └── types/                     # Shared TypeScript types
├── services/
│   ├── message-processor/         # Message queue worker
│   ├── webhook-dispatcher/        # Webhook delivery
│   └── analytics-aggregator/      # Usage analytics
├── infrastructure/
│   ├── docker/                    # Docker configurations
│   ├── k8s/                       # Kubernetes manifests
│   └── terraform/                 # Infrastructure as code
├── docs/
│   ├── api-reference.md           # API documentation
│   ├── quickstart.md              # Getting started guide
│   └── pricing.md                 # Pricing documentation
├── AGENTS.md                      # This file
├── README.md                      # Project overview
├── package.json                   # Root package.json (monorepo)
└── turbo.json                     # Turborepo configuration
```

---

## 🛠️ TECH STACK

### Backend
- **Runtime**: Node.js 20+ / Bun
- **Framework**: Express.js or Fastify
- **Language**: TypeScript 5.x
- **Database**: PostgreSQL 16 + TimescaleDB
- **Cache**: Redis 7.x
- **Queue**: BullMQ / Kafka
- **ORM**: Prisma or Drizzle

### Frontend (Dashboard)
- **Framework**: Next.js 14 (App Router)
- **Styling**: Tailwind CSS
- **Components**: Radix UI + shadcn/ui
- **State**: Zustand / TanStack Query
- **Charts**: Recharts

### Infrastructure
- **Containers**: Docker
- **Orchestration**: Kubernetes
- **IaC**: Terraform
- **CI/CD**: GitHub Actions
- **Monitoring**: Prometheus + Grafana
- **Logging**: ELK Stack

### SDKs
- **Node.js**: TypeScript, axios-based
- **Python**: requests-based, typed
- **Go**: net/http, idiomatic (future)
- **PHP**: Guzzle-based (future)

---

## 🔌 API DESIGN

### Base URL
```
https://api.beamz.io/v1
```

### Authentication
```bash
curl -X POST https://api.beamz.io/v1/messages \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

### Core Endpoints

#### Send SMS
```http
POST /v1/messages
{
  "to": "+1234567890",
  "from": "+0987654321",
  "body": "Hello from BeamZ!"
}

Response:
{
  "id": "msg_abc123",
  "status": "queued",
  "to": "+1234567890",
  "from": "+0987654321",
  "body": "Hello from BeamZ!",
  "cost": 0.003,
  "created_at": "2026-02-02T08:00:00Z"
}
```

#### Get Message Status
```http
GET /v1/messages/{id}
```

#### List Messages
```http
GET /v1/messages?from=2026-01-01&to=2026-02-01&limit=100
```

#### Buy Phone Number
```http
POST /v1/phone-numbers
{
  "country": "US",
  "area_code": "415",
  "capabilities": ["sms", "mms"]
}
```

#### Webhooks
```http
POST /v1/webhooks
{
  "url": "https://your-server.com/webhook",
  "events": ["message.delivered", "message.failed", "message.received"]
}
```

---

## 🎯 DEVELOPMENT GUIDELINES

### Code Style
- Use TypeScript strict mode
- ESLint + Prettier for formatting
- Conventional commits
- 100% type coverage on public APIs

### Testing
- Unit tests: Vitest
- Integration tests: Supertest
- E2E tests: Playwright (dashboard)
- Minimum 80% coverage

### Performance Targets
- API response time: <50ms p99
- Message delivery: <500ms to carrier
- Dashboard load: <1s FCP
- 99.9% uptime SLA

### Security
- API keys with scopes
- Rate limiting per key
- Request signing (optional)
- SOC2 compliance (roadmap)

---

## 🤖 AGENT BEHAVIORS

### When Building Features
1. Check existing architecture patterns
2. Use TypeScript with strict types
3. Add comprehensive tests
4. Update API documentation
5. Consider billing implications

### When Fixing Bugs
1. Write failing test first
2. Fix with minimal changes
3. Verify no regressions
4. Update changelog

### When Reviewing Code
1. Check type safety
2. Verify error handling
3. Assess performance impact
4. Ensure backward compatibility

### Carrier Integration Rules
1. Always use carrier abstraction layer
2. Implement retry logic with exponential backoff
3. Log all carrier responses
4. Handle carrier-specific error codes

---

## 📈 ROADMAP

### Phase 1: MVP (Q1 2026)
- [ ] Core messaging API
- [ ] Basic dashboard
- [ ] Node.js SDK
- [ ] US number provisioning
- [ ] Pay-as-you-go billing

### Phase 2: Growth (Q2 2026)
- [ ] Python SDK
- [ ] International numbers
- [ ] Webhook system
- [ ] Usage analytics
- [ ] Multi-user accounts

### Phase 3: Scale (Q3 2026)
- [ ] Direct carrier connections
- [ ] MMS support
- [ ] Two-way messaging
- [ ] API versioning
- [ ] SOC2 certification

### Phase 4: Enterprise (Q4 2026)
- [ ] Dedicated instances
- [ ] SLA guarantees
- [ ] White-label option
- [ ] Go & PHP SDKs

---

## 🔗 RESOURCES

### External APIs (Carriers)
- Telnyx: https://developers.telnyx.com
- Plivo: https://www.plivo.com/docs
- Sinch: https://developers.sinch.com

### Inspiration
- Twilio API: https://www.twilio.com/docs
- Resend (email): https://resend.com/docs

### Internal Services
- Memory Spine: http://127.0.0.1:8788
- Zearch: http://127.0.0.1:5001
- ChaozCode Services: Ports 8850-8863

---

*BeamZ - Fast, Cheap, Reliable SMS*
*Version 1.0.0 | 2026-02-02*
