# 🦉 OCrypt

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-0a0c10?style=flat-square"/>
  <img src="https://img.shields.io/badge/Category-OCipher-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/License-Proprietary-orange?style=flat-square"/>
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

This tool is part of the **OwlSec** suite — a collection of 275+ security and privacy tools.

🔗 [owlsec.org](https://owlsec.org)

---

## ©️ License

Proprietary — © 2026 Owlsec LLC. All rights reserved.

*Tools are distributed as pre-built executables. Source code is proprietary.*

---

## 🔍 Verification & Transparency

This tool is closed-source. These files let you see exactly what is inside it,
without the source:

- [`SBOM.cdx.json`](SBOM.cdx.json) — CycloneDX inventory: SHA-256 of this
  binary, bundled CPython version, and every bundled library with its exact
  version and license. Feed it to Grype, Trivy or Dependency-Track to audit
  our dependencies for CVEs yourself.
- [`THIRD-PARTY-NOTICES.md`](THIRD-PARTY-NOTICES.md) — the full license text
  of every third-party component, extracted from this binary.

**No telemetry, no analytics, no licence check-in.** This tool does not phone
home. Verify that claim yourself:

```bash
sudo strace -f -e trace=network ./OCrypt --help   # watch every network call
firejail --net=none ./OCrypt --help               # deny the network entirely
```

Release signing, GPL compliance and vulnerability reporting:
[**TRUST.md**](https://github.com/owlsecx/owl-os/blob/main/TRUST.md)
