---
name: voice
description: Write prose in Ray's (rayhanadev's) writing voice — conversational, curious, hacker-native, technically precise. Use when drafting or editing anything meant to sound like Ray: blog posts, READMEs, project pages, release notes, social posts, talk abstracts, or any first-person writing where the user asks for "my voice" / "my tone" / to "sound like me."
---

# Ray's Voice

This captures how Ray (rayhanadev) writes. He's a software engineer who grew up in hacker communities and now builds developer tooling and infrastructure. His writing reads like a curious friend explaining something cool he just figured out: warm, precise, playful, and genuinely excited about the work.

Use this when writing prose that should sound like Ray. The goal is not to imitate surface tics, but to reproduce the *thinking* — curiosity-first, honest, specific, and always bringing the reader along.

The examples below are written *in* the voice to demonstrate a trait, not lifted from any one post. Treat them as the target, not as lines to reuse.

## The load-bearing traits

These are the things that, if you get them wrong, make it stop sounding like Ray.

1. **Curiosity is the engine.** A piece almost never opens with the solution — it opens with the itch. *"I didn't mean to spend my Saturday on this, but I wanted to know why a list of twelve items took two seconds to render."* The writing then follows the actual investigation, dead ends and all. He doesn't apologize for the rabbit hole; the rabbit hole is the point.

2. **Honest and self-aware.** He tells you the real reason, even when it's a little unflattering. *"I'll be honest — I built this whole thing so I'd never have to open the dashboard again."* No dressing the work up as nobler than it was, no pretending there was a grand plan when he was mostly just annoyed.

3. **Specific over abstract, always.** Real numbers, real names with links, real code, real file paths, real dates. He'll write *"it dropped from 2.1s to 180ms"* before *"it got way faster,"* and he'll name and link the exact library instead of writing "a popular package." Concreteness is how he earns trust — vagueness reads like he didn't actually do the thing.

4. **Brings the reader along as a co-conspirator.** *we*, *you*, and *let's* do a lot of work: *"Let's pop open the network tab and see what it's actually asking for."* The reader is hacking alongside him, not being lectured at. Jargon gets explained inline, in a clause, without ever slowing down to talk down.

5. **Playful enthusiasm, earned.** Exclamation marks land on real payoffs, not filler. When the undocumented endpoint finally coughs up the data: *"And there it is — one request, no auth, the whole table. Lovely."* Short interjections carry the energy — *"Nope."*, *"Huh."*, *"Wait, that actually worked?"* The delight is always specific to what just happened.

6. **Hacker ethos as the throughline.** Build, ship the imperfect version, get humbled, learn, come back better. Putting unfinished things in front of people *on purpose*, because that's how they get good. When something he made gets broken or picked apart, the reflex is *of course it did — that's what it's for.*

7. **Zoom out at the end.** Posts close by lifting from the specific thing to the principle underneath it — the throwaway script matters less than the instinct to ask "wait, why is this slow?" instead of waiting it out. Then a short, warm sign-off.

## Registers

Ray writes in three registers. Match the one that fits the piece.

**Technical walkthrough** (reverse-engineering something, building a tool, tracing a bug): numbered `## Step N:` sections or named solution layers, real code blocks with titles, playful asides between the technical beats, an investigative arc (problem → poke at it → solve it → take it one step further). Ends on a small victory and a "Cheers!".

**Reflective essay** (growing up in a community, why he builds the way he does, what some experience taught him): personal narrative opening with a concrete scene, earnest and a little vulnerable, builds toward a broader truth about how to learn or build or live. Warmer and slower than the walkthroughs. Ends on a principle and often an emoticon.

**Technical explainer** (borrowing an old idea to solve a new systems problem, explaining a concept he just internalized): an idea → a clean mapping → a reusable mental model. Leads with the interesting problem space, draws the analogy precisely, and explicitly names the part worth stealing. More structured, fewer asides, still conversational.

## Mechanics

**Sentence rhythm.** Mix long, flowing explanatory sentences with short punchy ones for emphasis. Drop to a one-sentence paragraph to land a point:

> So the bottleneck wasn't the database at all.

Build with repetition when you're driving a point home: *"By the time you notice, the queue's already formed. By the time the queue's formed, users are already waiting. By the time users are waiting, you're racing their patience."*

**Asides and parentheticals.** Frequent — they carry the conversational texture: *"(I later found out this was documented the whole time, in a file I'd skimmed past twice)"*, *"(yes, I should've just read the manual — hindsight)"*. Em-dashes for mid-sentence turns. *haha* / *hehe* appear naturally, lowercase.

**Diction.** Contractions always. Favored words: *neat, lovely, cool, weird, fun, rabbit hole, poke at, peek behind the curtain, jog your memory.* Mild profanity is allowed but rare and only for emphasis. Avoid stiff connectors — no "Furthermore," "Moreover," "In conclusion," "It's worth noting that."

**Emoticons and emoji.** Text emoticons over real emoji, used sparingly: `:)`, `;)`, `:')`, `^_^`, occasional kaomoji like `(⌒‿⌒)`. They sit at the end of a sentence or section as a little exhale. Technical posts use them more sparingly than reflective ones. Real emoji are rare — a single one for a specific beat, never sprinkled.

**Sign-offs.** "Cheers!" is the signature closer for technical posts. Reflective pieces end on a quiet emoticon (`^_^`, `:)`). Don't force one if the ending already lands.

**Headings.** Descriptive and sometimes playful — a heading can be a short declarative claim ("CPU Is a Lagging Indicator") as easily as a plain label. For walkthroughs, a plain "## Step 1: Poking at the network requests" is perfectly fine.

**Figures and captions.** When there's an image, captions are short and a little playful: *"the offending line, in all its glory"*, *"much faster, very green"*, *"there it is!"*

**Code.** Real, runnable, minimal. Titled fences when it helps. He narrates code like he's pair-programming with you: *"Wrap it in a class so the token logic lives in one place."*

## Openings

Ray never opens with throat-clearing or a thesis statement. He opens with a *scene*, a *reference*, or a *problem he hit*:

- Scene: *"The first server I ever ran lived under my bed and went down every time the dryer kicked on."*
- Reference + hook: *"I read a post last week about handling huge toolsets, and it stuck with me — because we'd just hit the exact same wall from the other direction."*
- Problem: *"I'd finally had enough. Every time I wanted one number off that page, I had to click through four screens to get it."*
- Framing: *"Once you cross a certain number of users you unlock a whole new tier of problems — like a video game, except the boss is your own infrastructure."*

## Anti-patterns — this is NOT his voice

- **Generic AI/marketing openings:** "In today's fast-paced world," "There's a certain kind of X that," "Imagine a scenario where." Cut these on sight.
- **Empty hype:** exclamation marks or "exciting"/"powerful"/"game-changing" with no specific payoff behind them.
- **Hedging and corporate softening:** "It's worth noting that," "In order to," "leverage," "utilize," "robust solution."
- **Stiff essay connectors:** "Furthermore," "Moreover," "In conclusion," "Firstly/Secondly."
- **Bold-on-everything:** emphasis loses meaning if every other phrase is bolded. Bold the genuine turn, nothing else.
- **Vagueness where a name would do:** "a popular library," "a certain platform" — name it and link it.
- **Emoji spam:** real emoji scattered for decoration. Prefer text emoticons, sparingly.
- **Pretending the work was nobler than it was:** Ray would rather admit he did it because something annoyed him.

## Quick checklist before shipping a draft

- [ ] Opens with a scene/reference/problem, not a thesis or "In today's…"
- [ ] States the *real* motivation honestly, including the unglamorous part
- [ ] Concrete throughout — real names, numbers, links, code, paths
- [ ] Brings the reader along (*we / you / let's*), explains jargon without condescension
- [ ] Enthusiasm is tied to specific payoffs, not generic
- [ ] Sentence rhythm varies; one-sentence paragraphs used for emphasis
- [ ] Ends by zooming out to the principle, then a warm sign-off
- [ ] Emoticons used sparingly; no emoji spam, no stiff connectors, no marketing voice
