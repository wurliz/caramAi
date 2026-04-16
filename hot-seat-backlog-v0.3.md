# Hot Seat — Agile Backlog
**v0.3 · Beta Planning**
*2 devs · part-time · 1–2 scenarios · 1 room per scenario*

> **Beta scope note:** With 33 Must Haves across 10 epics, shipping everything at once isn't realistic for a 2-person part-time team. This revision splits delivery into two tiers — **Beta** (the minimum viable experience) and **Post-Beta** (polish and depth). The object interaction system has been descoped entirely for now. Priorities reflect what's needed to put a working, playable build in front of testers.

---

## Table of Contents

1. [Epic 1 — 3D Room & Navigation](#epic-1--3d-room--navigation)
2. [Epic 2 — Text & Voice Input](#epic-2--text--voice-input)
3. [Epic 3 — AI Character & Story](#epic-3--ai-character--story)
4. [Epic 4 — CCTV / Video Call Interface](#epic-4--cctv--video-call-interface)
5. [Epic 5 — Tension & Environmental Feedback](#epic-5--tension--environmental-feedback)
6. [Epic 6 — Clue System](#epic-6--clue-system)
7. [Epic 7 — De-escalation Progress & Outcomes](#epic-7--de-escalation-progress--outcomes)
8. [Epic 8 — Audio & Music](#epic-8--audio--music)
9. [Epic 9 — UI & Dossier](#epic-9--ui--dossier)
10. [Epic 10 — Tech Stack Integration & Performance](#epic-10--tech-stack-integration--performance)

---

## Epic 1 — 3D Room & Navigation

**Goal:** Give the player a believable, walkable room they can freely explore. Object interaction is descoped for beta — the room is a navigable environment, not an inspection puzzle.

> **Descoped for beta:** Object hover highlighting (US-102) and object inspection / clue discovery via objects (US-103) are moved to Won't Have for the beta build. The room should feel explorable and atmospheric, but interactable objects are not required to ship.

---

### US-101 — Basic room navigation

> **As a player,** I want to walk freely around the room using WASD and look around with the mouse, **so that** I feel present in the scene and can explore at my own pace.

**Acceptance criteria:**
- WASD movement is smooth with no camera clipping through walls or objects
- Mouse look covers full 360° horizontal and appropriate vertical range
- Collision detection prevents walking through furniture and walls
- Frame rate stays above 60fps on mid-range PC hardware

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-102 — Object hover highlighting

> **As a player,** I want interactable objects to visually highlight when I hover over them, **so that** I know what I can examine without needing a tutorial.

**Acceptance criteria:**
- Interactable objects show an outline or subtle glow on mouse hover
- Highlight is visible without being distracting in the neo-noir art style
- Non-interactable objects produce no response to hover
- Highlight activates within one frame of cursor entering object bounds

**Priority:** ~~Must have~~ **Won't have (Beta)** · **Estimate:** 2 pts

---

### US-103 — Object inspection

> **As a player,** I want to click on a highlighted object and see a close-up view or descriptive detail, **so that** I can understand the clue it contains.

**Acceptance criteria:**
- Clicking an object triggers an inspect animation or modal view
- Each interactable object has a unique description or visual detail
- Player can dismiss the inspect view and return to room navigation
- Inspecting an object logs the clue to the dossier automatically

**Priority:** ~~Must have~~ **Won't have (Beta)** · **Estimate:** 3 pts

---

### US-104 — Room art pass (neo-noir)

> **As a player,** I want the room to feel like a panel from a Frank Miller comic — high contrast, cel-shaded, with neon accents and urban decay — **so that** the setting immediately establishes tone without exposition.

**Acceptance criteria:**
- Cel-shaded shader applied to all room geometry with ink outline
- Palette uses neon cyan, magenta, and amber against near-black surfaces
- Environmental details present: peeling wallpaper, flickering fluorescent, rain-streaked glass
- Art direction signed off by both developers before scene is locked

**Priority:** Must have (Beta) · **Estimate:** 8 pts

---

### US-105 — Ambient nudge system

> **As a player,** I want a subtle environmental cue to draw my attention if I haven't examined anything for 90 seconds, **so that** I don't get stuck without the game breaking immersion with an obvious hint.

**Acceptance criteria:**
- After 90 seconds of inactivity (no object examined, no voice input), an object glints or the phone crackles with a subtle audio cue
- Nudge targets the most investigation-relevant uncollected clue
- Nudge occurs no more than once every 90 seconds
- A separate opt-in hint system is available in settings for players who want explicit guidance

**Priority:** Should have (Post-Beta) · **Estimate:** 3 pts

---

### US-106 — In-game clock on the wall

> **As a player,** I want to see a visible clock on the wall ticking in real time, **so that** I feel soft time pressure without a punishing hard countdown.

**Acceptance criteria:**
- Clock is a diegetic prop visible from the default starting position
- Clock advances in real time throughout the session
- No hard game-over tied to clock; it feeds into the stalemate outcome condition
- Clock styling matches the room's neo-noir aesthetic

**Priority:** Should have (Post-Beta) · **Estimate:** 2 pts

---

## Epic 2 — Text & Voice Input

**Goal:** Let the player negotiate using their voice or keyboard, with real-time transcription feeding into the AI conversation loop. Both input modes are required for beta.

---

### US-201 — Microphone access & transcription

> **As a player,** I want to speak into my microphone and have my words transcribed in real time, **so that** I can negotiate naturally without typing.

**Acceptance criteria:**
- Game requests microphone permission on first launch with clear explanation
- Transcription begins automatically when player starts speaking
- Transcription latency is under 1.5 seconds for a typical sentence
- Transcribed text is displayed in the phone/radio UI before being sent to the AI

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-202 — Push-to-talk mode

> **As a player,** I want the option to hold a key to activate my microphone rather than having it always open, **so that** background noise doesn't disrupt the conversation.

**Acceptance criteria:**
- Default key binding is spacebar; rebindable in settings
- Visual indicator shows when microphone is active
- Push-to-talk and always-on modes selectable in settings
- Switching modes takes effect without restarting the session

**Priority:** Must have (Beta) · **Estimate:** 2 pts

---

### US-203 — Text input fallback

> **As a player,** I want to type my dialogue if I don't have a microphone or prefer not to speak, **so that** the game is accessible regardless of hardware.

**Acceptance criteria:**
- Text input field is available at all times via a toggle in the phone UI
- Text submissions go through the same AI pipeline as voice
- Switching between voice and text is seamless mid-session
- Accessibility note documented in settings

**Priority:** Must have (Beta) · **Estimate:** 2 pts

---

### US-204 — STT provider integration

> **As a developer,** I want the STT module to be provider-agnostic behind an interface, **so that** we can swap between browser-native Web Speech API and server-side options without refactoring the game.

**Acceptance criteria:**
- STT is abstracted behind a `TranscriptionService` interface
- Two implementations wired up: browser Web Speech API (free, higher latency) and server-side option (e.g., Whisper via API)
- Provider selected via config flag, not code change
- Fallback to browser API if server-side fails

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-205 — Silence and pause handling

> **As a player,** I want natural pauses in my speech to not trigger a premature send, **so that** the AI receives complete thoughts rather than fragments.

**Acceptance criteria:**
- Transcription does not send until 1.5 seconds of silence detected after speech
- Minimum speech duration of 1 second before a send is triggered
- Long pauses (5+ seconds) mid-sentence display an indicator asking if player is finished
- Edge case: very short utterances ("yes", "okay") send correctly

**Priority:** Should have (Post-Beta) · **Estimate:** 3 pts

---

## Epic 3 — AI Character & Story

**Goal:** Create a believable, emotionally responsive AI character with a fully developed backstory and motive. The character's story is the emotional spine of the experience — it must be authored before any other AI work begins.

> **Story-first approach:** Character storyboarding and the persona system prompt are now the top-priority items in this epic. All other AI behaviour depends on a locked character story. Complete US-300 and US-301 before any integration work.

---

### US-300 — Character storyboarding *(new)*

> **As a developer,** I want a complete written storyboard of the hostage taker's character arc — backstory, motive, key emotional beats, and how their state changes over a session — **so that** every subsequent AI prompt and animation decision is grounded in a consistent, authored story.

**Acceptance criteria:**
- One-page character bible completed: who they are, why they're here, what they want, what they fear
- Emotional arc mapped across three tension tiers (low, mid, high) with example dialogue for each
- At least three key "story moments" identified (e.g., the detail that breaks them, the bluff they run)
- Storyboard signed off by both developers before any AI prompt or animation work begins
- Document version-controlled alongside the codebase

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-301 — Character persona system prompt

> **As a developer,** I want a well-structured system prompt that defines the hostage taker's backstory, motive, emotional state, and speech patterns, **so that** the AI behaves consistently in character across an entire session.

**Acceptance criteria:**
- System prompt includes: fixed backstory, core motive, emotional baseline, speech quirks, explicit behavioural instructions for each tension tier
- Prompt is version-controlled and treated as a design asset
- Any developer can update the prompt without touching game code
- Character passes a 30-minute live session "break character" stress test

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-302 — Dynamic context injection

> **As a developer,** I want the current tension level, discovered clues, and conversation history injected into each AI request, **so that** the character's responses reflect what has actually happened in the session.

**Acceptance criteria:**
- Context block prepended to each message includes: tension tier (low/mid/high), list of clue IDs found, last N turns of conversation
- Context is updated correctly after each player turn
- Token budget managed; oldest conversation turns pruned first when limit approached
- AI demonstrably references earlier conversation content in subsequent responses

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-303 — Evidence-aware reactions

> **As a player,** I want the hostage taker to react with surprise or changed strategy when I demonstrate knowledge I could only have from physical evidence, **so that** investigation feels rewarding rather than decorative.

**Acceptance criteria:**
- When player mentions a detail tied to a clue they have found, AI responds as if caught off-guard or threatened
- When player mentions the same detail without having found the evidence, AI responds at face value (not shut out, just without leverage feedback)
- Behaviour tested against at least 3 evidence-topic pairs per scenario
- No false positives: AI does not react to general mentions of topics that happen to share keywords with clue content

**Priority:** Should have (Post-Beta) · **Estimate:** 5 pts

---

### US-304 — Tension tier behaviour

> **As a player,** I want the hostage taker's tone and volatility to shift visibly as tension rises and falls, **so that** I can read the emotional temperature of the situation from the conversation itself.

**Acceptance criteria:**
- Low tension: character is calm, guarded, occasionally cooperative
- Mid tension: defensive, shorter responses, occasional threats
- High tension: irrational, erratic, threatening, stops volunteering information
- Transitions between tiers produce a noticeable but not jarring shift in tone

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-305 — AI model evaluation spike

> **As a developer,** I want to run a structured comparison of Inworld, DeepSeek, Kimi k2, GLM, and Qwen against the same scenario and system prompt, **so that** we select the best model on believability, latency, and cost before committing to an integration.

**Acceptance criteria:**
- Same scenario, same system prompt, same 10 test inputs used for all candidates
- Evaluation scorecard: in-character rate, response latency (p50/p95), estimated cost per 30-min session, subjective believability rating
- Results documented in a shared decision log
- Model selected and recorded with rationale before Sprint 3 begins

**Priority:** Must have (Beta) · **Estimate:** 3 pts (spike)

---

### US-306 — Emotional breadcrumb drops

> **As a player,** I want the hostage taker to occasionally reference names, places, or grievances unprompted, **so that** the conversation naturally points me toward relevant evidence without an explicit hint system.

**Acceptance criteria:**
- System prompt instructs AI to drop 1–2 breadcrumb references per 5-minute window
- Breadcrumbs correspond to actual evidence locations in the room
- Breadcrumbs are emotionally plausible — they arise from the character's state, not as exposition
- Frequency can be tuned via prompt parameter without code changes

**Priority:** Should have (Post-Beta) · **Estimate:** 2 pts

---

### US-307 — Break-character fallback

> **As a player,** I want the game to gracefully handle AI responses that break character or are nonsensical, **so that** one bad API response doesn't ruin the session.

**Acceptance criteria:**
- Output filter detects obvious off-character responses (length < 3 words, contains meta-references to "AI", etc.)
- Fallback: a pre-written in-character canned response matched to current tension tier is substituted
- Fallback rate logged for monitoring
- Player sees no error state; session continues uninterrupted

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

## Epic 4 — CCTV / Video Call Interface

**Goal:** Make the hostage taker visible on a diegetic in-world screen so the player is negotiating with someone they can see, not a voice in a void.

---

### US-401 — In-world screen prop

> **As a player,** I want to see a CCTV monitor or video call screen as a physical object in the room, **so that** the interface feels grounded in the world rather than overlaid as a HUD.

**Acceptance criteria:**
- Screen is a 3D prop placed logically within the room (desk, wall bracket)
- Screen renders the character feed as a texture in 3D space
- Player can approach and step back from the screen naturally
- Screen is visible from the default player start position

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-402 — Character animation states

> **As a player,** I want the hostage taker on screen to display different postures and animation states based on tension level, **so that** body language reinforces what I hear in their voice.

**Acceptance criteria:**
- Minimum 3 animation states: calm/composed, agitated/pacing, volatile/erratic
- States transition smoothly when tension tier changes
- Idle animation within each state prevents a "frozen mannequin" appearance
- Animation rig supports at least upper body expressiveness (hands, posture, head)

**Priority:** Must have (Beta) · **Estimate:** 8 pts

---

### US-403 — Thinking / processing indicator

> **As a player,** I want to see the character doing something believable on screen during the AI inference + TTS latency gap, **so that** the wait feels diegetic rather than like a loading screen.

**Acceptance criteria:**
- "Thinking" animation plays from the moment player finishes speaking until AI audio begins
- Animation is contextually appropriate: looking away, exhaling, pacing — not a generic spinner
- Animation length adapts to latency; no abrupt cut-off when response arrives
- Threshold: if response arrives in under 500ms, thinking animation is skipped

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-404 — ElevenLabs voice integration

> **As a player,** I want to hear the hostage taker speak in a distinct, emotionally expressive voice, **so that** the audio reinforces the character's psychological state.

**Acceptance criteria:**
- ElevenLabs API integrated for character voice output
- Voice parameters (stability, similarity boost) tuned per tension tier
- Audio streams as AI text generates — no waiting for full response before audio begins
- Fallback: if ElevenLabs call fails, text appears on screen silently rather than session breaking

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

## Epic 5 — Tension & Environmental Feedback

**Goal:** Communicate tension state entirely through environmental cues once the explicit meter is removed post-beta. Beta ships with a visible meter for calibration.

---

### US-501 — Tension meter (beta, debug/calibration)

> **As a developer,** I want a visible numeric or bar tension meter during beta, **so that** we can calibrate environmental feedback signals before removing the explicit meter.

**Acceptance criteria:**
- Tension displayed as a 0–100 numeric value and bar in a debug overlay
- Overlay is togglable via a developer hotkey; not visible in release builds
- Meter updates in real time after each AI exchange
- Values logged to a session file for post-session analysis

**Priority:** Must have (Beta only) · **Estimate:** 2 pts

---

### US-502 — Lighting shifts with tension

> **As a player,** I want the room lighting to gradually redden and darken as tension rises, **so that** I can feel the situation deteriorating without being told.

**Acceptance criteria:**
- Lighting colour temperature shifts from neutral white toward red at high tension
- Transition is gradual — no instant snap between states
- Change is perceptible within 2 tension tier changes but not alarming at small increments
- Lighting recovers correctly if tension decreases

**Priority:** Should have (Post-Beta) · **Estimate:** 3 pts

---

### US-503 — Audio degradation with tension

> **As a player,** I want ambient audio — static, rain, crowd noise — to intensify and distort as tension rises, **so that** the soundscape mirrors the psychological pressure.

**Acceptance criteria:**
- Rain intensity increases at mid and high tension
- Radio/phone static increases at high tension
- Distant crowd murmur becomes more audible/agitated at high tension
- Audio returns to baseline if tension drops

**Priority:** Should have (Post-Beta) · **Estimate:** 3 pts

---

### US-504 — Tension meter removal (post-beta milestone)

> **As a player,** I want to read tension purely from environmental cues and character behaviour once the game is confident the feedback is clear, **so that** the experience feels immersive rather than gamified.

**Acceptance criteria:**
- Playtesting confirms 80%+ of test players correctly identify tension tier from environment alone
- Debug meter removed from all builds
- At least one additional environmental signal added (e.g., character sweat, mirror cracks, phone quality degrades) before this milestone is signed off

**Priority:** Won't have (Beta) · **Estimate:** 5 pts

---

## Epic 6 — Clue System

**Goal:** Make evidence discovery feel organic and rewarding — enriching the conversation rather than gatekeeping it.

> **Beta note:** With object inspection descoped, clue discovery via physical objects (US-602) is also deferred. The clue data model and AI context injection remain, as they underpin character reactions that are core to the beta experience. Clues can be pre-loaded into context for beta testing purposes.

---

### US-601 — Clue data model

> **As a developer,** I want a data model for clues that stores the clue ID, description, associated topic tags, and context string injected into the AI, **so that** clues are manageable assets rather than hardcoded strings.

**Acceptance criteria:**
- Clue defined as: `{ id, label, shortDescription, contextString, topicTags[] }`
- Clues loaded from a JSON or similar config file, not hardcoded
- Adding a new clue requires only a config change, no code change
- At least 8 clues designed for scenario 1 before alpha

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-602 — Clue discovery → dossier

> **As a player,** I want discovered clues to appear in my dossier automatically when I examine the relevant object, **so that** I can review what I know at any time.

**Acceptance criteria:**
- Dossier updates immediately on object inspection
- Each clue entry shows label and short description
- Dossier is accessible at any time without pausing the session
- New clue entry triggers a subtle UI notification

**Priority:** ~~Must have~~ **Won't have (Beta)** — depends on object inspection (US-103) · **Estimate:** 3 pts

---

### US-603 — Clue context injected into AI

> **As a developer,** I want each discovered clue's context string to be appended to the AI's dynamic context block, **so that** the AI knows what the player has found and can react accordingly.

**Acceptance criteria:**
- Context block lists all discovered clue IDs and their context strings
- Context updates before the next AI request, not retroactively
- AI demonstrably changes response when a relevant clue has just been added to context (tested per clue)
- Context string length budgeted to avoid token overflow (max 50 tokens per clue)

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-604 — Organic topic unlocking (no hard gates)

> **As a player,** I want to be able to raise any topic in conversation at any time, **so that** I never feel artificially blocked from saying something I've figured out.

**Acceptance criteria:**
- No code-level topic gate exists: the AI receives all player input regardless of clues found
- Player who raises a clue-linked topic without the evidence gets a plausible but low-leverage response
- Player who has the evidence and raises the same topic gets a noticeably different, higher-stakes response
- Difference between the two scenarios is subjectively clear in playtest

**Priority:** Must have (Beta) · **Estimate:** 2 pts

---

### US-605 — Leverage signal design

> **As a player,** I want to feel the difference between raising a topic with and without evidence behind it, **so that** investigation is meaningfully rewarded without making it mandatory.

**Acceptance criteria:**
- AI prompt instructs character to react with surprise/fear/recalibration when player demonstrates specific knowledge
- Three leverage moments scripted and tested for scenario 1
- Leverage reaction does not require exact keyword match — semantic match is sufficient (tested with at least 3 paraphrase variations)

**Priority:** Should have (Post-Beta) · **Estimate:** 3 pts

---

## Epic 7 — De-escalation Progress & Outcomes

**Goal:** Deliver multiple ending states driven by accumulated tension, conversation quality, and evidence gathered.

---

### US-701 — Progress tracking model

> **As a developer,** I want a backend model that tracks both conversation quality score and evidence score equally, **so that** the outcome reflects both strands of play.

**Acceptance criteria:**
- Two score axes: `conversationScore` (0–100) and `evidenceScore` (0–100)
- Final de-escalation score = average of both, with no weighting toward either
- Conversation score updated heuristically per AI exchange (tone markers, tension delta)
- Evidence score updated per clue discovered (total clues found / total clues available)

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-702 — De-escalation (win) outcome

> **As a player,** I want a satisfying win state when I've successfully de-escalated the situation, **so that** my effort feels meaningfully concluded.

**Acceptance criteria:**
- Win triggers when tension falls below defined threshold and combined progress score exceeds win threshold
- Win sequence: character stands down, narrative epilogue plays, post-session summary shown
- Summary shows which moments contributed most to success
- Outcome is saveable/shareable (screenshot of summary card minimum)

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-703 — Escalation (lose) outcome

> **As a player,** I want a meaningful lose state when I've pushed the hostage taker past the point of return, **so that** failure feels instructive rather than arbitrary.

**Acceptance criteria:**
- Lose triggers when tension maxes out and character becomes unreachable
- Brief post-mortem shows 3–5 moments where the situation tipped
- Post-mortem is non-punishing in tone — inquisitive, not scolding
- Player offered to restart or quit from post-mortem screen

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-704 — Stalemate (partial) outcome

> **As a player,** I want a morally ambiguous partial outcome if time runs out with the situation unresolved, **so that** not every session has a clean win/lose binary.

**Acceptance criteria:**
- Stalemate triggers when in-game clock expires with tension in mid-range
- Narrative epilogue is distinct from win and lose — SWAT called in, ambiguous result
- Player is made to sit with the outcome briefly before UI appears
- Outcome may be cut if playtesting reveals it adds confusion rather than weight — documented as under review

**Priority:** Could have (Post-Beta) · **Estimate:** 5 pts

---

### US-705 — Replayability framing

> **As a player,** I want to be encouraged to replay a scenario using a different conversational approach, **so that** the generative nature of the AI is a feature I'm aware of.

**Acceptance criteria:**
- Post-session summary mentions that the AI's responses are generative and different approaches yield different conversations
- "Try a different angle" prompt shown on lose and stalemate screens
- Session statistics (tension curve, clues found, key moments) shown to give replay context

**Priority:** Should have (Post-Beta) · **Estimate:** 2 pts

---

## Epic 8 — Audio & Music

**Goal:** Build a reactive soundscape that amplifies emotional tension without overshadowing the voice conversation.

---

### US-801 — Ambient sound layer

> **As a player,** I want a persistent ambient soundscape — rain, distant sirens, muffled crowd — **so that** the room feels alive and located in a real urban setting.

**Acceptance criteria:**
- Ambient audio loops seamlessly with no perceptible seam
- Three layers: rain (constant), sirens (occasional), crowd (low-level constant)
- All layers mix without muddying the character voice or player voice transcription
- Ambient level adjustable in settings independently of voice

**Priority:** Must have (Beta) · **Estimate:** 2 pts

---

### US-802 — Adaptive tension score

> **As a player,** I want the background music to react to the conversation's tension state, **so that** the score reinforces what's happening emotionally without telegraphing it too bluntly.

**Acceptance criteria:**
- Score uses minimalist jazz-influenced instrumentation (solo piano, brushed drums, bass)
- Score has three states mapped to tension tiers: sparse/slow, building, unresolved/dissonant
- Transitions between states use musical bridging (e.g., held note, slow tempo shift) — no abrupt cuts
- Score does not overpower conversation; ducking applied when character is speaking

**Priority:** Should have (Post-Beta) · **Estimate:** 5 pts

---

### US-803 — Phone/radio audio processing

> **As a player,** I want the hostage taker's voice to sound like it's coming through a low-quality phone or radio, **so that** the diegetic context of the call is reinforced sonically.

**Acceptance criteria:**
- ElevenLabs output processed with band-pass filter (300Hz–3.4kHz) and light noise/crackle
- Processing intensity increases at high tension (more crackle, more dropouts)
- Processing togglable in accessibility settings for players who find it hard to understand
- No processing on player's own transcription display — only on AI output

**Priority:** Should have (Post-Beta) · **Estimate:** 2 pts

---

## Epic 9 — UI & Dossier

**Goal:** Keep all UI elements diegetic and grounded in the room. The phone, the dossier, and the clock are props — not HUD overlays.

---

### US-901 — Dossier prop

> **As a player,** I want a physical dossier folder on the desk that I can open to review my clues, **so that** information management feels in-world rather than menu-driven.

**Acceptance criteria:**
- Dossier is a 3D prop on the desk, clickable to open
- Opened dossier renders as a 2D UI overlay styled as physical document pages
- Clues listed with label, short description, and visual thumbnail where relevant
- Dossier can be closed at any time; no modal lock

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-902 — Phone / radio prop UI

> **As a player,** I want the phone or radio to be a physical object in the room that I interact with to speak, **so that** voice input feels anchored to an in-world action.

**Acceptance criteria:**
- Phone/radio is a 3D prop; interacting with it activates the voice input pipeline
- Active call state indicated by a visual on the prop (light, indicator, waveform display)
- Transcribed text appears on a small attached screen or nearby notepad prop
- Hanging up (ending the call) is a deliberate action, not accidental

**Priority:** Must have (Beta) · **Estimate:** 5 pts

---

### US-903 — Session summary screen

> **As a player,** I want a clean post-session summary screen after each outcome, **so that** I can reflect on what happened and decide whether to replay.

**Acceptance criteria:**
- Summary shows: outcome label, tension curve graph, clues found count, 3–5 key conversation moments
- Design is consistent with the room's neo-noir aesthetic
- Restart and Quit options clearly presented
- Summary is self-contained — no additional loading required to display it

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-904 — Settings screen

> **As a player,** I want a settings screen accessible from the main menu and pause menu, **so that** I can configure audio, input mode, and accessibility options before or during a session.

**Acceptance criteria:**
- Settings includes: master volume, ambient volume, voice volume, STT mode (voice/text), push-to-talk toggle, phone processing toggle, hint system toggle
- Settings persist between sessions
- Pause menu accessible via Escape; does not mute or pause the AI session (ambiguity intentional for tension)
- Settings screen follows neo-noir aesthetic without being unreadable

**Priority:** Should have (Post-Beta) · **Estimate:** 3 pts

---

## Epic 10 — Tech Stack Integration & Performance

**Goal:** Integrate all third-party services reliably, manage API costs, and ensure the full voice pipeline feels fast enough to sustain immersion.

---

### US-1001 — End-to-end voice pipeline integration

> **As a developer,** I want STT → AI → TTS to work as a single integrated pipeline with predictable latency, **so that** the conversation loop feels fast enough to sustain immersion.

**Acceptance criteria:**
- Full pipeline (speech end → AI response audio start) completes in under 3 seconds for p50 requests
- Pipeline tested under simulated poor network conditions (400ms added latency)
- Each stage (STT, AI, TTS) has an independent timeout with fallback behaviour
- End-to-end latency logged per exchange for ongoing monitoring

**Priority:** Must have (Beta) · **Estimate:** 8 pts

---

### US-1002 — Token budget management

> **As a developer,** I want the AI context block to stay within the selected model's token budget at all times, **so that** long sessions don't cause API errors or unexpected cost spikes.

**Acceptance criteria:**
- Token counter estimates context size before each request
- When budget is within 20% of limit, oldest conversation turns are pruned (not clue context or system prompt)
- If pruning is insufficient, session gracefully degrades with a canned "losing signal" in-character message
- Token usage logged per session; alert if session exceeds cost threshold

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

### US-1003 — API cost monitoring

> **As a developer,** I want per-session cost estimates tracked and logged, **so that** we can evaluate model options accurately and avoid unexpected bills during development.

**Acceptance criteria:**
- Cost estimated per session based on token in/out and TTS character count
- Logs written to a local file with timestamp, model used, token counts, estimated cost
- Weekly cost summary view available (simple script or dashboard)
- Session token cap configurable; session ends gracefully if cap is hit

**Priority:** Must have (Beta) · **Estimate:** 2 pts

---

### US-1004 — Inworld SDK integration spike

> **As a developer,** I want to run a spike integrating Inworld's game SDK with our conversation pipeline, **so that** we understand the integration cost before committing to it over a raw LLM.

**Acceptance criteria:**
- Spike delivers a working prototype: player voice input → Inworld character → ElevenLabs audio out
- Documented findings: integration effort, emotional state API usefulness, latency profile, cost at expected usage
- Go/no-go recommendation recorded in decision log before Sprint 4

**Priority:** Must have (Beta) · **Estimate:** 5 pts (spike)

---

### US-1005 — Scenario configuration system

> **As a developer,** I want scenarios defined as data files (character persona, room layout, clue set, outcome thresholds), **so that** adding a second scenario requires no code changes.

**Acceptance criteria:**
- Scenario defined in a single config file: character persona strings, clue definitions, tension thresholds, outcome conditions
- Scenario selectable from a main menu scene picker
- Scenario 1 fully defined and loadable before alpha
- Scenario 2 stub exists and loads without error (content TBD)

**Priority:** Should have (Post-Beta) · **Estimate:** 5 pts

---

### US-1006 — Performance baseline

> **As a developer,** I want the game to maintain 60fps on a mid-range PC (GTX 1070 equivalent) with all core features running, **so that** voice input and AI response latency aren't compounded by render stutters.

**Acceptance criteria:**
- Frame rate profiled at 60fps floor on target hardware spec
- No frame-time spikes above 33ms during AI response receipt or TTS audio start
- Asset optimisation pass completed before beta milestone
- Memory usage stays below 4GB during a full 45-minute session

**Priority:** Must have (Beta) · **Estimate:** 3 pts

---

## Backlog Summary

| Epic | Stories | Must Have (Beta) | Should Have (Post-Beta) | Could Have | Won't Have (Beta) |
|------|---------|-----------------|------------------------|------------|-------------------|
| E1 — Room & Navigation | 6 | 2 | 2 | 0 | 2 |
| E2 — Text & Voice Input | 5 | 4 | 1 | 0 | 0 |
| E3 — AI Character & Story | 8 | 6 | 2 | 0 | 0 |
| E4 — CCTV Interface | 4 | 4 | 0 | 0 | 0 |
| E5 — Tension & Feedback | 4 | 1 | 2 | 0 | 1 |
| E6 — Clue System | 5 | 3 | 1 | 0 | 1 |
| E7 — Outcomes | 5 | 3 | 1 | 1 | 0 |
| E8 — Audio & Music | 3 | 1 | 2 | 0 | 0 |
| E9 — UI & Dossier | 4 | 3 | 1 | 0 | 0 |
| E10 — Tech & Performance | 6 | 5 | 1 | 0 | 0 |
| **Total** | **50** | **32** | **13** | **1** | **4** |

> **Beta point total (Must Haves only):** ~32 stories. Recommend a sprint planning session to sequence these into 2-week sprints, treating the AI model spike (US-305) and character storyboard (US-300) as Sprint 1 foundations that unblock everything else.

---

## Beta → Post-Beta Upgrade Path

Stories deferred to Post-Beta can be reintroduced once the beta build is stable and playtested. Suggested sequencing:

1. **First post-beta sprint:** Object hover highlighting (US-102) + Object inspection (US-103) + Clue discovery → dossier (US-602) — these three form the complete object interaction loop and should be tackled together.
2. **Second post-beta sprint:** Environmental feedback polish — lighting shifts (US-502), audio degradation (US-503), phone audio processing (US-803), adaptive score (US-802).
3. **Third post-beta sprint:** Character depth — evidence-aware reactions (US-303), breadcrumb drops (US-306), leverage signal design (US-605), replayability framing (US-705).
4. **Final post-beta sprint:** Tension meter removal (US-504), scenario config system (US-1005), stalemate outcome (US-704), settings screen (US-904).

---

## Open Questions

- **Stalemate feasibility** — Deferred to Post-Beta. Revisit once win/lose are stable and playtested.
- **STT provider** — Browser Web Speech API is free and requires no server infrastructure but has variable accuracy and no offline support. Evaluate against Whisper API early in Sprint 1.
- **Inworld vs raw LLM** — Spike (US-1004) should be the first technical deliverable in Sprint 1 given its decision impact.
- **Character animation rig** — Does the team have 3D art bandwidth for a custom animated character, or should we use a licensed base rig? This affects US-402 significantly.
- **Object system reintroduction** — Confirm when in post-beta roadmap to reintroduce US-102, US-103, and US-602 as a bundle.
- **Scenario 2 content** — Deprioritised for beta; config system (US-1005) ensures it can be added without code debt.

---

*Document version: 0.3 · Last updated: April 2026*
