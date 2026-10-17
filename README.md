from pathlib import Path
import shutil, zipfile

root = Path("/mnt/data/birthday_site_final")
if root.exists():
    shutil.rmtree(root)
root.mkdir()

# Uploaded photos (exact mounted paths supplied for this turn)
photos = [
    Path("/mnt/data/29611.jpg"),
    Path("/mnt/data/29612.jpg"),
    Path("/mnt/data/20621.webp"),
    Path("/mnt/data/21652.jpg"),
    Path("/mnt/data/20374.jpg"),
    Path("/mnt/data/20369.jpg"),
    Path("/mnt/data/20370.jpg"),
]

photo_names = []
for i, src in enumerate(photos, 1):
    ext = src.suffix.lower()
    name = f"photo{i}{ext}"
    shutil.copy2(src, root / name)
    photo_names.append(name)

html = r'''<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For My LOML ♡</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&family=Playfair+Display:wght@500;600&display=swap');
*{box-sizing:border-box}html,body{margin:0;min-height:100%;font-family:'DM Sans',sans-serif;background:#fdf8f5;color:#30282a}
body{overflow-x:hidden}.page{min-height:100vh;display:none;align-items:center;justify-content:center;padding:28px 18px 70px;position:relative;overflow:hidden}
.page.active{display:flex;animation:fade .65s ease}@keyframes fade{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:none}}
.card{width:min(900px,100%);text-align:center}.eyebrow{letter-spacing:4px;text-transform:uppercase;font-size:11px;color:#9b747a}
.h1{font-family:'Playfair Display',serif;font-size:clamp(42px,12vw,78px);line-height:.98;margin:12px 0}
.sub{font-size:15px;line-height:1.7;color:#796b6e;max-width:560px;margin:auto}
.btn{border:0;background:#342b2e;color:#fff;padding:14px 24px;border-radius:999px;font-weight:700;cursor:pointer;box-shadow:0 10px 25px #342b2e18;margin-top:24px}
.btn.light{background:#fff;color:#342b2e;border:1px solid #eaded9}
.dotbar{position:fixed;bottom:17px;left:50%;transform:translateX(-50%);display:flex;gap:7px;z-index:10}
.dot{width:7px;height:7px;border-radius:50%;background:#d7c7c8}.dot.on{background:#80656b;width:19px;border-radius:10px}
.album{display:grid;grid-template-columns:repeat(2,1fr);gap:13px;margin:28px auto;max-width:680px}
.photo{aspect-ratio:4/5;border-radius:22px;overflow:hidden;background:#eee;position:relative;border:7px solid #fff;box-shadow:0 14px 35px #49363816}
.photo img{width:100%;height:100%;object-fit:cover;display:block}
.photo:after{content:'♡';position:absolute;top:8px;right:12px;font-size:24px;color:#fff;text-shadow:0 2px 7px #0008}
.photo.wide{grid-column:span 2;aspect-ratio:16/9}
.letter{background:#fffaf8;border:1px solid #eee1dc;border-radius:28px;padding:35px 25px;text-align:left;box-shadow:0 20px 50px #49363810;max-width:680px;margin:25px auto}
.letter h2{text-align:center;font-family:'Playfair Display',serif;font-size:30px;margin-top:0}
.letter p{line-height:1.9;color:#66585b;font-size:15px}.signature{text-align:right;font-family:'Playfair Display',serif;font-size:22px;color:#80656b}
.cake{font-size:92px;filter:drop-shadow(0 14px 18px #8b666622);animation:bob 2.5s ease-in-out infinite}@keyframes bob{50%{transform:translateY(-8px) rotate(2deg)}}
.big-heart{font-size:88px;animation:beat 1.3s infinite}@keyframes beat{50%{transform:scale(1.08)}}
.confetti{position:fixed;inset:0;pointer-events:none;overflow:hidden;z-index:20}.confetti i{position:absolute;top:-20px;width:7px;height:13px;border-radius:3px;animation:fall 3.2s linear forwards}
@keyframes fall{to{transform:translateY(110vh) rotate(720deg);opacity:.1}}
@media(max-width:600px){.album{gap:9px}.photo{border-width:5px;border-radius:17px}.letter{padding:28px 20px}}
</style>
</head>
<body>

<section class="page active" id="p1"><div class="card">
<div class="eyebrow">a tiny website made just for you ♡</div>
<div class="h1">Hey, LOML.</div>
<p class="sub">I made you a little corner of the internet because an ordinary birthday wish just wasn't enough. 🎀</p>
<button class="btn" onclick="go(2)">open your surprise →</button>
</div></section>

<section class="page" id="p2"><div class="card">
<div class="cake">🎂</div><div class="eyebrow">today is your day</div>
<div class="h1">Happy Birthday ♡</div>
<p class="sub">May this new chapter bring you soft days, genuine smiles, beautiful memories and everything your heart quietly wishes for.</p>
<button class="btn" onclick="burst();go(3)">there's more →</button>
</div></section>

<section class="page" id="p3"><div class="card">
<div class="eyebrow">our little album</div>
<div class="h1" style="font-size:clamp(34px,9vw,58px)">Pretty little memories</div>
<p class="sub">A tiny collection of your beautiful moments, because one picture could never be enough. 📸♡</p>
<div class="album">
<div class="photo"><img src="photo1.jpg" alt="memory 1"></div>
<div class="photo"><img src="photo2.jpg" alt="memory 2"></div>
<div class="photo"><img src="photo3.webp" alt="memory 3"></div>
<div class="photo"><img src="photo4.jpg" alt="memory 4"></div>
<div class="photo wide"><img src="photo5.jpg" alt="memory 5"></div>
<div class="photo"><img src="photo6.jpg" alt="memory 6"></div>
<div class="photo"><img src="photo7.jpg" alt="memory 7"></div>
</div>
<button class="btn" onclick="go(4)">read this →</button>
</div></section>

<section class="page" id="p4"><div class="card">
<div class="eyebrow">a letter for you</div>
<div class="letter">
<h2>To my LOML,</h2>
<p>Happy birthday to one of the sweetest people in my life. ♡ I'm genuinely grateful that our paths crossed. Even through a screen, you've become someone whose presence can make an ordinary day feel a little brighter.</p>
<p>I hope you never forget how loved, appreciated and special you are. Keep choosing yourself, keep chasing the things that make you happy, and please never stop being the person you are.</p>
<p>Here's to another year of memories, late conversations, random laughs, little wins and dreams coming true. I hope life is extra gentle with you this year. You deserve so many beautiful things. 🫶🏻</p>
<div class="signature">with lots of love ♡</div>
</div>
<button class="btn" onclick="burst();go(5)">one last thing →</button>
</div></section>

<section class="page" id="p5"><div class="card">
<div class="big-heart">♡</div><div class="h1" style="font-size:clamp(38px,11vw,70px)">Stay happy.</div>
<p class="sub">And whenever you look back at this little page, I hope it reminds you that someone was really, really happy that you exist.</p>
<button class="btn light" onclick="go(1)">start again ↺</button>
</div></section>

<div class="dotbar"><span class="dot on" id="d1"></span><span class="dot" id="d2"></span><span class="dot" id="d3"></span><span class="dot" id="d4"></span><span class="dot" id="d5"></span></div>

<script>
let current=1;
function go(n){document.getElementById('p'+current).classList.remove('active');current=n;document.getElementById('p'+current).classList.add('active');for(let i=1;i<=5;i++)document.getElementById('d'+i).classList.toggle('on',i===current);window.scrollTo({top:0,behavior:'smooth'})}
function burst(){const box=document.createElement('div');box.className='confetti';const chars=['♡','✦','•','✿'];for(let i=0;i<55;i++){const x=document.createElement('i');x.textContent=chars[Math.floor(Math.random()*chars.length)];x.style.left=Math.random()*100+'%';x.style.animationDelay=Math.random()*.5+'s';x.style.fontSize=(10+Math.random()*12)+'px';box.appendChild(x)}document.body.appendChild(box);setTimeout(()=>box.remove(),3600)}
</script>
</body>
</html>'''

(root/"index.html").write_text(html, encoding="utf-8")
(root/"README.txt").write_text(
    "Your finished birthday website. Open index.html to preview. Keep all photo files in the same folder as index.html.\n",
    encoding="utf-8"
)

zip_path = Path("/mnt/data/LOML_Birthday_Website_FINAL.zip")
if zip_path.exists():
    zip_path.unlink()
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for p in root.iterdir():
        z.write(p, p.name)

print(f"FINAL VERSION READY:\n{zip_path}")
