# NullState Solana x402 Settlement Scheme

> **Status:** Experimental — Live on Solana mainnet
> **Provider:** NullState Gateway (https://github.com/NullStateGGH/nullstate)
> **Network:** Solana
> **Asset:** USDC

## Overview

NullState provides an open-source x402 settlement gateway for AI agents on Solana. Agents can settle payments via x402 by posting a signed Solana transaction to the NullState gateway for verification.

## Settlement Endpoint

```
POST https://localhost:8080/api/settlement/verify
Content-Type: application/json
X-KYA-Token: <agent_auth_token>
```

### Request Body

```json
{
  "hash": "5K...tx_signature",
  "asset": "USDC",
  "network": "Solana",
  "amount": 4.99
}
```

### Response

```json
{
  "status": "verified",
  "amount": 4.99,
  "asset": "USDC",
  "network": "Solana",
  "timestamp": "2026-05-29T02:33:08Z"
}
```

## A2A Agent Card

NullState publishes an Agent Card at `/.well-known/agent-card.json` with 4 skills:

| Skill | Description |
|-------|-------------|
| x402-settlement | Verify on-chain USDC settlements |
| ap2-mandates | Generate and verify AP2 Intent/Cart/Payment mandates |
| credit-pooling | Prepaid USDC credit pools for agent billing |
| gcp-ecosystem | Credit-gated GCP workload orchestration |

## Agent Discovery

Agents discover NullState via:
- **A2A Agent Discovery Protocol**: Agent Card at `/.well-known/agent-card.json`
- **x402 Provider Registry**: Listed as a community x402 settlement provider

## Pricing

| Tier | Price | Requests/Month |
|------|-------|----------------|
| Free | $0    | 5              |
| Scout | $50  | 500            |
| Pro  | $200  | 5,000          |
| Enterprise | $500 | Unlimited |

## Integration Example (Python)

```python
import requests

resp = requests.post(
    "https://localhost:8080/api/settlement/verify",
    json={"hash": "tx_sig", "asset": "USDC", "network": "Solana", "amount": 4.99},
    headers={"Content-Type": "application/json"}
)
print(resp.json())
```

## Repository

- **Gateway**: https://github.com/NullStateGGH/nullstate
- **CLI**: https://github.com/NullStateGGH/nullstate-cli
- **Agent Card**: https://github.com/NullStateGGH/nullstate-cli/.well-known/agent-card.json
