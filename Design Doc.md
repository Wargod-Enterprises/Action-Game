# Action Game: Design Doc

**Created by:** David Anthony Martinez
**Working title:** Megametroidvania
**Doc started:** 10/07/2026

---

## Core idea
A **Mega Man-style action platformer** with **beat-'em-up** close combat, **Contra** intensity and **metroidvania** exploration, driven by **RPG-style progression** (skill trees and scaling enemies).

> Mega Man movement and shooting + Contra intensity + beat-'em-up dash/melee + metroidvania exploration + skill-tree progression.

This game split off from the stealth "Agent" concept (`Projects\Agent Game`). This one is about power growth and aggressive action, and the Agent game is about scanning, planning and stealth.

---

## Player moves
| Move | Notes |
|---|---|
| Run, jump | Mega Man feel: tight, responsive |
| **Wall jump** | Movement and exploration |
| **Dash** | Movement, and it **does damage** (beat-'em-up feel) |
| **Melee** | Close-range attack |
| **Buster** | Standard shot; hits ground and air enemies |
| **Charge shot** | Hold to charge; the heavy hitter |

**Feel:** aggressive and up close. Dash and melee should be fun enough that you *want* to get in close, with the buster and charge shot as what you fall back on for tougher armor.

### Weapon & melee switching (idea, undecided)
Multiple weapons and multiple melee styles, with L for weapons and R for melee. Two options:
- **Hold menu:** hold L1 (weapons) or R1 (melee) to open a menu and pick with the d-pad. Time **slows down** while it's open (no full stop).
- **SNES-style cycling:** tap L or R to scroll through weapons or melee styles; the current pick shows on screen.
- *Claude's suggestion:* combine them, so a tap cycles and a hold opens the menu.

Depends on how many weapons and melee styles there are, which depends on the weapons and armor work.

---

## Enemies: armor tiers
Enemy *type* (ground or air) doesn't change the rules, because the buster already hits fliers. **Armor** decides what works:

| Armor | Hurt by (at the start of the game) |
|---|---|
| **Weak** | Dash, melee, buster, charge shot |
| **Medium** | Buster, charge shot (melee and dash *clang* off) |
| **Heavy** | Charge shot only (buster bounces off) |

- Any enemy can have any tier: a weak flying drone, a heavy armored gunship, and so on.
- Each tier needs clear visuals (color or plating) so players can read it at a glance.
- Wrong-tool feedback: sparks, a clang sound, and possibly a small stagger for the player.

---

## Progression
- **Skill tree per move** (dash, melee, buster, charge, movement).
- **Upgrades break the armor rules, and that's built into the progression.** Examples:
  - Melee tree goes up to "cuts medium armor"
  - Dash tree goes up to "rams through medium armor"
  - Buster tree goes up to "chips heavy armor"
- **Enemies scale through the game.** A late-game weak enemy can be as tough as an early heavy enemy, but you've grown too, so it still *feels* weak.
- The armor tier rules stay the same throughout the game; only the numbers (health and damage) scale.

---

## Bosses & quests
- Bosses **don't** give you their powers (a deliberate break from Mega Man).
- Bosses drop **items** that belong to NPCs. Returning an item earns progression: skill points, upgrades, or new abilities taught by the NPC.
- Ability gating for the metroidvania map still works, just indirectly: NPC rewards open new areas.
- Idea: different NPCs give different kinds of rewards (skill points, weapon upgrades, map info for hidden rooms).

---

## Exploration (metroidvania)
- A connected map with backtracking
- Hidden items and secret rooms
- Areas gated by movement upgrades (wall jump, dash and so on) and NPC rewards

---

## Contra influences
- **More enemies on screen** than Mega Man; waves to plow through with dash and melee
- **Set pieces:** big multi-part bosses, chase sequences
- **Run-and-gun momentum**
- **Not** taking one-hit deaths, since there's a health bar to support the progression

### Vehicle sections
Occasional shmup-style sections, like Contra's perspective changes:
- **Horizontal:** a chase through traffic lanes
- **Vertical:** climbing or descending, with enemies coming from above or below
- Vehicle style leans toward **Blade Runner** (moody flying cars).
- The armor tier rules apply here too (rapid fire vs. a charged or missile shot).
- Use sparingly, for transitions between areas or story set pieces. Could later become fast travel.

---

## Setting
**Undecided.** Cyberpunk was the working direction (a vertical megacity, neon, rain, Blade Runner vehicles), but it's open now that the Agent game has its own high-tech world.

---

## Inspirations
*Mega Man X*, *Mega Man ZX*, *Contra*, beat-'em-ups, *Hollow Knight*, *Axiom Verge*, *Blade Runner* (vehicles and mood)

---

## Open decisions
1. **Setting:** cyberpunk or something new?
2. **Story & protagonist:** undecided.
3. **Skill tree contents:** what each tree unlocks, and at what point upgrades break which tier.
4. **How skill points are earned:** kills/XP, items from exploration, NPC quests, or a mix.
5. **What unlocks hidden rooms:** movement abilities, NPC rewards, something else?
6. **Vehicle progression:** separate upgrades, or shared with the player's stats?
7. **Title:** undecided.
8. **Weapons & melee styles:** how many of each, how they interact with armor tiers, and whether every weapon can charge. This decides the switching method (hold menu vs. cycling).

---

## Next step
**Test room prototype:** move, jump, wall jump, dash, melee, buster, charge, with one enemy per armor tier (including a flier) and a debug toggle to simulate upgrades that break armor.
