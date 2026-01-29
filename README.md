# daytrace 💭

tracing *why* days feel productive or unproductive by reasoning over passive signals using an explicit behavioral ontology.

focusing on abstracting raw personal data into higher-level explanations rather than just tracking it.

---

## why this exists

i kept asking the same questions about my days, and existing tools didn’t help.

not “how many hours did i work?”, but:

- why did today feel heavy?
- why do some busy days still feel empty?
- why do my days tend to fall apart after a certain point?

most productivity tools stop at tracking.

daytrace exists to push one layer deeper — from *events* to *explanations*.

---

## the problem

many productivity apps rely on self-reporting, scores, or charts that don’t explain much.

meanwhile, phones already emit a large amount of passive signal — time, location, routines, movement — but that data is rarely translated into meaning.

> what if you installed something once, and it explained your day back to you?

---

## the idea

daytrace is built around three layers:

1. collect **passive signals**
2. abstract those signals into **structured facts** using an ontology
3. reason over those facts to produce **explanations**

there is no self-reporting and no explicit productivity scoring.

the goal isn’t optimization — it’s understanding.

![system flow](docs/images/diagram-system-flow.png)

---

## what it observes

> strictly passive. zero user effort.
- passive signal collection
- basic inference engine
- ontology mapping layer


### raw signals

- **time** (durations, routines, gaps)
- **geolocation** (stays, transitions, environment changes)
- **health context** (movement and activity signals, when available)
- **motion / gyro** (to infer phone interaction vs ambient movement)

screen time apis are intentionally not used. they require special entitlements and app store deployment. this project explores what can be inferred *without* privileged access.

---

### inferred events

raw signals are converted into higher-level events such as:

- home / work / cafe sessions
- transitions between environments
- extended idle or low-movement blocks
- probable phone interaction windows

these events are intentionally fuzzy. they are inputs to reasoning, not ground truth.

---

### semantic facts (ontology layer)

instead of storing raw logs, the system stores semantic facts like:

- `late_start`
- `long_midday_break`
- `worked_from_home(morning)`
- `no_environment_change`

these facts form the basis for reasoning and explanation.

<p align="center">
  <img src="docs/images/diagram-abstraction-ladder.png"
       alt="abstraction ladder"
       width="220" />
</p>

---

## why ontologies (not ml-first)

ml is effective at pattern detection under sufficient supervision.

ontologies are better at:
- expressing meaning
- making reasoning explicit
- allowing llms to explain *using structure*

this project prioritizes understanding and debuggability first.

ml can come later.

---

## talking to your data

daytrace includes a chat layer where you can ask questions like:

> why did yesterday feel unproductive?

responses are framed as **hypotheses**, not judgments:

- started later than baseline
- long idle block mid-day
- minimal environment change
- pattern matches previous low-energy days

the goal is reflection, not scoring.

---

## architecture (high level)

```
expo app (ios)
  ↓
passive signal collectors
  ↓
event inference layer
  ↓
nestjs api
  ↓
ontology / knowledge graph (supabase)
  ↓
reasoning + llm explanation
  ↓
chat interface
```

this is optimized for understanding and debuggability.

clarity > scale.

---

## scope

* passive signal collection
* basic inference engine
* ontology mapping layer
* daily summaries
* why-style chat queries

---

## tech

* expo / react native (ios-first)
* typescript
* nestjs (backend api + domain boundaries)
* supabase (postgres, auth, storage)
* core location, motion, and health apis
* llm for explanation + summarization

screen time apis are deliberately avoided due to entitlement and deployment constraints.

this project explores what’s possible *without* that privileged access.

---

## what this project is (and isn’t)

this **is**:

* a systems design exercise
* an ontology + llm experiment
* a way to learn how personal data becomes insight

this **is not**:

* a shipped consumer product
* a motivation app
* a surveillance tool

---

## philosophy

> data shouldn’t shame you.

data should help you notice patterns you couldn’t see before.

---

## status

exploration project. intentionally rough.

---

## license

mit
