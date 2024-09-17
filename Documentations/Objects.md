# Objects
Objects are ledger entries that represent persistent data structures associated with an account on the XRPL. These objects are stored on the ledger and have an ongoing state that can be referenced and modified by transactions. Common types of objects include:

- Trust Lines: Represent a line of trust between two accounts for a specific issued currency.
- Offers: Entries for buy or sell orders on the decentralized exchange (DEX).
- Escrows: Conditional holds of XRP that are released when specific conditions are met.
- Payment Channels: Structures that allow off-ledger payments which can be settled later.
- SignerList: Lists of multi-signature signers for an account.

These objects contribute to the `OwnerCount` of an account and affect the account's reserve requirements.
