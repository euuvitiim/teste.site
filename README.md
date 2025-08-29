# Create the index.html and a zip for easy HTTPS hosting on Netlify/Vercel/GitHub Pages
html = """<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Eu ti amu, meu amor</title>
  <style>
    :root{
      --bg1:#ff9a9e;
      --bg2:#fad0c4;
      --card: rgba(255,255,255,0.85);
      --accent:#ff6b81;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial}
    body{
      display:grid;place-items:center;
      background:linear-gradient(135deg,var(--bg1),var(--bg2));
      -webkit-font-smoothing:antialiased;
    }
    .card{
      background:var(--card);
      padding:3rem 2.5rem;
      border-radius:18px;
      box-shadow:0 10px 30px rgba(0,0,0,0.12);
      text-align:center;
      transform:translateY(10px);
      animation:pop .9s cubic-bezier(.2,.9,.3,1) forwards;
      max-width:880px;
      width:90%;
    }
    h1{
      margin:0 0 .25rem 0;
      font-size:clamp(28px,6vw,56px);
      line-height:1.02;
      letter-spacing:0.2px;
      color:#222;
      display:flex;align-items:center;justify-content:center;gap:.6rem;
    }
    .heart{
      width:56px;height:56px;border-radius:50%;display:inline-grid;place-items:center;
      background:linear-gradient(135deg,var(--accent),#ff9fb1);
      color:white;font-weight:700;font-size:1.2rem;
      box-shadow:0 6px 18px rgba(255,107,129,0.36);
      transform:scale(.9);
      animation:beat 1s infinite ease-in-out .6s;
    }
    p.sub{margin:.5rem 0 0 0;color:#444;font-size:clamp(12px,2.6vw,18px)}
    @keyframes pop{from{opacity:0;transform:translateY(24px) scale(.98)}to{opacity:1;transform:translateY(0) scale(1)}}
    @keyframes beat{0%,100%{transform:scale(.95)}50%{transform:scale(1.08)}}
  </style>
</head>
<body>
  <main class="card" role="main" aria-labelledby="main-title">
    <h1 id="main-title"><span class="heart">❤</span> Eu ti amu, meu amor</h1>
    <p class="sub">Página simples para publicar com HTTPS.</p>
  </main>
</body>
</html>
"""
import os, zipfile, textwrap, pathlib, io

base_dir = "/mnt/data/eu-ti-amu-site"
os.makedirs(base_dir, exist_ok=True)
index_path = os.path.join(base_dir, "index.html")
with open(index_path, "w", encoding="utf-8") as f:
    f.write(html)

zip_path = "/mnt/data/eu-ti-amu-site.zip"
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    z.write(index_path, arcname="index.html")

index_path, zip_path
