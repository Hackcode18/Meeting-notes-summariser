<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MeetingMind — Transcript to Action Items</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Space+Grotesk:wght@400;500;700&display=swap');

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: #0B0F14;
    color: #E4E9ED;
    font-family: 'Space Grotesk', sans-serif;
    min-height: 100vh;
    padding: 40px 20px;
  }

  .container {
    max-width: 820px;
    margin: 0 auto;
  }

  header {
    margin-bottom: 32px;
  }

  .eyebrow {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.1em;
    color: #5EEAB4;
    text-transform: uppercase;
  }

  h1 {
    font-size: 36px;
    font-weight: 700;
    letter-spacing: -0.02em;
    margin-top: 8px;
  }

  h1 span { color: #5EEAB4; }

  .sub {
    color: #8A96A3;
    margin-top: 8px;
    font-size: 15px;
  }

  .key-row {
    margin-top: 24px;
    display: flex;
    gap: 8px;
  }

  input[type="password"], textarea {
    background: #10161D;
    border: 1px solid #1F2933;
    border-radius: 8px;
    color: #E4E9ED;
    padding: 12px 14px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    width: 100%;
  }

  textarea {
    margin-top: 20px;
    min-height: 220px;
    resize: vertical;
    font-family: 'Space Grotesk', sans-serif;
    font-size: 14px;
    line-height: 1.6;
  }

  textarea::placeholder { color: #4A5560; }

  button {
    background: #5EEAB4;
    color: #0B0F14;
    border: none;
    border-radius: 8px;
    padding: 12px 20px;
    font-weight: 700;
    font-size: 14px;
    cursor: pointer;
    font-family: 'Space Grotesk', sans-serif;
    white-space: nowrap;
  }

  button:hover { opacity: 0.9; }
  button:disabled { opacity: 0.4; cursor: not-allowed; }

  .run-btn {
    margin-top: 16px;
    width: 100%;
    padding: 14px;
  }

  .save-note {
    font-size: 11px;
    color: #4A5560;
    margin-top: 6px;
    font-family: 'JetBrains Mono', monospace;
  }

  #results { margin-top: 32px; }

  .section-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #5A6774;
    margin: 24px 0 12px;
  }

  .point-row, .task-row {
    background: #10161D;
    border: 1px solid #1F2933;
    border-radius: 8px;
    padding: 12px 14px;
    margin-bottom: 8px;
    display: flex;
    gap: 12px;
    align-items: flex-start;
  }

  .prio {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.06em;
    padding: 4px 9px;
    border-radius: 100px;
    text-transform: uppercase;
    flex-shrink: 0;
    margin-top: 2px;
  }

  .prio.high { background: rgba(255,107,107,0.15); color: #FF6B6B; }
  .prio.medium { background: rgba(255,209,102,0.15); color: #FFD166; }
  .prio.low { background: rgba(94,234,180,0.15); color: #5EEAB4; }

  .task-text { font-size: 14px; }
  .task-reason { font-size: 12px; color: #6B7684; margin-top: 3px; }

  .point-row { font-size: 14px; }
  .point-row::before {
    content: "•";
    color: #5EEAB4;
    font-weight: 700;
  }

  .error {
    background: rgba(255,107,107,0.1);
    border: 1px solid rgba(255,107,107,0.3);
    color: #FF6B6B;
    padding: 12px 14px;
    border-radius: 8px;
    margin-top: 16px;
    font-size: 13px;
    font-family: 'JetBrains Mono', monospace;
  }

  .loading {
    text-align: center;
    color: #8A96A3;
    padding: 24px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
  }

  footer {
    margin-top: 48px;
    text-align: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: #4A5560;
  }
</style>
</head>
<body>
  <div class="container">
    <header>
      <div class="eyebrow">AWS Builder Weekend Challenge</div>
      <h1>Meeting<span>Mind</span></h1>
      <div class="sub">Paste a meeting transcript. Get key points and action items back.</div>

      <div class="key-row">
        <input type="password" id="apiKey" placeholder="Paste your Groq API key here">
      </div>
      <div class="save-note">Your key is stored only in this browser (localStorage) — never sent anywhere except directly to Groq's API.</div>
    </header>

    <textarea id="transcript" placeholder="Paste your meeting transcript or notes here...

Example:
Sarah: We need the design mockups done by Wednesday.
Tom: I'll have the backend API ready by Friday.
Sarah: Let's also loop in marketing about the launch date.
Tom: I'll send the recap email after this call."></textarea>

    <button class="run-btn" id="runBtn">Summarize Transcript</button>

    <div id="results"></div>
  </div>

  <footer>Built with AWS Amplify + Groq API</footer>

<script>
  const keyInput = document.getElementById('apiKey');
  const transcriptInput = document.getElementById('transcript');
  const runBtn = document.getElementById('runBtn');
  const results = document.getElementById('results');

  // restore saved key
  const savedKey = localStorage.getItem('groq_api_key');
  if (savedKey) keyInput.value = savedKey;

  keyInput.addEventListener('change', () => {
    localStorage.setItem('groq_api_key', keyInput.value);
  });

  runBtn.addEventListener('click', async () => {
    const apiKey = keyInput.value.trim();
    const text = transcriptInput.value.trim();

    results.innerHTML = '';

    if (!apiKey) {
      results.innerHTML = '<div class="error">Please enter your Groq API key.</div>';
      return;
    }
    if (!text) {
      results.innerHTML = '<div class="error">Please paste a transcript first.</div>';
      return;
    }

    runBtn.disabled = true;
    results.innerHTML = '<div class="loading">Analyzing transcript...</div>';

    const prompt = `You are a meeting assistant. Read the transcript below and extract:
1. Key discussion points (3-6 short bullet points)
2. Action items with priority and reason

Return ONLY valid JSON, no markdown, no explanation, in this exact format:
{
  "key_points": ["point 1", "point 2"],
  "tasks": [{"task": "short description", "priority": "high|medium|low", "reason": "why this priority"}]
}

Transcript:
${text}`;

    try {
      const response = await fetch(
        'https://api.groq.com/openai/v1/chat/completions',
        {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${apiKey}`
          },
          body: JSON.stringify({
            model: 'llama-3.3-70b-versatile',
            messages: [{ role: 'user', content: prompt }],
            temperature: 0.3
          })
        }
      );

      const data = await response.json();

      if (!response.ok) {
        throw new Error(data.error?.message || 'Request failed');
      }

      let rawText = data.choices[0].message.content.trim();
      if (rawText.startsWith('```')) {
        rawText = rawText.split('```')[1];
        if (rawText.startsWith('json')) rawText = rawText.slice(4);
      }
      const parsed = JSON.parse(rawText.trim());

      renderResults(parsed);
    } catch (err) {
      results.innerHTML = `<div class="error">Error: ${err.message}</div>`;
    } finally {
      runBtn.disabled = false;
    }
  });

  function renderResults(data) {
    let html = '';

    if (data.key_points?.length) {
      html += '<div class="section-title">Key Points</div>';
      data.key_points.forEach(p => {
        html += `<div class="point-row">&nbsp;${escapeHtml(p)}</div>`;
      });
    }

    if (data.tasks?.length) {
      html += '<div class="section-title">Action Items</div>';
      data.tasks.forEach(t => {
        html += `
          <div class="task-row">
            <span class="prio ${t.priority}">${t.priority}</span>
            <div>
              <div class="task-text">${escapeHtml(t.task)}</div>
              <div class="task-reason">${escapeHtml(t.reason)}</div>
            </div>
          </div>`;
      });
    }

    results.innerHTML = html || '<div class="error">No results returned. Try a longer transcript.</div>';
  }

  function escapeHtml(str) {
    const div = document.createElement('div');
    div.textContent = str;
    return div.innerHTML;
  }
</script>
</body>
</html>
