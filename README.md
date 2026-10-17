<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
<title>EarnHub</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
/* ═══ iOS 26 / Liquid Glass ═══ */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
button, input { font: inherit; color: inherit; background: none; border: none; outline: none; }
button { cursor: pointer; }

:root {
  --bg: #000;
  --text: #fff;
  --text-2: rgba(255,255,255,.65);
  --text-3: rgba(255,255,255,.4);
  --glass: rgba(255,255,255,.055);
  --glass-hi: rgba(255,255,255,.10);
  --glass-bd: rgba(255,255,255,.11);
  --glass-inner: rgba(255,255,255,.18);
  --glass-blur: 28px;
  --glass-sat: 1.9;
  --blue: #0a84ff;
  --indigo: #5e5ce6;
  --purple: #bf5af2;
  --green: #30d158;
  --yellow: #ffd60a;
  --orange: #ff9f0a;
  --red: #ff453a;
  --spring: cubic-bezier(.22, 1, .36, 1);
  --safe-top: env(safe-area-inset-top, 0px);
  --safe-bottom: env(safe-area-inset-bottom, 0px);
}

html, body { height: 100%; }
body {
  font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Inter', 'Segoe UI', Roboto, sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
  -webkit-user-select: none; user-select: none;
  position: relative;
}
body::before {
  content: '';
  position: fixed; inset: -20%;
  background:
    radial-gradient(circle at 20% 15%, rgba(10,132,255,.28), transparent 42%),
    radial-gradient(circle at 85% 20%, rgba(191,90,242,.20), transparent 42%),
    radial-gradient(circle at 50% 100%, rgba(94,92,230,.22), transparent 45%),
    radial-gradient(circle at 10% 85%, rgba(255,55,95,.12), transparent 40%);
  filter: blur(20px);
  z-index: -1;
  animation: floatBg 20s ease-in-out infinite;
  pointer-events: none;
}
@keyframes floatBg {
  0%,100% { transform: translate(0,0) scale(1); }
  33% { transform: translate(2%, -2%) scale(1.05); }
  66% { transform: translate(-2%, 2%) scale(1.02); }
}

.app { max-width: 500px; margin: 0 auto; padding: calc(16px + var(--safe-top)) 16px calc(120px + var(--safe-bottom)); position: relative; }

/* HEADER */
.header { display: flex; justify-content: space-between; align-items: center; padding: 6px 0 22px; animation: slideDown .6s var(--spring) both; }
.user { display: flex; align-items: center; gap: 12px; }
.avatar {
  width: 48px; height: 48px; border-radius: 50%;
  background: linear-gradient(135deg, var(--blue), var(--indigo) 60%, var(--purple));
  display: grid; place-items: center; font-weight: 600; font-size: 19px; color: #fff;
  box-shadow: 0 8px 24px rgba(10,132,255,.35), inset 0 1px 0 rgba(255,255,255,.4);
  border: 1px solid rgba(255,255,255,.2); position: relative; overflow: hidden;
}
.avatar::after { content: ''; position: absolute; inset: 0; background: linear-gradient(180deg, rgba(255,255,255,.25), transparent 50%); border-radius: 50%; pointer-events: none; }
.greeting { font-size: 12px; color: var(--text-3); font-weight: 500; }
.username { font-size: 17px; font-weight: 600; letter-spacing: -.3px; margin-top: 1px; }
.header-actions { display: flex; gap: 8px; }
.icon-btn {
  width: 46px; height: 46px; border-radius: 15px;
  background: var(--glass); backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat));
  border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner), 0 4px 16px rgba(0,0,0,.35);
  font-size: 19px; transition: transform .2s var(--spring), background .2s;
  display: grid; place-items: center; color: var(--text);
}
.icon-btn:active { transform: scale(.9); background: var(--glass-hi); }

/* SF SYMBOL ICONS */
.sf {
  display: inline-block; width: 1em; height: 1em;
  background: currentColor;
  mask-size: contain; mask-repeat: no-repeat; mask-position: center;
  -webkit-mask-size: contain; -webkit-mask-repeat: no-repeat; -webkit-mask-position: center;
}
.sf-house { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><path d='M12 3l9 7v11h-6v-6h-6v6H3V10z'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><path d='M12 3l9 7v11h-6v-6h-6v6H3V10z'/></svg>"); }
.sf-target { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><circle cx='12' cy='12' r='9' fill='none' stroke='black' stroke-width='2'/><circle cx='12' cy='12' r='5' fill='none' stroke='black' stroke-width='2'/><circle cx='12' cy='12' r='1.5'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><circle cx='12' cy='12' r='9' fill='none' stroke='black' stroke-width='2'/><circle cx='12' cy='12' r='5' fill='none' stroke='black' stroke-width='2'/><circle cx='12' cy='12' r='1.5'/></svg>"); }
.sf-bag { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><path d='M6 7h12l1 13H5z'/><path d='M9 7a3 3 0 016 0' fill='none' stroke='black' stroke-width='2'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><path d='M6 7h12l1 13H5z'/><path d='M9 7a3 3 0 016 0' fill='none' stroke='black' stroke-width='2'/></svg>"); }
.sf-game { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><rect x='3' y='8' width='18' height='10' rx='4'/><circle cx='8' cy='13' r='1.5' fill='white'/><circle cx='16' cy='13' r='1.5' fill='white'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><rect x='3' y='8' width='18' height='10' rx='4'/><circle cx='8' cy='13' r='1.5' fill='white'/><circle cx='16' cy='13' r='1.5' fill='white'/></svg>"); }
.sf-person { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><circle cx='12' cy='8' r='4'/><path d='M4 21a8 8 0 0116 0z'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><circle cx='12' cy='8' r='4'/><path d='M4 21a8 8 0 0116 0z'/></svg>"); }
.sf-gear { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><circle cx='12' cy='12' r='3'/><path d='M12 2v3M12 19v3M2 12h3M19 12h3M4.9 4.9l2.1 2.1M17 17l2.1 2.1M19.1 4.9L17 7M7 17l-2.1 2.1' stroke='black' stroke-width='2'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><circle cx='12' cy='12' r='3'/><path d='M12 2v3M12 19v3M2 12h3M19 12h3M4.9 4.9l2.1 2.1M17 17l2.1 2.1M19.1 4.9L17 7M7 17l-2.1 2.1' stroke='black' stroke-width='2'/></svg>"); }
.sf-bell { mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><path d='M6 17V11a6 6 0 1112 0v6l2 2H4z'/><path d='M10 20a2 2 0 004 0' stroke='black' stroke-width='2' fill='none'/></svg>"); -webkit-mask-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black'><path d='M6 17V11a6 6 0 1112 0v6l2 2H4z'/><path d='M10 20a2 2 0 004 0' stroke='black' stroke-width='2' fill='none'/></svg>"); }

/* SCREENS */
.screen { display: none; }
.screen.active { display: block; animation: fadeUp .5s var(--spring) both; }
.screen-title { font-size: 32px; font-weight: 700; letter-spacing: -1px; margin: 6px 0 20px; background: linear-gradient(180deg, #fff 0%, rgba(255,255,255,.75) 100%); -webkit-background-clip: text; background-clip: text; color: transparent; }

/* BALANCE CARD */
.balance-card {
  position: relative; padding: 26px 24px 24px; border-radius: 30px;
  background: linear-gradient(135deg, rgba(10,132,255,.28) 0%, rgba(94,92,230,.22) 50%, rgba(191,90,242,.18) 100%);
  backdrop-filter: blur(32px) saturate(1.9); -webkit-backdrop-filter: blur(32px) saturate(1.9);
  border: 1px solid rgba(255,255,255,.16);
  box-shadow: inset 0 1px 0 rgba(255,255,255,.35), inset 0 -1px 0 rgba(255,255,255,.06), 0 20px 50px rgba(0,0,0,.5), 0 0 0 1px rgba(10,132,255,.1);
  overflow: hidden; isolation: isolate;
}
.balance-card::before { content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%; background: conic-gradient(from 0deg, transparent, rgba(255,255,255,.08), transparent 30%); animation: shine 8s linear infinite; pointer-events: none; }
@keyframes shine { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
.balance-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 22px; position: relative; z-index: 2; }
.balance-label { font-size: 13px; color: rgba(255,255,255,.6); font-weight: 500; }
.balance-value { font-size: 44px; font-weight: 700; letter-spacing: -2px; margin-top: 2px; display: flex; align-items: baseline; gap: 8px; background: linear-gradient(180deg, #fff 0%, rgba(255,255,255,.7) 100%); -webkit-background-clip: text; background-clip: text; color: transparent; }
.balance-value .cur { font-size: 18px; -webkit-text-fill-color: initial; opacity: .8; }
.level-badge { padding: 8px 14px; background: rgba(255,214,10,.12); border: 1px solid rgba(255,214,10,.35); border-radius: 14px; font-size: 11px; font-weight: 700; letter-spacing: .5px; color: var(--yellow); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); box-shadow: inset 0 1px 0 rgba(255,214,10,.25); }
.level-badge span { font-size: 16px; margin-left: 2px; }
.balance-actions { display: flex; gap: 10px; position: relative; z-index: 2; }
  /* BUTTONS */
.btn { padding: 14px 20px; border-radius: 17px; font-size: 15px; font-weight: 600; letter-spacing: -.2px; transition: transform .2s var(--spring), background .2s, box-shadow .2s; position: relative; overflow: hidden; }
.btn:active { transform: scale(.95); }
.btn-primary { background: linear-gradient(180deg, #3d9bff 0%, var(--blue) 50%, #0070e0 100%); color: #fff; box-shadow: inset 0 1px 0 rgba(255,255,255,.4), inset 0 -1px 0 rgba(0,0,0,.15), 0 8px 22px rgba(10,132,255,.45); flex: 1; text-shadow: 0 1px 2px rgba(0,0,0,.2); }
.btn-primary::after { content: ''; position: absolute; inset: 0; background: linear-gradient(180deg, rgba(255,255,255,.15), transparent 60%); pointer-events: none; }
.btn-ghost { background: var(--glass); backdrop-filter: blur(20px) saturate(1.8); -webkit-backdrop-filter: blur(20px) saturate(1.8); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner); color: #fff; flex: 1; }
.btn.big { width: 100%; padding: 16px; margin-top: 18px; font-size: 16px; }
.btn:disabled { opacity: .45; cursor: not-allowed; }

/* QUICK ACTIONS */
.quick-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-top: 18px; }
.quick-card { padding: 14px 8px; background: var(--glass); backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner), 0 4px 16px rgba(0,0,0,.3); border-radius: 20px; text-align: center; cursor: pointer; transition: transform .2s var(--spring), background .2s; }
.quick-card:active { transform: scale(.94); background: var(--glass-hi); }
.quick-icon { font-size: 26px; margin-bottom: 6px; display: block; filter: drop-shadow(0 2px 6px rgba(10,132,255,.3)); }
.quick-title { font-size: 12px; font-weight: 600; }
.quick-sub { font-size: 10px; color: var(--text-3); margin-top: 2px; font-weight: 500; }

/* SECTIONS */
.section { margin-top: 30px; animation: fadeUp .5s var(--spring) both; }
.section-head { display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; }
.section-head h3 { font-size: 20px; font-weight: 700; letter-spacing: -.4px; }
.link { color: var(--blue); font-size: 14px; font-weight: 600; padding: 4px 8px; border-radius: 8px; }
.link:active { background: rgba(10,132,255,.15); }

/* TASKS */
.task { display: flex; align-items: center; gap: 14px; padding: 16px; background: var(--glass); backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner), 0 4px 16px rgba(0,0,0,.3); border-radius: 22px; margin-bottom: 10px; cursor: pointer; transition: transform .25s var(--spring), background .2s; }
.task:active { transform: scale(.98); background: var(--glass-hi); }
.task.done { opacity: .5; pointer-events: none; }
.task.done .task-reward { color: var(--green); background: rgba(48,209,88,.12); border-color: rgba(48,209,88,.3); }
.task.pending { opacity: .8; pointer-events: none; }
.task.pending .task-reward { color: var(--orange); background: rgba(255,159,10,.12); border-color: rgba(255,159,10,.3); }
.task-icon { width: 50px; height: 50px; border-radius: 16px; background: linear-gradient(135deg, rgba(10,132,255,.25), rgba(94,92,230,.25)); border: 1px solid rgba(255,255,255,.08); display: grid; place-items: center; font-size: 23px; flex-shrink: 0; }
.task-info { flex: 1; min-width: 0; }
.task-title { font-size: 15px; font-weight: 600; letter-spacing: -.2px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.task-sub { font-size: 12px; color: var(--text-3); margin-top: 3px; font-weight: 500; }
.task-reward { font-size: 13px; font-weight: 700; color: var(--yellow); padding: 7px 12px; background: rgba(255,214,10,.1); border: 1px solid rgba(255,214,10,.22); border-radius: 11px; white-space: nowrap; }
.task-badge { font-size: 9px; padding: 4px 8px; border-radius: 8px; background: rgba(255,255,255,.06); color: var(--text-3); font-weight: 700; text-transform: uppercase; letter-spacing: .5px; }
.task-badge.manual { background: rgba(255,159,10,.12); color: var(--orange); }

/* PREMIUM BANNER */
.premium-banner { position: relative; display: flex; align-items: center; gap: 16px; padding: 20px; border-radius: 26px; background: linear-gradient(135deg, rgba(255,214,10,.14) 0%, rgba(255,159,10,.08) 50%, rgba(191,90,242,.08) 100%); backdrop-filter: blur(28px) saturate(1.7); -webkit-backdrop-filter: blur(28px) saturate(1.7); border: 1px solid rgba(255,214,10,.22); box-shadow: inset 0 1px 0 rgba(255,214,10,.25), 0 8px 30px rgba(255,159,10,.12); overflow: hidden; }
.premium-banner::before { content: ''; position: absolute; top: 0; left: -100%; width: 100%; height: 100%; background: linear-gradient(90deg, transparent, rgba(255,214,10,.15), transparent); animation: shimmer 3s ease-in-out infinite; pointer-events: none; }
@keyframes shimmer { 0%, 100% { left: -100%; } 50% { left: 100%; } }
.premium-crown { font-size: 42px; filter: drop-shadow(0 0 18px rgba(255,214,10,.55)); position: relative; z-index: 1; }
.premium-info { flex: 1; position: relative; z-index: 1; }
.premium-title { font-size: 17px; font-weight: 700; letter-spacing: -.3px; background: linear-gradient(135deg, var(--yellow), var(--orange)); -webkit-background-clip: text; background-clip: text; color: transparent; }
.premium-sub { font-size: 12px; color: var(--text-3); margin-top: 4px; font-weight: 500; }
.btn-buy { position: relative; z-index: 1; padding: 11px 18px; background: linear-gradient(180deg, #ffdc4a, var(--yellow) 40%, #e0a800); border-radius: 14px; font-weight: 700; font-size: 14px; color: #1a1000; box-shadow: inset 0 1px 0 rgba(255,255,255,.6), 0 6px 18px rgba(255,214,10,.45); transition: transform .2s var(--spring); }
.btn-buy:active { transform: scale(.93); }

/* TABS */
.tabs { display: flex; gap: 8px; margin-bottom: 20px; overflow-x: auto; padding-bottom: 6px; scrollbar-width: none; -ms-overflow-style: none; }
.tabs::-webkit-scrollbar { display: none; }
.tab { padding: 11px 18px; background: var(--glass); backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner); color: var(--text-2); border-radius: 15px; font-size: 14px; font-weight: 600; white-space: nowrap; transition: all .25s var(--spring); }
.tab:active { transform: scale(.96); }
.tab.active { background: linear-gradient(180deg, #3d9bff, var(--blue)); color: #fff; border-color: transparent; box-shadow: inset 0 1px 0 rgba(255,255,255,.4), 0 6px 18px rgba(10,132,255,.45); }

/* SHOP */
.shop-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
.shop-item { padding: 18px 16px; background: var(--glass); backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner), 0 6px 20px rgba(0,0,0,.35); border-radius: 24px; cursor: pointer; transition: transform .25s var(--spring), background .2s; position: relative; overflow: hidden; }
.shop-item:active { transform: scale(.96); background: var(--glass-hi); }
.shop-item.hit { border-color: rgba(255,214,10,.35); background: linear-gradient(135deg, rgba(255,214,10,.1), rgba(10,132,255,.06)); }
.shop-item.hit::after { content: 'ХИТ'; position: absolute; top: 14px; right: -26px; background: linear-gradient(90deg, var(--yellow), var(--orange)); color: #1a1000; font-size: 9px; font-weight: 800; letter-spacing: .5px; padding: 5px 28px; transform: rotate(45deg); box-shadow: 0 2px 8px rgba(255,214,10,.4); }
.shop-icon { font-size: 36px; margin-bottom: 10px; display: block; filter: drop-shadow(0 2px 8px rgba(10,132,255,.3)); }
.shop-title { font-size: 15px; font-weight: 600; letter-spacing: -.2px; }
.shop-sub { font-size: 11px; color: var(--text-3); margin: 3px 0 12px; font-weight: 500; }
.shop-price { display: inline-block; font-size: 13px; font-weight: 700; color: var(--blue); padding: 6px 12px; background: rgba(10,132,255,.12); border: 1px solid rgba(10,132,255,.25); border-radius: 11px; }

/* GAMES */
.game-card { padding: 26px 22px; background: var(--glass); backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(var(--glass-sat)); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner), 0 8px 24px rgba(0,0,0,.35); border-radius: 28px; margin-bottom: 16px; text-align: center; }
.game-title { font-size: 20px; font-weight: 700; letter-spacing: -.3px; }
.game-sub { font-size: 12px; color: var(--text-3); margin-top: 5px; font-weight: 500; }
.wheel-wrap { position: relative; display: inline-block; margin: 24px 0; }
.wheel { width: 190px; height: 190px; border-radius: 50%; background: conic-gradient(#0a84ff 0deg 45deg, #5e5ce6 45deg 90deg, #ffd60a 90deg 135deg, #ff375f 135deg 180deg, #30d158 180deg 225deg, #bf5af2 225deg 270deg, #0a84ff 270deg 315deg, #ff9f0a 315deg 360deg); display: grid; place-items: center; box-shadow: 0 12px 44px rgba(10,132,255,.4), inset 0 0 0 2px rgba(255,255,255,.12), inset 0 0 30px rgba(0,0,0,.35); transition: transform 3.2s var(--spring); border: 7px solid rgba(255,255,255,.09); }
.wheel-center { width: 66px; height: 66px; background: rgba(0,0,0,.65); backdrop-filter: blur(24px); -webkit-backdrop-filter: blur(24px); border-radius: 50%; display: grid; place-items: center; font-size: 28px; border: 2px solid rgba(255,255,255,.18); }
.wheel-pointer { position: absolute; top: -16px; left: 50%; transform: translateX(-50%); font-size: 28px; color: var(--yellow); filter: drop-shadow(0 0 12px var(--yellow)) drop-shadow(0 0 24px rgba(255,214,10,.5)); }
.dice { font-size: 78px; margin: 22px 0; display: inline-block; transition: transform .5s var(--spring); filter: drop-shadow(0 6px 24px rgba(10,132,255,.45)); }

/* PROFILE */
.profile-card { padding: 30px 22px; border-radius: 28px; text-align: center; position: relative; overflow: hidden; background: linear-gradient(135deg, rgba(10,132,255,.16) 0%, rgba(94,92,230,.14) 50%, rgba(191,90,242,.12) 100%); backdrop-filter: blur(32px) saturate(1.9); -webkit-backdrop-filter: blur(32px) saturate(1.9); border: 1px solid rgba(255,255,255,.14); box-shadow: inset 0 1px 0 rgba(255,255,255,.25), 0 12px 36px rgba(0,0,0,.4); }
.profile-avatar { width: 88px; height: 88px; border-radius: 50%; margin: 0 auto 14px; background: linear-gradient(135deg, var(--blue), var(--indigo) 60%, var(--purple)); display: grid; place-items: center; font-size: 36px; font-weight: 600; color: #fff; box-shadow: 0 12px 32px rgba(10,132,255,.45), inset 0 1px 0 rgba(255,255,255,.4); border: 2px solid rgba(255,255,255,.2); position: relative; z-index: 1; }
.profile-name { font-size: 24px; font-weight: 700; letter-spacing: -.5px; position: relative; z-index: 1; }
.profile-id { font-size: 12px; color: var(--text-3); margin-top: 5px; font-weight: 500; position: relative; z-index: 1; }
.profile-stats { display: flex; justify-content: space-around; margin-top: 24px; padding-top: 24px; border-top: 1px solid rgba(255,255,255,.08); position: relative; z-index: 1; }
.profile-stats > div { display: flex; flex-direction: column; gap: 5px; }
.profile-stats b { font-size: 22px; font-weight: 700; letter-spacing: -.5px; }
.profile-stats span { font-size: 11px; color: var(--text-3); font-weight: 500; }
.menu-item { display: flex; align-items: center; gap: 14px; padding: 18px 16px; background: var(--glass); backdrop-filter: blur(20px) saturate(1.8); -webkit-backdrop-filter: blur(20px) saturate(1.8); border: 1px solid var(--glass-bd); box-shadow: inset 0 1px 0 var(--glass-inner); border-radius: 20px; margin-bottom: 10px; font-size: 15px; transition: background .2s, transform .2s var(--spring); }
.menu-item:active { background: var(--glass-hi); transform: scale(.99); }
.menu-item span { flex: 1; font-weight: 500; letter-spacing: -.2px; }
.menu-item b { color: var(--yellow); font-size: 13px; font-weight: 700; }

/* BOTTOM NAV */
.bottom-nav { position: fixed; bottom: calc(16px + var(--safe-bottom)); left: 50%; transform: translateX(-50%); width: calc(100% - 32px); max-width: 460px; display: flex; justify-content: space-around; padding: 7px; background: rgba(18,18,24,.72); backdrop-filter: blur(40px) saturate(1.9); -webkit-backdrop-filter: blur(40px) saturate(1.9); border: 1px solid rgba(255,255,255,.1); border-radius: 28px; box-shadow: inset 0 1px 0 rgba(255,255,255,.15), 0 20px 50px rgba(0,0,0,.65); z-index: 100; }
.nav-item { flex: 1; color: var(--text-3); padding: 10px 0; border-radius: 22px; transition: all .3s var(--spring); position: relative; }
.nav-item .sf { width: 22px; height: 22px; margin: 0 auto; }
.nav-item span { display: block; font-size: 10px; margin-top: 3px; font-weight: 600; letter-spacing: .2px; text-align: center; }
.nav-item.active { color: #fff; background: linear-gradient(180deg, #3d9bff, var(--blue)); box-shadow: inset 0 1px 0 rgba(255,255,255,.4), 0 6px 18px rgba(10,132,255,.5); transform: translateY(-3px); }

/* TOAST */
.toast { position: fixed; top: calc(24px + var(--safe-top)); left: 50%; transform: translateX(-50%) translateY(-140px); padding: 16px 24px; background: rgba(22,22,28,.85); backdrop-filter: blur(40px) saturate(1.9); -webkit-backdrop-filter: blur(40px) saturate(1.9); border: 1px solid rgba(255,255,255,.13); border-radius: 20px; font-size: 14px; font-weight: 600; box-shadow: inset 0 1px 0 rgba(255,255,255,.15), 0 16px 44px rgba(0,0,0,.55); z-index: 999; transition: transform .5s var(--spring); pointer-events: none; white-space: nowrap; max-width: calc(100% - 40px); }
.toast.show { transform: translateX(-50%) translateY(0); }
.toast.success { border-color: rgba(48,209,88,.5); color: var(--green); }
.toast.error { border-color: rgba(255,69,58,.5); color: var(--red); }
.toast.warn { border-color: rgba(255,159,10,.5); color: var(--orange); }

/* MODALS */
.modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,.55); backdrop-filter: blur(24px) saturate(1.6); -webkit-backdrop-filter: blur(24px) saturate(1.6); z-index: 1000; display: none; align-items: flex-end; justify-content: center; padding: 16px; padding-bottom: calc(16px + var(--safe-bottom)); }
.modal-overlay.show { display: flex; animation: fadeIn .3s ease; }
.modal { width: 100%; max-width: 460px; background: rgba(26,26,32,.82); backdrop-filter: blur(44px) saturate(1.9); -webkit-backdrop-filter: blur(44px) saturate(1.9); border: 1px solid rgba(255,255,255,.13); border-radius: 30px; padding: 28px 24px; box-shadow: inset 0 1px 0 rgba(255,255,255,.2), 0 28px 68px rgba(0,0,0,.65); animation: slideUpModal .45s var(--spring); max-height: 90vh; overflow-y: auto; }
.modal-title { font-size: 24px; font-weight: 700; letter-spacing: -.5px; margin-bottom: 8px; }
.modal-sub { font-size: 14px; color: var(--text-3); margin-bottom: 22px; font-weight: 500; }
.modal-input { width: 100%; padding: 16px 18px; background: rgba(255,255,255,.06); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,.1); border-radius: 17px; color: var(--text); font-size: 16px; margin-bottom: 12px; transition: border-color .25s, background .25s; }
.modal-input:focus { border-color: var(--blue); background: rgba(255,255,255,.08); }
.modal-input::placeholder { color: var(--text-3); }
.modal-actions { display: flex; gap: 10px; margin-top: 12px; }
.modal-actions .btn { flex: 1; }
.method-list { display: flex; flex-direction: column; gap: 10px; margin-bottom: 18px; }
.method { display: flex; align-items: center; gap: 14px; padding: 17px; background: rgba(255,255,255,.05); border: 1px solid rgba(255,255,255,.08); border-radius: 18px; transition: all .25s var(--spring); font-size: 15px; font-weight: 600; }
.method:active { transform: scale(.98); }
.method.selected { border-color: var(--blue); background: rgba(10,132,255,.13); box-shadow: 0 4px 16px rgba(10,132,255,.2); }
.method-icon { font-size: 26px; }
.modal-note { font-size: 12px; color: var(--text-3); padding: 14px; background: rgba(255,159,10,.07); border: 1px solid rgba(255,159,10,.18); border-radius: 15px; margin-bottom: 18px; line-height: 1.55; font-weight: 500; }

@keyframes fadeUp { from { opacity: 0; transform: translateY(18px); } to { opacity: 1; transform: translateY(0); } }
@keyframes slideDown { from { opacity: 0; transform: translateY(-18px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes slideUpModal { from { opacity: 0; transform: translateY(60px) scale(.96); } to { opacity: 1; transform: translateY(0) scale(1); } }
</style>
</head>
<body>
<div class="app">
  <header class="header">
    <div class="user">
      <div class="avatar" id="avatar">?</div>
      <div>
        <div class="greeting">Добро пожаловать 👋</div>
        <div class="username" id="username">Гость</div>
      </div>
    </div>
    <div class="header-actions">
      <button class="icon-btn" id="settingsBtn" title="Настройки"><span class="sf sf-gear"></span></button>
      <button class="icon-btn" id="notifBtn" title="Уведомления"><span class="sf sf-bell"></span></button>
    </div>
  </header>

  <main class="screen active" id="screen-home">
    <section class="balance-card">
      <div class="balance-top">
        <div>
          <div class="balance-label">Ваш баланс</div>
          <div class="balance-value"><span class="cur" id="currencySymbol">₽</span><span id="balance">0</span></div>
        </div>
        <div class="level-badge">LVL <span id="level">1</span></div>
      </div>
      <div class="balance-actions">
        <button class="btn btn-primary" id="withdrawBtn">💸 Вывести</button>
        <button class="btn btn-ghost" data-goto="tasks">🎯 Задания</button>
      </div>
    </section>

    <section class="quick-grid">
      <div class="quick-card" data-goto="tasks"><span class="quick-icon">🎯</span><div class="quick-title">Задания</div><div class="quick-sub">+500</div></div>
      <div class="quick-card" data-goto="games"><span class="quick-icon">🎰</span><div class="quick-title">Игры</div><div class="quick-sub">x2</div></div>
      <div class="quick-card" data-goto="shop"><span class="quick-icon">⭐</span><div class="quick-title">Звёзды</div><div class="quick-sub">от 1</div></div>
      <div class="quick-card" data-goto="shop"><span class="quick-icon">👑</span><div class="quick-title">Premium</div><div class="quick-sub">выгодно</div></div>
    </section>

    <section class="section">
      <div class="section-head"><h3>🔥 Топ задания</h3><button class="link" data-goto="tasks">Все →</button></div>
      <div id="homeTasks"></div>
    </section>

    <section class="section">
      <div class="section-head"><h3>👑 Premium TG</h3></div>
      <div class="premium-banner">
        <div class="premium-crown">👑</div>
        <div class="premium-info"><div class="premium-title">Telegram Premium</div><div class="premium-sub">От 199 ₽ / месяц</div></div>
        <button class="btn-buy" data-goto="shop">Купить</button>
      </div>
    </section>
  </main>

  <main class="screen" id="screen-tasks">
    <h2 class="screen-title">🎯 Задания</h2>
    <div class="tabs">
      <button class="tab active" data-filter="all">Все</button>
      <button class="tab" data-filter="auto">🤖 Авто</button>
      <button class="tab" data-filter="manual">👤 Ручные</button>
    </div>
    <div id="tasksList"></div>
  </main>

  <main class="screen" id="screen-shop">
    <h2 class="screen-title">💎 Магазин</h2>
    <div class="tabs" id="shopTabs">
      <button class="tab active" data-shop="stars">⭐ Звёзды</button>
      <button class="tab" data-shop="premium">👑 TG Premium</button>
      <button class="tab" data-shop="brawl">🎮 Brawl Stars</button>
      <button class="tab" data-shop="roblox">🧱 Roblox</button>
      <button class="tab" data-shop="instagram">📸 Instagram</button>
      <button class="tab" data-shop="youtube">🎬 YouTube</button>
      <button class="tab" data-shop="tiktok">🎵 TikTok</button>
    </div>
    <div class="shop-grid" id="shopGrid"></div>
  </main>

  <main class="screen" id="screen-games">
    <h2 class="screen-title">🎰 Игры</h2>
    <div class="game-card">
      <div class="game-title">🎡 Колесо Фортуны</div>
      <div class="game-sub">Крути и выигрывай до x10</div>
      <div class="wheel-wrap"><div class="wheel" id="wheel"><div class="wheel-center">🎯</div></div><div class="wheel-pointer">▼</div></div>
      <button class="btn btn-primary big" id="spinBtn">Крутить за 50</button>
    </div>
    <div class="game-card">
      <div class="game-title">🎲 Кубик удачи</div>
      <div class="game-sub">Ставь и удваивай</div>
      <div class="dice" id="dice">🎲</div>
      <button class="btn btn-primary big" id="diceBtn">Бросить за 100</button>
    </div>
  </main>

  <main class="screen" id="screen-profile">
    <h2 class="screen-title">👤 Профиль</h2>
    <div class="profile-card">
      <div class="profile-avatar" id="profileAvatar">?</div>
      <div class="profile-name" id="profileName">Гость</div>
      <div class="profile-id" id="profileId">ID: —</div>
      <div class="profile-stats">
        <div><b id="statBalance">0</b><span>Баланс</span></div>
        <div><b id="statLevel">1</b><span>Уровень</span></div>
        <div><b id="statRefs">0</b><span>Рефералы</span></div>
      </div>
    </div>
    <div class="section">
      <div class="menu-item" id="dailyBonus">🎁 <span>Ежедневный бонус</span><b>+100</b></div>
      <div class="menu-item" id="inviteBtn">🤝 <span>Пригласить друга</span><b>+300</b></div>
      <div class="menu-item" id="withdrawMenu">💸 <span>Вывести средства</span><b>от 1000</b></div>
      <div class="menu-item" id="historyBtn">📜 <span>История операций</span></div>
      <div class="menu-item" id="supportBtn">💬 <span>Поддержка</span></div>
    </div>
  </main>

  <nav class="bottom-nav">
    <button class="nav-item active" data-screen="home"><span class="sf sf-house"></span><span>Главная</span></button>
    <button class="nav-item" data-screen="tasks"><span class="sf sf-target"></span><span>Задания</span></button>
    <button class="nav-item" data-screen="shop"><span class="sf sf-bag"></span><span>Магазин</span></button>
    <button class="nav-item" data-screen="games"><span class="sf sf-game"></span><span>Игры</span></button>
    <button class="nav-item" data-screen="profile"><span class="sf sf-person"></span><span>Профиль</span></button>
  </nav>
</div>
<div class="modal-overlay" id="withdrawModal">
  <div class="modal">
    <div class="modal-title">💸 Вывод средств</div>
    <div class="modal-sub">Минимальная сумма: 1000</div>
    <div class="modal-note">Заявка уйдёт администратору в бот. Проверка до 24 часов.</div>
    <div class="method-list" id="methodList">
      <div class="method selected" data-method="card"><div class="method-icon">💳</div><div>Банковская карта</div></div>
      <div class="method" data-method="crypto"><div class="method-icon">₿</div><div>Криптовалюта (USDT)</div></div>
      <div class="method" data-method="stars"><div class="method-icon">⭐</div><div>Telegram Stars</div></div>
    </div>
    <input type="number" class="modal-input" id="wdAmount" placeholder="Сумма (от 1000)" min="1000" />
    <input type="text" class="modal-input" id="wdDetails" placeholder="Реквизиты" />
    <div class="modal-actions">
      <button class="btn btn-ghost" id="wdCancel">Отмена</button>
      <button class="btn btn-primary" id="wdSubmit">Отправить</button>
    </div>
  </div>
</div>

<div class="modal-overlay" id="historyModal">
  <div class="modal">
    <div class="modal-title">📜 История операций</div>
    <div class="modal-sub">Последние 20 операций</div>
    <div id="historyList" style="max-height: 400px; overflow-y: auto;"></div>
    <div class="modal-actions" style="margin-top: 16px;"><button class="btn btn-primary" id="histClose">Закрыть</button></div>
  </div>
</div>

<!-- НАСТРОЙКИ -->
<div class="modal-overlay" id="settingsModal">
  <div class="modal">
    <div class="modal-title">⚙️ Настройки</div>
    <div class="modal-sub">Валюта отображения</div>
    <div class="method-list" id="currencyList">
      <div class="method" data-currency="RUB"><div class="method-icon">₽</div><div>Российский рубль</div></div>
      <div class="method" data-currency="USD"><div class="method-icon">$</div><div>Доллар США</div></div>
      <div class="method" data-currency="EUR"><div class="method-icon">€</div><div>Евро</div></div>
      <div class="method" data-currency="GRAM"><div class="method-icon">💎</div><div>Gram (TON)</div></div>
      <div class="method" data-currency="BTC"><div class="method-icon">₿</div><div>Bitcoin (BTC)</div></div>
      <div class="method" data-currency="ETH"><div class="method-icon">Ξ</div><div>Ethereum (ETH)</div></div>
      <div class="method" data-currency="USDT"><div class="method-icon">₮</div><div>Tether (USDT)</div></div>
      <div class="method" data-currency="SOL"><div class="method-icon">◎</div><div>Solana (SOL)</div></div>
      <div class="method" data-currency="TON"><div class="method-icon">💠</div><div>Toncoin (TON)</div></div>
      <div class="method" data-currency="XRP"><div class="method-icon">✕</div><div>XRP</div></div>
      <div class="method" data-currency="BNB"><div class="method-icon">⬡</div><div>BNB</div></div>
      <div class="method" data-currency="DOGE"><div class="method-icon">Ð</div><div>Dogecoin</div></div>
    </div>
    <div class="modal-actions"><button class="btn btn-primary" id="setClose">Готово</button></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const tg = window.Telegram?.WebApp;
if (tg) { tg.ready(); tg.expand(); tg.setHeaderColor('#000000'); tg.setBackgroundColor('#000000'); }
function haptic(s='light'){ try{tg?.HapticFeedback?.impactOccurred(s)}catch(e){} }
function notif(t='success'){ try{tg?.HapticFeedback?.notificationOccurred(t)}catch(e){} }

/* ═══ ВАЛЮТЫ ═══ */
const CURRENCIES = {
  RUB:{symbol:'₽',rate:1}, USD:{symbol:'$',rate:0.011}, EUR:{symbol:'€',rate:0.010},
  GRAM:{symbol:'GRAM',rate:0.15}, BTC:{symbol:'₿',rate:0.00000016}, ETH:{symbol:'Ξ',rate:0.0000033},
  USDT:{symbol:'₮',rate:0.011}, SOL:{symbol:'◎',rate:0.000065}, TON:{symbol:'💠',rate:0.0018},
  XRP:{symbol:'✕',rate:0.016}, BNB:{symbol:'⬡',rate:0.000020}, DOGE:{symbol:'Ð',rate:0.075}
};

const STORAGE_KEY = 'earnhub_state_v3';
let state = JSON.parse(localStorage.getItem(STORAGE_KEY) || 'null') || {
  balance:0, level:1, refs:0, currency:'RUB',
  doneTasks:[], pendingTasks:[], history:[], withdrawals:[]
};
function save(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); }
function fmt(amount){
  const c = CURRENCIES[state.currency];
  const val = amount * c.rate;
  if (state.currency === 'BTC' || state.currency === 'ETH') return val.toFixed(6);
  if (val < 1) return val.toFixed(4);
  return Math.round(val).toLocaleString('ru-RU');
}
function addHistory(text, amount, type='earn'){
  state.history.unshift({text, amount, type, date:new Date().toLocaleString('ru-RU',{day:'2-digit',month:'2-digit',hour:'2-digit',minute:'2-digit'})});
  if (state.history.length>50) state.history = state.history.slice(0,50);
}
function updateBalance(){
  const c = CURRENCIES[state.currency];
  document.getElementById('currencySymbol').textContent = c.symbol;
  document.getElementById('balance').textContent = fmt(state.balance);
  document.getElementById('statBalance').textContent = fmt(state.balance);
  document.getElementById('level').textContent = state.level;
  document.getElementById('statLevel').textContent = state.level;
  document.getElementById('statRefs').textContent = state.refs;
}

const user = tg?.initDataUnsafe?.user;
const userName = user?.first_name || 'Гость';
const userId = user?.id || 'demo';
if (user) {
  const init = userName[0].toUpperCase();
  document.getElementById('username').textContent = userName;
  document.getElementById('avatar').textContent = init;
  document.getElementById('profileAvatar').textContent = init;
  document.getElementById('profileName').textContent = userName;
  document.getElementById('profileId').textContent = 'ID: ' + userId;
}

const toastEl = document.getElementById('toast');
let toastTimer;
function showToast(text, type='success'){
  toastEl.textContent = text; toastEl.className = 'toast show ' + type;
  clearTimeout(toastTimer); toastTimer = setTimeout(()=>{toastEl.className='toast '+type}, 2400);
}

function goTo(screen){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('screen-'+screen)?.classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.toggle('active', n.dataset.screen===screen));
  window.scrollTo({top:0,behavior:'smooth'});
}
document.querySelectorAll('.nav-item').forEach(n=>n.addEventListener('click',()=>{haptic('light');goTo(n.dataset.screen)}));
document.querySelectorAll('[data-goto]').forEach(el=>el.addEventListener('click',()=>{haptic('light');goTo(el.dataset.goto)}));

/* ═══ ЗАДАНИЯ ═══ */
const TASKS = [
  {id:'t1',icon:'📢',title:'Подписка на канал',sub:'Проверка ~30 сек',reward:150,type:'auto',url:'https://t.me/telegram'},
  {id:'t2',icon:'👀',title:'Просмотр поста',sub:'10 секунд',reward:80,type:'auto',url:'https://t.me/telegram'},
  {id:'t3',icon:'🤝',title:'Пригласи друга',sub:'За каждого реферала',reward:300,type:'auto'},
  {id:'t4',icon:'🎮',title:'Установи приложение',sub:'Игра из каталога',reward:500,type:'manual'},
  {id:'t5',icon:'⭐',title:'Оцени бота',sub:'Оставить отзыв',reward:250,type:'manual'},
  {id:'t6',icon:'🎁',title:'Ежедневный бонус',sub:'Раз в 24 часа',reward:100,type:'auto'},
  {id:'t7',icon:'📸',title:'Подписка на Instagram',sub:'Ручная проверка',reward:400,type:'manual'},
  {id:'t8',icon:'🎬',title:'Подписка на YouTube',sub:'Ручная проверка',reward:350,type:'manual'}
];
function renderTask(task, container){
  const isDone = state.doneTasks.includes(task.id);
  const isPending = state.pendingTasks.includes(task.id);
  const el = document.createElement('div');
  el.className = 'task' + (isDone?' done':'') + (isPending?' pending':'');
  el.innerHTML = `
    <div class="task-icon">${task.icon}</div>
    <div class="task-info"><div class="task-title">${task.title}</div><div class="task-sub">${task.sub}</div></div>
    <div style="display:flex;flex-direction:column;gap:6px;align-items:flex-end;">
      <div class="task-reward">${isDone?'✅':isPending?'⏳':'+'+task.reward+' '+CURRENCIES[state.currency].symbol}</div>
      ${task.type==='manual'?'<div class="task-badge manual">Проверка</div>':''}
    </div>`;
  el.addEventListener('click',()=>handleTaskClick(task,el));
  container.appendChild(el);
}
function handleTaskClick(task, el){
  if (state.doneTasks.includes(task.id)) return;
  if (state.pendingTasks.includes(task.id)) { showToast('⏳ Уже на проверке','warn'); return; }
  haptic('medium');
  if (task.type==='auto'){
    tg?.showPopup?.({title:'🎯 '+task.title, message:'Выполнить и получить +'+task.reward+'?',
      buttons:[{id:'yes',type:'default',text:'✅ Выполнить'},{id:'no',type:'cancel',text:'Отмена'}]}, (btnId)=>{
      if (btnId==='yes'){
        if (task.url) tg?.openTelegramLink?.(task.url);
        setTimeout(()=>{
          state.balance += task.reward; state.doneTasks.push(task.id);
          addHistory(task.title, task.reward, 'earn'); checkLevel(); save(); updateBalance();
          el.classList.add('done'); notif('success');
          showToast('+'+task.reward+' '+CURRENCIES[state.currency].symbol+' начислено!','success');
        }, task.url?1500:0);
      }
    });
  } else { showManualTaskModal(task, el); }
}
function showManualTaskModal(task, el){
  const overlay = document.createElement('div');
  overlay.className = 'modal-overlay show';
  overlay.innerHTML = `
    <div class="modal">
      <div class="modal-title">👤 ${task.title}</div>
      <div class="modal-sub">Награда: +${task.reward} ${CURRENCIES[state.currency].symbol}</div>
      <div class="modal-note">Отправьте доказательство. Администратор проверит в течение 24 часов.</div>
      <input type="text" class="modal-input" id="manualProof" placeholder="Ссылка или описание" />
      <input type="text" class="modal-input" id="manualComment" placeholder="Комментарий (необязательно)" />
      <div class="modal-actions">
        <button class="btn btn-ghost" id="mCancel">Отмена</button>
        <button class="btn btn-primary" id="mSend">📤 Отправить</button>
      </div>
    </div>`;
  document.body.appendChild(overlay);
  overlay.querySelector('#mCancel').onclick = () => overlay.remove();
  overlay.querySelector('#mSend').onclick = () => {
    const proof = overlay.querySelector('#manualProof').value.trim();
    if (!proof) { showToast('⚠️ Укажите доказательство','warn'); return; }
    sendToAdmin({type:'manual_task',userId,userName,taskId:task.id,taskTitle:task.title,reward:task.reward,proof,comment:overlay.querySelector('#manualComment').value.trim()});
    state.pendingTasks.push(task.id); save();
    el.classList.add('pending'); el.querySelector('.task-reward').textContent = '⏳';
    overlay.remove(); notif('success'); showToast('📤 Отправлено на проверку!','success');
  };
}
function sendToAdmin(data){ if (tg?.sendData) tg.sendData(JSON.stringify(data)); else console.log('[sendToAdmin]', data); }
function renderAllTasks(){
  const hc = document.getElementById('homeTasks'); const tc = document.getElementById('tasksList');
  hc.innerHTML=''; tc.innerHTML='';
  TASKS.slice(0,3).forEach(t=>renderTask(t,hc));
  TASKS.forEach(t=>renderTask(t,tc));
}
renderAllTasks();
document.querySelectorAll('[data-filter]').forEach(tab=>{
  tab.addEventListener('click',()=>{
    haptic('light');
    document.querySelectorAll('[data-filter]').forEach(t=>t.classList.remove('active'));
    tab.classList.add('active');
    const filter = tab.dataset.filter;
    const tc = document.getElementById('tasksList'); tc.innerHTML='';
    TASKS.filter(t=>filter==='all'||t.type===filter).forEach(t=>renderTask(t,tc));
  });
});

/* ═══ МАГАЗИН ═══ */
const shopItems = {
  stars:[
    {icon:'⭐',title:'50 звёзд',sub:'Быстрая покупка',price:75},
    {icon:'🌟',title:'100 звёзд',sub:'Выгодно',price:149,hit:true},
    {icon:'💫',title:'250 звёзд',sub:'Для подарков',price:349},
    {icon:'✨',title:'500 звёзд',sub:'Максимум',price:649},
    {icon:'🌠',title:'1000 звёзд',sub:'Для блогеров',price:1199,hit:true},
    {icon:'🎇',title:'2500 звёзд',sub:'Для каналов',price:2799}
  ],
  premium:[
    {icon:'👑',title:'Premium 1 мес',sub:'Все функции',price:199,hit:true},
    {icon:'👑',title:'Premium 3 мес',sub:'Скидка 15%',price:499},
    {icon:'👑',title:'Premium 6 мес',sub:'Скидка 25%',price:899},
    {icon:'👑',title:'Premium 12 мес',sub:'Лучшая цена',price:1599,hit:true},
    {icon:'🎁',title:'Premium в подарок',sub:'Другу',price:199},
    {icon:'💎',title:'Premium + 500 ⭐',sub:'Комбо',price:599}
  ],
  brawl:[
    {icon:'🎮',title:'Гемы 30',sub:'Brawl Stars',price:199},
    {icon:'🎮',title:'Гемы 80',sub:'Brawl Stars',price:499,hit:true},
    {icon:'🎮',title:'Гемы 170',sub:'Brawl Stars',price:999},
    {icon:'🎮',title:'Гемы 360',sub:'Brawl Stars',price:1999,hit:true},
    {icon:'🎮',title:'Brawl Pass',sub:'Сезонный пропуск',price:599},
    {icon:'🎮',title:'Brawl Pass Plus',sub:'Все награды',price:999}
  ],
  roblox:[
    {icon:'🧱',title:'Robux 80',sub:'Roblox',price:99},
    {icon:'🧱',title:'Robux 400',sub:'Roblox',price:399,hit:true},
    {icon:'🧱',title:'Robux 800',sub:'Roblox',price:749},
    {icon:'🧱',title:'Robux 1700',sub:'Roblox',price:1499,hit:true},
    {icon:'🧱',title:'Robux 4500',sub:'Roblox',price:3499},
    {icon:'🧱',title:'Premium 1 мес',sub:'Roblox Premium',price:499}
  ],
  instagram:[
    {icon:'📸',title:'Подписчики 100',sub:'Instagram',price:149},
    {icon:'📸',title:'Подписчики 500',sub:'Instagram',price:599,hit:true},
    {icon:'📸',title:'Подписчики 1000',sub:'Instagram',price:999},
    {icon:'📸',title:'Лайки 100',sub:'Instagram',price:99},
    {icon:'📸',title:'Лайки 500',sub:'Instagram',price:349,hit:true},
    {icon:'📸',title:'Просмотры 10K',sub:'Instagram Reels',price:299}
  ],
  youtube:[
    {icon:'🎬',title:'Подписчики 100',sub:'YouTube',price:199},
    {icon:'🎬',title:'Подписчики 500',sub:'YouTube',price:799,hit:true},
    {icon:'🎬',title:'Подписчики 1000',sub:'YouTube',price:1499},
    {icon:'🎬',title:'Просмотры 1000',sub:'YouTube',price:149},
    {icon:'🎬',title:'Просмотры 10K',sub:'YouTube',price:999,hit:true},
    {icon:'🎬',title:'Лайки 500',sub:'YouTube',price:299}
  ],
  tiktok:[
    {icon:'🎵',title:'Подписчики 100',sub:'TikTok',price:149},
    {icon:'🎵',title:'Подписчики 500',sub:'TikTok',price:549,hit:true},
    {icon:'🎵',title:'Подписчики 1000',sub:'TikTok',price:999},
    {icon:'🎵',title:'Лайки 100',sub:'TikTok',price:99},
    {icon:'🎵',title:'Лайки 500',sub:'TikTok',price:349,hit:true},
    {icon:'🎵',title:'Просмотры 10K',sub:'TikTok',price:199}
  ]
};
function renderShop(category='stars'){
  const grid = document.getElementById('shopGrid'); grid.innerHTML='';
  shopItems[category].forEach(item=>{
    const el = document.createElement('div');
    el.className = 'shop-item' + (item.hit?' hit':'');
    el.innerHTML = `
      <div class="shop-icon">${item.icon}</div>
      <div class="shop-title">${item.title}</div>
      <div class="shop-sub">${item.sub}</div>
      <div class="shop-price">${item.price} ${CURRENCIES[state.currency].symbol}</div>`;
    el.addEventListener('click',()=>{
      haptic('medium');
      tg?.showPopup?.({title:item.title, message:'Купить за '+item.price+' '+CURRENCIES[state.currency].symbol+'?',
        buttons:[{id:'buy',type:'default',text:'💳 Купить'},{id:'cancel',type:'cancel',text:'Отмена'}]},(id)=>{
        if (id==='buy'){ sendToAdmin({type:'purchase',userId,userName,item:item.title,price:item.price}); notif('success'); showToast('✅ Заявка отправлена!','success'); }
      });
    });
    grid.appendChild(el);
  });
}
renderShop('stars');
document.querySelectorAll('[data-shop]').forEach(tab=>{
  tab.addEventListener('click',()=>{
    haptic('light');
    document.querySelectorAll('[data-shop]').forEach(t=>t.classList.remove('active'));
    tab.classList.add('active'); renderShop(tab.dataset.shop);
  });
});

/* ═══ ИГРЫ ═══ */
let wheelRotation = 0;
const spinBtn = document.getElementById('spinBtn'); const wheel = document.getElementById('wheel');
spinBtn.addEventListener('click',()=>{
  if (state.balance<50){notif('error');showToast('Недостаточно средств','error');return;}
  haptic('heavy'); state.balance-=50; addHistory('Крутка колеса',-50,'spend'); updateBalance(); save();
  const prizes=[0,10,25,50,75,100,150,500]; const prize=prizes[Math.floor(Math.random()*prizes.length)];
  wheelRotation += 360*5 + Math.random()*360; wheel.style.transform = `rotate(${wheelRotation}deg)`; spinBtn.disabled=true;
  setTimeout(()=>{
    state.balance+=prize; if(prize>0) addHistory('Выигрыш в колесе',prize,'earn');
    updateBalance(); save(); notif(prize>0?'success':'error');
    showToast(prize>0?`🎉 +${prize} ${CURRENCIES[state.currency].symbol}`:'😢 Пусто', prize>0?'success':'error');
    spinBtn.disabled=false;
  },3200);
});
const diceBtn = document.getElementById('diceBtn'); const diceEl = document.getElementById('dice');
const diceFaces=['⚀','⚁','⚂','⚃','⚄','⚅'];
diceBtn.addEventListener('click',()=>{
  if(state.balance<100){notif('error');showToast('Недостаточно средств','error');return;}
  haptic('heavy'); state.balance-=100; addHistory('Ставка в кубике',-100,'spend'); updateBalance(); save(); diceBtn.disabled=true;
  let rolls=0;
  const interval = setInterval(()=>{
    diceEl.textContent = diceFaces[Math.floor(Math.random()*6)];
    diceEl.style.transform = `rotate(${Math.random()*360}deg) scale(${1+Math.random()*0.3})`;
    rolls++;
    if(rolls>12){
      clearInterval(interval);
      const value = Math.floor(Math.random()*6)+1; diceEl.textContent = diceFaces[value-1];
      const win = value>=4; const prize = win?200:0;
      state.balance+=prize; if(win) addHistory('Победа в кубике',prize,'earn');
      updateBalance(); save(); notif(win?'success':'error');
      showToast(win?`🎉 Выпало ${value} — +200`:`😢 Выпало ${value}`, win?'success':'error');
      diceBtn.disabled=false;
    }
  },100);
});

/* ═══ ПРОФИЛЬ ═══ */
document.getElementById('dailyBonus').addEventListener('click',()=>{
  const last = parseInt(localStorage.getItem('lastBonus')||'0',10);
  if(Date.now()-last < 24*60*60*1000){notif('error');showToast('⏳ Бонус раз в 24 часа','error');return;}
  haptic('heavy'); localStorage.setItem('lastBonus', Date.now());
  state.balance+=100; addHistory('Ежедневный бонус',100,'earn'); checkLevel(); save(); updateBalance();
  notif('success'); showToast('🎁 +100 получено!','success');
});
document.getElementById('inviteBtn').addEventListener('click',()=>{
  haptic('medium');
  const link = 'https://t.me/share/url?url=' + encodeURIComponent('https://t.me/YourBot?start='+userId);
  tg?.openTelegramLink?.(link) || window.open(link,'_blank');
  showToast('🔗 Ссылка готова','success');
});
function checkLevel(){
  const newLevel = Math.floor(state.balance/1000)+1;
  if(newLevel>state.level){ state.level=newLevel; showToast(`🎉 Новый уровень: ${newLevel}!`,'success'); }
}

/* ═══ ВЫВОД ═══ */
const withdrawModal = document.getElementById('withdrawModal');
let selectedMethod = 'card';
function openWithdraw(){
  haptic('medium');
  if(state.balance<1000){showToast('⚠️ Минимум 1000','warn');return;}
  withdrawModal.classList.add('show');
}
document.getElementById('withdrawBtn').addEventListener('click',openWithdraw);
document.getElementById('withdrawMenu').addEventListener('click',openWithdraw);
document.getElementById('wdCancel').addEventListener('click',()=>withdrawModal.classList.remove('show'));
document.querySelectorAll('.method').forEach(m=>{
  m.addEventListener('click',()=>{
    haptic('light');
    document.querySelectorAll('.method').forEach(x=>x.classList.remove('selected'));
    m.classList.add('selected'); selectedMethod = m.dataset.method;
  });
});
document.getElementById('wdSubmit').addEventListener('click',()=>{
  const amount = parseInt(document.getElementById('wdAmount').value,10);
  const details = document.getElementById('wdDetails').value.trim();
  if(!amount||amount<1000){showToast('⚠️ Минимум 1000','warn');return;}
  if(amount>state.balance){showToast('⚠️ Недостаточно средств','warn');return;}
  if(!details){showToast('⚠️ Укажите реквизиты','warn');return;}
  haptic('heavy');
  sendToAdmin({type:'withdraw',userId,userName,amount,method:selectedMethod,details});
  state.balance-=amount; state.withdrawals.push({amount,method:selectedMethod,details,status:'pending',date:Date.now()});
  addHistory('Заявка на вывод',-amount,'withdraw'); save(); updateBalance();
  withdrawModal.classList.remove('show');
  document.getElementById('wdAmount').value=''; document.getElementById('wdDetails').value='';
  notif('success'); showToast('📤 Заявка отправлена!','success');
});

/* ═══ ИСТОРИЯ ═══ */
const historyModal = document.getElementById('historyModal');
document.getElementById('historyBtn').addEventListener('click',()=>{
  haptic('light');
  const list = document.getElementById('historyList'); list.innerHTML='';
  if(state.history.length===0){ list.innerHTML = '<div style="text-align:center;color:var(--text-3);padding:30px 0;">Пока пусто</div>'; }
  else {
    state.history.forEach(h=>{
      const el = document.createElement('div');
      el.style.cssText = 'display:flex;justify-content:space-between;align-items:center;padding:14px;background:rgba(255,255,255,.05);border-radius:14px;margin-bottom:8px;border:1px solid rgba(255,255,255,.06);';
      const color = h.type==='earn'?'var(--green)':h.type==='spend'?'var(--red)':'var(--orange)';
      const sign = h.amount>0?'+':'';
      el.innerHTML = `
        <div><div style="font-size:14px;font-weight:600;">${h.text}</div><div style="font-size:11px;color:var(--text-3);margin-top:3px;">${h.date}</div></div>
        <div style="font-weight:800;color:${color};">${sign}${h.amount} ${CURRENCIES[state.currency].symbol}</div>`;
      list.appendChild(el);
    });
  }
  historyModal.classList.add('show');
});
document.getElementById('histClose').addEventListener('click',()=>historyModal.classList.remove('show'));

/* ═══ НАСТРОЙКИ / ВАЛЮТА ═══ */
const settingsModal = document.getElementById('settingsModal');
document.getElementById('settingsBtn').addEventListener('click',()=>{
  haptic('light');
  document.querySelectorAll('#currencyList .method').forEach(m=>{
    m.classList.toggle('selected', m.dataset.currency === state.currency);
  });
  settingsModal.classList.add('show');
});
document.getElementById('setClose').addEventListener('click',()=>settingsModal.classList.remove('show'));
document.querySelectorAll('#currencyList .method').forEach(m=>{
  m.addEventListener('click',()=>{
    haptic('medium');
    document.querySelectorAll('#currencyList .method').forEach(x=>x.classList.remove('selected'));
    m.classList.add('selected');
    state.currency = m.dataset.currency; save(); updateBalance();
    showToast(`✅ Валюта: ${CURRENCIES[state.currency].symbol}`,'success');
    setTimeout(()=>settingsModal.classList.remove('show'), 400);
  });
});

/* ═══ УВЕДОМЛЕНИЯ ═══ */
document.getElementById('notifBtn').addEventListener('click',()=>{ haptic('light'); showToast('🔔 Новых уведомлений нет','success'); });

/* ═══ MAIN BUTTON ═══ */
if (tg?.MainButton) {
  tg.MainButton.setText('🚀 ЗАРАБОТАТЬ'); tg.MainButton.color = '#0a84ff'; tg.MainButton.textColor = '#ffffff';
  tg.MainButton.show(); tg.MainButton.onClick(()=>{ haptic('heavy'); goTo('tasks'); });
}

updateBalance();
</script>
</body>
  </html>
