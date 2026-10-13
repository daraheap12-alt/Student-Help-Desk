# How to Run the Monitoring Project

This repository contains a local student-support RAG app, PostgreSQL request logging, a Streamlit monitoring dashboard, and a provisioned Grafana dashboard. After each generated answer, the app asks the configured LLM to score its correctness, groundedness, and relevance against the retrieved FAQ context.The evaluation and judge token usage are saved with the conversation and shown in the chat and monitoring dashboard. This judge call uses the configured model provider and consumes additional API tokens; the interface shows an evaluation warning if judging fails while preserving the generated answer.

## Prerequisites
* **Docker Desktop** (required if running via Docker Compose)
* **Python** & **uv** package manager (required if running locally outside Docker)
* An active API key for your chosen model provider: **Groq** (`GROQ_API_KEY`) or **OpenAI** (`OPENAI_API_KEY`)

---

## Option 1: Run the full stack with Docker Compose (Recommended)

1. Copy `.env.example` to `.env` and configure your chosen provider (`LLM_PROVIDER`), API key, and database/Grafana passwords.
2. From the project root directory, build and start the services:
   ```powershell
   docker compose up --build -d
   ```
   *(The PostgreSQL tables will initialize automatically on startup).*
3. Access the applications in your browser:
   * **Streamlit App:** `http://localhost:8501`
   * **Grafana Dashboard:** `http://localhost:3000` (Username: `admin`, Password: the value you set in `GRAFANA_ADMIN_PASSWORD`, defaulting to `admin`)

*To stop the stack, run `docker compose down`. Only use `docker compose down -v` if you intend to completely delete the stored monitoring data.*

---

## Option 2: Run Streamlit outside Docker (Local Development)

1. Start only the PostgreSQL database container via Docker:
   ```powershell
   docker compose up -d postgres
   ```
2. Update your `DATABASE_URL` in `.env` to connect to `localhost`.
3. Install dependencies, initialize the database, and run the chat app:
   ```powershell
   uv sync
   uv run python db_init.py
   uv run streamlit run app.py
   ```
4. *(Optional)* Run the standalone monitoring dashboard in a separate terminal:
   ```powershell
   uv run streamlit run dashboard.py
   ```
5. *(Optional)* Insert synthetic conversation and feedback records for testing the dashboard:
   ```powershell
   uv run python generate_data.py --count 25 --seed 42
   ```

---

## Option 3: Deploy the chat app to Streamlit Community Cloud

1. Push your project files to a GitHub repository (ensure `.env` and `.venv` are excluded via `.gitignore`).
2. Go to [Streamlit Community Cloud](https://share.streamlit.io/), choose **Create app**, link your repository and branch, and set the **Main file path** to `app.py`.
3. Under the app's **Settings > Secrets**, add your provider configuration. For example, using Groq:
   ```toml
   LLM_PROVIDER = "groq"
   GROQ_API_KEY = "your-groq-api-key"
   GROQ_MODEL = "openai/gpt-oss-120b"
   ```
   *(Note: The app will run using the local FAQ dataset without a database, but conversations and monitoring metrics will not persist. To enable full persistence and dashboards on the cloud, you must also provide a cloud-hosted PostgreSQL `DATABASE_URL` secret, because a database running on `localhost` cannot be reached from Streamlit Cloud).*
