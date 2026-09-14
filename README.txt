TRAIN — Lia's personal training app
v1.1 · 14/09/2026

Built on the Amir PT architecture: one HTML file, no build step, Firebase for
the cloud copy, OpenAI for the coach's words only. Amir PT is untouched.


1. WHAT TO UPLOAD
=================
Put these in the repo through the GitHub web UI, and let Netlify deploy:

    index.html
    sw.js
    manifest.json
    icon-180.png
    icon-512.png
    icon-1024.png

Nothing else is required. It runs the moment it is live.


2. FIRESTORE — ONE PASTE, ABOUT 30 SECONDS
==========================================
    console.firebase.google.com
      -> project ptchat-170ff
      -> Build -> Firestore Database -> Rules tab
      -> select everything in the editor and paste firestore-rules.txt over it
      -> Publish

That file is your existing amirpt rule plus one new block for liapt. It does
not change anything about your app.

WHY: Lia's check-ins, cycle records, measurements, pain reports, photographs
and history are written to a collection called liapt. Without the rule,
Firestore refuses the write.

IF YOU DON'T DO IT, NOTHING BREAKS. The first cloud write fails with
permission-denied, the app notices, and puts her document inside the existing
collection instead, at amirpt/lia-7m2xv4. Still a separate document, still
invisible to your app — just an untidy address. Everything keeps working
either way.

TO CHECK WHICH IS IN USE: in Train, More -> Settings -> Backup and sync ->
"Check the connection". It names the exact document path and the time of the
last backup.

Her photographs are never uploaded. They stay on her phone.


3. HER OWN COACH — THE API KEY
==============================
Train talks to OpenAI directly from the phone. The key lives on her device
and is never uploaded with the backup.

IF YOU WANT A SEPARATE KEY AND SEPARATE BILLING (recommended)
    a. platform.openai.com -> sign in, or create an account in her name
    b. Settings -> Billing -> add a card, or buy credit. A key on an account
       with no credit returns a 429 and the coach stays silent.
    c. API keys -> Create new secret key -> name it "Train" -> copy it.
       It is shown once. Copy it then.
    d. On her phone, in Train: More -> Settings -> Coach -> paste it into
       OpenAI API key -> Save -> Test the connection.
       It should say "Connected. The coach is live."

IF YOU'D RATHER USE YOURS
    Paste your existing key into the same field. It's billed to your account.
    The two coaches read different Firestore documents, so neither can see
    the other's training.

MODEL
    gpt-4o-mini is the default and is the right one. A morning analysis plus a
    few messages is a fraction of a cent; a heavy month is a few dollars. The
    dropdown offers gpt-4o and gpt-5-mini if you ever want to spend more.

ON A SECOND DEVICE
    The key is deliberately not synced. If she adds the app to an iPad as
    well, paste it there too.

WITHOUT A KEY THE APP IS STILL FULLY FUNCTIONAL. The programme, the check-in
adjustments, the neck logic, the cycle logic, load suggestions, records,
replacements and the whole workout runner are decided in code. The key only
buys better sentences and a coach that answers questions.


4. ON THE PHONE
===============
Open the Netlify URL in Safari -> Share -> Add to Home Screen. It installs as
"Train" with the pulley icon, runs full screen and works offline.


5. EXERCISE DEMONSTRATIONS
==========================
169 movements. 27 have an animated demonstration already (the same source
your app uses). The rest show a labelled body map of what the movement
trains, with the full set-up, movement, cue, common mistake and neck note
behind "How?".

TO ADD YOUR OWN PICTURES OR CLIPS
    a. Make a folder in the repo called  demos
    b. Drop files in it named after the exercise, lower case, hyphens for
       spaces:   Hip Thrust  ->  demos/hip-thrust.jpg
       JPG for a photograph, MP4 for a short clip, GIF for a loop.
    c. Send me the list of what you added and I'll switch them on in one
       line each. Nothing is requested until it is switched on, so a phone
       never fires a hundred failed requests looking for files that aren't
       there.

Train-exercise-list.xlsx has every movement, the exact filename to use, and
a note on what each picture needs to show. The second tab is only the 142
that still need one, with the 56 in the weekly programme marked first.

A one-off link also works without touching the repo: any exercise -> How? ->
"Add a demonstration" takes a direct https URL.

Nothing from Instagram or any other subscription is downloaded or embedded.
A movement she likes from Senada Greca or Zubalenok is saved in
More -> My references as a name, a link, a target muscle and a note, and the
coach borrows the movement pattern rather than the content.


6. WHAT CHANGED IN v1.1
=======================
    · Bands added to her profile as a preference. 21 band movements in the
      library now, including banded versions of the hip thrust, squat,
      Romanian deadlift, row, chest press, kickback and woodchop.
    · A swap now offers band options first, because she likes them. It never
      removes anything from the programme — it only changes what comes top
      of the list.
    · demos/ folder support, and video (MP4) as well as photographs.
