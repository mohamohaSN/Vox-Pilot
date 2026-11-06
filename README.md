# Vox-Pilot
A lightweight local voice assistant built with Python and PowerShell, designed for AI-powered conversations and carefully controlled system automation.
# Local Voice Agent

> A lightweight, extensible voice assistant for local automation and AI-powered conversations.

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![PowerShell](https://img.shields.io/badge/PowerShell-7%2B-5391FE?logo=powershell&logoColor=white)](https://learn.microsoft.com/powershell/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Local Voice Agent** is an open-source project exploring how a local conversational assistant can understand voice input, interact with AI APIs, and perform carefully controlled system automation. It is designed as a lightweight, approachable starting point for developers and AI students.

> **Project status:** Early development. Features, commands, and setup details may change. Review every automation action before enabling it on your machine.

## Goals

- Make voice-driven automation approachable for developers and students.
- Keep the core lightweight and modular so components can be replaced.
- Support Python for assistant logic and PowerShell for Windows automation.
- Make API usage and system actions explicit, configurable, and easy to audit.
- Grow through documentation, examples, and community contributions.

## Features

The repository is intended to support the following capabilities as they are implemented:

- Voice input and conversational interaction.
- A modular assistant core that can connect to AI APIs.
- Optional speech-to-text and text-to-speech integrations.
- A command/skill system for adding automation tasks.
- PowerShell scripts for supported Windows actions.
- Configuration through environment variables, with secrets kept out of source control.
- A local-first workflow where API-dependent features can be configured separately.

See [Roadmap](#roadmap) for a suggested implementation order. Do not assume a listed capability is implemented until it is available in the codebase.

## Requirements

- Python 3.11 or later.
- PowerShell 7 or later for PowerShell automation (Windows-specific actions require Windows).
- Git.
- An API key only if you enable an AI provider that requires one.
- Microphone and audio output for voice features.

## Installation and launch

### Installation (en français)

1. **Cloner le dépôt et entrer dans le dossier :**

   ```powershell
   git clone https://github.com/<your-username>/<your-repository>.git
   cd <your-repository>
   ```

2. **Créer puis activer un environnement virtuel Python :**

   ```powershell
   py -3.11 -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   Si PowerShell bloque l’activation, vous pouvez lancer la session avec une politique adaptée à votre environnement, ou utiliser directement `\.venv\Scripts\python.exe` sans activer l’environnement.

3. **Installer les dépendances**, une fois le fichier `requirements.txt` ajouté au projet :

   ```powershell
   python -m pip install --upgrade pip
   python -m pip install -r requirements.txt
   ```

4. **Configurer les variables d’environnement :** copiez `.env.example` vers `.env`, puis renseignez uniquement les clés nécessaires au fournisseur choisi. Ne publiez jamais `.env` ni une clé API dans GitHub.

5. **Lancer l’assistant** (adaptez le point d’entrée à l’implémentation du dépôt) :

   ```powershell
    $env:PYTHONPATH = "src"
   python -m local_voice_agent
   ```

   La commande ci-dessus suppose que le paquet `src/local_voice_agent` et son point d’entrée `__main__.py` ont été créés. Consultez l’aide du projet (`python -m local_voice_agent --help`, si elle est disponible) pour connaître les commandes réellement prises en charge.

### Development on other platforms

The Python components can be developed on other platforms, but the PowerShell automation examples and Windows-specific actions require a compatible Windows environment. Use `pwsh` to invoke PowerShell 7 where appropriate.

## Configuration

Keep local settings in `.env` or another ignored configuration file. A future `.env.example` may document variable names without real credentials, for example:

```dotenv
AI_PROVIDER=
AI_API_KEY=
```

Only add variables that the implementation actually reads. Never commit real credentials, personal data, or machine-specific configuration. Prefer explicit allowlists and confirmation prompts for actions that modify files, settings, or other system state.

## Suggested repository structure

```text
.
├── .github/
│   ├── ISSUE_TEMPLATE/
│   └── workflows/
├── docs/                    # Setup notes, design decisions, supported actions
├── scripts/
│   └── powershell/          # Reviewed PowerShell automation scripts
├── src/
│   └── local_voice_agent/
│       ├── __init__.py
│       ├── __main__.py      # `python -m local_voice_agent` entry point
│       ├── assistant.py     # Conversation orchestration
│       ├── config.py        # Environment and settings
│       ├── audio/           # Speech input/output adapters
│       ├── providers/       # AI API provider adapters
│       └── skills/          # Explicitly registered automation actions
├── tests/                   # Unit and integration tests
├── .env.example             # Names of required settings; no secrets
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt         # Or pyproject.toml when packaging is introduced
```

This is a starting point, not a claim that these files already exist. Keep each integration optional where practical, and document platform-specific behavior.

## Safety and privacy

A voice assistant that can run system commands should be treated as privileged software. Start with read-only actions, use a small allowlist of commands, validate all input, and require confirmation before destructive or sensitive operations. Never pass raw model output directly to a shell. Review scripts before running them and understand what data is sent to any external AI API.

## Contributing

Contributions are welcome, especially documentation, small isolated features, provider adapters, and safety improvements.

1. Open an issue to discuss substantial changes or new automation capabilities.
2. Fork the repository and create a focused branch.
3. Make a small, documented change and add or update tests where relevant.
4. Run the project checks documented in the repository.
5. Open a pull request describing the change, platform tested, and any permissions or API services it needs.

Please do not include API keys, personal recordings, private data, or unreviewed system commands in contributions. Be respectful and follow the project’s code of conduct if one is adopted.

## Roadmap

- [ ] Establish a minimal command-line conversation loop.
- [ ] Add configurable AI provider adapters.
- [ ] Add opt-in speech-to-text and text-to-speech adapters.
- [ ] Define a permissioned skill interface and confirmation flow.
- [ ] Add tests, examples, and platform-specific setup guides.


