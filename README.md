# 🦉 OCrypt

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-0a0c10?style=flat-square"/>
  <img src="https://img.shields.io/badge/Category-OCipher-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square"/>
  <img src="https://img.shields.io/badge/Part%20of-OwlSec%20Toolkit-7b5ea7?style=flat-square"/>
  <img src="https://img.shields.io/badge/Version-1.0.0-cyan?style=flat-square"/>
</p>

> **OCrypt** — Modern encryption and public-key seal

---

> ⚠️ **AUTHORISED USE ONLY** — Use only on systems you own or have explicit written permission to test. Unauthorised use is illegal.

---

## 📌 Overview

OCrypt provides modern symmetric encryption and public-key sealing for files and text. Passwords are stretched with PBKDF2-SHA256, and seal mode wraps a random AES-256 data key with RSA-OAEP so a public key can protect arbitrary-size content. Keys and exports live under a dedicated data directory rather than the working folder.

---

## ✨ Features

- Password-based encryption with PBKDF2-SHA256 key stretching
- AES-256-GCM authenticated encryption for local secrets
- RSA-OAEP seal/open for text and files of any size
- Dedicated key and export storage under ~/.local/share/ocrypt
- CLI seal/open paths for automation alongside interactive use
- Clear separation of public seal versus private open operations

---

## ⚙️ Requirements

- **Linux**
- **No Python installation needed** — runs as a standalone executable

---

## 🚀 Usage

```bash
./OCrypt --seal-text --public pubkey.pem --text 'secret message'
./OCrypt --open-text --private privkey.pem --text '<sealed-blob>'
./OCrypt --seal-file --public pubkey.pem --in report.pdf --out report.seal
./OCrypt --help
```

---

## 📦 Part of OwlSec Toolkit

This tool is part of the **OwlSec** suite — a collection of 300+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

MIT License — © Khaled S. Haddad

*Tools are distributed as pre-built executables. Source code is proprietary.*
