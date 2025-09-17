<pre>
         █                                                  
      ████           ██                                     
       ███         ████    █      █                         
████   ████       █████  ███    ███   ████       ██         
████   ████      ██████  ███    ███  ████████  ████         
 ███    ████     ███████ ███    ███  ███ █████ ████         
 ███     ████   ████████ ███    ████ ████  ████████         
 ███      ████  ███ ████ ███    ████  ████   ███████        
 ████      ████ ███  ███ ███    ████   ████   ██████        
 ████       ███████  ███████    ████    ████   ██████       
  █████████████ ███  ███████    █████    ████   █████       
  ██████████   ████   ███████   █████  █  ████   █████      
  ███████      ████   ███████   █████████  █████   ███      
  █████████    ███    ███████   ██████████   █████ ██       
   ███  █████  ██      ███████  ████████████   █████        
   ███   █████████████████████████ ███ ██████    █████      
   ████    ████████████████ █████  ████ ███████    █████    
   ███        █████     ███  █      ███  ████████    █████  
                ██████  █           ██    ███████████  ████ 
                   ██████                  ██     ████████  
                     ██                                     </pre>
# Crypto Recon (OSINT) — Username & Wallet Address

A lightweight **defensive OSINT recon tool** to search for **usernames** or **wallet addresses** across the web and blockchain explorers. Designed for **ethical investigations**.

**Targets:** Bitcoin, Ethereum, Solana, Monero  
**APIs:** Optional Blockchair and Etherscan integration (requires environment API keys).  
**Output:** JSON reports, raw HTML snapshots, and detected credential signatures.

---

## Features

- Scan **blockchain explorers** for wallet addresses.
- Optional API enrichment for Ethereum (Etherscan) and multi-chain (Blockchair).
- Username reconnaissance via DuckDuckGo search, with **multi-page scraping** support.
- SQLite caching to avoid rechecking URLs.
- Signature-based detection for `email:password` and `user:pass`.
- CLI options:
  - `--no-cache` to bypass caching.
  - `--db` to configure cache path.
  - `--limit` to control number of username search results.
- Saves HTML snapshots for all pages fetched.

---

## Installation

### Prerequisites
- Python 3.8+
- Linux, macOS, or Windows

### Dependencies

```bash
pip3 install requests beautifulsoup4 lxml


⸻

Usage

# Wallet address reconnaissance
python3 crypto_recon.py --target <WALLET_ADDRESS> --type address

# Username reconnaissance
python3 crypto_recon.py --target <USERNAME> --type username --limit 20

# Bypass cache temporarily
python3 crypto_recon.py --target <TARGET> --type address --no-cache

# Use custom SQLite cache path
python3 crypto_recon.py --target <TARGET> --type username --db /path/to/mycache.db

Output
	•	findings_<target>.json — JSON report with matches and metadata.
	•	reports/<target>/ — raw HTML snapshots of pages fetched.

⸻

Ethics & Usage Notes
	•	Only investigate addresses or usernames you own or have explicit permission to investigate.
	•	Be polite with web scraping:
	•	Use --limit to avoid excessive requests.
	•	Respect robots.txt.
	•	Random delays are included by default to reduce rate-limit risk.
	•	Monero addresses are privacy-focused; expect fewer results.

⸻

To-Do / Next Improvements
	•	Enhance username recon
	•	Follow multiple DuckDuckGo result pages.
	•	Scrape links from result pages to increase coverage.
	•	Avoid blocks with polite delays and random user agents.
	•	Integrate Rotating Proxies for large-scale username scans.
	•	Add CSV output in addition to JSON.
	•	Add alerting / notifications for matches.
	•	Improve signature detection:
	•	Add more credential patterns (e.g., OAuth tokens, API keys).
	•	Detect pastes on known pastebin-style sites.
	•	Add optional integrations:
	•	Blockchair / Etherscan API queries (enhanced metadata)
	•	VirusTotal or Shodan enrichment (API keys required)
	•	Enhance caching:
	•	Implement TTL (time-to-live) for cached URLs.
	•	Store additional metadata (HTTP headers, content hash) to detect changes.
	•	Add progress bars / verbosity levels for CLI.
	•	Add modular plugins for new explorers or OSINT sources.
	•	Add automated test suite for parser resilience.

⸻

Notes
	•	This tool is defensive and educational — do not use it for unauthorized attacks.
	•	Blockchain explorer scraping is fragile; websites change often.
	•	API enrichment is optional and requires environment variables:
	•	BLOCKCHAIR_API_KEY
	•	ETHERSCAN_API_KEY
	•	Default caching uses cache.db in the working directory.

⸻

Example Workflow
	1.	Recon your BTC wallet:

python3 crypto_recon.py -t 1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa -y address

	2.	Recon a username with multi-page scraping:

python3 crypto_recon.py -t john_doe -y username --limit 50

	3.	Check findings_john_doe.json and reports/john_doe/ for raw HTML and matches.

⸻
