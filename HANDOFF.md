# NSENT Product / Engineering Handoff

## Product identity
**Name:** NSENT (Narrative, Situation, and Evidence Navigation Tool)
**Descriptor:** Causal Analysis Engine
**Line:** Explain the outcome. Expose the assumptions.

Brand direction: restrained analytical instrument, not "AI magic." Near-black surfaces, warm amber signal color, serif editorial headlines, monospace calculations. Avoid neon, chatbot imagery, circuit-board graphics, and generic AI gradients.

## User journey
1. User describes the situation and observable behavior.
2. User maps timing, incentives, constraints, capability, and benefit/cost distribution using plain-English prompts.
3. User enters concrete evidence separately from interpretation.
4. User supplies at least two competing explanations.
5. The live model visibly populates as fields are completed.
6. Analysis returns relative support, leading explanation, strongest dimensions, and transparent calculations.
7. Limitations remain visible beside the result.

## Architecture
The static version intentionally has three layers:

**Presentation — `index.html` + `styles.css`**
Accessible semantic form, brand system, responsive layout, results UI, methodology dialog.

**Application — `app.js`**
Dynamic evidence/hypothesis rows, validation, live model display, input collection, rendering. It knows nothing about scoring internals except `NsentEngine.analyze()`.

**Analysis — `engine.js`**
Pure deterministic scoring. Takes a structured object and returns ranked hypotheses plus dimension scores. No DOM dependency.

## Analysis input contract
```js
{
  situation: string,
  behavior: string,
  timing: string,
  incentives: string,
  constraints: string,
  capability: string,
  distribution: string,
  evidence: string[],
  hypotheses: string[]
}
```

## Production model adapter
Do not let an LLM simply output "the answer." Replace the lexical dimension scorer with a structured extractor returning, for each hypothesis:

```json
{
  "evidence_for": [],
  "evidence_against": [],
  "unsupported_assumptions": [],
  "missing_information": [],
  "dimensions": {
    "evidence": 0.0,
    "context": 0.0,
    "incentives": 0.0,
    "capability": 0.0,
    "constraints": 0.0,
    "timing": 0.0,
    "distribution": 0.0
  }
}
```

Validate all values server-side and perform normalization outside the model. Store the raw inputs, model version, scoring weights, structured output, and final calculation together for auditability.

## Next recommended features
- Evidence quality selector: direct record / first-hand / reputable secondary / hearsay / assumption.
- Evidence-for and evidence-against mapping per hypothesis.
- Required baseline/null hypothesis.
- Sensitivity analysis for scoring weights.
- Save/share analysis by immutable ID.
- Export a clean analysis report.
- Optional research mode that verifies user-entered evidence against sources.
- Contradiction detector and missing-evidence prompts.

## Deployment
This handoff is static and can deploy to Vercel, Netlify, GitHub Pages, Cloudflare Pages, or any ordinary web host. No secrets or environment variables are used in this edition.
