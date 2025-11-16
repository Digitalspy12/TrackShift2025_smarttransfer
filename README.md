# Smart File Transfer

Secure, peer-to-peer file transfer desktop application with NAT traversal. Built with Rust, Tauri, and the Iroh protocol for high-performance, direct file transfers without cloud intermediaries.

## Features

- **Encrypted P2P Transfers** - End-to-end encryption via QUIC + TLS 1.3 with perfect forward secrecy
- **Automatic NAT Traversal** - Hole punching with relay fallback for seamless connectivity behind firewalls
- **No File Size Limits** - Transfer directories and files of any size (tested up to 500GB+)
- **Cross-Platform** - Native builds for macOS, Linux, and Windows
- **High Performance** - Multi-gigabit throughput capable:
  - 1GbE: 70-115 MB/s
  - 10GbE: 900-1,100 MB/s
  - Optimized for high-latency and lossy networks
- **Resumable Transfers** - Automatic resume after disconnections
- **Cryptographic Integrity** - Real-time BLAKE3 chunk-level verification
- **Ticket-Based System** - Simple share tokens for easy recipient connection
- **CLI Compatible** - Interoperable with the `sendme` command-line tool

## Installation

### Prerequisites

**Rust 1.81+**

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

**Node.js 18+**

```bash
# Download from https://nodejs.org/ or use nvm:
nvm install 18
```

**Platform-Specific Dependencies**

_macOS_: None required.

_Linux (Ubuntu/Debian)_:

```bash
sudo apt update
sudo apt install libwebkit2gtk-4.1-dev build-essential curl wget libssl-dev libgtk-3-dev
```

_Windows_: Install Visual Studio Build Tools with "Desktop Development with C++" workload.

_macOS users_: After installation, run:

```bash
xattr -cr /Applications/fall_ak.app
```

### Build from Source

```bash
# Clone the repository
git clone https://github.com/Digitalspy12/TrackShift2025_smarttransfer.git
cd TrackShift2025_smarttransfer

# Install frontend dependencies
cd web-app && npm install

# Build the application
cd ../src-tauri
cargo tauri build

# The installer will be in src-tauri/target/release/bundle/
```

## Usage

### Sending Files

1. Launch the application
2. Click the "Send" tab
3. Drag and drop files/folders or click "Browse File"/"Browse Folder"
4. Click "Start Sharing"
5. Copy the generated ticket and share it with the recipient
6. Keep the application open until transfer completes

### Receiving Files

1. Click the "Receive" tab
2. Paste the ticket from the sender
3. Choose a save location
4. Click "Download"
5. Wait for the transfer to complete

## Development Setup

```bash
# Install dependencies
cd web-app && npm install

# Run in development mode (hot reload for both frontend and backend)
cd ../src-tauri && cargo tauri dev

# Lint frontend code
cd web-app && npm run lint

# Sync version across all package files
node scripts/sync-version.js
```

## Project Structure

```
fall_ak/
├── src/                      # Core Rust library
│   ├── core/send.rs         # File sharing implementation
│   ├── core/receive.rs      # File receiving implementation
│   └── core/types.rs        # Shared types and configurations
├── src-tauri/               # Tauri backend
│   ├── src/
│   │   ├── main.rs         # Application entry point
│   │   ├── commands.rs     # Tauri command handlers
│   │   └── state.rs        # Application state management
│   └── tauri.conf.json     # Tauri configuration
├── web-app/                 # React frontend
│   ├── src/
│   │   ├── App.tsx         # Main application component
│   │   ├── components/     # UI components
│   │   └── hooks/          # React hooks for Tauri integration
│   └── package.json        # Frontend dependencies
└── scripts/
    └── sync-version.js     # Version synchronization utility
```

## Building

### Development Build

```bash
cd src-tauri
cargo tauri build --no-bundle
# Binary: target/release/fall_ak
```

### Production Build

```bash
cd src-tauri
cargo tauri build
# Installers: target/release/bundle/
```

## License

- **Core Library** (`src/`): AGPL-3.0
- **Tauri Application** (`src-tauri/`): Apache-2.0 OR MIT

See individual LICENSE files for details.
