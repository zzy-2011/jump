(() => {
  'use strict';
  const cv = document.getElementById('game'); const ctx = cv.getContext('2d');
  const W = cv.width, H = cv.height;
  const dpr = Math.max(1, Math.min(3, window.devicePixelRatio || 1));
  cv.width = W * dpr; cv.height = H * dpr; ctx.scale(dpr, dpr);
  const scoreEl = document.getElementById('score'), bestEl = document.getElementById('best');
  const overlay = document.getElementById('overlay'), ovTitle = document.getElementById('ov-title'), ovSub = document.getElementById('ov-sub');
  const GY = 360, G = 0.8;
  let plats, px, py, vy, vx, onGround, down, power, score, best, over, camX, foot;

  function addPlat() {
    const last = plats[plats.length - 1];
    const gap = 40 + Math.random() * 90, w = 45 + Math.random() * 45;
    plats.push({ x: last.x + last.w + gap, w });
  }
  function reset() {
    plats = [{ x: 80, w: 80 }, { x: 240, w: 70 }, { x: 400, w: 60 }];
    while (plats[plats.length - 1].x < 1200) addPlat();
    px = 120; py = GY; vy = 0; vx = 0; onGround = true; down = false; power = 0; score = 0; over = false; camX = 0; foot = 0;
    scoreEl.textContent = '0'; bestEl.textContent = best || '0'; overlay.classList.add('hidden');
  }
  function launch() {
    if (over || !onGround) return;
    vx = 2 + power * 6; vy = -(7 + power * 7); onGround = false; down = false; power = 0;
  }
  function update() {
    if (over) return;
    if (down && onGround) power = Math.min(1, power + 0.02);
    if (!onGround) {
      vy += G; py += vy; px += vx;
      if (vy > 0 && py >= GY) {
        let hit = null;
        for (let i = 0; i < plats.length; i++) { const p = plats[i]; if (px >= p.x && px <= p.x + p.w) { hit = p; foot = i; break; } }
        if (hit) {
          py = GY; onGround = true; vy = 0; vx = 0;
          const center = hit.x + hit.w / 2;
          if (Math.abs(px - center) < hit.w * 0.25) score += 2; else score += 1;
          scoreEl.textContent = score; if (score > (best || 0)) { best = score; bestEl.textContent = best; }
          while (plats[plats.length - 1].x < px + W) addPlat();
          while (plats.length > 3 && plats[0].x + plats[0].w < camX - 80) plats.shift();
        } else { over = true; ovTitle.textContent = '掉下去了'; ovSub.textContent = '得分 ' + score; overlay.classList.remove('hidden'); }
      }
      if (py > H + 60) { over = true; ovTitle.textContent = '掉下去了'; ovSub.textContent = '得分 ' + score; overlay.classList.remove('hidden'); }
    }
    camX = Math.max(0, px - 120);
  }
  function draw() {
    ctx.fillStyle = '#1a1c3a'; ctx.fillRect(0, 0, W, H);
    for (const p of plats) { const x = p.x - camX; if (x > W || x + p.w < 0) continue; ctx.fillStyle = '#34386e'; ctx.fillRect(x, GY, p.w, H - GY); ctx.fillStyle = '#6c7bff'; ctx.fillRect(x, GY, p.w, 8); }
    const sx = px - camX;
    if (onGround) { ctx.fillStyle = 'rgba(108,123,255,0.5)'; ctx.fillRect(sx - 14, GY - 30 - power * 60, 28, 8 + power * 60); }
    ctx.fillStyle = '#ffd23f'; ctx.beginPath(); ctx.arc(sx, py - 14, 14, 0, Math.PI * 2); ctx.fill();
    ctx.fillStyle = '#10122a'; ctx.beginPath(); ctx.arc(sx, py - 14, 5, 0, Math.PI * 2); ctx.fill();
  }
  function setDown(v) { if (v && onGround && !over) down = true; else if (!v) { if (down) launch(); down = false; } }
  window.addEventListener('keydown', e => { if (e.key === ' ' || e.key === 'ArrowUp') { e.preventDefault(); setDown(true); } });
  window.addEventListener('keyup', e => { if (e.key === ' ' || e.key === 'ArrowUp') setDown(false); });
  cv.addEventListener('mousedown', () => setDown(true));
  window.addEventListener('mouseup', () => setDown(false));
  cv.addEventListener('touchstart', e => { e.preventDefault(); setDown(true); }, { passive: false });
  window.addEventListener('touchend', () => setDown(false));
  document.getElementById('new').addEventListener('click', reset);
  document.getElementById('ov-btn').addEventListener('click', reset);
  function loop() { update(); draw(); requestAnimationFrame(loop); }
  reset(); requestAnimationFrame(loop);
})();
