# QuantumShield 🛡️

**Next-Generation AI-Powered Honeypot & ML Firewall**

QuantumShield is an advanced cybersecurity defense system that sits in front of your web applications. Unlike traditional WAFs that simply block attacks, QuantumShield uses machine learning to detect threats and redirects attackers to a highly realistic, LLM-powered honeypot to gather intelligence while protecting your real infrastructure.

## Problem Statement

Modern web applications face increasingly sophisticated attacks that bypass rule-based defenses:

- **Zero-Day Exploits**: Novel attacks that signature-based WAFs miss.
- **Automated Scanning**: Relentless probing by bots and scripts.
- **Lack of Intelligence**: Blocking an IP provides no insight into the attacker's intent or methodology.
- **False Positives**: Legitimate users often get blocked by rigid rules.

**The Solution:** We need a system that adapts to threats, deceives attackers to waste their time, and learns from every interaction.

## Solution Overview

QuantumShield acts as a smart reverse proxy. It analyzes every incoming request using ML models trained on attack payloads.

- **Safe Traffic** is forwarded seamlessly to your application.
- **Suspicious Traffic** is quietly routed to a realistic honeypot (without the attacker knowing).
- **Malicious Traffic** is blocked with a progressive counter system.

### Architecture Diagram

[System Architecture Diagram Placeholder]

## User Flow

How a request travels through the system:

### Request Flow Diagram

[User/Request Flow Diagram Placeholder]

## Key Components

### 1. ML Firewall 🧠

The first line of defense.

- **SQLi & NoSQLi Detection**: Uses DistilBERT models to understand the semantic meaning of payloads, catching attacks that regex misses.
- **Confidence Scoring**: Assigns a threat score (0-1) to every request.
- **Smart Routing**: Decides whether to Forward, Trap, or Block based on confidence thresholds.

### 2. Adaptive Honeypot 🍯

A dynamic deception engine.

- **LLM-Powered Responses**: Uses Groq (LLM) to generate realistic HTML and JSON responses on the fly.
- **Context Awareness**: If an attacker asks for `/api/users`, the honeypot generates a believable list of fake users.
- **No 404s**: Trapped attackers never hit a dead end; the system hallucinates valid responses to keep them engaged.

### 3. Counter-Based Blocking 🛡️

A progressive response system.

- **Warning System**: Attackers get 5 chances before a permanent IP ban.
- **Persistence**: Blocks and traps survive server restarts (backed by MongoDB).

### 4. Live Dashboard 📊

Real-time visibility.

- **Live Feed**: Watch attacks happen in real-time.
- **Session Replay**: Analyze exactly what trapped attackers tried to do.

## Tools & Technologies

**Backend & AI**

- **Python / FastAPI**: High-performance async gateway.
- **Scikit-learn / XGBoost**: ML for traffic analysis.
- **Transformer Models**: DistilBERT for payload analysis.
- **Groq API**: Ultra-fast LLM inference for deception.

**Frontend & App**

- **Next.js / React**: For the dashboard and the vulnerable demo app (techshop).
- **Tailwind CSS**: For modern, responsive UI.

**Infrastructure**

- **MongoDB**: For storing logs, traps, and blocklists.
- **Docker**: For containerized deployment.

## Setup & Installation

### Prerequisites

- Python 3.9+
- Node.js 18+
- MongoDB

### Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/quantumshield.git
   ```

2. **Setup the Honeypot (Gateway)**

   ```bash
   cd honeypot
   pip install -r requirements.txt
   python main.py
   ```

3. **Setup the Dashboard & Demo App**

   ```bash
   cd frontend
   npm install && npm run dev
   ```

## Security Note

This project contains a **deliberately vulnerable application** (DVWA) for demonstration purposes. Do not expose the vulnerable component directly to the public internet without proper isolation.
