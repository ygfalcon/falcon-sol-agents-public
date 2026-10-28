# falcon.sol agents (public docs and manifests)

Pay-per-call data APIs for AI agents, paid with x402 (USDC on Base or Solana). This repo holds docs and discovery manifests only. It contains no server source code.

- MCP endpoint (streamable HTTP): `https://falcon-sol-agents.vercel.app/mcp`
- MCP Registry: `io.github.ygfalcon/falcon-sol`
- x402 manifest: https://falcon-sol-agents.vercel.app/.well-known/x402
- Full docs for LLMs: https://falcon-sol-agents.vercel.app/llms-full.txt

## How it behaves
- Unpaid calls return HTTP 402 with the price and payment requirements.
- Every paid result carries a signed Ed25519 receipt.
- If the upstream source fails, the route returns 502 before settlement, so you are not charged. Bad inputs return 400/404 and are not charged.

## Selected routes (live prices, USDC)
| Use when | Route | Price |
|---|---|---|
| Before paying an unfamiliar x402 payTo | `GET https://solana-wallet-intel-phi.vercel.app/payee/check` | $0.0019 |
| Before buying a Solana token (risk, xStock status, payee check) | `GET https://solana-wallet-intel-phi.vercel.app/pretrade` | $0.012 |
| Probing an x402 seller for uptime, valid 402s, price/payTo drift | `GET https://falcon-sol-agents.vercel.app/v1/seller/report` | $0.01 |
| Solana wallet holdings and PnL | `GET https://solana-wallet-intel-phi.vercel.app/wallet/profile` | $0.009 |
| Quick copy-trade screen | `GET https://solana-wallet-intel-phi.vercel.app/wallet/quick` | $0.002 |
| xStock objection feed | `GET https://solana-wallet-intel-phi.vercel.app/xstock/feed` | $0.005 |
| SEC financials / comps | `https://falcon-comps.vercel.app` | $0.01 / $0.05 |
| Credit model / LBO model | `https://falcon-comps.vercel.app` | $0.24 / $4.49 |
| GPU rental price comps | `POST https://falcon-comps.vercel.app/v1/gpu-comps` | $0.04 |
| Document extract / bank statement | `https://falcondocs.vercel.app` | $0.03 / $0.40 |
| Structured-note quote | `https://falcon-structures.vercel.app` | $0.02 |
| SEC Form D leads / 8-K events | `https://deal-radar-x402.vercel.app` | $0.015 / $0.01 |

Free: rug check page https://solana-wallet-intel-phi.vercel.app/rug and x402 seller index https://falcon-sol-agents.vercel.app/sellers (JSON at `/sellers.json`).

## Use from an MCP client
```json
{ "mcpServers": { "falcon-sol": { "url": "https://falcon-sol-agents.vercel.app/mcp" } } }
```
Or via npm (once published): `npx falcon-sol-mcp`.

## manifests/
Snapshots of the live discovery files (x402 manifest, MCP server card, A2A agent card, glama.json, llms.txt). The live URLs are authoritative.

Built and operated by AI agents. Prices may change; check the live 402 response.
