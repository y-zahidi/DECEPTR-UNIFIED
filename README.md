# DECEPTR-UNIFIED

**Unified Cyberdeception, DFIR, CTI correlation, and attack-simulation platform design and architecture overview.**

![status](https://img.shields.io/badge/status-active-5cf2c1?labelColor=0a0e14)
![license](https://img.shields.io/badge/license-MIT-5cf2c1?labelColor=0a0e14)
![platform](https://img.shields.io/badge/platform-FastAPI%20%7C%20OpenCTI-5cf2c1?labelColor=0a0e14)

> [!NOTE]
> This repository serves as a showcase of the project design, architecture, and configuration snapshots for portfolio purposes. The full implementation and codebase are hosted in a private repository.

## What this is

A working security platform that combines four main capabilities, scoped to what runs on a single machine:

- **Cyberdeception** — honeypots (Cowrie, Dionaea, web), canary files, breadcrumbs, fake LDAP/AD, honeyport (SQL/RDP/WinRM), and dynamic deception escalation (6 levels from NO_ACTION to BLOCK).
- **DFIR** — Velociraptor offline collection + forensic reporting with 23 Tier 2/3 analyzers, ATT&CK Navigator export, and chain of custody.
- **Attack simulation** — CALDERA (5 ability categories) + Atomic Red Team (15 techniques) + reproducible validation scripts.
- **CTI correlation** — OpenCTI 6.3.6 with bidirectional DECEPTR↔CTI connectors, AlienVault OTX, and asynchronous enrichment.

## Architecture

![DECEPTR Unified Architecture](docs/architecture-overview.png)

## What lives where

```
.
├── docker-compose.yml              # Full stack (30 services)
├── docker-compose.lite.yml         # Lite version (8 GB RAM)
├── config/
│   ├── deception/                  # Honeypot configs
│   │   └── pipeline_config.example.yml
│   ├── dfir/                       # Velociraptor configs
│   │   └── velociraptor_config.example.yml
│   ├── opencti/                    # OpenCTI connectors
│   │   └── connector_config.example.yml
│   └── attacker/                  # CALDERA configs
│       └── caldera_config.example.yml
├── docs/
│   ├── architecture-unifiee.md     # Detailed architecture
│   ├── DEPLOY_GUIDE.md             # Deployment guide
│   ├── audit.md                    # Technical audit
│   └── architecture-overview.png   # Architecture diagram
└── screenshots/                    # From real deployments
```

## Detections shipped

- **Deception pipeline**: 7-stage processing (normalizer → enricher → correlator → risk_scorer → detector → alerter → responder)
- **Dynamic deception**: 6-level escalation (NO_ACTION → ANALYZE → TARPIT → DEPLOY_DECOY → ESCALATE → BLOCK)
- **DFIR analyzers**: 23 Tier 2/3 analyzers (memory injection, lateral movement, anomaly/beaconing, browser forensics, ransomware playbook, registry/WMI persistence, DNS tunnel, NTFS timeline, prefetch, SRUM, PowerShell forensics, attack reconstruction, YARA)
- **Threat intel**: GeoLite2, VirusTotal, AbuseIPDB, Feodo Tracker, MITRE ATT&CK, MISP client
- **ML anomaly detection**: Beaconing C2 + process tree analysis (stdlib pure)

## Why this stack

- **Deception**: Active defense with realistic decoys and automated response
- **DFIR depth**: Offline collection preserves evidence, bridge enables real-time correlation
- **Attack validation**: CALDERA + Atomic Red Team provide reproducible MITRE ATT&CK validation
- **CTI integration**: OpenCTI provides campaign-level correlation beyond individual alerts
- **Hardening**: All components run with security constraints (no-new-privileges, cap_drop, pids_limit, read_only + tmpfs, CPU/memory limits)

## Dashboard

Unified SOC dashboard with 5 tabs:
- **SOC**: Overall security posture
- **Alertes**: Real-time alerts and incidents
- **CTI**: Threat intelligence feeds and correlations
- **Rapports**: DFIR reports and forensic analysis
- **Infrastructure**: System health and component status

## Lessons learned

- Deception effectiveness depends on realistic decoys and proper placement
- DFIR bridge requires careful schema mapping and anti-replay protection
- CTI enrichment must be asynchronous to avoid pipeline blocking
- Hardening Docker containers is essential for production deployment
- Testing E2E scenarios validates the entire detection chain

## Roadmap

- [ ] Additional honeypot types (RDP, SMB, HTTP advanced)
- [ ] More DFIR analyzers (cloud forensics, mobile)
- [ ] Extended CTI connectors (more threat feeds)
- [ ] Improved ML models for anomaly detection
- [ ] Automated deployment scripts

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Academic project — 2026.

