# Family Quiz Night 🎉

A family quiz app that installs on your phones from a web link. It has two ways to play:

- **Pass & Play**: one screen that you hand round. Works straight away, even offline.
- **Multi-screen**: one screen hosts (TV, laptop or tablet) and everyone answers on their own phone. It needs a free Firebase database (part 2). Nobody needs an account to play.

---

## Part 1: Put the app online with GitHub Pages (about 10 minutes)

1. Go to **github.com** and create a free account. Remember your username.
2. Click **+** (top right), then **New repository**.
   - Repository name: `quiz-night`
   - Choose **Public**
   - Click **Create repository**
3. On the next page, click the link **"uploading an existing file"**.
4. Drag **all the files from this folder** into the browser window (not the folder itself, the files inside it), then click **Commit changes**.
5. Go to **Settings**, then **Pages** (in the left menu).
   - Under *Build and deployment*, set Source: **Deploy from a branch**
   - Branch: **main**, folder **/ (root)**, then click **Save**
6. Wait 1–2 minutes and refresh the page. A link like this appears at the top:
   `https://YOUR-USERNAME.github.io/quiz-night/`

That's your app. **Pass & Play already works.**

## Part 2: Turn on multi-screen with Firebase (about 15 minutes)

1. Go to **console.firebase.google.com** and sign in with a Google account.
2. Click **Create a project** and name it `quiz-night`. You can turn Google Analytics off. Then click **Create project**.
3. In the left menu, open **Build**, then **Realtime Database**, then click **Create Database**.
   - Location: **Belgium (europe-west1)** is closest to Iceland
   - Choose **Start in locked mode**, then click **Enable**
4. Open the **Rules** tab, delete everything there, paste in the contents of `database.rules.json`, and click **Publish**.
5. Click the ⚙️ gear (top left), then **Project settings**. Scroll down to *Your apps* and click the **`</>`** (Web) icon.
   - App nickname: `quiz-night`. Leave Hosting unticked. Click **Register app**.
   - Firebase now shows a block of code containing `const firebaseConfig = { ... }`. Keep that page open.
6. Back on GitHub, open your `quiz-night` repository and click **firebase-config.js**, then the ✏️ pencil icon (Edit).
   Replace each `PASTE_...` value with the matching value from Firebase. Keep the quotes, for example:
   ```js
   databaseURL: "https://quiz-night-xxxxx-default-rtdb.europe-west1.firebasedatabase.app",
   ```
   If Firebase's code has no `databaseURL` line, copy the address shown at the top of the **Realtime Database** page instead.
   Click **Commit changes**.
7. Wait a minute, then reload the app. **Host a game** and **Join a game** now work.

## Part 3: Install on everyone's phones

Open your app link on each phone:

- **iPhone (Safari):** tap Share ⬆️, then **Add to Home Screen**
- **Android (Chrome):** tap ⋮, then **Install app** (or **Add to Home screen**)

The app gets its own icon and opens full screen.

## Playing multi-screen

1. On the TV or laptop, tap **Host a game**. A 4-letter code appears.
2. On each phone, tap **Join a game**, then type the code, a name, a face and a level.
3. The host can also play from the host screen: turn on **Host plays too?**
4. Press **Start**. Everyone gets their own question at their own level. A right answer is worth 10 points, plus up to 5 extra for speed.

## Adding your own questions

Open `questions.js` on GitHub and click ✏️. Each question is one line:

```js
["iceland","What is the name of our dog?","Kátur","Snati","Lappi","Bangsi"],
```

The order is: category, question, **right answer**, then three wrong answers. Add the line to the `BANK.e.push(` (Easy), `BANK.m.push(` (Medium) or `BANK.h.push(` (Hard) list. Each line must end with a comma.
Categories you can use: science, nature, geo, iceland, music, history, sports, food, misc, space, body, tech, words, movies, art.

**After changing any file**, open `sw.js` and change `quiz-night-v1` to `quiz-night-v2` (then v3, and so on). That makes the phones fetch the new version.

## Good to know

- Free: GitHub Pages and Firebase's free plan are more than enough for a family.
- The Firebase settings in `firebase-config.js` are not secret passwords. They only point the app at your database.
- Anyone who knows your app link could start a game, but games are deleted when the host leaves, and nothing personal is stored.
