# Agriculture Supply Chain Management Smart Contract

## About
This smart contract implements a comprehensive supply chain management system for agricultural products on the Stacks blockchain. It enables tracking of agricultural products, quality control mechanisms, and stakeholder management throughout the supply chain process.

## Features
- Stakeholder registration and management
- Product lifecycle tracking
- Quality control and certification
- Location tracking
- Ownership transfer management
- Detailed transaction history

## Contract Components

### Registry Systems
1. **Stakeholder Registry**
   - Maintains records of all authorized participants
   - Tracks participant roles, activity status, and reputation scores
   - Managed by contract owner

2. **Product Registry**
   - Records all registered agricultural products
   - Tracks current ownership, location, and quality metrics
   - Maintains product status and certification details

3. **Transaction History**
   - Records all supply chain activities
   - Maintains detailed audit trail of ownership transfers
   - Tracks quality assessments and location updates

### Key Functions

#### Administrative Functions
1. `register-stakeholder`
   - Parameters: `stakeholder-address`, `stakeholder-type`
   - Registers new supply chain participants
   - Only executable by contract owner

2. `update-stakeholder-status`
   - Parameters: `stakeholder-address`, `is-active`
   - Enables/disables stakeholder participation
   - Only executable by contract owner

#### Product Management
1. `register-product`
   - Parameters: `product-id`, `product-title`, `product-position`, `product-price`
   - Registers new agricultural products in the system
   - Only authorized stakeholders can register products

2. `update-product-phase`
   - Parameters: `product-id`, `new-phase`, `phase-notes`
   - Updates product status in the supply chain
   - Only current owner can update status

3. `transfer-ownership`
   - Parameters: `product-id`, `new-owner`, `transfer-details`
   - Transfers product ownership between stakeholders
   - Requires both parties to be authorized stakeholders

4. `update-quality`
   - Parameters: `product-id`, `new-quality-score`, `quality-details`
   - Updates product quality metrics
   - Records quality certification status

5. `update-position`
   - Parameters: `product-id`, `new-position`, `position-notes`
   - Updates product location information
   - Only current owner can update location

### Read-Only Functions
1. `get-product-details`
   - Retrieves complete product information
2. `get-stakeholder-info`
   - Retrieves stakeholder details
3. `get-transaction-details`
   - Retrieves specific transaction records

## Error Codes
- `ERROR-NOT-AUTHORIZED (u1)`: Unauthorized access attempt
- `ERROR-PRODUCT-DOES-NOT-EXIST (u2)`: Product not found in registry
- `ERROR-INVALID-STATUS-CHANGE (u3)`: Invalid status transition
- `ERROR-EXISTING-RECORD (u4)`: Duplicate record creation attempt
- `ERROR-INVALID-DATA (u5)`: Invalid input data

## Data Validation
The contract implements comprehensive validation for:
- String length constraints
- Numeric value ranges
- Authorization checks
- Data existence verification

## Quality Control
- Quality scores range from 0 to 100
- Minimum required quality score: 60
- Automatic certification status updates based on quality scores

## Usage Examples

### Registering a New Stakeholder
```clarity
(contract-call? 
    .agriculture-contract
    register-stakeholder
    'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
    "producer"
)
```

### Registering a New Product
```clarity
(contract-call?
    .agriculture-contract
    register-product
    u1
    "Organic Wheat"
    "Farm A, Location X"
    u1000
)
```

### Transferring Ownership
```clarity
(contract-call?
    .agriculture-contract
    transfer-ownership
    u1
    'ST2CY5V39NHDPWSXMW9QDT3HC3GD6Q6XX4CFRK9AG
    "Transfer to distributor"
)
```

## Security Considerations
1. Only the contract owner can register or modify stakeholder status
2. Only authorized stakeholders can perform supply chain operations
3. Product modifications restricted to current owners
4. All transactions are permanently recorded on the blockchain
5. Input validation prevents invalid data entry

## Best Practices
1. Always verify stakeholder authorization before transactions
2. Include detailed notes for all status updates
3. Maintain accurate location information
4. Regular quality assessments
5. Verify transaction success through response codes