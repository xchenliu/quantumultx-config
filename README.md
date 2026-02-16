# Quantumult X Configuration

> **sliu's Ultimate Enterprise Edition** - A comprehensive Quantumult X configuration featuring DNS isolation, AI service routing, streaming media optimization, and ad blocking.

## Features

### DNS Isolation
- Domestic sites (Taobao, JD, QQ, Bilibili, etc.) resolve via Alibaba/Tencent DNS (`223.5.5.5` / `119.29.29.29`)
- International sites (Google, AI services, social media) resolve via Google DNS (`8.8.8.8`)

### AI Service Routing
Each AI service has its own dedicated policy to avoid interference:

| Service | Policy | Default Region |
|---------|--------|----------------|
| ChatGPT / OpenAI | AI-US | Singapore |
| Claude / Anthropic | Claude | Singapore |
| Gemini | AI-US | US |
| Grok | AI-US | US |
| DeepSeek | AI-US | Singapore |
| Perplexity | AI-US | Singapore |
| Copilot | AI-US | Singapore |

### Streaming & Social Media
Independent policy groups with region selection for each service:
- **Streaming**: YouTube, Netflix, Spotify
- **Social**: Twitter/X, Facebook, Instagram, Reddit
- **Communication**: Telegram, WhatsApp, Discord
- **Development**: GitHub

### Ad Blocking
- Remote rule lists from [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- Local keyword-based fallback rules (active even when remote lists fail)

### Other
- **Apple / Microsoft**: Default DIRECT, switchable to proxy
- **Gaming**: Low-latency auto-select for Asia nodes (HK/JP/SG)
- **China**: DIRECT via GeoIP + ChinaMax rule list
- **Final fallback**: Global proxy

---

## Policy Group Architecture

```
Global (Auto / US / HK / JP / SG / TW / DIRECT)
  |
  |-- AI-US ........... ChatGPT, Gemini, Grok, DeepSeek, Perplexity, Copilot
  |-- AI-API .......... OpenAI API calls
  |-- Claude .......... Claude / Anthropic
  |
  |-- YouTube ......... YouTube + CDN
  |-- Netflix ......... Netflix
  |-- Spotify ......... Spotify
  |-- Media ........... Other streaming
  |
  |-- Twitter ......... Twitter / X
  |-- Facebook ........ Facebook
  |-- Instagram ....... Instagram
  |-- Reddit .......... Reddit
  |-- Discord ......... Discord
  |-- GitHub .......... GitHub
  |
  |-- Telegram ........ Telegram
  |-- WhatsApp ........ WhatsApp + IP-CIDR
  |-- Google .......... Google services
  |-- Apple ........... Apple (default DIRECT)
  |-- Microsoft ....... Microsoft (default DIRECT)
  |
  |-- Asia-LowLatency . Gaming (auto low-latency)
  |-- China ........... Domestic (DIRECT)
  |-- Advertising ..... Ad blocking (REJECT)
  |-- Privacy ......... Privacy tracking (REJECT)
  |-- Final ........... Fallback (Global / DIRECT)
```

---

## How to Import / Usage

### Step 1: Open Settings

Open Quantumult X, tap the **wind-vane icon** at the bottom-right corner to enter the settings page.

<img src="images/01-main-page.png" width="300">

### Step 2: Edit Profile

Tap the **link icon** at the top-right, then select **Edit** to open the configuration editor.

<img src="images/02-edit-profile.png" width="300">

### Step 3: Paste Configuration

**Clear the existing content**, then paste the entire configuration from [`QuantumultX.conf`](QuantumultX.conf). Tap the **checkmark** at the top-right to save.

<img src="images/03-paste-config.jpg" width="300">

### Step 4: Replace Subscription Link

Find this line in `[server_remote]`:

```
换成自己的订阅链接🔗,tag=Nodes,update-interval=172800,opt-parser=true,enabled=true
```

Replace `换成自己的订阅链接🔗` with your actual subscription URL.

### Step 5: Enable MitM (Optional)

If you need rewrite/MitM features, go to **MitM** section in settings and generate & install the CA certificate.

---

## Rule Priority

Rules are evaluated in the following order (highest priority first):

1. **Local rules** (`[filter_local]`) - AI, WhatsApp, YouTube, social media anti-hijack rules
2. **Remote rules** (`[filter_remote]`) - Comprehensive rule lists from blackmatrix7
3. **GeoIP CN** - Domestic traffic direct
4. **Final** - Everything else goes through Global proxy

---

## Credits

- Rule lists: [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- Icons: [Koolson/Qure](https://github.com/Koolson/Qure)
- Resource parser: [KOP-XIAO/QuantumultX](https://github.com/KOP-XIAO/QuantumultX)

## License

MIT
