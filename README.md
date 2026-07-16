# Monitor-App

A personal dashboard that tracks news, financial markets, your portfolio, weather, and Bitcoin miners on your network — with customizable watchlists and tickers. It also acts as a Nostr client with adjustable panes.

**Currently only works on Mac.**

## Requirements

- macOS
- Python 3 (comes pre-installed on modern Macs — check with `python3 --version` in Terminal)
- A modern web browser (Chrome, Safari, etc.)

No other installs, API keys, or accounts are required to get the dashboard running. (Financial statement data optionally uses a free [Financial Modeling Prep](https://financialmodelingprep.com/) key — see **Optional** below.)

## Setup

1. **Download the files.** Click the green `Code` button on this repo → `Download ZIP`, then unzip it. Or, if you have git installed:
   ```bash
   git clone https://github.com/<your-username>/Monitor-App.git
   ```
2. Make sure `monitor.html` and `proxy.py` are in the **same folder** — the server looks for `monitor.html` right next to itself.

## Running it

1. Open **Terminal** (search for it with Spotlight — `Cmd + Space`, type "Terminal").
2. Navigate to the folder where you saved the files, for example:
   ```bash
   cd ~/Downloads/Monitor-App
   ```
3. Start the server:
   ```bash
   python3 proxy.py
   ```
   You should see a message confirming the server is running on port `8082`.
4. Open your browser and go to:
   ```
   http://127.0.0.1:8082
   ```
5. Leave the Terminal window open — closing it stops the server. To stop it manually, click into the Terminal window and press `Ctrl + C`.

## Restarting later

Every time you want to use the dashboard again, just repeat the "Running it" steps: `cd` into the folder, run `python3 proxy.py`, and open `http://127.0.0.1:8082` in your browser.

If you'd rather not retype the `cd` command each time, you can create a simple double-clickable script:
1. Open TextEdit (or any text editor), paste in:
   ```bash
   #!/bin/bash
   cd "$(dirname "$0")"
   python3 proxy.py
   ```
2. Save it as `start.command` in the same folder as `monitor.html` and `proxy.py`.
3. In Terminal, run `chmod +x start.command` once to make it executable.
4. After that, you can just double-click `start.command` to launch the server.

## Notes

- **Local only:** the server binds to `127.0.0.1`, meaning it's only accessible from your own Mac — it isn't exposed to your network or the internet.
- **Your data stays local:** watchlist, portfolio, ticker settings, and weather location are all saved in your browser's local storage on your machine, not in this repo or anywhere online.
- **Miners:** if you use the Bitcoin miner tracking feature, miner IPs are saved to a `miners.json` file that the server creates in this folder. That file is specific to your setup — don't commit it if you push further changes back to GitHub.
- **Nostr login:** if you log into the Nostr client features using a private key (nsec), be aware it's stored in your browser's local storage in plain text. Only do this on a device you trust, and consider using a browser extension signer (NIP-07) instead where possible.

## Optional: Financial statement data

Company financial statements pull from free public sources (SEC EDGAR) by default and need no setup. If you want to add a [Financial Modeling Prep](https://financialmodelingprep.com/) API key for extended data, set it as an environment variable before starting the server:

```bash
export FMP_API_KEY=your_key_here
python3 proxy.py
```
