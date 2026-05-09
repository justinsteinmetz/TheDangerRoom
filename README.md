# The Danger Room

https://justinsteinmetz.github.io/TheDangerRoom/

**A digital Socratic chamber for Grades 11–12.**  
Issued under Assessment Protocol VI-DR · Verity Institute, Division of Internal Review.

Five propositions about identity. Students commit to a position, receive pressure specific to what they said, decide whether to hold or move, and explain their reasoning. The full record is read and interpreted by the model at the end.

---

## The mechanic

Each proposition runs a three-stage cycle:

1. **Commit** — the student writes their position in their own words. No multiple choice. The Submit button is locked until they've written enough. What they write is what the model reads.

2. **Pressure** — the model responds directly to their specific answer. It does not argue the other side. It finds the most uncomfortable implication of their own position and stays there. Under 120 words. Every sentence is traceable to what they wrote.

3. **Hold or move** — three options: *I hold my position. Something moved. I'm not sure.* Each triggers a follow-up prompt requiring at least 25 characters of explanation:
   - Held → *What still convinces you?*
   - Moved → *What changed?*
   - Unsure → *What remains unresolved?*

The Next button stays locked until the reflection is written. One-word responses don't pass.

---

## The five propositions

| # | Proposition |
|---|---|
| I | To what extent is identity socially constructed? |
| II | Are individuals responsible for beliefs they inherit? |
| III | Is conformity necessary for social life? |
| IV | Can authenticity exist? |
| V | Do actions define who we are more accurately than intentions? |

Each has a tailored pressure instruction. The model is told precisely where the discomfort lives for each proposition — not generically, but in response to the specific position the student committed to.

---

## The record

After all five propositions, students see their full session record: each proposition, their position, the pressure applied, their reflection sentence, and their verdict (Held / Moved / Unsure). The record is formatted as an institutional dossier — labelled rows, session ID, timestamp.

While the record renders, *The room is reading the record…* appears. When the synthesis arrives, the loading text fades out and the synthesis fades in.

The model reads the complete record and generates a closing synthesis of 60–90 words. The synthesis prompt instructs the model to:

- Treat reflection sentences as the most honest data in the record
- Identify contradictions between verdicts and reflections
- Name the moment pressure actually landed — not count outcomes but interpret the pattern
- Avoid moralising, praise, or therapeutic language
- Write in second person, cold and specific

---

## Design language — Verity Institute

The aesthetic is deliberately institutional. Cold, overlit, clinical. The horror is in the normalcy.

**Palette** — off-white background (`#f0f0ed`), cold grey surfaces, desaturated teal as the sole accent, warm brown for the pressure text. No red. No dramatic darkness. The dread comes from the mundanity.

**Typography** — IBM Plex Sans and IBM Plex Mono throughout. The font of internal documentation and technical reports.

**Institutional framing** — the intro screen reads as a departmental form: *Verity Institute / Division of Internal Review / Assessment Protocol VI-DR*. A session ID is generated on load and carried through to the record header. The propositions sit in a bordered table. The record is a dossier. The synthesis appears under a "Synthesis" label.

**The pressure box** — darker background, stronger border, brown left rule. More authority than the surrounding interface. The room doesn't raise its voice. It just has a different weight.

**Core principle** — the previous dark version asked: *"What happened to your ideas?"* This version asks: *"What did the system discover about you?"* That shift makes the experience more unsettling and more memorable.

---

## Design principles

**"Either is allowed. Neither is scored."** The tool records reasoning, not performance. Moving is not weakness. Holding is not strength.

**Pressure is specific, not oppositional.** The model does not argue the other side. It finds the uncomfortable implication of the student's own position. This is the difference between a debate and a Socratic chamber.

**Reflection is mandatory.** Selecting Held/Moved/Unsure without explaining the reasoning produces no data worth reading. The 25-character minimum exists to prevent the reflection from being a gesture.

**The synthesis reads the full record.** A student who says "Unsure" but writes a clear and confident reflection sentence is more certain than they admitted. The model is instructed to notice this.

---

## Classroom use

**Time:** 35–50 minutes, depending on how long students spend on each reflection.

**The result is private by default.** Students choose what, if anything, leaves the room.

**Discussion entry points:**
- "Where did the pressure land — and why that proposition?"
- "Did you hold a position you're now less sure about? Did you move on one you're now more sure about?"
- "What's the difference between the position you committed to and the reflection you wrote after holding it?"
- "The synthesis named something. Is it accurate? Where is it wrong — and why might it be wrong in that specific way?"
- "What does it mean that your thinking was processed and interpreted by an institutional system?"

**The propositions are shown on the intro screen.** Students know what's coming. Knowing does not help.

---

## Abitur Themenfeld relevance

| Themenfeld | Angle |
|---|---|
| The Individual & Society | Identity formation, conformity vs. individualism, authenticity, social construction of the self |
| Politics, Culture & Society — UK/USA | Inherited belief, responsibility, the gap between stated values and action |
| Science & Technology | The institutional processing of identity; algorithmic assessment; what it means for a system to interpret you |

---

## Technical architecture

Uses a Cloudflare Worker as a server-side proxy to the Anthropic API. The API key is stored as a Cloudflare environment secret and never exposed in the browser.

The tool makes six API calls per session: one per proposition (five, for the pressure responses) and one final call for the synthesis. All calls are proxied through the Worker.

The Worker URL is hardcoded in `index.html` as the `PROXY` constant:

```javascript
const PROXY = "https://anthropic-proxy.justin-steinmetz.workers.dev";
```

### Worker deployment

See the *Who Are You, Really* README for full Worker deployment instructions. The same Worker handles both tools — no additional setup needed once it's live.

### HTML deployment

Single file. No dependencies, no build step. Rename `danger-room-v2.html` to `index.html` and push to a GitHub Pages repository.

---

## Expansion

The Danger Room is a platform. The engine — commit → pressure → hold/move → reflect → synthesise — is stable and reusable. Only the propositions and their pressure instructions change between thematic versions.

Planned expansion packs: The Empire Room (colonialism and power), The Assembly Room (MUN/sovereignty), The Rights Room (human rights), The Future Room (technology and society).
