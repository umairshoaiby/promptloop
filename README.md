# PromptLoop 🔁

**An agentic loop that rewrites any prompt for any AI model — and learns from your feedback.**

One HTML file. No install, no server, no build. Download it, double-click it, paste a prompt, and watch four AI stages — **Analyze → Rewrite → Critique → Revise** — iterate until your prompt scores 90+/100 for the exact model you plan to use it with.

![MIT License](https://img.shields.io/badge/license-MIT-8b5cf6) ![Zero install](https://img.shields.io/badge/install-none%20%E2%80%94%20one%20HTML%20file-22d3ee) ![Works with](https://img.shields.io/badge/works%20with-Claude%20%C2%B7%20GPT%20%C2%B7%20Gemini%20%C2%B7%20DeepSeek%20%C2%B7%20Llama%20%C2%B7%20Mistral-34d399)

![PromptLoop demo — the agentic loop improving a weak prompt from 0 to 95](assets/demo.gif)

## What it does

- **Scores your prompt like an engineer, not a vibe.** Six ingredients — role, objective, context, constraints, output format, reasoning trigger — each rated 0–5 with evidence, plus six anti-pattern checks. The total is computed deterministically in code, so the AI can't grade its own homework.
- **Rewrites for the model you'll actually use.** A prompt tuned for Claude is not optimal for Llama. PromptLoop applies a per-model behavior profile (instruction style, format habits, known failure modes, house rules) and every single change is annotated with *why* it was made.
- **Improves itself every time you use it.** Give any change a 👍 or 👎. Votes promote profile rules to "learned" or disable them entirely — so the next run genuinely behaves differently. All learning stays in your browser.

## How it works

![PromptLoop architecture — Analyze, Rewrite, Critique, Revise loop with model profiles and feedback](assets/diagram.svg)

The loop stops honestly: when the score hits 90+, when a round stops adding value (plateau), or at the round cap — and it tells you which one happened. A "coach" model runs the loop (default: DeepSeek, costs about a cent per run); the "target" model is who your prompt is *for*. They're deliberately independent — that's the whole point.

## Get started in 60 seconds

1. **Download [`PromptLoop.html`](PromptLoop.html)** (right-click → Save link as) — or clone this repo.
2. **Double-click the file.** It opens in your browser. Click **▶ Watch a sample run** to see the loop with zero setup.
3. **For real runs:** grab a free key at [openrouter.ai/keys](https://openrouter.ai/keys), click **API key** in the top-right, paste it. One key unlocks every model.

Then paste any prompt you actually use, pick your target model, and hit **Run the loop**.

## How the learning works (honestly)

The six model profiles ship as **seed heuristics** — starting hypotheses written from public provider documentation and community experience, *not* benchmarked claims. Every field is labeled with its confidence and provenance, and the app exists to correct them:

- 👍 / 👎 on any change votes on the rule that motivated it.
- Net **+3** promotes a rule to medium confidence, **+6** to high ("learned").
- Net **−3** disables a rule — the rewriter stops applying it for that model.
- The **Model profiles** panel shows exactly what's seed vs. learned, with vote counts.

Everything — your API key, your votes, your learned profiles — lives in `localStorage` in your browser. Nothing is sent anywhere except your prompt to OpenRouter when you run the loop. Found profile rules that work? **Export the JSON** from the profiles panel and open a PR — the [`profiles/`](profiles/) folder is the shared, community-refined version.

## Supported models

| Model | OpenRouter id | Role |
|---|---|---|
| Claude Sonnet 5 | `anthropic/claude-sonnet-5` | target |
| GPT-5.5 | `openai/gpt-5.5` | target |
| Gemini 3.5 Flash | `google/gemini-3.5-flash` | target |
| DeepSeek V4 Flash | `deepseek/deepseek-v4-flash` | target + default coach |
| Llama 4 Maverick | `meta-llama/llama-4-maverick` | target |
| Mistral Large | `mistralai/mistral-large-2512` | target |

Any other OpenRouter model id works too — type it in the custom field (it just won't have a seeded profile until you teach it one).

## FAQ

**Is my API key safe?** It's stored only in your browser's localStorage and sent only to OpenRouter over HTTPS. This is a single static HTML file — there is no server, no analytics, no tracking. The code is right there; read it.

**Does it cost money?** A full loop makes 5–10 small model calls. With the default coach that's roughly **$0.01 per run**. OpenRouter also offers free-tier models you can set as coach.

**Why one HTML file instead of an app?** Zero friction and full auditability. Anyone can download it, open it, and read every line of what runs on their machine — which matters for a file you give an API key to.

**Can I add my own model?** Type any OpenRouter id in the custom field, or copy a JSON file in [`profiles/`](profiles/) as a template and PR it.

## Roadmap

- Community profile merging (import a shared profile pack)
- Side-by-side "prove it" runs — original vs. improved on the target model
- Packaged desktop build for offline-first teams
- More seeded models as their behavior stabilizes

---

Built by [Umair Shoaiby](https://github.com/umairshoaiby) · MIT License
