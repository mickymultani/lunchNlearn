# 🚀 Create Your Own SPL Token on Solana

A comprehensive guide to creating and managing your own token on the Solana blockchain using SPL Token standard.

## 📋 Prerequisites

- Windows (with WSL), Linux, or macOS
- Visual Studio Code
- Phantom Wallet (Solana Devnet)
- Free account on [Pinata Cloud](https://pinata.cloud) for IPFS storage
- [Canva](https://canva.com) for token image design

## 🛠️ Environment Setup

### System Dependencies

First, update your system and install required packages:

```bash
# Update system packages
sudo apt-get update

# Install development dependencies
sudo apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev \
    llvm \
    libclang-dev \
    protobuf-compiler \
    libssl-dev
```

### Install Rust

```bash
# Install Rust using rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# Reload PATH to include Cargo
. "$HOME/.cargo/env"

# Verify installation
rustc --version
```

Expected output: `rustc 1.83.0 (90b35a623 2024-11-26)` or newer

### Install Solana CLI

```bash
# Install Solana CLI tools
sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

# Add Solana to PATH
export PATH="$HOME/.local/share/solana/install/active_release/bin:$PATH"

# Verify installation
solana --version
```

Expected output: `solana-cli 1.18.18` or newer

## 🎯 Token Creation Process

### 1. Project Setup

```bash
# Create and navigate to project directory
mkdir ~/lunchlearn
cd ~/lunchlearn
```

### 2. Generate Keypair

```bash
# Create new keypair
solana-keygen new --outfile ./lnl-keypair.json
```

> ⚠️ **Important**: Save the seed phrase securely! It's required for wallet recovery.

### 3. Configure Solana CLI

```bash
# Get public key
solana-keygen pubkey ./lnl-keypair.json

# Set configuration
solana config set --url devnet --keypair ~/lunchlearn/lnl-keypair.json

# Verify configuration
solana config get
```

### 4. Fund Your Wallet

```bash
# Request devnet SOL
solana airdrop 1

# Check balance
solana balance
```

> 💡 **Tip**: If airdrop fails, send 0.5 SOL from Phantom wallet on devnet.

### 5. Install SPL Token CLI

```bash
# Install Node.js and npm
sudo apt-get update && sudo apt-get install nodejs npm -y

# Install SPL Token CLI
npm install -g @solana/spl-token

# Verify installation
spl-token --version
```

### 6. Create and Configure Token

```bash
# Create token
spl-token create-token --decimals 9

# Create token account
spl-token create-account <TOKEN_MINT_ADDRESS>

# Mint tokens
spl-token mint <TOKEN_MINT_ADDRESS> 10000

# Check balance and supply
spl-token balance <TOKEN_MINT_ADDRESS>
spl-token supply <TOKEN_MINT_ADDRESS>
```

## 🎨 Adding Metadata

### 1. Install Metaboss

```bash
# Install Metaboss
cargo install metaboss

# Verify installation
metaboss --version
```

### 2. Prepare Token Assets

1. Create token image using Canva
2. Upload to Pinata Cloud (IPFS)
3. Create metadata JSON file:

```json
{
  "name": "LunchNLearn",
  "symbol": "LNL",
  "description": "A fun fungible token for our lunch and learn",
  "image": "ipfs://bafkreihashOfYourImage",
  "external_url": "https://mylunchandlearn.example.com",
  "attributes": [],
  "properties": {
    "category": "SPL Token",
    "creators": []
  }
}
```

### 3. Upload and Update Metadata

```bash
# Create metadata
metaboss create metadata \
  --keypair ./lnl-keypair.json \
  --mint <MINT_ADDRESS> \
  --metadata ./metadata.json

# Update metadata (if needed)
metaboss update uri \
  --keypair ./lnl-keypair.json \
  --account <MINT_ADDRESS> \
  --new-uri "new-metadata-uri"
```

## 🔑 Security Notes

- Keep your keypair file (`lnl-keypair.json`) secure and private
- Back up your seed phrase in a safe location
- Never share your private keys or seed phrase
- Use a strong BIP39 passphrase during keypair generation

## 📚 Additional Resources

- [Solana Documentation](https://docs.solana.com)
- [SPL Token Documentation](https://spl.solana.com/token)
- [Metaboss GitHub](https://github.com/samuelvanderwaal/metaboss)

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Made with ❤️ for the Solana community
