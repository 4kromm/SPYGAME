# SPYGAME

A social deduction game built in **Roblox**, inspired by the classic "Spy vs Villagers" word game. One player is secretly the **Spy** everyone else shares a common word, the Spy gets a related but different one, and the group must find them out through conversation, deduction, and voting before it's too late.

---

##  How It Works

1. Players join a room and vote on a game mode before the round begins
2. Each player is secretly assigned a word all Villagers share the same word, while the Spy gets a different (but related) one
3. Players take turns dropping subtle clues about their word, without saying it outright
4. After a set number of rounds, everyone votes on who they think the Spy is
5. **Villagers win** by voting out the Spy. **The Spy wins** by staying hidden until only 2 players remain or by tricking the group into voting out an innocent player

---

## Features

- **Multiroom support** up to 5 independent rooms (`Room1`–`Room5`) running simultaneously, each with its own isolated game state
- **Mode voting** players vote on the game mode before each match starts
- **Turnbased clue phase** players take turns giving clues via chat, with a live per-turn timer
- **Realtime voting** vote tallies update live for everyone in the room
- **Two layer profanity filter** a custom Indonesian/English blacklist combined with Roblox's built-in `TextService` filter, with bypass-character normalization
- **Coin reward system** rewards scale with win/loss outcome, VIP status, and equipped "Keris" tool rarity (Common through Limited/Crystal)
- **Win streaks & stats** tracks player wins and current streak
- **Persistent data** player coin balances are saved via Roblox `DataStoreService`

---

## Project Structure

```
SPYGAME/
├── SPYGAME.rbxl       # Full Roblox place file (map + all scripts)
├── .gitignore         # Ignores Roblox Studio lock files
└── README.md
```

The core logic lives in the **`GameManager`** script under `ServerScriptService`, which drives the entire game loop — room joining, mode voting, word assignment, turn-based chat, voting, results, rewards, and game reset independently for each room.

### Required Workspace Setup

| Location | Contents |
|---|---|
| `ReplicatedStorage` | ModuleScript `GameConfig`; BindableFunctions `AddWin`, `AddStreak`, `ResetStreak` |
| `Workspace` | `SpawnLocation`; five rooms (`Room1`–`Room5`) each with seats, a `StartPart`, and a status SurfaceGui; five barrier folders (`Barrier`–`Barrier5`) |
| Player instance | `leaderstats.Koin` (IntValue); optional `IsVip` / `IsKerisVip` (BoolValue) |

---

## Tech Stack

- **Roblox Studio** engine & editor
- **Lua / Luau** server-side scripting
- **RemoteEvents** server-client communication (game state, voting, chat, timers)
- **DataStoreService** persistent player coin storage

---

## Getting Started

1. Clone this repository
2. Open `SPYGAME.rbxl` in Roblox Studio
3. Use **Test → Start Server / Local Server** to simulate multiple players (a match requires at least `GameConfig.MIN_PLAYERS` players)

---

## Status

 **Actively in development** currently working through server-client state consistency, UI sequencing, and cross-session timing issues.

---

## Contributors

- [4kromm](https://github.com/4kromm)
