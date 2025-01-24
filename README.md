# BTC-Stable Protocol

A sophisticated decentralized finance protocol enabling the creation of USD-pegged stablecoins collateralized by Bitcoin on the Stacks blockchain.

## Overview

BTC-Stable is a decentralized protocol that allows users to generate USD-pegged stablecoins using Bitcoin as collateral. The system maintains price stability through dynamic collateralization ratios, liquidation mechanisms, and decentralized price oracles.

## Key Features

- **Overcollateralized Stablecoin**: Create USD-pegged stablecoins backed by Bitcoin at a minimum collateralization ratio of 150%
- **Dynamic Risk Parameters**: Adjustable collateralization ratios and liquidation thresholds
- **Decentralized Price Oracle System**: Multiple authorized oracles for reliable price feeds
- **Liquidation Mechanism**: Automated liquidation process to maintain system solvency
- **Governance Controls**: Protocol parameters adjustable through governance mechanisms
- **Emergency Controls**: Emergency shutdown capability for risk mitigation

## Core Components

### Vaults

- Users can create vaults to deposit Bitcoin collateral
- Mint stablecoins against deposited collateral
- Maintain minimum collateralization ratio of 150%
- Liquidation triggered at 120% collateral ratio

### Risk Parameters

- Minimum Collateral Ratio: 150%
- Liquidation Ratio: 120%
- Stability Fee: 2% annual rate
- Price Validity Checks: Ensures oracle prices are within valid ranges

### Protocol Constraints

- Maximum Price: $1B USD
- Minimum Price: $1 USD
- Maximum Collateral Ratio: 1000%
- Minimum Collateral Ratio: 101%
- Maximum Fee: 100%

## Core Functions

### Vault Management

```clarity
(create-vault (collateral-amount uint))
(mint-stablecoin (amount uint))
(repay-debt (amount uint))
(withdraw-collateral (amount uint))
```

### Liquidation

```clarity
(liquidate (vault-owner principal))
```

### Oracle Management

```clarity
(update-price (new-price uint))
```

### Governance

```clarity
(set-minimum-collateral-ratio (new-ratio uint))
(set-liquidation-ratio (new-ratio uint))
(set-stability-fee (new-fee uint))
```

### Access Control

```clarity
(add-liquidator (liquidator principal))
(remove-liquidator (liquidator principal))
(add-oracle (oracle principal))
(remove-oracle (oracle principal))
```

## Error Codes

| Code | Description                    |
| ---- | ------------------------------ |
| u100 | Owner-only operation           |
| u101 | Insufficient collateral        |
| u102 | Below minimum collateral ratio |
| u103 | Already initialized            |
| u104 | Not initialized                |
| u105 | Low balance                    |
| u106 | Invalid price                  |
| u107 | Emergency shutdown active      |
| u108 | Invalid parameter              |

## Security Features

1. **Access Control**

   - Owner-only administrative functions
   - Authorized liquidators system
   - Verified oracle network

2. **Price Safety**

   - Valid price range enforcement
   - Multiple oracle support
   - Price validity tracking

3. **Risk Management**

   - Emergency shutdown mechanism
   - Dynamic collateral ratios
   - Liquidation thresholds

4. **Parameter Bounds**
   - Maximum/minimum constraints on all parameters
   - Validation checks on all ratio updates
   - Fee limitations

## Query Functions

### Vault Information

```clarity
(get-vault (owner principal))
(get-collateral-ratio (owner principal))
```

### System Parameters

```clarity
(get-stability-parameters)
```

### Authorization Checks

```clarity
(is-authorized-liquidator (address principal))
(is-authorized-oracle (address principal))
```

## Usage Example

1. Create a vault and deposit collateral:

```clarity
(create-vault u1000000) ;; Deposit 1M µSTX
```

2. Mint stablecoins against collateral:

```clarity
(mint-stablecoin u500000) ;; Mint 500k stablecoins
```

3. Repay debt:

```clarity
(repay-debt u100000) ;; Repay 100k stablecoins
```

4. Withdraw collateral:

```clarity
(withdraw-collateral u200000) ;; Withdraw 200k µSTX
```

## Risk Considerations

1. **Collateral Risk**

   - Price volatility of Bitcoin
   - Liquidation scenarios
   - Oracle reliability

2. **System Risk**

   - Smart contract vulnerabilities
   - Oracle manipulation
   - Market conditions

3. **User Risk**
   - Liquidation exposure
   - Price fluctuation impact
   - Transaction timing

## Best Practices

1. **For Users**

   - Maintain healthy collateralization ratios (>200% recommended)
   - Monitor Bitcoin price movements
   - Understand liquidation mechanisms

2. **For Liquidators**

   - Monitor under-collateralized positions
   - Understand liquidation incentives
   - Maintain adequate capital

3. **For Oracles**
   - Provide accurate and timely price feeds
   - Maintain high uptime
   - Follow price update protocols

## Governance

The protocol includes governance mechanisms for adjusting key parameters:

- Collateralization ratios
- Liquidation thresholds
- Stability fees
- Oracle and liquidator management

## Emergency Procedures

The contract includes an emergency shutdown mechanism that can be triggered by the contract owner in case of:

- Severe market volatility
- Technical vulnerabilities
- Systemic risks

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting pull requests.
