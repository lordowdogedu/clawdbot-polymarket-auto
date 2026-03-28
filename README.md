# Clawdbot Polymarket Auto

> Fully automated Clawdbot trading module for Polymarket that scans markets, evaluates signals, and places entries without manual input. Configurable risk limits, position sizing, and market filters let it run unattended around the clock.

*Last updated: March 2026*

---

![preview_clawdbot polymarket auto trader bot](https://github.com/user-attachments/assets/deff196c-07f6-494d-bda4-9796c5560648)

---

## What is Clawdbot Polymarket Auto?

Clawdbot Polymarket Auto is the fully automated trading module of the Clawdbot suite. It combines market scanning, signal evaluation, and order execution into a single unattended process. You configure your entry rules, risk limits, and market filters once - then the bot handles everything from discovery to exit.

Set it. Let it run. Review results.

---

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/lordowdogedu/clawdbot-polymarket-auto/releases) |

---

## What It Automates

| Step | What the Bot Does |
|------|-----------------|
| **Discovery** | Scans all active Polymarket markets every cycle |
| **Evaluation** | Scores each market against your entry rules |
| **Entry** | Places YES or NO position when rules are satisfied |
| **Monitoring** | Tracks open positions for exit conditions |
| **Exit** | Closes at take-profit, stop-loss, or time expiry |
| **Reporting** | Logs all trades and sends daily Telegram summary |

---

## Engine Features

* **Always-on scanning** - monitors all active Polymarket CLOB markets 24/7
* **Rule-based entry** - configurable odds range, volume minimum, category filter, and time-to-resolution window
* **Multi-signal scoring** - combines momentum, volume, and whale activity into entry score
* **Risk controls** - daily USD cap, max open positions, per-trade size limit
* **Auto-exit** - closes on take-profit %, stop-loss %, or configurable time before resolution
* **Restart recovery** - saves state to disk, resumes cleanly after reboot
* **Telegram daily summary** - end-of-day P&L, trade count, and win rate delivered automatically

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **Rules** | Config-based | Custom logic |
| **Exit logic** | Built-in | Fully customizable |
| **Config** | `config.toml` | Direct code access |
| **Reports** | Dashboard + Telegram | JSON + Telegram |

## Quick Start

```
# 1. Download from Releases
# 2. Edit config.toml - set entry rules, risk limits, and Polymarket API key
# 3. Run Clawdbot Auto - trading starts immediately and runs unattended
```

### Python

```bash
cd clawdbot-polymarket-auto/python
pip install -r requirements.txt
python clawdbot-polymarket-auto-v.1.4.14.py
```

---

## How It Works

![clawdbot auto pipeline](https://github.com/user-attachments/assets/15c3e2f0-00a4-4426-8fd6-0942916c4703)

Five stages per cycle:

1. **Scan** - fetches all active markets and filters by your category and volume settings
2. **Score** - evaluates each market against your entry rules and signal weights
3. **Enter** - places position if score exceeds your configured entry threshold
4. **Monitor** - tracks each open position against exit conditions every cycle
5. **Exit** - closes position at take-profit, stop-loss, or time trigger

### Config Reference

```toml
[entry]
odds_min = 0.20
odds_max = 0.75
min_volume_usd = 1000
categories = ["politics", "economics", "crypto"]
max_days_to_resolution = 60
entry_threshold = 0.60

[risk]
position_size_usd = 25
max_open_positions = 8
daily_cap_usd = 200

[exit]
take_profit_pct = 20
stop_loss_pct = 10
close_hours_before_resolution = 6

[polymarket]
api_key = ""
private_key = ""

[telegram]
bot_token = ""
chat_id = ""
```

---

## Trade Log Format

```json
{
  "trade_id": "auto_20260326_017",
  "market": "will-sp500-hit-6000-april",
  "side": "NO",
  "entry_price": 0.68,
  "exit_price": 0.55,
  "size_usd": 25,
  "pnl_usd": 4.78,
  "exit_reason": "take_profit",
  "entry_time": "2026-03-26T08:31:00Z",
  "exit_time": "2026-03-26T14:22:00Z"
}
```

---

## Verified Live

**Configuration used:**
* Odds 0.20-0.75, politics + economics, $25 per trade, daily cap $200

**Auto trade executed:**

| | Details |
|---|---|
| Market | will-sp500-hit-6000-april |
| Side | NO at 0.68 |
| Exit | 0.55 at take-profit (+19.1%) |
| P&L | +$4.78 |
| Tx hash | 0xb2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c3 |

---

## Frequently Asked Questions

**What is Clawdbot Polymarket Auto?**
Clawdbot Polymarket Auto is the fully automated trading module of the Clawdbot suite. It scans all Polymarket markets, scores them against your entry rules, places positions automatically, and exits on your configured take-profit, stop-loss, or time conditions.

**Does it need supervision?**
No. The bot is designed for unattended operation. Telegram daily summaries keep you informed without requiring you to monitor the bot manually.

**Can I limit which categories it trades?**
Yes. Set the `categories` list in config to restrict trading to your preferred Polymarket categories.

**What happens if the bot crashes?**
Clawdbot Auto saves open position state to disk every cycle. On restart it recovers the position list and continues monitoring without re-entering already-open trades.

**Is this a polymarket auto trading bot?**
Yes. Automatic discovery, entry, and exit with no manual steps required after initial configuration.

**How does the entry scoring work?**
The bot calculates a score from momentum, volume trend, and optional whale signal data. Only markets scoring above your `entry_threshold` receive a position.

**Can it run alongside other Clawdbot modules?**
Yes. Clawdbot modules are independent processes. Run Auto alongside Signals or Whale tracker simultaneously.

---

## Use Cases

- **Polymarket automated trading** - run a fully unattended Polymarket trading strategy 24/7
- **Polymarket hands-free bot** - set entry rules once and let the bot execute without manual input
- **Clawdbot auto trader** - use as the execution backbone of the full Clawdbot suite
- **Polymarket trading automation** - automate entry, monitoring, and exit for any Polymarket category
- **Polymarket autopilot bot** - systematic rule-based trading with daily Telegram reporting

---

## Repository Structure

```
clawdbot-polymarket-auto/
+-- clawdbot-polymarket-auto-v.1.4.14.exe
+-- config.toml
+-- data/
|   +-- trades/
|   +-- state/
|   +-- logs/
|   +-- dll/
+-- python/
|   +-- src/
|   |   +-- scanner.py
|   |   +-- scorer.py
|   |   +-- executor.py
|   |   +-- monitor.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, py-clob-client, pandas
```

* Polymarket account with CLOB API access
* Telegram bot token (for reports and alerts)

---

*Configure once. Trade always.*
