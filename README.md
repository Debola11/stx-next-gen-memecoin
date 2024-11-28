# Stacks next-gen Memecoin Token Contract

## Overview
The Stacks next-gen Memecoin Token Contract is a Stacks-based smart contract built using Clarity. It provides a robust infrastructure for managing a fungible token, MemeToken (MEME), while integrating features such as block-height-based operations, staking, and governance. This contract emphasizes secure token handling, time-based operations, and community-driven governance, all tailored for the Stacks blockchain ecosystem.

## Key Features
1. **Fungible Token (MEME)**
    - Fully compliant with Stacks' fungible token standard.
    - Supports basic token operations: transfer, staking, and governance.
2. **Manual Block Height Handling**
    - Tracks and updates the block height manually.
    - Used for cooldowns, staking periods, and governance voting deadlines.
3. **Cooldown-Enabled Token Transfers**
    - Prevents rapid sequential transfers by enforcing a block-height-based cooldown (10 blocks).
4. **Staking Mechanism**
    - Allows users to lock MEME tokens for a specified duration (in blocks).
    - Automatically calculates the unlock block height based on the staking period.
5. **Governance Proposal and Voting**
    - Users can propose governance changes with descriptions.
    - Supports voting within a defined block-height window.

## Deployment

### Prerequisites
- A Stacks wallet for deploying and interacting with the contract.
- A Clarity-compatible development environment (e.g., Clarinet).

### Deployment Steps
1. Clone this repository.
2. Compile the contract using Clarinet:
    ```bash
    clarinet check
    ```
3. Deploy the contract to the desired Stacks blockchain:
    ```bash
    clarinet deploy --network=<network>
    ```
    Replace `<network>` with testnet, mainnet, or another supported network.

## Usage

### Functions Overview

#### Block Height Management
- `update-block-height`: Increments the block height manually. This simulates the passage of time in a testnet environment or controlled scenarios.
- `get-block-height`: Returns the current block height.

#### Token Operations
- `transfer`: Transfers MEME tokens with a 10-block cooldown check.
  - **Arguments:**
     - `amount (uint)`: Amount to transfer.
     - `recipient (principal)`: Address of the recipient.
  - **Cooldown Enforcement:** Checks the sender’s last transfer block against the current block height.

#### Staking
- `stake-tokens`: Stakes MEME tokens for a specified lock period.
  - **Arguments:**
     - `amount (uint)`: Tokens to stake.
     - `lock-period (uint)`: Number of blocks to lock.
- `unstake-tokens`: Unstakes tokens if the lock period has passed.

#### Governance
- `create-governance-proposal`: Initiates a proposal with a description and voting period.
  - **Arguments:**
     - `description (string)`: A summary of the proposal.
     - `voting-period (uint)`: Number of blocks for voting.
- `vote-on-proposal`: Casts a vote on an active proposal.
  - **Arguments:**
     - `proposal-id (uint)`: ID of the proposal to vote on.

### Example Interactions

#### Transfer Tokens
```clarity
(contract-call? .memecoin transfer u1000 'SP3...)
```

#### Stake Tokens
```clarity
(contract-call? .memecoin stake-tokens u500 u20)
```

#### Propose Governance
```clarity
(contract-call? .memecoin create-governance-proposal "Increase max supply" u100)
```

## Design Considerations

### Manual Block Height Tracking
- Simulates blockchain time for testnets or off-chain controlled environments.
- Provides flexibility in time-sensitive operations without relying on external systems.

### Cooldown for Transfers
- Implements a basic rate-limiting mechanism, enhancing security by mitigating spam transfers.

### Governance with Deadlines
- Enables decentralized decision-making with a transparent voting mechanism.

## Security Notes
- **Owner Privileges:** The contract owner is designated as the deployer (tx-sender) and has exclusive control over certain operations.
- **Error Handling:** Errors are explicitly defined and handled for common scenarios like insufficient balance, cooldown violations, or governance conflicts.

## Stacks Ecosystem Integration

### Why Stacks?
Stacks enables Bitcoin-secured smart contracts through its unique proof-of-transfer (PoX) mechanism. This contract takes advantage of Stacks' clarity for determinism and the broader Bitcoin ecosystem for security.

### Potential Integrations
- **Stacks Wallets:** Manage MEME tokens.
- **Explorer Support:** Monitor transactions and governance activity.
- **Stacks dApps:** Integrate staking and governance directly.

## Future Enhancements
- Automated block height synchronization with Stacks’ native block data.
- Enhanced staking rewards mechanisms.
- Cross-contract interactions for broader ecosystem integration.

## Acknowledgments
Built using principles from "Clean Code" by Robert C. Martin, and Stacks' Clarity documentation.





