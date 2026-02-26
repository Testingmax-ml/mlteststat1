
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nexus Stats — MOBA Tracker</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&family=DM+Mono:wght@400;500&family=Sora:wght@600;700;800&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f5f5f4;--surface:#fff;--surface2:#fafaf9;--border:#e7e5e4;--border2:#d6d3d1;
  --text:#1c1917;--text2:#78716c;--text3:#a8a29e;
  --accent:#2563eb;--accent-h:#1d4ed8;--accent-l:#eff6ff;
  --win:#16a34a;--win-l:#f0fdf4;--loss:#dc2626;--loss-l:#fef2f2;
  --gold:#d97706;--gold-l:#fffbeb;
  --r:12px;--r-sm:8px;--r-xs:6px;
  --shadow:0 1px 3px rgba(0,0,0,.07),0 1px 2px rgba(0,0,0,.04);
  --shadow-md:0 4px 16px rgba(0,0,0,.08),0 2px 4px rgba(0,0,0,.04);
  --shadow-lg:0 10px 40px rgba(0,0,0,.12),0 4px 8px rgba(0,0,0,.06);
}
html{scroll-behavior:smooth}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;font-size:14px;line-height:1.5}
a{text-decoration:none;color:inherit}
button{cursor:pointer;font-family:inherit}
input,textarea,select{font-family:inherit}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:10px}

/* ── LAYOUT ── */
.layout{display:flex;min-height:100vh}
.sidebar{width:224px;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;position:fixed;top:0;bottom:0;left:0;z-index:100;overflow-y:auto}
.main{margin-left:224px;flex:1;display:flex;flex-direction:column;min-width:0}

/* ── SIDEBAR ── */
.sidebar-top{padding:20px 20px 16px;border-bottom:1px solid var(--border)}
.logo{font-family:'Sora',sans-serif;font-size:19px;font-weight:800;color:var(--text);letter-spacing:-.5px;display:flex;align-items:center;gap:6px}
.logo-dot{width:8px;height:8px;border-radius:50%;background:var(--accent);flex-shrink:0}
.logo-sub{font-size:11px;color:var(--text3);font-weight:400;margin-top:1px;letter-spacing:.02em}
.nav-body{padding:12px;flex:1}
.nav-group{margin-bottom:20px}
.nav-group-label{font-size:10px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--text3);padding:0 8px;margin-bottom:4px}
.nav-item{display:flex;align-items:center;gap:10px;padding:8px 10px;border-radius:var(--r-sm);color:var(--text2);font-weight:500;font-size:13.5px;cursor:pointer;transition:all .15s;margin-bottom:2px;user-select:none}
.nav-item:hover{background:var(--bg);color:var(--text)}
.nav-item.active{background:var(--accent-l);color:var(--accent);font-weight:600}
.nav-icon{font-size:15px;width:18px;text-align:center;flex-shrink:0}
.nav-badge{margin-left:auto;background:var(--accent);color:#fff;font-size:10px;font-weight:700;padding:1px 6px;border-radius:100px}
.sidebar-footer{padding:14px 12px;border-top:1px solid var(--border)}
.user-tile{display:flex;align-items:center;gap:10px;padding:8px;border-radius:var(--r-sm);cursor:pointer;transition:background .15s}
.user-tile:hover{background:var(--bg)}
.u-av{width:34px;height:34px;border-radius:50%;background:linear-gradient(135deg,#bfdbfe,#60a5fa);display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0;border:2px solid var(--surface);box-shadow:0 0 0 1.5px var(--border2)}
.u-name{font-weight:600;font-size:13px}
.u-meta{font-size:11px;color:var(--text3)}

/* ── TOPBAR ── */
.topbar{background:var(--surface);border-bottom:1px solid var(--border);padding:0 28px;height:58px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:50}
.page-heading{font-family:'Sora',sans-serif;font-size:15px;font-weight:700;letter-spacing:-.3px}
.topbar-right{display:flex;align-items:center;gap:10px}
.search-wrap{display:flex;align-items:center;gap:8px;background:var(--bg);border:1px solid var(--border2);border-radius:var(--r-sm);padding:7px 12px;transition:border-color .15s}
.search-wrap:focus-within{border-color:var(--accent);background:var(--surface)}
.search-wrap input{background:none;border:none;outline:none;font-size:13px;color:var(--text);width:160px}
.search-wrap input::placeholder{color:var(--text3)}

/* ── BUTTONS ── */
.btn{display:inline-flex;align-items:center;gap:6px;padding:7px 14px;border-radius:var(--r-sm);font-size:13px;font-weight:500;border:none;transition:all .15s;white-space:nowrap;cursor:pointer}
.btn-primary{background:var(--accent);color:#fff}
.btn-primary:hover{background:var(--accent-h)}
.btn-ghost{background:none;border:1px solid var(--border2);color:var(--text2)}
.btn-ghost:hover{background:var(--bg);color:var(--text)}
.btn-danger{background:none;border:1px solid #fecaca;color:var(--loss)}
.btn-danger:hover{background:var(--loss-l)}
.btn-sm{padding:5px 11px;font-size:12px}
.btn-lg{padding:10px 22px;font-size:14px;font-weight:600}
.btn-full{width:100%;justify-content:center}
.btn-win{background:var(--win);color:#fff}
.btn-win:hover{background:#15803d}

/* ── PAGE ── */
.page{display:none;padding:24px 28px 48px;animation:fadeUp .3s ease both}
.page.active{display:block}
@keyframes fadeUp{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}

/* ── CARDS ── */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);box-shadow:var(--shadow);overflow:hidden}
.card-hover{transition:box-shadow .2s,transform .2s}
.card-hover:hover{box-shadow:var(--shadow-md);transform:translateY(-1px)}
.card-header{padding:14px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:12px}
.card-title{font-size:13.5px;font-weight:600}
.card-sub{font-size:12px;color:var(--text3)}

/* ── BADGES ── */
.badge{display:inline-flex;align-items:center;gap:3px;padding:2px 7px;border-radius:100px;font-size:11px;font-weight:600}
.b-win{background:var(--win-l);color:var(--win)}
.b-loss{background:var(--loss-l);color:var(--loss)}
.b-gold{background:var(--gold-l);color:var(--gold)}
.b-blue{background:var(--accent-l);color:var(--accent)}
.b-gray{background:var(--bg);color:var(--text2);border:1px solid var(--border)}

/* ── WR PILL ── */
.wr{display:inline-flex;align-items:center;border-radius:100px;padding:3px 10px;font-family:'DM Mono',monospace;font-size:12px;font-weight:500;white-space:nowrap}
.wr-g{background:var(--win-l);color:var(--win);border:1px solid #bbf7d0}
.wr-w{background:var(--gold-l);color:var(--gold);border:1px solid #fde68a}
.wr-b{background:var(--loss-l);color:var(--loss);border:1px solid #fecaca}

/* ── TABS ── */
.tabs{display:flex}
.tab{padding:10px 14px;font-size:13px;font-weight:500;color:var(--text2);cursor:pointer;border-bottom:2px solid transparent;transition:all .15s;white-space:nowrap}
.tab:hover{color:var(--text)}
.tab.active{color:var(--accent);border-bottom-color:var(--accent);font-weight:600}

/* ── GRID HELPERS ── */
.g2{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.g3{display:grid;grid-template-columns:repeat(3,1fr);gap:16px}
.g4{display:grid;grid-template-columns:repeat(4,1fr);gap:16px}
.mb16{margin-bottom:16px}
.mb20{margin-bottom:20px}
.mb24{margin-bottom:24px}
.flex-col{display:flex;flex-direction:column;gap:16px}
.main-split{display:grid;grid-template-columns:1fr 336px;gap:16px}
.section-head{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.section-title{font-family:'Sora',sans-serif;font-size:15px;font-weight:700;letter-spacing:-.3px}

/* ── KPI ── */
.kpi{padding:20px}
.kpi-lbl{font-size:11px;color:var(--text3);font-weight:600;text-transform:uppercase;letter-spacing:.07em;margin-bottom:8px}
.kpi-val{font-family:'Sora',sans-serif;font-size:26px;font-weight:700;letter-spacing:-.8px;line-height:1;margin-bottom:7px}
.hi-dim{font-size:15px;color:var(--text3);font-weight:400}
.kpi-change{font-size:12px;font-weight:600}
.up{color:var(--win)}.down{color:var(--loss)}
.hi-blue{color:var(--accent)}.hi-green{color:var(--win)}.hi-gold{color:var(--gold)}.hi-red{color:var(--loss)}.hi-dim2{color:var(--text3)}
.mini-bar{height:3px;background:var(--border);border-radius:100px;overflow:hidden;margin-top:10px}
.mini-fill{height:100%;border-radius:100px}

/* ── PROFILE BAR ── */
.profile-bar{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:22px 24px;display:flex;align-items:center;gap:20px;box-shadow:var(--shadow);margin-bottom:20px}
.pa{width:62px;height:62px;border-radius:50%;background:linear-gradient(135deg,#dbeafe,#93c5fd);display:flex;align-items:center;justify-content:center;font-size:28px;flex-shrink:0;border:3px solid var(--surface);box-shadow:0 0 0 2px var(--border2)}
.pname{font-family:'Sora',sans-serif;font-size:19px;font-weight:700;letter-spacing:-.4px}
.pmeta{font-size:12.5px;color:var(--text2);display:flex;gap:10px;margin-top:2px;flex-wrap:wrap}
.pmeta-dot{color:var(--border2)}
.pstats{display:flex;gap:1px;background:var(--border);border-radius:var(--r-sm);overflow:hidden;margin-left:auto}
.pstat{background:var(--surface);padding:12px 18px;text-align:center;min-width:88px;transition:background .12s}
.pstat:hover{background:var(--surface2)}
.pstat-val{font-family:'Sora',sans-serif;font-size:17px;font-weight:700;letter-spacing:-.4px}
.pstat-lbl{font-size:10px;color:var(--text3);font-weight:600;text-transform:uppercase;letter-spacing:.05em;margin-top:1px}
.rank-tag{display:flex;align-items:center;gap:8px;background:var(--gold-l);border:1px solid #fde68a;border-radius:100px;padding:7px 16px;white-space:nowrap;flex-shrink:0}
.rank-tag-icon{font-size:20px}
.rank-tag-name{font-size:13px;font-weight:700;color:var(--gold)}
.rank-tag-lp{font-size:11.5px;color:#92400e;font-family:'DM Mono',monospace}

/* ── MATCH ROWS ── */
.match{display:flex;align-items:center;gap:13px;padding:11px 20px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .12s}
.match:last-child{border-bottom:none}
.match:hover{background:var(--surface2)}
.m-stripe{width:3px;border-radius:100px;align-self:stretch;flex-shrink:0}
.match.win .m-stripe{background:var(--win)}
.match.loss .m-stripe{background:var(--loss)}
.m-icon{width:40px;height:40px;border-radius:var(--r-sm);background:var(--bg);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:19px;flex-shrink:0}
.m-info{flex:1;min-width:0}
.m-top{display:flex;align-items:center;gap:6px;margin-bottom:2px;flex-wrap:wrap}
.m-champ{font-weight:600;font-size:13.5px}
.m-kda{font-family:'DM Mono',monospace;font-size:12px;color:var(--text2)}
.m-right{text-align:right;flex-shrink:0}
.m-ratio{font-family:'Sora',sans-serif;font-size:15px;font-weight:700;letter-spacing:-.3px}
.m-dur{font-size:11px;color:var(--text3);font-family:'DM Mono',monospace}

/* ── CHAMP ROWS ── */
.champ-row{display:flex;align-items:center;gap:11px;padding:10px 20px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .12s}
.champ-row:last-child{border-bottom:none}
.champ-row:hover{background:var(--surface2)}
.cr-num{width:20px;font-size:11px;color:var(--text3);font-weight:600;font-family:'DM Mono',monospace;flex-shrink:0}
.cr-portrait{width:36px;height:36px;border-radius:50%;background:var(--bg);border:1.5px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0}
.cr-info{flex:1;min-width:0}
.cr-name{font-weight:600;font-size:13.5px}
.cr-games{font-size:11px;color:var(--text3)}
.cr-stats{display:flex;gap:14px;flex-shrink:0}
.cr-s{text-align:right}
.cr-sv{font-size:13px;font-weight:600;font-family:'DM Mono',monospace}
.cr-sl{font-size:9.5px;color:var(--text3);text-transform:uppercase;letter-spacing:.05em}

/* ── LEADERBOARD ── */
.lb-row{display:flex;align-items:center;gap:14px;padding:12px 20px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .12s}
.lb-row:last-child{border-bottom:none}
.lb-row:hover{background:var(--surface2)}
.lb-rank{width:28px;text-align:center;font-family:'Sora',sans-serif;font-size:14px;font-weight:700;flex-shrink:0}
.lb-rank.top1{color:#f59e0b}.lb-rank.top2{color:#94a3b8}.lb-rank.top3{color:#b45309}
.lb-av{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0;border:1.5px solid var(--border);background:var(--bg)}
.lb-info{flex:1;min-width:0}
.lb-name{font-weight:600;font-size:13.5px}
.lb-server{font-size:11px;color:var(--text3)}
.lb-stats{display:flex;gap:20px;flex-shrink:0}
.lb-s{text-align:right}
.lb-sv{font-size:13.5px;font-weight:600;font-family:'DM Mono',monospace}
.lb-sl{font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.05em}
.tier-badge{padding:3px 10px;border-radius:100px;font-size:11px;font-weight:700;font-family:'DM Mono',monospace;white-space:nowrap}
.tier-chall{background:#fefce8;color:#92400e;border:1px solid #fde68a}
.tier-gm{background:#fff7ed;color:#c2410c;border:1px solid #fed7aa}
.tier-master{background:#fdf4ff;color:#7e22ce;border:1px solid #e9d5ff}
.tier-diamond{background:var(--accent-l);color:var(--accent);border:1px solid #bfdbfe}
.tier-plat{background:#f0fdfa;color:#0f766e;border:1px solid #99f6e4}
.tier-gold{background:var(--gold-l);color:var(--gold);border:1px solid #fde68a}
.tier-silver{background:var(--bg);color:var(--text2);border:1px solid var(--border2)}

/* ── CHARTS ── */
.bar-chart{display:flex;align-items:flex-end;gap:5px}
.bcol{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px}
.bcol-bars{display:flex;gap:2px;align-items:flex-end;width:100%}
.bseg{flex:1;border-radius:3px 3px 0 0;cursor:pointer;transition:opacity .15s}
.bseg:hover{opacity:.7}
.bw{background:var(--win)}.bl{background:#fca5a5}
.bday{font-size:9px;color:var(--text3);font-weight:600;font-family:'DM Mono',monospace;letter-spacing:.04em}
.chart-legend{display:flex;gap:14px}
.leg{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--text2)}
.leg-dot{width:8px;height:8px;border-radius:2px}

/* ── PROGRESS ── */
.prog-row{display:flex;align-items:center;gap:10px;margin-bottom:10px}
.prog-row:last-child{margin-bottom:0}
.prog-label{font-size:12.5px;font-weight:500;min-width:90px}
.prog-track{flex:1;height:6px;background:var(--border);border-radius:100px;overflow:hidden}
.prog-fill{height:100%;border-radius:100px;transition:width 1s ease}
.prog-val{font-size:12px;font-family:'DM Mono',monospace;font-weight:500;min-width:36px;text-align:right;color:var(--text2)}

/* ── ROLE CHIPS ── */
.role-row{display:flex;gap:7px;padding:12px 20px;border-top:1px solid var(--border)}
.role-chip{flex:1;padding:9px 5px;border-radius:var(--r-sm);border:1px solid var(--border);background:var(--surface2);text-align:center;cursor:pointer;transition:all .15s}
.role-chip:hover,.role-chip.active{border-color:var(--accent);background:var(--accent-l)}
.rc-icon{font-size:17px;margin-bottom:3px}
.rc-name{font-size:9px;color:var(--text3);font-weight:600;text-transform:uppercase;letter-spacing:.06em}
.rc-pct{font-size:12px;font-weight:700;color:var(--text);margin-top:1px}
.role-chip.active .rc-pct{color:var(--accent)}

/* ── LIVE ── */
.live-dot{width:7px;height:7px;border-radius:50%;background:var(--loss);animation:blink 1.2s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.15}}
.live-lbl{font-size:10.5px;font-weight:700;color:var(--loss);letter-spacing:.07em;text-transform:uppercase}
.live-timer-block{text-align:center;padding:18px 20px;border-bottom:1px solid var(--border)}
.live-time{font-family:'Sora',sans-serif;font-size:42px;font-weight:800;letter-spacing:-2px;line-height:1;margin-bottom:3px}
.live-sub{font-size:11px;color:var(--text3);font-weight:600;letter-spacing:.07em;text-transform:uppercase}
.live-grid{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:var(--border)}
.live-cell{background:var(--surface);padding:13px 14px;text-align:center;transition:background .12s}
.live-cell:hover{background:var(--surface2)}
.live-num{font-family:'Sora',sans-serif;font-size:22px;font-weight:700;letter-spacing:-.5px;line-height:1;margin-bottom:2px}
.live-lbl2{font-size:9.5px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;font-weight:600}
.cmp-block{padding:14px 20px;border-top:1px solid var(--border)}
.cmp-row{margin-bottom:10px}
.cmp-row:last-child{margin-bottom:0}
.cmp-meta{display:flex;justify-content:space-between;font-size:11px;font-weight:600;margin-bottom:5px}
.cmp-track{height:5px;background:var(--border);border-radius:100px;overflow:hidden}
.cmp-fill{height:100%;border-radius:100px}

/* ── FILTER BAR ── */
.filter-bar{display:flex;align-items:center;gap:8px;padding:12px 20px;border-bottom:1px solid var(--border);flex-wrap:wrap}
.filter-label{font-size:12px;color:var(--text3);font-weight:500;margin-right:2px}
.filter-pill{padding:5px 12px;border-radius:100px;font-size:12px;font-weight:500;border:1px solid var(--border2);background:var(--surface);color:var(--text2);cursor:pointer;transition:all .15s}
.filter-pill:hover{border-color:var(--accent);color:var(--accent)}
.filter-pill.active{background:var(--accent);color:#fff;border-color:var(--accent)}

/* ── STAT TABLE ── */
.stat-table{width:100%;border-collapse:collapse}
.stat-table th,.stat-table td{padding:10px 20px;text-align:left;font-size:13px}
.stat-table th{font-size:10.5px;font-weight:700;text-transform:uppercase;letter-spacing:.07em;color:var(--text3);border-bottom:1px solid var(--border);background:var(--surface2)}
.stat-table td{border-bottom:1px solid var(--border)}
.stat-table tr:last-child td{border-bottom:none}
.stat-table tr:hover td{background:var(--surface2);cursor:pointer}

/* ── SUM GRID ── */
.sum-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--border)}
.sum-cell{background:var(--surface);padding:16px;text-align:center;transition:background .12s}
.sum-cell:hover{background:var(--surface2)}
.sum-val{font-family:'Sora',sans-serif;font-size:20px;font-weight:700;letter-spacing:-.5px;margin-bottom:2px}
.sum-lbl{font-size:10.5px;color:var(--text3);font-weight:600;text-transform:uppercase;letter-spacing:.06em}

/* ════════════════════════════════════════
   AUTH SCREENS
════════════════════════════════════════ */
#auth-screen{position:fixed;inset:0;background:var(--bg);z-index:999;display:flex;align-items:center;justify-content:center;padding:20px}
.auth-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);box-shadow:var(--shadow-lg);width:100%;max-width:420px;overflow:hidden}
.auth-header{padding:28px 28px 0;text-align:center}
.auth-logo{font-family:'Sora',sans-serif;font-size:24px;font-weight:800;color:var(--text);display:inline-flex;align-items:center;gap:7px;margin-bottom:6px}
.auth-logo-dot{width:9px;height:9px;border-radius:50%;background:var(--accent)}
.auth-tagline{font-size:13px;color:var(--text3);margin-bottom:24px}
.auth-tabs{display:flex;border-bottom:1px solid var(--border)}
.auth-tab{flex:1;padding:12px;text-align:center;font-size:13px;font-weight:600;color:var(--text2);cursor:pointer;border-bottom:2px solid transparent;transition:all .15s}
.auth-tab.active{color:var(--accent);border-bottom-color:var(--accent)}
.auth-body{padding:24px 28px 28px}
.form-group{margin-bottom:16px}
.form-label{display:block;font-size:12.5px;font-weight:600;color:var(--text2);margin-bottom:6px}
.form-input{width:100%;padding:9px 12px;border:1px solid var(--border2);border-radius:var(--r-sm);font-size:13.5px;color:var(--text);background:var(--surface);outline:none;transition:border-color .15s}
.form-input:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(37,99,235,.08)}
.form-input::placeholder{color:var(--text3)}
.form-select{width:100%;padding:9px 12px;border:1px solid var(--border2);border-radius:var(--r-sm);font-size:13.5px;color:var(--text);background:var(--surface);outline:none;transition:border-color .15s;cursor:pointer}
.form-select:focus{border-color:var(--accent)}
.form-hint{font-size:11.5px;color:var(--text3);margin-top:5px}
.auth-divider{display:flex;align-items:center;gap:10px;margin:16px 0}
.auth-divider::before,.auth-divider::after{content:'';flex:1;height:1px;background:var(--border)}
.auth-divider span{font-size:11px;color:var(--text3);font-weight:500}
.auth-switch{text-align:center;font-size:12.5px;color:var(--text3);margin-top:14px}
.auth-switch a{color:var(--accent);font-weight:600;cursor:pointer}
.auth-error{background:var(--loss-l);border:1px solid #fecaca;border-radius:var(--r-sm);padding:10px 12px;font-size:12.5px;color:var(--loss);margin-bottom:14px;display:none}
.auth-error.show{display:block}

/* ════════════════════════════════════════
   LOG GAME MODAL
════════════════════════════════════════ */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.35);z-index:500;display:none;align-items:center;justify-content:center;padding:20px;backdrop-filter:blur(4px)}
.modal-overlay.open{display:flex}
.modal{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);box-shadow:var(--shadow-lg);width:100%;max-width:560px;max-height:90vh;overflow-y:auto;animation:slideUp .25s ease both}
@keyframes slideUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.modal-header{padding:20px 24px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between}
.modal-title{font-family:'Sora',sans-serif;font-size:16px;font-weight:700;letter-spacing:-.3px}
.modal-close{width:30px;height:30px;border-radius:var(--r-sm);border:none;background:none;font-size:18px;color:var(--text3);cursor:pointer;display:flex;align-items:center;justify-content:center;transition:background .15s}
.modal-close:hover{background:var(--bg);color:var(--text)}
.modal-body{padding:24px}
.modal-footer{padding:16px 24px;border-top:1px solid var(--border);display:flex;gap:10px;justify-content:flex-end}

/* Screenshot upload zone */
.upload-zone{border:2px dashed var(--border2);border-radius:var(--r);padding:32px 20px;text-align:center;cursor:pointer;transition:all .2s;background:var(--surface2);position:relative;margin-bottom:20px}
.upload-zone:hover,.upload-zone.drag{border-color:var(--accent);background:var(--accent-l)}
.upload-zone input[type=file]{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.upload-icon{font-size:36px;margin-bottom:10px}
.upload-title{font-weight:600;font-size:14px;margin-bottom:4px}
.upload-sub{font-size:12px;color:var(--text3)}
.upload-preview{width:100%;border-radius:var(--r-sm);max-height:200px;object-fit:cover;display:none;margin-bottom:16px;border:1px solid var(--border)}

/* AI reading state */
.ai-reading{background:var(--accent-l);border:1px solid #bfdbfe;border-radius:var(--r-sm);padding:14px 16px;display:none;margin-bottom:16px}
.ai-reading.show{display:flex;align-items:center;gap:12px}
.ai-spinner{width:20px;height:20px;border:2px solid #bfdbfe;border-top-color:var(--accent);border-radius:50%;animation:spin .7s linear infinite;flex-shrink:0}
@keyframes spin{to{transform:rotate(360deg)}}
.ai-reading-text{font-size:13px;color:var(--accent);font-weight:500}

/* Extracted stats form */
.extracted-form{display:none}
.extracted-form.show{display:block}
.extracted-note{background:var(--win-l);border:1px solid #bbf7d0;border-radius:var(--r-sm);padding:10px 14px;font-size:12.5px;color:var(--win);margin-bottom:16px;display:flex;align-items:center;gap:8px}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px}
.form-row-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:16px}

/* ════════════════════════════════════════
   NOTIFICATION TOAST
════════════════════════════════════════ */
.toast{position:fixed;bottom:24px;right:24px;background:var(--text);color:#fff;padding:12px 18px;border-radius:var(--r-sm);font-size:13px;font-weight:500;z-index:9999;opacity:0;transform:translateY(8px);transition:all .3s;pointer-events:none;max-width:320px}
.toast.show{opacity:1;transform:translateY(0)}
.toast.success{background:var(--win)}
.toast.error{background:var(--loss)}

/* ════════════════════════════════════════
   EMPTY STATES
════════════════════════════════════════ */
.empty-state{padding:48px 20px;text-align:center}
.empty-icon{font-size:40px;margin-bottom:10px;opacity:.5}
.empty-title{font-weight:600;font-size:15px;margin-bottom:6px}
.empty-sub{font-size:13px;color:var(--text3);margin-bottom:20px}

/* ════════════════════════════════════════
   PROFILE PAGE SPECIFIC
════════════════════════════════════════ */
.avatar-selector{display:flex;gap:8px;flex-wrap:wrap;margin-top:6px}
.av-opt{width:40px;height:40px;border-radius:50%;background:var(--bg);border:2px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:19px;cursor:pointer;transition:all .15s}
.av-opt:hover{border-color:var(--accent)}
.av-opt.selected{border-color:var(--accent);background:var(--accent-l);box-shadow:0 0 0 2px rgba(37,99,235,.2)}

/* Settings sections */
.settings-section{margin-bottom:28px}
.settings-section-title{font-weight:600;font-size:13.5px;margin-bottom:12px;padding-bottom:8px;border-bottom:1px solid var(--border)}
.settings-row{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid var(--border)}
.settings-row:last-child{border-bottom:none}
.settings-row-label{font-size:13.5px;font-weight:500}
.settings-row-sub{font-size:12px;color:var(--text3);margin-top:1px}

/* Toggle switch */
.toggle{width:40px;height:22px;background:var(--border2);border-radius:100px;position:relative;cursor:pointer;transition:background .2s;flex-shrink:0}
.toggle.on{background:var(--accent)}
.toggle::after{content:'';position:absolute;width:16px;height:16px;background:#fff;border-radius:50%;top:3px;left:3px;transition:transform .2s;box-shadow:0 1px 3px rgba(0,0,0,.2)}
.toggle.on::after{transform:translateX(18px)}
</style>
</head>
<body>

<!-- ════════════════════════════════════════
     AUTH SCREEN
════════════════════════════════════════ -->
<div id="auth-screen">
  <div class="auth-card">
    <div class="auth-header">
      <div class="auth-logo">nexus<span class="auth-logo-dot"></span></div>
      <div class="auth-tagline">Track your MOBA stats. Improve every game.</div>
    </div>
    <div class="auth-tabs">
      <div class="auth-tab active" id="tab-login" onclick="switchAuthTab('login')">Sign In</div>
      <div class="auth-tab" id="tab-signup" onclick="switchAuthTab('signup')">Create Account</div>
    </div>

    <!-- LOGIN -->
    <div class="auth-body" id="auth-login">
      <div class="auth-error" id="login-error">Incorrect username or password.</div>
      <div class="form-group">
        <label class="form-label">Username</label>
        <input class="form-input" type="text" id="login-user" placeholder="Your username" autocomplete="username">
      </div>
      <div class="form-group">
        <label class="form-label">Password</label>
        <input class="form-input" type="password" id="login-pass" placeholder="Your password">
      </div>
      <button class="btn btn-primary btn-full btn-lg" onclick="doLogin()" style="margin-top:4px">Sign In →</button>
      <div class="auth-switch">Don't have an account? <a onclick="switchAuthTab('signup')">Create one</a></div>
      <div class="auth-divider"><span>or try a demo</span></div>
      <button class="btn btn-ghost btn-full" onclick="demoLogin()">👾 Demo Account</button>
    </div>

    <!-- SIGNUP -->
    <div class="auth-body" id="auth-signup" style="display:none">
      <div class="auth-error" id="signup-error">Username already taken.</div>
      <div class="form-row">
        <div class="form-group" style="margin-bottom:0">
          <label class="form-label">Username</label>
          <input class="form-input" type="text" id="signup-user" placeholder="Choose a username">
        </div>
        <div class="form-group" style="margin-bottom:0">
          <label class="form-label">Display Name</label>
          <input class="form-input" type="text" id="signup-name" placeholder="Your name">
        </div>
      </div>
      <div class="form-group" style="margin-top:16px">
        <label class="form-label">Email</label>
        <input class="form-input" type="email" id="signup-email" placeholder="you@email.com">
      </div>
      <div class="form-group">
        <label class="form-label">Password</label>
        <input class="form-input" type="password" id="signup-pass" placeholder="Choose a password (min 6 chars)">
      </div>
      <div class="form-group">
        <label class="form-label">Favourite Role</label>
        <select class="form-select" id="signup-role">
          <option value="Mid">Mid Lane</option>
          <option value="Top">Top Lane</option>
          <option value="Bot">Bot Lane (ADC)</option>
          <option value="Jungle">Jungle</option>
          <option value="Support">Support</option>
        </select>
      </div>
      <button class="btn btn-primary btn-full btn-lg" onclick="doSignup()" style="margin-top:4px">Create Account →</button>
      <div class="auth-switch">Already have an account? <a onclick="switchAuthTab('login')">Sign in</a></div>
    </div>
  </div>
</div>

<!-- ════════════════════════════════════════
     MAIN APP
════════════════════════════════════════ -->
<div class="layout" id="app" style="display:none">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sidebar-top">
      <div class="logo">nexus<span class="logo-dot"></span></div>
      <div class="logo-sub">MOBA Stats Tracker</div>
    </div>
    <nav class="nav-body">
      <div class="nav-group">
        <div class="nav-group-label">Dashboard</div>
        <div class="nav-item active" data-page="overview"><span class="nav-icon">📊</span>Overview</div>
        <div class="nav-item" data-page="champions"><span class="nav-icon">🗡️</span>Champions</div>
        <div class="nav-item" data-page="matches"><span class="nav-icon">📋</span>Match History</div>
        <div class="nav-item" data-page="performance"><span class="nav-icon">📈</span>Performance</div>
      </div>
      <div class="nav-group">
        <div class="nav-group-label">Community</div>
        <div class="nav-item" data-page="leaderboard"><span class="nav-icon">🏆</span>Leaderboard</div>
        <div class="nav-item" data-page="friends"><span class="nav-icon">👥</span>Friends</div>
      </div>
      <div class="nav-group">
        <div class="nav-group-label">Account</div>
        <div class="nav-item" data-page="settings"><span class="nav-icon">⚙️</span>Settings</div>
        <div class="nav-item" onclick="doLogout()"><span class="nav-icon">🚪</span>Sign Out</div>
      </div>
    </nav>
    <div class="sidebar-footer">
      <div class="user-tile" onclick="navigate('settings')">
        <div class="u-av" id="sidebar-avatar">⚡</div>
        <div>
          <div class="u-name" id="sidebar-name">—</div>
          <div class="u-meta" id="sidebar-rank">—</div>
        </div>
      </div>
    </div>
  </aside>

  <div class="main">
    <header class="topbar">
      <div class="page-heading" id="pageHeading">Overview</div>
      <div class="topbar-right">
        <div class="search-wrap"><span>🔍</span><input type="text" placeholder="Search players…" id="searchInput"></div>
        <button class="btn btn-primary" onclick="openLogGame()">+ Log Game</button>
      </div>
    </header>

    <!-- ═══ PAGE: OVERVIEW ═══ -->
    <div class="page active" id="page-overview">
      <div class="profile-bar">
        <div class="pa" id="ov-avatar">⚡</div>
        <div>
          <div class="pname" id="ov-name">—</div>
          <div class="pmeta"><span id="ov-role">—</span><span class="pmeta-dot">·</span><span id="ov-joined">—</span></div>
        </div>
        <div class="pstats">
          <div class="pstat"><div class="pstat-val" id="ov-wr">—</div><div class="pstat-lbl">Win Rate</div></div>
          <div class="pstat"><div class="pstat-val" id="ov-kda">—</div><div class="pstat-lbl">KDA</div></div>
          <div class="pstat"><div class="pstat-val" id="ov-games">—</div><div class="pstat-lbl">Games</div></div>
          <div class="pstat"><div class="pstat-val" id="ov-cs">—</div><div class="pstat-lbl">Avg CS</div></div>
        </div>
        <div class="rank-tag">
          <span class="rank-tag-icon">🏆</span>
          <span class="rank-tag-name" id="ov-rank">Unranked</span>
          <span class="rank-tag-lp" id="ov-lp">0 LP</span>
        </div>
      </div>

      <div class="g4 mb20" id="ov-kpis">
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">⚔️ Avg K/D/A</div><div class="kpi-val" id="kpi-kda">—</div><div class="kpi-change" id="kpi-kda-sub" style="color:var(--text3)">Log games to see stats</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">💥 Avg Damage</div><div class="kpi-val" id="kpi-dmg">—</div><div class="kpi-change" id="kpi-dmg-sub" style="color:var(--text3)">No data yet</div><div class="mini-bar"><div class="mini-fill" id="kpi-dmg-bar" style="width:0;background:var(--accent)"></div></div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">⏱ Avg Duration</div><div class="kpi-val" id="kpi-dur">—</div><div class="kpi-change" id="kpi-dur-sub" style="color:var(--text3)">No data yet</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🌾 Avg CS</div><div class="kpi-val" id="kpi-cs">—</div><div class="kpi-change" id="kpi-cs-sub" style="color:var(--text3)">No data yet</div><div class="mini-bar"><div class="mini-fill" id="kpi-cs-bar" style="width:0;background:var(--win)"></div></div></div></div>
      </div>

      <div class="main-split">
        <div class="flex-col">
          <div class="card">
            <div class="card-header"><div class="card-title">Recent Matches</div><button class="btn btn-ghost btn-sm" data-page="matches">View all →</button></div>
            <div id="ov-matches-list"></div>
          </div>
          <div class="card">
            <div class="card-header"><div class="card-title">7-Day Performance</div><div class="chart-legend"><div class="leg"><div class="leg-dot" style="background:var(--win)"></div>Wins</div><div class="leg"><div class="leg-dot" style="background:#fca5a5"></div>Losses</div></div></div>
            <div style="padding:20px"><div class="bar-chart" style="height:90px" id="ov-chart"></div></div>
            <div class="role-row" id="role-chips"></div>
          </div>
        </div>
        <div class="flex-col">
          <div class="card">
            <div class="card-header"><div class="card-title">Quick Log</div></div>
            <div style="padding:20px;text-align:center">
              <div style="font-size:36px;margin-bottom:10px">🎮</div>
              <div style="font-weight:600;margin-bottom:6px">Just finished a game?</div>
              <div style="font-size:13px;color:var(--text3);margin-bottom:16px">Upload a screenshot and we'll read your stats automatically.</div>
              <button class="btn btn-primary btn-full" onclick="openLogGame()">+ Log New Game</button>
            </div>
          </div>
          <div class="card">
            <div class="card-header"><div class="card-title">Top Champions</div><button class="btn btn-ghost btn-sm" data-page="champions">View all →</button></div>
            <div id="ov-champs"></div>
          </div>
        </div>
      </div>
    </div>

    <!-- ═══ PAGE: CHAMPIONS ═══ -->
    <div class="page" id="page-champions">
      <div class="section-head mb20">
        <div class="section-title">Champion Statistics</div>
      </div>
      <div class="g3 mb20">
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🥇 Best Champion</div><div class="kpi-val" style="font-size:18px" id="champ-best">—</div><div class="kpi-change hi-green" id="champ-best-sub">Log games to see</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🎯 Most Played</div><div class="kpi-val" style="font-size:18px" id="champ-most">—</div><div class="kpi-change hi-blue" id="champ-most-sub">No data yet</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">📉 Needs Work</div><div class="kpi-val" style="font-size:18px" id="champ-worst">—</div><div class="kpi-change hi-red" id="champ-worst-sub">No data yet</div></div></div>
      </div>
      <div class="main-split">
        <div class="card">
          <div class="card-header"><div class="card-title">All Champions</div><div class="card-sub" id="champ-count-label">0 champions</div></div>
          <div class="filter-bar">
            <span class="filter-label">Role:</span>
            <div class="filter-pill active" data-cfilter="all">All</div>
            <div class="filter-pill" data-cfilter="Mid">Mid</div>
            <div class="filter-pill" data-cfilter="Top">Top</div>
            <div class="filter-pill" data-cfilter="Bot">Bot</div>
            <div class="filter-pill" data-cfilter="Jungle">Jungle</div>
            <div class="filter-pill" data-cfilter="Support">Support</div>
          </div>
          <div id="champ-list"></div>
        </div>
        <div class="flex-col">
          <div class="card">
            <div class="card-header"><div class="card-title">Win Rate by Role</div></div>
            <div style="padding:20px" id="role-wr-bars"></div>
          </div>
          <div class="card">
            <div class="card-header"><div class="card-title">Summary</div></div>
            <div class="sum-grid" id="champ-summary"></div>
          </div>
        </div>
      </div>
    </div>

    <!-- ═══ PAGE: MATCH HISTORY ═══ -->
    <div class="page" id="page-matches">
      <div class="section-head mb20">
        <div class="section-title">Match History</div>
        <button class="btn btn-primary btn-sm" onclick="openLogGame()">+ Log Game</button>
      </div>
      <div class="g4 mb20">
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">📅 Total Games</div><div class="kpi-val" id="mh-total">0</div><div class="kpi-change hi-green" id="mh-wr-label">No games yet</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🔥 Win Streak</div><div class="kpi-val" id="mh-streak">0</div><div class="kpi-change hi-blue" id="mh-streak-label">Current streak</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">⚔️ Best KDA</div><div class="kpi-val" id="mh-bestkda">—</div><div class="kpi-change hi-gold" id="mh-bestkda-label">No games yet</div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🌾 Most CS</div><div class="kpi-val" id="mh-mostcs">—</div><div class="kpi-change hi-blue" id="mh-mostcs-label">No games yet</div></div></div>
      </div>
      <div class="card">
        <div style="display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--border)">
          <div class="tabs" style="border-bottom:none;padding:0 12px" id="tabs-matches">
            <div class="tab active">All</div><div class="tab">Wins</div><div class="tab">Losses</div>
          </div>
          <div style="padding:0 20px;font-size:12px;color:var(--text3)" id="mh-count-label">0 games</div>
        </div>
        <div id="mh-list"></div>
      </div>
    </div>

    <!-- ═══ PAGE: PERFORMANCE ═══ -->
    <div class="page" id="page-performance">
      <div class="section-head mb20">
        <div class="section-title">Performance Analysis</div>
      </div>
      <div class="g4 mb20">
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">📊 Overall WR</div><div class="kpi-val" id="perf-wr">—</div><div class="mini-bar"><div class="mini-fill" id="perf-wr-bar" style="width:0;background:var(--win)"></div></div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🎯 Avg KDA</div><div class="kpi-val" id="perf-kda">—</div><div class="mini-bar"><div class="mini-fill" id="perf-kda-bar" style="width:0;background:var(--accent)"></div></div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">🌾 Avg CS</div><div class="kpi-val" id="perf-cs">—</div><div class="mini-bar"><div class="mini-fill" id="perf-cs-bar" style="width:0;background:var(--gold)"></div></div></div></div>
        <div class="card card-hover"><div class="kpi"><div class="kpi-lbl">💥 Avg Damage</div><div class="kpi-val" id="perf-dmg">—</div><div class="mini-bar"><div class="mini-fill" id="perf-dmg-bar2" style="width:0;background:var(--loss)"></div></div></div></div>
      </div>
      <div class="g2 mb16">
        <div class="card">
          <div class="card-header"><div class="card-title">Win Rate by Champion</div></div>
          <div style="padding:20px" id="perf-champ-bars"></div>
        </div>
        <div class="card">
          <div class="card-header"><div class="card-title">Game Length Analysis</div></div>
          <div class="scroll-x">
            <table class="stat-table" id="perf-duration-table">
              <thead><tr><th>Duration</th><th>Games</th><th>Win Rate</th><th>Avg KDA</th></tr></thead>
              <tbody id="perf-duration-body"></tbody>
            </table>
          </div>
        </div>
      </div>
    </div>

    <!-- ═══ PAGE: LEADERBOARD ═══ -->
    <div class="page" id="page-leaderboard">
      <div class="section-head mb20">
        <div class="section-title">Leaderboard</div>
      </div>
      <div class="card mb20">
        <div class="card-header"><div class="card-title">Top Players</div><div class="card-sub" id="lb-count">All registered players</div></div>
        <div id="lb-list"></div>
      </div>
    </div>

    <!-- ═══ PAGE: FRIENDS ═══ -->
    <div class="page" id="page-friends">
      <div class="section-head mb20">
        <div class="section-title">Friends</div>
      </div>
      <div class="card">
        <div class="card-header"><div class="card-title">Find Players</div></div>
        <div style="padding:20px;display:flex;gap:10px">
          <input class="form-input" type="text" id="friend-search" placeholder="Search by username…" style="flex:1">
          <button class="btn btn-primary" onclick="searchPlayers()">Search</button>
        </div>
        <div id="friend-results"></div>
      </div>
    </div>

    <!-- ═══ PAGE: SETTINGS ═══ -->
    <div class="page" id="page-settings">
      <div class="section-head mb20"><div class="section-title">Settings</div></div>
      <div class="g2">
        <div class="flex-col">
          <div class="card">
            <div class="card-header"><div class="card-title">Profile</div></div>
            <div style="padding:20px">
              <div class="form-group">
                <label class="form-label">Display Name</label>
                <input class="form-input" type="text" id="set-name">
              </div>
              <div class="form-group">
                <label class="form-label">Favourite Role</label>
                <select class="form-select" id="set-role">
                  <option>Mid</option><option>Top</option><option>Bot</option><option>Jungle</option><option>Support</option>
                </select>
              </div>
              <div class="form-group">
                <label class="form-label">Avatar</label>
                <div class="avatar-selector" id="av-selector">
                  <div class="av-opt" data-av="⚡">⚡</div><div class="av-opt" data-av="🧙">🧙</div>
                  <div class="av-opt" data-av="🌙">🌙</div><div class="av-opt" data-av="🔥">🔥</div>
                  <div class="av-opt" data-av="❄️">❄️</div><div class="av-opt" data-av="🌊">🌊</div>
                  <div class="av-opt" data-av="⚔️">⚔️</div><div class="av-opt" data-av="🌿">🌿</div>
                  <div class="av-opt" data-av="🛡️">🛡️</div><div class="av-opt" data-av="🌑">🌑</div>
                </div>
              </div>
              <div class="form-group">
                <label class="form-label">Rank</label>
                <select class="form-select" id="set-rank">
                  <option>Unranked</option><option>Iron</option><option>Bronze</option><option>Silver</option>
                  <option>Gold</option><option>Platinum</option><option>Diamond</option><option>Master</option>
                  <option>Grandmaster</option><option>Challenger</option>
                </select>
              </div>
              <div class="form-group">
                <label class="form-label">LP</label>
                <input class="form-input" type="number" id="set-lp" min="0" max="100" placeholder="0–100">
              </div>
              <button class="btn btn-primary" onclick="saveSettings()">Save Changes</button>
            </div>
          </div>
        </div>
        <div class="flex-col">
          <div class="card">
            <div class="card-header"><div class="card-title">Danger Zone</div></div>
            <div style="padding:20px">
              <div style="font-size:13px;color:var(--text2);margin-bottom:14px">Permanently delete all your match history. This cannot be undone.</div>
              <button class="btn btn-danger" onclick="clearMatchHistory()">🗑 Clear All Match History</button>
            </div>
          </div>
          <div class="card">
            <div class="card-header"><div class="card-title">About</div></div>
            <div style="padding:20px;font-size:13px;color:var(--text2);line-height:1.7">
              <strong style="color:var(--text)">Nexus Stats</strong> is a self-hosted MOBA tracker. All data is stored locally in your browser. No data is sent to any external server unless you use the AI screenshot feature, which uses the Anthropic API.<br><br>
              <span style="color:var(--text3)">v1.0.0 · Single-file build</span>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div><!-- /main -->
</div><!-- /layout -->

<!-- ════════════════════════════════════════
     LOG GAME MODAL
════════════════════════════════════════ -->
<div class="modal-overlay" id="log-modal">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Log New Game</div>
      <button class="modal-close" onclick="closeLogGame()">✕</button>
    </div>
    <div class="modal-body">

      <!-- Step 1: Upload -->
      <div id="step-upload">
        <p style="font-size:13px;color:var(--text2);margin-bottom:16px">Upload your end-of-game screenshot and our AI will automatically read your stats. Or fill in the form manually below.</p>
        <div class="upload-zone" id="upload-zone">
          <input type="file" accept="image/*" id="screenshot-input" onchange="handleScreenshot(this)">
          <div class="upload-icon">📸</div>
          <div class="upload-title">Drop screenshot here or click to upload</div>
          <div class="upload-sub">PNG, JPG, WEBP supported</div>
        </div>
        <img id="screenshot-preview" class="upload-preview" alt="Screenshot preview">
        <div class="ai-reading" id="ai-reading">
          <div class="ai-spinner"></div>
          <div class="ai-reading-text">AI is reading your screenshot and extracting stats…</div>
        </div>
      </div>

      <!-- Extracted / Manual form -->
      <div class="extracted-form" id="extracted-form">
        <div class="extracted-note" id="extracted-note" style="display:none">
          ✅ Stats extracted from screenshot — please review and correct if needed.
        </div>
        <div class="form-row">
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Champion Name *</label>
            <input class="form-input" type="text" id="f-champ" placeholder="e.g. Stormcaller">
          </div>
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Champion Icon</label>
            <select class="form-select" id="f-icon">
              <option value="🧙">🧙 Mage</option><option value="⚔️">⚔️ Fighter</option>
              <option value="🏹">🏹 Marksman</option><option value="🌙">🌙 Assassin</option>
              <option value="🛡️">🛡️ Tank</option><option value="🌊">🌊 Support</option>
              <option value="🔥">🔥 Mage (Fire)</option><option value="❄️">❄️ Mage (Ice)</option>
              <option value="🌿">🌿 Jungler</option><option value="⚡">⚡ Fighter</option>
              <option value="🌑">🌑 Assassin</option>
            </select>
          </div>
        </div>
        <div class="form-row-3">
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Kills *</label>
            <input class="form-input" type="number" id="f-k" min="0" placeholder="0">
          </div>
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Deaths *</label>
            <input class="form-input" type="number" id="f-d" min="0" placeholder="0">
          </div>
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Assists *</label>
            <input class="form-input" type="number" id="f-a" min="0" placeholder="0">
          </div>
        </div>
        <div class="form-row" style="margin-top:16px">
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">CS (Creep Score)</label>
            <input class="form-input" type="number" id="f-cs" min="0" placeholder="e.g. 220">
          </div>
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Damage Dealt</label>
            <input class="form-input" type="number" id="f-dmg" min="0" placeholder="e.g. 24000">
          </div>
        </div>
        <div class="form-row" style="margin-top:16px">
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Game Duration (mins)</label>
            <input class="form-input" type="number" id="f-dur" min="1" placeholder="e.g. 28">
          </div>
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Role</label>
            <select class="form-select" id="f-role">
              <option>Mid</option><option>Top</option><option>Bot</option><option>Jungle</option><option>Support</option>
            </select>
          </div>
        </div>
        <div class="form-row" style="margin-top:16px">
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Result *</label>
            <select class="form-select" id="f-result">
              <option value="win">Victory 🏆</option>
              <option value="loss">Defeat 💀</option>
            </select>
          </div>
          <div class="form-group" style="margin-bottom:0">
            <label class="form-label">Game Mode</label>
            <select class="form-select" id="f-mode">
              <option>Ranked</option><option>Normal</option><option>ARAM</option><option>Custom</option>
            </select>
          </div>
        </div>
        <div class="form-group" style="margin-top:16px">
          <label class="form-label">Notes (optional)</label>
          <input class="form-input" type="text" id="f-notes" placeholder="e.g. great early game, team was behind">
        </div>
      </div>

      <div style="margin-top:16px">
        <button class="btn btn-ghost btn-full" id="manual-toggle" onclick="toggleManual()">✏️ Fill in manually instead</button>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeLogGame()">Cancel</button>
      <button class="btn btn-primary" onclick="saveGame()" id="save-game-btn" disabled>Save Game</button>
    </div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
/* ══════════════════════════════════════════
   STORAGE HELPERS  (localStorage as DB)
══════════════════════════════════════════ */
const DB = {
  get: k => { try { return JSON.parse(localStorage.getItem(k)); } catch { return null; } },
  set: (k, v) => localStorage.setItem(k, JSON.stringify(v)),
  del: k => localStorage.removeItem(k),
};

function getUsers() { return DB.get('nx_users') || {}; }
function saveUsers(u) { DB.set('nx_users', u); }
function getCurrentUser() { return DB.get('nx_current'); }
function setCurrentUser(u) { DB.set('nx_current', u); }

function getUserMatches(username) { return DB.get('nx_matches_' + username) || []; }
function saveUserMatches(username, matches) { DB.set('nx_matches_' + username, matches); }

/* ══════════════════════════════════════════
   AUTH
══════════════════════════════════════════ */
function switchAuthTab(tab) {
  document.getElementById('auth-login').style.display  = tab === 'login'  ? '' : 'none';
  document.getElementById('auth-signup').style.display = tab === 'signup' ? '' : 'none';
  document.getElementById('tab-login').classList.toggle('active',  tab === 'login');
  document.getElementById('tab-signup').classList.toggle('active', tab === 'signup');
}

function doLogin() {
  const user = document.getElementById('login-user').value.trim().toLowerCase();
  const pass = document.getElementById('login-pass').value;
  const users = getUsers();
  const err = document.getElementById('login-error');
  if (!users[user] || users[user].password !== pass) {
    err.classList.add('show'); return;
  }
  err.classList.remove('show');
  setCurrentUser(user);
  launchApp();
}

function doSignup() {
  const user  = document.getElementById('signup-user').value.trim().toLowerCase();
  const name  = document.getElementById('signup-name').value.trim();
  const email = document.getElementById('signup-email').value.trim();
  const pass  = document.getElementById('signup-pass').value;
  const role  = document.getElementById('signup-role').value;
  const err   = document.getElementById('signup-error');
  if (!user || !pass || !name) { err.textContent = 'Please fill in all required fields.'; err.classList.add('show'); return; }
  if (pass.length < 6) { err.textContent = 'Password must be at least 6 characters.'; err.classList.add('show'); return; }
  const users = getUsers();
  if (users[user]) { err.textContent = 'Username already taken.'; err.classList.add('show'); return; }
  err.classList.remove('show');
  users[user] = { username: user, name, email, password: pass, role, avatar: '⚡', rank: 'Unranked', lp: 0, joined: new Date().toLocaleDateString('en-GB', { month: 'short', year: 'numeric' }) };
  saveUsers(users);
  setCurrentUser(user);
  launchApp();
}

function demoLogin() {
  const users = getUsers();
  if (!users['demo']) {
    users['demo'] = { username:'demo', name:'Demo Player', email:'demo@nexus.gg', password:'demo123', role:'Mid', avatar:'⚡', rank:'Gold', lp:78, joined:'Jan 2025' };
    saveUsers(users);
    // seed some demo matches
    const demoMatches = [
      { id:1, champ:'Stormcaller', icon:'🧙', k:9, d:2, a:14, cs:234, dmg:31000, dur:28, role:'Mid', result:'win', mode:'Ranked', notes:'', date: new Date(Date.now()-1*86400000).toISOString() },
      { id:2, champ:'Ironclad',    icon:'⚔️', k:3, d:8, a:5,  cs:181, dmg:14000, dur:36, role:'Top', result:'loss', mode:'Ranked', notes:'', date: new Date(Date.now()-1*86400000).toISOString() },
      { id:3, champ:'Voidwhisper', icon:'🌙', k:7, d:3, a:18, cs:268, dmg:28000, dur:22, role:'Mid', result:'win', mode:'Ranked', notes:'', date: new Date(Date.now()-2*86400000).toISOString() },
      { id:4, champ:'Emberlord',   icon:'🔥', k:12,d:4, a:7,  cs:302, dmg:38000, dur:31, role:'Bot', result:'win', mode:'Normal', notes:'', date: new Date(Date.now()-2*86400000).toISOString() },
      { id:5, champ:'Frostbite',   icon:'❄️', k:2, d:6, a:9,  cs:193, dmg:19000, dur:41, role:'Support', result:'loss', mode:'Ranked', notes:'', date: new Date(Date.now()-3*86400000).toISOString() },
      { id:6, champ:'Stormcaller', icon:'🧙', k:6, d:1, a:21, cs:289, dmg:34000, dur:19, role:'Mid', result:'win', mode:'Ranked', notes:'Perfect game', date: new Date(Date.now()-4*86400000).toISOString() },
    ];
    saveUserMatches('demo', demoMatches);
  }
  setCurrentUser('demo');
  launchApp();
}

function doLogout() {
  DB.del('nx_current');
  document.getElementById('app').style.display = 'none';
  document.getElementById('auth-screen').style.display = 'flex';
  navigate('overview');
}

function launchApp() {
  document.getElementById('auth-screen').style.display = 'none';
  document.getElementById('app').style.display = 'flex';
  updateSidebar();
  refreshAllPages();
  navigate('overview');
}

/* ══════════════════════════════════════════
   NAVIGATION
══════════════════════════════════════════ */
const PAGE_LABELS = { overview:'Overview', champions:'Champions', matches:'Match History', performance:'Performance', leaderboard:'Leaderboard', friends:'Friends', settings:'Settings' };

function navigate(pageId) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  const t = document.getElementById('page-' + pageId);
  if (t) { t.classList.add('active'); t.style.animation='none'; requestAnimationFrame(()=>{t.style.animation=''}); }
  document.querySelectorAll('.nav-item[data-page]').forEach(n => n.classList.toggle('active', n.dataset.page === pageId));
  document.getElementById('pageHeading').textContent = PAGE_LABELS[pageId] || pageId;
}

document.querySelectorAll('.nav-item[data-page]').forEach(n => n.addEventListener('click', () => navigate(n.dataset.page)));
document.querySelectorAll('[data-page]').forEach(btn => { if (btn.tagName === 'BUTTON') btn.addEventListener('click', () => navigate(btn.dataset.page)); });

/* ══════════════════════════════════════════
   SIDEBAR UPDATE
══════════════════════════════════════════ */
function updateSidebar() {
  const u = getCurrentUser();
  if (!u) return;
  const users = getUsers();
  const user = users[u];
  if (!user) return;
  document.getElementById('sidebar-avatar').textContent = user.avatar || '⚡';
  document.getElementById('sidebar-name').textContent = user.name || u;
  document.getElementById('sidebar-rank').textContent = (user.rank || 'Unranked') + ' · ' + (user.role || 'Mid');
}

/* ══════════════════════════════════════════
   STAT CALCULATIONS
══════════════════════════════════════════ */
function calcStats(matches) {
  if (!matches.length) return null;
  const wins = matches.filter(m => m.result === 'win').length;
  const totalK = matches.reduce((s,m) => s + (m.k||0), 0);
  const totalD = matches.reduce((s,m) => s + (m.d||0), 0);
  const totalA = matches.reduce((s,m) => s + (m.a||0), 0);
  const totalCS = matches.reduce((s,m) => s + (m.cs||0), 0);
  const totalDmg = matches.reduce((s,m) => s + (m.dmg||0), 0);
  const totalDur = matches.reduce((s,m) => s + (m.dur||0), 0);
  const n = matches.length;
  const avgD = totalD / n;
  const kda = avgD === 0 ? totalK + totalA : ((totalK + totalA) / totalD / n).toFixed(2);
  return {
    wins, losses: n - wins,
    wr: Math.round((wins / n) * 100),
    kda: avgD === 0 ? 'Perfect' : ((totalK / n + totalA / n) / (totalD / n)).toFixed(2),
    avgK: (totalK/n).toFixed(1), avgD: (totalD/n).toFixed(1), avgA: (totalA/n).toFixed(1),
    avgCS: Math.round(totalCS / n),
    avgDmg: Math.round(totalDmg / n),
    avgDur: Math.round(totalDur / n),
    n,
  };
}

function ratioColor(r) {
  const n = parseFloat(r);
  if (n >= 10) return 'var(--gold)';
  if (n >= 5)  return 'var(--win)';
  if (n >= 3)  return 'var(--text)';
  if (n >= 2)  return 'var(--text2)';
  return 'var(--loss)';
}
function wrClass(pct) { return pct >= 60 ? 'wr-g' : pct >= 50 ? 'wr-w' : 'wr-b'; }
function calcRatio(m) {
  if (m.d === 0) return (m.k + m.a).toFixed(1);
  return ((m.k + m.a) / m.d).toFixed(1);
}

/* ══════════════════════════════════════════
   MATCH HTML
══════════════════════════════════════════ */
function matchHTML(m) {
  const ratio = calcRatio(m);
  const durStr = m.dur ? `${m.dur}:00` : '—';
  const dmgStr = m.dmg ? (m.dmg >= 1000 ? Math.round(m.dmg/1000) + 'k' : m.dmg) : '—';
  return `<div class="match ${m.result}">
    <div class="m-stripe"></div>
    <div class="m-icon">${m.icon || '🎮'}</div>
    <div class="m-info">
      <div class="m-top">
        <span class="m-champ">${m.champ}</span>
        <span class="badge ${m.result==='win'?'b-win':'b-loss'}">${m.result==='win'?'Win':'Loss'}</span>
        <span class="badge b-gray">${m.role||'—'}</span>
        <span class="badge b-blue">${m.mode||'Ranked'}</span>
      </div>
      <div class="m-kda">${m.k}/${m.d}/${m.a} · ${m.cs||0} CS · ${dmgStr} dmg${m.notes?' · <em style="color:var(--text3)">'+m.notes+'</em>':''}</div>
    </div>
    <div class="m-right">
      <div class="m-ratio" style="color:${ratioColor(ratio)}">${ratio}</div>
      <div class="m-dur">${durStr}</div>
    </div>
  </div>`;
}

/* ══════════════════════════════════════════
   OVERVIEW PAGE
══════════════════════════════════════════ */
function renderOverview() {
  const u = getCurrentUser(); if (!u) return;
  const users = getUsers(); const user = users[u];
  const matches = getUserMatches(u);
  const stats = calcStats(matches);

  // Profile bar
  document.getElementById('ov-avatar').textContent = user.avatar || '⚡';
  document.getElementById('ov-name').textContent = user.name;
  document.getElementById('ov-role').textContent = (user.role || 'Mid') + ' Main';
  document.getElementById('ov-joined').textContent = 'Joined ' + (user.joined || '—');
  document.getElementById('ov-rank').textContent = user.rank || 'Unranked';
  document.getElementById('ov-lp').textContent = (user.lp || 0) + ' LP';

  if (stats) {
    document.getElementById('ov-wr').textContent   = stats.wr + '%';
    document.getElementById('ov-kda').textContent  = stats.kda;
    document.getElementById('ov-games').textContent= stats.n;
    document.getElementById('ov-cs').textContent   = stats.avgCS;
    document.getElementById('kpi-kda').innerHTML   = `${stats.avgK} <span class="hi-dim">/ ${stats.avgD} / ${stats.avgA}</span>`;
    document.getElementById('kpi-kda-sub').textContent = stats.n + ' games tracked';
    document.getElementById('kpi-kda-sub').className = 'kpi-change hi-blue';
    const dmgK = stats.avgDmg >= 1000 ? (stats.avgDmg/1000).toFixed(1) + 'k' : stats.avgDmg;
    document.getElementById('kpi-dmg').innerHTML = `${dmgK}`;
    document.getElementById('kpi-dmg-sub').textContent = 'per game';
    document.getElementById('kpi-dmg-sub').className = 'kpi-change hi-dim2';
    document.getElementById('kpi-dmg-bar').style.width = Math.min(100, Math.round(stats.avgDmg/500)) + '%';
    document.getElementById('kpi-dur').innerHTML = `${stats.avgDur}<span class="hi-dim">m</span>`;
    document.getElementById('kpi-dur-sub').textContent = 'avg game length';
    document.getElementById('kpi-dur-sub').className = 'kpi-change hi-dim2';
    document.getElementById('kpi-cs').innerHTML = `${stats.avgCS}`;
    document.getElementById('kpi-cs-sub').textContent = 'per game';
    document.getElementById('kpi-cs-sub').className = 'kpi-change hi-dim2';
    document.getElementById('kpi-cs-bar').style.width = Math.min(100, Math.round(stats.avgCS/3)) + '%';
  } else {
    ['ov-wr','ov-kda','ov-games','ov-cs'].forEach(id => document.getElementById(id).textContent = '—');
  }

  // Recent matches
  const el = document.getElementById('ov-matches-list');
  const recent = [...matches].reverse().slice(0, 6);
  el.innerHTML = recent.length ? recent.map(matchHTML).join('') : `<div class="empty-state"><div class="empty-icon">🎮</div><div class="empty-title">No games logged yet</div><div class="empty-sub">Click "Log Game" to add your first match</div><button class="btn btn-primary" onclick="openLogGame()">+ Log Game</button></div>`;

  // Top champs mini
  renderChampList(null, 'ov-champs', 5);
  // 7 day chart
  renderWeekChart();
  // Roles
  renderRoleChips();
}

/* ══════════════════════════════════════════
   CHAMPION PAGE
══════════════════════════════════════════ */
function getChampStats(matches, roleFilter) {
  const map = {};
  matches.forEach(m => {
    if (roleFilter && roleFilter !== 'all' && m.role !== roleFilter) return;
    if (!map[m.champ]) map[m.champ] = { champ: m.champ, icon: m.icon || '🎮', games: 0, wins: 0, k:0, d:0, a:0, cs:0, dmg:0, role: m.role };
    const c = map[m.champ];
    c.games++; if (m.result==='win') c.wins++;
    c.k += m.k||0; c.d += m.d||0; c.a += m.a||0;
    c.cs += m.cs||0; c.dmg += m.dmg||0;
  });
  return Object.values(map).sort((a,b) => b.games - a.games).map(c => ({
    ...c,
    wr: Math.round((c.wins/c.games)*100),
    kda: c.d===0 ? 'Perf' : ((c.k+c.a)/c.d/c.games).toFixed(2),
    avgCS: Math.round(c.cs/c.games),
    avgDmg: Math.round(c.dmg/c.games),
  }));
}

function renderChampList(roleFilter, targetId = 'champ-list', limit = 999) {
  const u = getCurrentUser(); if (!u) return;
  const matches = getUserMatches(u);
  const champs = getChampStats(matches, roleFilter).slice(0, limit);
  const el = document.getElementById(targetId);
  if (!el) return;
  el.innerHTML = champs.length ? champs.map((c,i) => `<div class="champ-row">
    <div class="cr-num">${String(i+1).padStart(2,'0')}</div>
    <div class="cr-portrait">${c.icon}</div>
    <div class="cr-info"><div class="cr-name">${c.champ}</div><div class="cr-games">${c.games} game${c.games>1?'s':''} · ${c.wins}W ${c.games-c.wins}L · ${c.role}</div></div>
    <div class="cr-stats">
      <div class="cr-s"><div class="cr-sv">${c.kda}</div><div class="cr-sl">KDA</div></div>
      <div class="cr-s"><div class="cr-sv">${c.avgCS}</div><div class="cr-sl">Avg CS</div></div>
    </div>
    <div class="wr ${wrClass(c.wr)}">${c.wr}%</div>
  </div>`).join('') : `<div class="empty-state"><div class="empty-icon">🗡️</div><div class="empty-title">No champions yet</div><div class="empty-sub">Log some games to see your champion stats</div></div>`;
}

function renderChampionPage() {
  const u = getCurrentUser(); if (!u) return;
  const matches = getUserMatches(u);
  const champs = getChampStats(matches, null);
  document.getElementById('champ-count-label').textContent = champs.length + ' champion' + (champs.length!==1?'s':'');
  if (champs.length) {
    const best = [...champs].sort((a,b) => b.wr - a.wr)[0];
    const most = champs[0];
    const worst = champs.length > 1 ? [...champs].sort((a,b) => a.wr - b.wr)[0] : null;
    document.getElementById('champ-best').textContent = best.champ;
    document.getElementById('champ-best-sub').textContent = best.wr + '% WR · ' + best.games + ' games';
    document.getElementById('champ-most').textContent = most.champ;
    document.getElementById('champ-most-sub').textContent = most.games + ' games · ' + most.role;
    if (worst) { document.getElementById('champ-worst').textContent = worst.champ; document.getElementById('champ-worst-sub').textContent = worst.wr + '% WR · ' + worst.games + ' games'; }
    else { document.getElementById('champ-worst').textContent = '—'; document.getElementById('champ-worst-sub').textContent = 'Need more data'; }
  }
  renderChampList(null);
  // Role WR bars
  const roles = ['Mid','Top','Bot','Jungle','Support'];
  const roleEl = document.getElementById('role-wr-bars');
  const colors = ['var(--accent)','var(--win)','var(--gold)','var(--text3)','#fca5a5'];
  roleEl.innerHTML = roles.map((r, i) => {
    const rm = matches.filter(m => m.role === r);
    if (!rm.length) return `<div class="prog-row"><span class="prog-label">${r}</span><div class="prog-track"><div class="prog-fill" style="width:0;background:${colors[i]}"></div></div><span class="prog-val hi-dim2">—</span></div>`;
    const wr = Math.round((rm.filter(m=>m.result==='win').length/rm.length)*100);
    return `<div class="prog-row"><span class="prog-label">${r}</span><div class="prog-track"><div class="prog-fill" style="width:${wr}%;background:${colors[i]}"></div></div><span class="prog-val">${wr}%</span></div>`;
  }).join('');
  // Summary
  const stats = calcStats(matches);
  const sumEl = document.getElementById('champ-summary');
  sumEl.innerHTML = stats ? `
    <div class="sum-cell"><div class="sum-val">${stats.avgCS}</div><div class="sum-lbl">Avg CS</div></div>
    <div class="sum-cell"><div class="sum-val">${stats.kda}</div><div class="sum-lbl">KDA</div></div>
    <div class="sum-cell"><div class="sum-val">${stats.avgDmg>=1000?(stats.avgDmg/1000).toFixed(1)+'k':stats.avgDmg}</div><div class="sum-lbl">Avg Dmg</div></div>
    <div class="sum-cell"><div class="sum-val">${stats.avgDur}m</div><div class="sum-lbl">Avg Dur</div></div>
    <div class="sum-cell"><div class="sum-val">${stats.wr}%</div><div class="sum-lbl">Win Rate</div></div>
    <div class="sum-cell"><div class="sum-val">${stats.n}</div><div class="sum-lbl">Games</div></div>` : '<div style="padding:20px;color:var(--text3);font-size:13px;text-align:center;grid-column:1/-1">No data yet</div>';
}

/* ══════════════════════════════════════════
   MATCH HISTORY PAGE
══════════════════════════════════════════ */
function renderMatchHistory(filter = 'all') {
  const u = getCurrentUser(); if (!u) return;
  const matches = [...getUserMatches(u)].reverse();
  const filtered = filter === 'all' ? matches : matches.filter(m => (filter==='wins'?m.result==='win':m.result==='loss'));
  document.getElementById('mh-list').innerHTML = filtered.length ? filtered.map(matchHTML).join('') : `<div class="empty-state"><div class="empty-icon">📋</div><div class="empty-title">No matches found</div><div class="empty-sub">${filter==='all'?'Click "+ Log Game" to record your first match.':'No '+filter+' to show.'}</div>${filter==='all'?'<button class="btn btn-primary" onclick="openLogGame()">+ Log Game</button>':''}</div>`;
  document.getElementById('mh-count-label').textContent = filtered.length + ' game' + (filtered.length!==1?'s':'');

  // stats
  const stats = calcStats(matches);
  document.getElementById('mh-total').textContent = matches.length;
  document.getElementById('mh-wr-label').textContent = stats ? stats.wr + '% win rate' : 'No games yet';
  document.getElementById('mh-wr-label').className = stats ? (stats.wr >= 50 ? 'kpi-change hi-green' : 'kpi-change hi-red') : 'kpi-change hi-dim2';

  // streak
  let streak = 0, lastRes = matches[0]?.result;
  for (const m of matches) { if (m.result === lastRes) streak++; else break; }
  document.getElementById('mh-streak').textContent = streak;
  document.getElementById('mh-streak-label').textContent = lastRes === 'win' ? '🔥 Win streak' : lastRes === 'loss' ? '❄️ Loss streak' : 'No games';

  // best kda
  if (matches.length) {
    const best = [...matches].sort((a,b) => parseFloat(calcRatio(b)) - parseFloat(calcRatio(a)))[0];
    document.getElementById('mh-bestkda').textContent = calcRatio(best);
    document.getElementById('mh-bestkda-label').textContent = `${best.k}/${best.d}/${best.a} · ${best.champ}`;
    const mostCS = [...matches].sort((a,b) => (b.cs||0) - (a.cs||0))[0];
    document.getElementById('mh-mostcs').textContent = mostCS.cs || 0;
    document.getElementById('mh-mostcs-label').textContent = mostCS.champ + ' · ' + mostCS.dur + 'min';
  }
}

/* ══════════════════════════════════════════
   PERFORMANCE PAGE
══════════════════════════════════════════ */
function renderPerformance() {
  const u = getCurrentUser(); if (!u) return;
  const matches = getUserMatches(u);
  const stats = calcStats(matches);
  if (!stats) {
    ['perf-wr','perf-kda','perf-cs','perf-dmg'].forEach(id => document.getElementById(id).textContent = '—');
    document.getElementById('perf-champ-bars').innerHTML = '<div style="color:var(--text3);font-size:13px">No games yet</div>';
    document.getElementById('perf-duration-body').innerHTML = '<tr><td colspan="4" style="color:var(--text3);text-align:center;padding:20px">No data</td></tr>';
    return;
  }
  document.getElementById('perf-wr').innerHTML = stats.wr + '<span class="hi-dim">%</span>';
  document.getElementById('perf-wr-bar').style.width = stats.wr + '%';
  document.getElementById('perf-kda').textContent = stats.kda;
  document.getElementById('perf-kda-bar').style.width = Math.min(100, parseFloat(stats.kda) * 12) + '%';
  document.getElementById('perf-cs').textContent = stats.avgCS;
  document.getElementById('perf-cs-bar').style.width = Math.min(100, Math.round(stats.avgCS/3)) + '%';
  const dmgK = stats.avgDmg >= 1000 ? (stats.avgDmg/1000).toFixed(1)+'k' : stats.avgDmg;
  document.getElementById('perf-dmg').textContent = dmgK;
  document.getElementById('perf-dmg-bar2').style.width = Math.min(100, Math.round(stats.avgDmg/500)) + '%';

  // champ bars
  const champs = getChampStats(matches, null).slice(0, 6);
  const colors = ['var(--accent)','var(--win)','var(--gold)','var(--text3)','#fca5a5','#a78bfa'];
  document.getElementById('perf-champ-bars').innerHTML = champs.length ? champs.map((c,i) =>
    `<div class="prog-row"><span class="prog-label">${c.champ}</span><div class="prog-track"><div class="prog-fill" style="width:${c.wr}%;background:${colors[i%colors.length]}"></div></div><span class="prog-val">${c.wr}%</span></div>`
  ).join('') : '<div style="color:var(--text3);font-size:13px">No data</div>';

  // duration table
  const buckets = [['< 20', m=>m.dur<20],['20–30',m=>m.dur>=20&&m.dur<30],['30–40',m=>m.dur>=30&&m.dur<40],['40–50',m=>m.dur>=40&&m.dur<50],['50+',m=>m.dur>=50]];
  document.getElementById('perf-duration-body').innerHTML = buckets.map(([label, fn]) => {
    const bm = matches.filter(fn);
    if (!bm.length) return `<tr><td>${label} min</td><td style="color:var(--text3)">0</td><td>—</td><td>—</td></tr>`;
    const bStats = calcStats(bm);
    const wrBadge = bStats.wr >= 60 ? 'b-win' : bStats.wr >= 50 ? 'b-gold' : 'b-loss';
    return `<tr><td>${label} min</td><td>${bm.length}</td><td><span class="badge ${wrBadge}">${bStats.wr}%</span></td><td>${bStats.kda}</td></tr>`;
  }).join('');
}

/* ══════════════════════════════════════════
   LEADERBOARD
══════════════════════════════════════════ */
function renderLeaderboard() {
  const users = getUsers();
  const rows = Object.values(users).map(u => {
    const matches = getUserMatches(u.username);
    const stats = calcStats(matches);
    return { ...u, stats, n: matches.length };
  }).filter(u => u.n > 0).sort((a, b) => (b.stats?.wr||0) - (a.stats?.wr||0));

  const el = document.getElementById('lb-list');
  const cur = getCurrentUser();
  document.getElementById('lb-count').textContent = rows.length + ' player' + (rows.length!==1?'s':'') + ' with games';

  if (!rows.length) { el.innerHTML = `<div class="empty-state"><div class="empty-icon">🏆</div><div class="empty-title">No players yet</div><div class="empty-sub">Be the first to log a game!</div></div>`; return; }

  const tierMap = { Challenger:'tier-chall',Grandmaster:'tier-gm',Master:'tier-master',Diamond:'tier-diamond',Platinum:'tier-plat',Gold:'tier-gold',Silver:'tier-silver',Bronze:'tier-silver',Iron:'tier-silver',Unranked:'tier-silver' };
  const rankIcons = {1:'🥇',2:'🥈',3:'🥉'};
  el.innerHTML = rows.map((u, i) => {
    const rank = i + 1;
    const rankClass = rank <= 3 ? ['top1','top2','top3'][rank-1] : '';
    const isYou = u.username === cur;
    return `<div class="lb-row" style="${isYou?'background:var(--accent-l)':''}">
      <div class="lb-rank ${rankClass}">${rankIcons[rank] || rank}</div>
      <div class="lb-av">${u.avatar||'⚡'}</div>
      <div class="lb-info">
        <div class="lb-name">${u.name || u.username}${isYou?' <span class="badge b-blue" style="font-size:9px">You</span>':''}</div>
        <div class="lb-server">${u.role||'Mid'} · ${u.rank||'Unranked'}</div>
      </div>
      <div class="lb-stats">
        <div class="lb-s"><div class="lb-sv">${u.stats?.wr||0}%</div><div class="lb-sl">Win Rate</div></div>
        <div class="lb-s"><div class="lb-sv">${u.stats?.kda||'—'}</div><div class="lb-sl">KDA</div></div>
        <div class="lb-s"><div class="lb-sv">${u.n}</div><div class="lb-sl">Games</div></div>
      </div>
      <div class="tier-badge ${tierMap[u.rank||'Unranked']||'tier-silver'}">${u.rank||'Unranked'}</div>
    </div>`;
  }).join('');
}

/* ══════════════════════════════════════════
   FRIENDS SEARCH
══════════════════════════════════════════ */
function searchPlayers() {
  const q = document.getElementById('friend-search').value.trim().toLowerCase();
  const users = getUsers();
  const cur = getCurrentUser();
  const results = Object.values(users).filter(u => u.username !== cur && (u.username.includes(q) || (u.name||'').toLowerCase().includes(q)));
  const el = document.getElementById('friend-results');
  if (!q) { el.innerHTML = ''; return; }
  el.innerHTML = results.length ? results.map(u => {
    const matches = getUserMatches(u.username);
    const stats = calcStats(matches);
    return `<div class="lb-row">
      <div class="lb-av">${u.avatar||'⚡'}</div>
      <div class="lb-info"><div class="lb-name">${u.name||u.username}</div><div class="lb-server">${u.role||'Mid'} · ${u.rank||'Unranked'} · ${matches.length} games</div></div>
      <div class="lb-stats"><div class="lb-s"><div class="lb-sv">${stats?.wr||0}%</div><div class="lb-sl">WR</div></div><div class="lb-s"><div class="lb-sv">${stats?.kda||'—'}</div><div class="lb-sl">KDA</div></div></div>
    </div>`;
  }).join('') : `<div class="empty-state"><div class="empty-icon">👤</div><div class="empty-title">No players found</div><div class="empty-sub">Try a different search</div></div>`;
}
document.getElementById('friend-search').addEventListener('keydown', e => { if (e.key === 'Enter') searchPlayers(); });

/* ══════════════════════════════════════════
   SETTINGS
══════════════════════════════════════════ */
function renderSettings() {
  const u = getCurrentUser(); if (!u) return;
  const users = getUsers(); const user = users[u];
  document.getElementById('set-name').value = user.name || '';
  document.getElementById('set-role').value = user.role || 'Mid';
  document.getElementById('set-rank').value = user.rank || 'Unranked';
  document.getElementById('set-lp').value = user.lp || 0;
  document.querySelectorAll('.av-opt').forEach(opt => opt.classList.toggle('selected', opt.dataset.av === (user.avatar||'⚡')));
}

document.querySelectorAll('.av-opt').forEach(opt => {
  opt.addEventListener('click', () => {
    document.querySelectorAll('.av-opt').forEach(o => o.classList.remove('selected'));
    opt.classList.add('selected');
  });
});

function saveSettings() {
  const u = getCurrentUser(); if (!u) return;
  const users = getUsers();
  users[u].name = document.getElementById('set-name').value.trim() || users[u].name;
  users[u].role = document.getElementById('set-role').value;
  users[u].rank = document.getElementById('set-rank').value;
  users[u].lp   = parseInt(document.getElementById('set-lp').value) || 0;
  const selAv = document.querySelector('.av-opt.selected');
  if (selAv) users[u].avatar = selAv.dataset.av;
  saveUsers(users);
  updateSidebar();
  renderOverview();
  showToast('Settings saved!', 'success');
}

function clearMatchHistory() {
  if (!confirm('Delete all your match history? This cannot be undone.')) return;
  const u = getCurrentUser(); if (!u) return;
  saveUserMatches(u, []);
  refreshAllPages();
  showToast('Match history cleared.', 'success');
}

/* ══════════════════════════════════════════
   CHARTS & CHIPS
══════════════════════════════════════════ */
function renderWeekChart() {
  const u = getCurrentUser(); if (!u) return;
  const matches = getUserMatches(u);
  const el = document.getElementById('ov-chart'); if (!el) return;
  const days = ['MON','TUE','WED','THU','FRI','SAT','SUN'];
  const today = new Date().getDay();
  const data = days.map((d, i) => {
    const dayIdx = (i + 1) % 7; // 0=Sun
    const dayMatches = matches.filter(m => new Date(m.date).getDay() === dayIdx);
    return { d, w: dayMatches.filter(m=>m.result==='win').length, l: dayMatches.filter(m=>m.result==='loss').length };
  });
  const max = Math.max(1, ...data.map(d => d.w + d.l));
  el.innerHTML = '';
  el.style.height = '90px';
  data.forEach(d => {
    const g = document.createElement('div'); g.className = 'bcol';
    const wH = Math.round((d.w/max)*74), lH = Math.round((d.l/max)*74);
    g.innerHTML = `<div class="bcol-bars"><div class="bseg bw" style="height:${Math.max(d.w?2:0,wH)}px" title="${d.w}W"></div><div class="bseg bl" style="height:${Math.max(d.l?2:0,lH)}px" title="${d.l}L"></div></div><div class="bday">${d.d}</div>`;
    el.appendChild(g);
  });
}

function renderRoleChips() {
  const u = getCurrentUser(); if (!u) return;
  const matches = getUserMatches(u);
  const roles = ['Mid','Top','Bot','Jungle','Support'];
  const icons = {Mid:'✨',Top:'🗡️',Bot:'🏹',Jungle:'🌿',Support:'🛡️'};
  const el = document.getElementById('role-chips'); if (!el) return;
  el.innerHTML = roles.map((r, i) => {
    const pct = matches.length ? Math.round((matches.filter(m=>m.role===r).length / matches.length) * 100) : 0;
    return `<div class="role-chip ${i===0?'active':''}" onclick="this.parentElement.querySelectorAll('.role-chip').forEach(c=>c.classList.remove('active'));this.classList.add('active')">
      <div class="rc-icon">${icons[r]}</div><div class="rc-name">${r}</div><div class="rc-pct">${pct}%</div>
    </div>`;
  }).join('');
}

/* ══════════════════════════════════════════
   LOG GAME MODAL
══════════════════════════════════════════ */
let screenshotBase64 = null;
let manualVisible = false;

function openLogGame() {
  document.getElementById('log-modal').classList.add('open');
  resetLogForm();
}
function closeLogGame() {
  document.getElementById('log-modal').classList.remove('open');
}

function resetLogForm() {
  screenshotBase64 = null;
  document.getElementById('screenshot-preview').style.display = 'none';
  document.getElementById('ai-reading').classList.remove('show');
  document.getElementById('extracted-form').classList.remove('show');
  document.getElementById('extracted-note').style.display = 'none';
  document.getElementById('manual-toggle').style.display = '';
  document.getElementById('save-game-btn').disabled = true;
  ['f-champ','f-k','f-d','f-a','f-cs','f-dmg','f-dur','f-notes'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('f-result').value = 'win';
  document.getElementById('f-role').value = 'Mid';
  document.getElementById('f-mode').value = 'Ranked';
  document.getElementById('f-icon').value = '🧙';
  manualVisible = false;
  document.getElementById('manual-toggle').textContent = '✏️ Fill in manually instead';
}

function toggleManual() {
  manualVisible = !manualVisible;
  const ef = document.getElementById('extracted-form');
  ef.classList.toggle('show', manualVisible);
  document.getElementById('manual-toggle').textContent = manualVisible ? '↑ Hide manual form' : '✏️ Fill in manually instead';
  document.getElementById('save-game-btn').disabled = !manualVisible;
}

async function handleScreenshot(input) {
  const file = input.files[0]; if (!file) return;
  // Show preview
  const reader = new FileReader();
  reader.onload = async e => {
    const preview = document.getElementById('screenshot-preview');
    preview.src = e.target.result;
    preview.style.display = 'block';
    screenshotBase64 = e.target.result.split(',')[1];
    // Show AI reading
    document.getElementById('ai-reading').classList.add('show');
    document.getElementById('manual-toggle').style.display = 'none';
    try {
      const stats = await readScreenshotWithAI(screenshotBase64, file.type || 'image/png');
      populateForm(stats, true);
    } catch(err) {
      document.getElementById('ai-reading').classList.remove('show');
      showToast('Could not read screenshot — please fill in manually.', 'error');
      toggleManual();
    }
  };
  reader.readAsDataURL(file);
}

async function readScreenshotWithAI(base64, mediaType) {
  const res = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      model: 'claude-sonnet-4-20250514',
      max_tokens: 1000,
      messages: [{
        role: 'user',
        content: [
          {
            type: 'image',
            source: { type: 'base64', media_type: mediaType, data: base64 }
          },
          {
            type: 'text',
            text: `You are a MOBA game stats reader. Look at this end-of-game screenshot and extract the player's stats.
Return ONLY valid JSON with these fields (use null if you cannot find a value):
{
  "champion": "champion name as string",
  "kills": number,
  "deaths": number,
  "assists": number,
  "cs": number or null,
  "damage": number or null,
  "duration_minutes": number or null,
  "result": "win" or "loss",
  "role": "Mid" or "Top" or "Bot" or "Jungle" or "Support" or null
}
Return ONLY the JSON object, no other text.`
          }
        ]
      }]
    })
  });
  if (!res.ok) throw new Error('API error');
  const data = await res.json();
  const text = data.content?.[0]?.text || '';
  const clean = text.replace(/```json|```/g, '').trim();
  return JSON.parse(clean);
}

function populateForm(stats, fromAI) {
  document.getElementById('ai-reading').classList.remove('show');
  document.getElementById('extracted-form').classList.add('show');
  if (fromAI) document.getElementById('extracted-note').style.display = 'flex';
  document.getElementById('manual-toggle').style.display = 'none';
  if (stats.champion)       document.getElementById('f-champ').value = stats.champion;
  if (stats.kills   != null) document.getElementById('f-k').value = stats.kills;
  if (stats.deaths  != null) document.getElementById('f-d').value = stats.deaths;
  if (stats.assists != null) document.getElementById('f-a').value = stats.assists;
  if (stats.cs      != null) document.getElementById('f-cs').value = stats.cs;
  if (stats.damage  != null) document.getElementById('f-dmg').value = stats.damage;
  if (stats.duration_minutes != null) document.getElementById('f-dur').value = stats.duration_minutes;
  if (stats.result)         document.getElementById('f-result').value = stats.result;
  if (stats.role)           document.getElementById('f-role').value = stats.role;
  document.getElementById('save-game-btn').disabled = false;
}

function saveGame() {
  const champ = document.getElementById('f-champ').value.trim();
  const k = parseInt(document.getElementById('f-k').value);
  const d = parseInt(document.getElementById('f-d').value);
  const a = parseInt(document.getElementById('f-a').value);
  if (!champ) { showToast('Please enter a champion name.', 'error'); return; }
  if (isNaN(k) || isNaN(d) || isNaN(a)) { showToast('Please enter K/D/A values.', 'error'); return; }
  const u = getCurrentUser(); if (!u) return;
  const matches = getUserMatches(u);
  const newMatch = {
    id: Date.now(),
    champ,
    icon: document.getElementById('f-icon').value,
    k, d, a,
    cs:   parseInt(document.getElementById('f-cs').value)  || 0,
    dmg:  parseInt(document.getElementById('f-dmg').value) || 0,
    dur:  parseInt(document.getElementById('f-dur').value) || 0,
    role: document.getElementById('f-role').value,
    result: document.getElementById('f-result').value,
    mode: document.getElementById('f-mode').value,
    notes: document.getElementById('f-notes').value.trim(),
    date: new Date().toISOString(),
  };
  matches.push(newMatch);
  saveUserMatches(u, matches);
  closeLogGame();
  refreshAllPages();
  showToast('Game logged! 🎮', 'success');
}

/* ══════════════════════════════════════════
   REFRESH ALL
══════════════════════════════════════════ */
function refreshAllPages() {
  renderOverview();
  renderChampionPage();
  renderMatchHistory();
  renderPerformance();
  renderLeaderboard();
  renderSettings();
}

/* ══════════════════════════════════════════
   TOAST
══════════════════════════════════════════ */
function showToast(msg, type = '') {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast ' + type;
  requestAnimationFrame(() => t.classList.add('show'));
  setTimeout(() => t.classList.remove('show'), 3000);
}

/* ══════════════════════════════════════════
   TABS
══════════════════════════════════════════ */
function initTabs(groupId, onSelect) {
  const group = document.getElementById(groupId); if (!group) return;
  group.querySelectorAll('.tab').forEach((t, i) => {
    t.addEventListener('click', () => {
      group.querySelectorAll('.tab').forEach(x => x.classList.remove('active'));
      t.classList.add('active');
      onSelect(i, t.textContent.trim().toLowerCase());
    });
  });
}
initTabs('tabs-matches', (i, label) => renderMatchHistory(label === 'all' ? 'all' : label === 'wins' ? 'wins' : 'losses'));

/* Champion filter pills */
document.querySelectorAll('[data-cfilter]').forEach(pill => {
  pill.addEventListener('click', () => {
    pill.closest('.filter-bar').querySelectorAll('[data-cfilter]').forEach(p => p.classList.remove('active'));
    pill.classList.add('active');
    renderChampList(pill.dataset.cfilter === 'all' ? null : pill.dataset.cfilter);
  });
});

/* ══════════════════════════════════════════
   DRAG & DROP
══════════════════════════════════════════ */
const zone = document.getElementById('upload-zone');
if (zone) {
  zone.addEventListener('dragover', e => { e.preventDefault(); zone.classList.add('drag'); });
  zone.addEventListener('dragleave', () => zone.classList.remove('drag'));
  zone.addEventListener('drop', e => {
    e.preventDefault(); zone.classList.remove('drag');
    const file = e.dataTransfer.files[0];
    if (file && file.type.startsWith('image/')) {
      const input = document.getElementById('screenshot-input');
      const dt = new DataTransfer(); dt.items.add(file); input.files = dt.files;
      handleScreenshot(input);
    }
  });
}

/* Close modal on overlay click */
document.getElementById('log-modal').addEventListener('click', e => { if (e.target === document.getElementById('log-modal')) closeLogGame(); });

/* ══════════════════════════════════════════
   AUTO LOGIN (if session exists)
══════════════════════════════════════════ */
window.addEventListener('DOMContentLoaded', () => {
  const cur = getCurrentUser();
  if (cur && getUsers()[cur]) launchApp();
});
</script>
</body>
</html>
