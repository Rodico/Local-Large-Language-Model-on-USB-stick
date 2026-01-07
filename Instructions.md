# Ollama Server & Model Scripts

This repository contains convenient scripts to start the Ollama server and run the Dolphin model on Windows, Linux, macOS, and WSL.

## Windows Batch Scripts

### start_server.bat
Starts the Ollama server and keeps the window open for logs.
```batch
@echo off
REM Start Ollama server (keep window open for logs)
echo Starting Ollama server...
ollama serve
pause
```

### run_model.bat
Runs the Dolphin model interactively. Change the model tag if needed.
```batch
@echo off
REM Run Dolphin interactively. Change model tag if needed.
echo Running Dolphin model...
ollama run dolphin3:latest
pause
```

### start_both.bat
Opens two command windows: one for the server and one for the model.
```batch
@echo off
REM Opens two new cmd windows: one for server, one for model
start "Ollama Server" cmd /k "%~dp0start_server.bat"
timeout /t 1 >nul
start "Ollama Model" cmd /k "%~dp0run_model.bat"
exit
```

**Windows Notes:**
- If Ollama is installed locally on a USB drive, replace `ollama` with `.\ollama\ollama.exe` or use the full path
- These scripts assume the drive has already been changed (e.g., `D:`)
- The `start_both.bat` file uses `%~dp0` so it works when double-clicked from any location

## POSIX Scripts (Linux / macOS / WSL)

### start_server.sh
Starts the Ollama server in the foreground with visible logs.
```bash
#!/usr/bin/env bash
set -e
echo "Starting Ollama server (foreground) — logs will show here"
ollama serve
```

Make executable:
```bash
chmod +x start_server.sh
```

### run_model.sh
Runs the Dolphin model interactively.
```bash
#!/usr/bin/env bash
set -e
echo "Running Dolphin model interactively"
ollama run dolphin3:latest
```

Make executable:
```bash
chmod +x run_model.sh
```

### start_both.sh
Uses `tmux` to run both server and model in split panes. Falls back to background server if `tmux` is unavailable.
```bash
#!/usr/bin/env bash
set -e
if command -v tmux >/dev/null 2>&1; then
  tmux new-session -d -s ollama_server "bash -lc './start_server.sh'"
  tmux split-window -v -t ollama_server "bash -lc './run_model.sh'"
  tmux attach -t ollama_server
else
  echo "tmux not found — starting server in background and model in foreground"
  ./start_server.sh & disown
  sleep 1
  ./run_model.sh
fi
```

Make executable:
```bash
chmod +x start_both.sh
```

## Installation & Setup

### First Time: Pull the Model
Before running the model, download it with:
```bash
ollama pull dolphin3:latest
```

Or for the 8B parameter version:
```bash
ollama pull dolphin3:8b
```

## Troubleshooting

- **`ollama` command not found**: Install Ollama from [https://ollama.com](https://ollama.com)
- **Model is missing**: Run `ollama pull dolphin3:latest` to download it
- **Default server address**: [http://localhost:11434/](http://localhost:11434/)

## License

Ollama and Dolphin models are Free and Open Source Software (FOSS).

---

**Quick Start:**
- **Windows**: Double-click `start_both.bat`
- **Linux/macOS**: Run `./start_both.sh`
