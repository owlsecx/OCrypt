# 🦉 OCrypt

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux%20%2F%20Windows-informational?style=flat-square&logo=linux&logoColor=white&color=0a0c10"/>
  <img src="https://img.shields.io/badge/Category-OCipher%20%2F%20Modern%20Encryption-cyan?style=flat-square"/>
  <img src="https://img.shields.io/badge/KDF-PBKDF2--SHA256%20%C2%B7%20200k%20rounds-blueviolet?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0-cyan?style=flat-square"/>
</p>

> **OCrypt** is a modern encryption tool — AES-256-CBC, AES-256-GCM, ChaCha20, Fernet, RSA, DES, and 3DES, all with PBKDF2-SHA256 password-based key derivation (200,000 iterations), plus a secure key and password generator.

---

## 📌 Overview

OCrypt wraps industry-standard symmetric and asymmetric ciphers behind a password prompt. Keys are never stored — every encryption derives a fresh key from the password using PBKDF2-SHA256 with a random salt. All ciphertext is serialised as Base64-encoded JSON payloads containing the salt, IV/nonce, and ciphertext — portable and self-contained.

---

## 🔐 Algorithms

| # | Algorithm | Type | Key Size | Notes |
|---|-----------|------|----------|-------|
| **[1] AES-256-CBC** | Symmetric block cipher | 256-bit | PKCS7 padding · 16-byte IV | ✅ Recommended |
| **[2] AES-256-GCM** | Authenticated symmetric | 256-bit | 16-byte nonce + auth tag | ✅ **Most recommended** — detects tampering |
| **[3] DES** | Legacy symmetric | 56-bit | ⚠️ Not secure for real use |
| **[4] 3DES** | Legacy symmetric | 168-bit | ⚠️ Legacy — prefer AES-256 |
| **[5] RSA** | Asymmetric | 2048 / 3072 / 4096-bit | PKCS1-OAEP padding · PEM key files |
| **[6] ChaCha20** | Modern stream cipher | 256-bit | 64-bit nonce | ✅ Fast, modern alternative to AES |
| **[7] Fernet** | Symmetric + HMAC | 128-bit AES | AES-128-CBC + HMAC-SHA256 | ✅ Simple and authenticated |
| **[8] Key Generator** | — | — | Keys, passwords, UUID v4 |

---

## 🔑 Key Derivation

All password-based modules use:

| Property | Value |
|----------|-------|
| Algorithm | PBKDF2-HMAC-SHA256 |
| Iterations | 200,000 |
| Salt | 16 bytes random (per operation) |
| Output key length | 32 bytes (AES-256, ChaCha20) · 24 bytes (3DES) · 8 bytes (DES) |

The salt is embedded in the ciphertext payload — decryption only requires the same password.

---

## 📦 Ciphertext Format

All symmetric outputs are self-contained Base64-encoded JSON:

| Algorithm | Payload Fields |
|-----------|---------------|
| AES-256-CBC | `salt` + `iv` + `ciphertext` |
| AES-256-GCM | `salt` + `nonce` + `tag` + `ciphertext` |
| DES / 3DES | `salt` + `iv` + `ciphertext` |
| ChaCha20 | `salt` + `nonce` + `ciphertext` |
| Fernet | `salt_b64` + `:` + Fernet token |

---

## 🔒 RSA Module

| Operation | Description |
|-----------|-------------|
| **Generate Key Pair** | Generates 2048/3072/4096-bit RSA keys — saved as `ocrypt_rsa_public_*.pem` and `ocrypt_rsa_private_*.pem` |
| **Encrypt** | PKCS1-OAEP encryption using a public key `.pem` file |
| **Decrypt** | PKCS1-OAEP decryption using a private key `.pem` file |

---

## 🔧 Key Generator

| Option | Output |
|--------|--------|
| **[1] Random hex key** | 128-bit, 192-bit, 256-bit hex strings |
| **[2] Random base64 key** | 128-bit, 256-bit base64 strings |
| **[3] Fernet key** | URL-safe base64 Fernet key |
| **[4] RSA key pair** | 2048-bit RSA PEM key pair saved to files |
| **[5] Secure password** | Configurable length — `a-Z` + `0-9` + `!@#$%^&*()-_=+` · strength rated WEAK/MEDIUM/STRONG |
| **[6] UUID v4 token** | Random UUID v4 |

---

## 📤 Export

After every operation:

| Option | Output |
|--------|--------|
| **[J] JSON** | `ocrypt_<algo>_YYYYMMDD_HHMMSS.json` — algorithm, mode, input, output |
| **[T] TXT** | `ocrypt_<algo>_YYYYMMDD_HHMMSS.txt` — same fields as plain text |
| **[L] Log** | Appended to `ocrypt_log.txt` with timestamp |
| **[N] No** | Skip export |

---

## 🛡️ Security Notes

- **AES-256-GCM** is the recommended choice — it encrypts and authenticates simultaneously, detecting any tampering on decryption
- **DES and 3DES** are included for legacy compatibility only — do not use for new projects
- **RSA keys** should be 2048 bits minimum; 4096 bits for long-term security
- **Never reuse IVs or nonces** — OCrypt generates a fresh random IV/nonce per encryption automatically
- The banner shows live `[✔]` / `[✘]` status for both required libraries on startup

---

## ⚙️ Requirements

- **Linux or Windows**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OCrypt
```

---

## 🔗 Companion Tools

| Tool | Role |
|------|------|
| **OClassic / OCipher** | Classical cipher encoding layer — use after OCrypt for extra obfuscation |
| **OSteg** | Steganographic hiding with optional AES-256 encryption |
| **OCrack** | Password and hash auditing |

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
