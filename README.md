![Stock](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExbXdzN3RwMjk2YnR2eDU4cDE4ZmptZzcxeTM5cTQzZjRnbWEyeHJlZyZlcD12MV9naWZzX3NlYXJjaCZjdD1n/8UvSgaSul5f9o4jIVx/200.webp)

# _**TradeGenie**_
TradeGenie is an educational, proof-of-concept trading platform that combines a sleek React-and-Vite web interface with a robust Python-based backend powered by FastAPI and Poetry (using Python 3.11.9). Its frontend lets users visualize real-time signals, portfolio allocations, and backtesting outcomes, while the backend orchestrates multiple AI “agents”—from value-investing gurus like Ben Graham and Warren Buffett to growth and sentiment analysts—via REST endpoints. With simple commands (e.g., poetry run python main.py --tickers AAPL,MSFT) you can execute live trading simulations or comprehensive backtests, specify custom date ranges, and even toggle local LLM support (--ollama) or verbose agent reasoning. TradeGenie integrates seamlessly with your own API keys for OpenAI, Anthropic, DeepSeek, Groq, Google Gemini, and financial datasets. Designed for learning rather than live trading, it emphasizes modularity, clear project structure, and ease of contribution—making it a perfect sandbox for exploring AI-driven investment strategies.

# _**Base Paper**_

+ https://www.researchgate.net/publication/379835420_When_AI_Meets_Finance_StockAgent_Large_Language_Model-_based_Stock_Trading_in_Simulated_Real-world_Environments
+ https://www.researchgate.net/publication/349189858_Artificial_Intelligence_Applied_to_Stock_Market_Trading_A_Review
+ https://www.researchgate.net/publication/349189858_Artificial_Intelligence_Applied_to_Stock_Market_Trading_A_Review

# _**Algorithm Description**_

The core TradeGenie algorithm orchestrates a team of specialized “agents” to turn raw market data into actionable trading decisions in three broad stages. First, data ingestion and signal generation: price, volume, fundamental, and sentiment feeds are loaded and passed to the Technicals, Fundamentals, Valuation, and Sentiment agents, each of which applies its own models (e.g. moving-average crossovers, NPV-based intrinsic valuation, NLP sentiment scoring) to produce buy/sell/hold signals. Second, signal aggregation and risk filtering: these discrete signals flow into the Portfolio Manager, which weighs them according to predefined confidence and correlation criteria, then hands preliminary position suggestions to the Risk Manager. The Risk Manager enforces position-size limits, stop-loss rules, and overall portfolio volatility constraints, pruning or scaling back suggested trades to ensure adherence to risk budgets. Finally, order generation and execution simulation: the filtered positions are consolidated into executable orders, which the Execution component routes to either the live trading API (for paper or real-money mock trades) or to the Backtester module, where simulated fills and P&L are computed over historical data. At every step, detailed reasoning logs can be emitted—if the --show-reasoning flag is set—to trace how each agent’s insights influenced the final trade decisions.

### _**Setup**_

### Using Poetry

Clone the repository:
```bash
git clone https://github.com/Mudassiruddin7/ai-hedge-fund.git
cd TradeGenie


1. Install Poetry (if not already installed):

curl -sSL https://install.python-poetry.org | python3 -


2. Install dependencies:

poetry install

3. Set up your environment variables:

# Create .env file for your API keys
cp .env.example .env
```

4. Set your API keys.
5. You can run two main operations:

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

## Frontend

### Installation

```bash
# In the frontend directory
git clone https://github.com/Mudassiruddin7/TradeGenie.git
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
* 
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

![thanks](https://media1.tenor.com/images/11ae4fcfc41bb9e66a0176fcfc38e695/tenor.gif?itemid=8486985)


### _**Project Structure**_

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


### _**File & Directory Descriptions**_

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

### _**Disclaimer**_

This project is for **educational and research purposes only**:

* **Not** intended for real trading or investment.
* **No** warranties or guarantees.
* Creator assumes **no liability** for financial losses.
* **Consult a financial advisor** for investment decisions.

By using this software, you agree to use it **solely for learning**.

---

### _**Contributing**_

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-feature`.
3. Commit your changes: `git commit -m "Add awesome feature"`.
4. Push to your branch: `git push origin feature/my-feature`.
5. Open a Pull Request.

Please keep PRs small and focused to simplify review and merging.


 # _**Issues Faced.**_
1. We might face an issue while installing specific libraries.
2. Make sure you have the latest version of python or 3.9, since sometimes it might cause version mismatch.
3. Adding path to environment variables in order to run python files and anaconda environment in code editor, specifically in visual studio code.

# _**Note:**_
**All the required data hasn't been provided over here. Please feel free to contact me for any issues. You can also download the dataset from the given link below.**

### _**Let’s Connect**_

<a href="https://linkedin.com/in/mudassiruddin21" target="blank"><img align="center" src="https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/linkedin.svg" alt="mudassiruddin21" height="30" width="40" /></a>

![Connect](https://media2.giphy.com/media/l1O6zvqu7O317887HF/source.gif)

# _**Yes, you now have more knowledge than yesterday, Keep Going.**_
![Happy](https://media.giphy.com/media/GK7grZYLG7cs0/giphy.gif)
