# tixaho.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tixaho – Custom AI Companions</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <!-- Puter.js for free client-side AI image generation -->
  <script src="https://js.puter.com/v2/"></script>
  <style>
    :root {
      --bg: #0f0f11;
      --surface: #16181d;
      --text: #e5e7eb;
      --text-secondary: #9ca3af;
      --accent: #6366f1;
      --accent-dark: #4f46e5;
      --border: #272a31;
    }

    * { margin:0; padding:0; box-sizing:border-box; }
    body { font-family:'Inter',system-ui,sans-serif; background:var(--bg); color:var(--text); line-height:1.6; }
    .container { max-width:1280px; margin:0 auto; padding:0 1.5rem; }
    header { padding:1.5rem 0; border-bottom:1px solid var(--border); position:sticky; top:0; background:rgba(15,15,17,0.85); backdrop-filter:blur(12px); z-index:100; }
    nav { display:flex; justify-content:space-between; align-items:center; }
    .logo { font-size:1.5rem; font-weight:700; letter-spacing:-0.025em; background:linear-gradient(90deg,#a5b4fc,#c4b5fd); -webkit-background-clip:text; -webkit-text-fill-color:transparent; }
    .nav-links a { color:var(--text-secondary); text-decoration:none; margin-left:2rem; font-weight:500; transition:color 0.2s; cursor:pointer; }
    .nav-links a:hover { color:white; }
    .hero { padding:8rem 0 6rem; text-align:center; }
    .hero h1 { font-size:clamp(2.8rem,8vw,5.5rem); font-weight:700; line-height:1.05; margin-bottom:1.5rem; background:linear-gradient(90deg,#e0e7ff,#c7d2fe,#a5b4fc); -webkit-background-clip:text; -webkit-text-fill-color:transparent; }
    .hero p { font-size:1.375rem; color:var(--text-secondary); max-width:640px; margin:0 auto 2.5rem; }
    .price-tag { display:inline-block; background:rgba(99,102,241,0.12); border:1px solid rgba(99,102,241,0.3); border-radius:999px; padding:1rem 2rem; font-size:1.5rem; font-weight:600; margin:1.5rem 0 3rem; }
    .price-tag strong { color:#e0e7ff; }
    .cta-buttons { display:flex; gap:1.25rem; justify-content:center; flex-wrap:wrap; }
    .btn { padding:1rem 2.25rem; font-size:1.125rem; font-weight:600; border-radius:999px; text-decoration:none; transition:all 0.25s; cursor:pointer; }
    .btn-primary { background:var(--accent); color:white; border:none; }
    .btn-primary:hover { background:var(--accent-dark); transform:translateY(-2px); }
    .btn-outline { background:transparent; border:1.5px solid var(--accent); color:var(--accent); }
    .btn-outline:hover { background:rgba(99,102,241,0.1); }
    .features, .generator, .gallery { padding:6rem 0; }
    .features { background:var(--surface); }
    .section-title { text-align:center; font-size:2.5rem; font-weight:700; margin-bottom:4rem; }
    .grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(320px,1fr)); gap:2rem; }
    .card { background:rgba(30,32,40,0.6); border:1px solid var(--border); border-radius:1rem; padding:2rem; transition:all 0.3s; }
    .card:hover { transform:translateY(-8px); border-color:var(--accent); box-shadow:0 20px 40px rgba(0,0,0,0.4); }
    .card h3 { font-size:1.5rem; margin-bottom:1rem; color:#e0e7ff; }
    .promo { text-align:center; padding:5rem 0; background:linear-gradient(135deg,#1e1b4b 0%,#312e81 100%); }
    .promo h2 { font-size:2.8rem; margin-bottom:1.5rem; }
    .promo .highlight { color:#c4b5fd; font-weight:600; }
    footer { padding:4rem 0 2rem; text-align:center; color:var(--text-secondary); border-top:1px solid var(--border); }

    /* Generator styles */
    #generator-form { max-width:600px; margin:0 auto 3rem; display:flex; flex-direction:column; gap:1.5rem; }
    #prompt { padding:1rem; font-size:1.125rem; border-radius:0.75rem; border:1px solid var(--border); background:var(--surface); color:var(--text); }
    #generate-btn { align-self:center; }
    #results { display:grid; grid-template-columns:repeat(auto-fit,minmax(280px,1fr)); gap:1.5rem; }
    .generated-img { width:100%; border-radius:0.75rem; border:1px solid var(--border); }
    .img-card { position:relative; }
    .download-btn { position:absolute; bottom:1rem; left:50%; transform:translateX(-50%); background:rgba(0,0,0,0.6); color:white; padding:0.5rem 1rem; border-radius:999px; font-size:0.9rem; cursor:pointer; }

    /* Modal */
    #signin-modal { display:none; position:fixed; inset:0; background:rgba(0,0,0,0.8); align-items:center; justify-content:center; z-index:200; }
    .modal-content { background:var(--surface); padding:3rem; border-radius:1rem; max-width:400px; text-align:center; border:1px solid var(--border); }
    .close { float:right; font-size:2rem; cursor:pointer; }

    @media (max-width:640px) {
      .hero { padding:6rem 0 4rem; }
      .hero h1 { font-size:3.5rem; }
      .price-tag { font-size:1.25rem; padding:0.875rem 1.5rem; }
    }
  </style>
</head>
<body>

  <header>
    <div class="container">
      <nav>
        <div class="logo">Tixaho</div>
        <div class="nav-links">
          <a onclick="document.getElementById('features').scrollIntoView({behavior:'smooth'})">Features</a>
          <a onclick="document.getElementById('generator').scrollIntoView({behavior:'smooth'})">Create</a>
          <a onclick="document.getElementById('gallery').scrollIntoView({behavior:'smooth'})">Gallery</a>
          <a onclick="document.getElementById('signin-modal').style.display='flex'">Sign In</a>
        </div>
      </nav>
    </div>
  </header>

  <section class="hero">
    <div class="container">
      <h1>Build Your Perfect AI Companion</h1>
      <p>Customize personality, appearance, voice, knowledge, hobbies, relationship style — then chat in real-time with ultra-realistic memory & emotional depth.</p>
      <div class="price-tag">
        <strong>$2.50</strong> per minute • Billed only for active chat time • Competitive industry rates
      </div>
      <div class="cta-buttons">
        <a href="#" class="btn btn-primary">Start Free Onboarding</a>
        <a onclick="document.getElementById('generator').scrollIntoView({behavior:'smooth'})" class="btn btn-outline">Generate Character Now</a>
      </div>
    </div>
  </section>

  <section class="generator" id="generator">
    <div class="container">
      <h2 class="section-title">Generate Your AI Companion</h2>
      <p style="text-align:center; max-width:700px; margin:0 auto 2rem; color:var(--text-secondary);">
        Describe your ideal companion (appearance, style, mood, clothing, etc.) and generate realistic images instantly — free previews powered by advanced AI models.
      </p>
      <form id="generator-form">
        <textarea id="prompt" rows="4" placeholder="e.g., A stunning 25-year-old woman with long wavy black hair, green eyes, wearing a red dress, soft lighting, highly detailed, realistic"></textarea>
        <button type="button" id="generate-btn" class="btn btn-primary">Generate Images</button>
      </form>
      <div id="results"></div>
    </div>
  </section>

  <section class="features" id="features">
    <div class="container">
      <h2 class="section-title">Everything You Need to Create Something Real</h2>
      <div class="grid">
        <div class="card"><h3>Deep Personality Builder</h3><p>Over 40 sliders & text fields: dominance, affection, sarcasm, kink preferences, moral alignment, speech patterns, emotional triggers...</p></div>
        <div class="card"><h3>Visual Customization</h3><p>Upload reference images or describe in detail — get consistent character visuals across messages, selfies & voice calls.</p></div>
        <div class="card"><h3>Long-term Memory</h3><p>Remembers months of conversation, inside jokes, your preferences, anniversaries — feels like talking to the same person every time.</p></div>
        <div class="card"><h3>Voice & Video Calls</h3><p>Real-time voice (multiple accents/styles) + animated talking avatar (coming soon).</p></div>
        <div class="card"><h3>Privacy First</h3><p>End-to-end encryption, no training on your chats, option to fully delete character & history instantly.</p></div>
        <div class="card"><h3>Free Onboarding Forever</h3><p>Create & test your character completely free. Only pay when you start real 1:1 conversations.</p></div>
      </div>
    </div>
  </section>

  <section class="gallery" id="gallery">
    <div class="container">
      <h2 class="section-title">Example Characters</h2>
      <p style="text-align:center; color:var(--text-secondary);">Browse generated examples or create your own above.</p>
      <div class="grid">
        <div class="card"><img src="https://via.placeholder.com/400x500/4f46e5/fff?text=Example+1" alt="Example character" style="width:100%;border-radius:0.75rem;"></div>
        <div class="card"><img src="https://via.placeholder.com/400x500/6366f1/fff?text=Example+2" alt="Example character" style="width:100%;border-radius:0.75rem;"></div>
        <div class="card"><img src="https://via.placeholder.com/400x500/a5b4fc/000?text=Example+3" alt="Example character" style="width:100%;border-radius:0.75rem;"></div>
      </div>
    </div>
  </section>

  <section class="promo">
    <div class="container">
      <h2>Get <span class="highlight">2 hours free credit</span><br>when you finish onboarding</h2>
      <p style="font-size:1.25rem; max-width:600px; margin:2rem auto; color:#d1d5db;">
        No credit card required to build your character.<br>
        Only charged when you decide to begin the real conversation — at competitive $2.50/min rates.
      </p>
      <a href="#" class="btn btn-primary" style="font-size:1.25rem; padding:1.25rem 3rem;">
        Create My Character → Free
      </a>
    </div>
  </section>

  <footer>
    <div class="container">
      <p>© 2026 Tixaho • All rights reserved • <a href="#" style="color:var(--text-secondary);">Terms</a> • <a href="#" style="color:var(--text-secondary);">Privacy</a></p>
    </div>
  </footer>

  <!-- Sign In Modal (placeholder) -->
  <div id="signin-modal">
    <div class="modal-content">
      <span class="close" onclick="document.getElementById('signin-modal').style.display='none'">&times;</span>
      <h2>Sign In to Tixaho</h2>
      <p style="margin:2rem 0;">Coming soon: Full login with email or social.<br>For now, browse and generate freely!</p>
      <button class="btn btn-primary" onclick="alert('Demo login successful! Welcome back.')">Demo Login</button>
    </div>
  </div>

  <script>
    // AI Image Generator using Puter.js (free, no key)
    const generateBtn = document.getElementById('generate-btn');
    const promptInput = document.getElementById('prompt');
    const resultsDiv = document.getElementById('results');

    generateBtn.addEventListener('click', async () => {
      const prompt = promptInput.value.trim();
      if (!prompt) {
        alert('Please enter a description!');
        return;
      }

      resultsDiv.innerHTML = '<p style="text-align:center;">Generating... (usually 5-30 seconds)</p>';

      try {
        const imageUrl = await puter.ai.imageGen(prompt);
        resultsDiv.innerHTML = `
          <div class="img-card">
            <img class="generated-img" src="${imageUrl}" alt="Generated AI companion">
            <button class="download-btn" onclick="window.open('${imageUrl}', '_blank')">Download</button>
          </div>
        `;
      } catch (err) {
        resultsDiv.innerHTML = `<p style="color:#ef4444; text-align:center;">Error: ${err.message || 'Try again later'}</p>`;
      }
    });
  </script>

</body>
</html>
