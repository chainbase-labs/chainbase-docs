# Documentation Restructure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Restructure Chainbase documentation from product-centric to developer-integration-first with 5 tabs: Getting Started (primary), Developer Resources, API Reference, Data Catalog, Chainbase Network.

**Architecture:** Mintlify assigns pages to tabs via URL prefix matching. To achieve the desired 5-tab structure, we must reorganize files into directories matching tab URL prefixes: `getting-started/` (primary), `resources/` (Developer Resources), `api-reference/` (stays), `catalog/` (stays), `network/` (Chainbase Network). We create 6 new scenario-driven pages, move existing MDX files via `git mv`, rewrite `mint.json` navigation, and bulk-update internal links.

**Tech Stack:** Mintlify (MDX), mint.json configuration, git mv, grep/sed for link updates

---

### Task 1: Create Getting Started Pages

Create 6 new MDX files under a new `getting-started/` directory. These are the scenario-driven pages for the primary tab.

**Files:**
- Create: `getting-started/welcome.mdx`
- Create: `getting-started/explore-all-products.mdx`
- Create: `getting-started/query-blockchain-data.mdx`
- Create: `getting-started/build-ai-agents.mdx`
- Create: `getting-started/stream-and-process-data.mdx`
- Create: `getting-started/explore-data-in-cloud.mdx`

- [ ] **Step 1: Create getting-started directory**

```bash
mkdir -p getting-started
```

- [ ] **Step 2: Create welcome.mdx**

```mdx
---
title: "Chainbase Documentation"
sidebarTitle: "Welcome"
description: "Access blockchain data from 90+ chains. Build with APIs, AI agents, or data pipelines."
---

Chainbase provides the data infrastructure for Web3 developers. Whether you're querying on-chain data via APIs, building AI agents with blockchain context, or streaming data into your own infrastructure — start here.

<CardGroup cols={2}>
  <Card title="Query Blockchain Data" icon="magnifying-glass" href="/getting-started/query-blockchain-data">
    Use CLI, Web3 API, SQL API, or Tops API to access token, wallet, NFT, and social data across 90+ chains.
  </Card>
  <Card title="Build AI Agents" icon="robot" href="/getting-started/build-ai-agents">
    Connect AI agents to real-time Web3 data via MCP, x402 micropayments, or Claude Code skills.
  </Card>
  <Card title="Stream & Process Data" icon="arrow-right-arrow-left" href="/getting-started/stream-and-process-data">
    Build custom data pipelines with Manuscript or sync chain data to your own infrastructure.
  </Card>
  <Card title="Explore Data in Cloud" icon="cloud" href="/getting-started/explore-data-in-cloud">
    Run SQL queries against terabytes of indexed on-chain data in Chainbase Data Cloud.
  </Card>
</CardGroup>

---

Looking for a specific product? See [all Chainbase products](/getting-started/explore-all-products).
```

- [ ] **Step 3: Create explore-all-products.mdx**

```mdx
---
title: "All Products"
sidebarTitle: "Explore All Products"
description: "Browse all Chainbase products and tools"
---

## AI Integration

Build AI agents and LLM applications with real-time Web3 data.

<CardGroup cols={2}>
  <Card title="Web3 Data MCP" icon="plug" href="/resources/ai/mcp">
    Connect on-chain data to any MCP-compatible AI client.
  </Card>
  <Card title="Tops Data MCP" icon="chart-line" href="/resources/ai/mcp-tops">
    Connect crypto social intelligence to AI clients. Free, no API key.
  </Card>
  <Card title="x402 Payment Protocol" icon="credit-card" href="/resources/ai/x402">
    AI Agent pay-per-call API access via HTTP 402 and stablecoins.
  </Card>
  <Card title="Web3 Data Skill" icon="robot" href="/resources/ai/web3-data-skill">
    Claude Code skill for natural language blockchain queries.
  </Card>
</CardGroup>

## Data Access

Query blockchain data programmatically across 90+ chains.

<CardGroup cols={2}>
  <Card title="Web3 API" icon="code" href="/resources/platform/features/api/web3-api">
    REST API for token, NFT, balance, domain, and transaction data.
  </Card>
  <Card title="SQL API" icon="database" href="/resources/platform/features/api/sql-api/overview">
    Run custom SQL queries against indexed on-chain datasets.
  </Card>
  <Card title="Tops API" icon="chart-line" href="/api-reference/tops-api/tool/list-trending-topics">
    Crypto social intelligence — trending narratives, mentions, and signals.
  </Card>
  <Card title="CLI" icon="terminal" href="/resources/ai/cli">
    Command-line tool for Web3 data and Tops queries. JSON output for scripting.
  </Card>
</CardGroup>

## Data Processing

Build data pipelines and stream chain data to your infrastructure.

<CardGroup cols={3}>
  <Card title="Manuscript" icon="scroll" href="/resources/manuscript/overview">
    Blockchain data streaming framework for custom data pipelines.
  </Card>
  <Card title="Data Cloud" icon="cloud" href="/resources/platform/features/datacloud/overview">
    Online data warehouse for SQL queries on terabytes of chain data.
  </Card>
  <Card title="Data Sync" icon="arrows-rotate" href="/resources/platform/features/sync/overview">
    Stream real-time chain data to your own databases and storage.
  </Card>
</CardGroup>

## Data Discovery

<CardGroup cols={2}>
  <Card title="Data Catalog" icon="book" href="/catalog/overview">
    Browse data schemas for 50+ blockchain networks.
  </Card>
</CardGroup>
```

- [ ] **Step 4: Create query-blockchain-data.mdx**

```mdx
---
title: "Query Blockchain Data"
description: "Access token, wallet, NFT, and social data across 90+ chains"
---

Chainbase provides multiple ways to query on-chain data. Choose the approach that fits your use case.

## Quick Start: CLI

The fastest way to try Chainbase. Install the CLI and run a query in under a minute:

```bash
npm install -g chainbase-cli
chainbase config set api-key YOUR_API_KEY
```

```bash
# Get ETH price
chainbase token price 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2

# Check wallet balances
chainbase balance tokens 0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045

# Trending crypto narratives (free, no API key)
chainbase tops trending
```

<Tip>
Get your API key at [console.chainbase.com](https://console.chainbase.com/). For demo purposes, use the key "demo".
</Tip>

Full CLI reference: [CLI Documentation](/resources/ai/cli)

## Web3 API

REST API for structured queries — token metadata, balances, NFT ownership, ENS domains, and more.

```bash
curl -X GET 'https://api.chainbase.com/v1/token/price?chain_id=1&contract_address=0xdAC17F958D2ee523a2206206994597C13D831ec7' \
  -H 'X-API-KEY: YOUR_API_KEY'
```

Available API suites:
- **Basic API** — Block and transaction queries
- **Token API** — Price, holders, metadata, transfers
- **NFT API** — Metadata, ownership, rarity, transfers
- **Balance API** — Native and ERC-20 token balances
- **Domain API** — ENS resolution and reverse lookup
- **Label API** — Address classification (exchange, whale, contract)

Full reference: [Web3 API Documentation](/resources/platform/features/api/web3-api) | [API Reference](/api-reference/overview)

## SQL API

Run custom SQL queries against Chainbase's indexed on-chain data warehouse for complex analytics.

```sql
SELECT block_timestamp, _from, _to, _value
FROM ethereum.erc20_transfer
WHERE contract_address = '0xdAC17F958D2ee523a2206206994597C13D831ec7'
  AND block_number > 19000000
LIMIT 10
```

Full reference: [SQL API Documentation](/resources/platform/features/api/sql-api/overview) | [API Reference](/api-reference/sql-api/execute-queries)

## Tops API

Query crypto social intelligence — trending narratives, Twitter/X mentions, and sentiment signals. **Free, no API key required.**

```bash
# Via CLI
chainbase tops trending

# Via API
curl -X GET 'https://api.chainbase.com/tops/v1/trending'
```

Full reference: [Tops API Reference](/api-reference/tops-api/tool/list-trending-topics)

## Next Steps

- [Explore All Products](/getting-started/explore-all-products) — See all Chainbase tools and services
- [API Reference](/api-reference/overview) — Complete endpoint documentation
- [Data Catalog](/catalog/overview) — Browse available chain data schemas
- [Tutorials](/getting-started/tutorials/balance-api/get-native-token-balances) — Step-by-step guides
```

- [ ] **Step 5: Create build-ai-agents.mdx**

```mdx
---
title: "Build AI Agents"
description: "Connect AI agents to real-time Web3 data and crypto social intelligence"
---

Chainbase provides multiple integration paths for AI agents and LLM applications to access on-chain data and crypto social signals.

## Quick Start: MCP

The fastest way to connect an AI client to Chainbase data. MCP (Model Context Protocol) gives your AI agent direct access to token, wallet, NFT, and transaction data through natural language.

<Tabs>
  <Tab title="Claude Code">
  ```bash
  # Web3 data (requires API key)
  claude mcp add --transport http chainbase https://api.chainbase.com/v1/mcp --header "X-API-KEY: YOUR_API_KEY"

  # Tops social data (free)
  claude mcp add --transport http tops https://api.chainbase.com/tops/v1/mcp
  ```
  </Tab>
  <Tab title="Cursor">
  Add to `~/.cursor/mcp.json`:
  ```json
  {
    "mcpServers": {
      "chainbase": {
        "url": "https://api.chainbase.com/v1/mcp",
        "headers": { "X-API-KEY": "YOUR_API_KEY" }
      },
      "tops": {
        "url": "https://api.chainbase.com/tops/v1/mcp"
      }
    }
  }
  ```
  </Tab>
  <Tab title="Claude Desktop">
  Settings > Connectors > Add custom connector

  - Name: `Chainbase Web3 Data`
  - Endpoint: `https://api.chainbase.com/v1/mcp`

  For Tops (free): add another connector with endpoint `https://api.chainbase.com/tops/v1/mcp`
  </Tab>
</Tabs>

Once connected, ask your AI agent questions like:
- "What are the top 10 holders of USDT on Ethereum?"
- "What's trending in crypto right now?"
- "Show me the NFTs owned by vitalik.eth"

Full reference: [Web3 Data MCP](/resources/ai/mcp) | [Tops Data MCP](/resources/ai/mcp-tops)

## x402 Payment Protocol

Enable AI agents to autonomously pay for API calls using stablecoins (USDC) via the HTTP 402 standard. No subscriptions — just $0.002 per call.

```python
from x402 import x402ClientSync
from x402.http.clients import x402_requests
from x402.mechanisms.evm import EthAccountSigner
from x402.mechanisms.evm.exact.register import register_exact_evm_client

client = x402ClientSync()
register_exact_evm_client(client, EthAccountSigner(account))
session = x402_requests(client)

response = session.get(
    "https://api.chainbase.com/v1/token/holders?chain_id=1&contract_address=0xdac17f958d2ee523a2206206994597c13d831ec7",
    headers={"x-api-key": "x402"}
)
```

Full reference: [x402 Integration](/resources/ai/x402)

## Web3 Data Skill for Claude Code

A Claude Code skill for on-chain data and crypto social intelligence via natural language:

```bash
npx skills add https://github.com/lxcong/web3-data-skill --skill web3-data
```

```
> /web3-data top 10 holders of USDT on Ethereum
> /web3-data what are the trending crypto narratives?
```

Full reference: [Web3 Data Skill](/resources/ai/web3-data-skill)

## Next Steps

- [Explore All Products](/getting-started/explore-all-products) — See all Chainbase tools
- [CLI Reference](/resources/ai/cli) — Command-line tool also designed for AI agent automation
- [API Reference](/api-reference/overview) — Full endpoint documentation
```

- [ ] **Step 6: Create stream-and-process-data.mdx**

```mdx
---
title: "Stream & Process Data"
description: "Build custom blockchain data pipelines with Manuscript and Data Sync"
---

Chainbase provides two approaches for building data pipelines: Manuscript for custom data processing, and Data Sync for streaming raw chain data to your infrastructure.

## Manuscript

Manuscript is a blockchain data streaming framework that lets you define data sources, transformations (SQL), and destinations in a single YAML file.

**Install and create your first pipeline:**

```bash
curl -fsSL https://github.com/chainbase-labs/manuscript-core/raw/main/install-gui.sh | bash
./manuscript
```

With Manuscript you can:
- Select data from any supported blockchain on the Chainbase DA layer
- Transform data using standard SQL and Flink SQL functions
- Export results to PostgreSQL, MySQL, S3, and more
- Deploy locally or to the Chainbase network

Full reference: [Manuscript Documentation](/resources/manuscript/overview) | [QuickStart](/resources/manuscript/QuickStart/prerequisites)

## Data Sync

Stream real-time blockchain data directly to your own databases and storage systems:

- Complete historical data synchronized with Data Cloud tables
- Real-time incremental updates after initial sync
- Support for PostgreSQL, MySQL, S3, and other targets

Set up via the [Chainbase Console](https://console.chainbase.com/):
1. Select your data source and target storage
2. Choose data type (raw, decoded, or abstracted)
3. Configure sync frequency
4. Start syncing and monitor progress

Full reference: [Data Sync Documentation](/resources/platform/features/sync/overview)

## Next Steps

- [Explore All Products](/getting-started/explore-all-products) — See all Chainbase tools
- [Data Catalog](/catalog/overview) — Browse available data schemas
- [Data Cloud](/resources/platform/features/datacloud/overview) — Query data online before building a pipeline
```

- [ ] **Step 7: Create explore-data-in-cloud.mdx**

```mdx
---
title: "Explore Data in Cloud"
description: "Run SQL queries against terabytes of indexed on-chain data"
---

Chainbase Data Cloud is an online data warehouse for Web3. Run SQL queries against terabytes of indexed blockchain data — no infrastructure setup required.

## Quick Start

1. Go to [console.chainbase.com/dataCloud](https://console.chainbase.com/dataCloud)
2. Enter a SQL query:

```sql
SELECT block_timestamp, block_number, _value, _from, _to
FROM ethereum.erc20_transfer
WHERE block_number = 17089970
```

3. Click **Execute** to see results instantly.

## Key Features

- **Unified datasets** — raw, decoded, and abstracted tables across 50+ chains
- **Parameterized queries** — use `{parameter}` placeholders for reusable templates
- **File Explorer** — save and organize your queries
- **Generate API** — turn any saved query into a REST endpoint with one click

## Generate an API from Your Query

After saving a query, click **Generate API** to create a callable endpoint:

```typescript
const response = await fetch(
  `https://api.chainbasehq.com/v1/query/${queryId}/execute`,
  { method: "POST", headers: { "API-KEY": apiKey } }
);
```

Full reference: [Data Cloud Documentation](/resources/platform/features/datacloud/overview) | [SQL API](/resources/platform/features/api/sql-api/overview)

## Next Steps

- [Data Catalog](/catalog/overview) — Browse available tables and schemas
- [SQL API Reference](/api-reference/sql-api/execute-queries) — Call Data Cloud queries programmatically
- [Data Sync](/resources/platform/features/sync/overview) — Stream data to your own infrastructure instead
```

- [ ] **Step 8: Commit all Getting Started pages**

```bash
git add getting-started/
git commit -m "feat: add Getting Started scenario-driven pages

Create 6 new pages: welcome, explore-all-products, query-blockchain-data,
build-ai-agents, stream-and-process-data, explore-data-in-cloud"
```

---

### Task 2: Move Files to network/ Directory

Move all narrative/network content into a `network/` directory so they appear under the "Chainbase Network" tab (url prefix: `network`).

**Files to move:**
- `introduction/` → `network/introduction/`
- `core-concepts/` (except `manuscript/`) → `network/core-concepts/`
- `developers/` → `network/developers/`
- `contributing/` → `network/contributing/`
- `node/` → `network/node/`
- `theia/` → `network/theia/`

- [ ] **Step 1: Create network directory and move files**

```bash
mkdir -p network

# Move entire directories
git mv introduction network/introduction
git mv developers network/developers
git mv contributing network/contributing
git mv node network/node
git mv theia network/theia

# Move core-concepts EXCEPT manuscript
mkdir -p network/core-concepts/architecture
git mv core-concepts/dual-chain.mdx network/core-concepts/
git mv core-concepts/dual-staking.mdx network/core-concepts/
git mv core-concepts/data-processing-based-on-avs.mdx network/core-concepts/
git mv core-concepts/avs-design.mdx network/core-concepts/
git mv core-concepts/glossary.mdx network/core-concepts/
git mv core-concepts/architecture/overview.mdx network/core-concepts/architecture/
git mv core-concepts/architecture/execution_layer.mdx network/core-concepts/architecture/
git mv core-concepts/architecture/consensus_layer.mdx network/core-concepts/architecture/
git mv core-concepts/architecture/data_accessibility_layer.mdx network/core-concepts/architecture/
git mv core-concepts/architecture/co_processor_layer.mdx network/core-concepts/architecture/
```

- [ ] **Step 2: Verify the moves**

```bash
# Check that manuscript is still in its original location
ls core-concepts/manuscript/overview.mdx

# Check that network/ has the expected structure
find network/ -name "*.mdx" | head -20
```

Expected: `core-concepts/manuscript/overview.mdx` still exists. `network/` contains all moved files.

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "refactor: move narrative content to network/ directory

Move introduction, core-concepts (except manuscript), developers,
contributing, node, and theia into network/ for Chainbase Network tab."
```

---

### Task 3: Move Files to resources/ Directory

Move developer tool/product reference content into a `resources/` directory so they appear under the "Developer Resources" tab (url prefix: `resources`).

**Files to move:**
- `chainbase-ai/` → `resources/ai/`
- `platform/` → `resources/platform/`
- `core-concepts/manuscript/` → `resources/manuscript/`

- [ ] **Step 1: Create resources directory and move files**

```bash
mkdir -p resources

# Move chainbase-ai to resources/ai
git mv chainbase-ai resources/ai

# Move platform to resources/platform
git mv platform resources/platform

# Move manuscript to resources/manuscript
git mv core-concepts/manuscript resources/manuscript

# Clean up empty core-concepts directory if empty
rmdir core-concepts 2>/dev/null || true
```

- [ ] **Step 2: Create Developer Resources overview page**

Create `resources/overview.mdx`:

```mdx
---
title: "Developer Resources"
sidebarTitle: "Overview"
description: "Complete reference documentation for all Chainbase products and tools"
---

Detailed documentation for every Chainbase product. For scenario-based guides, see [Getting Started](/getting-started/welcome).

## Chainbase AI

Tools and protocols for AI agent integration with Web3 data.

<CardGroup cols={2}>
  <Card title="MCP Servers" href="/resources/ai/mcp" />
  <Card title="Tops Data MCP" href="/resources/ai/mcp-tops" />
  <Card title="x402 Payment" href="/resources/ai/x402" />
  <Card title="Web3 Data Skill" href="/resources/ai/web3-data-skill" />
</CardGroup>

## Data Platform

APIs and infrastructure for accessing and processing chain data.

<CardGroup cols={2}>
  <Card title="Web3 API" href="/resources/platform/features/api/web3-api" />
  <Card title="SQL API" href="/resources/platform/features/api/sql-api/overview" />
  <Card title="Data Cloud" href="/resources/platform/features/datacloud/overview" />
  <Card title="Data Sync" href="/resources/platform/features/sync/overview" />
</CardGroup>

## Manuscript

<CardGroup cols={2}>
  <Card title="Manuscript Overview" href="/resources/manuscript/overview" />
  <Card title="QuickStart" href="/resources/manuscript/QuickStart/prerequisites" />
</CardGroup>

## CLI

<CardGroup cols={1}>
  <Card title="CLI Reference" href="/resources/ai/cli" />
</CardGroup>
```

- [ ] **Step 3: Verify the moves**

```bash
# Check resources structure
find resources/ -name "*.mdx" | wc -l
find resources/ -type d | sort
```

- [ ] **Step 4: Commit**

```bash
git add -A
git commit -m "refactor: move developer content to resources/ directory

Move chainbase-ai to resources/ai, platform to resources/platform,
manuscript to resources/manuscript for Developer Resources tab."
```

---

### Task 4: Move Tutorials to getting-started/

Move tutorial/use-case content from `resources/platform/usecases/` to `getting-started/tutorials/` so they appear under the Getting Started tab.

**Files to move:**
- `resources/platform/usecases/` → `getting-started/tutorials/`

- [ ] **Step 1: Move tutorial files**

```bash
git mv resources/platform/usecases getting-started/tutorials
```

- [ ] **Step 2: Verify**

```bash
find getting-started/tutorials/ -name "*.mdx" | sort
```

Expected: All tutorial MDX files under `getting-started/tutorials/`.

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "refactor: move tutorials to getting-started/tutorials/"
```

---

### Task 5: Rewrite mint.json Navigation

Replace the entire `tabs`, `primaryTab`, and `navigation` sections of `mint.json` with the new 5-tab structure.

**Files:**
- Modify: `mint.json`

- [ ] **Step 1: Rewrite mint.json**

Replace the entire content of `mint.json` with:

```json
{
  "$schema": "https://mintlify.com/schema.json",
  "name": "Chainbase Docs",
  "logo": {
    "dark": "/logo/dark.svg",
    "light": "/logo/light.svg"
  },
  "favicon": "/favicon.png",
  "colors": {
    "primary": "#000000",
    "light": "#A5CFFF",
    "dark": "#000000",
    "background": {
      "light": "#fdfdf7",
      "dark": "#000000"
    }
  },
  "topbarLinks": [
    {
      "name": "Support",
      "url": "mailto:support@chainbase.com"
    }
  ],
  "tabs": [
    {
      "name": "Developer Resources",
      "url": "resources"
    },
    {
      "name": "API Reference",
      "url": "api-reference"
    },
    {
      "name": "Data Catalog",
      "url": "catalog"
    },
    {
      "name": "Chainbase Network",
      "url": "network"
    }
  ],
  "primaryTab": {
    "name": "Getting Started"
  },
  "navigation": [
    {
      "group": "Getting Started",
      "pages": [
        "getting-started/welcome",
        "getting-started/explore-all-products"
      ]
    },
    {
      "group": "Query Blockchain Data",
      "pages": [
        "getting-started/query-blockchain-data"
      ]
    },
    {
      "group": "Build AI Agents",
      "pages": [
        "getting-started/build-ai-agents"
      ]
    },
    {
      "group": "Stream & Process Data",
      "pages": [
        "getting-started/stream-and-process-data"
      ]
    },
    {
      "group": "Explore Data in Cloud",
      "pages": [
        "getting-started/explore-data-in-cloud"
      ]
    },
    {
      "group": "Tutorials & Use Cases",
      "pages": [
        {
          "group": "Balance API Tutorials",
          "pages": [
            "getting-started/tutorials/balance-api/get-native-token-balances",
            "getting-started/tutorials/balance-api/get-nfts-owned-by-address"
          ]
        },
        {
          "group": "NFT API Tutorials",
          "pages": [
            "getting-started/tutorials/nft-api/get-all-transfers-of-a-collection",
            "getting-started/tutorials/nft-api/get-nft-metadata",
            "getting-started/tutorials/nft-api/get-nft-owners-by-collection",
            "getting-started/tutorials/nft-api/get-nft-owner-by-token"
          ]
        },
        {
          "group": "Token API Tutorials",
          "pages": [
            "getting-started/tutorials/token-api/get-erc20-tokens-by-address",
            "getting-started/tutorials/token-api/get-erc20-transfers-by-contract",
            "getting-started/tutorials/token-api/get-token-metadata",
            "getting-started/tutorials/token-api/get-holders-of-a-token",
            "getting-started/tutorials/token-api/get-top-token-holders",
            "getting-started/tutorials/token-api/get-token-price",
            "getting-started/tutorials/token-api/get-token-price-history"
          ]
        },
        {
          "group": "Domain API Tutorials",
          "pages": [
            "getting-started/tutorials/domain-api/resolve-domain",
            "getting-started/tutorials/domain-api/reverse-resolve-domain",
            "getting-started/tutorials/domain-api/get-domain-names-by-address"
          ]
        }
      ]
    },
    {
      "group": "Developer Resources",
      "pages": [
        "resources/overview"
      ]
    },
    {
      "group": "Chainbase AI",
      "pages": [
        "resources/ai/overview",
        "resources/ai/mcp",
        "resources/ai/mcp-tops",
        "resources/ai/x402",
        "resources/ai/web3-data-skill"
      ]
    },
    {
      "group": "Data Platform",
      "pages": [
        "resources/platform/overview",
        "resources/platform/supported-networks/supported-networks",
        {
          "group": "Datasets",
          "pages": [
            "resources/platform/datasets/overview",
            "resources/platform/datasets/inscription-and-rune",
            "resources/platform/datasets/data-catalog"
          ]
        },
        {
          "group": "Data Cloud",
          "pages": [
            "resources/platform/features/datacloud/overview",
            "resources/platform/features/datacloud/write-efficient-queries"
          ]
        },
        {
          "group": "Data Sync",
          "pages": [
            "resources/platform/features/sync/overview"
          ]
        },
        {
          "group": "APIs",
          "pages": [
            "resources/platform/features/api/web3-api",
            {
              "group": "SQL API",
              "pages": [
                "resources/platform/features/api/sql-api/overview",
                "resources/platform/features/api/sql-api/datacloud-task-api",
                "resources/platform/features/api/sql-api/datacloud-custom-api",
                "resources/platform/features/api/sql-api/datacloud-api-classic"
              ]
            }
          ]
        },
        "resources/platform/faqs/faq",
        "resources/platform/pricing/pricing",
        "resources/platform/support"
      ]
    },
    {
      "group": "Manuscript",
      "pages": [
        "resources/manuscript/overview",
        {
          "group": "QuickStart",
          "pages": [
            "resources/manuscript/QuickStart/prerequisites",
            "resources/manuscript/QuickStart/create_manuscript",
            "resources/manuscript/QuickStart/run_manuscript",
            "resources/manuscript/QuickStart/advanced_options"
          ]
        },
        "resources/manuscript/zone"
      ]
    },
    {
      "group": "CLI",
      "pages": [
        "resources/ai/cli"
      ]
    },
    {
      "group": "API Reference",
      "pages": [
        "api-reference/overview",
        "api-reference/status-code",
        "api-reference/jtw"
      ]
    },
    {
      "group": "Web3 API",
      "pages": [
        {
          "group": "Basic API",
          "pages": [
            "api-reference/web3-api/basic/block/get-latest-block-number",
            "api-reference/web3-api/basic/block/get-block-by-number",
            "api-reference/web3-api/basic/transaction/get-transaction",
            "api-reference/web3-api/basic/transaction/get-transactions-by-account",
            "api-reference/web3-api/basic/contract/contract-call"
          ]
        },
        {
          "group": "Balance API",
          "pages": [
            "api-reference/web3-api/balance/token-balances/get-erc20-token-balances",
            "api-reference/web3-api/balance/nft-balances/get-nfts-owned-by-address",
            "api-reference/web3-api/balance/token-balances/get-native-token-balances"
          ]
        },
        {
          "group": "Token API",
          "pages": [
            "api-reference/web3-api/token/token-metadata/get-token-metadata",
            "api-reference/web3-api/token/token-holders/get-top-token-holders",
            "api-reference/web3-api/token/token-holders/get-token-holders",
            "api-reference/web3-api/token/market-data/get-token-price",
            "api-reference/web3-api/token/market-data/get-token-price-history",
            "api-reference/web3-api/token/token-transfers/get-token-transfers-by-contract"
          ]
        },
        {
          "group": "NFT API",
          "pages": [
            "api-reference/web3-api/nft/nft-metadata/get-nft-metadata",
            "api-reference/web3-api/nft/nft-ownership/get-nft-owners-by-collection",
            "api-reference/web3-api/nft/nft-ownership/get-nft-owner-by-token",
            "api-reference/web3-api/nft/nft-metadata/get-nft-rarity",
            "api-reference/web3-api/nft/nft-ownership/get-nft-owner-history-by-token",
            "api-reference/web3-api/nft/nft-transfers/get-nft-transfers-by-collection",
            "api-reference/web3-api/nft/nft-collections/get-nft-collection-items",
            "api-reference/web3-api/nft/nft-collections/get-nft-collection-metadata"
          ]
        },
        {
          "group": "Domain API",
          "pages": [
            "api-reference/web3-api/domain/ens-domain-endpoints/get-ens-domains",
            "api-reference/web3-api/domain/ens-domain-endpoints/reverse-resolve-ens-domain",
            "api-reference/web3-api/domain/ens-domain-endpoints/resolve-ens-domain"
          ]
        },
        {
          "group": "Label API",
          "pages": [
            "api-reference/web3-api/basic/labels/get-address-labels"
          ]
        }
      ]
    },
    {
      "group": "SQL API",
      "pages": [
        {
          "group": "Alpha",
          "pages": [
            "api-reference/sql-api/execute-queries",
            "api-reference/sql-api/get-query-status",
            "api-reference/sql-api/get-query-results"
          ]
        },
        {
          "group": "Classic(Deprecated)",
          "pages": [
            "api-reference/sql-api/data-cloud-sql-query"
          ]
        }
      ]
    },
    {
      "group": "Tops API",
      "pages": [
        "api-reference/tops-api/tool/list-trending-topics",
        "api-reference/tops-api/tool/get-topic-detail",
        "api-reference/tops-api/tool/get-posts-for-a-topic",
        "api-reference/tops-api/tool/search-narrative-candidate-topics-by-keyword",
        "api-reference/tops-api/tool/search-social-mentions-by-keyword"
      ]
    },
    {
      "group": "Data Catalog",
      "pages": [
        "catalog/overview"
      ]
    },
    {
      "group": "EVM",
      "icon": "ethereum",
      "pages": [
        {
          "group": "Ethereum",
          "icon": "ethereum",
          "pages": [
            "catalog/Ethereum/Overview",
            "catalog/Ethereum/Abstracted",
            "catalog/Ethereum/Raw"
          ]
        },
        {
          "group": "BSC",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/BSC/Overview",
            "catalog/BSC/Abstracted",
            "catalog/BSC/Raw"
          ]
        },
        {
          "group": "Polygon",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Polygon/Overview",
            "catalog/Polygon/Abstracted",
            "catalog/Polygon/Raw"
          ]
        },
        {
          "group": "Avalanche",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Avalanche/Overview",
            "catalog/Avalanche/Abstracted",
            "catalog/Avalanche/Raw"
          ]
        },
        {
          "group": "Fantom",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Fantom/Overview",
            "catalog/Fantom/Raw"
          ]
        },
        {
          "group": "Tron",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Tron/Overview",
            "catalog/Tron/Raw"
          ]
        }
      ]
    },
    {
      "group": "EVM L2",
      "pages": [
        {
          "group": "Arbitrum",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Arbitrum/Overview",
            "catalog/Arbitrum/Abstracted",
            "catalog/Arbitrum/Raw"
          ]
        },
        {
          "group": "Optimism",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Optimism/Overview",
            "catalog/Optimism/Abstracted",
            "catalog/Optimism/Raw"
          ]
        },
        {
          "group": "Base",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Base/Overview",
            "catalog/Base/Abstracted",
            "catalog/Base/Raw"
          ]
        },
        {
          "group": "Blast",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Blast/Overview",
            "catalog/Blast/Raw"
          ]
        },
        {
          "group": "zkSync",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/zkSync/Overview",
            "catalog/zkSync/Abstracted",
            "catalog/zkSync/Raw"
          ]
        }
      ]
    },
    {
      "group": "Non-EVM",
      "pages": [
        {
          "group": "Bitcoin",
          "icon": "bitcoin",
          "iconType": "solid",
          "pages": [
            "catalog/Bitcoin/Abstracted"
          ]
        },
        {
          "group": "Merlin",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Merlin/Overview",
            "catalog/Merlin/Raw"
          ]
        },
        {
          "group": "Sui",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Sui/Overview",
            "catalog/Sui/Raw"
          ]
        },
        {
          "group": "Ton",
          "icon": "database",
          "iconType": "solid",
          "pages": [
            "catalog/Ton/Overview",
            "catalog/Ton/Raw"
          ]
        }
      ]
    },
    {
      "group": "Other-Network",
      "pages": [
        "catalog/OtherEvm/Beam",
        "catalog/OtherEvm/Berachain_Artio",
        "catalog/OtherEvm/Bitlayer_Mainnet",
        "catalog/OtherEvm/Immutable_zkEVM",
        "catalog/OtherEvm/Mantle",
        "catalog/OtherEvm/Mint_Mainnet",
        "catalog/OtherEvm/Moonbeam",
        "catalog/OtherEvm/Scroll",
        "catalog/OtherEvm/Taiko_Hekla_L2",
        "catalog/OtherEvm/opBNB_Mainnet",
        {
          "group": "Others",
          "pages": [
            "catalog/OtherEvm/APEX_Testnet",
            "catalog/OtherEvm/AgentLayer_Testnet",
            "catalog/OtherEvm/Ancient8",
            "catalog/OtherEvm/Atleta_Olympia",
            "catalog/OtherEvm/Automata_Testnet",
            "catalog/OtherEvm/B2_Testnet",
            "catalog/OtherEvm/Bitlayer_Mainnet",
            "catalog/OtherEvm/B2_Hub_Mainnet",
            "catalog/OtherEvm/BEVM_Mainnet",
            "catalog/OtherEvm/BEVM_Testnet",
            "catalog/OtherEvm/BNB_Smart_Chain_Testnet",
            "catalog/OtherEvm/Bahamut",
            "catalog/OtherEvm/Beam",
            "catalog/OtherEvm/Berachain_Artio",
            "catalog/OtherEvm/Berachain_bArtio",
            "catalog/OtherEvm/Bifrost_Mainnet",
            "catalog/OtherEvm/Bifrost_Testnet",
            "catalog/OtherEvm/Bitlayer_Testnet",
            "catalog/OtherEvm/BlackFort_Exchange_Network",
            "catalog/OtherEvm/BlackFort_Exchange_Network_Testnet",
            "catalog/OtherEvm/Blast_Sepolia_Testnet",
            "catalog/OtherEvm/Crab_Network",
            "catalog/OtherEvm/Chiliz_Chain_Mainnet",
            "catalog/OtherEvm/Celo_Alfajores_Testnet",
            "catalog/OtherEvm/Creditcoin_Testnet",
            "catalog/OtherEvm/Crypto_Emergency",
            "catalog/OtherEvm/Cyber_Mainnet",
            "catalog/OtherEvm/Cyber_Testnet",
            "catalog/OtherEvm/Darwinia_Network",
            "catalog/OtherEvm/DOS_Chain",
            "catalog/OtherEvm/Darwinia_Koi_Testnet",
            "catalog/OtherEvm/Dodao",
            "catalog/OtherEvm/Ethereum_Classic",
            "catalog/OtherEvm/Forma",
            "catalog/OtherEvm/Fhenix_Helium",
            "catalog/OtherEvm/Form_Testnet",
            "catalog/OtherEvm/Forma_Sketchpad",
            "catalog/OtherEvm/Fuse_Mainnet",
            "catalog/OtherEvm/Fuse_Sparknet",
            "catalog/OtherEvm/GEEK_Verse_Mainnet",
            "catalog/OtherEvm/GEEK_Verse_Testnet",
            "catalog/OtherEvm/GUNZ_Testnet",
            "catalog/OtherEvm/Gnosis",
            "catalog/OtherEvm/Gnosis_Chiado_Testnet",
            "catalog/OtherEvm/Gobbl_Testnet",
            "catalog/OtherEvm/Hybrid_Testnet",
            "catalog/OtherEvm/Hemi_Sepolia",
            "catalog/OtherEvm/Immutable_zkEVM",
            "catalog/OtherEvm/Immutable_zkEVM_Testnet",
            "catalog/OtherEvm/Kakarot_Sepolia",
            "catalog/OtherEvm/Karak_Sepolia",
            "catalog/OtherEvm/Kingdom_Chain",
            "catalog/OtherEvm/Klaytn_Testnet_Baobab",
            "catalog/OtherEvm/Kroma",
            "catalog/OtherEvm/Kroma_Sepolia",
            "catalog/OtherEvm/Kyoto",
            "catalog/OtherEvm/Kyoto_Testnet",
            "catalog/OtherEvm/LUKSO_Mainnet",
            "catalog/OtherEvm/LUKSO_Testnet",
            "catalog/OtherEvm/Lambda_Chain_Testnet",
            "catalog/OtherEvm/LayerEdge_testnet",
            "catalog/OtherEvm/Linea_Sepolia",
            "catalog/OtherEvm/Lambda_Chain_Mainnet",
            "catalog/OtherEvm/MAXI_Chain_Testnet",
            "catalog/OtherEvm/Mantle",
            "catalog/OtherEvm/Memo_Smart_Chain_Mainnet",
            "catalog/OtherEvm/Meter_Mainnet",
            "catalog/OtherEvm/Meter_Testnet",
            "catalog/OtherEvm/Mint_Mainnet",
            "catalog/OtherEvm/Mint_Sepolia_Testnet",
            "catalog/OtherEvm/Mint_Testnet",
            "catalog/OtherEvm/Mode_Testnet",
            "catalog/OtherEvm/Moonbeam",
            "catalog/OtherEvm/Numbers_Mainnet",
            "catalog/OtherEvm/Opal_testnet_by_Unique",
            "catalog/OtherEvm/Open_Campus_Codex",
            "catalog/OtherEvm/Orderly_Sepolia_Testnet",
            "catalog/OtherEvm/Ozone_Chain_Mainnet",
            "catalog/OtherEvm/Ozone_Chain_Testnet",
            "catalog/OtherEvm/PLAYA3ULL_GAMES",
            "catalog/OtherEvm/Plume_Testnet",
            "catalog/OtherEvm/Pools_Mainnet",
            "catalog/OtherEvm/PulseChain",
            "catalog/OtherEvm/PulseChain_Testnet_v4",
            "catalog/OtherEvm/RSS3_VSL_Sepolia_Testnet",
            "catalog/OtherEvm/Reya_Network",
            "catalog/OtherEvm/Rollux_Testnet",
            "catalog/OtherEvm/Saakuru_Mainnet",
            "catalog/OtherEvm/Scroll",
            "catalog/OtherEvm/Scroll_Sepolia_Testnet",
            "catalog/OtherEvm/Shyft_Mainnet",
            "catalog/OtherEvm/Step_Network",
            "catalog/OtherEvm/Swan_Proxima_Testnet",
            "catalog/OtherEvm/Swan_Saturn_Testnet",
            "catalog/OtherEvm/Syndicate_Frame_Chain",
            "catalog/OtherEvm/TAPROOT_Mainnet",
            "catalog/OtherEvm/Taiko_Hekla_L2",
            "catalog/OtherEvm/Tanssi_Demo",
            "catalog/OtherEvm/UPB_CRESCDI_Testnet",
            "catalog/OtherEvm/Unique",
            "catalog/OtherEvm/Vana_Satori_Testnet",
            "catalog/OtherEvm/Vanar_Mainnet",
            "catalog/OtherEvm/VeChain",
            "catalog/OtherEvm/VeChain_Testnet",
            "catalog/OtherEvm/Vitruveo_Mainnet",
            "catalog/OtherEvm/Vitruveo_Testnet",
            "catalog/OtherEvm/WeaveVM_Testnet",
            "catalog/OtherEvm/XDC_Apothem_Network",
            "catalog/OtherEvm/XR_Sepolia",
            "catalog/OtherEvm/Xai_Mainnet",
            "catalog/OtherEvm/Xterio_Testnet",
            "catalog/OtherEvm/Zilliqa_EVM",
            "catalog/OtherEvm/Zilliqa_EVM_Devnet",
            "catalog/OtherEvm/Zilliqa_EVM_Testnet",
            "catalog/OtherEvm/Zircuit_Testnet",
            "catalog/OtherEvm/Zora",
            "catalog/OtherEvm/opBNB_Mainnet",
            "catalog/OtherEvm/opBNB_Testnet",
            "catalog/OtherEvm/re.al",
            "catalog/OtherEvm/zkCandy_Sepolia_Testnet"
          ]
        }
      ]
    },
    {
      "group": "Token",
      "icon": "database",
      "pages": [
        {
          "group": "token_price",
          "icon": "database",
          "pages": [
            "catalog/Price/Overview",
            "catalog/Price/Abstracted"
          ]
        }
      ]
    },
    {
      "group": "Labels",
      "icon": "database",
      "pages": [
        {
          "group": "addresses",
          "icon": "database",
          "pages": [
            "catalog/Labels/Overview",
            "catalog/Labels/Abstracted"
          ]
        }
      ]
    },
    {
      "group": "Introduction",
      "pages": [
        "network/introduction/about",
        "network/introduction/tokenomics",
        "network/introduction/litepaper",
        "network/introduction/faqs"
      ]
    },
    {
      "group": "Chainbase Network",
      "pages": [
        "network/introduction/networks/overview",
        "network/introduction/networks/developers",
        "network/introduction/networks/operators",
        "network/introduction/networks/validators",
        "network/introduction/networks/delegators"
      ]
    },
    {
      "group": "Core Concepts",
      "pages": [
        "network/core-concepts/dual-chain",
        "network/core-concepts/dual-staking",
        "network/core-concepts/data-processing-based-on-avs",
        "network/core-concepts/avs-design",
        "network/core-concepts/glossary",
        {
          "group": "Architecture",
          "pages": [
            "network/core-concepts/architecture/overview",
            "network/core-concepts/architecture/execution_layer",
            "network/core-concepts/architecture/consensus_layer",
            "network/core-concepts/architecture/data_accessibility_layer",
            "network/core-concepts/architecture/co_processor_layer"
          ]
        }
      ]
    },
    {
      "group": "Crypto World Model",
      "pages": [
        "network/theia/World_model/welcome",
        "network/theia/World_model/theia",
        "network/theia/World_model/features"
      ]
    },
    {
      "group": "TheiaChat",
      "pages": [
        "network/theia/TheiaChat/overview",
        "network/theia/TheiaChat/task-models",
        "network/theia/TheiaChat/create-task-models"
      ]
    },
    {
      "group": "Theia Developers",
      "pages": [
        "network/theia/Developers/Open-APIs",
        {
          "group": "Glossary",
          "pages": [
            "network/theia/Developers/Glossary/D2ORA",
            "network/theia/Developers/Glossary/G2D"
          ]
        }
      ]
    },
    {
      "group": "Theia Resources",
      "pages": [
        "network/theia/Resources/Roadmap",
        "network/theia/Resources/Whitepaper",
        "network/theia/Resources/FAQs"
      ]
    },
    {
      "group": "Run a Node",
      "pages": [
        "network/node/introduction",
        "network/node/operator",
        "network/node/validator",
        "network/node/configuration",
        "network/node/testnet"
      ]
    },
    {
      "group": "Contributing",
      "pages": [
        "network/contributing/overview",
        "network/contributing/roadmap",
        "network/contributing/governance",
        "network/contributing/cips",
        "network/contributing/legal-disclaimer",
        "network/contributing/micar_whitepaper"
      ]
    }
  ],
  "footerSocials": {
    "x": "https://twitter.com/chainbaseHQ",
    "discord": "https://chainbase.com/discord",
    "github": "https://github.com/chainbase-labs"
  }
}
```

- [ ] **Step 2: Validate JSON syntax**

```bash
python3 -c "import json; json.load(open('mint.json')); print('Valid JSON')"
```

Expected: `Valid JSON`

- [ ] **Step 3: Commit**

```bash
git add mint.json
git commit -m "feat: rewrite mint.json with new 5-tab navigation structure

Tabs: Getting Started (primary), Developer Resources, API Reference,
Data Catalog, Chainbase Network. Remove Chain RPC from API Reference."
```

---

### Task 6: Update Internal Links in Moved Files

All internal links in MDX files that reference moved paths must be updated. Use bulk find-and-replace.

**Link mapping (old path → new path):**

| Old | New |
|-----|-----|
| `/chainbase-ai/` | `/resources/ai/` |
| `/platform/` | `/resources/platform/` |
| `/core-concepts/manuscript/` | `/resources/manuscript/` |
| `/core-concepts/` | `/network/core-concepts/` |
| `/introduction/` | `/network/introduction/` |
| `/contributing/` | `/network/contributing/` |
| `/developers/` | `/network/developers/` |
| `/node/` | `/network/node/` |
| `/theia/` | `/network/theia/` |
| `/platform/usecases/` | `/getting-started/tutorials/` |

**Important:** Process replacements in specificity order (most specific first) to avoid double-replacing. For example, `/core-concepts/manuscript/` must be replaced before `/core-concepts/`.

- [ ] **Step 1: Run link replacements across all MDX files**

```bash
# Most specific first to avoid double-replacement

# platform/usecases → getting-started/tutorials (before platform)
find . -name "*.mdx" -exec sed -i 's|(/platform/usecases/|(/getting-started/tutorials/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/platform/usecases/|href="/getting-started/tutorials/|g' {} +

# core-concepts/manuscript → resources/manuscript (before core-concepts)
find . -name "*.mdx" -exec sed -i 's|(/core-concepts/manuscript/|(/resources/manuscript/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/core-concepts/manuscript/|href="/resources/manuscript/|g' {} +

# chainbase-ai → resources/ai
find . -name "*.mdx" -exec sed -i 's|(/chainbase-ai/|(/resources/ai/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/chainbase-ai/|href="/resources/ai/|g' {} +

# platform → resources/platform
find . -name "*.mdx" -exec sed -i 's|(/platform/|(/resources/platform/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/platform/|href="/resources/platform/|g' {} +

# core-concepts → network/core-concepts
find . -name "*.mdx" -exec sed -i 's|(/core-concepts/|(/network/core-concepts/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/core-concepts/|href="/network/core-concepts/|g' {} +

# introduction → network/introduction
find . -name "*.mdx" -exec sed -i 's|(/introduction/|(/network/introduction/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/introduction/|href="/network/introduction/|g' {} +

# contributing → network/contributing
find . -name "*.mdx" -exec sed -i 's|(/contributing/|(/network/contributing/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/contributing/|href="/network/contributing/|g' {} +

# developers → network/developers
find . -name "*.mdx" -exec sed -i 's|(/developers/|(/network/developers/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/developers/|href="/network/developers/|g' {} +

# node → network/node
find . -name "*.mdx" -exec sed -i 's|(/node/|(/network/node/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/node/|href="/network/node/|g' {} +

# theia → network/theia
find . -name "*.mdx" -exec sed -i 's|(/theia/|(/network/theia/|g' {} +
find . -name "*.mdx" -exec sed -i 's|href="/theia/|href="/network/theia/|g' {} +
```

- [ ] **Step 2: Fix relative image paths in moved files**

All moved files go exactly one level deeper. Use a Python script to safely prepend one `../` to every relative image path. This avoids sed substring collision issues (e.g., `../../images/` containing `../images/`).

```bash
python3 -c "
import re, glob

# All directories that moved one level deeper
moved_dirs = [
    'network/introduction', 'network/core-concepts', 'network/theia',
    'network/node', 'network/contributing', 'network/developers',
    'resources/ai', 'resources/platform'
]
# Note: resources/manuscript/ was core-concepts/manuscript/ (depth 2 → depth 2), no change needed

count = 0
for d in moved_dirs:
    for f in glob.glob(f'{d}/**/*.mdx', recursive=True):
        with open(f) as fh:
            content = fh.read()
        # Match any relative path to images/: prepend one ../
        # Pattern: (one or more ../) followed by images/
        new_content = re.sub(r'(\.\./)+images/', lambda m: '../' + m.group(0), content)
        # Also handle bare images/ (no ../ prefix, same directory)
        new_content = re.sub(r'(?<![./])images/', '../images/', new_content)
        if new_content != content:
            with open(f, 'w') as fh:
                fh.write(new_content)
            count += 1
            print(f'  Fixed: {f}')

print(f'Updated {count} files')
"
```

- [ ] **Step 3: Verify no broken links remain**

```bash
# Check for any remaining old-path links
grep -r '"/chainbase-ai/' --include="*.mdx" . | grep -v node_modules || echo "No old chainbase-ai links"
grep -r '"/platform/' --include="*.mdx" . | grep -v node_modules | grep -v '/resources/platform/' || echo "No old platform links"
grep -r '"/core-concepts/' --include="*.mdx" . | grep -v node_modules || echo "No old core-concepts links"
grep -r '"/introduction/' --include="*.mdx" . | grep -v node_modules || echo "No old introduction links"
grep -r '"/node/' --include="*.mdx" . | grep -v node_modules || echo "No old node links"
grep -r '"/theia/' --include="*.mdx" . | grep -v node_modules || echo "No old theia links"
grep -r '"/contributing/' --include="*.mdx" . | grep -v node_modules || echo "No old contributing links"
grep -r '"/developers/' --include="*.mdx" . | grep -v node_modules || echo "No old developers links"
```

If any old links remain, fix them manually.

- [ ] **Step 4: Commit**

```bash
git add -A
git commit -m "fix: update all internal links to match new directory structure"
```

---

### Task 7: Remove Discontinued Chain RPC Content

Remove the Chain RPC (node-rpc) files from the API reference since the service has been discontinued. These files are already not referenced in the navigation.

**Files:**
- Delete: `api-reference/node-rpc/` (entire directory)

- [ ] **Step 1: Remove node-rpc directory**

```bash
git rm -r api-reference/node-rpc/
```

- [ ] **Step 2: Commit**

```bash
git commit -m "chore: remove discontinued Chain RPC documentation"
```

---

### Task 8: Final Verification

- [ ] **Step 1: Verify mint.json is valid JSON**

```bash
python3 -c "import json; json.load(open('mint.json')); print('Valid JSON')"
```

- [ ] **Step 2: Verify all pages referenced in mint.json exist**

```bash
python3 -c "
import json, os
with open('mint.json') as f:
    data = json.load(f)

def extract_pages(obj):
    pages = []
    if isinstance(obj, str):
        pages.append(obj)
    elif isinstance(obj, dict):
        for v in obj.values():
            pages.extend(extract_pages(v))
    elif isinstance(obj, list):
        for item in obj:
            pages.extend(extract_pages(item))
    return pages

all_pages = extract_pages(data.get('navigation', []))
missing = [p for p in all_pages if not os.path.exists(p + '.mdx')]
if missing:
    print(f'MISSING {len(missing)} pages:')
    for p in missing:
        print(f'  {p}')
else:
    print(f'All {len(all_pages)} pages exist')
"
```

Expected: `All N pages exist`

- [ ] **Step 3: Verify directory structure**

```bash
echo "=== Getting Started ==="
find getting-started/ -name "*.mdx" | sort

echo "=== Resources ==="
find resources/ -name "*.mdx" | wc -l

echo "=== Network ==="
find network/ -name "*.mdx" | wc -l

echo "=== API Reference ==="
find api-reference/ -name "*.mdx" | wc -l

echo "=== Catalog ==="
find catalog/ -name "*.mdx" | wc -l

echo "=== Old directories (should not exist) ==="
ls -d chainbase-ai platform introduction core-concepts node theia contributing developers 2>&1
```

Expected: Old directories should not exist (except potentially empty ones).

- [ ] **Step 4: Commit any remaining fixes**

```bash
git add -A
git status
# Only commit if there are changes
git diff --cached --quiet || git commit -m "fix: final cleanup after restructure verification"
```
