# Contributing to DECEPTR-UNIFIED

Thanks for your interest in contributing! This guide will help you get started.

## Getting started

1. **Fork** the repository
2. **Clone** your fork locally
3. Create a **feature branch** from `main`
4. Make your changes
5. **Test** that `docker compose up -d` still works
6. Submit a **pull request**

## Development setup

```bash
git clone https://github.com/<your-username>/DECEPTR-UNIFIED.git
cd DECEPTR-UNIFIED

# Copy example configs
cp config/deception/pipeline_config.example.yml config/deception/pipeline_config.yml
cp config/opencti/connector_config.example.yml config/opencti/connector_config.yml

# Start the stack
docker compose up -d
```

## Project structure

| Directory | What lives there |
|---|---|
| `config/deception/` | Honeypot and pipeline configuration |
| `config/dfir/` | Velociraptor configuration |
| `config/opencti/` | OpenCTI connector configuration |
| `config/attacker/` | CALDERA configuration |
| `docs/` | Architecture docs and guides |
| `screenshots/` | Dashboard and deployment screenshots |

## Commit messages

Use clear, descriptive commit messages:

```
feat(deception): add SMB canary token detection
fix(bridge): correct HMAC validation on sync endpoint
docs: update architecture diagram
```

## Pull request checklist

- [ ] `docker compose up -d` starts without errors
- [ ] Changes are documented if they affect the user
- [ ] No secrets or credentials are committed
- [ ] `.gitignore` is updated if new generated files are introduced

## Reporting bugs

Use the [bug report template](https://github.com/y-zahidi/DECEPTR-UNIFIED/issues/new?template=bug_report.yml) — it helps triage faster.

## Code of conduct

Be respectful. We're all here to learn and build better security tools.
