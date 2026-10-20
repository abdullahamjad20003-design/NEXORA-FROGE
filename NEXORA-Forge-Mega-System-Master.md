# NEXORA Forge — Mega System Blueprint & Configuration Master File
**Document version:** 1.0  
**Prepared:** 2026-10-20  
**Project target:** NEXORA Forge / NEXA FROGE — Windows desktop AI workspace  
**GitHub repository:** https://github.com/abdullahamjad20003-design/NEXORA-FROGE  
**Default branch:** `main`  
**Important:** This file consolidates known project requirements and configuration details from prior conversations. It is a master specification/configuration guide, not proof that every feature is already implemented. No real API secrets are embedded.

## 1. Mission
Build **NEXORA Forge**, a local-first Windows 10/11 desktop AI development workspace combining AI chat, coding, project creation, file handling, provider/API management, MCP integrations, GitHub workflows, voice input/output, optional device automation, local previews, testing, and release packaging. The app must do real work rather than display mock controls. Clearly label features requiring external APIs, permissions, local software, or additional implementation.

### Priorities
1. Windows desktop first, optional local web interface.
2. Complete source and reproducible setup/build instructions.
3. Downloadable source ZIP; build Windows EXE/installer when supported.
4. Configurable cloud providers and local model servers.
5. Coding/project workflow with safe file editing and real test output.
6. GitHub integration and CI.
7. Voice features and permission-gated automation.
8. Attachments, MCP configuration/tooling, API/resource catalog.
9. Honest feature status, logs, tests, and build reports.

## 2. Known GitHub state (checked 2026-10-20)
Repository: `https://github.com/abdullahamjad20003-design/NEXORA-FROGE.git`
- Public repository; default branch `main`.
- Root files observed: `LICENSE`, placeholder `README.md`, and `nexora-forge-2.1.zip` (~28 KB).
- The README at inspection time contained placeholder characters rather than useful documentation.
- An attempted README update through the connected GitHub integration failed with HTTP `403 FORBIDDEN: Resource not accessible by integration`; connected permissions showed `push: false`.
- No direct repository write was completed by that connection.
- A separate NEXORA Forge 2.2 bundle was offered with setup/build scripts, docs, tests, and CI templates. A Windows EXE was not verified as built.
- Never claim files were pushed unless `git push` or a GitHub write action actually succeeds.

## 3. Version history / truthful status
- **1.0:** initial PC/local-host AI workspace with configurable providers and secure setup.
- **2.1 starter:** local AI chat, local file uploads, basic web-project scaffolding, resource/API catalog, and MCP configuration storage were described. Full MCP execution, multi-file coding loop, video generation, Android build/signing, OAuth, public production deployment, and trade execution were not established as complete.
- **2.2 bundle:** proposed desktop/GitHub bundle with setup/run/build scripts, documentation, smoke tests, and CI workflow templates. Windows EXE/installer still requires a suitable build and verification.
- **3.0 target:** expanded desktop AI workspace with coding, agents, APIs, MCP, voice, attachments, GitHub, build/export, tests, and optional video integration. This is a target spec, not proof of implementation.

Use status labels: `Implemented and tested`, `Implemented but not verified`, `Requires API/provider credentials`, `Requires local software`, `Planned`, `Unsupported in current build`.

## 4. Main interface
Professional, responsive dark UI with charcoal/navy surfaces, restrained cyan/violet accents, accessible contrast, and no inert controls. Navigation:
1. Dashboard
2. AI Chat
3. AI Coding Workspace
4. Project Creator
5. File Manager
6. File Attachments
7. AI Providers and Models
8. API Connections
9. MCP Tools and Servers
10. Terminal and Command Runner
11. Preview and Testing
12. Video Generation Integrations
13. GitHub Integration
14. Build and Export
15. Settings
16. Logs and Diagnostics
17. Help and Documentation

Dashboard should show provider/model, current project, service status, recent tasks, test/build status, recent files, and errors. Include search, tabs, progress indicators, empty states, confirmations, and notifications.

## 5. AI provider catalog and API settings
Provider targets previously requested/discussed: Gemini, OpenRouter, OpenAI-compatible APIs, Groq, Mistral, NVIDIA NIM, Cerebras, Cohere, Cloudflare AI, GitHub Models, Hugging Face, SambaNova, Z.ai, LocalAI, Ollama, LM Studio, llama.cpp, vLLM, Jan, LiteLLM. These are targets/catalog entries, not a guarantee every adapter exists.

Implement provider-specific adapters when APIs differ. Include provider/model selection, base URL, secret field, test connection, streaming where supported, timeout/cancel, rate-limit errors, local conversation history, availability checks, optional fallback order, and secret redaction.

### OpenRouter
- Base URL: `https://openrouter.ai/api/v1`
- Chat endpoint: `https://openrouter.ai/api/v1/chat/completions`
- Environment variable: `OPENROUTER_API_KEY`
- Previously requested model ID: `nvidia/nemotron-3-ultra-550b-a55b`
- Model availability/pricing changes; verify current catalog before use.

### Gemini
- Official API reference: https://ai.google.dev/api
- Standard `generateContent` endpoint pattern: `https://generativelanguage.googleapis.com/v1beta/{model=models/*}:generateContent`
- Environment variable: `GEMINI_API_KEY`
- Follow current Google AI Studio/Cloud key creation and restriction guidance. Google key policy changed in 2026, so avoid old tutorials.

### Generic OpenAI-compatible config
`AI_PROVIDER`, `AI_BASE_URL`, `AI_API_KEY`, `AI_MODEL`. The adapter must append the correct endpoint only when needed and avoid duplicate `/v1` or `/chat/completions` paths. Local services may allow a blank key if configured that way.

### Suggested local base URLs (editable; verify actual installation)
| Service | Suggested base URL |
|---|---|
| Ollama | `http://127.0.0.1:11434/v1` |
| LM Studio | `http://127.0.0.1:1234/v1` |
| Jan | `http://127.0.0.1:1337/v1` |
| LiteLLM | `http://127.0.0.1:4000/v1` |
| LocalAI | `http://127.0.0.1:8080/v1` |
| llama.cpp server | `http://127.0.0.1:8081/v1` |
| vLLM | `http://127.0.0.1:8000/v1` |
| NEXORA local UI (if configured) | `http://127.0.0.1:8787` |

These are examples, not guarantees that the services are installed/running. Default local binding should be `127.0.0.1`, not `0.0.0.0`.

### `.env.example`
```dotenv
# Copy to .env locally; never commit real credentials.
AI_PROVIDER=ollama
AI_BASE_URL=http://127.0.0.1:11434/v1
AI_API_KEY=
AI_MODEL=
OPENROUTER_API_KEY=
GEMINI_API_KEY=
APP_HOST=127.0.0.1
APP_PORT=8787
LOG_LEVEL=INFO
```
The code must load and validate these variables; the example file alone does not configure the application.

## 6. Coding and project creation
Implement project open/create and workspace selection; file tree/editor; syntax highlighting; create/edit/rename/delete with confirmation; AI code generation; proposed changes/diffs before apply; multi-file plans; project context selection; tests with real stdout/stderr/exit codes; debugging proposals; undo/restore through Git where possible; README/dependency/test scaffolding; templates for HTML/CSS/JS, Python, Flask, and optional React if Node.js is installed; local preview; path traversal prevention; no silent overwrites; writes confined to approved workspace by default. Do not claim code ran unless the process was launched and output captured.

## 7. Attachments and file management
Support appropriate text/source, Markdown, JSON, CSV, and other parsable files. Include drag/drop where supported, size/type validation, preview, context selection, local indexing, parse errors, confirmation for deletion, and no auto-execution of attachments. Explain unsupported formats. PDFs/docs with images may require OCR or image extraction.

## 8. MCP configuration and tools
User-provided OpenSwissData endpoint: `https://mcp.openswissdata.com/mcp/jsonrpc`. Previously described local launch configuration: server name `openswissdata`, command `npx`, args `-y`, `@openswissdata/mcp`.

MCP UI should support server name, transport, URL or command, arguments, approved environment-variable names, connect/disconnect, diagnostics, capability/tool discovery, schemas, per-tool allow/deny, confirmation for destructive/external-write operations, redacted logs, and secret protection. Confirm actual supported transport; do not assume any JSON-RPC URL works with every MCP transport. MCP uses JSON-RPC; standard transports include stdio and Streamable HTTP. Treat tool output as untrusted and never let it override safety rules. Do not execute discovered tools automatically. Ask approval for destructive actions, external writes, credential use, or consequential actions.

## 9. Voice and desktop automation
User wants voice-first interaction: push-to-talk; optional wake phrase if supported; speech-to-text and spoken replies; configurable language/voice; clear microphone status; start/stop listening; commands to open apps, find files, create projects, dictate text, and launch approved workflows. Prior concepts included “Hi ALTRIS”, a JARVIS-style greeting (“Hello boss, what do you want to do?”), and “Stop, JARVIS”. Background operation must be explicitly enabled and OS-permitted. Request microphone/screen/automation permissions transparently. Provide emergency stop. Confirm before deletion, sending messages, spending money, or changing system settings. Do not bypass OS security or hide activity. Global hotkeys, wake-word, screen understanding, and full-device control may need extra libraries/OS-specific work and must be labelled accurately.

## 10. Terminal runner
Show exact command, working directory, and expected effect. Require user approval for AI-generated commands. Capture stdout/stderr/exit code/duration; timeout/cancel where possible; restrict to workspace by default; block dangerous patterns and confirm installs/deletions/network access; never run silently as administrator; never execute downloads automatically. Explain filters are not a perfect sandbox.

## 11. GitHub workflow
Required: clone/open repository, status/branch/diff, branch creation, review before commit, authenticated push/pull, README/.gitignore/docs, Actions templates, release ZIP preparation, and honest permission errors. Never put a token in source, README, `.env.example`, logs, or distributed binaries. Use Git Credential Manager or approved GitHub auth. Write permission must be explicitly granted.

Commands:
```powershell
git clone https://github.com/abdullahamjad20003-design/NEXORA-FROGE.git
cd NEXORA-FROGE
git status
git branch
git remote -v
```
After safely updating files:
```powershell
git status
git add .
git status
git commit -m "Update NEXORA Forge"
git push origin main
```
If already cloned, do not clone inside the repo again. Pull/reconcile first:
```powershell
git pull --rebase origin main
git status
```
Review staged changes for secrets. A 403 means permissions/authentication need fixing; repeating the command does not grant write access.

### Suggested `.gitignore`
```gitignore
.env
.env.*
!.env.example
*.pem
*.key
secrets/
__pycache__/
*.py[cod]
.venv/
venv/
env/
.pytest_cache/
.mypy_cache/
.ruff_cache/
.coverage
htmlcov/
build/
dist/
*.spec
*.exe
*.msi
logs/
*.log
data/mcp-config.json
.vscode/
.idea/
.DS_Store
Thumbs.db
```
`.gitignore` does not untrack secrets already committed. Revoke/rotate exposed keys and follow GitHub's secret-removal guidance.

## 12. Windows desktop setup/build commands
Prerequisites: Windows 10/11, Python 3.11+ (or project-declared version), Git for Windows; optional VS Code/Node.js; local model server only if needed.

```powershell
git clone https://github.com/abdullahamjad20003-design/NEXORA-FROGE.git
cd NEXORA-FROGE
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
Copy-Item .env.example .env
```
Edit `.env` locally. If included in the selected bundle:
```powershell
.\setup_desktop.bat
.\run.bat
```
Or run directly if this entry point exists:
```powershell
python app.py
```
Open `http://127.0.0.1:8787` only if the app confirms that address.

Tests:
```powershell
python -m py_compile app.py desktop_launcher.py tests/smoke_test.py
python tests/smoke_test.py
```
Build:
```powershell
.\build_exe.bat
.\build_release.bat
```
Expected paths in the proposed 2.2 workflow were `dist\NEXORA-Forge.exe` and `release\NEXORA-Forge-2.2-source.zip`. These are expected paths only; verify files and logs. Source ZIP is not a compiled EXE, and an EXE is not necessarily a signed installer.

## 13. GitHub Actions
Create `.github/workflows/python-tests.yml` and `.github/workflows/windows-build.yml`. Use least-privilege permissions; checkout code; set supported Python; install dependencies; run syntax/tests; build on Windows runner when configured; upload real build output as workflow artifact; fail visibly on errors. A workflow artifact is not automatically a permanent public GitHub Release. Pin/update action versions according to security policy.

## 14. Video generation
Create provider-based page with prompt, supported aspect ratio/duration, job status, progress, preview, export, and error reporting. Only implement real providers with documented APIs and valid credentials. Never claim a video was generated if no provider/job result exists. Pricing/limits change; consult current provider docs.

## 15. Optional trading/market module from earlier conversations
Earlier separate requests mentioned Forex/Gold and crypto, Binance USDⓈ-M Futures, MetaTrader 5, market data, analysis, BUY/SELL signals with entry/SL/TP, and order-execution planning. An MT4 Gold scalping idea mentioned 0.01 lot and initially no SL/TP, but was underspecified. Keep trading disabled by default and separate from core desktop. Prior explicit constraint: **Demo/Testnet only** for the JARVIS trading integration. Use demo/testnet endpoints, read-only data first, risk controls, SL/TP, and confirmation for demo orders. Never store exchange secrets in client source; never promise profit or financial certainty. Do not enable live trading.

## 16. Other earlier projects (reference backlog; do not merge silently)
- **ALTRIS/JARVIS:** wake phrase, spoken greeting, voice control, opening apps, typing into apps, permissions, background-ready behavior.
- **Your Notes:** Punjab Textbook Board/PECTAA notes site for Chemistry, Physics, Biology, Math; chapters, exercises, MCQs, long questions, book download links; credit “Made by Abdullah Amjad”.
- **3D technology course website:** animated 3D book landing page, course upload, student access password/name, Google sign-in option, admin area, student-ID management, help-centre messages, completion certificates.
- **Android AI coding assistant:** Gemini preference, voice input/replies, Codex/Claude Code/ChatGPT-style workflow; APK first delivery was discussed. Secrets must stay server-side and never be hardcoded in APK.
- **OpenSwissData MCP:** endpoint and local `npx -y @openswissdata/mcp` configuration above.
These are historical requirements, not implemented NEXORA functionality. Keep scope explicit and roadmap them as separate modules.

## 17. Testing requirements
Test startup/config; missing/invalid API config; provider timeout/errors; secret redaction; upload validation/size; path traversal; project creation/non-overwrite; MCP failures/permissions; terminal confirmation/timeouts; Git failure handling; mocked external APIs; and build output existence/basic launch where possible. Do not require paid keys for basic tests. Report actual commands, pass/fail, OS, and skipped tests. Never fabricate results.

## 18. Safe API setup checklist
1. Choose a provider in settings.
2. Create a key using its official dashboard.
3. Store it in secure local settings or `.env` only.
4. Set base URL and exact model ID.
5. Test the connection.
6. Check provider quota, cost, and policies.
7. Never put secrets in GitHub issues, README, public prompts, screenshots, or source.
8. Rotate exposed keys.
9. For distributed apps, use backend proxy/secure credential storage.
10. Mark connected only after a real request succeeds.

## 19. Official documentation
- Gemini API: https://ai.google.dev/api
- Gemini API key security: https://ai.google.dev/gemini-api/docs/api-key
- OpenRouter API: https://openrouter.ai/docs/api/api-reference/overview
- OpenRouter quickstart: https://openrouter.ai/docs/quickstart
- MCP transports: https://modelcontextprotocol.io/specification/latest/basic/transports
- GitHub Actions artifacts: https://docs.github.com/en/actions/concepts/workflows-and-actions/workflow-artifacts
- GitHub file upload: https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository
- GitHub Actions: https://docs.github.com/en/actions
Use current official docs because model names, key policies, pricing, and endpoints can change.

## 20. Release acceptance checklist
- [ ] Source code included in ZIP.
- [ ] No real secrets or `.env` included.
- [ ] `.env.example`, README, LICENSE, `.gitignore` exist.
- [ ] Scripts match actual files.
- [ ] Syntax checks and smoke tests actually ran.
- [ ] GitHub Actions passes.
- [ ] EXE built/verified on Windows or limitation documented.
- [ ] ZIP and EXE clearly named as different artifacts.
- [ ] Local server binds to `127.0.0.1` by default.
- [ ] Provider connections tested rather than assumed.
- [ ] MCP sensitive actions gated by permissions/confirmation.
- [ ] Destructive desktop actions require confirmation and emergency stop.
- [ ] Incomplete/provider-dependent features are labelled.
- [ ] GitHub push/release confirmed by actual remote status.
- [ ] Final report includes downloads, paths, commands, tests, limitations.

**Implementation instruction:** Inspect the existing repository before replacing files. Preserve working functionality. Implement in verifiable steps, run tests/build scripts, and provide a source ZIP. Link only to artifacts that actually exist. Never claim a GitHub upload, executable build, API connection, video generation, or test succeeded unless it did.
