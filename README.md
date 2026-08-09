# SeedCryptor 16B / 32B 🔐

A lightweight, zero-dependency, single-file client-side tool for encrypting existing cryptocurrency seed entropy into a secure Base58 text backup. Designed for offline use, it encrypts raw hex entropy (16-byte / 12 words or 32-byte / 24 words) using native WebCrypto API.

---

## ⚠️ Critical Security Warnings

* **Not Audited:** This project is educational and has not undergone a formal security audit.
* **Strictly Offline:** Run this tool exclusively in an air-gapped browser environment.
* **No Seed Generation:** This tool does NOT generate new seed phrases; it only encrypts your existing entropy.

---

## 🔄 Workflow (Words ↔ Hex)

SeedCryptor operates directly on raw entropy hex. Converting between mnemonic words and hex is done offline using a trusted tool like `iancoleman.io/bip39`.

### 1. Encrypting a Seed
* **Extract Hex:** Open `iancoleman.io/bip39` strictly offline. Enter your mnemonic phrase to view the **Entropy hex** (32 characters for 12 words / 16B, or 64 characters for 24 words / 32B).
* **Encrypt:** Paste the hex into the corresponding tab in SeedCryptor, enter a password (>= 8 characters), and generate your Base58 backup block.

### 2. Decrypting a Seed
* **Decrypt Hex:** Paste your Base58 backup block into SeedCryptor and enter your password to reveal the original 32 or 64-character hex.
* **Restore Words:** Open `iancoleman.io/bip39` offline, navigate to the **Entropy** section, paste your decrypted hex, and generate your mnemonic words.

---

## 🛠️ Technical & Cryptographic Specifications

| Parameter | Specification |
| :--- | :--- |
| **KDF** | PBKDF2-HMAC-SHA256 (600,000 iterations, 256-bit key) |
| **Encryption** | AES-GCM 256 |
| **Encoding** | Base58 (`123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz`) |
| **Dependencies** | Pure WebCrypto API + Vanilla JS (Zero external libraries) |
| **Network Access** | None (Fully air-gapped execution) |

### Binary Payload Structure (Base58 Decoded)
* `[0 : 16]` — Salt (16 bytes)
* `[16 : 28]` — Initialization Vector / IV (12 bytes)
* `[28 : end]` — Ciphertext + Auth Tag (16 bytes)

---

## 🚀 How to Run

1. Save `index.html` to an offline storage device (e.g., USB drive).
2. Open `index.html` in any modern web browser on an air-gapped machine.
3. Select either **16 BYTE (12 words)** or **32 BYTE (24 words)** tab to begin.

