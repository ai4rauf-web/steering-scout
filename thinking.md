# AI-thinking summary — Steering Scout

*Submitted as the optional `.md` reflection the brief invited: "you're welcome to share an .md summary from any AI tools you used to capture your thinking process."*

## How I approached the brief

I read the task twice before opening a tool. The line that framed everything for me was this one:

> "In an LLM-powered experience, those preferences are inferred through conversation, they can accumulate, change, or sometimes be misunderstood without the user necessarily knowing."

That sentence names the actual design problem — not steering, not correction. **Trust in a model of yourself you never chose to build.** Every downstream decision — the provenance vocabulary, the long-press unsay, the composer prediction pattern — is a consequence of taking that sentence seriously.

## What I did before designing

I audited the current Scout product on a real mobile viewport, not from screenshots. I typed a real query, watched Scout reply, and looked for how it acknowledged what it had understood. It didn't. That absence, more than any positive design idea, became the anchor. The audit produced 14 findings organised P0/P1/P2 (Section iii of the case study), and the strategic finding — *"the empty state is a landing page; Scout is a chat"* — is the reason the steering problem exists at all. If the surface never asks the user to think of the interaction as a conversation, of course preferences arrive silently and drift silently.

I also extracted the actual PF design system (Open Sans, secondary-07 purple accent, purple-tinted shadows, `--gradient-hero-overlay` token exists but is unused) so the proposal reads as a fit for the product, not as a designer's aesthetic exercise.

## Where the direction came from

I framed the problem as *three linked questions* — Visibility, Correction, Steering — and *three friction moments* — After Scout replies (Moment A), While composing the next reply (Moment B), Right after a misunderstanding (Moment C). A concept had to solve at least two moments to earn advancement.

I sketched eight divergent concepts. Three cleared the bar:

1. **In-message provenance highlights** — amber underline for stated, dashed dusk for inferred, both rendered inside Scout's reply prose. Covers Moments A and C.
2. **Composer prediction pills** — three predictive corrections appear when the composer opens. Covers Moment B.
3. **Long-press to unsay** — the correction card is anchored to the specific inferred word, not a global sheet. Covers Moment C.

Together they form one interaction model. The provenance vocabulary teaches the user what to trust; the composer predicts the next steer; long-press reverses any inference with one gesture.

## Four principles I designed against

Before I drew anything I wrote four rules, and used them to kill my first three concepts:

- **Provenance over panel.** If a concept could exist as a filter panel with the labels changed, it isn't conversational.
- **Correction cheaper than typing.** If a fix takes more taps than re-explaining, users just re-explain.
- **Confidence is a visual property.** Stated and inferred are different objects with different rights. They cannot look the same.
- **Undo before UI.** A gesture to unsay a phrase belongs in the interaction model before any new surface does.

## What I chose to invest craft in

Two places, deliberately:

1. **The visual vocabulary of provenance.** Amber underline for user-stated phrases, dashed dusk for Scout-inferred phrases. I let the case-study document itself teach the vocabulary — the same underlines appear in the prose throughout, so by the time the reader sees them on the mobile mockup they already read as familiar.

2. **The Arabic RTL treatment.** The JD names Arabic RTL and MENA code-switching as desirables, and I built the RTL variant end-to-end — a mirrored empty state, the same three moments in Arabic (Read / Correct / Steer), a five-moment interaction model for language auto-detection, and a "what flips / what doesn't" table with the Unicode Bidi behaviour called out. The point of the section is that direction can be an *emergent property of what the user types* — not a settings toggle — and the steering system was designed for language, not for a specific axis, so nothing fights the flip.

## What I explicitly did not do

- **No polished visual mockups beyond three frames.** The brief said polished UI isn't expected; I invested in *thinking* over *finish* and made three mid-fidelity phone frames per direction (LTR + RTL).
- **No animated prototype.** Time budget was 2–3 hours; a Framer prototype eats that whole budget for one moment of interaction. The trade was correct for this brief.
- **No branded aesthetic mimicry.** I extracted PF's design system as a reference, but the case study renders in a neutral typographic identity (Fraunces + Instrument Sans) so the reader focuses on the argument, not on whether I matched Property Finder's palette.

## What I would test first if this shipped

I listed six tradeoffs in the case study (Section x), each with a specific research question. The top three:

1. **Discoverability of the underlines.** Are provenance highlights subtle enough to feel native to the prose, but obvious enough that a first-time user notices they're tappable? I'd add a first-run coach mark on the first inferred word only, and measure first-tap rate over three sessions.
2. **Composer prediction quality.** If the predictions frequently miss, they add noise instead of removing typing. I'd show pills only above a confidence threshold and log tap-through vs. dismiss.
3. **Trust drift over long sessions.** After 20 turns, the provenance chain gets long. A `"what do you know about me?"` meta-utterance flattens the chain into a scannable summary on demand — I kept it in the pile as an ambient hint, not a primary affordance.

## How I used AI in producing this

Every piece of user-facing writing, structure, and design in the deliverable is mine. I used Claude as a working partner to:

- **Stress-test the framing.** After I read the brief, I asked it to challenge my initial framing and surface angles I might miss — that's how the "three friction moments" structure crystallised.
- **Rapid prose iteration.** For the case-study document, I wrote key phrases and let AI produce candidate sentences that I then edited. The document went through five prose passes.
- **The RTL Arabic content.** I don't write Arabic natively. I checked every Arabic sentence in the deliverable against three independent MSA translations before finalising, and adjusted where the literal translation broke the interaction's tone.
- **The design-system extraction.** I inspected `:root` and computed styles on `propertyfinder.ae/scout/v2` directly. AI helped me structure the tokens into a readable reference and flag the unused `--gradient-hero-overlay` token as a fix that's already scaffolded in the codebase.
- **The SVG mockups.** I drafted the layout and interaction detail; AI wrote the SVG scaffolding, which I then adjusted for typography, alignment and detail.

I did not use AI to make design decisions. The direction — provenance over panel, correction inside the message, undo before UI, the RTL-as-emergent claim — is authored, not generated. AI accelerated the *production* of what I had already decided.

## What I want to discuss in the technical interview

Three things I'd love to open up:

1. **The chip-strip trap.** I want to hear whether Scout's team has already had the internal argument about a preferences-chip strip, and what killed it (or didn't). My framing of *"any panel-shaped fix is filter-panel-shaped in disguise"* is opinionated; I'd want to hear where it doesn't land.
2. **The composer prediction cost.** Prediction pills only work if latency is low. I'd want to hear how the Scout backend handles the "user has focused the composer, produce three high-confidence corrections in <500ms" problem — is it cached, streamed, or precomputed on the last reply?
3. **The RTL rollout in practice.** Auto-detecting direction from the first message is easy to describe and harder to ship. I'd want to hear whether PF has an existing telemetry signal for language use per user, and whether per-conversation direction storage would fit the current session model.

---

*Rauf · September 2026*
