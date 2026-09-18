# Steering Scout: thinking summary

*The `.md` summary the brief invited, capturing my thinking process and how I used AI tools along the way.*

- Prototype: https://scout-app-five.vercel.app (best on a phone)
- Case study: https://steering-scout.vercel.app
- FigJam board (research, audit, exploration, wireframes): https://www.figma.com/board/9JpWHm8YZRxyR9XY9PzZg6/ConvLLM_PF?node-id=0-1

---

## 1. The brief in my own words

The task asks how a person can **see** what Scout has understood about them, **disagree with or correct** it, and **steer** the experience mid-conversation, on a 375px screen, with one hand, without a traditional filter panel.

The sentence that framed everything for me was this one from the brief: preferences "can accumulate, change, or sometimes be misunderstood without the user necessarily knowing." That is a trust problem before it is an interface problem. The user is being modelled, and cannot see the model.

I also named the trap early so I could keep checking myself against it. A chip strip pinned to the top of the chat, or a bottom sheet titled "understood preferences", is a filter panel wearing a chat costume. Both fail the brief on its own terms.

## 2. Research

I started with the product, not with ideas.

- **The Property Finder portal**, to understand how search and filters work today and what users already expect.
- **The Scout web app**, used on a real phone. I typed real questions and watched how Scout answered, what it showed, and what it left out.
- **Other conversational products**, mainly how Perplexity structures an answer, a composer and voice input, using Mobbin for reference screens. I adapted patterns to property search instead of copying them.
- **Scout's design system**, which I extracted from the live product (colours, type, shadows, the brand gradient) so the proposal would read as part of Property Finder and not as a personal style exercise.

## 3. Audit

I audited the current mobile experience screen by screen on my FigJam board.

1. The hero paragraph sits in white over a photo and fails contrast.
2. The input is type-first. On a phone, speaking a sentence is faster than typing one.
3. The quick-search chips look like buttons but slide in two directions when held, which feels broken.
4. The Market Pulse cards are inconsistent and pull focus from the search area.
5. Choosing a recent conversation does not close the side panel, which costs an extra tap.

I then tested **language switching inside one conversation**: English, then Chinese, then Arabic. The prose followed me, but names and labels inside the results stayed in English. For a non-English reader that is exactly where understanding breaks. I also noted that tapping the input after a result makes the page jump wider, like an accidental zoom.

**The finding that set the direction.** I asked the live Scout for "New Emaar launches in Dubai South under 2M". It returned projects that were already ready and earlier phases that were sold out, and never said so. Scout had made a call about what "new" means, which is reasonable. The user never saw the call, so they could neither agree nor disagree with it. That is the brief's problem, caught in the live product.

The full audit, 14 findings ranked by priority, is in section iii of the case study.

Later I ran a second audit, comparing my own prototype against the live product and checking accessibility on both. It found real problems in my work (zoom was locked, the brand green and red failed contrast as text, invented listing data contradicted the real figures) and I fixed them.

## 4. Brainstorming and structure

I broke the single brief into **three questions**:

- **Visibility.** How does the user see the model Scout is working from, without breaking the conversation?
- **Correction.** How can they disagree with one piece of it in a single thumb tap?
- **Steering.** How can they add a priority, drop an old one, or branch to a new angle?

And into **three moments** a real user meets, in their own voice: after Scout replies ("did it understand me, or fill in blanks?"), while composing ("I want to change one thing, not re-explain everything"), and after a misunderstanding ("these are not what I meant, roll back"). Correction is a moment, not a screen.

Then I asked what conversation can do that a filter panel cannot. A filter holds a value. A sentence holds a value, a **source** (the words that created it), a **confidence** (stated or guessed), a **moment in time**, and an **interpretation** ("family" expands to bedrooms and schools). Those became the material to design with.

Before drawing anything I wrote **four principles** and used them to reject my own first ideas:

- **Provenance over panel.** If it could exist as a filter panel with the labels changed, it is not conversational.
- **Correction cheaper than typing.** If a fix costs more than re-explaining, people re-explain.
- **Confidence is a visual property.** Stated and inferred cannot look the same.
- **Undo before UI.** A gesture to unsay something comes before any new surface.

## 5. Ideation

I generated eight concepts and scored each against the three moments and the four principles.

**Taken forward**

1. **In-message provenance.** The phrases in Scout's answer that came from a preference are underlined: solid for what the user said, dashed for what Scout assumed.
2. **Composer predictions.** Likely corrections offered as one tap instead of a typed sentence. In the prototype this became the Refine rows under each answer, the suggestions in the text sheet, and Scout's own question back to the user.
3. **Long-press to unsay.** Hold an assumed phrase, see where it came from, drop it, and Scout re-answers.

**Set aside, and why**

4. A running "currently looking for…" sentence. It duplicated concept 1.
5. A pull-down memory card. The closest to a panel, kept only as a benchmark.
6. Swipe to rewind a whole turn. Too coarse. A phrase is the right unit.
7. A "what do you know about me?" utterance. The user has to know the trick. Kept as a possible answer to long threads.
8. An ambient "based on 3 things you said, 2 I guessed" caption. It moves the work to a second screen.

I also rethought the **input**. Voice leads and typing is one tap away, because people describe a home in sentences. Speech can be misheard, and a misheard preference is the brief's problem all over again, so the transcript is shown for review, with Edit and Re-record, before anything is sent. That confirm step is the first place the user sees what Scout understood.

## 6. Wireframing

I drew the flow before any screen, to make sure seeing, disagreeing and steering all happen in one place: the answer. Nothing sends the user to a settings surface.

Then seven lo-fi states at true 375px, starting from a hand sketch: landing, history, text input, voice, confirm, answer, and the provenance card. Working at the real width settled the structural decisions early:

- The greeting is the hero of the landing, and everything else recedes.
- The profile sits on the left and opens conversation history.
- History is full width, not a drawer, and closes itself when a conversation is picked. This answers audit finding 5.
- No bottom tab bar.
- The composer is a launcher: the field opens a text sheet, the waveform opens voice.
- The provenance card sits directly under the prose it explains, not in a global sheet.

## 7. Refining with the new UI

The hi-fi prototype uses Property Finder's palette and the Inter typeface, with Noto faces for Arabic, Chinese, Japanese and Hindi, in light and dark mode.

- **See.** The answer itself is the summary of what Scout understood. Solid underline means "you said it". Dashed means "Scout assumed it". No chip strip, no sheet, no panel.
- **Disagree.** Holding a dashed phrase opens a card that quotes the user's own words, explains the assumption, and previews the consequence ("Without it: 7 projects, +2"). Unsay drops it and re-answers as a new turn. The old phrase is struck through so the thread stays honest, and the listings really change: the ready projects come back as cards.
- **Steer.** Scout asks back with tappable options. Refinements re-answer as a new turn. Dig deeper opens one project inside the conversation. "See all" opens a ranked list of answers, which is not a filter panel. Every step becomes a turn, so the history of decisions is the conversation.
- **One colour rule: solid is you, gradient is Scout.** The brand gradient appears only where the AI is present: listening, thinking, speaking, explaining. Everything the user controls is solid. I introduced this because a single accent colour made the product feel flat, and I wanted the gradient to mean something instead of decorating.
- **Languages.** Six languages in one thread: English, Arabic, Chinese, Japanese, Russian, Hindi. Direction belongs to the message, so an Arabic answer reads right to left while navigation never changes sides. Names, labels, prices, buttons and the read-aloud voice follow the reader. What the user said earlier carries across languages and is quoted in its original script. This answers the multi-language audit.
- **Accessibility.** I checked every state against WCAG 2.2 AA with automated tooling, then fixed contrast problems the tooling missed. Pinch zoom, keyboard access and reduced-motion settings are respected, and anything that moves on its own has a pause control.

## 8. What is real and what is simulated

I would rather be plain about this than have it discovered.

- **Scripted answers.** The prototype's answers are written in advance. Provenance needs structure (which phrase came from which words), and scripting let me show the idea end to end.
- **Real figures.** The Emaar South projects, prices, down payments, handover quarters and the Market pulse numbers mirror what the live Scout returned.
- **Illustrative listings.** The Dubai Marina and villa listings, and the result counts for the quick searches, are illustrative.
- **AI-generated photos.** The listing photos are AI-generated and do not depict the real buildings.
- **Voice.** Voice input is simulated with a fixed transcript. Listen uses the device's own speech voices.
- **Translations.** The non-English copy was drafted with AI and needs a native review before anyone relies on it.
- **Not built.** The Map and Sources tabs are placeholders.

## 9. What I would test next

None of this has been tested with users yet, and it has not been tried with a real screen reader. Both come first. The questions I would take into research:

- **Discoverability.** Underlines are subtle. Does a first-time user realise a phrase can be held? I would try a coach mark on the first assumed phrase only, and measure the first-hold rate.
- **Legibility.** Do two underline styles feel busy in longer answers? I would cap highlights per answer and compare comprehension.
- **Latency.** Unsay re-runs a search. On a slow network I would dim the affected phrases in place and re-render only the listings.
- **Trust over long threads.** After many turns the chain of assumptions gets long. A "what do you know about me?" summary on demand is the first thing I would try.
- **Prediction quality.** Refinements that miss add noise. I would show them only above a confidence threshold and log taps against dismissals.

## 10. How I used AI

I used AI heavily, and I directed it.

**Tools**

- **Claude (Claude Code)** as my main working partner: research synthesis, structuring the audit, drafting copy, and writing the code for the case-study site and the prototype.
- **FigJam** for my own research, audit notes and sketches, which is where the thinking started.
- **Mobbin** for benchmark references.
- **Higgsfield** for the listing photos and for exploring the voice-sphere motion. The final sphere is rendered from code.
- **axe-core** for automated accessibility checks.
- **GitHub and Vercel** to host both sites.

**What I decided**

The direction and the judgement calls are mine: the framing of the problem, the audit findings, the four principles, which concepts went forward, voice first with a review step, profile on the left, full-width history, no tab bar, Inter as the typeface, the "solid is you, gradient is Scout" rule, translating listing names on the card, showing real result counts with a full list, the auto-moving Market pulse, and replacing the new-chat plus icon because plus already meant "add a refinement". I reviewed the build repeatedly and sent it back with corrections.

**What AI did**

It turned those decisions into working screens quickly, proposed options when I asked for them, caught problems I had not seen (the locked zoom, the contrast failures, my invented data contradicting the live product) and drafted the non-English copy. When it got things wrong, I caught that too: a default read-aloud voice that sounded wrong, English names left inside translated cards, a label that stayed in English.

AI did not replace the thinking. It let me take an idea all the way to something a person can hold in one hand and argue with, which is the best way I know to test whether the idea is any good.

## 11. What I want to discuss in the technical interview

Three things I would love to open up with the team:

1. **The chip-strip trap.** Has Scout's team already had the internal argument about a preferences chip strip, and what decided it? My position that any panel-shaped fix is a filter panel in disguise is opinionated, and I want to hear where it does not hold.
2. **The cost of predictions.** Refinements and Scout's question back only work if they arrive quickly and are usually right. I would like to understand how the backend could produce a few high-confidence corrections as the answer lands: cached, streamed, or computed with the reply.
3. **Languages in practice.** Following the user's language per message is easy to describe and harder to ship. Does Property Finder already have a signal for language use per user? Would per-message direction and localised listing names fit the current data and session model, for example through an identifier-based system that renders names in the reader's language?

---

*Rauf*
