# NEXORA Forge — Desktop Setup Guide with Pictures

![NEXORA Forge desktop setup infographic](a_tall_detailed_infographic_poster_guide_image.png)

**Windows 10/11 · GitHub · Python · Tests · EXE build**

## 1. Install prerequisites

- Python: https://www.python.org/downloads/
- Git for Windows: https://git-scm.com/downloads/win
- Optional VS Code: https://code.visualstudio.com/

Select **Add Python to PATH** during Python installation.

```powershell
python --version
git --version
pip --version
```

## 2. Clone the repository

```powershell
cd "$HOME\Downloads"
git clone https://github.com/abdullahamjad20003-design/NEXORA-FROGE.git
cd NEXORA-FROGE
git status
```

If you already cloned the repository, open the existing folder instead of cloning again.

## 3. Create a virtual environment and install dependencies

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If PowerShell blocks activation, use this for the current process only:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

## 4. Configure API settings

```powershell
Copy-Item .env.example .env
notepad .env
```

Example placeholders, if supported by the app:

```dotenv
AI_PROVIDER=ollama
AI_BASE_URL=http://127.0.0.1:11434/v1
AI_API_KEY=
AI_MODEL=
APP_HOST=127.0.0.1
APP_PORT=8787
```

Never commit real keys. Local endpoints require the relevant local server to be installed and running.

## 5. Start the app

```powershell
python app.py
```

Or, if included in your bundle:

```powershell
.\setup_desktop.bat
.\run.bat
```

Open the local address printed by the app. `http://127.0.0.1:8787` is only the expected address for builds configured to use that port.

## 6. Run checks

```powershell
python -m py_compile app.py desktop_launcher.py tests/smoke_test.py
python tests/smoke_test.py
```

## 7. Build the Windows EXE

```powershell
.\build_exe.bat
```

Expected path in the proposed workflow: `dist\NEXORA-Forge.exe`. Verify the file exists and launches.

## 8. Build a release ZIP

```powershell
.\build_release.bat
```

Expected path in the proposed workflow: `release\NEXORA-Forge-2.2-source.zip`. Verify actual output and version.

## 9. Push changes to GitHub

```powershell
git status
git add .
git status
git commit -m "Update NEXORA Forge desktop setup"
git push origin main
```

Review the staged files before committing. Never upload `.env`, access tokens, private keys, or sensitive MCP config. A 403 error requires fixing GitHub authentication/write permissions.

## Troubleshooting

- **Python not found:** install Python with Add Python to PATH, then reopen PowerShell.
- **Git not found:** install Git for Windows, then reopen PowerShell.
- **Missing requirements.txt:** confirm you are in the correct project root.
- **ModuleNotFoundError:** activate `.venv` and install `requirements.txt`.
- **Provider error:** check base URL, model, network, quota, and key validity without printing the key.
- **EXE missing:** inspect the actual build logs and output folder; expected paths do not prove a build succeeded.

## Security

- Keep API keys local and private.
- Bind local servers to `127.0.0.1` by default.
- Require approval before destructive commands and external writes.
- Verify tests, builds, and uploads before claiming success.

Repository: https://github.com/abdullahamjad20003-design/NEXORA-FROGE
