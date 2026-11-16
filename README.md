# Blink RNG

A phone app for RNG manipulation of stationary encounters in Pokémon Brilliant Diamond and Shining Pearl, using the blink method. Record your trainer's blinks, find your RNG seed, pick a target (shiny, IVs, nature), and get a countdown telling you exactly when to press A.

It's a single web page that runs entirely on your phone. Nothing is sent anywhere. Once installed, it works offline.

## Put it on GitHub Pages

1. Create a new repository on GitHub. It can be public or private, but GitHub Pages on a private repo needs a paid plan.
2. Upload every file in this folder to the root of the repo, keeping the file names as they are.
3. Go to **Settings → Pages**. Under "Build and deployment", set the source to **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. Wait a minute or two. GitHub shows the address, something like `https://yourname.github.io/blink-reader/`.

## Install it on your Android phone

1. Open the GitHub Pages address in Chrome.
2. Tap the three-dot menu and choose **Install app** (on some versions it's **Add to Home screen**, then **Install**).
3. Open it once while you're online so it can save itself for offline use. After that it works with no signal.

Your seed, target, offset and settings are stored on the phone and survive closing the app. Uninstalling the app or clearing Chrome's site data wipes them.

## Updating

If you change `index.html`, also change `VERSION` at the top of `sw.js` (for example `blink-reader-v2`). Otherwise phones keep using the cached copy until it refreshes in the background. Open the app twice while online to pick up an update.

## How it works, briefly

1. **Find seed.** Record 40 blinks in a quiet spot by tapping along, pointing the camera at the screen, or uploading a video. Each blink reveals a few bits of the game's Xorshift128 RNG, and 40 are enough to solve for the full 128-bit state.
2. **Pick target.** Search ahead for a stationary Pokémon matching your filters. The RNG moves about one advance per second while you stand still.
3. **Line up.** Walk to the Pokémon and record 10 more blinks to find exactly where you are. Keep recording until you press A, especially if the Pokémon blinks too, as its blinks make long-range prediction unreliable.
4. **Hit it.** Press A on the countdown. If you miss, tap what you actually got and it learns your offset for next time.

Video upload only works for step 1, because a recorded clip can't tell the app exactly when each blink happened in real time. Steps 3 and 4 need live tapping or the live camera.

## Supported encounters

Starters, gifts (Eevee and the Happiny and Riolu eggs), fossils, Drifloon, Spiritomb, Rotom, the lake trio's Uxie and Azelf, Dialga, Palkia, Heatran, Regigigas, Giratina, every Ramanas Park legendary, and the mythicals. Roamers, wild encounters and bred eggs aren't covered.

## Testing

The ported maths was checked against the original code: seed recovery against Project_Xs on 20 random seeds, line-up against Project_Xs's Python on synthetic data, and Pokémon generation against all 50 of PokéFinder's BDSP static test results. The full app was tested in a browser with simulated human tapping (including deliberate mistakes), a fake webcam, and an uploaded test video. It has not yet been tested against a real Switch.

## Credits and licence

- RNG state recovery and blink timing are ported from [Project_Xs](https://github.com/niart120/Project_Xs) by niart120 (MIT licence, see `LICENSE-Project_Xs-MIT.txt`).
- Stationary Pokémon generation and encounter data are ported from [PokéFinder](https://github.com/Admiral-Fish/PokeFinder) by Admiral_Fish, bumba and EzPzStreamz (GPL-3.0).

Because it includes code derived from PokéFinder, this project is released under the **GNU General Public License v3.0** (see `LICENSE`).

Fan-made tool. Not affiliated with or endorsed by Nintendo, Game Freak, Creatures or The Pokémon Company.
