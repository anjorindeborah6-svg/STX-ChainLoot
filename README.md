

# STX-ChainLoot - Gamin Gaming Platform Smart Contract

A Clarity smart contract for managing in-game asset creation, ownership, trading, and player progression on the Stacks blockchain.

## 🚀 Overview

The **Gamin Gaming Platform Smart Contract** enables game developers and platforms to mint, manage, and trade in-game digital assets securely and transparently. It supports batch operations for minting and transferring, enforces access control and asset validation, and features an integrated marketplace for buying and selling assets.

---

## 🔐 Features

### ✅ Asset Management

* Mint individual or batch in-game assets
* Track asset ownership and metadata
* Transfer assets between players
* Enforce transferability rules
* Self-transfer prevention

### 🛒 Marketplace

* List assets for sale
* Purchase listed assets
* Delist assets from the marketplace
* Atomic STX payment and ownership transfer

### 🎮 Player Stats

* Track player experience and level
* Input validation for player progression

### 🔍 Read-Only Views

* Fetch asset details
* Fetch marketplace listings
* Fetch player stats
* Total number of assets minted

---

## ⚙️ Contract Architecture

### Constants

| Name                                    | Description                                      |
| --------------------------------------- | ------------------------------------------------ |
| `contract-owner`                        | Admin who can mint assets                        |
| `err-owner-only`, `err-not-found`, etc. | Common error codes for input and auth validation |
| `max-level`, `max-experience`           | Capped player stats                              |
| `max-metadata-length`, `max-batch-size` | Prevents bloated inputs and gas inefficiencies   |

### Data Maps

| Map                    | Purpose                            |
| ---------------------- | ---------------------------------- |
| `assets`               | Stores asset details by ID         |
| `asset-prices`         | (Deprecated / Placeholder)         |
| `marketplace-listings` | Stores current asset sale listings |
| `player-stats`         | Tracks player experience and level |

### Variables

* `asset-counter`: Incremental counter for asset IDs

---

## 🧾 Function Reference

### 🧱 Public Functions

#### 🔨 Minting

* `mint-asset(metadata-uri, transferable)`: Mint a single asset
* `batch-mint-assets(metadata-uris, transferable-list)`: Mint multiple assets (up to 10)

#### 🔄 Transferring

* `transfer-asset(asset-id, recipient)`: Transfer a single asset
* `batch-transfer-assets(asset-ids, recipients)`: Batch transfer

#### 🏷 Marketplace

* `list-asset-for-sale(asset-id, price)`: List an asset for sale
* `purchase-asset(asset-id)`: Buy a listed asset
* `delist-asset(asset-id)`: Remove asset from marketplace

#### 📊 Player Stats

* `update-player-stats(experience, level)`: Update stats with limits

---

### 📖 Read-Only Functions

* `get-asset-details(asset-id)`
* `get-marketplace-listing(asset-id)`
* `get-player-stats(player)`
* `get-total-assets()`

---

## 🧪 Example Usage

### Minting an Asset

```clojure
(contract-call? .gamin mint-asset "ipfs://some-asset-uri" true)
```

### Listing for Sale

```clojure
(contract-call? .gamin list-asset-for-sale u1 u500000)
```

### Buying an Asset

```clojure
(contract-call? .gamin purchase-asset u1)
```

---

## 🛡 Security Notes

* Only the contract owner can mint assets.
* Transferability is enforced strictly.
* All user inputs are validated for safety.
* Asset listings use `block-height` to track listing times (e.g., for future expiration logic).

---

## 🧱 Deployment

To deploy:

1. Compile the Clarity contract using the Stacks CLI or IDE like Clarinet.
2. Ensure you initialize `contract-owner` correctly.
3. Run tests using Clarinet or deploy to a Stacks testnet.

---
