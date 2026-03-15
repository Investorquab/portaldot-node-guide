# 🟣 Portaldot Node Runner Guide
### Run a real Portaldot P2P network — from zero to two connected nodes

> **Why run a node?**
> Network rewards (POT) go exclusively to those who operate nodes. Running a node = securing the network = earning POT. This guide gets you there in minutes, no matter what device you're using.

---

## 📋 What You Will Do

1. **Set up your environment** — pick the one that fits you
2. **Start Node 1 (Alice)** — the bootnode that anchors the network
3. **Start Node 2 (Bob)** — connect a second node to Alice via P2P
4. **Validate** — confirm `1 peers` in the logs — you're live!

---

## 🖥️ Pick Your Environment

| Environment | Best For |
|---|---|
| [Windows (WSL2 Ubuntu)](#-windows-wsl2-ubuntu) | Most Windows users |
| [Ubuntu / Linux (native)](#-ubuntu--linux-native) | Linux users |
| [GitHub Codespaces](#-github-codespaces) | Anyone with a browser — no install needed |
| [Termux (Android phone)](#-termux-android-phone) | Mobile users |
| [PowerShell (Windows)](#-powershell-windows-only) | Windows without WSL |

---

## 🪟 Windows (WSL2 Ubuntu)

### Step 1 — Install WSL (one time only)

Open **PowerShell** as Administrator and run:

```powershell
wsl --install -d Ubuntu
```

- Wait for it to finish (may take a few minutes)
- Restart your PC if asked
- After restart, Ubuntu opens and asks you to create a username and password

> ⚠️ While typing your password, nothing shows on screen — this is normal. Just type and press Enter.

### Step 2 — Open Ubuntu

Press `Win` key → search **PowerShell** → type:

```powershell
wsl
```

You should see something like:
```
yourname@YourPC:/mnt/c/Users/YourName$
```

### Step 3 — Go to home folder and download the node

```bash
cd ~
mkdir -p portaldot && cd portaldot
wget https://github.com/portaldotVolunteer/Portaldot-node/raw/main/portaldot-testnet-ubuntu.tar.gz
tar -xzvf portaldot-testnet-ubuntu.tar.gz
cd portaldot-testnet-ubuntu
chmod +x portaldot_dev
```

### Step 4 — Start Node 1 (Alice)

> Replace `YOUR_NAME` with your actual username — this is how the team identifies your node!

```bash
./portaldot_dev --dev --alice --name YOUR_NAME --base-path /tmp/alice
```

Wait for this line to appear:
```
🏷 Local node identity is: 12D3KooW...
```

**Copy that Peer ID** — you need it for Bob.

> ⚠️ Keep this terminal open! Alice must stay running.

### Step 5 — Open a NEW terminal for Bob

Open a new PowerShell window and run:

```powershell
wsl
cd ~/portaldot/portaldot-testnet-ubuntu
```

Then run Bob, replacing `YOUR_NAME_BOB` with your username and `PASTE_ALICE_PEER_ID` with the ID you copied:

```bash
./portaldot_dev --dev --bob --name YOUR_NAME_BOB \
  --base-path /tmp/bob \
  --port 30334 \
  --rpc-port 9945 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/PASTE_ALICE_PEER_ID
```

### Step 6 — Validate ✅

After ~30 seconds, look for this in Bob's terminal:

```
💤 Idle (1 peers), best: #...
```

**`1 peers` = Alice and Bob found each other. Your P2P network is live!**

---

## 🐧 Ubuntu / Linux (native)

Same steps as WSL above — just open your terminal directly. No PowerShell needed.

### One-time setup

```bash
cd ~
mkdir -p portaldot && cd portaldot
wget https://github.com/portaldotVolunteer/Portaldot-node/raw/main/portaldot-testnet-ubuntu.tar.gz
tar -xzvf portaldot-testnet-ubuntu.tar.gz
cd portaldot-testnet-ubuntu
chmod +x portaldot_dev
```

### Start Alice

```bash
./portaldot_dev --dev --alice --name YOUR_NAME --base-path /tmp/alice
```

### Start Bob (new terminal tab)

```bash
cd ~/portaldot/portaldot-testnet-ubuntu
./portaldot_dev --dev --bob --name YOUR_NAME_BOB \
  --base-path /tmp/bob \
  --port 30334 \
  --rpc-port 9945 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/PASTE_ALICE_PEER_ID
```

---

## ☁️ GitHub Codespaces

> No installation needed — runs entirely in your browser.

### Step 1 — Open a Codespace

1. Go to [github.com/portaldotVolunteer/Portaldot-node](https://github.com/portaldotVolunteer/Portaldot-node)
2. Click **Code** → **Codespaces** → **Create codespace on main**
3. Wait for the environment to load

### Step 2 — Download and extract the node

In the Codespace terminal:

```bash
cd ~
wget https://github.com/portaldotVolunteer/Portaldot-node/raw/main/portaldot-testnet-ubuntu.tar.gz
tar -xzvf portaldot-testnet-ubuntu.tar.gz
cd portaldot-testnet-ubuntu
chmod +x portaldot_dev
```

### Step 3 — Start Alice

```bash
./portaldot_dev --dev --alice --name YOUR_NAME --base-path /tmp/alice
```

Copy the Peer ID from the logs.

### Step 4 — Open a second terminal

In Codespaces: click the `+` button in the terminal panel to open a new terminal tab.

```bash
cd ~/portaldot-testnet-ubuntu
./portaldot_dev --dev --bob --name YOUR_NAME_BOB \
  --base-path /tmp/bob \
  --port 30334 \
  --rpc-port 9945 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/PASTE_ALICE_PEER_ID
```

---

## 📱 Termux (Android Phone)

> You can run a Portaldot node from your Android phone!

### Step 1 — Install Termux

Download **Termux** from [F-Droid](https://f-droid.org/packages/com.termux/) (not Play Store — the Play Store version is outdated).

### Step 2 — Update packages

```bash
pkg update && pkg upgrade -y
pkg install wget tar -y
```

### Step 3 — Download the node

```bash
cd ~
wget https://github.com/portaldotVolunteer/Portaldot-node/raw/main/portaldot-testnet-ubuntu.tar.gz
tar -xzvf portaldot-testnet-ubuntu.tar.gz
cd portaldot-testnet-ubuntu
chmod +x portaldot_dev
```

### Step 4 — Start Alice

```bash
./portaldot_dev --dev --alice --name YOUR_NAME --base-path /tmp/alice
```

### Step 5 — Start Bob in a new Termux session

Swipe from the left edge to open the Termux sidebar → tap **New Session**

```bash
cd ~/portaldot-testnet-ubuntu
./portaldot_dev --dev --bob --name YOUR_NAME_BOB \
  --base-path /tmp/bob \
  --port 30334 \
  --rpc-port 9945 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/PASTE_ALICE_PEER_ID
```

> 📝 Note: Keep your phone screen on and plugged in while running nodes.

---

## 💻 PowerShell (Windows only)

> Use this if you can't install WSL.

PowerShell doesn't run Linux binaries natively. The easiest path is to use **GitHub Codespaces** (browser-based) instead.

Alternatively, enable WSL with:

```powershell
wsl --install
```

Then follow the [Windows WSL2 guide](#-windows-wsl2-ubuntu) above.

---

## 🔧 Common Fixes

### Lock file error
```
Error: While lock file: .../LOCK: Resource temporarily unavailable
```
**Fix:**
```bash
rm /tmp/alice/chains/dev/db/LOCK
# or for bob:
rm /tmp/bob/chains/dev/db/LOCK
```

### Port already in use
```
Error: Address already in use
```
**Fix:** Kill the existing process and restart:
```bash
pkill portaldot_dev
```

### Node not finding peers (0 peers)
- Make sure Alice is running before starting Bob
- Double-check you pasted the correct Peer ID
- Wait up to 60 seconds — peer discovery takes time

### wget not found (Termux)
```bash
pkg install wget -y
```

### Permission denied
```bash
chmod +x portaldot_dev
```

---

## 📸 Screenshot Requirement

The Portaldot team requires **your username to appear in the node name** to verify your contribution. Generic screenshots will not be accepted.

Make sure your command includes your actual username:

```bash
# ✅ Correct — username visible in node name
./portaldot_dev --dev --alice --name investorquab --base-path /tmp/alice

# ❌ Wrong — generic name not accepted
./portaldot_dev --dev --alice --name YOUR_NAME --base-path /tmp/alice
```

Take a screenshot showing `💤 Idle (1 peers)` with **your username** visible in the logs.

---

## 🌐 View Your Node in the Browser

1. Open [polkadot.js.org/apps](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer)
2. It connects to Alice at `127.0.0.1:9944` automatically
3. You should see blocks being produced in real time ✅

Or use the **Portaldot Developer Playground**:
👉 [portaldot-playground.vercel.app](https://portaldot-playground.vercel.app)

---

## 🏆 Report Your Node

Found a bug? Want your contribution counted? Submit here:

👉 [Portaldot Notion Bug Report](https://www.notion.so/Portaldot-Local-Development-Node-Installation-Guide-on-Windows-via-WSL2-2e06bdef409680618bf6dbcaa1423508)

Include:
- Your wallet address
- Screenshot showing `1 peers` with your username in the node name
- Any bugs or issues you encountered

---

## ✅ Quick Reference

| Node | Command flag | Port | RPC |
|------|-------------|------|-----|
| Alice (bootnode) | `--alice` | 30333 | 9944 |
| Bob (peer) | `--bob` | 30334 | 9945 |

**Key rule:** Alice must start first. Bob connects to Alice using her Peer ID.

---

*Built by the Portaldot volunteer community · [Developer Playground](https://portaldot-playground.vercel.app) · [GitHub](https://github.com/Investorquab/portaldot-playground)*
