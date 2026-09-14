TRAIN — Lia's personal training app
v2.0 · 14/09/2026

One HTML file, no build step. Firebase for the cloud copy, OpenAI for the
coach's words only. Amir PT is untouched.


1. WHAT TO UPLOAD
=================
    index.html
    sw.js
    manifest.json
    icon-180.png
    icon-512.png
    icon-1024.png
    demos/            (the folder — exercise pictures go in here)

Through the GitHub web UI as usual. It runs the moment Netlify deploys.


2. FIRESTORE — ONE PASTE
========================
    console.firebase.google.com
      -> project ptchat-170ff
      -> Build -> Firestore Database -> Rules
      -> paste firestore-rules.txt over what's there -> Publish

That's your existing amirpt rule plus one new liapt block. It changes
nothing about your app.

If you skip it nothing breaks: the first cloud write fails, the app notices
and puts her document inside the existing collection at amirpt/lia-7m2xv4
instead. Still separate, still invisible to your app.
Check which is in use: More -> Settings -> Backup and sync -> Check the
connection.


3. HER COACH — THE API KEY
==========================
    platform.openai.com -> sign in or create an account in her name
      -> Settings -> Billing -> add a card or buy credit
      -> API keys -> Create new secret key -> copy it (shown once)
    In Train: More -> Settings -> Coach -> paste -> Save -> Test the connection

Yours works too — same field, billed to you, and the two coaches still read
different documents. Keep gpt-4o-mini.

The key is stored on her device and is never uploaded with the backup, so if
she also installs it on an iPad, paste it there as well.

WITHOUT A KEY THE APP IS COMPLETE. The programme, the duration scaling, the
check-in adjustments, the neck logic, the cycle logic, load suggestions,
records, swaps, rest timers and the whole workout runner are decided in
code. The key only buys better sentences and a coach that answers questions
and can change the session by name.


4. THE EXERCISE PICTURES
========================
Drop them in the demos folder. Nothing needs registering.

    Hip Thrust                  ->  demos/hip-thrust.jpg
    Romanian Deadlift           ->  demos/romanian-deadlift.jpg
    90/90 Breathing             ->  demos/90-90-breathing.jpg

Lower case, hyphens for spaces and punctuation. jpg, webp, png, gif and mp4
all work — an mp4 plays muted and loops. 4:3 landscape, 1200x900 or larger;
the app crops to fill, so keep the body roughly centred.

Train-exercise-list.xlsx has the exact filename for all 169 movements.

Anything without a picture shows a labelled body map of what the movement
trains, so a half-filled folder never breaks a screen. There is also a
per-exercise URL field (any exercise -> How? -> Add a demonstration) if you
ever want to point at something hosted elsewhere.

Nothing from Instagram or any other subscription is downloaded or embedded.
A movement she likes from Senada Greca or Zubalenok is saved in
More -> My references as a name, a link, a target muscle and a note, and the
coach borrows the movement pattern rather than the content.


5. ON THE PHONE
===============
Open the Netlify URL in Safari -> Share -> Add to Home Screen.


6. WHAT'S IN v2.0
=================
THE SCREENS
  Home is the greeting, the week and today's workout. The check-in is three
  taps — energy, neck, time — with "Say more" opening the full version if
  she wants to log sleep, stress, soreness, pain, cycle and a note.
  The workout screen is a photograph, the prescription, one cue and one blue
  button, with Swap, How?, Skip and More underneath.

PAUSE
  A labelled Pause button sits on screen through the warm-up, every set,
  every timed hold, every rest and the cool-down, and again on the rest
  screen. It stops the workout clock, the rest countdown and the exercise
  countdown together, keeps the exact remainder, and says Resume. Paused
  time never counts toward the session length.

LENGTH
  Quick, Standard, Full or Custom, before or during. A shorter session is
  rebuilt, not truncated: the warm-up, block A, the superset structure and
  the cool-down all survive, rounds come off the back first, and anything
  already logged is kept. The estimate is on screen before Start.

REST
  Four separate timers with their own defaults — the changeover inside a
  superset (20s), between rounds (75s), between straight sets (75s) and
  between blocks (100s) — each configurable, each overridable per block.
  Skip, +15s, −15s, the next movement named, sound and vibration, and it
  survives the phone being locked.

EVERYTHING ELSE RESTORED
  169 movements with easier and harder versions; swap with recommended,
  easier, harder and different-kit sections plus full search by name, muscle
  or equipment; add, remove, reorder, skip and go back; adjust reps, time
  and weight; add kilograms to a reps-only movement; log a hold instead of
  reps; rounds per block; workout history; previous performance; progression
  suggestions she confirms herself; personal records; readiness, pain, neck
  and cycle adjustments; delete, rebuild, and resume an unfinished session
  after a reload; and a coach that can set the length, the rounds, add,
  replace, remove or ban a movement and have Train show it immediately.

BANDS
  21 band movements, and swaps offer them first.

STOPPING, DISCARDING, DELETING
  Three different things, and the sheet says which is which.
    Stop and keep what I did   — ends the session, saves the sets completed
    I didn't actually do this  — the session never happened: every set logged
                                 that day comes out of the strength history,
                                 any record claimed that day is taken back,
                                 the streak is recounted, and a fresh session
                                 takes its place. The check-in is kept.
    Clear today entirely       — no session at all today; rebuild any time
  Reachable from the session menu, from the finished screen, and from any day
  in the calendar or in the workout history. Every one of them leaves an Undo.
