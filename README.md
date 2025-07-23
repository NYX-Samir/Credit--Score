# DeFi Wallet Scoring Project

## Objective

This notebook builds a full pipeline to evaluate wallet behavior in DeFi. It reads raw transaction data, generates wallet-level features like activity span, protocol usage, and financial signals, then applies a scoring logic to assign a numeric score to each wallet. These scores help segment users by engagement, risk, or strategy.

The repo includes:
- One Python notebook with all processing and scoring logic.
- `README.md` for quick overview.
- `analysis.md` with behavior insights based on scores.

## Input Format

Input is a JSON file (`user-wallet-transactions.json`) where each record is one transaction with fields like:

- `_id`: Unique transaction ID.
- `userWallet`: User's wallet address.
- `network`: Chain name (e.g., `"polygon"`).
- `protocol`: DeFi protocol (e.g., `"aave_v2"`, `"uniswap_v3"`).
- `txHash`: Transaction hash.
- `timestamp`: Unix time of transaction.
- `action`: Type of interaction (`"deposit"`, `"borrow"`, `"repay"`, `"swap"` etc.).
- `actionData`: Nested object with:
  - `amount`: Volume of asset.
  - `assetSymbol`: Token symbol (e.g., `"ETH"`).
  - `assetPriceUSD`: USD value at time of action.
  - Optional: `poolId`, `userId`.
- `createdAt`, `updatedAt`: Metadata timestamps.

Schema is general-purpose and works across protocols.

## Method: Rule-Based Scoring

This system uses a transparent rule-based model to assign scores to wallets based on observable DeFi activity. It emphasizes interpretability—each behavioral signal (e.g., deposit size, protocol diversity, repayment activity) maps directly to scoring logic. Unlike opaque machine learning models, this structure is traceable and modular, ideal for early-stage analytics or product segmentation.

## Architecture Flow

```mermaid
graph TD
    A[Raw JSON Transaction Data] --> B[Data Preprocessing]
    B --> C[Cleaned DataFrame]
    C --> D[Feature Engineering]
    D --> E[Wallet-Level Metrics]
    E --> F[Rule-Based Scoring]
    F --> G[Wallet Score Dictionary]
    G --> H[Export to JSON]
    G --> I[Visual Analysis + Reporting]
