# MeetingMind

**AI-powered meeting assistant that turns raw transcripts into structured key points and prioritized action items — built for the AWS Builder Weekend Productivity Challenge.**

🔗 **Live app:** [add your Amplify URL here]
📄 **Full write-up:** [add your Builder Center article link here]

---

## Overview

Meetings generate a lot of conversation and very little structure. You leave a call knowing roughly what was discussed, but turning that into a clear record of decisions and next steps usually falls to whoever remembers to write it down.

MeetingMind closes that gap. Paste in a transcript or rough notes, and in seconds you get back:

- **Key Points** — a concise summary of what was actually discussed
- **Action Items** — specific tasks extracted from the conversation
- **Priority** — high / medium / low, based on urgency and stated deadlines
- **Reasoning** — a one-line explanation for each priority ranking

No accounts. No setup. Paste in, structured output out.

---

## Features

- 🤖 AI-powered transcript analysis with visible reasoning per task
- 🎯 Automatic priority ranking (high / medium / low)
- 📝 Key-point extraction, separate from action items
- ⚡ Instant results — a single API call, no backend round trip
- 🔒 API key stored only in the browser, sent nowhere except directly to the AI provider
- ☁️ Fully static, serverless architecture
- 🎨 Framework-free frontend — plain HTML, CSS, and JavaScript, zero build step

---

## Architecture

```
Browser (HTML/CSS/JS on AWS Amplify Hosting)
   │  Direct HTTPS call
   ▼
Groq API (llama-3.3-70b-versatile)
   │  Structured JSON response
   ▼
Rendered in-browser — key points + prioritized action items
```

There's no backend compute layer. AWS Amplify Hosting serves the static assets; all AI processing happens via a direct client-side API call. The entire stack runs inside AWS's free tier for personal use, with the only external dependency being the AI API call itself.

| Service | Purpose |
|---|---|
| **AWS Amplify Hosting** | Deploys and serves the static frontend directly from GitHub, with automatic builds on push |
| **Groq API** | Extracts key points and prioritized action items from transcript text |

---

## How It Works

1. User pastes a meeting transcript into the textarea.
2. On submit, the app sends a single structured prompt to the Groq API, explicitly specifying the expected JSON schema (`key_points` array + `tasks` array, each task with a priority and reasoning field).
3. The response is defensively parsed — markdown code fences are stripped before `JSON.parse()` runs, since language models occasionally wrap output in explanatory text.
4. Results are rendered directly into the UI, grouped into Key Points and Action Items sections.

---

## Run It Yourself

1. Clone this repo.
2. Open `frontend/index.html` directly in a browser — no build step, no dependencies.
3. Get a free API key at [console.groq.com](https://console.groq.com) (no billing setup required for free-tier usage).
4. Paste your key into the app and start summarizing transcripts.

### Deploy your own copy on AWS Amplify

1. Fork this repo.
2. AWS Console → **Amplify** → **New app** → **Deploy from GitHub**.
3. Connect your fork. Since the site lives in `frontend/`, set that as the app's root directory in the build settings.
4. Amplify builds and gives you a live URL in a few minutes.

---

## Why This Architecture

Built to run entirely client-side so it deploys instantly on AWS Amplify with zero backend infrastructure — no Lambda, no API Gateway, no database. This kept the build scoped tightly enough to ship reliably within a weekend timeframe, while still fully satisfying the challenge's AWS-service requirement through Amplify Hosting.

---

## Challenges

The main technical challenge was getting consistently parseable output from the model — early responses sometimes included explanatory text or markdown fences around the JSON. This was solved with a strict prompt schema plus a defensive stripping step before parsing, rather than relying on the model to always format perfectly on the first try.

---

## What I Learned

- Treating an LLM as a structured-data API, not a chat partner — a strict schema plus defensive parsing is the difference between a demo and something that works reliably every time.
- How much of a time-boxed build can be shaped by infrastructure and account onboarding, not just code — and how to design around that constraint rather than fight it.
- The value of shipping the smallest thing that fully works over a half-finished, more ambitious architecture.

---

## Future Improvements

- Move the API call behind a lightweight backend (e.g., AWS Lambda) so the API key never touches the client
- Persist past summaries so users can revisit previous meetings
- Support direct audio upload with transcription before summarization
- Export action items to a calendar or task manager
- Multi-speaker attribution, tagging action items to the person who owns them

---

Built for the AWS Builder Center Weekend Productivity Challenge.
