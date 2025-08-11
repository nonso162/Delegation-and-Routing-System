# Contract Router

A sophisticated smart contract routing and delegation system built on the Stacks blockchain, enabling secure, efficient, and controlled contract-to-contract interactions.

## Overview

Contract Router provides an advanced proxy architecture that allows for secure delegation of contract calls with granular access control, operation whitelisting, and comprehensive routing metrics. This system is designed to facilitate complex DeFi protocols, modular contract architectures, and upgradeable smart contract patterns.

## Key Features

- **Secure Routing**: Implements robust authorization mechanisms for contract-to-contract communication
- **Operation Registry**: Granular control over which operations can be routed through the system
- **Router Authorization**: Multi-level access control for different types of callers
- **Routing Metrics**: Built-in analytics and usage tracking for optimization
- **Emergency Controls**: Administrative pause/resume functionality for security incidents
- **Trait-Based Architecture**: Type-safe contract interactions using Clarity traits

## Architecture

The Contract Router operates as an intermediary layer between calling contracts and destination contracts, providing:

1. **Authorization Layer**: Validates that only authorized routers can initiate calls
2. **Operation Registry**: Ensures only registered operations are permitted
3. **Metrics Collection**: Tracks usage patterns and routing statistics
4. **Administrative Controls**: Provides emergency controls and configuration management

## Core Components

### Traits
- `routable-contract-trait`: Interface that destination contracts must implement

### Data Variables
- `destination-contract`: The currently configured destination for routing
- `router-active`: Global activation status of the routing system

### Maps
- `authorized-routers`: Tracks which principals can initiate routes
- `operation-registry`: Whitelist of permitted operations
- `routing-metrics`: Usage statistics per router

## Usage

### Initialization
```clarity
;; Activate the router with a destination contract
(contract-call? .contract-router activate-router 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.destination-contract)
```

### Router Authorization
```clarity
;; Authorize a new router
(contract-call? .contract-router authorize-router 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.my-router true)
```

### Operation Registration
```clarity
;; Register a new operation
(contract-call? .contract-router register-operation "transfer-tokens" true)
```

### Routing Operations
```clarity
;; Route an operation to the destination contract
(contract-call? .contract-router route-operation 
    destination-contract 
    "transfer-tokens" 
    (list u100 u200))
```

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 200 | `err-admin-only` | Only the router admin can perform this action |
| 201 | `err-router-not-active` | Router system is not currently active |
| 202 | `err-router-already-active` | Router is already activated |
| 203 | `err-invalid-destination` | Invalid destination contract address |
| 204 | `err-unauthorized-route-access` | Caller not authorized to route operations |
| 205 | `err-forbidden-operation` | Operation not registered in the operation registry |
| 206 | `err-metrics-update-failure` | Failed to update routing metrics |
| 207 | `err-invalid-route-caller` | Invalid caller for router authorization |
| 208 | `err-invalid-operation-id` | Invalid operation identifier |
| 209 | `err-invalid-destination-contract` | Invalid destination contract for routing |

## Security Considerations

- **Admin Access**: Only the router admin can modify system configuration
- **Authorization Checks**: All routing operations require proper authorization
- **Operation Validation**: Only pre-registered operations can be executed
- **Emergency Controls**: System can be paused in case of security incidents
- **Input Validation**: All inputs are validated before processing

## Development

### Prerequisites
- Stacks blockchain development environment
- Clarity smart contract knowledge
- Understanding of proxy patterns and delegation

### Testing
Comprehensive test coverage should include:
- Authorization mechanism testing
- Operation registry validation
- Routing metrics accuracy
- Emergency control functionality
- Edge case handling

## Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your changes with tests
4. Submit a pull request with detailed description

## Support

For questions, issues, or contributions, please open an issue in the repository.