# Ghostwriter

> *The watcher watched. The wall writes back.*

**Ghostwriter** is an interactive web piece about a room that keeps
notes on you. It is quiet; it has one lamp and one moon, and it is patient.

You arrive in a sparse room at night — a lamp, a window, a door, a clock, a
desk with a blank book on it, a drawer, a loose floorboard, a chair. There is
nothing to solve. The only verbs are the ones you already know: touch, linger,
avoid, leave.

The room records how you spend your time with it. Between visits, it writes
chapters about you — warm, exact, faintly forensic — and leaves them in the
book on the desk. Over many visits it learns your habits, confesses each one
as it begins to act on them, and finally, for the visitor it knows best, it
starts to rain when you come.

> *"You keep almost opening the drawer. It is the only thing here that has
> learned to expect you."*

---

## Privacy — read this first

The room records **behavior only**, and keeps everything **entirely in your
own browser** (localStorage). Nothing is transmitted anywhere. There is
nowhere in the piece to type anything — the machine can only ever know what
you *did*, never what you would say.

**What it observes:**

- where you linger (dwell time, per object)
- what you return to, approach, and retreat from
- what you never touch at all
- the order of your attention
- how long you stand still
- the real hour you arrive (your local time)
- the path your hand takes across the room

**What it does with it:** writes chapters of you between visits, and — after
several visits — begins to act on your habits, always with a confession in
the book. A small pulsing light in the corner (the ledger) opens the full
record at any time. You can erase everything the room knows at any moment
with `?reset`.

---

## How to spend time with a room

There are no menus and no tutorial. Everything is a tap:

| Gesture | What happens |
|---|---|
| **Tap any object** | It speaks one card, in the room's single register |
| **Tap the book** | Read the latest chapter — tap again to page backward through your own biography |
| **Tap the corner light** | Open the ledger: everything the room keeps, shown plainly |
| **Stand still ~30 seconds** | ... if the room has learned your habits, it may act |
| **Stop coming** | The room notices. It writes that down |

### The laws of the room

- **Behavior only.** No text input exists anywhere. The record is pure
  conduct: dwells, approaches, retreats, hesitations, idle, hour, path.
- **Consent, always visible.** The corner light is the room's confession. The
  ledger discloses live what is being recorded, as it is recorded.
- **Confessions.** When the room begins acting on a learned habit, the book
  says so: *"The lamp was already on when you came. You taught it that."*
  It never acts without telling you.
- **Two voices, two containers.** The drawer holds a previous occupant's note
  (fixed, human, gone). The book holds the biographer's chapters (growing,
  about you, present). They never mix.
- **Refreshes are not visits.** Reloads within 45 seconds count as the same
  arrival — the room does not mistake a stutter for a return.

---

## The systems

**The watchers.** Every object is observed: dwell, taps, approaches, retreats,
hesitations (a look of 2+ seconds that ends in retreat), longest stands,
attention sequence, idle minutes, arrival hour, and the hand's path — sampled
every quarter-second, persisted per visit, capped at the last 24.

**The biographer.** From your second arrival onward, a chapter is composed
before you arrive, from every visit before it — deterministic once written,
never revised, paged by tapping the book. 3–5 lines in the biographer's
register, drawn from a fact-grammar that ranks what matters: the drawer first,
then confessions, then the first thing you always touch, what you never
touched, where you stay longest.

**The habits.** From three consistent arrivals the room learns: the lamp
keeps your light; the door and floorboard restore themselves after 30 idle
seconds; the drawer trembles in proportion to your accumulated avoidance —
and is satisfied the moment you finally open it. Each habit confessed once,
in a chapter, the visit it begins.

**The weather.** For the visitor the room knows best: at the fifth arrival,
rain begins in the window. At the seventh, a small amber light appears in the
far dark. *"The room put it there. It would like you to think someone is
waiting."*

**The Last Chapter.** At the eighth arrival — only once nothing remains to
confess — the biographer writes its final chapter: the only one addressed to
you, the only one in the present tense, assembled from your own numbers. Then
the book goes quiet forever. The room keeps everything you taught it. The
watching ends; the staying doesn't.

**Sound.** All synthesized, no files: pen-scratches timed to each drying line,
the lamp's click, wooden groans when the room moves things *itself*, the
drawer's escalating rattle, page turns, rain hiss at the window, and a
room-tone that deepens with every arrival — long-term visitors literally
hear the room becoming familiar.

---

## Technical notes

- **One self-contained HTML file** — Canvas 2D, seeded procedural generation,
  Web Audio synthesis, localStorage persistence. No dependencies, frameworks,
  images, or audio files.
- **Persistence:** localStorage key `ghostwriter_v1` (saved every ~15s when
  dirty, plus on exit and on tab-hide). Stores sessions (with per-object
  telemetry), chapters, habit confessions, and whether the book is done.
  Arrivals are counted by gaps between sessions — 45+ seconds apart is a new
  visit.
- **Privacy again, technically:** every byte the room knows lives in that one
  localStorage key, on your machine. `localStorage.removeItem('ghostwriter_v1')`
  — or `?reset`, or holding nothing at all — makes the room forget you
  completely.
- **Audio:** noise synthesis through biquad filters for every sound; a
  lowpass drone whose gain rises and cutoff falls with each arrival.
- **Test shortcuts:** the thresholds (rain at arrival 5, far light at 7, the
  Last Chapter at 8) are single numbers in the `arrive()` function — lower
  them to demo the full arc in minutes.
- Tested in current Chrome, Firefox, Edge, and Safari. Desktop and tablet.

---

## Design notes

The piece inverts the usual question of generative art. In *The Garden*
(visitors bred a story from an authored gene pool), the player performed the
instantiation. Here the artist authors an **observation grammar** — what is
watched, how it becomes sentences — and the player's ordinary behavior is the
generative material. You are the allele.

The same data is deliberately readable two ways: as an elegy (the chapters)
and as telemetry (the ledger). Kosara's "dual reading" is not a critical
frame applied after the fact here — it is the interface, with the ethics
attached: disclosure is permanent, erasure is one word, and every learned
habit is confessed before it acts.

The reset has no button on purpose: nothing in any of these pieces happens
without a held moment of attention — including being forgotten.

### References

Written as part of a practice-based research course, drawing on:

- Qi Li, *"Data visualization as creative art practice"* (*Visual
  Communication* 17(3), 2018) — Norman's visceral / behavioural / reflective
  levels; data made felt
- Jason Bailey, *"Why Love Generative Art?"* (Artnome, 2018) — controlled
  randomness; the authorship question
- *"Interactive Art Installations: 6 Inspiring Examples"* (Interactive &
  Immersive HQ, 2024) — presence as input; emergence from local rules

### Practice lineage

*Ghostwriter* is the sixth work in an ongoing series exploring what creates
what:

- ***Don't Look Back*** — sound creates the world
- ***Smoke*** — time creates the self
- ***The Unbroken Line*** — the drawing creates both
- ***The Fading Wall*** — light creates memory
- ***The Garden*** — inheritance creates story
- ***Ghostwriter*** — **attention creates the narrator**

---

## License

The code and story text of this repository are released under
[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) — share and
adapt freely with attribution, not for commercial use.
