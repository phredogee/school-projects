OLLAMA_URL=http://localhost:11434
WEAVIATE_URL_VERBA=http://localhost:8080
WEAVIATE_API_KEY=

Absolutely, Alfredo! Here’s the full Verba RAG Deployment Playbook in plain text format—ready for you to copy and paste into Notepad, VS Code, or anywhere else you want to save it:

🧠 Verba RAG Deployment Playbook (Step-by-Step)
Set up a local Retrieval-Augmented Generation (RAG) system using Verba, Docker, and Ollama on Windows.

🔧 1. Install Prerequisites
- Download and install:
- Docker Desktop → https://www.docker.com/products/docker-desktop
- Git for Windows → https://git-scm.com/downloads
- Ollama → https://ollama.com/download

🛠️ 2. Create Launch Script (start-verba.sh)
- Open Git Bash
- Run:
nano ~/start-verba.sh
- Paste:
#!/bin/bash
echo "🚀 Starting Ollama..."
ollama serve &

echo "🐳 Starting Docker containers..."
cd ~/phredo/my_project/verba
docker compose up -d

echo "🌐 Opening Verba in browser..."
sleep 5
start http://localhost:8000

read -p "Press Enter to close this window..."
- Save (Ctrl+O → Enter), then exit (Ctrl+X)
- Make executable:
chmod +x ~/start-verba.sh



🛑 3. Create Shutdown Script (stop-verba.sh)
- In Git Bash, run:
nano ~/stop-verba.sh
- Paste:
#!/bin/bash
echo "🛑 Stopping Verba containers..."
cd ~/phredo/my_project/verba
docker compose down

echo "🧠 Stopping Ollama (if running)..."
pkill -f "ollama serve"

echo "✅ All systems powered down."
- Save and exit
- Make executable:
chmod +x ~/stop-verba.sh



✨ 4. Add Aliases to .bashrc
- Open:
nano ~/.bashrc
- Add:
alias verba-start="~/start-verba.sh"
alias verba-stop="~/stop-verba.sh"
- Save and reload:
source ~/.bashrc



🖥️ 5. Create Desktop Shortcuts
- Launch Verba:
"C:\Program Files\Git\git-bash.exe" --cd="C:\Users\alfre" -i -c "./start-verba.sh"
- Stop Verba:
"C:\Program Files\Git\git-bash.exe" --cd="C:\Users\alfre" -i -c "./stop-verba.sh"



🔐 6. Create .env File
In ~/phredo/my_project/verba/.env, paste:
OLLAMA_URL=http://host.docker.internal:11434
OLLAMA_MODEL=llama3
OLLAMA_EMBED_MODEL=nomic-embed-text
WEAVIATE_URL_VERBA=http://weaviate:8080



🐳 7. Build and Start Verba with Docker
cd ~/phredo/my_project/verba
docker compose down
docker compose up --build -d


If needed, prune Docker cache:
docker builder prune -af
docker system prune -af



🛠️ 8. Troubleshooting Common Issues
- Blank Page: Check .env is set; inspect logs:
docker compose logs verba
- Port 8080 in use:
netstat -ano | findstr :8080
tasklist /FI "PID eq <PID>"   # In CMD or PowerShell
taskkill /PID <PID> /F



✅ 9. Final Checks
- Run:
verba-start
- Open: http://localhost:8000
- Interact with Verba
- Shut down with:
verba-stop



Copy all of the above into Notepad, save it as verba_setup.txt or verba_setup.md, and you’re good to go! Want me to turn this into a downloadable file for even easier access next?
