# Chainbase Documentation Restructure Design

## Background

The current Chainbase documentation is organized around product lines and network concepts ("Learn and build" as primary tab), which is not optimized for developer onboarding. The goal is to restructure the documentation to be **developer-integration-first**, inspired by Stripe's documentation system.

### Core Objectives

1. **Developer-first**: Developers should immediately see integration paths when landing on the docs
2. **Elevate AI**: Raise Chainbase AI integration visibility to be parallel with API and Data Platform
3. **De-emphasize network narrative**: Move network concepts, architecture, tokenomics, run-a-node, and Theia into a "Chainbase Network" tab that is not the primary focus

## Design

### Tab Structure (5 tabs)

```
[Getting Started] | Developer Resources | API Reference | Data Catalog | Chainbase Network
```

| Tab | Purpose | Priority |
|-----|---------|----------|
| Getting Started | Scenario-driven developer onboarding | Primary (default) |
| Developer Resources | Product/tool reference documentation | Secondary |
| API Reference | Complete API endpoint documentation | Secondary |
| Data Catalog | Chain data schema reference (50+ chains) | Secondary |
| Chainbase Network | Network narrative, architecture, governance | De-emphasized |

### Tab 1: Getting Started (primaryTab, scenario-driven)

**Homepage**: One-line tagline + four scenario cards + "Explore All Products" link.

**Sidebar structure**:

```
├── Welcome
├── Explore All Products
├── Query Blockchain Data
│   ├── Quick Start (CLI quick experience)
│   ├── Using Web3 API
│   ├── Using SQL API
│   └── Using Tops API
├── Build AI Agents
│   ├── Quick Start (MCP quick integration)
│   ├── x402 Payment Protocol
│   └── Web3 Data Skill
├── Stream & Process Data
│   ├── Quick Start (Manuscript)
│   └── Data Sync
├── Explore Data in Cloud
│   └── Data Cloud Quick Start
└── Tutorials & Use Cases
    ├── Balance API Tutorials
    ├── Token API Tutorials
    ├── NFT API Tutorials
    └── Domain API Tutorials
```

**Explore All Products page** — product index grouped by capability:

| Category | Products |
|----------|----------|
| AI Integration | MCP Servers, x402 Payment Protocol, Web3 Data Skill |
| Data Access | Web3 API, SQL API, Tops API, CLI |
| Data Processing | Manuscript, Data Cloud, Data Sync |
| Data Discovery | Data Catalog |

Each product links to its detailed page in Developer Resources.

### Tab 2: Developer Resources (tool reference, product-organized)

```
├── Chainbase AI
│   ├── Overview
│   ├── MCP Servers
│   ├── x402 Payment Protocol
│   └── Web3 Data Skill
├── Data Platform
│   ├── Overview
│   ├── Web3 API
│   ├── SQL API
│   ├── Tops API
│   ├── Data Cloud
│   └── Data Sync
├── Manuscript
│   ├── Overview
│   ├── QuickStart (Prerequisites / Create / Run / Advanced)
│   └── Zone
└── CLI
    └── Installation & Commands
```

### Tab 3: API Reference (existing, remove Chain RPC)

```
├── Overview / Status Codes / JWT Auth
├── Web3 API (Basic / Balance / Token / NFT / Domain / Label)
├── SQL API (Alpha / Classic)
└── Tops API
```

Chain RPC is removed (service discontinued).

### Tab 4: Data Catalog (unchanged)

```
├── Overview
├── EVM (Ethereum, BSC, Polygon, Avalanche, Fantom, Tron)
├── EVM L2 (Arbitrum, Optimism, Base, Blast, zkSync)
├── Non-EVM (Bitcoin, Merlin, Sui, Ton)
├── Other Networks
├── Token Price
└── Labels
```

### Tab 5: Chainbase Network (de-emphasized, narrative content)

```
├── Introduction
│   ├── What Is Chainbase
│   ├── Tokenomics
│   ├── Litepaper
│   └── FAQs
├── Network
│   ├── Overview / Developers / Operators / Validators / Delegators
├── Core Concepts
│   ├── Dual-Chain / Dual-Staking / AVS Design
│   └── Architecture (Execution / Consensus / DA / Co-Processor)
├── Crypto World Model (Theia)
│   ├── World Model / TheiaChat / Developers / Resources
├── Run a Node
│   ├── Introduction / Operator / Validator / Configuration / Testnet
└── Contributing
    ├── Roadmap / Governance / CIPs / Legal
```

### Cross-Linking Strategy

- Getting Started scenario pages → link to Developer Resources full reference at bottom
- Getting Started scenario pages → link to relevant API Reference endpoints
- Developer Resources pages → link to API Reference specific endpoints
- Explore All Products → each product links to Developer Resources detail page

## Content Migration Map

### Content that moves

| Current Location | New Location |
|-----------------|--------------|
| primaryTab "Learn and build" → Introduction | Chainbase Network → Introduction |
| primaryTab → Core Concepts (except Manuscript) | Chainbase Network → Core Concepts |
| primaryTab → Contributing | Chainbase Network → Contributing |
| primaryTab → Developers (Testnet/Open APIs) | Chainbase Network → Network |
| Tab "Run a node" | Chainbase Network → Run a Node |
| Tab "Crypto World Model" | Chainbase Network → Crypto World Model |
| Tab "Chainbase AI" | Developer Resources → Chainbase AI |
| Tab "Data Platform" | Developer Resources → Data Platform |
| Core Concepts → Manuscript | Developer Resources → Manuscript |

### Content that stays

| Content | Location |
|---------|----------|
| API Reference | API Reference tab (remove Chain RPC) |
| Data Catalog | Data Catalog tab (unchanged) |

### New content to create

| Page | Description |
|------|-------------|
| Welcome (homepage) | Tagline + 4 scenario cards + Explore All Products link |
| Explore All Products | Product index page grouped by capability |
| Query Blockchain Data | Scenario guide: CLI → Web3 API → SQL API → Tops API |
| Build AI Agents | Scenario guide: MCP → x402 → Web3 Data Skill |
| Stream & Process Data | Scenario guide: Manuscript → Data Sync |
| Explore Data in Cloud | Scenario guide: Data Cloud |

## What This Design Does NOT Change

- Individual page content (MDX files) — only their location in navigation changes
- API Reference endpoint documentation
- Data Catalog structure and content
- Mintlify framework — no platform migration
