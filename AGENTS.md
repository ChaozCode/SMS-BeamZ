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

## 📊 SMS MARKET RESEARCH (2025-2026) - US & CANADA FOCUS

### 🏆 RECOMMENDED CARRIERS (Best Price + AI/API Success)

#### Primary: **Telnyx** ⭐ (Best Overall for US/Canada)
- **Base Rate**: $0.004/SMS + carrier fees
- **Effective US Cost**: ~$0.007-0.008/SMS (includes AT&T $0.003, T-Mobile $0.0045, Verizon $0.004)
- **Canada**: Bell, Telus, Rogers - competitive rates
- **Why Telnyx**:
  - ✅ Best developer experience (REST + WebSocket)
  - ✅ Excellent AI/automation support
  - ✅ Direct carrier connections
  - ✅ Real-time delivery webhooks
  - ✅ 10DLC pre-registered = no extra fees
  - ✅ Volume discounts at 100M+ messages

#### Backup: **Bandwidth** (Direct Carrier - Enterprise)
- **10DLC Rate**: $0.004/SMS + $0.015/MMS
- **Toll-Free**: $0.007/SMS
- **Short Code**: $0.008/SMS
- **Why Bandwidth**:
  - ✅ Direct-to-carrier (owns network)
  - ✅ Powers Zoom, Microsoft, Google, RingCentral
  - ✅ Best for high-volume enterprise
  - ✅ No middleman markup

#### Alternative: **Plivo** (Good API, Higher Cost)
- **Base Rate**: $0.0055/SMS + carrier surcharges
- **Effective Cost**: ~$0.0085-0.0105/SMS
- **Carrier Fees**: AT&T $0.003, T-Mobile $0.0025, Verizon $0.005
- **Why Consider**:
  - ✅ Simple API, good docs
  - ✅ Powerpack included (smart routing)
  - ❌ Higher effective cost than Telnyx/Bandwidth

### 💰 REAL COST COMPARISON (US 10DLC)

| Provider | Base | + AT&T | + T-Mobile | + Verizon | Effective Avg |
|----------|------|--------|------------|-----------|---------------|
| **Telnyx** | $0.004 | $0.007 | $0.0085 | $0.008 | **$0.0075** |
| **Bandwidth** | $0.004 | ~$0.007 | ~$0.008 | ~$0.008 | **$0.0075** |
| **Plivo** | $0.0055 | $0.0085 | $0.008 | $0.0105 | **$0.009** |
| **Twilio** | $0.0079 | $0.011 | $0.012 | $0.012 | **$0.012** |

### 🇨🇦 CANADA PRICING

| Provider | Bell/Virgin | Telus | Rogers | Effective |
|----------|-------------|-------|--------|-----------|
| **Telnyx** | $0.004 | $0.004 | $0.004 | **$0.004** (no carrier fees!) |
| **Bandwidth** | Custom | Custom | Custom | ~$0.005-0.007 |
| **Plivo** | $0.0143 | $0.0152 | $0.0155 | **$0.015** (expensive!) |

### 🎯 BEAMZ STRATEGY

**Primary Carrier**: Telnyx (US + Canada)
- Best price-to-reliability ratio
- Excellent API for AI integration
- Direct carrier relationships
- Auto-failover built-in

**Failover Carrier**: Bandwidth
- Enterprise-grade reliability
- Direct network ownership
- Use for high-priority messages

**Pricing Tiers**:
| Tier | Price/SMS | Margin | Target |
|------|-----------|--------|--------|
| Pay-as-you-go | $0.003 | ~60% | Developers |
| Starter (10K+) | $0.0025 | ~65% | Startups |
| Growth (100K+) | $0.002 | ~70% | Scale-ups |
| Enterprise (1M+) | Custom | ~75% | Enterprise |

### Key Differentiators
1. **Price Leadership**: 60% cheaper than Twilio
2. **US + Canada Native**: Optimized for North America
3. **AI-Friendly API**: Built for automation/AI workflows
4. **Transparent Pricing**: No hidden carrier fees (we absorb them)
5. **Smart Routing**: Auto-select cheapest carrier per destination

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
│  Carrier Aggregation Layer (US/Canada Optimized)             │
│  ├─ Telnyx (PRIMARY - US/Canada, best price)                │
│  │   └─ $0.004 base + carrier fees, excellent AI/API        │
│  ├─ Bandwidth (FAILOVER - direct carrier, enterprise)       │
│  │   └─ $0.004 base, owns network, powers Zoom/Microsoft    │
│  └─ Smart Router: Auto-select cheapest per destination      │
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
