TRAIN — Lia's personal training app
v2.1 · 14/09/2026

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
    demos/            (the folder — 157 exercise pictures, already in it)

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


4. THE EXERCISE PICTURES — ALREADY DONE
=======================================
157 photographs ship in the demos folder, one per movement, and index.html
carries a map from every exercise name to its file. Nothing to set up.

Twelve band variants have no still of their own yet. Each shows the picture
of the movement it is built on with a small label on the card saying so
("Glute Bridge shown — add the band"). demos/README.txt lists the twelve
filenames; drop one in and its label disappears.

To replace a picture, use the filename it already has. To add one for a
movement that has none, name it after the exercise in lower case with
hyphens for spaces and punctuation — hip-thrust.webp, 90-90-breathing.webp.
jpg, webp, png, gif and mp4 all work.

    More -> Settings -> Programme -> Demonstration pictures -> Check
walks all 169 movements and lists exactly what is still missing.

Nothing from Instagram or any other subscription is downloaded or embedded.
A movement she likes from Senada Greca or Zubalenok is saved in
More -> My references as a name, a link, a target muscle and a note, and the
coach borrows the movement pattern rather than the content.

5. ON THE PHONE
===============
Open the Netlify URL in Safari -> Share -> Add to Home Screen.


6. WHAT'S NEW IN v2.1 — THE COACH ACTUALLY COACHES
==================================================
THE PROGRAMME, NOT A FIXED LIST
  Every Monday used to be the same nine movements. The five weekday
  templates now describe the SHAPE of each day — how many blocks, how many
  rounds, which movement pattern sits where — and the app chooses what fills
  each slot from what she has actually done.

  The 169 movements are grouped into ten categories: squat, hinge,
  single-leg, glute isolation, push, pull, core, mobility, conditioning and
  accessory. Rotation happens inside a category, so a squat is replaced by
  another squat, never by a stretch.

  Block A's first two loaded lifts are HELD for the four-week block so
  progress on them can be measured. Everything else rotates.

THE FOUR-WEEK BLOCK
  Week 1  baseline — settle the technique
  Week 2  one step up
  Week 3  the strongest week
  Week 4  lighter on purpose, a round off each block
  Progression moves ONE variable at a time and the variable rotates: reps
  until they reach the top of the range, then the weight goes up and the
  reps reset, or a longer hold for a timed movement. Never both at once.
  Settings -> Programme shows the week and can restart the block.

THE RULES IT WILL NOT BREAK
  Every session is checked before it reaches the screen:
    · nothing she performed in either of the last two sessions
    · no more than 40% carried over from the previous workout
    · never the same workout inside 30 days
    · nothing on hold after a pain report, nothing on her avoid list
    · nothing needing kit she says she hasn't got today
    · no overhead loading when the neck is up, no impact when the pelvic
      symptoms are
    · the minutes on the screen are the minutes it will take
  Anything that fails is re-picked, up to four passes. If a category is
  genuinely exhausted it widens into the neighbouring one, and if it still
  has to repeat a movement it SAYS SO rather than repeating quietly.

THE CHECK-IN
  Four one-tap rows — energy, neck, where you're sore, how long — plus two
  quiet pills: what you want from today ("Coach picks" by default) and what
  kit you've got. Sore legs moves the day to upper body and alternates with
  mobility rather than giving you the same session twice. Unticking the rack
  keeps today buildable instead of prescribing a barbell you haven't got.

WHY THIS?
  A button on the home card and the ready screen. Three reasons at most,
  every one from real data: the block week, a lift held for progress, what
  the check-in changed, what the last session felt like.

AFTER THE SESSION
  Too easy / Just right / Too hard, then whether anything hurt, then an
  optional best and worst movement. Too easy raises the numbers next time,
  too hard holds them, a pain report takes the movement out until you put it
  back (Settings -> Programme -> Movements on hold), and a movement you
  dislike comes round less often. Skip something three times and it asks one
  short question instead of prescribing it again.

SWAP
  Now leads with the three you actually want — Easier, Same level,
  Different kit — each with a one-line reason. It never offers something on
  hold, on the avoid list, or done in the last two days. What you choose is
  remembered.

THE COACH
  Warm, confident and concise by default. The direct voice is still there in
  Settings -> Session -> Coach's voice. It sees the last ten workouts, the
  category balance, the block week, the held lifts, your feedback and what's
  on hold — and today's session comes with the app's approved alternatives
  already attached, so it chooses between options the rules have cleared
  rather than inventing one. Every change it proposes goes through the same
  validation; anything that breaks a rule is refused with the reason.
  Without an API key it still answers, from the same engine.

CANCEL WORKOUT
  A plain "Cancel workout" on every live screen — warm-up, working set and
  cool-down. One confirmation, and an undo afterwards.

THE PHONE AND THE IPAD
  No longer locked to portrait. In landscape the iPhone puts the picture
  beside the prescription, the tab bar loses its second line and the rest
  screen reads across, so Complete sits above the fold. The iPad gets the
  two-column home and the same side-by-side working set. Pinch-zoom works
  again.

THE PICTURES
  A picture in the demos folder now BEATS the built-in animation, which
  lives on someone else's server. So the pictures you add are the ones she
  sees. The folder is checked across jpg, webp, png and gif, so a folder of
  webp is no longer mistaken for no folder at all.
  Settings -> Programme -> Demonstration pictures -> Check walks all 169
  movements and lists exactly which filenames are still missing, ready to
  paste into the folder.

7. WHAT WAS IN v2.0
===================
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
