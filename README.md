# Sports, Politics & Weather Assistant

An AI chatbot that gives you the latest sports headlines, politics news, and live weather for any city, all in one chat window. Ask a question in plain English and the assistant picks the right tool, fetches fresh data, and replies with a short, easy-to-read answer.

![Screenshot](screenshot.png)

## Features
- **Live weather** for any city in the world
- **Sports news**, with a dedicated football (soccer) feed
- **Politics news** covering the UK, Africa, and the wider world
- **Multi-part questions**, e.g. "Give me Africa politics headlines and the weather in Lagos"
- **Conversation memory**, so follow-ups like "what about Lagos?" just work
- **Neutral on politics**: it reports what happened and never takes sides
- **Honest about failures**: if a feed or service is down, it says so instead of making things up
- **No extra API keys** needed for the data, only a model key

## Tech Stack
- Python
- OpenAI Agents SDK (agent and function tools)
- OpenRouter (model access)
- Gradio (chat interface)
- Open-Meteo (weather data)
- BBC RSS feeds (news headlines)
- uv (package management)

## How It Works
1. The user asks a question in the Gradio chat window.
2. The conversation is sent to an agent built with the OpenAI Agents SDK.
3. The agent decides which tool to call: `get_weather` or one of the news tools. For multi-part questions, it calls several and combines the results.
4. Each tool fetches live data and returns it to the agent.
5. The agent writes a short answer, with links for any news story.

## Getting Started

### Prerequisites
- Python 3.10 or newer
- [uv](https://docs.astral.sh/uv/) installed
- An [OpenRouter](https://openrouter.ai) API key

### Setup

1. Clone the repo
   ```
   git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
   cd YOUR-REPO
   ```

2. Install dependencies
   ```
   uv sync
   ```

3. Create a `.env` file in the project folder
   ```
   API_TOKEN=your-openrouter-api-key
   ```

4. Open the notebook in VS Code, select the `.venv` kernel, and run the cells from top to bottom. The chat interface will launch in your browser.

## Example Questions
- "What's the weather in Abuja?"
- "Any big football news today?"
- "Give me Africa politics headlines and the weather in Lagos"
- "What's happening in world politics?"

## Project Structure
```
├── your-notebook.ipynb   # Main notebook
├── pyproject.toml        # Dependencies
├── uv.lock               # Locked versions
├── .env                  # API key (never committed)
└── .gitignore
```

## Adding a New Topic
News tools are generated from a single dictionary called `NEWS_FEEDS`. To add a topic like business or technology, add one entry with a tool name, a description, and an RSS feed URL. The agent picks it up automatically.

For other data sources (live scores, another weather provider), write a new `@function_tool` and add it to `ALL_TOOLS`.

## Troubleshooting
- **API key not found:** make sure `.env` is saved in the project folder and the variable is named exactly `API_TOKEN`.
- **A news feed returns nothing:** feed URLs can change. Swap in a working RSS link in `NEWS_FEEDS`.
- **Gradio errors on Windows ("Application Control policy has blocked this file"):** a security policy is blocking some compiled files. Move the project to a simple folder like `C:\dev`, or run it in Google Colab or GitHub Codespaces.

## Limitations
- News comes from BBC feeds, so coverage leans UK and international.
- Weather shows current conditions only, not forecasts.
- Answers are limited to sports, politics, and weather.

## Roadmap
- Specialist agents (sports, politics, weather) coordinated by a main agent
- Weather forecasts
- Live match scores
- More news categories

## Author
Built by **Churchill Educe**
[LinkedIn](https://linkedin.com/in/your-profile)