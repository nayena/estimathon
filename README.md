# Estimathon Scoring Dashboard

A web-based scoring dashboard for running [Estimathon](https://en.wikipedia.org/wiki/Estimathon) competitions with up to 10 teams. Supports **real-time multiplayer** — multiple admins can enter data simultaneously, and players see a live scoreboard.

## What is an Estimathon?

An Estimathon is a team-based math competition where teams estimate answers to 13 Fermi-style problems. Instead of exact answers, teams submit intervals `[min, max]` — the goal is to keep intervals tight while still containing the correct answer. **Lowest score wins.**

## Scoring Formula

```
Score = (10 + Σ⌊max/min⌋ for good intervals) × 2^(13 − number of good intervals)
```

- An interval is **good** if `min ≤ correct answer ≤ max`
- Missing or wrong intervals double the score (the exponent increases)
- Teams can make up to 18 total submissions across all 13 problems (only the last submission per problem counts)

## Features

- **Real-time multiplayer** via Firebase Realtime Database — multiple admins can collaborate simultaneously
- **Two modes**:
  - **Admin** — full access: enter answers, team intervals, control timer
  - **Player** — scoreboard only: sees rankings, scores, timer (no answers or intervals visible)
- **30-minute synced countdown timer** — all devices stay in sync
- **Live scoreboard** with automatic ranking and gold/silver/bronze highlighting
- **Reveal button** for a dramatic final rankings animation
- **Connection status indicator**
- **Mobile-friendly** responsive layout
- **Zero backend** — just a single HTML file + free Firebase project

## Setup

### 1. Create a Firebase Project (free)

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click **Add Project** and follow the prompts
3. In the left sidebar, go to **Build → Realtime Database**
4. Click **Create Database**, choose any region, and start in **test mode**
5. Go to **Project Settings** (gear icon) → **General** → scroll to **Your apps**
6. Click the web icon (`</>`) to add a web app
7. Copy the `firebaseConfig` object

### 2. Open the Dashboard

1. Open `index.html` in a browser
2. Paste your Firebase config JSON into the setup screen
3. Enter a room name (e.g., `estimathon-2026`) — all users must use the same room
4. Click **Join as Admin** or **Join as Player**

### 3. Share with Others

- **Admins**: Share the HTML file + Firebase config. Each admin joins with "Join as Admin"
- **Players**: Share the HTML file + Firebase config. Players join with "Join as Player" to see only the scoreboard

You can also use URL parameters to auto-connect:
```
index.html?config=BASE64_CONFIG&room=my-room&mode=player
```
Where `BASE64_CONFIG` is your Firebase config JSON encoded as base64.

### 4. Run the Competition

1. Admins start the timer when the competition begins
2. During the game, admins enter team intervals in the Admin tab (multiple admins can work on different teams simultaneously)
3. After time is up, enter the correct answers at the top of the Admin tab
4. Players see live score updates on the Scoreboard tab
5. Click **Reveal Final Rankings** for a dramatic reveal

## Security Note

For a competition, Firebase test-mode rules (`".read": true, ".write": true`) are fine. For production use, consider adding authentication and tighter security rules.

## Tech

Single vanilla HTML/CSS/JS file with Firebase Realtime Database SDK loaded from CDN. All game state syncs in real-time across all connected devices.
