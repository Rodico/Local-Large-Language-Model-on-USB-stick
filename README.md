# Local-Large-Language-Model-on-USB-stick

Local Dolphin (Ollama) — USB quick start
--------------------------------------
Prereqs on the target machine:
- Ollama installed and on PATH (install from https://ollama.com). 
- If you pre-downloaded Dolphin Modelfile(s) to the USB, copy them into a local Ollama models dir or use `ollama pull` as shown below.

Quick steps (Windows):
1. Insert USB and open PowerShell / cmd.
2. Switch to the USB drive, e.g.:
   PS> D:
3. Start server (one terminal):
   PS> .\start_server.bat
4. In a second terminal, switch to D: and run model:
   PS> .\run_model.bat

Quick steps (Linux / mac / WSL):
1. Open two terminals.
2. In both: `cd /path/to/usb` (e.g. `/media/you/USB`)
3. Terminal A: `./start_server.sh`
4. Terminal B: `./run_model.sh`

Commands used:
- Start server: `ollama serve` (default binds to http://localhost:11434). :contentReference[oaicite:1]{index=1}
- Pull model (optional): `ollama pull dolphin3:latest` or `ollama pull dolphin3:8b`. :contentReference[oaicite:2]{index=2}
- Run model interactively: `ollama run dolphin3:latest` (or `dolphin3:8b`).

Notes:
- First `run` may initialize and take a minute while weights load.
- If you want the USB to contain a fully offline Modelfile, copy that Modelfile into the Ollama models location on the host before running.
