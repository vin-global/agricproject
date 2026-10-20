# ENHANCEMENT OF AGRICULTURAL PRODUCT TRACEABILITY USING BLOCKCHAIN

A decentralized, tamper-proof farm-to-consumer agricultural provenance and supply-chain traceability platform. Built with **Solidity**, **Hardhat**, **OpenZeppelin**, **IPFS**, **Ethers.js**, **MetaMask**, and **React**.

---

## 🌾 Project Overview

In traditional agricultural supply chains, information is siloed in opaque centralized databases. Consumers face food fraud (counterfeits and falsely labeled organic goods), while supply chain actors suffer from undocumented cold-chain temperature violations that spoil perishable produce. 

**AgriTrace** solves these challenges by combining:
1. **Ethereum Smart Contracts (`AgriTrace.sol`)**: Enforcing role-based access control and state transitions across the supply chain.
2. **Decentralized Off-Chain Storage (IPFS)**: Pinning laboratory phytosanitary certificates, soil test documents, and sensor logs with immutable Content Identifiers (CIDs).
3. **Cold-Chain IoT Telemetry**: Logging ambient temperature (°C) and humidity (%) at transit checkpoints to detect thermal excursions.
4. **Physical-to-Digital QR Bridge**: Generating packaging QR codes that allow any consumer to scan and verify origin, milestones, and safety seals with zero login required.

---

## 👥 Stakeholder Role-Based Access Control

The smart contract implements OpenZeppelin's `AccessControl` to cryptographically enforce operational boundaries:

| Role Name | AccessControl Constant | Permitted Actions |
| :--- | :--- | :--- |
| **Producer** | `PRODUCER_ROLE` | Register harvested crop batches, log GPS coordinates, seed variety, and initial moisture. |
| **Processor** | `PROCESSOR_ROLE` | Record sorting, grading, milling, de-husking, and food-grade packaging. |
| **Logistics Provider** | `LOGISTICS_ROLE` | Record cold storage hub handovers, fleet transport, and IoT temperature/humidity readings. |
| **Sales Enterprise / Retailer** | `RETAILER_ROLE` | Record supermarket inventory receipt, retail shelf stocking, and mark items sold. |
| **Government Regulator** | `REGULATOR_ROLE` | Audit compliance, attach phytosanitary inspection certificates, or issue emergency recalls. |
| **Public Consumer** | *Public / View-Only* | Scan packaging QR codes, search batch provenance, and inspect safety certificates. |
| **System Admin** | `DEFAULT_ADMIN_ROLE` | Grant/revoke stakeholder roles, system pause/unpause, and emergency audit oversight. |

---

## 🛠️ Technology Stack

- **Smart Contract Language**: Solidity `^0.8.20`
- **Smart Contract Framework**: Hardhat `2.22.x` + `@nomicfoundation/hardhat-toolbox`
- **Security & Standards**: OpenZeppelin Contracts (`AccessControl`, `Pausable`, `ReentrancyGuard`)
- **Decentralized Storage**: InterPlanetary File System (IPFS) CID v1 content addressing
- **Blockchain Client**: Ethers.js `v6`
- **Web3 Wallet**: MetaMask integration with automatic chain detection + Local EVM Simulation Engine
- **Frontend Architecture**: React 19 + Vite (Vanilla CSS design system, no Tailwind dependencies)
- **Visual & Utility Libraries**: `lucide-react`, `qrcode.react`, `canvas-confetti`

---

## 🚀 Quick Start & Setup Instructions

### 1. Prerequisites
- **Node.js** (v18+ or v20+ recommended)
- **npm** (v9+ or v10+)

### 2. Install Dependencies
```bash
npm install
```

### 3. Compile Smart Contracts
Compile `AgriTrace.sol` with the Solidity 0.8.20 compiler:
```bash
npx hardhat compile --config hardhat.config.cjs
```

### 4. Run Automated Smart Contract Unit Tests
Execute the comprehensive Hardhat test suite (9 passing tests verifying role access, batch minting, cold chain telemetry, regulator certification, and emergency recall reverts):
```bash
npx hardhat test --config hardhat.config.cjs test/AgriTrace.test.cjs
```

### 5. Deploy Smart Contract Locally
Deploy the contract and auto-export the contract address and compiled ABI to `src/contracts/contractData.json`:
```bash
npx hardhat run scripts/deploy.cjs --config hardhat.config.cjs
```

### 6. Run Frontend Application
Launch the local development server:
```bash
npm run dev
```
Open **`http://127.0.0.1:5173/`** in your browser.

---

## 🖥️ Application Features & Walkthrough

1. **Professional Landing Page**:
   - Hero section with live metric cards (verified batches, cryptographic trust index).
   - Instant Batch Search bar with one-click test chips (e.g. *Organic Criollo Cocoa*, *Hass Avocado*, *Golden Maize*).
   - "How Blockchain Enhances Traceability" interactive visual pipeline.
   - Live on-chain transaction ticker.

2. **Supply Chain Hub (Dashboard)**:
   - Dynamic persona switcher (test actions as Producer, Processor, Logistics, Retailer, Regulator, or Admin).
   - Filterable & searchable batch table with real-time status badges.
   - Batch registration modal with automatic IPFS metadata pinning.
   - Checkpoint update modal with cold-chain sensor telemetry inputs (Temperature °C & Humidity %).

3. **Product Provenance Journey**:
   - Step-by-step interactive timeline showing checkpoint titles, actor names, wallet addresses, and timestamps.
   - Authenticity Seal verified against the EVM smart contract.
   - IoT Cold-Chain Stability report (analyzing temperature deviations and thermal breaches).
   - IPFS Off-Chain JSON inspector showing decoded certificates.

4. **Public Consumer Verification Portal**:
   - Zero login required.
   - Search by Batch ID or scan QR code.
   - Displays farm origin, organic certification, and the complete provenance road.

5. **QR Code Generator & Scanner**:
   - High-resolution SVG/PNG packaging QR codes with custom branding and download capability.
   - Interactive optical scanner simulation with quick batch selection.

6. **Blockchain Ledger Explorer**:
   - Live transaction receipts displaying hashes (`0x...`), block heights, gas consumption, and event signatures.
   - Built-in Smart Contract ABI inspector.

---

## 🧪 Smart Contract Verification Test Summary

```
  AgriTrace - Agricultural Product Traceability Smart Contract
    Deployment & Role Initialization
      ✔ Should assign DEFAULT_ADMIN_ROLE and initial roles to deployer/admin
      ✔ Should deny unauthorized accounts without designated roles
    Product Batch Registration (Producer Role)
      ✔ Should allow an authorized Producer to register an agricultural product batch
      ✔ Should REVERT if an unauthorized user attempts to register a batch
      ✔ Should prevent duplicate batch ID registration
    End-to-End Supply Chain Traceability
      ✔ Should record Processing stage by an authorized Processor
      ✔ Should record Logistics stage with cold-chain sensor telemetry
      ✔ Should allow Government Regulator to audit and certify the batch
      ✔ Should allow Regulator to trigger emergency product recall

  9 passing (3s)
```

---

## 📜 Academic Project Notice
This project was implemented as a Capstone Final-Year Project titled **"ENHANCEMENT OF AGRICULTURAL PRODUCT TRACEABILITY USING BLOCKCHAIN"**. It demonstrates practical decentralization, food safety assurance, and transparency in contemporary agribusiness.
