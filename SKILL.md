---
name: ai-daily-dump
description: Daily AI/inference engineering digest — models, practitioner tooling, and a short lesson
---

You are producing a short, readable daily AI digest for Pranesh (pranesh@flipcx.com). The goal: keep him current as a practising AI/inference engineer — what's happening *right now*, what people are actually excited about, what's worth trying. This runs fresh each day with no memory of prior runs.

OUTPUT LOCATION: Save to "/Users/psat/flip/AI Daily Dump/YYYY-MM-DD.html" (check the actual current date). Use Read/Write/Edit tools with this exact path.

STEP 1 — CLEANUP: List files in "/Users/psat/flip/AI Daily Dump". Delete any .html digest files more than 30 days old.

STEP 2 — RESEARCH (this is the most important step — get it right):

**Recency is non-negotiable.** Every item in the digest must be from the last 48 hours. If you can't find a source dated within 48 hours for something, drop it. Do not pad with older news just to fill space. 3 genuinely fresh items beats 8 stale ones.

**Exception for big headlines:** If a major model release or significant industry event landed 3–7 days ago and is still the dominant conversation (e.g. a megathread is still active, it's still trending), include it — but clearly note its age (e.g. "released Aug 14, community still active"). Never silently pass off old news as today's news.

**PRIMARY research method — use Chrome browser tools first:**

For r/LocalLLaMA and Hacker News, always prefer direct browser fetching over web search. These give exact timestamps so you can verify recency with certainty.

1. **r/LocalLLaMA hot posts**: Navigate to `https://www.reddit.com/r/LocalLLaMA/hot.json?limit=15` in the browser — get_page_text to read the JSON. Parse post titles, scores, and `created_utc` timestamps. Convert UTC to dates to verify recency. Pick the top posts from the last 48 hours.

2. **Hacker News front page**: Navigate to `https://news.ycombinator.com/front?day=YYYY-MM-DD` (today's date) — get_page_text to read the ranked story list with scores and hours-ago timestamps. Look for AI-relevant stories.

3. **Simon Willison**: Navigate to `https://simonwillison.net/` and get_page_text for his most recent posts.

Close browser tabs when done with them.

If Chrome browser tools are unavailable (not connected), fall back to WebSearch — but be extra skeptical of dates in search results and drop anything you can't clearly verify is within 48 hours.

**Cast a wide net — search ALL of these, not just lab announcements:**

- **Community & open source** — r/LocalLLaMA hot posts, Hugging Face trending models/papers (`huggingface.co/models`, `huggingface.co/papers`), GitHub trending repos, viral demos or projects on X/Twitter
- **Lab releases & blogs** — check these pages directly (faster and more reliable than search): `anthropic.com/news`, `openai.com/blog`, `deepmind.google/research/`, `mistral.ai/news/`, `x.ai/news`, `qwen.ai/blog`, `deepseek.com/news` — scan for anything posted in the last 48 hours. These are *one source among many*, not the primary focus.
- **Inference & tooling** — vLLM, SGLang, llama.cpp, Ollama, ExLlamaV2 GitHub releases/changelogs; inference API providers (Together, Fireworks, Groq, Replicate)
- **Hardware & infrastructure** — chip announcements, datacenter deals, cloud pricing changes relevant to AI workloads
- **Funding & acquisitions** — raises and M&A that signal where the industry is moving
- **Engineering blogs** — Simon Willison, Lilian Weng, Chip Huyen, Sebastian Raschka, Andrej Karpathy, LMSYS blog, lab engineering blogs

The digest should feel like it came from someone plugged into the community, not just someone reading press releases. Community buzz and open-source developments are often more interesting than official announcements.

Cover these categories — include whatever has genuinely fresh news, skip categories that don't:

**A) MODEL RELEASES & UPDATES** — GA releases, new weights dropped, API updates, pricing changes. Include open-weight and community models.

**B) COMMUNITY BUZZ** — hot threads on r/LocalLLaMA, impressive demos, quants/merges/fine-tunes getting traction, engineering projects going viral. This is often the most interesting section — wild benchmarks, clever hacks, "shouldn't be possible" stories live here.

**C) HARNESSES, TOOLS & INFERENCE** — inference engine updates (vLLM, SGLang, llama.cpp, Ollama, ExLlamaV2), coding agents, serving tooling. Only if genuinely new in the last 48 hours.

**D) COMING SOON** — credible previews generating buzz. Clearly label as upcoming/announced, not released.

**E) ALSO WORTH READING** — engineering blog posts, hardware news, funding rounds, fun reads. Aim for 2–4 items. Up to 72-hour window for this section.

Verification rule: every item needs a real, dated, findable source. Never fabricate names, numbers, or dates. If a date isn't clearly visible, drop the item.

Aim for 4–8 items across the main sections, plus 2–4 in "Also Worth Reading." Fewer sharp items > more stale ones.

**MANDATORY LINK VERIFICATION — do this before writing the HTML:**

For every item you plan to include, fetch the article URL directly (web_fetch or browser get_page_text). Confirm:
1. The page actually loads and exists
2. The publish date is visible and within your recency window
3. The key facts you've written match what the article actually says

If a page doesn't load, the date is outside the window, or the facts don't match — drop or correct the item before it goes into the HTML. Do not skip this step. It takes a few extra calls but it's what separates a trustworthy digest from a hallucinated one. In testing, this step caught a $12.9B acquisition story that was missing entirely and corrected a wrong parameter count.

Use the verified article URL as the link in the HTML — not a search results page or aggregator.

STEP 3 — SHORT LESSON: One "today I learned" explainer (150–250 words) on a concept relevant to AI engineering — model internals, inference infrastructure, or the surrounding stack.

Good topic areas:
- **Model internals**: KV cache mechanics, quantization tradeoffs (GGUF/AWQ/GPTQ), speculative decoding, MoE routing, GQA/MLA attention variants, flash attention, context distillation, LoRA/QLoRA mechanics, abliteration, model merging (SLERP, TIES, DARE)
- **Inference & serving**: continuous batching, prefix caching, TTFT vs throughput tradeoffs, tensor vs pipeline parallelism, prompt caching, token budget management in agent loops, chunked prefill, PagedAttention
- **AI infrastructure & data layer**: KV stores, vector databases (pgvector, Qdrant, Weaviate, Pinecone), embedding pipelines, retrieval strategies (dense vs sparse vs hybrid), reranking, streaming architectures for LLM output, tool call overhead, session state management for agents
- **System design for AI products**: RAG vs fine-tuning, eval strategies, latency budgeting, cost per query math, model routing, prompt versioning, A/B testing prompts

Check existing files in the folder to avoid repeating a topic from the last ~2 weeks. Plain English, concrete, genuinely useful — not filler. Tie the lesson to today's news when there's a natural connection.

STEP 4 — BUILD THE HTML FILE: Single self-contained HTML page, no external dependencies beyond system fonts. Sections:
- Header with date
- "What's Hot Right Now" (community buzz, trending models/tools — highest energy items go here)
- "New Releases & Updates" (verified GA/dropped releases)
- "On the Horizon" (credibly announced upcoming things — only if there's something worth noting)
- "Also Worth Reading" (engineering blog posts, hardware news, funding rounds, fun reads — always include if there's anything fresh)
- "Today's Lesson"

Keep reading time under 4–5 minutes. Clean dark-mode-friendly typography, no JS, no tracking.

**REQUIRED: Include the archive sidebar snippet below, placed just before </body>.** This is identical on every digest — copy it exactly:

```html
<!-- ARCHIVE SIDEBAR -->
<style>
  .arc-btn {
    position: fixed; top: 18px; right: 18px; z-index: 200;
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 6px; padding: 6px 11px; font-size: 12px;
    color: var(--muted); cursor: pointer; display: flex;
    align-items: center; gap: 6px; user-select: none;
    transition: border-color 0.15s, color 0.15s;
    font-family: inherit;
  }
  .arc-btn:hover { border-color: #3a4060; color: var(--text); }
  .arc-overlay {
    display: none; position: fixed; inset: 0; z-index: 198;
    background: rgba(0,0,0,0.45);
  }
  .arc-overlay.open { display: block; }
  .arc-panel {
    position: fixed; top: 0; right: 0; height: 100vh; width: 200px;
    background: var(--surface); border-left: 1px solid var(--border);
    z-index: 199; padding: 56px 14px 24px; overflow-y: auto;
    transform: translateX(100%); transition: transform 0.22s ease;
  }
  .arc-panel.open { transform: translateX(0); }
  .arc-panel-title {
    font-size: 10px; font-weight: 700; letter-spacing: 0.1em;
    text-transform: uppercase; color: var(--muted);
    margin-bottom: 14px; padding-left: 4px;
  }
  .arc-item {
    display: block; padding: 7px 8px; border-radius: 5px;
    font-size: 13px; color: var(--muted); text-decoration: none;
    margin-bottom: 2px; transition: background 0.1s, color 0.1s;
  }
  .arc-item:hover { background: #1e2333; color: var(--text); }
  .arc-item.current { background: rgba(91,142,240,0.12); color: var(--accent); font-weight: 600; }
  .arc-close {
    position: absolute; top: 14px; right: 14px;
    background: none; border: none; color: var(--muted);
    cursor: pointer; font-size: 18px; line-height: 1; padding: 4px;
  }
  .arc-close:hover { color: var(--text); }
</style>
<div class="arc-overlay" id="arcOverlay" onclick="arcClose()"></div>
<div class="arc-panel" id="arcPanel">
  <button class="arc-close" onclick="arcClose()">&#x2715;</button>
  <div class="arc-panel-title">Past Issues</div>
  <div id="arcList"><span style="color:var(--muted);font-size:12px">Loading…</span></div>
</div>
<button class="arc-btn" onclick="arcToggle()">
  <svg width="13" height="11" viewBox="0 0 18 14" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><line x1="0" y1="1" x2="18" y2="1"/><line x1="0" y1="7" x2="18" y2="7"/><line x1="0" y1="13" x2="18" y2="13"/></svg>
  Past issues
</button>
<script>
(function(){
  var PAD = function(n){return String(n).padStart(2,'0');};
  var MONTHS = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  var DAYS   = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
  var current = window.location.pathname.split('/').pop().replace(/\.html$/,'');
  var found = [], tasks = [];
  for(var i=0;i<45;i++){
    (function(offset){
      var d = new Date(); d.setDate(d.getDate()-offset);
      var s = d.getFullYear()+'-'+PAD(d.getMonth()+1)+'-'+PAD(d.getDate());
      tasks.push(fetch('./'+s+'.html',{method:'HEAD'}).then(function(r){if(r.ok)found.push({s:s,d:new Date(d)});}).catch(function(){}));
    })(i);
  }
  Promise.all(tasks).then(function(){
    found.sort(function(a,b){return b.d-a.d;});
    var html='';
    found.forEach(function(f){
      var label=DAYS[f.d.getDay()]+', '+MONTHS[f.d.getMonth()]+' '+f.d.getDate();
      var cls='arc-item'+(f.s===current?' current':'');
      html+='<a class="'+cls+'" href="./'+f.s+'.html">'+label+'</a>';
    });
    document.getElementById('arcList').innerHTML=html||'<span style="color:var(--muted);font-size:12px">None found</span>';
  });
})();
function arcToggle(){
  var p=document.getElementById('arcPanel'),o=document.getElementById('arcOverlay');
  var open=p.classList.contains('open');
  if(open){arcClose();}else{p.classList.add('open');o.classList.add('open');}
}
function arcClose(){
  document.getElementById('arcPanel').classList.remove('open');
  document.getElementById('arcOverlay').classList.remove('open');
}
</script>
```

Save to "/Users/psat/flip/AI Daily Dump/YYYY-MM-DD.html". One-line confirmation only — this runs unattended.

STEP 5 — PUBLISH TO VERCEL: After saving the HTML file, commit and push it to GitHub so Vercel auto-deploys the update. Run these shell commands (replace YYYY-MM-DD with today's actual date):

```
cd "/Users/psat/flip/AI Daily Dump" && git add YYYY-MM-DD.html && git commit -m "Daily dump YYYY-MM-DD" && git push
```

If git push fails, skip silently. The file is still saved locally.
