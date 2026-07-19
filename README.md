````markdown
# AGORA3

### OffGrid PIX Payment Framework for LoRa Mesh Networks

**AGORA3** is an open-source research framework exploring how **Brazil's PIX payment ecosystem** can be integrated with **LoRa mesh communications** to enable payment requests in environments with limited or intermittent Internet connectivity.

The project investigates a hybrid architecture where a LoRa radio transports **payment instructions**, while an Internet-connected gateway securely interacts with participating Brazilian banks' official APIs.

> **AGORA3 is an experimental engineering project. It is not a financial institution, payment processor, or banking service.**

---

# Vision

Modern payment systems assume continuous Internet connectivity.

AGORA3 explores a resilient architecture where:

- LoRa carries payment requests over long distances
- Mesh networks extend communication coverage
- A trusted gateway performs authenticated API calls
- Payment confirmations are transmitted back through the radio network

The objective is to improve resilience for:

- rural communities
- farms
- disaster recovery
- outdoor events
- remote research stations
- community mesh networks
- emergency communications

---

# Project Goals

AGORA3 investigates:

- PIX over LoRa
- Offline payment requests
- Mesh networking
- Local-first payment infrastructure
- Secure gateway authentication
- Open-source embedded hardware
- Energy-efficient payment terminals

---

# System Overview

```
┌───────────────────────┐
│ Merchant Cardputer    │
│ M5 Cardputer Zero     │
│                       │
│ Amount                │
│ PIX Key               │
│ Merchant ID           │
└────────────┬──────────┘
             │
        LoRa Packet
             │
             ▼
┌───────────────────────┐
│ LoRa Gateway          │
│ Raspberry Pi          │
│ ESP32 Gateway         │
│ Linux Server          │
└────────────┬──────────┘
             │
      HTTPS + OAuth
             │
             ▼
┌───────────────────────┐
│ Brazilian Bank API    │
│ Official PIX API      │
└────────────┬──────────┘
             │
      Payment Result
             │
             ▼
 Confirmation via LoRa
```

---

# Proposed Hardware

## Payment Terminal

- M5 Cardputer
- M5 Cardputer Zero (future concept)
- ESP32
- SX1262 LoRa Module
- Battery powered

Functions:

- enter payment amount
- choose merchant
- generate request
- encrypt payload
- transmit over LoRa

---

## Gateway

Possible hardware:

- Raspberry Pi
- Mini PC
- Linux server
- ESP32 Ethernet Gateway

Responsibilities:

- receive LoRa packets
- verify signatures
- authenticate with bank
- call PIX API
- send confirmation back

---

# Why LoRa?

Advantages include:

- several kilometers of range
- extremely low power consumption
- inexpensive hardware
- license-free spectrum
- ideal for rural deployments

Potential applications:

- farms
- festivals
- emergency response
- isolated communities
- backup communication

---

# Banking APIs

AGORA3 is designed around official Open Finance and PIX APIs provided by Brazilian financial institutions.

Potential integrations include:

- Banco do Brasil
- Caixa Econômica Federal
- Itaú Unibanco
- Bradesco
- Santander Brasil
- Sicredi
- Sicoob
- BTG Pactual
- Inter
- C6 Bank
- Nubank (if and when suitable public APIs become available)
- Banco Central do Brasil Open Finance ecosystem

Support depends entirely on each institution's published developer APIs, authentication methods, and terms of service.

---

# Security Model

The payment terminal **never stores banking credentials**.

Instead:

- OAuth tokens remain only on the gateway
- API secrets remain only on the gateway
- Device identities use public/private keys
- LoRa packets are digitally signed
- Every packet contains:
  - timestamp
  - nonce
  - device ID
  - signature
- Replay protection
- End-to-end encryption for payment requests

---

# Example Flow

1. Merchant enters payment amount.
2. Customer confirms the transaction request.
3. The Cardputer signs and encrypts the request.
4. The request is transmitted via LoRa.
5. A trusted gateway receives and validates it.
6. The gateway calls the bank's official PIX API.
7. The bank processes the payment.
8. The gateway receives the response.
9. Confirmation is sent back over LoRa.
10. The terminal displays the payment status.

---

# Network Architecture

```
Cardputer
      │
      ▼
LoRa Mesh
      │
      ▼
Gateway
      │
 HTTPS
      │
      ▼
Bank API
      │
      ▼
PIX Network
```

---

# Software Stack

Embedded

- ESP-IDF
- Arduino Framework
- FreeRTOS

Gateway

- Go
- Rust
- Python
- Node.js

Communication

- LoRa
- Meshtastic-inspired routing concepts
- MQTT (optional)
- HTTPS
- REST APIs

Security

- TLS
- OAuth2
- Device certificates
- Ed25519 signatures
- AES-256 encrypted payloads

---

# Repository Structure

```
firmware/
    cardputer/

gateway/
    api-client/
    lora-service/
    auth/

protocol/
    packet-specification/
    encryption/

docs/
    architecture/
    hardware/
    security/

examples/

simulations/
```

---

# Possible Future Features

- QR Code fallback
- NFC support
- Bluetooth provisioning
- Wi-Fi fallback
- Satellite gateway integration
- Solar-powered relay stations
- Multi-bank support
- Offline transaction queue
- Mesh routing optimization
- Remote firmware updates

---

# Research Topics

- LoRa latency
- Packet fragmentation
- Secure key exchange
- Offline authentication
- Gateway redundancy
- Mesh routing
- Power optimization
- Cryptographic signing
- Rural communication reliability

---

# Limitations

AGORA3 **does not** make PIX itself operate offline.

Instead, it explores an architecture where:

- payment instructions travel over LoRa,
- a connected gateway performs the online banking transaction,
- confirmations are relayed back through the mesh.

An Internet-connected gateway is still required for final settlement with the banking system.

---

# Intended Applications

- Remote farms
- Community markets
- Outdoor events
- Emergency communications
- Disaster recovery
- Scientific expeditions
- Rural commerce
- Educational research
- IoT payment experiments

---

# Roadmap

- [ ] LoRa packet specification
- [ ] Cryptographic protocol
- [ ] Cardputer firmware
- [ ] Gateway implementation
- [ ] PIX API abstraction layer
- [ ] Multi-bank adapter interface
- [ ] Mesh routing support
- [ ] End-to-end encryption
- [ ] Simulation environment
- [ ] Hardware reference designs
- [ ] Developer documentation

---

# Contributing

Contributions are welcome in areas such as:

- Embedded systems
- ESP32 development
- LoRa networking
- Cryptography
- Open Finance
- API integrations
- Security reviews
- Documentation
- Hardware design
- Testing

---

# Legal Notice

AGORA3 is an open-source research project.

It is **not**:

- a bank
- a payment institution
- a financial intermediary
- a PIX provider

Users and implementers are solely responsible for complying with applicable laws, banking regulations, API licensing terms, and security requirements.

---

# License

MIT License

---

# AGORA3

> **Resilient payments. Open hardware. Mesh networking. Secure gateways.**
>
> **Building the future of resilient payment infrastructure, one packet at a time.**
````
