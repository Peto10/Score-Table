# Score table

Two-window app to run on localhost:
- **Display (public scoreboard)**: `/display_score`
- **Control panel (admin)**: `/control_panel`

## Quick start (Docker)

```bash
docker compose up -d --build
```

If `8080` is busy:

```bash
HOST_PORT=8090 docker compose up -d --build
```

Open:
- `http://localhost:8080/display_score` (or `http://localhost:8090/display_score`)
- `http://localhost:8080/control_panel/` (or `http://localhost:8090/control_panel/`)

Data persists in `./data/app.db` (SQLite).

## Config (`config/teams.yaml`)

Teams/players and timer defaults live in `config/teams.yaml` (ignored by git).

First time setup:

```bash
cp config/teams.example.yaml config/teams.yaml
```

```yaml
timer:
  default_minutes: 15
  default_seconds: 0
  show_by_default: true

teams:
  - id: team_red
    name: "Red Rockets"
    players:
      - id: red_alex
        name: "Alex"
      - id: red_ben
        name: "Ben"
```


## Functionality

- **Live scoreboard**: `/display_score` updates automatically (no refresh).
- **Start match**: pick two teams and start from `/control_panel/`.
- **Add/remove goals**: `+` / `-` per player in active match.
- **Store matches**: writes match + goal rows into SQLite.
- **Timer**: start/pause, reset, set minutes/seconds, show/hide.
- **Swap display sides**: flip left/right teams on the public display.
- **Match history**: list saved matches and delete them (with confirmation).
- **Edit match**: open a saved match and adjust goals.
- **Player stats matrix**: player goals per opponent team + TOTAL.

