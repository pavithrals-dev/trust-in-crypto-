

Trust  is a composable Reputation-as-a-Service protocol built for ETHOnline 2025.  
It verifies completed freelance work, manages multi-rail escrow payouts, and generates on-chain reputation proofs — composable across the Web3 ecosystem.
Trust  integrates PayPal USD (PYUSD) and KIRAPAY as dual payment rails while anchoring every proof of payment and reputation update transparently on-chain via Blockscout.

---

## ⚙️ Architecture Overview

Core Contracts  
- Escrow.sol — Manages escrow creation, fund locking, and milestone-based releases.  
- PYUSDHandler.sol — Handles PayPal USD (PYUSD) stablecoin transfers on-chain.  
- KiraPayAdapter.sol — Off-chain KIRAPAY settlement adapter that anchors proof of payment on-chain.  
- Reputation.sol — Generates verifiable reputation scores and emits reputation proofs for freelancers and clients.  
- IPaymentRail.sol — Interface for modular payment rails (PYUSD, KIRAPAY, etc).

Frontend Stack  
- Next.js + TypeScript + Tailwind (deployed on Vercel)  
- Wagmi + Ethers.js for contract calls  
- Filecoin/IPFS for metadata storage  
- Blockscout SDK for on-chain verification UI  

---

## 🧩 Partner Integrations

PayPal USD (PYUSD):  
Used as the default on-chain stablecoin for escrow and payout settlements.  

KIRAPAY:  
Integrated via backend adapter — allows off-chain settlement with verifiable on-chain proof events.  

Blockscout:  
Used for transparent contract and event verification, ensuring auditability of each reputation update and escrow transaction.  

---

## 🚀 Quick Start (Local Setup)

```# 1. Clone the repository```
git clone https://github.com/hilmikt/raas.git  
cd raas  

```# 2. Install dependencies```
pnpm install  

```# 3. Compile and test contracts```
cd contracts  
npx hardhat compile  
npx hardhat test  

```# 4. Deploy contracts (Sepolia recommended)```
npx hardhat run scripts/deploy.js --network sepolia  

```# 5. Update frontend env```
cd ../frontend  
cp .env.example .env.local  
(Add your deployed contract addresses, RPC URL, and private key)  

```# 6. Run frontend locally```
pnpm dev  

---

## 🌍 Vercel Deployment

The frontend is pre-configured for Vercel.  
Ensure .vercelignore excludes all contract folders to avoid build errors.

Deploy:  
vercel --prod  

Check deployment logs at vercel.com/dashboard for region and caching details.  

---

## 🪙 Smart Contract Verification

Each deployment emits the following on Blockscout:  
- EscrowCreated(address client, address freelancer, uint256 amount)  
- MilestoneReleased(uint256 escrowId, uint256 amount)  
- ReputationUpdated(address user, uint256 score)  
- PaymentProofAnchored(bytes32 proofHash, string railType)

To verify:  
1. Visit your Blockscout instance (example: sepolia.blockscout.com)  
2. Paste your deployed contract address  
3. Confirm verified source + emitted events  

---

## 🧠 Reputation Logic

Reputation is computed by weighting:  
- Escrow completion rate  
- Dispute ratio  
- Peer rating  
- On-chain payment proofs  

Each freelancer’s address can be queried on-chain:  
```getReputation(address user) returns (uint256 score)```

---

## 🧭 Project Structure

/contracts  
  /escrow/Escrow.sol  
  /interfaces/IPaymentRail.sol  
  /rails/PYUSDHandler.sol  
  /rails/KiraPayAdapter.sol  
  /reputation/Reputation.sol  

/frontend  
  /components  
  /pages  
  /hooks  
  /lib  

---

