(() => {
  'use strict';
  const cv = document.getElementById('game'); const ctx = cv.getContext('2d');
  const W = cv.width, H = cv.height;
  const dpr = Math.max(1, Math.min(3, window.devicePixelRatio || 1));
  cv.width = W * dpr; cv.height = H * dpr; ctx.scale(dpr, dpr);
  const youEl = document.getElementById('you'), cpuEl = document.getElementById('cpu');
  const overlay = document.getElementById('overlay'), ovTitle = document.getElementById('ov-title'), ovSub = document.getElementById('ov-sub');
  const PW = 14, PH = 80, WIN = 7;
  let you, cpu, ball, over, keys;

  function reset() { you = { y: H / 2 - PH / 2 }; cpu = { y: H / 2 - PH / 2 }; ball = { x: W / 2, y: H / 2, vx: 4 * (Math.random() < 0.5 ? -1 : 1), vy: (Math.random() - 0.5) * 4 }; over = false; youEl.textContent = '0'; cpuEl.textContent = '0'; overlay.classList.add('hidden'); }
  function update() {
    if (over) return;
    if (keys['ArrowUp'] || keys['w']) you.y -= 7;
    if (keys['ArrowDown'] || keys['s']) you.y += 7;
    you.y = Math.max(0, Math.min(H - PH, you.y));
    const cpuCenter = cpu.y + PH / 2;
    if (cpuCenter < ball.y - 12) cpu.y += 4.5; else if (cpuCenter > ball.y + 12) cpu.y -= 4.5;
    cpu.y = Math.max(0, Math.min(H - PH, cpu.y));
    ball.x += ball.vx; ball.y += ball.vy;
    if (ball.y < 8) { ball.y = 8; ball.vy *= -1; }
    if (ball.y > H - 8) { ball.y = H - 8; ball.vy *= -1; }
    if (ball.vx < 0 && ball.x < 20 + PW && ball.y > you.y && ball.y < you.y + PH) { ball.x = 20 + PW; ball.vx = Math.abs(ball.vx); ball.vy = ((ball.y - (you.y + PH / 2)) / PH) * 6; speedUp(); }
    if (ball.vx > 0 && ball.x > W - 20 - PW && ball.y > cpu.y && ball.y < cpu.y + PH) { ball.x = W - 20 - PW; ball.vx = -Math.abs(ball.vx); ball.vy = ((ball.y - (cpu.y + PH / 2)) / PH) * 6; speedUp(); }
    if (ball.x < 0) { score('cpu'); }
    if (ball.x > W) { score('you'); }
  }
  function speedUp() { const s = Math.hypot(ball.vx, ball.vy) * 1.04; const m = Math.min(s, 11); ball.vx = ball.vx / Math.hypot(ball.vx, ball.vy) * m; ball.vy = ball.vy / Math.hypot(ball.vx, ball.vy) * m; }
  function score(who) {
    if (who === 'you') youEl.textContent = +youEl.textContent + 1; else cpuEl.textContent = +cpuEl.textContent + 1;
    if (+youEl.textContent >= WIN || +cpuEl.textContent >= WIN) { over = true; ovTitle.textContent = +youEl.textContent >= WIN ? '你赢了！' : '电脑赢了'; ovSub.textContent = youEl.textContent + ' : ' + cpuEl.textContent; overlay.classList.remove('hidden'); return; }
    ball = { x: W / 2, y: H / 2, vx: 4 * (who === 'you' ? 1 : -1), vy: (Math.random() - 0.5) * 4 };
  }
  function draw() {
    ctx.fillStyle = '#1a1c3a'; ctx.fillRect(0, 0, W, H);
    ctx.strokeStyle = 'rgba(255,255,255,0.15)'; ctx.setLineDash([6, 8]); ctx.beginPath(); ctx.moveTo(W / 2, 0); ctx.lineTo(W / 2, H); ctx.stroke(); ctx.setLineDash([]);
    ctx.fillStyle = '#4fd1ff'; ctx.fillRect(20, you.y, PW, PH);
    ctx.fillStyle = '#ff5c7a'; ctx.fillRect(W - 20 - PW, cpu.y, PW, PH);
    ctx.fillStyle = '#fff'; ctx.beginPath(); ctx.arc(ball.x, ball.y, 7, 0, Math.PI * 2); ctx.fill();
  }
  window.addEventListener('keydown', e => { keys[e.key] = true; if (['ArrowUp', 'ArrowDown', 'w', 's'].includes(e.key)) e.preventDefault(); });
  window.addEventListener('keyup', e => { keys[e.key] = false; });
  cv.addEventListener('mousemove', e => { const rect = cv.getBoundingClientRect(); const py = (e.clientY - rect.top) / rect.height * H; you.y = Math.max(0, Math.min(H - PH, py - PH / 2)); });
  cv.addEventListener('touchmove', e => { const t = e.touches[0]; const rect = cv.getBoundingClientRect(); const py = (t.clientY - rect.top) / rect.height * H; you.y = Math.max(0, Math.min(H - PH, py - PH / 2)); }, { passive: true });
  document.getElementById('new').addEventListener('click', reset);
  document.getElementById('ov-btn').addEventListener('click', reset);
  function loop() { update(); draw(); requestAnimationFrame(loop); }
  reset(); requestAnimationFrame(loop);
})();
