# Base MCP Integration with Flock Web3 Agent Model

This guide provides step-by-step instructions for setting up and running the Base MCP (Model Context Protocol) with the Flock Web3 Agent Model.

## Prerequisites

- Node.js and npm installed
- Python 3.8+ installed
- Git installed

## Installation and Setup

### 1. Install and Configure Base MCP

Base MCP Server extends any MCP client's capabilities by providing tools to do anything on Base. Follow these steps to install:

```bash
# Clone the repository
git clone https://github.com/base/base-mcp.git
cd base-mcp
```

Modify the network configuration in `src/index.ts` file:

Find this code:
```typescript
const cdpWalletProvider = await CdpWalletProvider.configureWithWallet({
  mnemonicPhrase: seedPhrase,
  apiKeyName,
  apiKeyPrivateKey: privateKey,
  networkId: 'base-mainnet',
});
```

Change it to use the test network (Base Sepolia):
```typescript
const cdpWalletProvider = await CdpWalletProvider.configureWithWallet({
  mnemonicPhrase: seedPhrase,
  apiKeyName,
  apiKeyPrivateKey: privateKey,
  networkId: 'base-sepolia',
});
```

Install dependencies and build the project:
```bash
npm install
npm run build
```

### 2. Install SGLang and Host the Flock Web3 Agent Model

```bash
# Install SGLang (reference: https://docs.sglang.ai/start/install.html)

# Install Hugging Face Hub CLI
pip install -U "huggingface_hub[cli]"

# Download the Flock Web3 Agent Model
huggingface-cli download flock-io/Flock_Web3_Agent_Model --local-dir Flock_Web3_Agent_Model

# Launch the model server
python -m sglang.launch_server --model-path Flock_Web3_Agent_Model --host 0.0.0.0
```

### 3. Set Up the Awesome Web3 MCP Project

```bash
# Clone the repository
git clone https://github.com/FLock-io/awesome-web3-mcp.git

# Navigate to the example directory
cd awesome-web3-mcp/examples/base-mcp/mcp_simple_chatbot

# Create environment file from the example
cp .env.example .env
```

If you didn't set an API_KEY when launching the SGLang model server, you can set `LLM_API_KEY=None` in the `.env` file.

### 4. Configure and Run

1. Modify the `servers_config.json` file to update the server path and COINBASE-related environment variables.

2. Run the chatbot:
```bash
python main-flock-model.py
```

## Usage

You can now try out the examples listed in the [Base MCP documentation](https://github.com/base/base-mcp?tab=readme-ov-file#available-tools).

## Resources

- [Base MCP Repository](https://github.com/base/base-mcp)
- [SGLang Documentation](https://docs.sglang.ai/start/install.html)
- [Flock Web3 Agent Model](https://github.com/FLock-io/awesome-web3-mcp)