# Ethereum MCP Server

[![Python Version](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A powerful and lightweight MCP (Machine-to-Machine Communication Protocol) server for the Ethereum blockchain, built with Python. This server provides a simple interface to query crucial on-chain data, making it an excellent backend for blockchain applications, bots, or data analysis tools.

## ✨ Features

- **Account Balance:** Get the ETH balance for any Ethereum address.
- **Real-time Price:** Fetch the current price of Ethereum in USD.
- **Network Gas Price:** Retrieve the current gas price from the network.
- **Block Information:** Get details about the latest mined block.
- **Transaction Details:** Look up specific transactions by their hash.
- **Fee Estimation:** Estimate transaction fees based on gas amount.
- **Full Transaction History:** Pull the complete transaction history for any account using the Etherscan API.
- **REST-like Resources:** Access common data points like price, network stats, and address info through resource URIs.
- **Async Ready:** Built on `FastMCP` for efficient, non-blocking operations.

## 🛠️ Setup and Installation

Follow these steps to get the server up and running on your local machine.

### 1. Clone the Repository

```bash
git clone https://github.com/mukku27/ethereum-mcp-server.git
cd ethereum-mcp-server
```

### 2. Create a Virtual Environment

It is recommended to use a virtual environment to manage dependencies.

```bash
# For Unix/macOS
python3 -m venv venv
source venv/bin/activate

# For Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies

This project uses `uv` for fast dependency management. Install the required packages using:

```bash
pip install uv
uv pip install -e .
```
This command installs the project in editable mode and all its dependencies listed in `pyproject.toml`.

### 4. Set Up Environment Variables

The server requires an Etherscan API key to fetch account transaction histories.

1.  Create a `.env` file in the root of the project directory:
    ```bash
    touch .env
    ```
2.  Get a free API key from [Etherscan](https://etherscan.io/myapikey).
3.  Add your API key to the `.env` file:
    ```env
    ETHERSCAN_API_KEY="YOUR_ETHERSCAN_API_KEY_HERE"
    ```

## 🚀 Running the Server

Once set up, you can run the MCP server directly from the command line. It will listen for JSON-RPC requests on `stdio`.

```bash
python main.py
```

The server is now running and waiting for input.

### Example Interaction

You can interact with the server by sending JSON-RPC formatted requests through standard input.

#### Get ETH Balance

**Request:**
```json
{"jsonrpc": "2.0", "method": "get_eth_balance", "params": {"address": "0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae"}, "id": 1}
```

**Response:**
```json
{"jsonrpc": "2.0", "result": "10419.49799152033 ETH", "id": 1}
```

#### Get Latest Block Information

**Request:**
```json
{"jsonrpc": "2.0", "method": "get_latest_block", "params": {}, "id": 2}
```

**Response:**
```json
{
  "jsonrpc": "2.0",
  "result": {
    "number": 20349835,
    "timestamp": 1715878259,
    "miner": "0x1f9090aae28b8a3dceadf281b0f12828e676c326",
    "transaction_count": 145,
    "gas_used": 15724285,
    "gas_limit": 30000000
  },
  "id": 2
}
```

## 📚 API Reference

The server exposes the following methods and resources.

### Tools (RPC Methods)

| Method                       | Parameters                                     | Description                                          |
| ---------------------------- | ---------------------------------------------- | ---------------------------------------------------- |
| `get_eth_balance`            | `address: str`                                 | Get the ETH balance of an Ethereum address.          |
| `get_eth_price`              | -                                              | Get the current Ethereum price in USD.               |
| `get_gas_price`              | -                                              | Get the current Ethereum network gas price in Gwei.  |
| `get_latest_block`           | -                                              | Get information about the latest block.              |
| `get_transaction`            | `tx_hash: str`                                 | Get details for a specific transaction.              |
| `estimate_tx_fee`            | `gas_amount: int`                              | Estimate a transaction fee in ETH.                   |
| `get_account_transactions`   | `address: str`, `page: int=1`, `offset: int=20` | Get transaction history for an account.              |

### Resources

| URI                                   | Description                                                 |
| ------------------------------------- | ----------------------------------------------------------- |
| `ethereum://price`                    | Get Ethereum price information from CoinGecko.              |
| `ethereum://stats`                    | Get general Ethereum network statistics.                    |
| `ethereum://address/{address}`        | Get balance and transaction count for a specified address.  |
| `ethereum://address/{address}/transactions` | Get the transaction history for a specified address.        |

## 🤝 Contributing

Contributions are welcome! If you have ideas for new features or improvements, feel free to open an issue to discuss it or submit a pull request.

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
