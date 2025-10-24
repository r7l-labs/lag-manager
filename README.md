# Lag Manager

Lightweight lag mitigation for Minecraft servers (R7L Suite). Monitors server TPS and clears dropped items / experience or forces GC when TPS falls below a configurable threshold.

## Features
- Periodic TPS sampling and automatic mitigation
- Manual commands for admins:
  - /tpsinfo — show last TPS sample and last mitigation
  - /tpsinfo gc — trigger GC + entity clear (admin)
  - /tpsinfo clear — clear dropped items / XP (admin)
  - /tpsinfo threshold <value> — set TPS threshold (admin)

## Configuration
Edit constants in main.py to adjust behavior:
- `CHECK_INTERVAL_TICKS` — how often to check TPS
- `INITIAL_DELAY_TICKS` — start delay
- `TPS_THRESHOLD` — below this triggers mitigation
- `MIN_TPS_TO_SKIP` — skip mitigation if TPS is very high
- `CLEAR_ENTITY_CLASSES` — classes to remove
- `VERBOSE`, `ADMIN_PERMISSION`

## Important symbols (see implementation in main.py)
- Monitoring and sampling: [`get_tps_values`](main.py)
- Entity clearing: [`clear_entities`](main.py)
- Mitigation runner: [`run_mitigation`](main.py)
- Scheduled task: [`tps_check_task`](main.py)
- Command handler: [`tps_command`](main.py)
- Safe registration wrapper: [`safe_tps_command`](main.py)

## Installation
Place `main.py` into your pyspigot plugin environment (follow your server's pyspigot packaging steps). Restart the server; the plugin will:
- schedule the TPS check task on load
- register the `/tpsinfo` command and aliases

## Notes
- The plugin attempts cross-version compatibility for TPS retrieval.
- Admin checks use `ADMIN_PERMISSION` and op status.
