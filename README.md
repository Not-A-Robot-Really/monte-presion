# Monte-Presion
 
A little pixel-art bluffing card game I built for the browser, kind of like "Cheat" / "I Doubt It" but with a countdown timer to keep things tense. It's you against 3 bots (Jimmy, Gus, Juan) and you're all racing a number that counts down from 13 to 1.
 
This was built in HTML/CSS/Javascript

## About

A simple card game where four enemies all race against the clock to clear their cards and bluff their way out of their situation at-hand, or die trying.

## Why "monte presion"?
'Monte' refers to any sort of card game. 'Presion' is directly translated to "pressure" in Spanish.
 
## Features
 
- Deals out a full deck to you and 3 CPU players (you'll get to learn their names soon enough)
- Counts down from 13, and on every number you get a short window to drop a card and claim it matches (or bluff, or pass)
- You can accuse someone of lying by clicking the hourglass in the middle of the table
- Bots aren't dumb, they kind of "watch" how fast your pile grows and get suspicious of you over time
- Everything visual (suits, hourglass icon, gear icon, chat icon) is drawn from little pixel bitmaps in the code, not image files
- Sound effects are generated with the Web Audio API, so there's no sound files for those, but there IS a real mp3 for the background music
- Settings (sound on/off, volume) get saved in localStorage so they stick around between visits
## Files
 
```
countdown.html   -> the actual page + all the game logic (JS is inline in a <script> tag)
styles.css       -> all the styling, pulled out into its own file
game-theme.mp3   -> background music, loaded by filename, not embedded in the HTML
README.md
LICENSE
```
 
## Run the game
 
Honestly, you can probably just double click `countdown.html` and it'll work. However, if the music/sound is acting weird, try running a quick local server instead:
 
```bash
python3 -m http.server 8000
```
 
then go to `http://localhost:8000/countdown.html`
 
## How to Play
 
Ranks map to numbers like this: A = 1, 2 through 10 are just their number, J = 11, Q = 12, K = 13. Jokers are wild and can be claimed as any number.
 
Each round the countdown number ticks down. For every number you get two phases:
 
1. **Place phase** - play a card face down and claim it matches the number (true or not), pass, or pull a card back off your own pile instead of playing
2. **Wait phase** - short pause before the next number, bots decide here if they want to accuse someone
There's a yellow bar at the top that fills up so you can actually see how much time you've got left in the current phase.
 
If you think someone's bluffing, click the hourglass in the middle and pick who to accuse. Their top card flips over:
- if the card doesn't match what they claimed, they lose a life ♥
- if the card does match, congrats, you just falsely accused someone and YOU lose a life instead
If the countdown hits 0 and nobody got caught, whoever placed the fewest cards that round loses a life. This rule makes frequently passing a risky and tactical decision you will have to think through.
 
Everyone starts with 2 lives. Last person standing wins. Oh also, if you manage to sneak a 3-of-a-kind or a full run of all 4 suits without getting caught, you get a bonus life for next round.
 
## Controls
 
- Click a card in your hand to play it
- PASS button to skip your turn
- PULL CARD FROM PILE to take your top pile card back (only shows up once you have a pile)
- Click the hourglass to accuse someone
- Chat bubble icon (top left) opens/closes the event log
- Gear icon opens settings
## A few implementation notes
 
The bot AI isn't too complex. Each bot keeps a number (0 or 1) for every other player and adjusts it depending on whether that player's pile is growing faster than expected. When it's time to maybe accuse someone, it rolls a random die weighted by how suspicious it currently is of each player.
 
Sound effects are all generated with oscillators (no actual audio files for those), but the background music was made by me (kinda rushed, but it will do) on Flat.
 
## License
 
MIT, see the LICENSE file.
