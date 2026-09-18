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
THE BODY SHE IS BUILDING
  This is the point of the app, so it is not left to a sentence in a prompt.
  Progress -> What you're building (or Settings -> The body you're building)
  asks the question directly, and she picks up to three aims IN ORDER:

    Glutes            thrusts, hinges, abduction, single leg
    Back & shoulders  rows, pulldowns, rear delts
    Waist & abs       anti-rotation, anti-extension
    Legs              squats, lunges, step-ups
    Arms & chest      presses, curls, raises
    Leaner & fitter   rowing, carries, circuits

  plus an approach: leaner, stronger at the same weight, or build size.
  Hers is set to glutes, back, abs — the same thing her written goals said,
  in a shape the engine can act on.

  The order matters, because the engine acts on it three ways:

  1. It tips every close call. A movement is scored on how much it serves
     those muscles — the one it trains FIRST counting double — alongside
     recency, variety, equipment and the block. Big enough to decide a close
     call and to beat a mild recency penalty; deliberately not big enough to
     override "you did this two days ago", or it would be the same four
     glute movements forever.

  2. It re-points the day. Choosing a better exercise for a slot is not
     enough: if the template gives a day one pull slot, a back goal still
     only gets one pull. So one accessory slot (two on a long day) is
     re-pointed at what she is building. Never an anchor, never the slot the
     weekly balance check needs, and nothing at all on a day that already
     serves the goal — the day stays hers.

  3. It raises the weekly bar. Glutes first means glute work three days a
     week instead of two, and hinges twice. The goal never LOWERS the base,
     so chasing glutes cannot cost her a back day.

  Measured over eight simulated weeks, switching the goal from glutes/back/
  abs to arms/legs/fitter moved the actual training:

    glutes + hamstrings    660 -> 474 weighted sets
    back + lats            317 -> 215
    arms + chest + delts   202 -> 332
    share of work serving the stated goal    68% -> 45%

  ...while still producing 40 distinct sessions out of 40 and 105 different
  movements, so nothing was flattened to get there.

  Change the goal and tap "Aim the programme at this" and today is rebuilt
  immediately, not next month.

BUILDING ON WHAT SHE HAS DONE
  The same card shows what the work has actually produced, per aim: the
  movements that genuinely serve it, and the biggest gain since. So:

    1  Glutes             Hip Thrust 20 kg -> 25 kg         +5 kg
    2  Back & shoulders   Band Pull-Apart 8 -> 14 reps      +6 reps
    3  Waist & abs        Banded Pallof Press 10 -> 12      +2 reps

  A movement only counts toward an aim if that is what it is FOR — the
  muscle it trains first, or a close second. A goblet squat braces the
  trunk, but it is not ab work, and counting it as such would flatter the
  number and tell her nothing.

  Two engine bugs surfaced while proving this out, both now fixed:

    - A movement could be prescribed FEWER reps than last time simply
      because it turned up in a shorter slot. Nothing outside week four (the
      deload) is ever allowed to ask for less than she has already done.

    - A band movement at the top of its rep range was being reset to eight
      reps "because the weight goes up". You cannot put 2.5 kg on a
      resistance band. Bands and bodyweight now climb on reps and hold at
      the top, and she is told to move up a band when it feels easy. Only
      movements that take actual kilos reset.

  And a session she gave a thumbs up now comes back as she liked it: "you
  did this recently" is exactly what a thumbs up overrides, so the replay is
  exempt from the recency and overlap checks. Pain, the neck, the avoid list
  and missing kit still get the last word.

  The coach is handed all of this structurally — the ranked aims, the
  muscles that matter and by how much, the weekly targets, and what has gone
  up — not as prose, and it is told to explain today in those terms.

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

THE TRAINING WEEK, AND BODYBUILDING DAYS
  More -> Settings -> Programme -> Training week.

    Lia's week        the five days as written: compounds, supersets,
                      pelvic and neck work.                   (the default)
    Mixed             her week, with two of the five turned into volume
                      sessions — back and shoulders, chest and arms.
    Bodybuilding      a five-day hypertrophy split: glutes and legs, back
                      and shoulders, quads and hamstrings, chest arms and
                      core, full body.

  The volume days are higher-rep (12 on average), more isolation, shorter
  rests, straight sets on the main lifts. They obey the same rules as
  everything else — nothing overhead when the neck is loud, nothing she has
  ruled out, and the movements still rotate.

  She can also take one volume day without changing the week: the focus
  button on the check-in now lists all five.

THE WEEK, NOT JUST THE DAY
  The engine used to build each day in isolation, which let her pull on one
  day a week and press on none. It now knows what the week has covered, what
  is still to come and what is missing, and leans each session toward the
  gap.

  On the LAST training day of the week one accessory slot is given to
  whatever the week never got to — "Last day of the week and you hadn't done
  any pulling, so Banded Row goes in." Over four simulated weeks that took
  her from one pulling day a week to two. On a bands-only week that costs
  one rotating slot; pulling twice is the better trade.

  The coach sees all of it: the whole week day by day, what is done, what is
  left, and what is still short. Ask it what to do today and it answers in
  the context of the week.

STARTING WEIGHTS
  The first suggestion for a movement she has never done is now worked out
  from her bodyweight rather than a fixed table, so it is hers and it moves
  if she does. At 65 kg a hip thrust starts at 20 kg; at 80 kg it starts at
  25. A logged weight beats the profile figure. Height makes a small
  difference, and only on squats and hinges, where a longer body genuinely
  moves the bar further — never more than a tenth either way.
  The card says where a number came from, and every suggestion is still
  hers to accept or change.

VARIETY AGAINST STRENGTH
  She wants different sessions AND numbers that go up, so one control decides
  how much is held still long enough to build on. Every setting still rotates
  the accessory work and still refuses the same session twice inside a month.

    More variety     1 lift held for 2 weeks. Almost everything changes.
    Balanced         2 lifts held for 4 weeks.  (the default)
    Build strength   4 lifts held for 8 weeks and driven up.

  More -> Settings -> Programme -> Variety and strength.
  Over eight simulated weeks: more variety gave 123 different movements and
  came back to each loaded one 3 times; build strength gave 83 and came back
  6 times, and put 8.75 kg on the hip thrust against 6.25.

  Rotation used to throw strength away: a movement she had never done started
  from a generic table, so the weight reset every time it changed. Now a new
  movement inherits what she is already lifting on its close relatives — the
  same pattern at the same station — and the card says where the number came
  from. It never guesses across equipment, because 20 kg on a barbell is not
  20 kg on a dumbbell.

  Progress -> Building on shows the held lifts and what has happened to them
  since the programme started holding them. The working card shows what today
  is trying to beat.

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
  First: do you want this workout again? Thumbs up or thumbs down.

    Thumbs up    the session is kept exactly as it was and comes back on the
                 same day next week, one step heavier on everything that can
                 be loaded. It compounds — 20 kg, then 21.25, then 22.5 —
                 because it steps up from what she actually lifted last time,
                 not from what was written. It holds for the rest of the
                 four-week block, then the rotation takes back over. The
                 ready screen shows a "back by request" chip, and "Build me a
                 different one" cancels it.

    Thumbs down  that exact combination is never built again, at any distance
                 in time, and the movements in it lose a little ground so
                 they come round less often.

  Then: too easy / just right / too hard, whether anything hurt, and an
  optional best and worst movement. Too easy raises the numbers next time,
  too hard holds them, a pain report takes the movement out until you put it
  back (Settings -> Programme -> Movements on hold), and a movement you
  dislike comes round less often. Skip something three times and it asks one
  short question instead of prescribing it again.

SWAP, AND "I DON'T LIKE THIS ONE"
  Tap any movement anywhere — a working set, a warm-up move, a cool-down
  stretch — and the sheet that opens has Swap it and Don't like it sitting
  right under the picture.

  Swap leads with the three you actually want — Easier, Same level,
  Different kit — each with a one-line reason. It never offers something on
  hold, on the avoid list, or done in the last two days. What you choose is
  remembered: it scores higher next time, and the one you swapped out scores
  lower.

  Don't like it asks once, says what it will put in its place, and then that
  movement is never built into a session again — not in the working sets,
  not in the warm-up, not in the cool-down. Put it back any time in
  Settings -> Programme -> Movements you like and avoid.

EASIER MEANS EASIER
  Asking the swap sheet for an easier movement could hand her a harder one.
  Every entry in the catalogue names an easier and a harder version of
  itself, so there is a real ladder to read — the swap sheet just was not
  reading it. Three separate faults:

  1. The fallback was inverted. When the movement's own declared easier
     version was not available, the code looked for movements whose EASIER
     version is the one she is doing — which is the definition of harder.
     Swept across all 169 movements, that produced 34 sheets offering a
     harder movement under the heading "Easier".

  2. The declared easier version skipped every check. It was taken straight
     from the catalogue rather than from the approved list, so "Easier"
     could offer something she had banned, something on hold after pain,
     something needing kit she hasn't got today, something already in the
     session, or the same movement straight back.

  3. Nothing verified the direction. "Same level" and "Different kit" could
     both hand her something harder too.

  Now there is one difficulty ladder, built from all four declarations each
  pair makes about the other, and the sections are chosen from the approved
  list only. Two refinements the data forced:

    - Some pairs contradict each other. Clamshell and Side-lying Hip
      Abduction each name the other as easier; DB Curl and Hammer Curl each
      name the other as harder. The catalogue is not ranking those, so they
      are treated as the same level rather than letting a tiebreak invent an
      order.

    - A step must stay the same kind of movement. On rank alone a Pallof
      Press is a "harder Deadlift" — true on the ladder, useless as a swap.
      Candidates now have to share the movement pattern, or failing that the
      muscle the movement is actually for.

  Swept over every movement twice, once with the obvious kind option taken
  off the table: 0 sheets now offer a harder movement under "Easier", 0
  under a same-level heading, 0 non-harder under "Harder", 0 options the
  engine would refuse, and 0 offering the same movement back. The ladder
  itself has no contradictory pairs.

  She can also just say it. "This is too hard", "give me something easier",
  "I'm struggling with this one", "that was too easy", "step me up" are read
  as a step down or up the ladder — with or without the API key, and never
  in the wrong direction. Before this they fell through to a plain rotate,
  which ignores difficulty entirely.

  When there genuinely is nothing kinder or harder that fits, it says so
  instead of substituting nonsense: "There is nothing harder than Deadlift
  that fits today — add weight or reps instead." Which is the right answer:
  a deadlift is the top of its ladder, and the progression there is load.

TALKING TO THE COACH CHANGES THE APP
  She can say what she wants in her own words and the programme changes.
  Seventeen validated actions, and the engine still gets the last word on
  every one: change the length of today, take a rest day, rebuild, rotate or
  replace a movement, add or remove one, change the rounds, put a movement
  on hold after pain, ban one for good, put a banned one back, mark one she
  likes, change what body she is building, change today's equipment, change
  the programme style or the variety-against-strength dial.

  Three things make that work rather than nearly work:

  SHE RARELY SAYS ONE THING. "My knee hurts on split squats and I have only
  got 25 minutes" is two instructions. Up to three are now returned and
  applied in order, and each is reported. It used to take one and drop the
  rest.

  IT UNDERSTANDS HER WITHOUT THE KEY. The OpenAI key lives on one device, so
  on any other phone the coach would hear "my knee hurts" and change
  nothing. The plain cases are now read in code — how long she has, what
  hurts, what she hates, what she wants to build, what kit she has today, a
  rest day, a rebuild — and turned into the same validated actions. It also
  runs as a safety net when the model replies warmly but returns no action,
  so "I have only got 20 minutes" can never be answered with agreement and
  no change.

  The reading is careful about which half of a sentence is which: "my back
  hurts and I want to work on my arms" is a held movement and an ARMS goal,
  not a back goal. Aims are only read from the part of the sentence asking
  for them, in the order she said them.

  SHE CAN SEE IT AND UNDO IT. What changed is its own line in the chat,
  ticked and in green, with an Undo on the last one. Undo puts back
  everything a coach action can touch — the session, the check-in, the avoid
  list, what is on hold, the body goal and the preferences — not just the
  session, which is all the workout undo covered.

  What it will not do is unchanged. It cannot add a barbell movement on a
  bodyweight day, bring back something held for pain, or break the recency
  and equipment rules. It says why instead: "I can't add that — you haven't
  got the Barbell today."

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

THE TIMER RUNS ITSELF
  A timed movement used to sit there waiting to be tapped, count down in
  silence, and only beep at the end. Now she never has to look at it.

    It counts her in       five seconds, with a tick at three, two and one
                           and a higher note on go, so she can get into
                           position without watching.
    It runs itself         the clock starts the moment the movement comes up.
    It counts her out      a tick at three, two and one, then a two-note
                           finish, and it logs the set and moves on.
    "Each side" means two  a 30-second side plank now runs 30 seconds, calls
                           "Swap sides" out loud, and runs 30 more. It used
                           to run once and stop.
    The rest does it too   the rest clock counts her back in and says the
                           next movement by name.

  The countdown is large and white on black, readable at arm's length.
  Tapping it stops it, and it will not restart itself until the next
  movement.

  More -> Settings -> Session:
    Start timed moves for me   the count-in and the automatic clock
    Beeps                      how loud — normal, loud, as loud as it goes
    Hear the count-in          plays three, two, one and the end of a set
    Keep the screen awake      the phone stays lit while the app is open
    Say what is next           the spoken side change and next movement
  The switches are on and the beeps ship all the way up. The existing sound
  and vibration switches still apply.

WHEN THE COACH IS SILENT
  iOS speech fails silently in three ways, and all three were reachable:

    - THE QUEUE WEDGES. speechSynthesis gets stuck with speaking=true and
      never clears, usually after the page has been in the background —
      which now happens constantly, since the app reopens into a live
      session. Every later utterance is swallowed. The queue is now cleared
      before every cue, IN ITS OWN TASK, because cancel() and speak() in the
      same task makes iOS drop the new one. Both halves of that are needed;
      doing either alone is silence.

    - A VOICE OBJECT GOES STALE. After the voice list changes, the old
      object is dead and assigning it kills the utterance without a sound.
      The list is re-read whenever it changes rather than latched once.

    - A NETWORK VOICE DIES QUIETLY. Voices with localService false need the
      network and fail without a sound mid-set. Local voices now win over
      any remote one, however good it sounds.

  On top of that there is a watchdog. If nothing has actually started
  speaking within 700ms, the cue is said again in the phone's own default
  voice. Tested against all six failure modes, including one where the
  chosen voice is accepted and then silently refuses: in every one, a word
  still comes out of the phone.

  AND IT TELLS HER WHICH IT IS. Settings -> Session -> Test the voice speaks
  a line and then reports what the phone actually did: working (and which
  voice), accepted-but-never-spoke, refused, or no voices loaded. A silent
  coach is now diagnosable on the phone instead of guessed at.

HOW LOUD THE VOICE CAN GET
  Not as loud as the beeps, and this is a platform limit rather than a
  setting: an utterance's volume caps at 1, and synthesised speech does not
  pass through the AudioContext, so it cannot go through the compressor and
  limiter that put the cues at -3.5 dBFS. There is no volume above maximum
  to reach for.

  THE RINGER VOLUME IS THE USUAL CULPRIT. iOS plays speech on the ringer
  channel while Web Audio — the beeps — uses the media channel. Media up
  and ringer down is exactly "the beeps are loud and the voice is silent".
  Turn the ringer up with the side buttons while nothing is playing, and
  check the Silent switch. The app now says this in Settings rather than
  leaving it to be worked out.

  What the app does do: it holds the media route while speaking, by keeping
  a 40 Hz source at a thousandth of full scale running under the voice,
  straight to the output rather than through the compressor, so it is
  inaudible on a phone speaker. That can pull speech onto the louder route.
  Best effort, not a promise — iOS decides.

  And an Enhanced or Premium voice is markedly louder than the compact ones
  iOS ships: Settings -> Accessibility -> Spoken Content -> Voices ->
  English. Settings names the voice in use so she can see which she has.

THE SPOKEN CUES
  The voice was already at the browser's maximum — an utterance's volume
  caps at 1 and there is no way to amplify synthesised speech the way the
  beeps go through a compressor. It sounded quiet for two other reasons,
  both now fixed:

  IT WAS TALKING OVER THE BEEP. "Next. Lat Pulldown" started at the same
  instant as the finish cue, and that cue now peaks near full scale, so the
  voice was simply masked by it. Each spoken cue now waits for its own beep
  to finish: the end-of-set cue sounds for 980ms and the voice starts at
  1050ms; the side change cue ends at 460ms and "Swap sides" starts at
  520ms.

  IT WAS USING WHATEVER VOICE CAME FIRST. iOS ships compact voices that are
  noticeably thinner and quieter than the enhanced ones. The app now picks
  the best voice on the phone — enhanced and premium first, Siri next,
  compact last, English and local over anything else — and names it in
  Settings. If the best one available is still a compact voice, Settings
  says so and gives the one-download fix: iPhone Settings -> Accessibility
  -> Spoken Content -> Voices -> English -> an Enhanced or Premium voice.

  Two smaller things. speechSynthesis.cancel() was being called before every
  utterance, which on iOS makes it drop the new one; it now only clears
  something genuinely stuck. And if the platform refuses the chosen voice,
  the cue is spoken in the default voice rather than silently lost.

THE BEEPS ARE LOUD
  A phone speaker is small and she is at the far end of a gym with music
  on, so the cues were rebuilt to carry:

    - they go through a compressor and a soft clip, which puts them near
      the top of what the speaker can do without tearing
    - they sit at 1-2 kHz, where both a phone speaker and the ear are at
      their loudest, instead of down at 660-880 Hz
    - each one is a square wave plus its harmonics, not a pure sine — that
      is what makes a beep cut through rather than blend in
    - on Safari 16.4+ the app claims the media channel, so the cues come
      out at media volume and the silent switch does not swallow them

  Measured on the rendered waveform: the countdown ticks went from -32 to
  -7 dBFS and the end-of-set beep from -24 to -3.5 dBFS, with nothing
  clipped. That is roughly five times and four times as loud.

  The end of a set is now two short beeps and one long held one, with a
  long vibration under it, so it is unmistakable even mid-effort. Settings
  -> Beeps turns it down; Hear the count-in plays the whole thing so she
  can set the volume before she needs it.

THE PHONE DOES NOT GO DARK
  The screen is held awake the whole time the app is open, not only during
  a live set — propped on a bench between rounds, on the floor during the
  cool-down, sitting on the readiness questions. iOS hands the lock back
  every time the page is hidden (a call, the home screen), so the app asks
  for it again the moment she returns, and again on her first tap if the
  browser would only give it out off the back of one. Turn it off under
  More -> Settings -> Session -> Keep the screen awake.

  Two things beyond the lock make the app actually stay open:

  SHE COMES BACK TO THE SET SHE WAS ON. iOS evicts a PWA from memory
  whenever it feels like it — a call, a photo, a couple of minutes on
  something else — and the app reloads from scratch. Nothing is lost when
  that happens: the whole session, the logged sets, her position and even a
  running set timer survive, because the state is written to disk and every
  clock is a timestamp rather than a running count (a 60-second timer
  reloaded two seconds in comes back with 57 left). But she was being
  dropped on the Home screen with that timer ticking behind her. Now, if a
  session is live, the app opens straight back into it.

  IT WRITES BEFORE IT IS TAKEN AWAY. The local save is flushed on pagehide
  and the moment the page is hidden, so nothing depends on a debounce
  finishing before iOS freezes the page.

  IT TAKES THE LOCK BACK IF THE SYSTEM GRABS IT. The lock can be revoked
  without the page ever being hidden, so while a session is live the ticker
  re-asks every ten seconds rather than waiting for her to touch something.

  AND IT SAYS SO WHEN THE PHONE REFUSES. Low Power Mode makes iOS reject the
  screen lock outright. That used to fail silently, which is the worst
  possible way to find out — the screen just dies mid-set. A live session
  now carries one line: "Your phone is refusing to stay awake — that is
  almost always Low Power Mode, which also forces Auto-Lock down to 30
  seconds. Turn it off in Settings → Battery." with a Got it to silence it.

  That wording matters: when Low Power Mode is on, iOS greys the Auto-Lock
  setting out and pins it at 30 seconds, so telling her to change Auto-Lock
  would be telling her to do something the phone will not let her do. The
  only fix in that state is turning Low Power Mode off.

  AUTO-LOCK, FOR THE RECORD. When the lock is working, Auto-Lock is
  irrelevant — the screen does not sleep at all during a session, whatever
  it is set to. It only matters as a fallback for when the lock is refused,
  and iPhone's longest setting short of Never is 5 minutes, which is longer
  than any rest the app prescribes.

  For the best result: add Train to the home screen rather than running it
  in a Safari tab. Safari discards background tabs far more aggressively
  than it does an installed app.

  If she does lock the phone by hand the clock is still right when she
  comes back — it always was, it is kept by timestamps — but the cues will
  not have sounded while it was off.

SHE ALWAYS LANDS ON THE PICTURE
  Every time she moves on — out of the warm-up, on to the next movement,
  round two, the next block, into the cool-down — the page snaps to the top
  of the card, where the photograph is. It snaps rather than glides: a
  smooth scroll is still travelling when the next repaint replaces the page
  under it, which is how she used to end up halfway down the up-next list.
  When nothing has moved — the clock repainting, a warm-up move ticked off
  — she is left exactly where she was, so she can read ahead in peace.

THE WARM-UP AND THE COOL-DOWN RUN THEMSELVES
  They used to be checklists: read a move, do it, tap a tick, read the next
  one. They now run exactly like the session does. The clock counts her in
  three-two-one, runs the hold, beeps when the time is up, calls "swap
  sides" half way through anything marked each side, says the name of the
  next move out loud and moves the picture on to it. She can put the phone
  down and get through the whole warm-up without touching it, and the
  cool-down finishes the session by itself at the end of the last stretch.

  Moves written in reps rather than seconds — twelve band pull-aparts, eight
  wall slides — get a generous clock of their own (four seconds a rep, 20 to
  60 seconds) so the sequence never stalls waiting to be tapped. The card
  still says "12 reps"; the button says how long it will run.

  Nothing is taken away. Tapping the running clock stops it and stops it
  starting itself again on that move; the tick beside any move still marks
  it done by hand and kills the clock on it; "Done — next" steps on
  immediately; and the Start timed moves for me switch in Settings turns the
  whole thing off, in the warm-up and cool-down exactly as in the session.

  Fixing this turned up a real bug worth naming. A clock belongs to one
  movement, and nothing was clearing it when she moved on some other way —
  tapping "start block A" part-way through a warm-up hold, for instance. The
  stale timer then sat there for ever pointing at a movement she had left,
  and because a timer was running, nothing would start the next one either:
  the auto-timer was dead for the rest of the session. Every tick now drops
  a clock whose movement is no longer the one she is on.

THE WARM-UP AND THE COOL-DOWN
  Both now show the move she is on, full width, with its cue — not just a
  thumbnail. Tick it and the picture moves to the next one. Tapping any name
  in the list below opens the full instructions, and gives her Swap it and
  Don't like it.

  And both now MATCH THE SESSION. They used to be built from the day's label
  — "Glutes & Hamstrings" — which stopped being the whole truth once the
  movements started rotating. They are now built from the movements actually
  chosen:

    The warm-up keeps the neck and rib work, which is the point of this app,
    and then rehearses every movement pattern the session contains, one move
    per pattern before any pattern gets a second. A squat day opens the hips
    and does a bodyweight squat; a pulling day does scapular pulls and band
    pull-aparts; a conditioning day raises the heart rate.

    The cool-down stretches the muscles she actually worked, hardest-worked
    first, and never repeats a movement from the session itself. The top
    three muscles each get their own stretch; the fourth slot rotates, so it
    still varies week to week.

WHAT YOU DID, AND WHEN
  Progress leads with two things:

    Ready to go up   the lifts due a step, said plainly —
                     "Last time 20 kg and it felt easy — try 22.5 kg."
                     It uses what she actually lifted and what she said the
                     session felt like. If she said it was hard it says stay
                     there instead.

    What you did     every session, newest first: the day, what it was, how
                     many sets she got through, how long it took and whether
                     she gave it a thumbs up. Tap one to open that day.

  The same sentence appears on the working card when the movement comes back,
  with a "Keep 20 kg" and a "Go 22.5 kg" button, so the number she is aiming
  at is one tap.

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
