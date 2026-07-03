<div align="center">

<img src="images/logo.png" alt="Edge Mining logo" width="16%" />

# Edge Mining

**Turn excess energy — especially from renewables — into Bitcoin and heat.**

[![Release](https://img.shields.io/github/v/release/edge-mining/app?logo=github)](https://github.com/edge-mining/app/releases)
[![License: MIT](https://img.shields.io/github/license/edge-mining/app)](LICENSE)
[![Docs](https://img.shields.io/badge/docs-edge--mining%2Fdocs-informational)](https://github.com/edge-mining/docs)
[![Website](https://img.shields.io/website?up_message=online&down_message=offline&url=https%3A%2F%2Fedge-mining.github.io%2F&label=website)](https://edge-mining.github.io/)

</div>

> **Disclaimer:** This project is in a preliminary state and under active development. Features and functionality may change significantly.

---

## What is Edge Mining?

Edge Mining is software that optimizes the use of excess energy, especially from renewable sources, through Bitcoin mining. It automates turning ASIC miners on and off based on energy availability, production forecasts, and user-defined policies — consuming surplus power when it is available and stopping the moment it is needed elsewhere.

Because a miner converts virtually 100% of the electricity it draws into heat, that heat can be reused (for example, for space heating), turning otherwise wasted energy into economic value.

For the full rationale — the challenge of managing excess energy and why Bitcoin mining is a flexible, dispatchable load — see the [Edge Mining documentation](https://github.com/edge-mining/docs).

## Features

- **Automated ASIC control** — miners are switched on/off automatically based on real-time energy availability.
- **User-defined policies** — declarative optimization rules written in YAML.
- **Production forecasts** — solar/renewable forecasting driven by your location (latitude/longitude) and sunrise/sunset.
- **Heat reuse** — designed around repurposing the miners' heat output.
- **Web UI, REST API and CLI** — manage miners, energy sources, controllers and policies from a browser, over HTTP, or through an interactive terminal.
- **Home Assistant integration** — via the companion [add-on](https://github.com/edge-mining/addon).
- **Single-container deployment** — backend, frontend and reverse proxy shipped together via Docker Compose.

## Screenshots

<!-- TODO: add screenshots of the Web UI to images/ and reference them here -->

| Dashboard | Policies | Configuration |
| :---: | :---: | :---: |
| _screenshot coming soon_ | _screenshot coming soon_ | _screenshot coming soon_ |

## The Edge Mining ecosystem

Edge Mining is split across a few repositories:

| Repository | Role |
| --- | --- |
| **[`app`](https://github.com/edge-mining/app)** _(you are here)_ | The full application — backend engine, Web UI, REST API and CLI — packaged for Docker deployment. |
| **[`addon`](https://github.com/edge-mining/addon)** | Home Assistant integration. |
| **[`docs`](https://github.com/edge-mining/docs)** | Project documentation: the problem/solution rationale, Domain-Driven Design architecture and glossary. |

## Quick Start

### Prerequisites

- [Git](https://git-scm.com/)
- [Docker](https://docs.docker.com/get-docker/) and Docker Compose

### Install & run

Clone the repository and start the stack with the first-run helper, which initializes `user_data/`, builds the image (backend + frontend + nginx) and brings everything up on port `80`:

```bash
git clone https://github.com/edge-mining/app.git
cd app/
./scripts/first_start.sh
```

Then open:

- **Web UI** — <http://localhost/>
- **API** — <http://localhost/api>
- **API docs** — <http://localhost/docs>

> **Note:** the `user_data/` directory is mounted as a volume, so your database, policies and backups persist across restarts and container rebuilds.

<details>
<summary><strong>Common commands</strong></summary>

```bash
# Start (after the first run, no rebuild)
docker compose up -d

# Follow logs
docker compose logs -f

# Stop the stack
docker compose down

# Rebuild after code changes
docker compose up -d --build

# Open the interactive Core CLI inside the running container
docker compose exec edge-mining python -m edge_mining cli interactive

# Update to the latest version
./scripts/update.sh
```

</details>

For first-run details, environment variables, the interactive CLI, updating, switching branches and troubleshooting, see the **[Installation & Operations guide](docs/INSTALL.md)**.

## Configuration & Data

User-specific data lives in the `user_data/` folder, which is mounted into the container:

- `user_data/policies/` — optimization policy YAML files
- `user_data/examples/` — example rule files (`start/` and `stop/`)
- `user_data/db/edgemining.db` — SQLite database (automatic backups in `user_data/db/backups/`)

Runtime behavior is tuned through a few environment variables (`TIMEZONE`, `LATITUDE`/`LONGITUDE`, `SCHEDULER_INTERVAL_SECONDS`) set in `compose.yaml`.

See the [Installation & Operations guide](docs/INSTALL.md) for the full configuration reference.

## Documentation

| Document | Contents |
| --- | --- |
| [`docs/INSTALL.md`](docs/INSTALL.md) | Full installation, configuration and operations guide |
| [`DEVELOPMENT.md`](DEVELOPMENT.md) | Local development setup and daily workflow |
| [`DEV_TOOLS.md`](DEV_TOOLS.md) | Linting, formatting and testing tools |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Contribution guidelines and PR rules |
| [edge-mining/docs](https://github.com/edge-mining/docs) | Project rationale, DDD architecture and glossary |

## Contributing

Contributions are welcome! Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) before opening a pull request.

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.
