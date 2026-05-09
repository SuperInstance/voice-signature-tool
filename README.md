# Voice Signature Analyzer 🔮

A zero-dependency, single-file web tool that analyzes any text against 10 anchor points to produce a model voice signature — and recommends which AI model matches that voice.

## How to Use

1. **Open `index.html`** in any modern browser. No server needed. No install. No API keys.
2. **Paste or type text** into the textarea — any article, AI output, prompt, or writing sample.
3. **Click "Analyze Signature"** (or Ctrl+Enter).
4. Get:
   - **10-character voice signature** — the hero element, prominently displayed
   - **Per-dimension breakdown** — each anchor point scored with confidence
   - **Model matches** — ranked by Hamming distance against the 14 stored signatures
   - **Recommendations** — best-matching model with temperature, prompt prefix, and known warnings

## How It Works

### 10 Anchor Points

| # | Dimension | What It Measures | Possible Values |
|---|-----------|-----------------|-----------------|
| 1 | Opening Strategy | How the text opens | sensorium(S), abstraction(A), grounded(G), paradox(P), theorem(T) |
| 2 | Reader Relationship | How the text positions the reader | direct(D), impersonal(I), collaborative(C), instructive(N), confrontational(F) |
| 3 | Negative Space Use | How the text uses negation | baseline(B), texture(T), insight(I), absent(A) |
| 4 | Time Relationship | How the text relates to time | linear(L), cyclic(C), athermal(A), circular(R), seasonal(S) |
| 5 | Math Role | How mathematics appears | absent(A), poetic(P), embedded(E), structural(S), theorem(T) |
| 6 | Paragraph Length | Dominant paragraph size | short(S), medium(M), long(L), mixed(X) |
| 7 | Sentence Fragments | Frequency of fragments | none(N), rare(R), moderate(M), frequent(F) |
| 8 | Metaphor Density | Density of figurative language | literal(L), occasional(O), woven(W), dense(D) |
| 9 | Parenthetical Frequency | How often parentheticals appear | none(N), rare(R), moderate(M), frequent(F), structural(S) |
| 10 | Closing Strategy | How the text closes | summary(S), return(R), provocation(P), image(I), open(O) |

The signature is a 10-character string like `G-D-I-S-S-X-N-O-M-S` — one code per dimension, in order.

### Scoring

Each dimension has a JavaScript scoring function (ported from the Python `anchor_analyzer.py` in the [Casting-Call](https://github.com/SuperInstance/casting-call) repository). Functions look at:

- Word frequency patterns (negation words, metaphor markers)
- Structural patterns (paragraph length, fragment detection)
- Opening/closing analysis (echo detection for circular time, return closings)
- Domain-specific vocabulary (math terms, nautical language, philosophical markers)

### Matching

Hamming distance is computed between the input signature and 14 stored signatures from the casting-call database. Closest matches are shown with distance scores (0 = perfect match, 10 = completely opposite).

### Database

The 14 embedded signatures span 6 model families:
- **DeepSeek v4-flash** (Oracle1)
- **DeepSeek v4-pro**
- **GLM-5.1**
- **Seed-2.0-mini**
- **Kimi K2.5**
- **Hermes-405B**

Recommendations include temperature settings and prompt prefixes from the casting-call's accumulated evaluations.

## Technical Details

- **Zero dependencies** — no frameworks, no CDN, no build step
- **100% client-side** — all analysis runs in your browser
- **~400 lines** of HTML/CSS/JS
- **Dark theme** matching superinstance.ai aesthetic
- **Mobile responsive** — works on phones and tablets
- **No data leaves your machine** — privacy-first design

## Files

- `index.html` — the complete tool (open in browser and use)
- `README.md` — this file

## Deploy

This tool is designed for GitHub Pages. Push `index.html` to any GitHub Pages-enabled repo and it works immediately.

```bash
git clone git@github.com:SuperInstance/voice-signature-tool.git
cd voice-signature-tool
# Just push index.html to your GitHub Pages branch
```

No build, no config, no server.

## Related

- [Casting-Call](https://github.com/SuperInstance/casting-call) — the original Python anchor analyzer and signature database
- [Casting-Call GPU](https://github.com/SuperInstance/casting-call-gpu) — GPU-accelerated signature matching
- [Model Voice Signatures paper](https://arxiv.org/abs/...) — the academic paper behind the framework

## License

MIT
## Data Source
Voice signatures and model templates sourced from [SuperInstance/casting-call](https://github.com/SuperInstance/casting-call) — the fleet's federated model evaluation database.
