# 32 Jersey Challenge — zero-cost deployment

This is a small multiplayer web app for up to 8 friends.

## What it does

- One shared game room/code
- 8 players can join from their phones
- Each player has an individual 32-team board
- Claims update live for everyone
- Live leaderboard
- "Most Wanted" teams
- Optional photo evidence without uploading/storing photos
- No passwords or paid accounts required for players

## Free stack

- GitHub Pages = website hosting
- Firebase Realtime Database = shared game state
- Firebase Anonymous Authentication = simple player access

GitHub Pages is available on GitHub Free for public repositories.
Firebase's Spark plan provides no-cost quotas for Realtime Database/other Firebase services.

## IMPORTANT: Firebase setup

1. Go to https://console.firebase.google.com/
2. Create a new project, e.g. "32 Jersey Challenge".
3. Add a Web App to the project.
4. In Firebase Console > Build > Realtime Database, create a database.
5. Start in locked/production mode.
6. In Firebase Console > Authentication > Sign-in method, enable "Anonymous".
7. In Realtime Database > Rules, paste the contents of `firebase-rules.json`.
8. In Project settings > Your apps > Web app, copy the Firebase configuration.
9. Replace the placeholder values in `firebase-config.js`.

The app does not use Firebase Storage, so photos are deliberately NOT uploaded.

## Create a host game

Use `host.html` to create a room. Open it after you have uploaded the files and configured Firebase.

Enter:
- Game code, e.g. `LONDON26`
- Game title, e.g. `NFL London 2026`

Click **Create Game**.

Then give everyone the main website URL and the game code.



The simplest zero-code method is to create one document manually in Realtime Database:

games
  LONDON26
    title: "London 2026"
    players: {}

Then share the website URL and code `LONDON26`.

For a cleaner host experience, the next version can add a "Create Game" button that generates the room automatically.

## Publish with GitHub Pages

1. Create a GitHub account if you don't already have one.
2. Create a new PUBLIC repository called `jersey-challenge`.
3. Upload:
   - index.html
   - firebase-config.js
   - firebase-rules.json
4. Open Settings > Pages.
5. Under Build and deployment choose "Deploy from a branch".
6. Select the `main` branch and `/root`.
7. Save.
8. GitHub will give you a `github.io` URL.

It can take a few minutes for the site to appear.

## First use

Open your new URL.

Enter the game code.

The app currently needs a player record in the room. To make the experience cleaner, the recommended next change is adding:
- Create Game
- Join Game
- Host controls
- 8-player cap
- QR code for joining
- automatic random game code
- end-game/winner screen

## Security note

This is intentionally a lightweight game rather than an account system. Do not put personal information into player names. Firebase anonymous authentication is used so the database isn't completely open to unauthenticated users.
