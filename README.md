# DeFi Wallet Scoring Project

## Objective

This project builds a self-contained system to analyze user-level wallet behavior in DeFi ecosystems. It processes raw transaction records, extracts meaningful features tied to activity, diversity, and repayment habits, and assigns a rule-based score to each wallet. The final output is a per-wallet numeric score, which can be used for segmentation, risk profiling, or engagement strategies.

All logic is implemented in a single Python notebook. The repository also includes a `README.md` (this file) for orientation and an `analysis.md` containing post-scoring behavioral insights.

## Input Format

The system takes a JSON file (e.g., `user-wallet-transactions.json`) as input. Each entry in the list corresponds to one DeFi transaction with fields such as:

- `_id`: Unique identifier for the transaction.
- `userWallet`: Wallet address involved in the transaction.
- `network`: Blockchain network (e.g., `"polygon"`).
- `protocol`: Protocol used (e.g., `"aave_v2"`, `"uniswap_v3"`).
- `txHash`: Blockchain transaction hash.
- `timestamp`: Unix epoch of transaction confirmation.
- `action`: Operation performed (`"deposit"`, `"borrow"`, `"repay"`, `"swap"`, etc.).
- `actionData`: Dictionary holding structured details like:
  - `amount`: Amount of asset transacted.
  - `assetSymbol`: Symbol of the asset (e.g., `"USDC"`, `"ETH"`).
  - `assetPriceUSD`: Asset price at transaction time in USD.
  - `poolId`, `userId`: Optional protocol-specific fields.
- `createdAt`, `updatedAt`: Internal timestamps for the record.

The schema is designed to be extensible and protocol-agnostic.
