# XRPL Common Fields

Every transaction has the same set of common fields, plus additional fields based on the transaction type. Field names are case-sensitive. The common fields for all transactions are:

### 1. **Account**
- **JSON Type**: String  
- **Internal Type**: AccountID  
- **Description**: (Required) The unique address of the account that initiated the transaction. This field specifies the sender of the transaction and is mandatory for all transaction types.
- **Example**: `"rXieaAC3nevTKgVu2SYoShjTCS2Tfczqx"`

### 2. **TransactionType**
- **JSON Type**: String  
- **Internal Type**: UInt16  
- **Description**: (Required) The type of transaction. Valid transaction types include `Payment`, `OfferCreate`, `TrustSet`, and others. This field dictates how the transaction is processed and what additional fields are required.
- **Example**: `"Payment"`

### 3. **Fee**
- **JSON Type**: String  
- **Internal Type**: Amount  
- **Description**: (Required; auto-fillable) The amount of XRP, in drops, to be destroyed as a cost for distributing this transaction to the network. Some transaction types have different minimum fee requirements. This field prevents spam by ensuring transactions have a cost.
- **Example**: `"12"` (equivalent to 0.000012 XRP)

### 4. **Sequence**
- **JSON Type**: Number  
- **Internal Type**: UInt32  
- **Description**: (Required; auto-fillable) The sequence number of the account sending the transaction. Each transaction from an account must have a `Sequence` number exactly 1 greater than the previous transaction. The special case of `0` means the transaction uses a Ticket (requires the TicketBatch amendment).
- **Example**: `25`

### 5. **AccountTxnID**
- **JSON Type**: String  
- **Internal Type**: Hash256  
- **Description**: (Optional) A hash value identifying another transaction. If this field is provided, the current transaction is only valid if the sending account's previous transaction matches the provided hash. This can be used to ensure that transactions occur in a specific order.
- **Example**: `"5A8D3F7A7F2E94C0..."`

### 6. **Flags**
- **JSON Type**: Number  
- **Internal Type**: UInt32  
- **Description**: (Optional) A set of bit-flags that modify the behavior of the transaction. Different flags can be used depending on the transaction type to change how the transaction is processed.
- **Example**: `2147483648`

### 7. **LastLedgerSequence**
- **JSON Type**: Number  
- **Internal Type**: UInt32  
- **Description**: (Optional; strongly recommended) The highest ledger index in which this transaction can appear. This field sets a strict upper limit on how long the transaction can wait to be validated. If the transaction is not validated by this ledger, it is considered failed.
- **Example**: `50000000`

### 8. **Memos**
- **JSON Type**: Array of Objects  
- **Internal Type**: Array  
- **Description**: (Optional) An array containing arbitrary information attached to the transaction. Each memo can include data like transaction notes or identifiers, commonly used for referencing purposes or to include supplementary information.
- **Example**:
  ```json
  [
    {
      "Memo": {
        "MemoType": "687474703a2f2f6578616d706c652e636f6d", // Hex for "http://example.com"
        "MemoData": "72656d61726b73" // Hex for "remarks"
      }
    }
  ]
  ```

### 9. **NetworkID**
- **JSON Type**: Number  
- **Internal Type**: UInt32  
- **Description**: (Network-specific) The network ID of the chain the transaction is intended for. This field is required on chains with a network ID of 1025 or higher but must be omitted for the Mainnet and some test networks. This field helps direct the transaction to the correct network.
- **Example**: `1025`

### 10. **Signers**
- **JSON Type**: Array  
- **Internal Type**: Array  
- **Description**: (Optional) An array of objects representing a multi-signature that authorizes the transaction. This allows multiple accounts to sign a single transaction, increasing security and flexibility in account management.
- **Example**:
  ```json
  [
    {
      "Signer": {
        "Account": "rHnVdV...5ZKd",
        "TxnSignature": "3044022079...",
        "SigningPubKey": "ED5F0B9..."
      }
    }
  ]
  ```

### 11. **SourceTag**
- **JSON Type**: Number  
- **Internal Type**: UInt32  
- **Description**: (Optional) An arbitrary integer used to identify the reason for this payment or to specify a sender on whose behalf the transaction is made. Often used in situations where one account handles multiple customers.
- **Example**: `12345`

### 12. **SigningPubKey**
- **JSON Type**: String  
- **Internal Type**: Blob  
- **Description**: (Automatically added when signing) The hexadecimal representation of the public key corresponding to the private key that signed the transaction. If this field is an empty string, it indicates the presence of a multi-signature in the `Signers` field.
- **Example**: `"ED5F0B9F30DB74FC5BA4F8429E..."`

### 13. **TicketSequence**
- **JSON Type**: Number  
- **Internal Type**: UInt32  
- **Description**: (Optional) The sequence number of a ticket to use instead of a regular sequence number. If this is provided, the `Sequence` field must be `0`. Tickets provide flexibility in transaction management by allowing transactions to use a reserved sequence slot.
- **Example**: `101`

### 14. **TxnSignature**
- **JSON Type**: String  
- **Internal Type**: Blob  
- **Description**: (Automatically added when signing) The cryptographic signature that verifies this transaction originates from the account it claims to. It ensures the transaction is authorized by the account owner.
- **Example**: `"3045022100A8E8B1E..."`
