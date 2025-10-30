# StakeGuard

> Privacy‑preserving staking powered by Zama FHEVM

StakeGuard is a decentralized staking protocol where stake amounts, rewards accrual, and user signals remain confidential. Using Fully Homomorphic Encryption (FHE) with Zama’s FHEVM, the protocol computes rewards and penalties over encrypted balances while keeping results verifiable on‑chain.

---

## Why StakeGuard

- ❌ Public stake sizes leak strategy → ✅ Encrypted stake amounts and signals
- ❌ Opaque reward math → ✅ On‑chain, verifiable FHEVM computations
- ❌ Centralized control → ✅ Self‑custodial, non‑custodial staking

---

## Zama FHEVM for Private Staking

FHEVM lets smart contracts operate on ciphertexts. StakeGuard tracks balances and computes rewards without ever decrypting user data.

```
Staker Client
  └─ FHE Encrypt (amount, action)
         └─ Encrypted Tx → FHEVM Contracts
                              └─ Encrypted Accrual/Slashing
                                       └─ Encrypted Balance → Verifiable Payout
```

Key properties
- No plaintext stake balances on‑chain
- Encrypted reward accrual and slashing logic
- Auditable payouts and protocol state

---

## Getting Started

Prerequisites: Node.js 18+, MetaMask, Sepolia ETH

Setup
```bash
git clone https://github.com/torneylo/StakeGuard
cd StakeGuard
npm install
cp .env.example .env.local
```

Deploy
```bash
npm run deploy:sepolia
```

Run
```bash
npm run dev
```

---

## Staking Flow

1) Deposit: client encrypts stake amount and submits
2) Accrual: FHEVM contracts update encrypted balances/rewards
3) Claim: user requests payout; verifiable rewards are paid
4) Withdraw: user exits; privacy preserved throughout

Privacy model
- Encrypted: stake amounts, accrual signals, penalties
- Transparent: contract code, total supply proofs, payout events

---

## Architecture

| Layer            | Technology            | Role                                  |
|------------------|-----------------------|---------------------------------------|
| Encryption       | Zama FHE              | Client‑side encryption                 |
| Smart Contracts  | Solidity + FHEVM      | Encrypted accounting and rewards       |
| Blockchain       | Ethereum Sepolia      | Execution and persistence              |
| Frontend         | React + TypeScript    | Staking UI + local crypto              |
| Tooling          | Hardhat, Ethers       | Build/test/deploy                      |

Core contracts
- StakeVault: encrypted deposits/withdrawals
- RewardEngine: encrypted reward accrual and slashing
- Treasury: payout and accounting hooks

---

## Features

- 🔐 Encrypted balances and accrual
- 💸 Verifiable, privacy‑preserving rewards
- 🧾 Auditable payouts and protocol metrics
- 🧩 Policy modules (lockups, tiers, penalties)

---

## Security & Best Practices

- Independent audits (circuits and contracts) recommended
- EIP‑712 signing to prevent replay
- Rotate FHE keys per epoch; minimize metadata
- Monitor gas footprint of FHE computations

---

## Roadmap

- v1: Core encrypted staking, accrual, claims
- v1.1: Tiered rewards, lockups, fee rebates
- v1.2: Cross‑chain deployments, watchdog oracles

---

## Contributing

Contributions welcome: performance, audits, policy modules, UI/UX.

---

## Resources

- Zama: https://www.zama.ai
- FHEVM Docs: https://docs.zama.ai/fhevm
- Sepolia Explorer: https://sepolia.etherscan.io

---

## License

MIT — see LICENSE.

Built with Zama FHEVM — private balances, fair rewards, public trust.
