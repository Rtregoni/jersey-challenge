# FOOLPROOF SETUP — 32 JERSEY CHALLENGE

This guide assumes you have never built a website before.

You need:
1. A free GitHub account.
2. A free Firebase account.
3. The ZIP file supplied with this guide.
4. About 15–25 minutes.

No coding is required. You will copy and paste one Firebase configuration block.

---

## PART 1 — Create the Firebase project

### 1. Open Firebase

Go to:
https://console.firebase.google.com/

Sign in with your Google account.

Click **Create a Firebase project**.

Name it:

`32 Jersey Challenge`

You can leave Google Analytics OFF.

Click **Create project**.

---

## PART 2 — Add the web app

Inside your new Firebase project:

1. Click the **Web** icon (`</>`).
2. App nickname:
   `Jersey Challenge`
3. Do NOT enable Firebase Hosting.
4. Click **Register app**.

Firebase will show you a block of code containing:

`apiKey`
`authDomain`
`databaseURL`
`projectId`
`storageBucket`
`messagingSenderId`
`appId`

KEEP THIS PAGE OPEN.

You will copy these values in Part 5.

Firebase's official web setup documentation confirms that registering the web app provides the configuration object needed to connect your website to Firebase. 

---

## PART 3 — Turn on anonymous sign-in

In Firebase:

1. Click **Authentication**.
2. Click **Sign-in method**.
3. Find **Anonymous**.
4. Click it.
5. Turn on **Enable**.
6. Click **Save**.

This is what allows your friends to play without creating accounts or entering passwords. Firebase describes anonymous authentication as temporary accounts that can access data protected by Firebase Security Rules.

---

## PART 4 — Create the shared database

In Firebase:

1. Click **Realtime Database**.
2. Click **Create Database**.
3. Choose a location.

If you are offered a European location, choose one reasonably close to your players, such as a European region.

4. When asked about security rules, choose **Locked mode**.
5. Click **Enable**.

Firebase's documentation explains that Realtime Database synchronises data between connected clients in real time.

---

## PART 5 — Add the security rules

Download the ZIP and unzip it.

You will see:

`firebase-rules.json`

Open it with Notepad.

It contains:

{
  "rules": {
    "games": {
      "$game": {
        ".read": "auth != null",
        ".write": "auth != null",
        "players": {
          "$player": {
            ".validate": "newData.hasChildren(['name','claims'])",
            "name": { ".validate": "newData.isString() && newData.val().length <= 24" },
            "claims": {
              "$team": { ".validate": "newData.isNumber()" }
            }
          }
        }
      }
    }
  }
}

Copy that entire block.

Back in Firebase:

1. Open **Realtime Database**.
2. Click **Rules**.
3. Delete the existing rules.
4. Paste the rules above.
5. Click **Publish**.

IMPORTANT: do not leave the database in public/test rules.

---

## PART 6 — Put your Firebase details into the app

Open:

`firebase-config.js`

You will see:

apiKey: "PASTE_API_KEY_HERE"

etc.

Replace the placeholders with the values Firebase gave you in Part 2.

For example:

export default {
  apiKey: "AIza...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "your-project",
  storageBucket: "your-project.firebasestorage.app",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};

Do not change the property names.

Save the file.

---

## PART 7 — Create your free website

Go to:
https://github.com/

Create a free account if you don't already have one.

After signing in:

1. Click **+** in the top-right.
2. Click **New repository**.
3. Repository name:

`jersey-challenge`

4. Choose **Public**.
5. Click **Create repository**.

GitHub Pages is available for public repositories on GitHub Free.

---

## PART 8 — Upload the files

Open your new `jersey-challenge` repository.

Click:

**Add file → Upload files**

From the ZIP, upload these files:

`index.html`
`host.html`
`firebase-config.js`
`firebase-rules.json`
`README.md`

DO NOT upload the ZIP itself.

Click **Commit changes**.

---

## PART 9 — Turn on GitHub Pages

Inside your GitHub repository:

1. Click **Settings**.
2. Click **Pages** in the left-hand menu.
3. Under **Build and deployment**, find **Source**.
4. Select:

`Deploy from a branch`

5. Branch:
   `main`
6. Folder:
   `/ (root)`
7. Click **Save**.

Wait a few minutes.

GitHub will display a website address similar to:

`https://YOURUSERNAME.github.io/jersey-challenge/`

GitHub says publishing can take up to around 10 minutes after changes are pushed.

---

# PART 10 — CREATE YOUR GAME

Open:

`https://YOURUSERNAME.github.io/jersey-challenge/host.html`

Replace YOURUSERNAME with your GitHub username.

Enter:

Game code:
`LONDON26`

Game title:
`NFL London 2026`

Click:

**Create Game**

You should see a confirmation.

---

# PART 11 — TEST IT BEFORE THE DAY

Open your main website:

`https://YOURUSERNAME.github.io/jersey-challenge/`

Enter:

Name:
`Ross`

Game code:
`LONDON26`

Click **Join**.

You should see the 32 teams.

Open the same website in another browser/device.

Enter:

Name:
`Test Player`

Game code:
`LONDON26`

Click **Join**.

Now claim a team on one device.

The other device should immediately show the updated leaderboard.

If that works, you're ready.

---

# PART 12 — SEND IT TO YOUR FRIENDS

Put this in your WhatsApp group:

🏈 **32 JERSEY CHALLENGE**

We're hunting all 32 NFL teams.

Join here:
YOUR WEBSITE URL

Game code:
**LONDON26**

Enter your own name when you join.

Rules:
• You need to actually spot the team.
• Each team can be claimed once by each player.
• Photos are optional.
• First person to find all 32 wins.
• Don't count team logos on adverts, phones or screens.
• Jerseys, shirts, hoodies, hats or other clearly identifiable team gear count.

---

# HOW THE GAME WORKS

Each player has their own 32-team checklist.

If Ross spots the Packers:
Ross → Packers = ✓

Dave can still spot the Packers:
Dave → Packers = ✓

So the same team can be found by all 8 players.

The leaderboard shows everyone's individual progress.

"Most Wanted" shows teams nobody has found yet.

---

# PHOTO RULE

The app deliberately does NOT upload photos.

If you want evidence:

1. Open your phone camera.
2. Take the photo.
3. Claim the team in the app.

The photo remains in your normal phone photos.

This keeps the app simpler, more private and cheaper to operate.

---

# IF SOMETHING DOESN'T WORK

### "That game code doesn't exist"

Go to:

`host.html`

Create the game first.

Then try joining again.

### "Couldn't connect"

Check:

1. Firebase Authentication → Anonymous is enabled.
2. Realtime Database exists.
3. The Firebase config in `firebase-config.js` is correct.
4. The Firebase Rules have been published.
5. The website is being opened through GitHub Pages, not by double-clicking `index.html`.

### The website shows old content

Wait a few minutes and refresh.

GitHub Pages can take time to publish changes.

### The leaderboard doesn't update

Check the Firebase Realtime Database console.

If players are appearing under:

`games → LONDON26 → players`

then Firebase is working.

---

# IMPORTANT

The Firebase configuration in `firebase-config.js` is designed to be used by a browser app. Do NOT put a Firebase Admin SDK private key, service-account JSON file or other server secret into this website.

Only use the normal Firebase Web App configuration.

---

# BEFORE THE EVENT

Do one complete rehearsal:

1. Create a test game.
2. Join as Player 1.
3. Join as Player 2 on another phone.
4. Claim different teams.
5. Confirm both phones update.
6. Delete the test game in Firebase.
7. Create your real London game.

Then send the link to your WhatsApp group.

You should not need to touch the Firebase console during the actual game.
