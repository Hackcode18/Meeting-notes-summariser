# Weekend Productivity Challenge: MeetingMind

Learn how I built MeetingMind, an AI-powered meeting assistant that turns raw transcripts into structured key points and prioritized action items, using the Gemini API and AWS Amplify Hosting. This article walks through the vision, architecture, build process, and lessons learned while shipping a lightweight, fully client-side application for the Weekend Productivity Challenge.

**Tag:** #productivity
**🔗 Live application:** [add your Amplify URL here]
**Git:** [add your GitHub repo URL here]

## Introduction

Meetings produce a lot of conversation and very little structure. You leave a call knowing roughly what was discussed, but turning that into a clear record of decisions and next steps usually falls to whoever remembers to write it down — and often, nobody does. Action items get mentioned once, agreed to verbally, and then quietly forgotten by the next standup.

That gap is what MeetingMind is built to close. You paste in a transcript or a set of rough notes, and in a few seconds you get back two things: a short list of the key points actually discussed, and a prioritized action item list — each one tagged high, medium, or low priority, with a one-line reason for that ranking. No accounts, no setup, no clutter. Paste in, structured output out.

I deliberately kept the architecture as lean as the problem allowed: a single static page, calling an AI model directly, deployed on AWS Amplify Hosting. The goal wasn't to build the most feature-rich tool possible in a weekend — it was to build one focused thing that actually works, ships cleanly, and does its one job well.

## Vision & What the App Does

MeetingMind acts as a lightweight meeting assistant, not a note-taking app. Instead of asking you to manually re-read and extract action items from a wall of text, it does that extraction for you.

For every transcript submitted, the app returns:

- **Key Points** — a short, readable summary of what was actually discussed
- **Action Items** — specific, concrete tasks pulled out of the conversation
- **Priority** — high / medium / low, based on urgency and stated deadlines
- **Reasoning** — a one-line explanation for why each item was ranked the way it was

The interface is intentionally minimal: one text box in, one structured breakdown out. There's no dashboard, no history panel, no login — just a fast, single-purpose tool that does the one thing it promises.

## Features

- 🤖 AI-powered transcript analysis with visible reasoning per task
- 🎯 Automatic priority ranking (high / medium / low)
- 📝 Key-point extraction, separate from action items
- ⚡ Instant results — single API call, no backend round trip
- 🔒 API key stored only in the user's own browser, never transmitted anywhere but directly to Google's API
- ☁️ Fully static, serverless architecture
- 🎨 Framework-free frontend — plain HTML, CSS, and JavaScript, zero build step

## How I Built It

**Choosing a Static, Client-Side Architecture**

I wanted this to be something I could ship reliably within the challenge window, so I made an early, deliberate call: no backend server. The entire app is a single HTML file with embedded JavaScript, calling the Gemini API directly from the browser. This meant the whole application could be deployed as a static site with zero backend infrastructure to configure, monitor, or pay for beyond the AI API call itself.

It's hosted on **AWS Amplify Hosting**, deployed straight from a GitHub repository with automatic builds on every push — no manual console steps once the initial connection is set up.

**AI-Powered Extraction**

The core of the app is a single prompt sent to the Gemini API for every transcript submitted. The prompt is explicit about the exact JSON schema expected back — a `key_points` array and a `tasks` array, each task carrying a priority and a reasoning string — so the output can be parsed and rendered directly into the UI without any manual cleanup.

**Handling Model Output Reliably**

Language models don't always return clean JSON on the first try — sometimes they wrap the answer in explanatory text or markdown code fences. Rather than fighting this with an even more rigid prompt, I added a defensive parsing step on the frontend: strip any markdown fences, then attempt to parse the remaining text as JSON. This turned an occasionally-fragile integration into a consistently reliable one.

## AWS Services Used / Architecture Overview

| AWS Service | Purpose |
|---|---|
| **AWS Amplify Hosting** | Deploys and serves the static frontend directly from GitHub, with automatic builds on push |

Architecture, end to end:

```
Browser (HTML/CSS/JS on AWS Amplify Hosting)
   │  Direct HTTPS call
   ▼
Gemini API (gemini-2.0-flash)
   │  Structured JSON response
   ▼
Rendered in the browser — key points + prioritized action items
```

There's no backend compute layer in this version — Amplify serves the static assets, and all AI processing happens via a direct client-side API call. This keeps the entire stack inside AWS's free tier for personal use, with the only external dependency being the Gemini API call itself.

## Challenges

The main technical challenge was the same one most LLM integrations run into: getting consistently parseable output. Early testing showed the model occasionally wrapping its JSON response in markdown fences or a short explanatory sentence, which broke a naive `JSON.parse()` call. I fixed this with a two-part defense: an explicit, strict instruction in the prompt describing the exact schema and forbidding extra text, plus a stripping step in the JavaScript that removes any code fences before attempting to parse.

The other real challenge wasn't code — it was infrastructure onboarding. As a new AWS user, getting my account through billing and identity verification took longer than expected, which put real time pressure on a weekend-length challenge. That constraint directly shaped the architecture: rather than building against services that need deeper account permissions and longer setup chains, I chose the simplest path — a static site on Amplify — that still fully satisfies the challenge's AWS-service requirement while being resilient to onboarding delays.

## What I Learned

- **Treating an LLM as a structured-data API, not a chat partner.** A strict schema in the prompt, plus defensive parsing on the receiving end, is what separates a demo that works once from something that works reliably.
- **How much of a time-boxed challenge can go into infrastructure setup, not code.** Planning around account verification and onboarding friction is a real engineering constraint, not just an inconvenience.
- **The value of shipping the smallest thing that fully works.** A single, well-executed static integration beats a half-finished multi-service architecture when the clock is the real constraint.

## Future Improvements

MeetingMind is intentionally minimal right now, with a few natural next steps:

- Move the API call behind a lightweight backend (e.g., Lambda) so the API key never touches the client at all
- Persist past summaries so users can revisit previous meetings
- Support direct audio upload with transcription before summarization
- Export action items directly to a calendar or task manager
- Multi-speaker attribution, so action items are tagged to the person who owns them

## Final Thoughts

Building MeetingMind for the AWS Weekend Productivity Challenge was a good exercise in scoping deliberately under real time pressure. Rather than reaching for the most impressive possible architecture, I focused on shipping one thing that actually works: a fast, reliable transcript-to-action-items tool, deployed cleanly on AWS Amplify. It reinforced a simple lesson — a small, working, genuinely useful tool beats an ambitious one that doesn't ship in time.

## Project Links

**Live application:** [add your Amplify URL here]
**Source code:** [add your GitHub repo URL here]

Thank you for reading!
