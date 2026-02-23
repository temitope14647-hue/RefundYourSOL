# RefundYourSOL — Recover Locked SOL from Empty Token Accounts

**The #1 SOL recovery tool on Solana.** Close unused token accounts, burn worthless tokens & NFTs, and get your trapped SOL back instantly. Trusted by 500,000+ users with 8,000+ SOL recovered.

[![Website](https://img.shields.io/badge/Website-refundyoursol.com-blue)](https://refundyoursol.com)
[![CoinMarketCap](https://img.shields.io/badge/CoinMarketCap-Listed-green)](https://coinmarketcap.com/currencies/refundyoursol/)
[![CoinGecko](https://img.shields.io/badge/CoinGecko-Verified-green)](https://www.coingecko.com/en/coins/refundyoursol)
[![Jupiter](https://img.shields.io/badge/Jupiter-Verified-green)](https://jup.ag/tokens/8gHPxqgHj6JQ2sQtMSghQYVN5qRP8wm5T6HNejuwpump)
[![Phantom](https://img.shields.io/badge/Phantom-dApp%20Listed-purple)](https://phantom.com/apps/refundyoursol)
[![Solscan](https://img.shields.io/badge/Solscan-Verified-blue)](https://solscan.io/account/8gHPxqgHj6JQ2sQtMSghQYVN5qRP8wm5T6HNejuwpump)

---

## The Problem

Every token purchase on Solana creates a **token account** that locks **0.00204 SOL** in rent. Even after selling all your tokens, that SOL stays trapped in empty accounts. If you've traded 500 tokens, that's over **1 SOL** sitting in accounts you'll never use again.

Most recovery tools only scan the newer Token-2022 program. **RefundYourSOL scans both the old 2022 SPL Token Program AND Token-2022** — finding significantly more locked SOL that competitors miss entirely.

## Key Features

- **Instant SOL Recovery** — Close empty token accounts and reclaim rent deposits in seconds
- **Safe Token & NFT Burning** — Burn worthless shitcoins and scam NFTs; recoverable if burned by mistake
- **Zero Risk** — We pay all gas fees. Empty wallet? No problem. You only gain SOL, never lose it
- **Dual Program Scanning** — Finds SOL locked in both old SPL Token and new Token-2022 program accounts
- **Multi-Wallet Support** — Phantom, Solflare, Backpack, OKX, Bybit, Coinbase, Brave, Bitget & more
- **Lowest Fees** — 15% base, down to 2.5% with fee matching. Hold $RYS for up to 50% off
- **Complete Wallet Refund** — Drain & consolidate multiple wallets (bot wallets, old wallets) into one
- **Referral Program** — Earn SOL for every user you refer. Instant, automatic payouts

## Live Stats

| Metric | Value |
|--------|-------|
| Users Served | 530,000+ |
| Accounts Closed | 4,400,000+ |
| SOL Recovered | 8,900+ SOL |
| $RYS Holders | 22,000+ |
| Supply Staked | 67%+ |

---

## API Reference

Integrate SOL recovery, token account closing, DEX trading, and token metadata into your applications, bots, AI agents, or scripts.

**Base URL:** `https://refundyoursol.com/api/`

**Full Documentation:** [refundyoursol.com/docs](https://refundyoursol.com/docs)

### Endpoints Overview

| Endpoint | Method | Description | Auth |
|----------|--------|-------------|------|
| `/api/checkTokenAccounts` | POST | Scan wallets for closable token accounts and estimate SOL recovery | None |
| `/api/closeAccounts` | POST | Get unsigned close transactions (client-side signing) | None |
| `/api/closeTokenAccounts` | POST | Close accounts with server-side signing | Private Key |
| `/api/trade` | POST | Build or execute DEX trades across Raydium, Orca, PumpSwap, Meteora | None (`returnTx`) |
| `/api/trade/detect/:mint` | GET | Detect which AMM/DEX a token trades on and its pool address | None |
| `/api/token-info` | GET | Token metadata + live price | None |
| `/api/get-token-metadata` | GET | Extended metadata + price for integrations | API Key |
| `/api/solana-price` | GET | Current SOL/USD price | API Key |

### Quick Start — Check Wallet for Recoverable SOL

```bash
curl -X POST https://refundyoursol.com/api/checkTokenAccounts \
  -H "Content-Type: application/json" \
  -d '{"walletAddresses": ["YOUR_WALLET_ADDRESS"]}'
```

### Quick Start — Get Unsigned Close Transactions

```bash
curl -X POST https://refundyoursol.com/api/closeAccounts \
  -H "Content-Type: application/json" \
  -d '{
    "walletAddresses": ["YOUR_WALLET_ADDRESS"],
    "refundWallet": "DESTINATION_WALLET"
  }'
```

The response contains base64-encoded unsigned transactions. Sign them locally with your wallet — **your private keys never leave your device**.

### Quick Start — Detect Token Pool

```bash
curl https://refundyoursol.com/api/trade/detect/TOKEN_MINT_ADDRESS
```

Returns the DEX (Raydium CPMM, Raydium CLMM, Orca, PumpSwap, Meteora, PumpFun), pool address, and liquidity information for any SPL token.

### Quick Start — Execute a Trade

```bash
curl -X POST https://refundyoursol.com/api/trade \
  -H "Content-Type: application/json" \
  -d '{
    "action": "buy",
    "mint": "TOKEN_MINT_ADDRESS",
    "amount": 0.1,
    "slippage": 10,
    "walletAddress": "YOUR_WALLET",
    "returnTx": true
  }'
```

Set `returnTx: true` to receive an unsigned transaction for client-side signing. Supports multi-hop swaps through intermediate tokens (USDC, USD1, USDT) for optimal routing.

### JavaScript Integration Example

```javascript
const response = await fetch('https://refundyoursol.com/api/checkTokenAccounts', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    walletAddresses: ['YourSolanaWalletAddress']
  })
});

const data = await response.json();
console.log(`Found ${data.totalEmptyAccounts} empty accounts`);
console.log(`Recoverable SOL: ${data.totalPotentialRecovery}`);
```

### Python Integration Example

```python
import requests

response = requests.post('https://refundyoursol.com/api/checkTokenAccounts', json={
    'walletAddresses': ['YourSolanaWalletAddress']
})

data = response.json()
print(f"Found {data['totalEmptyAccounts']} empty accounts")
print(f"Recoverable SOL: {data['totalPotentialRecovery']}")
```

### For AI Agents & Bots

The RefundYourSOL API is designed for programmatic use by trading bots, portfolio managers, AI agents, and automated workflows:

- **No authentication required** for core endpoints (`checkTokenAccounts`, `closeAccounts`, `trade` with `returnTx`)
- **Unsigned transaction responses** — safe for client-side signing without exposing private keys
- **Pool detection** — automatically find the best DEX and pool for any SPL token
- **Multi-hop routing** — optimal trade execution through intermediate stablecoins
- **Batch operations** — scan and close accounts across up to 20 wallets in a single request

---

## White-Label API

Build your own SOL recovery website using our infrastructure. No coding required.

**White-Label Portal:** [api.refundyoursol.com](https://api.refundyoursol.com)

| Plan | Price | Revenue Share | Branding |
|------|-------|---------------|----------|
| Free | $0 | Keep 75% of fees | "Powered by RYS" |
| Pro | 0.5 SOL (one-time) | Keep 75% of fees | Your own branding |

Features: plug-and-play widget, 20+ themes, real-time dashboard, domain restrictions, custom logos, and unlimited API requests.

```html
<!-- Embed the widget on your site -->
<script src="https://api.refundyoursol.com/sdk/widget.js"
  data-api-key="YOUR_API_KEY"
  data-theme="dark">
</script>
```

---

## $RYS Token

**Contract:** `8gHPxqgHj6JQ2sQtMSghQYVN5qRP8wm5T6HNejuwpump`

$RYS powers the RefundYourSOL ecosystem with revenue sharing, fee discounts, and community governance.

### Staking — 18%+ APY

Stake $RYS to earn daily rewards from 50% of platform revenue. Lock periods from 1 to 6 months with reward multipliers up to 100%.

| Lock Period | Reward Multiplier |
|-------------|-------------------|
| 1 Month | 65% |
| 3 Months | 75% |
| 6 Months | 100% |

### Holder Fee Discounts

| $RYS Held | Fee Discount | Effective Fee |
|-----------|-------------|---------------|
| 100K+ | 10% off | 13.5% |
| 500K+ | 20% off | 12.0% |
| 1M+ | 30% off | 10.5% |
| 5M+ | 50% off | 7.5% |

### Tokenomics

- **67%+** of supply is staked
- **3%+** permanently burned
- **9%** LP locked
- Only ~20% circulates, amplifying price impact on every buy

Auto-compound stakers convert daily SOL rewards into $RYS market buys, creating constant organic buy pressure.

---

## Supported DEXs

RefundYourSOL's trading API supports pool detection and execution across all major Solana AMMs:

- **Raydium** (CPMM & CLMM)
- **Orca**
- **PumpSwap**
- **PumpFun**
- **Meteora**
- **Jupiter** (aggregated routing)

---

## Security

- **No private key access** — website transactions are signed locally in your browser wallet
- **Unsigned transaction API** — `/api/closeAccounts` and `/api/trade` with `returnTx` return unsigned transactions; keys never leave your device
- **Verified everywhere** — Phantom dApp, Solscan labeled fee wallet, CoinMarketCap, CoinGecko, Jupiter verified
- **Safe Burns** — tokens sent to a recoverable wallet by default; contact support to restore accidental burns
- **On-chain transparency** — every transaction is publicly verifiable on Solscan

---

## Listings & Verifications

- [CoinMarketCap](https://coinmarketcap.com/currencies/refundyoursol/)
- [CoinGecko](https://www.coingecko.com/en/coins/refundyoursol)
- [Jupiter Verified Token](https://jup.ag/tokens/8gHPxqgHj6JQ2sQtMSghQYVN5qRP8wm5T6HNejuwpump)
- [Phantom dApp Store](https://phantom.com/apps/refundyoursol)
- [Solscan Verified](https://solscan.io/account/8gHPxqgHj6JQ2sQtMSghQYVN5qRP8wm5T6HNejuwpump)
- [Solana Seeker Mobile App Store](https://refundyoursol.com/project)

---

## Community

| Channel | Link |
|---------|------|
| Website | [refundyoursol.com](https://refundyoursol.com) |
| Twitter/X | [@RefundYourSOL](https://x.com/RefundYourSOL) |
| Telegram News | [t.me/refundyoursol](https://t.me/refundyoursol) |
| Telegram Chat | [t.me/refundyoursolcom](https://t.me/refundyoursolcom) |
| Discord | [discord.gg/refundyoursol](https://discord.gg/refundyoursol) |
| Documentation | [refundyoursol.com/docs](https://refundyoursol.com/docs) |
| API Portal | [api.refundyoursol.com](https://api.refundyoursol.com) |
| Staking | [refundyoursol.com/staking](https://refundyoursol.com/staking) |

---

## How It Works

```
1. Connect Wallet  →  Phantom, Solflare, Backpack, OKX, etc.
2. Auto-Scan       →  Detect all empty token accounts (SPL + Token-2022)
3. Sign & Claim    →  One transaction, SOL appears in your wallet instantly
```

We cover all gas fees. You approve every transaction. Zero risk.

---

## Use Cases

- **Solana Traders** — Recover SOL from hundreds of token accounts after trading
- **NFT Collectors** — Burn scam NFTs and recover locked rent
- **Trading Bots** — Programmatically clean up bot wallets via API
- **Market Makers** — Batch-close accounts across multiple wallets with the Smart Batch Optimizer
- **AI Agents** — Integrate wallet cleanup and trading into autonomous workflows
- **Portfolio Managers** — Consolidate funds from multiple wallets with Complete Wallet Refund
- **Project Builders** — White-label the entire platform under your own brand

---

## License

This repository contains documentation and public API references for RefundYourSOL. The platform source code is proprietary. See [Terms of Service](https://refundyoursol.com/terms) for usage terms.

---

<p align="center">
  <b>Built on Solana</b> · Shipping since January 2025 · 400+ days of continuous development
  <br><br>
  <a href="https://refundyoursol.com">refundyoursol.com</a>
</p>
