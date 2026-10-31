# falcon.sol agents (public docs and manifests)

Pay-per-call data APIs for AI agents, paid with x402 (USDC on Base or Solana). This repo holds docs and discovery manifests only. It contains no server source code.

- MCP endpoint (streamable HTTP): `https://falcon-sol-agents.falcon-sol.workers.dev/mcp`
- MCP Registry: `io.github.ygfalcon/falcon-sol`
- x402 manifest: https://falcon-sol-agents.falcon-sol.workers.dev/.well-known/x402
- Full docs for LLMs: https://falcon-sol-agents.falcon-sol.workers.dev/llms-full.txt

## How it behaves
- Unpaid calls return HTTP 402 with the price and payment requirements.
- Every paid result carries a signed Ed25519 receipt.
- If the upstream source fails, the route returns 502 before settlement, so you are not charged. Bad inputs return 400/404 and are not charged.

## Selected routes (live prices, USDC)
| Use when | Route | Price |
|---|---|---|
| Before paying an unfamiliar x402 payTo | `GET https://solana-wallet-intel.falcon-sol.workers.dev/payee/check` | $0.0019 |
| Before buying a Solana token (risk, xStock status, payee check) | `GET https://solana-wallet-intel.falcon-sol.workers.dev/pretrade` | $0.012 |
| Probing an x402 seller for uptime, valid 402s, price/payTo drift | `GET https://falcon-sol-agents.falcon-sol.workers.dev/v1/seller/report` | $0.01 |
| Solana wallet holdings and PnL | `GET https://solana-wallet-intel.falcon-sol.workers.dev/wallet/profile` | $0.009 |
| Quick copy-trade screen | `GET https://solana-wallet-intel.falcon-sol.workers.dev/wallet/quick` | $0.002 |
| xStock objection feed | `GET https://solana-wallet-intel.falcon-sol.workers.dev/xstock/feed` | $0.005 |
| SEC financials / comps | `https://falcon-comps.falcon-sol.workers.dev` | $0.01 / $0.05 |
| Credit model / LBO model | `https://falcon-comps.falcon-sol.workers.dev` | $0.24 / $4.49 |
| GPU rental price comps | `POST https://falcon-comps.falcon-sol.workers.dev/v1/gpu-comps` | $0.04 |
| Document extract / bank statement | `https://falcon-docs.falcon-sol.workers.dev` | $0.03 / $0.40 |
| Structured-note quote | `https://falcon-structures.falcon-sol.workers.dev` | $0.02 |
| SEC Form D leads / 8-K events | `https://deal-radar.falcon-sol.workers.dev` | $0.015 / $0.01 |

## Free endpoints
- Rug check page: https://solana-wallet-intel.falcon-sol.workers.dev/rug
- x402 seller index: https://falcon-sol-agents.falcon-sol.workers.dev/sellers (JSON at `/sellers.json`)

## Use from an MCP client
```json
{ "mcpServers": { "falcon-sol": { "url": "https://falcon-sol-agents.falcon-sol.workers.dev/mcp" } } }
```
The npm wrapper (`falcon-sol-mcp`) is not published yet; use the URL above.

## manifests/
Snapshots of the live discovery files (x402 manifest, MCP server card, A2A agent card, glama.json, llms.txt). The live URLs are authoritative.

## Notes
- Prices may change. The live 402 response is authoritative.
- Not investment advice. Outputs are data and model estimates; verify before relying on them.
- Built and operated by falcon.sol (GitHub [ygfalcon](https://github.com/ygfalcon)).
