# 🔐 Website Fraud Detector

A Python-based CLI tool that analyzes URLs for fraud, phishing, and security risks using static analysis + AI (Groq - Llama 3.3 70B).



## 🎯 What It Does

Ever received a suspicious link? This tool instantly tells you if a website is safe or a potential fraud — combining rule-based static checks with AI-powered analysis.

- ✅ Detects phishing keywords in URLs
- ✅ Identifies temporary tunnels used by attackers (ngrok, Cloudflare tunnels, etc.)
- ✅ Checks for suspicious domain extensions (.xyz, .tk, .ml, .cf, etc.)
- ✅ Detects IP-based domains (a classic hacker trick)
- ✅ Flags unencrypted HTTP connections
- ✅ Gives a **Safety Score (0–100)** with color-coded terminal output
- ✅ **AI verdict** powered by Groq (Llama 3.3 70B) explaining risks in plain English

---

## 📸 Demo

```
╔══════════════════════════════════════════╗
║      Website Fraud Detector v3.0         ║
║       Powered by Static Checks + Groq    ║
╚══════════════════════════════════════════╝

  Enter URL to analyze: https://precision-hang-succeed-purple.trycloudflare.com

  Analyzing precision-hang-succeed-purple.trycloudflare.com...
  Getting AI analysis from Groq...

  ───────────────────────────────────────────────────────
  URL     : https://precision-hang-succeed-purple.trycloudflare.com
  Domain  : precision-hang-succeed-purple.trycloudflare.com
  ───────────────────────────────────────────────────────

  Safety Score : 19/100  —  High Risk ✘
  █████░░░░░░░░░░░░░░░░░░░░░░░░░

  Check                  Result                              Status
  ─────────────────────────────────────────────────────────────────
  HTTPS                  Secure (HTTPS)                      ✔ SAFE
  Domain Extension       .com — normal                       ✔ SAFE
  Tunnel / Proxy         Temporary tunnel detected!          ✘ RISK
  Phishing Keywords      None found                          ✔ SAFE
  IP as Domain           Normal domain name                  ✔ SAFE
  Special Characters     Clean domain                        ✔ SAFE
  Excessive Dashes       3 dashes — suspicious               ⚠ WARN
  Domain Length          47 chars — very long!               ⚠ WARN

  ───────────────────────────────────────────────────────
  AI Analysis (Groq — Llama 3.3 70B):
  → This URL is highly suspicious and should be avoided.
  → It uses a temporary Cloudflare tunnel, commonly misused for phishing.
  → Do not enter any personal data, passwords, or allow camera/location access.
```

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Language | Python 3.8+ |
| AI Model | Groq — Llama 3.3 70B (Free) |
| Terminal UI | Colorama |
| Analysis | Regex + Rule-based engine |
| Platform | Windows / Linux / Mac |

---

## ⚡ Installation

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/website-fraud-detector.git
cd website-fraud-detector
```

### 2. Install dependencies
```bash
pip install groq colorama
```

### 3. Get a FREE Groq API Key
- Go to [console.groq.com](https://console.groq.com)
- Sign in with Google
- Click **API Keys** → **Create API Key**
- Copy your key (`gsk_...`)

### 4. Add your API key
Open `urlanalyzer.py` and replace line 16:
```python
GROQ_API_KEY = "gsk_your_key_here"
```

### 5. Run the tool
```bash
python urlanalyzer.py
```

Or pass URL directly:
```bash
python urlanalyzer.py https://suspicious-site.com
```

---

## 🔍 How It Works

```
URL Input
   ↓
Static Analysis Engine
   ├── HTTPS Check         (weight: 20)
   ├── TLD Check           (weight: 15)
   ├── Tunnel Detection    (weight: 25)
   ├── Phishing Keywords   (weight: 15)
   ├── IP Domain Check     (weight: 10)
   ├── Special Characters  (weight:  5)
   ├── Excessive Dashes    (weight:  5)
   └── Domain Length       (weight:  5)
         ↓
   Safety Score (0–100)
         ↓
   Groq AI Analysis (Llama 3.3 70B)
         ↓
   Final Verdict + Precautions
```

---

## 🔎 Checks Explained — What Each Check Means

| Check | ON ✅ (Safe) | OFF ❌ (Risky) |
|---|---|---|
| **HTTPS** | Site uses encrypted connection | Site uses plain HTTP — data can be stolen |
| **Domain Extension** | Normal TLD like .com .in .org | Suspicious TLD like .xyz .tk .ml .cf — often used in fraud |
| **Tunnel / Proxy** | Normal permanent domain | Temporary tunnel (ngrok, Cloudflare) — hacker tool to hide identity |
| **Phishing Keywords** | No suspicious words in URL | Words like "login", "verify", "bank", "wallet" found — classic phishing |
| **IP as Domain** | Proper domain name used | Raw IP address used (e.g. 192.168.1.1) — real sites never do this |
| **Special Characters** | Clean domain name | Weird characters in domain — used to visually trick users |
| **Excessive Dashes** | 0–2 dashes in domain | 3+ dashes — fake sites use this (e.g. secure-bank-login.com) |
| **Domain Length** | Short, readable domain | Very long domain (30+ chars) — used to hide real destination |

> **Pro Tip:** Even if a site scores Safe, always verify the domain exactly matches the brand. Typosquatting (e.g. arnazon.com instead of amazon.com) may not be caught automatically.

---

## 📊 Score Interpretation

| Score | Verdict | Meaning |
|---|---|---|
| 75 – 100 | 🟢 Likely Safe | No major red flags found |
| 45 – 74 | 🟡 Suspicious | Multiple warning signs — be cautious |
| 0 – 44 | 🔴 High Risk | Serious red flags — avoid this site |

---

## ⚠️ Security Note

**Never hardcode your API key in public code.**
Use environment variables instead:

```python
import os
GROQ_API_KEY = os.getenv("GROQ_API_KEY")
```

Then set it in terminal:
```bash
# Windows
set GROQ_API_KEY=gsk_your_key_here

# Linux/Mac
export GROQ_API_KEY=gsk_your_key_here
```

---

## 🚀 Future Plans

- [ ] Bulk URL scanning from CSV file
- [ ] VirusTotal API integration
- [ ] WHOIS domain age checker
- [ ] Email/SMS phishing text analyzer
- [ ] Export report as PDF

---

## 👨‍💻 About

Built by **Shivam Prajapati**
BCA Student @ IMS Ghaziabad | Cybersecurity Enthusiast

- 🔗 [LinkedIn](www.linkedin.com/in/shivam-prajapati-923923312)
- 💻 [GitHub](https://github.com/shiwvam)

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

⭐ If you found this useful, give it a star!
