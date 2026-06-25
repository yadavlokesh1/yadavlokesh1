<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Lokesh Yadav — README Header</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: #0d1117; }

  .header-wrap {
    width: 100%;
    background: #0d1117;
    overflow: hidden;
    position: relative;
    min-height: 220px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  canvas#net {
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
  }
  .header-content {
    position: relative;
    z-index: 2;
    text-align: center;
    padding: 36px 24px 28px;
  }
  .header-name {
    font-family: 'Segoe UI', system-ui, sans-serif;
    font-size: 42px;
    font-weight: 700;
    color: #ffffff;
    letter-spacing: 4px;
    margin: 0 0 6px;
    text-transform: uppercase;
  }
  .header-role {
    font-family: 'Segoe UI', system-ui, sans-serif;
    font-size: 12px;
    color: #58a6ff;
    letter-spacing: 3px;
    text-transform: uppercase;
    margin: 0 0 20px;
  }
  .header-divider {
    width: 60px;
    height: 2px;
    background: #58a6ff;
    margin: 0 auto 20px;
    border-radius: 2px;
  }
  .header-icons {
    display: flex;
    gap: 20px;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
  }
  .icon-pill {
    display: flex;
    align-items: center;
    gap: 7px;
    background: rgba(31,111,235,0.12);
    border: 1px solid rgba(88,166,255,0.2);
    border-radius: 20px;
    padding: 5px 14px 5px 10px;
    color: #c9d1d9;
    font-family: 'Segoe UI', system-ui, sans-serif;
    font-size: 12px;
    letter-spacing: 0.04em;
  }
  .icon-pill img {
    width: 18px;
    height: 18px;
  }
</style>
</head>
<body>

<div class="header-wrap">
  <canvas id="net"></canvas>
  <div class="header-content">
    <div class="header-name">Lokesh Yadav</div>
    <div class="header-role">Sysadmin · Cloud · Automation</div>
    <div class="header-divider"></div>
    <div class="header-icons">
      <div class="icon-pill">
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/azure/azure-original.svg"/>
        Azure
      </div>
      <div class="icon-pill">
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/powershell/powershell-original.svg"/>
        PowerShell
      </div>
      <div class="icon-pill">
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/terraform/terraform-original.svg"/>
        Terraform
      </div>
      <div class="icon-pill">
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-plain-wordmark.svg"/>
        AWS
      </div>
    </div>
  </div>
</div>

<script>
const canvas = document.getElementById('net');
const ctx = canvas.getContext('2d');
const wrap = canvas.parentElement;

let W, H, dots;

function resize() {
  W = canvas.width = wrap.offsetWidth;
  H = canvas.height = wrap.offsetHeight;
  initDots();
}

function initDots() {
  dots = Array.from({length: 55}, () => ({
    x: Math.random() * W,
    y: Math.random() * H,
    vx: (Math.random() - 0.5) * 0.6,
    vy: (Math.random() - 0.5) * 0.6,
    r: Math.random() * 1.8 + 1
  }));
}

function draw() {
  ctx.clearRect(0, 0, W, H);

  dots.forEach(d => {
    d.x += d.vx;
    d.y += d.vy;
    if (d.x < 0 || d.x > W) d.vx *= -1;
    if (d.y < 0 || d.y > H) d.vy *= -1;
  });

  for (let i = 0; i < dots.length; i++) {
    for (let j = i + 1; j < dots.length; j++) {
      const dx = dots[i].x - dots[j].x;
      const dy = dots[i].y - dots[j].y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if (dist < 110) {
        ctx.beginPath();
        ctx.strokeStyle = `rgba(88,166,255,${(1 - dist/110) * 0.35})`;
        ctx.lineWidth = 0.8;
        ctx.moveTo(dots[i].x, dots[i].y);
        ctx.lineTo(dots[j].x, dots[j].y);
        ctx.stroke();
      }
    }
  }

  dots.forEach(d => {
    ctx.beginPath();
    ctx.arc(d.x, d.y, d.r, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(88,166,255,0.7)';
    ctx.fill();
  });

  requestAnimationFrame(draw);
}

resize();
window.addEventListener('resize', resize);
draw();
</script>

</body>
</html>
