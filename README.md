# NSENT — Narrative, Situation, and Evidence Navigation Tool

An MIT-licensed static prototype for turning plain-language situation inputs into a transparent, structured comparison of competing explanations.

NSENT uses deterministic lexical matching to rank explanations supplied by the user. Its normalized support scores are not real-world probabilities and do not establish causation, intent, or wrongdoing. See [METHODOLOGY.md](METHODOLOGY.md) for the scoring model and limitations.

## Run
No build step is required. Open `index.html` directly or serve this directory with any static server.

```bash
python -m http.server 8080
```

Then open <http://localhost:8080>. No package installation, build step, account, API key, or backend is required.

## Privacy

This edition processes form entries locally in your browser. It includes no analytics, external requests, or saved analysis storage. Reloading the page does not restore a saved analysis.

## Structure
- `index.html` — semantic application shell
- `assets/styles.css` — complete responsive design/brand system
- `assets/app.js` — form state, dynamic fields, live formula, rendering
- `assets/engine.js` — isolated deterministic analysis engine
- `METHODOLOGY.md` — formula, interpretation, limitations
- `HANDOFF.md` — product and engineering handoff

The engine is deliberately isolated from the UI. A future LLM/NLP extraction adapter can replace `engine.js` without redesigning the application.

## Contributing

Issues and pull requests are welcome. Keep changes focused and explain how you verified them. Preserve the distinction between lexical support scores and real-world probabilities.

## License

Copyright (c) 2026 Clear Frameworks. Released under the [MIT License](LICENSE).
