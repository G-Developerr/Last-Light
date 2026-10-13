# LAST LIGHT

**Hold the light until dawn.**

LAST LIGHT is a dark fantasy survivor game for the browser. You are alone in an endless night with nothing but a lantern, and hundreds of monsters are closing in from every direction. You only move. Your weapons fire on their own. Kill, collect experience crystals, level up, pick your blessings, and try to stay alive for 20 minutes, until the sun comes up.

It runs on desktop and mobile, installs as a PWA, and is built to be wrapped with Capacitor for Google Play.

---

## Features

### The run
- **Auto-attacking weapons, manual survival.** Move with WASD / arrow keys on PC or the floating on-screen joystick on mobile. Your weapons handle the rest.
- **Dash** out of trouble with a short cooldown, and fire your hero's **signature ability** when things get desperate.
- **Level-up cards.** Every level offers 3 choices (sometimes 4 with enough luck): a new weapon, a new passive, or an upgrade. Rerolls can be unlocked in the Armory.
- **13 weapons, 5 levels each:** Blood Whip, Silver Arrows, Fireballs, Frost Shards, Chain Lightning, Holy Aura, Moon Blades, Alchemist Bombs, War Axes, Holy Spear, Boomerang, Venom Cloud and Shadow Clone.
- **10 passives:** max health, move speed, damage, pickup range, cooldown, area, armor, luck/crit, regeneration and experience gain.
- **13 evolutions.** Max out a weapon, own its paired passive, then open a treasure chest to evolve it into something much nastier, from Bloodlash and Meteor Storm to Plague and the Shadow Legion. Time stops for a moment when it happens. The level-up card for every new weapon tells you which passive it needs.
- **Unions.** Max out two specific weapons and a chest fuses them into one: Fireballs + Frost Shards become **Thermal Shock**, Chain Lightning + Holy Spear become the **Thunder Spear**.
- **Monsters with their own behaviour:** slimes, fast zig-zagging bats, skeletons, slow heavy golems, cultists that keep their distance and shoot, and big slimes that split in two when they die. Elite variants show up regularly.
- **Every map has its own monster:** spore-spewing Sporelings in the forest, Ghosts that drift through the horde in the crypt, Wolves that hunt in packs on the snow, and Imps that leave fire behind them in the volcano.
- **Bosses every 3 minutes,** with an on-screen warning: dashes, bullet rings, spirals and summons. Below half health they **enrage** and fight harder. Each map has its own boss at 12:00 (the Elder Fungus, the Spectral Queen, the White Alpha, the Ifrit), and the Night Lord arrives at 18:00.
- **Events:** bat swarms that sweep across the screen and rings of monsters that surround you.
- **Pickups:** healing flasks, a lodestone that pulls in every crystal on the map, and a holy nova that wipes the screen. Smash the lamp posts scattered around the map for extra loot.
- **Endless mode:** survive past dawn and the night keeps going, with bosses that come back stronger every three minutes.

### Between runs
- **10 heroes**, each with a different starting weapon, stats and signature ability. Eight are bought with gold, two are earned through achievements.
- **24 skins** to buy with gold or unlock through achievements, some with their own glow.
- **21 achievements** that reward gold, heroes, skins and Arcana.
- **Arcana:** pick one card before a run to bend the rules (more monsters for more gold, glass-cannon damage, blood-pact healing and more).
- **Three difficulty levels** (Normal, Hard, Nightmare) with bigger gold rewards.
- **Codex:** every weapon, evolution, union, passive, monster and boss you have discovered, with evolution recipes.
- **Armory:** permanent upgrades (might, vitality, armor, recovery, speed, magnet, haste, luck, greed, wisdom, rerolls and one revival).
- **4 maps:** Haunted Forest, The Crypt, Frozen Wastes and Volcano Heart. Each one is tougher and pays more gold, and is unlocked by how long you survive.
- **Local leaderboard** with your 10 best runs, plus lifetime stats.
- Progress is saved automatically in `localStorage`.

### Presentation
- Every sprite, icon, tile and effect is drawn in code. There are no image files in the game itself.
- Dynamic lighting: your lantern carves a circle out of the dark, and fireballs, glowing mushrooms, candles and lava pools light up the night around them. The darkness lifts during the last two minutes as dawn approaches.
- Damage numbers with CRIT pops, hit flashes, explosions, screen shake and particles.
- Music and sound effects are synthesized live with the Web Audio API. Every map has its own theme, and bosses switch the score to a faster war theme. Music and SFX have separate volume sliders.
- Settings for damage numbers, screen shake, vibration (on supported phones) and joystick size.
- Greek and English, switchable at any time.

---

## Controls

| Action | PC | Mobile |
|---|---|---|
| Move | WASD / Arrow keys | Drag anywhere (floating joystick) |
| Dash | Space / Shift | Dash button |
| Hero ability | E / Q | Ability button |
| Pause | Esc / P / pause button | Pause button |
| Pick a card | Click or keys 1-4 | Tap |
| Reroll | R | Reroll button |

---

## Tech stack

- **Vanilla JavaScript** (ES5-style, no `??` or `?.`), **HTML5 Canvas 2D**, plain CSS
- **Web Audio API** for all music and sound
- **No frameworks, no libraries, no build step.** The whole game is a single `index.html`
- **PWA:** `manifest.webmanifest` plus a network-first `sw.js`, so it works offline after the first visit
- **Performance:** a uniform spatial grid for collisions and separation, pre-rendered sprite atlases (with flipped and hit-flash variants), object pooling for particles and damage numbers, and a quarter-resolution light map. Built to handle 500+ monsters on screen.

## Project structure

```
index.html              the whole game (HTML + CSS + JS)
manifest.webmanifest    PWA manifest
sw.js                   service worker (network-first)
icons/                  app icons 180 / 192 / 512
```

## Running locally

Any static file server will do:

```bash
npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080`. The service worker only registers over `http(s)`, not `file://`.

## Deploying on Render

1. Push the repository to GitHub.
2. On Render, create a new **Static Site** from the repository.
3. Leave the build command empty and set the publish directory to `.` (the repository root).

## Android (Capacitor)

The game uses relative paths only, so it can be dropped straight into a Capacitor `www` folder:

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init "Last Light" com.gnavos.lastlight --web-dir www
# copy index.html, manifest.webmanifest, sw.js and icons/ into www/
npx cap add android
npx cap open android
```

Lock the activity to landscape in `AndroidManifest.xml` (`android:screenOrientation="sensorLandscape"`).

---

Made by **G-navos Developer**: [Instagram @mhtsos_tzinavos](https://www.instagram.com/mhtsos_tzinavos/) · [GitHub @G-Developerr](https://github.com/G-Developerr)
