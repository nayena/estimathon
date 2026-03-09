# Estimathon Scoring Dashboard

A web-based scoring dashboard for running [Estimathon](https://en.wikipedia.org/wiki/Estimathon) competitions with up to 10 teams.

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

- **30-minute countdown timer** with start, pause, and reset controls — changes color as time runs low
- **Admin panel** to enter correct answers and each team's `[min, max]` intervals
- **Live scoreboard** with automatic ranking, good/bad indicators per problem, and gold/silver/bronze highlighting
- **Reveal button** for a dramatic final rankings animation (last place to first)
- **Editable team names**
- **Mobile-friendly** responsive layout
- **Zero dependencies** — single HTML file, no build step, no backend

## Usage

1. Open `index.html` in any browser
2. Start the timer when the competition begins
3. During the game, switch to the **Admin** tab to enter team intervals as they submit
4. After time is up, enter the correct answers at the top of the Admin panel
5. Switch to the **Scoreboard** tab to see live rankings
6. Click **Reveal Final Rankings** for a dramatic reveal

## Tech

Single vanilla HTML/CSS/JS file. All state is stored in memory — just refresh to reset.
