# FlareTrader — Multi-Asset DeFi Platform on Flare Network

> Built at **EasyA Hackathon** · Flare Network (Coston2 Testnet) · Real-time FTSO price oracle integration

![Stack](https://img.shields.io/badge/Blockchain-Flare%20Network-E63946?style=flat-square)
![Stack](https://img.shields.io/badge/Web3-Ethers.js%20v5-purple?style=flat-square)
![Stack](https://img.shields.io/badge/Oracle-FTSO-orange?style=flat-square)
![Stack](https://img.shields.io/badge/Wallet-MetaMask-F6851B?style=flat-square&logo=metamask)

---

## Overview

FlareTrader is a decentralized trading interface built in 24 hours at the EasyA Hackathon. It enables simulated trading of **crypto, stocks, and precious metals** in a single unified interface — powered by Flare's **FTSO (Flare Time Series Oracle)** for real-time, decentralized price feeds.

The core challenge we tackled: most DeFi platforms only support crypto. FTSO uniquely supports cross-asset price data (equities + metals + crypto), so we built a UI to demonstrate that breadth.

---

## What It Does

- **Multi-asset trading** — 8 cryptocurrencies, 8 stocks (AAPL, NVDA, TSLA...), 4 precious metals (XAU, XAG, XPT, XPD)
- **Live FTSO price feeds** — decentralized oracle data, auto-refreshed every 30 seconds
- **Buy / Sell with P&L tracking** — portfolio view with average cost basis and performance
- **MetaMask wallet integration** — connects to Flare Coston2 testnet, auto-switches network
- **Transaction history** — tracks all simulated trades in-session

> **Note:** This runs on Coston2 testnet. No real funds involved — trades are simulated against mock on-chain state.

---

## Architecture

```
┌──────────────────────────────────────────────────┐
│              Browser (HTML/CSS/JS)               │
│   Asset selector → Trade UI → Portfolio view     │
└───────────────────┬──────────────────────────────┘
                    │ Ethers.js
        ┌───────────▼───────────┐
        │     MetaMask Wallet   │
        │   (Coston2 Testnet)   │
        └───────────┬───────────┘
                    │ RPC calls
        ┌───────────▼───────────┐
        │   Flare Network       │
        │   FTSO Price Oracle   │
        │   Smart Contracts     │
        └───────────────────────┘
```

**Key technical decisions:**
- **Client-side only** — no backend server; all state managed in-browser via Ethers.js
- **FTSO over Chainlink** — Flare's native oracle supports equities and metals natively, which Chainlink does not on this network
- **Coston2 testnet** — allows full on-chain interaction without real asset risk

---

## Quick Start

### Prerequisites
- [MetaMask](https://metamask.io/) browser extension
- Coston2 testnet tokens from the [Faucet](https://coston2-faucet.towolabs.com/) (min 10 C2FLR)

### Run Locally

```bash
git clone https://github.com/Drashti0913/EasyA_Hackathon.git
cd EasyA_Hackathon

# Option 1: Python
python -m http.server 8000

# Option 2: Node
npx serve .
```

Open `http://localhost:8000`, click **Connect MetaMask**, and approve the Coston2 network switch.

### Network Config (if needed)

| Field | Value |
|---|---|
| Network Name | Flare Testnet Coston2 |
| RPC URL | `https://coston2-api.flare.network/ext/C/rpc` |
| Chain ID | 114 (0x72) |
| Currency | C2FLR |
| Explorer | https://coston2-explorer.flare.network |

---

## Project Structure

```
├── server.js              # Local dev server
├── portfolio_server.js    # Portfolio state handler
├── contracts/             # Solidity smart contracts
├── scripts/               # Deployment scripts (Hardhat)
├── models/                # Data models
├── public/                # Frontend assets
├── hardhat.config.js      # Hardhat + Flare network config
└── .env.example           # Required env vars
```

---

## FTSO Feeds Used

| Category | Assets |
|---|---|
| Crypto | BTC/USD, ETH/USD, XRP/USD, ADA/USD, DOT/USD, SOL/USD, MATIC/USD, AVAX/USD |
| Stocks | AAPL, GOOGL, MSFT, AMZN, TSLA, META, NFLX, NVDA |
| Metals | XAU/USD, XAG/USD, XPT/USD, XPD/USD |

---

## Hackathon Context

Built at **EasyA Hackathon** focused on the Flare Network ecosystem. The goal was to demonstrate FTSO's unique cross-asset oracle capability — something no major DeFi platform had fully explored at the time. The 24-hour constraint meant prioritizing working FTSO integration and clean UX over production-grade smart contracts.

**What we'd improve with more time:**
- Real on-chain trade execution (currently simulated)
- Persistent portfolio state via contract storage
- Price chart history using FTSO historical feeds

---

## License

MIT
