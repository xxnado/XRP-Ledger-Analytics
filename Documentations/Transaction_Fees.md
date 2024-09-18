# Transaction Fees 
#### (≠ Transfer Fees for Tokens!)

On the XRP Ledger (XRPL), the sender of the transaction is responsible for paying the transaction fees. This fee is deducted from the sender's account balance and is not transferred to any other party or validator; it is instead destroyed (burned) to reduce the total supply of XRP slightly. The recipient always obtains the full intended amount.

### 1. Base Fee
- The base fee is denominated in drops of XRP, where 1 XRP = 1,000,000 drops. The typical base fee is 10 drops (0.00001 XRP), though it can vary depending on network conditions.


### 2. Load Factor (Fee Variability)
- While the base transaction fee is usually very low, the XRPL can adjust this fee dynamically based on network load. If the ledger is experiencing high traffic, the required fee may increase to prevent the network from becoming congested.
- During normal operations, the load factor is 1, so the fee is simply the base fee (10 drops). If the network experiences heavy usage, the load factor increases, raising the fee to prevent spam.

### 3. How to Calculate the Total Fee

The base fee is multiplied by the load factor (adjusted by the network to reflect the current traffic) 

`Fee = Base Fee × Load Factor`

Example: If the load factor increases to 5 due to high traffic, the fee would be:
`Fee = 10 drops × 5 = 50 drops = 0.00005 XRP`

### 3. Reserve Requirements
- In addition to transaction fees, the XRPL also implements a reserve requirement. This is the minimum amount of XRP that an account must hold to exist on the ledger.
- The current reserve requirement is 10 XRP for a new account and an additional 2 XRP for each object (e.g., trust lines, offers) that the account creates on the ledger.
- Reserve requirements help prevent the ledger from being filled with unused or low-value accounts.

### 4. Special Cases
- Multi-Signing: When a transaction requires multiple signatures, each additional signature may slightly increase the transaction fee.
  `Fee = (Base Fee × Load Factor) + (Extra Fee per Signature)`
- Escrow and Payment Channels: Advanced features like escrow and payment channels may have specific fee implications based on how they interact with   the network.
