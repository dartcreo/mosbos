# Mosbos Cross-Chain Bridge Event Listener

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Production-grade simulation of a cross-chain bridge event listener** for decentralized systems. This is not a simple utility but a comprehensive component demonstrating enterprise blockchain architecture patterns.

## Concept

This repository implements a **Cross-Chain Bridge Event Listener** - a critical component in multi-chain DeFi ecosystems. The system:

- Monitors bridge contracts across **4 major EVM chains** (Ethereum, Polygon, BSC, Arbitrum)
- Processes **TransferInitiated** events in real-time
- Validates event integrity using Web3.py
- Handles **edge cases** (invalid addresses, negative amounts, network failures)
- Provides **thread-safe concurrent processing** with ThreadPoolExecutor
- Includes **comprehensive logging** and health monitoring
- Simulates realistic bridge events for development/testing

**Use Cases:**
- Cross-chain asset monitoring
- Bridge analytics dashboards
- Automated alerting systems
- Risk monitoring for bridge exploits

## Code Architecture

```
mosbos_event_listener/
├── RPCProvider          # Manages multi-chain Web3 connections
├── EventSimulator       # Generates realistic mock events
├── EventProcessor       # Validates & processes events
├── CrossChainEventListener  # Main orchestrator
├── BridgeEvent          # Event data model
└── ChainType           # Chain enumeration
```

**Key Design Patterns:**
- **Dependency Injection**: RPCProvider passed to EventProcessor
- **Thread Safety**: Lock-protected event storage
- **Dataclasses**: Immutable event models
- **Enum-based configuration**: Type-safe chain selection
- **Graceful degradation**: Continues operation on RPC failures

## How it Works

1. **Initialization**: Connects to 4 RPC endpoints, deploys mock bridge contracts
2. **Event Generation**: Simulates TransferInitiated events across chain pairs
3. **Validation Pipeline**: 
   - Address format validation
   - Amount positivity check
   - Token contract verification
4. **Concurrent Processing**: ThreadPoolExecutor handles high throughput
5. **Status Tracking**: Pending → Confirmed based on mock confirmations
6. **Metrics Collection**: Real-time stats with recent events

**Production Features:**
- Health checks for all RPC connections
- Comprehensive logging (file + console) 
- Graceful shutdown handling
- Configurable worker pools
- Edge case handling

## Features

✅ **Multi-Chain Support**: Ethereum, Polygon, BSC, Arbitrum
✅ **Real-time Processing**: Concurrent event handling
✅ **Event Validation**: Comprehensive data integrity checks
✅ **Production Logging**: Structured logs with rotation
✅ **Health Monitoring**: RPC connection status
✅ **Statistics Dashboard**: Processing metrics
✅ **Mock Event Generation**: Realistic simulation data
✅ **Type Hints**: Full static type checking
✅ **Graceful Error Handling**: Continues operation on failures

## Usage Example

```bash
# Install dependencies
pip install -r requirements.txt

# Run the listener (30-second demo)
python mosbos_event_listener.py
```

**Sample Output:**
```json
{
  "rpc_healthy": true,
  "stats": {
    "total_events": 60,
    "processed": 58,
    "rejected": 1,
    "errors": 1
  },
  "recent_events": [
    {
      "event_id": "evt_00000060",
      "chain_from": "polygon",
      "chain_to": "arbitrum",
      "amount": 1012.3
    }
  ]
}
```

## API Methods

```python
listener = CrossChainEventListener(max_workers=8)

# Health check
listener.health_check()

# Start listening
listener.listen_to_bridge_events(duration=300)  # 5 minutes

# Get statistics
listener.get_stats()

# Graceful shutdown
listener.shutdown()
```

## Production Deployment

```bash
# Docker (recommended)
docker build -t mosbos-listener .
docker run -d --name bridge-listener mosbos-listener

# Systemd service
git clone https://github.com/yourorg/mosbos.git
cd mosbos
pip install -r requirements.txt
python mosbos_event_listener.py
```

## Configuration

Environment variables for production:

```bash
export RPC_ETHEREUM=https://your-alchemy-url
export RPC_POLYGON=https://your-polygon-rpc
export LOG_LEVEL=DEBUG
export MAX_WORKERS=16
```

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/chain-support`)
3. Commit changes (`git commit -m 'Add new chain support'`)
4. Push to branch (`git push origin feature/chain-support`)
5. Open Pull Request

## License

MIT License - see [LICENSE](LICENSE) file.

---

**Built with ❤️ for blockchain architects**
