TRAIN — Lia's personal training app
v1.0 · 14/09/2026

Built on the Amir PT architecture: one HTML file, no build step, Firebase for
the cloud copy, OpenAI for the coach's words only. Amir PT is untouched.


WHAT TO UPLOAD
==============
Put all of these in the repo, through the GitHub web UI as usual, and let
Netlify deploy it:

    index.html
    sw.js
    manifest.json
    icon-180.png
    icon-512.png
    icon-1024.png

Nothing else is required. It runs the moment it is live.


ONE THING TO PASTE (30 seconds)
===============================
Firebase console → Firestore → Rules → paste the contents of
firestore-rules.txt → Publish.

That adds a `liapt` block alongside the existing `amirpt` one. Lia's
check-ins, cycle records, measurements, pain reports and history live in
their own collection; neither app can read the other's document.

If you don't paste it, nothing breaks. The first cloud write fails with
permission-denied, the app notices, and falls back to a separate document
inside the existing collection (amirpt/lia-7m2xv4). Still completely
isolated from your data — just a less tidy address. Settings → Backup and
sync → "Check the connection" always tells you which one is in use.


THE API KEY
===========
Settings → Coach → paste the same OpenAI key you use, then "Test the
connection". Billed to the same account; the two coaches read different
documents so they can't see each other's training.

Without a key the app is still fully functional. Every decision — the
programme, the check-in adjustments, the neck logic, the cycle logic,
load suggestions, records, replacements — is made in code. The key only
buys better sentences and a coach that answers questions.


ON THE PHONE
============
Open the Netlify URL in Safari → Share → Add to Home Screen. It installs as
"Train" with the pulley icon, runs full screen and works offline.


WHAT'S NOT THERE YET
====================
Exercise demonstrations. 27 of the 157 movements have a real animated demo
(the same source your app uses). The other 130 show a labelled body map of
what the movement trains, and every one has a "How?" panel with the set-up,
the movement, the main cue, the common mistake and the neck note.

The media slot is a proper field, not a placeholder graphic: Train → any
exercise → How? → "Add a demonstration" takes a direct https link to an
image, GIF or video and stores it per exercise. Nothing from Instagram or
any other subscription is downloaded or embedded — a movement she likes from
Senada Greca or Zubalenok is saved in More → My references as a name, a
link, a target muscle and a note, and the coach uses the pattern rather than
the content.
