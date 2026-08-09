# SeedCryptor 16B / 32B 🔐

A lightweight, zero-dependency, single-file client-side tool for encrypting existing cryptocurrency seed entropy into a secure Base58 text backup[span_0](start_span)[span_0](end_span). Designed for offline use, it encrypts raw hex entropy (16-byte / 12 words or 32-byte / 24 words) using native WebCrypto API[span_1](start_span)[span_1](end_span).

---

## ⚠️ Critical Security Warnings

* **Not Audited:** This project is educational and has not undergone a formal security audit[span_2](start_span)[span_2](end_span).
* **Strictly Offline:** Run this tool exclusively in an air-gapped browser environment[span_3](start_span)[span_3](end_span).
* **No Seed Generation:** This tool does NOT generate new seed phrases; it only encrypts your existing entropy[span_4](start_span)[span_4](end_span).

---

## 🔄 Workflow (Words ↔ Hex)

SeedCryptor operates directly on raw entropy hex[span_5](start_span)[span_5](end_span). Converting between mnemonic words and hex is done offline using a trusted tool like `iancoleman.io/bip39`[span_6](start_span)[span_6](end_span).

### 1. Encrypting a Seed
* **Extract Hex:** Open `iancoleman.io/bip39` strictly offline[span_7](start_span)[span_7](end_span). Enter your mnemonic phrase to view the **Entropy hex** (32 characters for 12 words / 16B, or 64 characters for 24 words / 32B)[span_8](start_span)[span_8](end_span).
* **Encrypt:** Paste the hex into the corresponding tab in SeedCryptor, enter a password (>= 8 characters), and generate your Base58 backup block[span_9](start_span)[span_9](end_span).

### 2. Decrypting a Seed
* **Decrypt Hex:** Paste your Base58 backup block into SeedCryptor and enter your password to reveal the original 32 or 64-character hex[span_10](start_span)[span_10](end_span).
* **Restore Words:** Open `iancoleman.io/bip39` offline, navigate to the **Entropy** section, paste your decrypted hex, and generate your mnemonic words[span_11](start_span)[span_11](end_span).

---

## 🛠️ Technical & Cryptographic Specifications

| Parameter | Specification |
| :--- | :--- |
| **KDF** | PBKDF2-HMAC-SHA256 (600,000 iterations, 256-bit key)[span_12](start_span)[span_12](end_span) |
| **Encryption** | AES-GCM 256[span_13](start_span)[span_13](end_span) |
| **Encoding** | Base58 (`123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz`)[span_14](start_span)[span_14](end_span) |
| **Dependencies** | Pure WebCrypto API + Vanilla JS (Zero external libraries)[span_15](start_span)[span_15](end_span) |
| **Network Access** | None (Fully air-gapped execution)[span_16](start_span)[span_16](end_span) |

### Binary Payload Structure (Base58 Decoded)
* `[0 : 16]` — Salt (16 bytes)[span_17](start_span)[span_17](end_span)
* `[16 : 28]` — Initialization Vector / IV (12 bytes)[span_18](start_span)[span_18](end_span)
* `[28 : end]` — Ciphertext + Auth Tag (16 bytes)[span_19](start_span)[span_19](end_span)

---

## 🚀 How to Run

1. Save `index.html` to an offline storage device (e.g., USB drive).
2. Open `index.html` in any modern web browser on an air-gapped machine[span_20](start_span)[span_20](end_span).
3. Select either **16 BYTE (12 words)** or **32 BYTE (24 words)** tab to begin[span_21](start_span)[span_21](end_span).
