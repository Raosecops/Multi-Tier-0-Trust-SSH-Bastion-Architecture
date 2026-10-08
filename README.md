# Multi-Tier 0 Trust SSH Bastion Architecture

A production-grade network segmentation and host hardening lab built on Ubuntu 22.04 using Multipass.
 This project demonstrates defense-in-depth security by isolating internal production workloads behind a hardened, Zero-Trust SSH bastion gateway.

## 🏗️ Architecture Overview
* **Bastion Gateway (`bastion`)**:
 The sole public/edge entry point enforcing key-only authentication, UFW ingress rules, and Fail2Ban brute-force monitoring.
* **Production Tier (`prd-euw`)**:
 An isolated internal server with **zero direct public exposure**, reachable exclusively via secure multi-hop SSH tunneling (`ProxyJump` with `ForwardAgent`).

[ Client / Operator ]
│
▼ (SSH Port 22 - Key Only)
┌────────────────────────┐
│   Bastion Gateway      │ (Public/Edge Tier)
└──────────┬─────────────┘
│
▼ (Internal Network / ProxyJump + ForwardAgent)
┌────────────────────────┐
│   prd-euw              │ (Isolated Internal Tier)
└────────────────────────┘

## 🔒 Implemented Security Controls
* **Cryptographic Enforcement**: Disabled password authentication (`PasswordAuthentication no`) and root logins globally.
* **Perimeter Defense**: Strict UFW ingress filtering and Fail2Ban active SSH jail monitoring.
* **Seamless Traversal**: Configured native OpenSSH `ProxyJump` and agent forwarding.

## Brute-Force Attack proof Surface

* ** Tested the Architecture with Multiple Brute-Force Attacks, system remained un-touched.
