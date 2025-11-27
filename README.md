<!-- ...existing code... -->

# LearningBuddy

LearningBuddy is a personalized AI-powered learning platform with a React + Vite frontend, a FastAPI backend, and a multi-agent AI system (AgentSystem) that uses Google Gemini (configured via GOOGLE_API_KEY).

## Quick overview

- Frontend: frontend (Vite, React, TypeScript, Tailwind)
- Backend: main.py (FastAPI)
- Agent system: AgentSystem/agentsys.py and AgentSystem/main.py
- Local tasks: tasks.json
- Agent logs: AgentSystem/logs

## Requirements (macOS)

- Git
- Python 3.10+ (or 3.x)
- Node 18+ / npm or pnpm
- (Optional) GitHub CLI (gh)

## Security / .gitignore

Do not commit secrets. Add a .env to .gitignore (node_modules, .venv, AgentSystem/logs, etc.). Recommended entries:

```text
node_modules/
frontend/node_modules/
.venv/
.env
.env.*
__pycache__/
*.pyc
dist/
build/
AgentSystem/logs/
.DS_Store
.vscode/
*.log
```

## Environment variables

Create a `.env` in repo root with at least:

```ini
GOOGLE_API_KEY=your_gemini_api_key
FASTAPI_PORT=8000
FRONTEND_URL=http://localhost:3000
```

Do not commit `.env`.

## Setup (one-time)

Open Terminal in repo root:
```bash
cd /Users/priyanshigoyal/Downloads/learning-buddy-Palak-js
```

Create Python venv and install backend deps:
```bash
python -m venv .venv
source .venv/bin/activate
# if requirements.txt exists
pip install -r requirements.txt || true
# minimal fallback
pip install fastapi uvicorn python-dotenv
```

Install frontend deps:
```bash
cd frontend
npm install
cd ..
```

## Run locally (development)

1) Start backend (from repo root):
```bash
# Activate venv if not active
source .venv/bin/activate
# Option A: direct
python main.py
# Option B: uvicorn
uvicorn main:app --reload --host 0.0.0.0 --port ${FASTAPI_PORT:-8000}
```

2) Start agent system (separate terminal; ensure .env is loaded):
```bash
cd AgentSystem
# use same venv or a Python env with required deps
python main.py
```

3) Start frontend (separate terminal):
```bash
cd frontend
npm run dev
# open the Vite URL (usually http://localhost:5173)
```

## Testing / Quick check

- Open frontend dev URL and use the Chat page to submit a task.
- Backend endpoint add_task is in main.py — verify requests there.
- AgentSystem reads tasks.json and writes logs to AgentSystem/logs.

## Common commands

Initialize git & push (example):
```bash
git init
git add .
git commit -m "Initial commit: LearningBuddy"
# create GitHub repo with gh (optional)
gh auth login
gh repo create learning-buddy-Palak-js --public --source=. --remote=origin --push
```

Remove accidentally committed secrets: rotate keys and use BFG or git filter-repo.

## Notes & troubleshooting

- Ensure GOOGLE_API_KEY is set before starting AgentSystem.
- If AgentSystem requires additional AI libs (autogen_*), install them per project requirements.
- If frontend cannot reach backend, update FRONTEND_URL and CORS settings in main.py.

## Contributing

- Open issues / PRs.
- Follow code style in frontend and backend.
- Add tests when adding features.

## License

Add your chosen license