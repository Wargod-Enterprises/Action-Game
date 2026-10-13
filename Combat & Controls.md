# Action Game — Combat & Controls Design Handoff

## Overview
2D action-platformer inspired by Mega Man X, Contra, Metroid, and Castlevania,
with a real beat-'em-up melee layer alongside shooting. Weapons double as
progression keys (metroidvania-style gating, tied to the armor-tier idea).

Status legend: [DECIDED] = confirmed by David. [PROPOSED] = suggested, not yet
confirmed — implement as a default that's easy to change.

---

## 1. Controls [DECIDED]

| Button | Function |
|---|---|
| Melee | Melee attack (context-sensitive, see §3) |
| Shoot | Fire current shot weapon (hold = charge) |
| Jump | Jump |
| Dash | Dash (also a body attack) |
| L | Tap: cycle shot quick slots. Hold: open shot menu |
| R | Tap: cycle melee quick slots. Hold: open melee menu |
| D-pad | Movement; directional modifiers for attacks; menu navigation |

---

## 2. Ranged System [DECIDED]

- **Default shot:** straight.
- **Trajectories (weapon types):** stream, spread, homing, placed, arc,
  boomerang, ricochet.
- **Charge:** a modifier, not a weapon. Hold Shoot to charge whatever shot
  weapon is equipped.
- **Shield:** belongs to a separate defense category, not ranged.
- **Claw:** pull/grapple, not ranged.

[PROPOSED] Each weapon = trajectory + effect. Effects: pierce, explode,
freeze, pull, break blocks, burn. Open question: one fixed effect per
trajectory vs. effects as global upgrades (see §8).

---

## 3. Melee System

[DECIDED] Melee includes a dash body attack and melee weapons. Goal: keep a
real beat-'em-up feel even though jump and weapons have separate buttons.

[PROPOSED] Context-sensitive moveset on the single Melee button:

| Input | Result |
|---|---|
| Melee (repeated taps) | 3–4 hit combo; final hit knocks back |
| Up + Melee | Launcher / anti-air |
| Down + Melee | Sweep / low hit |
| Melee near stunned enemy | Grab; then direction + Melee to throw |
| Melee while airborne | Air attack |
| Down + Melee while airborne | Dive / ground pound |
| Dash | Body-attack dash (damages on contact) |
| Melee during Dash | Dash strike finisher |
| Melee + Jump together | Crowd-clearing special, costs a little health |

[PROPOSED] Starting melee weapon types, each playing differently:
- **Fast** (saber/fists): quick combos, default brawler feel.
- **Heavy** (hammer/axe): slow, big knockback, breaks blocks/armor.
- **Reach** (chain/whip): long range; hosts the claw grapple (pull enemies,
  pull items, swing from points).

[PROPOSED] Design rules for melee:
- Melee must out-reward shooting at close range (more damage, stun, or
  refills weapon energy on hit/kill).
- Support cross-button combos (launch → shoot in air; freeze shot → shatter
  with melee).
- Include brawl-arena rooms where groups surround the player.

---

## 4. Quick Slots [DECIDED]

- Two separate quick-slot sets: **L = shot weapons**, **R = melee weapons**.
- Only a few weapons per set are available for quick swapping; the full
  arsenal can be large.
- [PROPOSED] 3 slots per set. Tapping cycles one direction and wraps.

---

## 5. Hold Menu [DECIDED]

- **Hold L** → pauses game, opens the shot menu (shot weapons only).
- **Hold R** → pauses game, opens the melee menu (melee weapons only).
- **Left/Right** selects which quick slot to fill.
- **Up/Down** scrolls the full list of owned weapons of that type.

Layout: quick slots in a row across the top; full weapon list vertical below.

[DECIDED] **Two jobs, two speeds:** tap-cycling (§4) is for swapping in the
middle of Contra-style action and never stops the game. The hold menu is for
setting up a loadout before a fight, so it **fully pauses** (no slow-motion).

[PROPOSED] Menu behavior:
- **Release L/R** confirms and unpauses (no confirm/cancel buttons needed).
- Menu opens with the currently equipped weapon highlighted, so an instant
  release changes nothing.
- Choosing a weapon already in another slot swaps the two (no duplicates).
- Show a short description/icon for the highlighted weapon.

---

## 6. Input Handling Notes [PROPOSED]

L/R need tap-vs-hold detection:
- On press: start timer, do nothing yet.
- If released before ~300 ms → cycle quick slot (on release).
- If held past ~300 ms → pause and open menu.
- While menu is open: D-pad navigates; releasing L/R confirms and closes.
- Make the threshold a tunable constant.

Melee + Jump pressed within a small window (~1–3 frames) = special move;
make the window tunable.

---

## 7. HUD [PROPOSED]

- Always show current shot weapon (left side) and current melee weapon
  (right side), matching L and R.
- Show charge level while holding Shoot.
- Show health and weapon energy (if weapons use energy).

---

## 8. Progression & Gating

[DECIDED context] Armor tiers / colored-door style gating (Metroid doors):
certain barriers require certain abilities.

[PROPOSED]
- Gates can require a **shot** type or a **melee** type (two kinds of keys).
- Gates check for an *effect* (e.g., "explode"), not one specific weapon,
  where possible, so players have more than one solution.
- Utility examples: freeze shot turns enemies into platforms; heavy melee
  and break-blocks effect open walls; reach weapon/claw grapples to points.

---

## 9. Open Questions
1. Effects: fixed one-per-trajectory, or global upgrades applied to all shots?
2. Final quick-slot count per set (3 suggested).
3. Full melee weapon roster beyond fast / heavy / reach.
4. Weapon energy/ammo: does it exist, and does melee refill it?
5. Shield/defense category: how is it activated with no spare button?
6. How weapons are acquired (bosses, pickups, shops).

## 10. Reference: series inspirations
- MMX: X-Buster charge, boss weapons, Strike Chain (pull items / pull self
  to walls), Zero's saber combos, L/R weapon cycling.
- Contra III: carry two weapons, spread/laser/homing/flame.
- Metroid: colored doors, Ice Beam platforms, Grapple Beam, Screw Attack,
  Speed Booster.
- Castlevania: whip, sub-weapons (axe arc, cross boomerang, holy water),
  whip swing on rings.
- Beat-'em-ups (Final Fight, Streets of Rage): one attack button with
  context moves, grabs/throws, health-cost special.
