# TradeGenie

This repository contains two main components:

1. **Frontend**: A React + Vite application providing a web interface to visualize and control the TradeGenie system.  
2. **Backend**: A FastAPI server offering a REST API for running trading analysis and backtests via Poetry (Python 3.11.9).

---

## Table of Contents

- [TradeGenie](#tradegenie)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Frontend](#frontend)
    - [Installation](#installation)
    - [Running](#running)
  - [Backend](#backend)
    - [Installation (Poetry)](#installation-poetry)
    - [Environment Variables](#environment-variables)
    - [Running the Server](#running-the-server)
  - [Project Structure](#project-structure)
  - [File \& Directory Descriptions](#file--directory-descriptions)
  - [Disclaimer](#disclaimer)
  - [Contributing](#contributing)

---

## Overview

TradeGenie is a proof-of-concept AI-driven trading analysis toolkit for educational and research purposes.  
- The **frontend** (React + Vite) lets you visualize signals, portfolios, and backtest results.  
- The **backend** (FastAPI) exposes endpoints to run trading agents, backtests, and risk analysis using multiple LLM-based “agents.”  

---

## Frontend

### Installation

```bash
# In the frontend directory
cd app/frontend
npm install        # or yarn install / pnpm install
````

### Running

```bash
npm run dev
```

Once running, the dev server’s live-reload will reflect code changes instantly in your browser.

---

## Backend

### Installation (Poetry)

1. **Clone** the repo and enter backend folder:

   ```bash
   git clone https://github.com/Mudassiruddin7/TradeGenie.git
   cd TradeGenie/app/backend
   ```
2. **Ensure** you’re using **Python 3.11.9** (e.g. via `pyenv` or `asdf`).
3. **Install Poetry** (if not already):

   ```bash
   curl -sSL https://install.python-poetry.org | python -
   ```
4. **Install dependencies**:

   ```bash
   poetry install
   ```

### Environment Variables

Create a `.env` file in `app/backend/` (you can copy from `.env.example`) and fill in your API keys:

```dotenv
# Anthropic (claude-3-5-sonnet, claude-3-opus, claude-3-5-haiku)
# Get your key from https://anthropic.com/
ANTHROPIC_API_KEY=your-anthropic-api-key

# DeepSeek (deepseek-chat, deepseek-reasoner, etc.)
# Get your key from https://deepseek.com/
DEEPSEEK_API_KEY=your-deepseek-api-key

# Groq (deepseek, llama3, etc.)
# Get your key from https://groq.com/
GROQ_API_KEY=your-groq-api-key

# Google Gemini (gemini-2.0-flash, gemini-2.0-pro)
# Get your key from Google Cloud Console
GOOGLE_API_KEY=your-google-api-key

# Financial datasets
# Get your key from https://financialdatasets.ai/
FINANCIAL_DATASETS_API_KEY=your-financial-datasets-api-key

# OpenAI (gpt-4o, gpt-4o-mini, etc.)
# Get your key from https://platform.openai.com/
OPENAI_API_KEY=your-openai-api-key
```

### Running the Server

From within `app/backend/`:

```bash
poetry run uvicorn main:app --reload
```

* **API Base URL**: `http://localhost:8000`
* **Swagger Docs**: `http://localhost:8000/docs`

You can run two main operations:

* **Trading Analysis**:

  ```bash
  poetry run python src/main.py --tickers TSLA
  ```
* **Backtesting**:

  ```bash
  poetry run python src/backtester.py --tickers TSLA
  ```

Add flags like `--start-date YYYY-MM-DD`, `--end-date YYYY-MM-DD`, `--ollama` (for local LLMs), or `--show-reasoning` as needed.

---

## Project Structure

```
TradeGenie/
├── app/
│   ├── frontend/         # React + Vite client
│   │   ├── public/       # Static assets
│   │   ├── src/          # React components, hooks, styles
│   │   ├── index.html
│   │   └── package.json
│   └── backend/          # FastAPI server (Python 3.11.9)
│       ├── src/
│       │   ├── api/            # API layer (future expansion)
│       │   ├── models/         # Pydantic schemas
│       │   ├── routes/         # Route definitions (hedge_fund, health)
│       │   ├── services/       # Business logic (agents, portfolio, graph)
│       │   ├── main.py         # Entry point for FastAPI
│       │   ├── backtester.py   # Backtesting CLI script
│       │   └── __init__.py
│       ├── pyproject.toml
│       ├── poetry.lock
│       └── .env.example
├── README.md           # This file
└── .gitignore
```

---

## File & Directory Descriptions

* **app/frontend/**: Contains all web-UI code powered by React & Vite.
* **app/backend/src/routes/**: Defines REST endpoints:

  * `hedge_fund.py`: `/hedge-fund/run` endpoint for trading analysis.
  * `health.py`: `/ping` health-check endpoint.
* **app/backend/src/services/**: Implements core logic:

  * `graph.py`: Orchestrates agent workflow.
  * `portfolio.py`: Manages portfolio state, risk limits, and order generation.
* **app/backend/src/models/**: Pydantic schemas for request/response validation.
* **app/backend/main.py**: FastAPI app instance and router inclusion.
* **app/backend/backtester.py**: CLI tool for backtesting strategies.
* **pyproject.toml**: Poetry project configuration (dependencies, scripts).

---

## Disclaimer

This project is for **educational and research purposes only**:

* **Not** intended for real trading or investment.
* **No** warranties or guarantees.
* Creator assumes **no liability** for financial losses.
* **Consult a financial advisor** for investment decisions.

By using this software, you agree to use it **solely for learning**.

---

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-feature`.
3. Commit your changes: `git commit -m "Add awesome feature"`.
4. Push to your branch: `git push origin feature/my-feature`.
5. Open a Pull Request.

Please keep PRs small and focused to simplify review and merging.
