# I Can Be a Builder!

A talking picture book for young kids (around age 5) about building a house, made for phones and tablets. Every page is read aloud in very simple English, and every page has something to tap.

- **Hello!** Sam waves. Tap Sam to say hi.
- **What do builders do?** A house, a school and a tall tower pop up. Tap one to hear its name.
- **Get dressed!** Drag the hard hat, vest, boots, gloves and goggles onto Sam (or just tap them). Each one says why it keeps Sam safe.
- **My tools.** Tap the hammer, saw, tape measure, drill and level to hear them work.
- **Big machines.** Tap the digger, cement mixer, dump truck and crane to see them move.
- **Dig, pour, stack.** Tap to dig a hole, fill it with concrete, then stack ten bricks while counting out loud from one to ten.
- **The roof.** Drag the roof up with the crane (or tap it) until it sits on the walls.
- **Paint it.** Windows and a door appear; pick a colour for the house.
- **A team.** Tap the electrician, plumber and painter: lights on, water on, flowers.
- **Safe or not safe?** Four little questions with thumbs up or thumbs down. A wrong answer just says "Oops! Try again."
- **How do I become a builder?** Play with blocks, be careful and help others, then go to builder school.
- **You did it!** Confetti, the finished house and a Junior Builder badge.

The ▶ button always works, so nothing has to be finished to turn the page; it pulses when the page's job is done. 🔊 reads the page again, ◀ goes back, and the small speaker in the corner turns sound off and on. 🏠 in the other corner goes back to the list of all games.

## Run it

It's one page plus the sound clips in `assets/`. Serve the folder (for example `python -m http.server 5208`) and open it in a browser; it needs an internet connection the first time, for the font. No build step. Opened straight from disk it still works, but the browser won't load the clips, so you hear synthesized sounds and the device's own voice instead.

## Play offline (add to Home Screen)

On iPhone or iPad, open the book in Safari, tap **Share → Add to Home Screen**, then open it once from the new icon while online. After that it starts full screen and works without internet. Changes arrive on their own: the next online launch downloads them and the one after shows them.

(How: `manifest.webmanifest` gives the icon and full-screen mode; `sw.js`, a service worker, keeps a copy of every file the book uses, including the font and the sound clips.)

## Tuning knobs

At the top of the script in `index.html`:

- `DIG_TAPS`: taps on the digger before the hole is done (5).
- `POUR_TAPS`: taps on the cement mixer before the hole is full (3).
- `BRICKS`: bricks in the wall (10; there are spoken numbers up to ten).
- `BRICK_GAP`: the shortest time between two bricks, so fast tapping doesn't skip numbers.
- `QUIZ_PAUSE`: the pause after a quiz answer before the next question.
- `COLOURS`: the paint colours on the colour page.
- `ASSET_V`: bump it after replacing any file in `assets/`, so phones don't keep the old one.

In the sound section: `VOICE_VOL` and `CLIP_VOL` (0 to 1) for the voice and the sound effects, and `CLIP_TRIM`, per-clip trims that even out the effects, which ElevenLabs made at different levels. Lower a number if a sound is too loud.

All the words are in `LINES` near the top. If you change a line, its recorded clip still says the old words, so regenerate that clip too (or delete it, and the device voice reads the new text).

## Audio credits

Voices and sounds: [elevenlabs.io](https://elevenlabs.io). All clips were made on 2026-10-08 with an ElevenLabs **free** plan, so they may only be used non-commercially and must credit ElevenLabs (the last page shows the credit). They are not covered by any licence on this book's code.

- **Sam's lines** (`assets/say-*.mp3` except the three below, 63 clips): voice "Jessica", model Eleven Multilingual v2. Every narrated line, the item and tool lines, the machine names, the numbers one to ten, the colour names, the quiz questions and answers, and the badge.
- **The team** (3 clips), model Eleven Multilingual v2: `say-electrician.mp3` voice "Liam", `say-plumber.mp3` voice "Roger", `say-painter.mp3` voice "Laura".
- **Sound effects** (`assets/sfx-*.mp3`, 12 clips): ElevenLabs Sound Effects. Hammer, saw, drill, digger, concrete pour, truck horn, crane winch, brick clunk, roof thud, light switch, water tap and kids cheering.

The small UI sounds (pop, sparkle, boop, tape-measure zip, level bloop) are synthesized in the browser.
