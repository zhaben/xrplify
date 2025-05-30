# 🧞‍♂️ XRP Genie — XRPL Wallet CLI & SDK (Next.js)

🧞‍♂️ **XRP Genie** is a CLI tool and SDK for rapidly scaffolding XRPL wallet applications. Choose
  from three integration modes—devnet faucet, Xaman wallet, or Web3Auth social login—and get a
  production-ready Next.js app in seconds.

Generate complete XRPL wallet apps with `npx xrp-genie init`.

It supports three levels of complexity — from beginner-friendly devnet wallets for testing to advanced account abstraction for the most sophisticated production use cases with mainstream users.

---

## 🧠 Modes

| Mode | Description |
|------|-------------|
| 🟢 **Mode 1: XRPL Devnet** | Create and manage wallets using `xrpl.js` on the XRPL devnet. |
| 🔵 **Mode 2: Xaman Wallet** | Authenticate users with Xaman (XUMM) Wallet using QR login and transaction signing. |
| 🟣 **Mode 3: Account Abstraction** | Uses Web3Auth to securely manage private keys via social login and MPC. No private key is ever stored or exposed directly — keys are reconstructed securely on the client using threshold cryptography. |

---

## 🚀 Quick Start

### 0. Set Up Your Dev Environment Properly The First Time (Beginner Devs Only)
Install Git SSH
- Go to an empty terminal
- Type: ```bash ssh-keygen```
- Set your password
- Type: ```bash cat /Users/yourusername/.ssh/id_ed25519.pub```
- Copy your ssh key
- Go to your Github user account account settings --> Click "SSH and CPG Keys" --> Click "New SSH Key" --> Paste your SSH Key

Install Oh My ZSH ```bash sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"```

Install pnpm ```bash npm i pnpm```

### 1. Clone the Repo

```bash
git clone git@github.com:yourusername/xrp-genie.git xrp-genie
cd xrp-genie
```

### 2. Install Dependencies

```bash
pnpm install
# or
npm install
```

### 3. Initialize Your Project (OR START WITH SDK)
Choose your mode
```bash
# Generates a fully-typed TypeScript Next.js app

npx xrp-genie init my-wallet-app
```

### 4. Configure Environment
Create .env.local in the root directory

```bash
cp .env.local.example .env.local
```

Creat and save your API keys
```bash
# .env.local

# mode2
XUMM_API_KEY=your_xumm_api_key
XUMM_API_SECRET=your_xumm_api_secret

# mode3
WEB3AUTH_CLIENT_ID=your-web3auth-client-id
```

### 4. Configure Environment
```bash
./cli/bin/xrp-genie init my-test-app
```

## 🧪 Run Locally

```bash
npm run dev
```
Visit: http://localhost:3000

---
  ## 🔧 Features by Mode
  🟢 Mode 1: XRPL Devnet (Beginner)
  - Connect to the XRPL Devnet using xrpl.js
  - Generate non-custodial wallets locally
  - Fund wallets using XRPL faucet
  - View balance, transaction history
  - Send XRP to other accounts

  🔵 Mode 2: Xaman Wallet (Intermediate)
  - Login with XUMM (Xaman Wallet) via QR code
  - Fetch XRPL account info securely
  - Prepare and push-sign transactions through user approval
  - Works with both mainnet and devnet

  🟣 Mode 3: Account Abstraction (Advanced)
  - 🔐 Authenticate users via social login (Google, Apple, etc.) using Web3Auth
  - 🧠 Reconstruct private keys securely in-browser via MPC (multi-party computation)
  - 🪪 Generate and persist XRPL wallets with no user seed phrases
  - 🧾 Sign and submit transactions programmatically (smart wallet behavior)
  - 🧱 Ideal for delegated signing, gas sponsorship, or future multisig/ZK workflows

---

## 🔒 Security Best Practices
❌ Never:

Don’t hardcode private keys or API secrets in your codebase
(e.g. const PRIVATE_KEY = "rXXXXXXXXXXXXXXXXXX")

Don't commit .env.local to Git.

✅ Always:

Store secrets in .env.local only, never in source code.


📦 What to include in .gitignore to prevent accidentally exposing secrets:

```bash
# Environment variables
.env
.env.local
.env.*.local
```
This keeps all environment-specific and secret config out of your Git history — especially important for API keys, client IDs, and anything else that shouldn't be public.

✅ We are Secure:

  1. 🔒 API keys on server-side - No more NEXT_PUBLIC_ exposure
  2. 🛡️ API routes created - /api/xumm/signin, /api/xumm/payment, /api/xumm/status
  3. 🔐 Client-side hook updated - calls secure API routes instead of direct SDK
  4. ⚡ No API key in browser - XUMM operations happen server-side only

  How it works:

  1. Frontend: Calls /api/xumm/signin to create QR code
  2. Backend: Uses XUMM SDK with private API keys
  3. Frontend: Displays QR code, polls for status
  4. Backend: Checks XUMM payload status securely
  5. Frontend: Updates UI when user signs/pays

  API keys stay on the server, only QR codes and status updates go to the client.

  The Xaman template is production-ready and secure! 🎉
  
  ✅ Web3Auth Security:

  Server-side approach:

  - ✅ No NEXT_PUBLIC_ environment variables
  - ✅ Client ID stored in .env.local (server-side only)
  - ✅ API route for initialization - /api/web3auth/init
  - ✅ Server-side account info - /api/xrpl/account-info
  - ✅ Consistent with Xaman approach

  How it works:

  1. Frontend calls /api/web3auth/init to get client ID and network config
  2. Web3Auth initializes with server-provided configuration
  3. Account info fetched via server-side API (same as Xaman)
  4. All sensitive data stays on the server

  Environment variables:

  - WEB3AUTH_CLIENT_ID - Server-side only
  - XRPL_NETWORK - Configured by CLI based on user selection


## 🛠️ Built With
- **Next.js 15** - React framework with App Router [https://nextjs.org/docs/app]
- **TypeScript** - Type-safe development [https://www.typescriptlang.org/]
- **Tailwind CSS** - Utility-first styling [https://tailwindcss.com/]
- **XRPL.js** - Official XRP Ledger library [https://xrpl.org/]
- **XUMM SDK** - [https://xumm.readme.io/]
- **Web3Auth** - [https://web3auth.io/docs/]
- **pnpm** - [https://pnpm.io/]
- **Oh My ZSH** - [https://ohmyz.sh/]

## 🧞 Contribution & Roadmap
**xrp-genie** is designed to grow. 

Planned features: NFT minting, Payment Abstraction

PRs and feature requests are welcome!

🪙 License
MIT © 2025 xrp-genie Contributors
