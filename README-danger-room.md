# The Danger Room

**A digital Socratic chamber for Grades 11–12.**

Five propositions about identity. Students commit to a position, receive pressure specific to what they said, decide whether to hold or move, and explain their reasoning. The full record is interpreted by the model at the end.

---

## The mechanic

Each proposition runs a three-stage cycle:

1. **Commit** — the student writes their position in their own words. No multiple choice. The Enter button is locked until they've written enough. What they write is what the model reads.

2. **Pressure** — the model responds directly to their specific answer. It does not argue the other side. It finds the most uncomfortable implication of their own position and stays there. Under 120 words. Every sentence is traceable to what they wrote.

3. **Hold or move** — three options: *I hold my position. Something moved. I'm not sure.* Each triggers a follow-up prompt requiring at least 25 characters of explanation:
   - Held → *What still convinces you?*
   - Moved → *What changed?*
   - Unsure → *What remains unresolved?*

The Next button stays locked until the reflection is written. "idk" doesn't pass.

---

## The five propositions

| # | Proposition |
|---|---|
| I | To what extent is identity socially constructed? |
| II | Are individuals responsible for beliefs they inherit? |
| III | Is conformity necessary for social life? |
| IV | Can authenticity exist? |
| V | Do actions define who we are more accurately than intentions? |

Each has a tailored pressure instruction. The model is told where the pressure should land for each proposition — not generically, but in response to the specific position the student committed to.

---

## The record

After all five propositions, students see their full record: each proposition, their position, the pressure applied, their reflection sentence, and their verdict (Held / Moved / Unsure).

While the record renders, the model reads the complete record and generates a closing synthesis of 60–90 words. The synthesis prompt instructs the model to:

- Treat reflection sentences as the most honest data in the record
- Identify contradictions between verdicts and reflections
- Name the moment pressure actually landed
- Not count outcomes but interpret the pattern
- Avoid moralising, praise, or therapeutic language

The loading text (*The room is reading the record…*) fades out. The synthesis fades in. Nothing is resolved. The record is the student's.

---

## Design principles

**"Either is allowed. Neither is scored."** The tool records reasoning, not performance. Moving is not weakness. Holding is not strength. The mechanic models real intellectual engagement rather than debate performance.

**Pressure is specific, not oppositional.** The model does not argue the other side. It finds the uncomfortable implication of the student's own position. This is the difference between a debate and a Socratic chamber.

**Reflection is mandatory.** Selecting Held/Moved/Unsure without explaining the reasoning produces no data worth reading. The 25-character minimum exists to prevent the reflection from being a gesture.

**The synthesis reads the full record.** A student who says "Unsure" but writes a clear and confident reflection sentence is more certain than they admitted. The model is instructed to notice this.

---

## Classroom use

**Time:** 35–50 minutes, depending on how long students spend on each reflection.

**The result is private by default.** Students choose what, if anything, leaves the room. This is stated at the end of the record screen.

**Discussion entry points:**
- "Where did the pressure land — and why that proposition?"
- "Did you hold a position you're now less sure about? Did you move on one you're now more sure about?"
- "What's the difference between the position you committed to and the reflection you wrote after holding it?"
- "The synthesis named something. Is it accurate? Where is it wrong — and why might it be wrong in that specific way?"

**The propositions are shown on the intro screen.** Students know what's coming. Knowing does not help.

---

## Abitur Themenfeld relevance

| Themenfeld | Angle |
|---|---|
| The Individual & Society | Identity formation, conformity vs. individualism, authenticity, social construction of the self |
| Politics, Culture & Society — UK/USA | Inherited belief, responsibility, the gap between stated values and action |

---

## Technical architecture

Uses the same Cloudflare Worker proxy as *Who Are You, Really*. The API key is stored as a Cloudflare environment secret and never exposed in the browser.

The Worker must be deployed before the tool is functional. See the *Who Are You, Really* README for full deployment instructions. The Worker URL is hardcoded in `index.html` as the `PROXY` constant.

### Deployment

Single HTML file. No dependencies, no build step. Rename `danger-room.html` to `index.html` and push to a GitHub Pages repository.

The tool makes two API calls per session: one per proposition (five total, for the pressure) and one final call for the synthesis. All calls are proxied through the Cloudflare Worker.
