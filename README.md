
# ResearchX

ResearchX is a deep-research web app built with Python, Gradio, and the OpenAI Agents SDK. It turns a user question into a multi-step research workflow: planning search queries, gathering web results, synthesizing a detailed markdown report, and optionally emailing the result.

Try it at https://amitg23-researchx.hf.space/

## What it does

- Accepts a research prompt from the UI
- Plans a set of targeted web searches
- Uses the search agent to gather concise summaries from multiple sources
- Combines those findings into a long-form report in markdown
- Sends the final report by email (or pushes a notification if email is disabled)

## Project structure

- `app.py` – Gradio app entry point
- `research_manager.py` – orchestrates the research workflow
- `planner_agent.py` – creates the search plan
- `search_agent.py` – performs web search and summarizes results
- `writer_agent.py` – writes the final detailed report
- `email_agent.py` – sends the report via email or Pushover-style push fallback
- `messenger.py` – SMTP and notification helpers
- `styles.py` – Gradio theme and custom UI styling
- `simple.py` – alternate minimal Gradio interface

## Features

- Multistep research orchestration
- Web-based search with OpenAI Agents tooling
- Long-form markdown report generation
- Optional email delivery of the finished research brief
- Lightweight local UI with Gradio

## Requirements

- Python 3.10+
- An OpenAI API key
- Internet access for web search tooling

## Setup

1. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the project root with the required variables:

   ```env
   OPENAI_API_KEY=your_openai_api_key
   DEFAULT_MODEL_NAME=gpt-5.4-nano
   HOW_MANY_SEARCHES=5
   USE_EMAIL=True

   # Optional email settings if USE_EMAIL=True
   EMAIL_ADDRESS=you@example.com
   EMAIL_SMTP_SERVER=smtp.gmail.com
   EMAIL_APP_PASSWORD=your_app_password

   # Optional Pushover fallback
   PUSHOVER_USER=your_pushover_user
   PUSHOVER_TOKEN=your_pushover_token
   ```

   Note: if you are not using email delivery, set `USE_EMAIL=False` and the app will log a push-style message instead.

## Run the app

Start the main Gradio application:

```bash
python app.py
```

This launches a local Gradio UI in the browser, typically at:

```text
http://localhost:7860
```

You can also run the simpler example interface:

```bash
python simple.py
```

## Typical workflow

1. Enter a research question in the app
2. The planner creates a search strategy
3. The search agents gather and summarize relevant web content
4. The writer compiles a detailed markdown report
5. The email agent sends the finished result

## Notes

- The app depends on the OpenAI Agents SDK and web search tools, so your environment must be able to access the configured model and web search provider.
- `.env` values are loaded automatically from the project root using `python-dotenv`.
- The reporting and search prompts are configurable in the agent modules if you want to customize behavior.

## License

This project is provided as-is for research and experimentation.
