# The number hidden in the stripes

An interactive page that shows how a barcode (UPC-A) turns 12 digits into 95 black-or-white slots, and how a scanner decides whether to trust what it read.

Entry for the Global Virtual Hackathon 2026, theme: Unveiling Technology.

## What you can do
- Type 11 digits. The 12th (check digit) is worked out and shown step by step.
- Tap any slot to flip it. The scanner re-reads the code and accepts or rejects it, with the reason.
- Turn the code upside down. The scanner notices and reads it backwards.
- Watch a 50-second captioned tour (the video is embedded in the page).
- Press Scan it to watch a laser read the code and beep.
- Pick any digit to see how it is drawn on the left and right of a barcode.
- Typo lab: test every one-digit typo and every neighbour swap against the check digit.
- Read short answers to questions like "Does the barcode contain the price?".
- Run a stress test: flip 1 to 8 random slots 20,000 times and count how often a wrong number is accepted.

## The one idea
A barcode is a number written in slot patterns, protected by two safety nets: odd/even parity inside each digit, and a check digit across the whole number.

## How it works (all in `index.html`)
- `enc()` builds the 95 slots: guard 101, six left digits, centre 01010, six right digits, guard 101. Right-hand patterns are the opposite colours of the left-hand ones.
- `dec()` checks the guards and looks up each 7-slot group in the left or right table.
- `read()` decodes both ways round and keeps the better read, which is how upside-down codes work.
- Check digit: 3 x (digits 1, 3, 5...) + (digits 2, 4, 6...) must be a multiple of 10.
- The stress test flips random slots and runs the same `read()` the scanner uses.

## Simplified
UPC-A only. The scanner sees a perfect row of slots (no blur, tilt or camera).

## Not made by us
Nothing: no libraries, fonts, images or network calls. AI tools (Claude) were used to help write the code, as the hackathon rules allow.

## Run it
Open `index.html` in a browser. No build step, nothing to install.

## Licence
MIT, see `LICENSE`.
