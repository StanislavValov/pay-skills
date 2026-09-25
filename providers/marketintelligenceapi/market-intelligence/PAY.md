---
name: market-intelligence
title: "Market Intelligence API"
description: "On-chain trade-flow market intelligence for crypto and tokenized US stocks: buy/sell pressure, signals, opportunity scans with evidence and risk, perp positioning, smart money, token risk and rates."
use_case: "Use when trading crypto or tokenized US stocks: see what is being bought or sold now, scan for unusual buying, breakouts, crowded perps or smart-money flows, get a pre-trade verdict, screen a token, or read the rates backdrop."
category: finance
service_url: https://api.marketintelligenceapi.com
version: v1
openapi:
  path: openapi.json
---

Market Intelligence API turns executed swaps on public DEX pools (Base, Ethereum,
Arbitrum, Optimism, Polygon, Robinhood Chain and Solana) into trading signals for
crypto assets and 24/7 tokenized US stocks and ETFs. The aggressor side of every
swap is exact, and arbitrage, sandwich (MEV) and two-sided bot trades are excluded
from buy pressure.

Every paid route costs a fixed price per call in USDC ($0.001 to $0.05), paid with
x402 on Solana, Base, Polygon or Arbitrum. A call is charged only when it succeeds:
no data for the query (404) and invalid requests (400) are free.

## Where to start

- `GET /api/v1/intelligence/snapshot/{symbol}` ($0.001): price, change, buy pressure, signal and confidence of one asset.
- `GET /api/v1/intelligence/opportunities?objective=unusual_buying` ($0.03): ranked symbols for a goal (unusual_buying, unusual_selling, breakout, breakdown, crowded_positioning, smart_money_accumulation, smart_money_distribution) with supporting and conflicting evidence by independent source, risk factors and the signal's live hit rate. Also POST with a JSON body.
- `GET /api/v1/intelligence/pre-trade?symbol=ETHUSD&side=buy` ($0.005): FAVORABLE / CAUTION / UNFAVORABLE verdict with the checks behind it.
- `GET /api/v1/intelligence/positioning/{symbol}` ($0.01): perp open interest long/short and crowding (GMX v2, gTrade) for stocks, ETFs and commodities.
- `GET /api/v1/rates/curve` ($0.005): Treasury curve, slopes, inversion, SOFR, EFFR and euro STR.

## Identifiers

Symbols are plain tickers: crypto as `ETHUSD`, `BTCUSD`; tokenized stocks and ETFs as
`NVDA`, `TSLA`, `SPY`; perp-only markets as `XAUUSD`, `WTIUSD`. The free `/coverage`
route lists which sources cover each symbol. Windows are `1m`, `5m` or `15m`.

## Free

`/api/v1/preview` (15-minute delayed candles), `/track-record` (live hit rate of the
signals), `/coverage`, `/status`, `/llms.txt`, `/openapi.json`. MCP server at `/mcp`
(official MCP Registry: com.marketintelligenceapi.api/market-intelligence).

Informational market data, not investment advice.
