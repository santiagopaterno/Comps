[README.md](https://github.com/user-attachments/files/26096372/README.md)
# Live Comps Builder

Automated comparable company analysis tool that replicates the core workflow of a junior IB analyst — select a target, define a peer set, and get a full comps table with implied valuation ranges in seconds.

**[Live Demo →](https://santiagopaterno.github.io/comps-builder)**

---

## What It Does

This tool automates the most repetitive part of investment banking: building a comparable company analysis from scratch. Instead of manually pulling financials from Bloomberg or Capital IQ, computing enterprise value bridges, and calculating multiples in a spreadsheet, this tool does it in one click.

**Inputs:** A target company ticker and 2–6 peer company tickers.

**Outputs:**
- Full comps table with Market Cap, EV, Revenue, EBITDA, margins, and three standard trading multiples (EV/EBITDA, EV/Revenue, P/E)
- Statistics row with mean, median, 25th and 75th percentile across the peer set
- Implied equity valuation for the target company at each percentile and methodology
- Football field chart showing valuation ranges visually
- One-click CSV export ready for pitchbook integration

## How It Works

The tool has two modes:

**Demo Mode** — Pre-loaded with financial data for seven major tech companies (MSFT, AAPL, GOOGL, AMZN, META, CRM, ORCL). No setup required. Works immediately for anyone visiting the link.

**Live Mode** — Connects to the [Financial Modeling Prep API](https://site.financialmodelingprep.com/) to pull real-time financials for any publicly traded company. Requires a free API key (250 requests/day on the free tier).

### Data Pipeline (Live Mode)

For each ticker, the tool makes three parallel API calls:

1. **Company Profile** — market cap, current price, sector
2. **Income Statement** (most recent annual) — revenue, EBITDA, net income
3. **Balance Sheet** (most recent annual) — total debt, cash and equivalents

From these, it calculates:
- **Enterprise Value** = Market Cap + Total Debt − Cash
- **EV/EBITDA**, **EV/Revenue**, **P/E** multiples
- **EBITDA Margin**, **Net Margin**
- Percentile statistics across the peer set
- Implied equity value = (Peer Multiple × Target Metric) − Net Debt

## Getting a Free API Key

1. Go to [financialmodelingprep.com](https://site.financialmodelingprep.com/)
2. Sign up with your email (free)
3. Copy your API key from the dashboard
4. Paste it into the Live Mode field in the tool

The free tier allows 250 API calls per day. Each comps run uses approximately 3 calls per company (target + peers), so a typical 5-peer analysis uses around 18 calls.

## Deployment

This is a single self-contained HTML file — no build tools, no npm, no dependencies to install.

**GitHub Pages (free):**

1. Create a new repository on GitHub
2. Upload `index.html` to the repo
3. Go to Settings → Pages → Source → select `main` branch, root folder
4. Your tool is live at `yourusername.github.io/repo-name`

**Any static host:** Upload the HTML file to Netlify, Vercel, Cloudflare Pages, or any web server. It just works.

## Tech Stack

- **React 18** — UI components and state management
- **Babel Standalone** — JSX compilation in the browser (no build step)
- **Financial Modeling Prep API** — live financial data
- **Vanilla CSS** — no frameworks, fully self-contained

Single file, ~480 lines, zero external dependencies at build time.

## Why This Exists

In investment banking, comparable company analysis is one of the most common deliverables. Analysts build these tables multiple times per week, and the data-gathering step — pulling market caps, computing EV bridges, sourcing EBITDA from filings — is purely mechanical. This tool eliminates that step entirely.

Built as part of a self-directed IB training program focused on financial modelling, Excel automation, and AI-assisted workflows.

## Author

**Santiago Paternó**
Economics Graduate · Universidad del CEMA · Buenos Aires, Argentina

---

*Financial data provided by [Financial Modeling Prep](https://site.financialmodelingprep.com/). Data is for informational purposes only and should not be considered investment advice.*
