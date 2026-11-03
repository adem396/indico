# Indico Custom

A customized fork of [Indico](https://github.com/indico/indico), the open-source event management system developed at CERN.

> **This is a fork, not an original project.** All credit for Indico goes to CERN and its contributors. This repository keeps the original MIT license and copyright notice (see [LICENSE](LICENSE)).

## What is Indico?

Indico is a web application for managing events such as conferences, meetings and lectures. It handles:

- Event timetables and scheduling
- Abstract submission and review
- Registration forms and payments
- Room booking
- Badges, tickets and certificates
- Plugins to extend it

## What I changed

- **Custom theme (CSS):** a new look for the interface (purple/blue gradient header, rounded buttons, hover effects), loaded through Indico's `CUSTOMIZATION_DIR` setting. The file is in [`customization/css/`](customization/css/).
- _Add your next changes here (for example a plugin, a new route or a new feature), and say exactly what each one does._

## Tech stack

| Part | Technology |
|---|---|
| Backend | Python 3.12, Flask |
| Database | PostgreSQL |
| Cache / task queue | Redis, Celery |
| Frontend | React (JavaScript), SCSS, Jinja2 templates |
| Build tools | webpack, npm, uv |

## Run it locally (Windows + WSL2)

Indico is built for Linux and macOS, so on Windows it runs inside Ubuntu on WSL2.

1. Install Ubuntu: `wsl --install -d Ubuntu` (PowerShell as administrator), then restart.
2. Inside Ubuntu, install the system packages (git, build tools, PostgreSQL, Redis, and the libraries listed in the official guide).
3. Install [`uv`](https://docs.astral.sh/uv/) and Node.js (LTS).
4. Create a PostgreSQL database named `indico` with the `unaccent` and `pg_trgm` extensions.
5. Create the environment and install the dependencies:
   ```bash
   uv venv --python=3.12
   source .venv/bin/activate
   uv pip install -e '.[dev]'
   npm ci
   ```
6. Configure and prepare Indico:
   ```bash
   indico setup wizard --dev
   indico db prepare
   indico i18n compile indico
   ```
7. Add the theme by setting `CUSTOMIZATION_DIR` in `indico.conf` to this repo's `customization/` folder.
8. Start the app and open <http://127.0.0.1:8000>:
   ```bash
   indico run -h 127.0.0.1 -p 8000 -q --enable-evalex
   ```

For the full, official instructions, see the [development installation guide](https://docs.getindico.io/en/latest/installation/development/).

## Project layout

| Folder | Contents |
|---|---|
| `indico/` | The application: Python backend, React frontend, templates |
| `indico/modules/` | The core features (events, rooms, users, and so on) |
| `docs/` | Sphinx documentation |
| `customization/` | My custom CSS |
| `.github/` | CI workflows and templates |

## License and credits

Indico is released under the [MIT License](LICENSE). Copyright (c) European Organization for Nuclear Research (CERN).

This fork keeps that license. The changes listed above are mine, and everything else belongs to the original Indico authors.
