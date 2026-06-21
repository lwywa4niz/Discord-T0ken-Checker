<div align="center">

# Karenisme — Discord Token Checker

```
██╗  ██╗ █████╗ ██████╗ ███████╗███╗   ██╗██╗███████╗███╗   ███╗███████╗
██║ ██╔╝██╔══██╗██╔══██╗██╔════╝████╗  ██║██║██╔════╝████╗ ████║██╔════╝
█████╔╝ ███████║██████╔╝█████╗  ██╔██╗ ██║██║███████╗██╔████╔██║█████╗  
██╔═██╗ ██╔══██║██╔══██╗██╔══╝  ██║╚██╗██║██║╚════██║██║╚██╔╝██║██╔══╝  
██║  ██╗██║  ██║██║  ██║███████╗██║ ╚████║██║███████║██║ ╚═╝ ██║███████╗
╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚═╝  ╚═══╝╚═╝╚══════╝╚═╝     ╚═╝╚══════╝
```

**A fast, multi-threaded Discord token checker** with proxy support and detailed classification by status, account age, Nitro subscription, and server boosts.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?logo=windows&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

</div>

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/2728.svg" width="22" align="center"/> Features

- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/2705.svg" width="16"/> Checks tokens and classifies them as **Valid**, **Invalid**, **Locked**, or **Flagged**
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f510.svg" width="16"/> Verification type detection: `unclaimed`, `email verified`, `phone verified`, `fully verified`
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f382.svg" width="16"/> Account age sorting by months or years
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f48e.svg" width="16"/> Nitro detection with days remaining
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f680.svg" width="16"/> Available server boost slot detection
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f504.svg" width="16"/> HTTP proxy support with auto-rotation on rate limit
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/26a1.svg" width="16"/> Multi-threaded for high-speed checking (configurable thread count)
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f3a8.svg" width="16"/> Colorized console output with real-time title bar stats (Windows)
- <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f4c1.svg" width="16"/> Organized output files sorted by type, age, and boost count

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f4c1.svg" width="22" align="center"/> Project Structure

```
├── main.py
├── data/
│   ├── config.toml       # Main configuration (threads, proxyless mode)
│   ├── settings.json     # Feature toggles (flagged, type, age, nitro)
│   ├── tokens.txt        # Input tokens (one per line)
│   └── proxies.txt       # Proxy list (one per line, user:pass@host:port or host:port)
└── output/
    └── YYYY-MM-DD HH-MM-SS/
        ├── valid.txt
        ├── invalid.txt
        ├── locked.txt
        ├── flagged.txt
        ├── email verified.txt
        ├── phone verified.txt
        ├── fully verified.txt
        ├── age/
        │   └── {X months | X years}/
        │       └── {type}.txt
        └── boosts/
            └── {X days}/
                └── {Y boosts}.txt
```

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/2699.svg" width="22" align="center"/> Configuration

### `data/config.toml`

```toml
[main]
threads = 50        # Number of concurrent threads
proxyless = false   # Set to true to run without proxies
```

### `data/settings.json`

```json
{
  "flagged": true,
  "type": true,
  "age": true,
  "nitro": true
}
```

| Key | Description |
|-----|-------------|
| `flagged` | Detect and separate flagged accounts |
| `type` | Classify by verification type |
| `age` | Sort by account age |
| `nitro` | Detect Nitro subscriptions and boosts |

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f4cb.svg" width="22" align="center"/> Input Format

**`data/tokens.txt`** — One token per line. Supports both raw tokens and `email:password:token` format:

```
mfa.xxxxxxxxxxxxxxxx...
user@email.com:password:xxxxxxxxxxxxxxxx...
```

**`data/proxies.txt`** — One proxy per line:

```
host:port
user:password@host:port
```

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f680.svg" width="22" align="center"/> Installation & Usage

### Requirements

- Python 3.8+

### Install dependencies

```bash
pip install tls-client colorama toml
```

### Run

```bash
python main.py
```

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f4ca.svg" width="22" align="center"/> Console Output

The checker displays real-time colored logs for each token:

| Status | Description |
|--------|-------------|
| `[VALID]` | Token is active and usable |
| `[INVALID]` | Token is expired or incorrect |
| `[LOCKED]` | Account has been locked by Discord |
| `[FLAGGED]` | Account is flagged (spammer flag detected) |
| `[RATE LIMITED]` | Too many requests — proxy rotated automatically |

Each valid token log displays: `token` · `username` · `user ID` · `guild count` · `age` · `nitro` · `boosts`

**Windows title bar** updates in real-time with:

```
Token Checker - Valid: X | Invalid: X | Locked: X | Flagged: X | Remaining: X | Progress: XX.XX% | CPM: X
```

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f4e4.svg" width="22" align="center"/> Output

Results are saved to a timestamped folder under `output/` after each run. Files are automatically created only when tokens of that category are found.

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/26a0.svg" width="22" align="center"/> Disclaimer

This tool is provided for **educational purposes only**. Using this tool may violate [Discord's Terms of Service](https://discord.com/terms). The author is not responsible for any misuse or consequences arising from the use of this software. Use at your own risk.

---

## <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f496.svg" width="22" align="center"/> Donate

<div align="center">

If this project helped you, consider supporting its development — every bit is appreciated! <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f64f.svg" width="16"/>

<table>
  <tr>
    <td align="center">
      <img src="https://img.shields.io/badge/USDT-Polygon-26A17B?style=for-the-badge&logo=tether&logoColor=white" alt="USDT Polygon"/>
    </td>
    <td><code>0xfCc8d58C8577B3aDA2fd27b9a368F3d6DEC947A5</code></td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://img.shields.io/badge/Litecoin-LTC-345D9D?style=for-the-badge&logo=litecoin&logoColor=white" alt="Litecoin"/>
    </td>
    <td><code>LcggSz6zqNzPejreVmG3y6LpPzCCkfnpf2</code></td>
  </tr>
</table>

</div>

---

<div align="center">

### <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f4ec.svg" width="20" align="center"/> Contact

[![Discord](https://img.shields.io/badge/Discord-2rht-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/users/961994878546485268)
[![Telegram](https://img.shields.io/badge/Telegram-@swllette-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/swllette)
[![Store](https://img.shields.io/badge/Store-store.waniboostz.cc-7076CC?style=for-the-badge&logo=shopify&logoColor=white)](https://store.waniboostz.cc)

<br>

**Thank you for your support! <img src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/2b50.svg" width="15"/> Star the repo if you like it!**

</div>
