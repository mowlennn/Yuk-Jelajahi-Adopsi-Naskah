<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Adopsi Naskah · Hukum Perjanjian Internasional</title>
<script>document.documentElement.classList.add('js');</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500&family=IBM+Plex+Sans:wght@400;500;600;700&family=Newsreader:ital,opsz,wght@0,6..72,300;0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400;1,6..72,500;1,6..72,600&display=swap" rel="stylesheet">
<script defer src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script defer src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script defer src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
:root{
    --bg:#080F18;
    --bg-soft:#0C1622;
    --ink:#0A121C;
    --ink-2:#0E1A28;
    --ink-3:#0A1420;
    --panel:rgba(18,32,47,.72);
    --panel-solid:#12202F;
    --glass-line:rgba(160,190,220,.14);
    --paper:#EFE9DA;
    --paper-2:#F6F1E6;
    --paper-light:#EDE7D8;
    --muted:#9DAABC;
    --muted-dark:#8593A6;
    --line-dark:rgba(200,150,58,.22);
    --teal:#1E7A6E;
    --teal-bright:#3FB8A6;
    --gold:#C8963A;
    --gold-soft:#9d7c3e;
    --claret:#B5432F;
    --claret-bright:#E0654E;
    --font-display:'Newsreader',serif;
    --font-body:'IBM Plex Sans',system-ui,sans-serif;
    --font-mono:'IBM Plex Mono',monospace;
    --rail:270px;
    --maxw:1180px;
    --readw:720px;
}
*{box-sizing:border-box;}
html{scroll-behavior:smooth;}
html.js.gsap-ready{scroll-behavior:auto;}
body{
    margin:0;background:var(--bg);color:var(--paper-light);
    font-family:var(--font-body);font-size:17px;line-height:1.68;
    -webkit-font-smoothing:antialiased;overflow-x:hidden;
}
::selection{background:rgba(63,184,166,.28);color:#fff;}
h1,h2,h3{font-family:var(--font-display);margin:0;color:var(--paper-light);line-height:1.08;font-weight:400;letter-spacing:-.015em;}
h2{font-size:clamp(2rem,4.4vw,3.3rem);}
h3{font-weight:500;}
p{margin:0 0 1rem;}
a{color:inherit;text-decoration:none;}
em{font-style:italic;}
:focus-visible{outline:2px solid var(--teal-bright);outline-offset:3px;border-radius:2px;}

/* ---- scrollbar ---- */
::-webkit-scrollbar{width:11px;}
::-webkit-scrollbar-track{background:var(--ink-3);}
::-webkit-scrollbar-thumb{background:#2a3d52;border-radius:8px;border:2px solid var(--ink-3);}
::-webkit-scrollbar-thumb:hover{background:var(--teal);}

/* ---- preloader ---- */
#preloader{
    position:fixed;inset:0;z-index:600;background:var(--bg);
    display:flex;flex-direction:column;align-items:center;justify-content:center;gap:1.3rem;
    transition:opacity .7s ease,visibility .7s ease;
}
#preloader.hide{opacity:0;visibility:hidden;pointer-events:none;}
.pre-mark{font-family:var(--font-display);font-style:italic;font-size:2rem;color:var(--paper-light);letter-spacing:-.02em;}
.pre-bar{width:190px;height:2px;background:rgba(160,190,220,.16);border-radius:2px;overflow:hidden;}
.pre-bar span{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--teal),var(--teal-bright));animation:preload 1.25s ease forwards;}
@keyframes preload{to{width:100%;}}
.pre-sub{font-family:var(--font-mono);font-size:.62rem;letter-spacing:.24em;text-transform:uppercase;color:var(--muted-dark);}

/* ---- 3D canvas ---- */
#bg3d{position:fixed;inset:0;width:100%;height:100%;z-index:0;pointer-events:none;opacity:1;transition:opacity .6s ease;}
.bg-aurora{position:fixed;inset:0;z-index:-1;pointer-events:none;
    background:
      radial-gradient(50% 55% at 78% 18%, rgba(63,184,166,.16), transparent 60%),
      radial-gradient(45% 50% at 12% 82%, rgba(200,150,58,.12), transparent 62%),
      radial-gradient(60% 60% at 50% 120%, rgba(181,67,47,.08), transparent 60%);
}

/* ---- scroll progress ---- */
.progress{position:fixed;top:0;left:0;height:3px;width:100%;transform:scaleX(0);transform-origin:0 50%;
    background:linear-gradient(90deg,var(--teal-bright),var(--gold));z-index:200;}

/* ---- side rail ---- */
.rail{
    position:fixed;top:0;left:0;height:100vh;width:var(--rail);z-index:120;
    padding:2.4rem 1.5rem;overflow-y:auto;
    background:linear-gradient(180deg,rgba(8,15,24,.9),rgba(8,15,24,.72));
    backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);
    border-right:1px solid var(--glass-line);
}
.rail__brand{font-family:var(--font-mono);font-size:.6rem;letter-spacing:.14em;color:var(--muted-dark);text-transform:uppercase;margin-bottom:2.1rem;line-height:1.7;}
.rail__brand strong{font-family:var(--font-display);font-style:italic;text-transform:none;letter-spacing:-.01em;color:var(--paper-light);display:block;font-size:1.5rem;margin-bottom:.4rem;font-weight:500;}
.rail__label{font-family:var(--font-mono);font-size:.55rem;letter-spacing:.24em;color:var(--gold);text-transform:uppercase;padding-bottom:.8rem;margin-bottom:.5rem;border-bottom:1px solid var(--glass-line);}
.rail nav{display:flex;flex-direction:column;}
.rail nav a{display:flex;gap:.6rem;padding:.42rem 0 .42rem .8rem;color:var(--muted-dark);font-family:var(--font-mono);font-size:.73rem;letter-spacing:.01em;border-left:2px solid rgba(160,190,220,.1);transition:color .25s,border-color .25s;line-height:1.4;}
.rail nav a .lead{color:var(--gold-soft);flex:none;min-width:1.1em;}
.rail nav a:hover{color:var(--paper-light);border-left-color:var(--gold-soft);}
.rail nav a.active{color:var(--paper-light);border-left-color:var(--teal-bright);}
.rail nav a.active .lead{color:var(--teal-bright);}
.rail nav a.sub{padding-left:1.8rem;font-size:.7rem;color:#6f7c90;}
.rail nav a.sub .lead{min-width:1.4em;}
.rail .gap{height:.9rem;}

/* ---- mobile bar ---- */
.mobile-bar{display:none;position:fixed;top:0;left:0;right:0;height:58px;z-index:130;background:rgba(8,15,24,.92);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);align-items:center;justify-content:space-between;padding:0 1.2rem;border-bottom:1px solid var(--glass-line);}
.mobile-bar__title{font-family:var(--font-display);font-style:italic;font-size:1.15rem;color:var(--paper-light);}
.nav-toggle{background:none;border:1px solid var(--gold-soft);color:var(--paper-light);font-family:var(--font-mono);font-size:.64rem;letter-spacing:.08em;text-transform:uppercase;padding:.44rem .72rem;border-radius:5px;cursor:pointer;}

.content{margin-left:var(--rail);position:relative;z-index:1;}

@media (max-width:960px){
    .mobile-bar{display:flex;}
    .rail{transform:translateX(-100%);transition:transform .35s cubic-bezier(.4,0,.2,1);top:58px;height:calc(100vh - 58px);width:280px;box-shadow:14px 0 40px rgba(0,0,0,.4);}
    .rail.open{transform:translateX(0);}
    .content{margin-left:0;padding-top:58px;}
}

/* ---- section shells ---- */
.section{position:relative;padding:7rem 2.4rem;}
.section__in{max-width:var(--maxw);margin:0 auto;}
.read{max-width:var(--readw);}
@media (max-width:760px){.section{padding:4.4rem 1.3rem;}}

.eyebrow{font-family:var(--font-mono);font-size:.68rem;letter-spacing:.2em;text-transform:uppercase;color:var(--gold);margin-bottom:1.1rem;display:flex;align-items:center;gap:.75rem;}
.eyebrow .num{color:var(--claret-bright);font-weight:500;border:1px solid var(--claret);border-radius:6px;min-width:1.7em;height:1.7em;display:inline-flex;align-items:center;justify-content:center;font-size:.64rem;padding:0 .35em;}
.lead-p{color:var(--muted);font-size:1.08rem;margin-top:1.2rem;}
.big-lead{font-family:var(--font-display);font-size:clamp(1.25rem,2.3vw,1.7rem);line-height:1.45;color:var(--paper-light);font-weight:300;margin-top:1.4rem;}
.big-lead b{color:var(--teal-bright);font-weight:500;}

/* editorial two-column with sticky label */
.ed{display:grid;grid-template-columns:.34fr .66fr;gap:2.6rem;align-items:start;}
.ed__label{position:sticky;top:120px;}
.ed__label .k{font-family:var(--font-mono);font-size:.66rem;letter-spacing:.16em;text-transform:uppercase;color:var(--gold-soft);}
.ed__label h2{margin-top:.8rem;}
@media (max-width:860px){.ed{grid-template-columns:1fr;gap:1.4rem;}.ed__label{position:static;}}

/* statement full-bleed */
.statement h2{font-size:clamp(2.1rem,5vw,4rem);font-weight:300;max-width:16ch;}
.statement .pull-accent{color:var(--teal-bright);font-style:italic;}

/* glass panel */
.panel{background:var(--panel);border:1px solid var(--glass-line);border-radius:16px;padding:2rem 1.9rem;backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);box-shadow:0 24px 60px rgba(0,0,0,.32);}
@media (max-width:760px){.panel{padding:1.5rem 1.3rem;}}

/* numbered list (de-cards) */
.numlist{list-style:none;margin:1.8rem 0 0;padding:0;counter-reset:nl;}
.numlist>li{position:relative;padding:1.5rem 0 1.5rem 4.2rem;border-top:1px solid var(--glass-line);counter-increment:nl;}
.numlist>li:last-child{border-bottom:1px solid var(--glass-line);}
.numlist>li::before{content:counter(nl,decimal-leading-zero);position:absolute;left:0;top:1.4rem;font-family:var(--font-mono);font-size:.85rem;color:var(--teal-bright);letter-spacing:.05em;}
.numlist h3{font-size:1.22rem;margin-bottom:.4rem;color:var(--paper-light);}
.numlist p{color:var(--muted);margin:0;font-size:.99rem;}
.numlist .tag{font-family:var(--font-mono);font-size:.62rem;letter-spacing:.1em;text-transform:uppercase;color:var(--gold);display:block;margin-bottom:.45rem;}

/* connected vertical timeline */
.flow{list-style:none;margin:1.8rem 0 0;padding:0;position:relative;}
.flow::before{content:"";position:absolute;left:11px;top:6px;bottom:6px;width:2px;background:linear-gradient(180deg,var(--teal),var(--gold-soft));opacity:.4;}
.flow li{position:relative;padding:0 0 1.5rem 3rem;}
.flow li:last-child{padding-bottom:0;}
.flow .node{position:absolute;left:2px;top:2px;width:22px;height:22px;border-radius:50%;background:var(--ink-2);border:2px solid var(--teal-bright);display:flex;align-items:center;justify-content:center;font-family:var(--font-mono);font-size:.62rem;color:var(--teal-bright);}
.flow strong{color:var(--paper-light);font-weight:600;}
.flow p{color:var(--muted);margin:.2rem 0 0;font-size:.97rem;}

/* pro / con split */
.split{display:grid;grid-template-columns:1fr 1fr;gap:1.3rem;margin-top:1.8rem;}
@media (max-width:640px){.split{grid-template-columns:1fr;}}
.split__col{background:var(--panel);border:1px solid var(--glass-line);border-radius:14px;padding:1.5rem 1.4rem;backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);}
.split__col--good{border-top:3px solid var(--teal-bright);}
.split__col--bad{border-top:3px solid var(--claret-bright);}
.split__col h3{font-size:1.05rem;margin-bottom:.5rem;}
.split__col p{color:var(--muted);margin:0;font-size:.96rem;}

/* stat block with counters */
.statgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:1.2rem;margin-top:1.8rem;}
@media (max-width:640px){.statgrid{grid-template-columns:1fr;}}
.stat{background:var(--panel);border:1px solid var(--glass-line);border-radius:14px;padding:1.5rem 1.4rem;text-align:center;backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);}
.stat__num{font-family:var(--font-display);font-size:2.9rem;line-height:1;color:var(--paper-light);}
.stat--yes .stat__num{color:var(--teal-bright);}
.stat--no .stat__num{color:var(--claret-bright);}
.stat--abs .stat__num{color:var(--muted);}
.stat__lab{font-family:var(--font-mono);font-size:.64rem;letter-spacing:.1em;text-transform:uppercase;color:var(--muted-dark);margin-top:.6rem;}

.pull{border-left:3px solid var(--teal-bright);padding:.4rem 0 .4rem 1.4rem;margin:2rem 0 0;font-family:var(--font-display);font-style:italic;font-size:clamp(1.3rem,2.4vw,1.7rem);line-height:1.4;color:var(--paper-light);}
.subhead{font-family:var(--font-mono);font-size:.68rem;letter-spacing:.16em;text-transform:uppercase;color:var(--gold-soft);margin:2.8rem 0 .9rem;display:flex;align-items:center;gap:.7rem;}
.subhead::before{content:"";width:24px;height:1px;background:var(--gold);flex:none;}

/* paper contrast panel */
.paper-panel{background:linear-gradient(180deg,var(--paper-2),var(--paper));color:#22303f;border-radius:16px;padding:2.2rem;box-shadow:0 30px 70px rgba(0,0,0,.4);}
.compare{width:100%;border-collapse:collapse;font-size:.94rem;}
.compare caption{text-align:left;font-family:var(--font-mono);font-size:.66rem;letter-spacing:.12em;text-transform:uppercase;color:var(--gold-soft);margin-bottom:1rem;}
.compare th,.compare td{text-align:left;padding:.9rem 1rem;border-bottom:1px solid rgba(34,48,63,.14);vertical-align:top;}
.compare tr:last-child td{border-bottom:none;}
.compare th{font-family:var(--font-mono);font-size:.64rem;letter-spacing:.06em;text-transform:uppercase;color:var(--teal);}
.compare td{color:#4a5a6b;}
.compare td:first-child{color:#22303f;font-weight:600;}
.compare em{color:var(--teal);}
.table-scroll{overflow-x:auto;-webkit-overflow-scrolling:touch;}
@media (max-width:640px){
    .paper-panel{padding:1.4rem;}
    .compare{min-width:480px;}
    .table-scroll{margin:0 -.2rem;}
}

/* ---- HERO ---- */
.hero{position:relative;min-height:100vh;display:flex;flex-direction:column;justify-content:center;padding:7rem 2.4rem 4rem;overflow:hidden;}
.hero__grid{max-width:var(--maxw);margin:0 auto;width:100%;position:relative;z-index:2;}
.hero .eyebrow{color:var(--gold);}
.hero h1{font-size:clamp(3.2rem,9vw,7rem);line-height:.92;font-weight:400;letter-spacing:-.03em;margin-top:.3rem;}
.hero h1 .l2{color:var(--teal-bright);font-style:italic;font-weight:400;}
.hero h1 .word{display:inline-block;}
.hero__lede{font-size:1.18rem;color:#c3cedb;max-width:44ch;margin-top:1.8rem;line-height:1.6;}
.hero__meta{margin-top:2rem;display:flex;gap:1.6rem;flex-wrap:wrap;font-family:var(--font-mono);font-size:.68rem;letter-spacing:.08em;text-transform:uppercase;color:var(--muted-dark);}
.hero__meta b{color:var(--gold);font-weight:500;}
.scroll-cue{margin-top:2.6rem;font-family:var(--font-mono);font-size:.66rem;letter-spacing:.14em;text-transform:uppercase;color:var(--gold-soft);display:inline-flex;align-items:center;gap:.6rem;}
.scroll-cue::after{content:"";width:1px;height:26px;background:linear-gradient(var(--gold-soft),transparent);animation:cue 1.8s ease-in-out infinite;}
@keyframes cue{0%,100%{transform:scaleY(.5);opacity:.4;}50%{transform:scaleY(1);opacity:1;}}

/* ---- process horizontal ---- */
.process-outer{position:relative;background:linear-gradient(180deg,transparent,rgba(10,20,32,.6),transparent);}
.process-vp{overflow:hidden;}
.process-track{display:flex;gap:1.5rem;padding:1rem 0;width:max-content;}
.pstep{width:340px;flex:none;background:var(--panel);border:1px solid var(--glass-line);border-radius:16px;padding:1.7rem 1.6rem;backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);}
.pstep.is-here{border-color:var(--teal-bright);box-shadow:0 0 0 1px rgba(63,184,166,.35),0 24px 50px rgba(0,0,0,.3);}
.pstep__n{font-family:var(--font-mono);font-size:.72rem;color:var(--gold);letter-spacing:.08em;}
.pstep h3{font-size:1.35rem;margin:.6rem 0 .5rem;}
.pstep p{color:var(--muted);margin:0;font-size:.97rem;}
.pstep__art{font-family:var(--font-display);font-size:3.4rem;line-height:1;color:rgba(63,184,166,.28);margin-bottom:.6rem;}
.process-hint{font-family:var(--font-mono);font-size:.62rem;letter-spacing:.14em;text-transform:uppercase;color:var(--muted-dark);margin-top:1.4rem;}
@media (max-width:960px){
    .process-track{flex-direction:column;width:auto;}
    .pstep{width:auto;}
}

/* ---- Ahli slider ---- */
.ahli-wrap{position:relative;margin-top:2rem;}
.ahli-slider{display:flex;overflow:hidden;border-radius:18px;background:var(--panel);border:1px solid var(--glass-line);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);box-shadow:0 30px 70px rgba(0,0,0,.34);}
.ahli-slide{flex:0 0 100%;display:flex;flex-wrap:wrap;align-items:center;gap:2.2rem;padding:2.6rem;opacity:0;visibility:hidden;transition:opacity .35s ease;position:absolute;top:0;left:0;width:100%;}
.ahli-slide.active{opacity:1;visibility:visible;position:relative;}
.ahli-foto{flex-shrink:0;width:120px;height:120px;border-radius:50%;background:#3D4B60;border:2px solid var(--gold);display:flex;align-items:center;justify-content:center;overflow:hidden;}
.ahli-foto svg{width:58%;height:58%;flex-shrink:0;fill:#B8C2D1;}
.ahli-teks{flex:1;min-width:220px;}
.ahli-teks .idx{font-family:var(--font-mono);font-size:.66rem;letter-spacing:.1em;color:var(--claret-bright);text-transform:uppercase;display:block;margin-bottom:.5rem;}
.ahli-teks h3{font-size:1.4rem;margin-bottom:.6rem;}
.ahli-teks p{color:var(--muted);margin:0;font-size:1rem;}
.ahli-teks .who{display:block;margin-top:.9rem;font-family:var(--font-mono);font-size:.7rem;letter-spacing:.06em;color:var(--gold);text-transform:uppercase;}
.slider-arrow{position:absolute;top:50%;transform:translateY(-50%);background:var(--panel-solid);border:1px solid var(--teal-bright);color:var(--teal-bright);font-size:1.3rem;width:46px;height:46px;border-radius:50%;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:.2s;z-index:10;}
.slider-arrow:hover{background:var(--teal-bright);color:var(--ink);}
.slider-arrow--left{left:-22px;}.slider-arrow--right{right:-22px;}
.ahli-dots{display:flex;gap:.5rem;justify-content:center;margin-top:1.2rem;}
.ahli-dots button{width:9px;height:9px;border-radius:50%;border:none;background:rgba(160,190,220,.22);cursor:pointer;padding:0;transition:.2s;}
.ahli-dots button.active{background:var(--teal-bright);transform:scale(1.35);}
@media (max-width:700px){.ahli-slide{flex-direction:column;text-align:center;padding:2rem 1.4rem;}.ahli-foto{width:96px;height:96px;}.slider-arrow{width:36px;height:36px;font-size:1rem;}.slider-arrow--left{left:-8px;}.slider-arrow--right{right:-8px;}}

/* ---- simulations ---- */
.sim{background:var(--panel);border:1px solid var(--glass-line);border-radius:16px;padding:1.9rem 1.8rem;margin-top:1.9rem;backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);box-shadow:0 24px 60px rgba(0,0,0,.3);}
.sim__head{display:flex;align-items:baseline;justify-content:space-between;gap:1rem;flex-wrap:wrap;margin-bottom:1.3rem;}
.sim__title{font-family:var(--font-mono);font-size:.68rem;letter-spacing:.12em;text-transform:uppercase;color:var(--teal-bright);}
.sim__title::before{content:"\25C6\00a0";color:var(--gold);}
.sim__hint{font-family:var(--font-mono);font-size:.64rem;color:var(--muted-dark);}
.floor{display:flex;flex-wrap:wrap;gap:.55rem;margin-bottom:1.2rem;}
.seat{width:32px;height:32px;border-radius:50% 50% 46% 46%;border:2px solid var(--muted-dark);background:transparent;cursor:pointer;position:relative;transition:.28s;padding:0;}
.seat:hover{border-color:var(--paper-light);}
.seat.agree{border-color:var(--teal-bright);background:var(--teal);}
.seat.object{border-color:var(--claret-bright);background:var(--claret);}
.seat.object::after{content:"!";position:absolute;inset:0;display:flex;align-items:center;justify-content:center;color:var(--paper-light);font-family:var(--font-mono);font-size:.82rem;}
.btn-row{display:flex;gap:.7rem;flex-wrap:wrap;margin-bottom:1rem;}
.btn{font-family:var(--font-mono);font-size:.75rem;letter-spacing:.03em;cursor:pointer;padding:.65rem 1.15rem;border-radius:8px;transition:.2s;border:1px solid var(--glass-line);background:var(--ink-2);color:var(--paper-light);}
.btn:hover{border-color:var(--teal-bright);color:var(--teal-bright);}
.btn--primary{background:var(--teal);border-color:var(--teal-bright);color:#fff;}
.btn--primary:hover{background:var(--teal-bright);color:var(--ink);}
.btn--ghost{background:transparent;}
.verdict{display:inline-flex;align-items:center;gap:.55rem;font-family:var(--font-mono);font-size:.77rem;letter-spacing:.06em;text-transform:uppercase;color:var(--paper-light);padding:.55rem 1rem;border-radius:8px;border:1.5px solid var(--gold-soft);background:rgba(200,150,58,.08);opacity:0;transform:scale(.92);transition:.35s;}
.verdict.show{opacity:1;transform:scale(1);}
.verdict.pass{border-color:var(--teal-bright);background:rgba(63,184,166,.12);color:var(--teal-bright);}
.verdict.fail{border-color:var(--claret-bright);background:rgba(224,101,78,.1);color:var(--claret-bright);}
.verdict::before{content:"";width:9px;height:9px;border-radius:50%;background:var(--gold);}
.verdict.pass::before{background:var(--teal-bright);}
.verdict.fail::before{background:var(--claret-bright);}
.sim__caption{color:var(--muted);font-size:.95rem;margin:1rem 0 0;}

.vote-controls{display:grid;grid-template-columns:repeat(3,1fr);gap:.85rem;margin-bottom:1.4rem;}
@media (max-width:560px){.vote-controls{grid-template-columns:1fr;}}
.vote-ctrl{background:var(--ink-2);border-radius:10px;padding:1rem .9rem;text-align:center;border-top:3px solid var(--gold-soft);}
.vote-ctrl--yes{border-top-color:var(--teal-bright);}
.vote-ctrl--no{border-top-color:var(--claret-bright);}
.vote-ctrl--abs{border-top-color:#6b7893;}
.vote-ctrl__label{font-family:var(--font-mono);font-size:.64rem;letter-spacing:.08em;text-transform:uppercase;color:var(--muted-dark);}
.vote-ctrl--yes .vote-ctrl__label{color:var(--teal-bright);}
.vote-ctrl--no .vote-ctrl__label{color:var(--claret-bright);}
.vote-ctrl__val{font-family:var(--font-display);font-size:2.2rem;color:var(--paper-light);line-height:1.2;margin:.15rem 0 .45rem;}
.stepper-mini{display:flex;gap:.4rem;justify-content:center;}
.stepper-mini button{width:34px;height:34px;border-radius:7px;border:1px solid var(--glass-line);background:var(--ink-3);color:var(--paper-light);font-family:var(--font-mono);font-size:1.05rem;cursor:pointer;transition:.15s;}
.stepper-mini button:hover{border-color:var(--gold);color:var(--gold);}
.range-wrap{margin:.75rem 0 0;}
.range-wrap input[type=range]{width:100%;accent-color:var(--teal-bright);}
.hemicycle{display:flex;flex-wrap:wrap;gap:5px;justify-content:center;padding:1.15rem;background:var(--ink-3);border-radius:10px;margin-bottom:1.3rem;min-height:70px;border:1px solid var(--glass-line);}
.dot{width:15px;height:15px;border-radius:50%;transition:.2s;}
.dot.yes{background:var(--teal-bright);box-shadow:0 0 8px rgba(63,184,166,.5);}
.dot.no{background:var(--claret-bright);box-shadow:0 0 8px rgba(224,101,78,.5);}
.dot.abs{background:transparent;border:1.5px dashed #5c6a85;}
.hemicycle.small .dot{width:11px;height:11px;}
.calc{display:grid;grid-template-columns:1fr 1fr;gap:.7rem 1.5rem;background:var(--ink-3);border-radius:10px;padding:1.2rem 1.35rem;margin-bottom:1.2rem;font-family:var(--font-mono);font-size:.82rem;}
.calc .row{display:flex;justify-content:space-between;gap:1rem;color:var(--muted-dark);border-bottom:1px dotted var(--glass-line);padding-bottom:.42rem;}
.calc .row b{color:var(--paper-light);font-weight:500;}
.calc .row.excl b{color:#7f8ba3;text-decoration:line-through;}
.calc .row.key{grid-column:1 / -1;border-bottom:none;padding-top:.2rem;}
.calc .row.key b{color:var(--gold);font-size:.95rem;}
@media (max-width:560px){.calc{grid-template-columns:1fr;}}
.gauge{height:30px;border-radius:10px;background:var(--ink-3);position:relative;overflow:hidden;margin-bottom:.6rem;border:1px solid var(--glass-line);}
.gauge-fill{height:100%;width:0%;background:linear-gradient(90deg,var(--teal),var(--teal-bright));transition:width .4s ease;}
.gauge-threshold{position:absolute;top:-4px;bottom:-4px;width:2px;background:var(--claret-bright);}
.gauge-threshold::after{content:"2/3";position:absolute;top:-16px;left:50%;transform:translateX(-50%);font-family:var(--font-mono);font-size:.6rem;color:var(--claret-bright);white-space:nowrap;}
.gauge-note{font-family:var(--font-mono);font-size:.7rem;color:var(--muted-dark);margin-bottom:1.1rem;}
.preset-row{display:flex;gap:.55rem;flex-wrap:wrap;margin-bottom:1.2rem;}
.chip{font-family:var(--font-mono);font-size:.68rem;letter-spacing:.02em;cursor:pointer;padding:.5rem .85rem;border-radius:999px;border:1px solid var(--glass-line);background:transparent;color:var(--muted-dark);transition:.18s;}
.chip:hover{border-color:var(--gold);color:var(--gold);}
.chip.active{background:var(--gold);border-color:var(--gold);color:var(--ink-3);}
.forum-tabs{display:flex;gap:.6rem;flex-wrap:wrap;margin-bottom:1.3rem;}
.forum-tab{flex:1;min-width:150px;font-family:var(--font-mono);font-size:.74rem;letter-spacing:.02em;cursor:pointer;padding:1rem .85rem;border-radius:10px;border:1px solid var(--glass-line);background:var(--ink-2);color:var(--muted);transition:.2s;text-align:center;line-height:1.4;}
.forum-tab small{display:block;font-size:.6rem;color:var(--gold-soft);margin-top:.28rem;}
.forum-tab:hover{color:var(--paper-light);border-color:var(--teal-bright);}
.forum-tab.active{background:var(--teal);border-color:var(--teal-bright);color:#fff;}
.forum-tab.active small{color:#cfeee8;}
.forum-out{background:var(--ink-3);border-radius:12px;padding:1.7rem;border-top:4px solid var(--gold);}
.forum-out h3{font-size:1.25rem;margin-bottom:.3rem;}
.forum-out .basis{font-family:var(--font-mono);font-size:.66rem;letter-spacing:.06em;color:var(--gold);text-transform:uppercase;display:block;margin-bottom:.9rem;}
.forum-out ul{margin:0;padding-left:1.15rem;}
.forum-out li{margin-bottom:.5rem;font-size:.96rem;color:var(--muted);}
.forum-out li:last-child{margin-bottom:0;}
.forum-out b{color:var(--paper-light);}
.forum-out em{color:var(--teal-bright);}

/* quiz */
.quiz{background:var(--panel);border:1px solid var(--glass-line);border-radius:16px;padding:1.8rem;margin-top:1.9rem;backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);box-shadow:0 24px 60px rgba(0,0,0,.3);}
.quiz__bar{height:5px;border-radius:999px;background:rgba(160,190,220,.14);overflow:hidden;margin-bottom:1.4rem;}
.quiz__bar-fill{height:100%;width:0%;background:linear-gradient(90deg,var(--teal),var(--teal-bright));transition:width .35s ease;}
.quiz__scenario{font-family:var(--font-display);font-style:italic;font-size:1.3rem;line-height:1.5;margin-bottom:1.3rem;color:var(--paper-light);}
.quiz__opts{display:flex;flex-direction:column;gap:.65rem;}
.quiz__opt{text-align:left;font-family:var(--font-body);font-size:.97rem;cursor:pointer;padding:.85rem 1.1rem;border-radius:10px;border:1px solid var(--glass-line);background:var(--ink-2);color:var(--paper-light);transition:.18s;}
.quiz__opt:hover:not(:disabled){border-color:var(--teal-bright);transform:translateX(4px);}
.quiz__opt.correct{border-color:var(--teal-bright);background:rgba(63,184,166,.14);}
.quiz__opt.wrong{border-color:var(--claret-bright);background:rgba(224,101,78,.1);}
.quiz__opt:disabled{cursor:default;}
.quiz__feedback{margin-top:1.1rem;color:var(--muted);font-size:.96rem;min-height:1em;line-height:1.55;}
.quiz__feedback b{color:var(--paper-light);}
.quiz__foot{display:flex;justify-content:space-between;align-items:center;margin-top:1.3rem;gap:1rem;flex-wrap:wrap;}
.quiz__count{font-family:var(--font-mono);font-size:.68rem;color:var(--gold-soft);letter-spacing:.05em;}
.quiz__score{font-family:var(--font-mono);font-size:.68rem;color:var(--teal-bright);letter-spacing:.05em;}
.quiz__result{text-align:center;padding:1.3rem;background:var(--ink-3);border:1px solid var(--glass-line);border-radius:12px;font-family:var(--font-display);font-size:1.4rem;font-style:italic;color:var(--paper-light);display:none;margin-top:.5rem;}
.quiz__result span{color:var(--teal-bright);font-style:normal;font-weight:600;}
.quiz__restart{margin-top:1rem;display:none;}

/* checklist */
.checklist{list-style:none;margin:2rem 0 0;padding:0;display:flex;flex-direction:column;gap:0;}
.checklist li{display:flex;gap:1.2rem;align-items:flex-start;padding:1.4rem 0;border-top:1px solid var(--glass-line);}
.checklist li:last-child{border-bottom:1px solid var(--glass-line);}
.checklist .mark{flex:none;width:30px;height:30px;border-radius:50%;border:2px solid var(--teal-bright);display:flex;align-items:center;justify-content:center;font-family:var(--font-mono);font-size:.8rem;color:var(--teal-bright);}
.checklist p{margin:0;color:var(--muted);}
.checklist strong{color:var(--paper-light);}

.sources{margin:2rem 0 0;padding:0;list-style:none;display:flex;flex-direction:column;gap:1rem;}
.sources li{font-size:.93rem;color:var(--muted);padding-left:1.6rem;position:relative;}
.sources li::before{content:"\00A7";position:absolute;left:0;color:var(--gold);font-family:var(--font-mono);}

footer{padding:4rem 2.4rem;text-align:center;color:var(--muted-dark);font-size:.82rem;border-top:1px solid var(--glass-line);background:rgba(8,15,24,.6);position:relative;z-index:1;}
footer em{color:var(--gold);font-style:italic;}

/* reveal defaults (only when JS) */
html.js .reveal{opacity:0;}
.reveal.in{opacity:1;}

@media (prefers-reduced-motion: reduce){
    html{scroll-behavior:auto;}
    .scroll-cue::after{animation:none;}
    #preloader span{animation:none;width:100%;}
    html.js .reveal{opacity:1;}
}
</style>
</head>
<body>

<div id="preloader">
    <div class="pre-mark">Adopsi Naskah</div>
    <div class="pre-bar"><span></span></div>
    <div class="pre-sub">Menyusun ruang sidang</div>
</div>

<canvas id="bg3d"></canvas>
<div class="bg-aurora"></div>
<div class="progress" id="progress"></div>

<div class="mobile-bar">
    <span class="mobile-bar__title">Adopsi Naskah</span>
    <button class="nav-toggle" aria-label="Buka daftar isi">Daftar Isi</button>
</div>

<aside class="rail">
    <div class="rail__brand">
        <strong>Adopsi Naskah</strong>
        Hukum Perjanjian Internasional · Pasal 9 VCLT 1969
    </div>
    <div class="rail__label">Navigasi</div>
    <nav>
        <a href="#beranda"><span class="lead">&#9671;</span>Beranda</a>
        <div class="gap"></div>
        <a href="#ahli"><span class="lead">1</span>Definisi Menurut Para Ahli</a>
        <a href="#umum"><span class="lead">2</span>Definisi Secara Umum</a>
        <a href="#mekanisme"><span class="lead">3</span>Mekanisme Adopsi</a>
        <a href="#konsensus" class="sub"><span class="lead">A.</span>Konsensus</a>
        <a href="#voting" class="sub"><span class="lead">B.</span>Voting &amp; Hak Suara</a>
        <a href="#dua-pertiga" class="sub"><span class="lead">C.</span>Aturan Dua Pertiga</a>
        <a href="#perbedaan"><span class="lead">4</span>Adopsi vs Penandatanganan</a>
        <a href="#konferensi"><span class="lead">5</span>Konferensi &amp; Forum</a>
        <a href="#aklamasi"><span class="lead">6</span>Aklamasi &amp; Uji Pemahaman</a>
        <div class="gap"></div>
        <a href="#ringkasan"><span class="lead">&#9671;</span>Ringkasan</a>
        <a href="#sumber"><span class="lead">&#9671;</span>Rujukan</a>
    </nav>
</aside>

<div class="content">

    <!-- HERO -->
    <section class="hero" id="beranda">
        <div class="hero__grid">
            <span class="eyebrow"><span class="num">9</span>Pasal 9 Konvensi Wina 1969</span>
            <h1><span class="word l1">Adopsi</span><br><span class="word l2">Naskah</span></h1>
            <p class="hero__lede">Sebelum sebuah rancangan perjanjian dapat ditandatangani atau mengikat siapa pun, bentuk akhirnya harus dikunci terlebih dahulu. Itulah tahap adopsi naskah.</p>
            <div class="hero__meta"><span><b>6</b> Bagian</span><span><b>4</b> Simulasi interaktif</span><span><b>10</b> Soal</span></div>
            <span class="scroll-cue">Gulir untuk memulai</span>
        </div>
    </section>

    <!-- 1 · PARA AHLI -->
    <section class="section" id="ahli">
        <div class="section__in">
            <div class="read reveal">
                <span class="eyebrow"><span class="num">1</span>Definisi Menurut Para Ahli</span>
                <h2>Adopsi Naskah dalam Literatur</h2>
                <p class="lead-p">Tiga penulis berikut menyorot adopsi naskah dari sudut yang berbeda, namun bertemu pada satu titik: adopsi adalah momen ketika hasil perundingan diterima resmi sebagai teks final, sebelum otentikasi dan sebelum negara terikat.</p>
            </div>
            <div class="ahli-wrap reveal">
                <button class="slider-arrow slider-arrow--left" aria-label="Ahli sebelumnya">&#10094;</button>
                <div class="ahli-slider" id="ahliSlider">
                    <div class="ahli-slide active" data-index="0">
                        <div class="ahli-foto"><svg viewBox="0 0 100 100" aria-hidden="true"><circle cx="50" cy="38" r="19"/><circle cx="50" cy="112" r="46"/></svg></div>
                        <div class="ahli-teks">
                            <span class="idx">Perspektif 01</span>
                            <h3>Langkah Keempat: Penerimaan Naskah</h3>
                            <p>Dari sembilan langkah formal pembuatan perjanjian menurut Konvensi Wina 1969, adopsi (<em>adoption of the text</em>) adalah langkah keempat: rumusan hasil perundingan diterima resmi oleh negara peserta, sebelum otentikasi dan pernyataan terikat. Isi perjanjian "dikunci" sebagai versi final.</p>
                            <span class="who">I Wayan Parthiana</span>
                        </div>
                    </div>
                    <div class="ahli-slide" data-index="1">
                        <div class="ahli-foto"><svg viewBox="0 0 100 100" aria-hidden="true"><circle cx="50" cy="38" r="19"/><circle cx="50" cy="112" r="46"/></svg></div>
                        <div class="ahli-teks">
                            <span class="idx">Perspektif 02</span>
                            <h3>Wadah Kehendak Bersama</h3>
                            <p>Perjanjian internasional adalah instrumen yuridik yang menampung kehendak dan persetujuan negara untuk tujuan bersama. Adopsi naskah adalah saat kehendak bersama itu pertama kali dituangkan resmi ke dalam satu rumusan teks yang disepakati semua pihak.</p>
                            <span class="who">Boer Mauna</span>
                        </div>
                    </div>
                    <div class="ahli-slide" data-index="2">
                        <div class="ahli-foto"><svg viewBox="0 0 100 100" aria-hidden="true"><circle cx="50" cy="38" r="19"/><circle cx="50" cy="112" r="46"/></svg></div>
                        <div class="ahli-teks">
                            <span class="idx">Perspektif 03</span>
                            <h3>Penutup Resmi Fase Perundingan</h3>
                            <p>Perundingan adalah fase krusial karena di sinilah negara menentukan ruang lingkup dan substansi perjanjian. Adopsi menutup fase itu: begitu kompromi tercapai, teks itulah yang diadopsi sebagai naskah final sebelum penandatanganan.</p>
                            <span class="who">Anthony Aust</span>
                        </div>
                    </div>
                </div>
                <button class="slider-arrow slider-arrow--right" aria-label="Ahli berikutnya">&#10095;</button>
                <div class="ahli-dots" id="ahliDots"></div>
            </div>
        </div>
    </section>

    <!-- 2 · SECARA UMUM -->
    <section class="section statement" id="umum">
        <div class="section__in">
            <div class="reveal">
                <span class="eyebrow"><span class="num">2</span>Definisi Secara Umum</span>
                <h2>Adopsi <span class="pull-accent">mengunci bentuk</span>, belum mengunci kewajiban.</h2>
                <p class="big-lead">Adopsi naskah adalah tindakan formal menetapkan rumusan akhir teks perjanjian sebagai versi resmi setelah perundingan selesai. Dasar hukumnya <b>Pasal 9 Konvensi Wina 1969</b>, yang mengatur dua cara adopsi menurut jenis forumnya.</p>
            </div>
            <ol class="numlist reveal">
                <li>
                    <span class="tag">Ayat (1) · Konsensus</span>
                    <h3>Persetujuan Seluruh Peserta</h3>
                    <p>Untuk perjanjian bilateral atau perundingan terbatas, naskah diadopsi dengan persetujuan bulat (konsensus) semua negara yang ikut merumuskannya.</p>
                </li>
                <li>
                    <span class="tag">Ayat (2) · Konferensi</span>
                    <h3>Suara Dua Pertiga</h3>
                    <p>Untuk perjanjian multilateral dalam konferensi internasional, naskah diadopsi dengan dua pertiga suara negara yang hadir dan memberikan suara, kecuali disepakati aturan lain.</p>
                </li>
            </ol>
            <p class="pull reveal">Ibarat menyepakati draf final sebuah kontrak: isinya sudah tidak bisa diubah sepihak, tetapi belum ada tanda tangan yang benar-benar mengikat.</p>
        </div>
    </section>

    <!-- 3 · MEKANISME intro -->
    <section class="section" id="mekanisme">
        <div class="section__in read reveal">
            <span class="eyebrow"><span class="num">3</span>Mekanisme Adopsi Naskah</span>
            <h2>Konsensus dan Voting dalam Pasal 9</h2>
            <p class="lead-p">Pasal 9 menyediakan dua jalur. Jalur pertama, yaitu konsensus, adalah aturan umum yang mengutamakan kebulatan. Jalur kedua, yaitu voting dua pertiga, dipakai ketika konsensus tidak tercapai dalam sebuah konferensi. Bagian A, B, dan C berikut menelusuri keduanya, lengkap dengan simulasi interaktif.</p>
        </div>
    </section>

    <!-- 3A · KONSENSUS -->
    <section class="section" id="konsensus">
        <div class="section__in">
            <div class="ed">
                <div class="ed__label reveal">
                    <span class="k">Bagian 3 · A</span>
                    <h2>Diterima Bila Tak Ada Keberatan</h2>
                </div>
                <div class="ed__body">
                    <p class="lead-p reveal" style="margin-top:0;">Pasal 9 ayat (1) mensyaratkan kebulatan (konsensus) semua peserta. Namun konsensus <em>bukan</em> pemungutan suara bulat: keputusan dianggap diterima apabila tidak ada satu pun delegasi yang menyatakan keberatan formal saat pimpinan sidang mengetuk naskah. Ketiadaan keberatan sudah dianggap sebagai persetujuan diam-diam.</p>

                    <div class="sim reveal" id="simConsensus">
                        <div class="sim__head">
                            <span class="sim__title">Simulasi · Sidang Konsensus</span>
                            <span class="sim__hint">Klik kursi untuk memunculkan keberatan, lalu ketuk palu.</span>
                        </div>
                        <div class="floor" id="consFloor" aria-label="Sembilan delegasi"></div>
                        <div class="btn-row">
                            <button class="btn btn--primary" id="consGavel" type="button">&#128296; Ketuk palu: "Ada keberatan?"</button>
                            <button class="btn btn--ghost" id="consReset" type="button">Ulangi</button>
                        </div>
                        <span class="verdict" id="consVerdict"></span>
                        <p class="sim__caption" id="consCaption">Sembilan delegasi hadir. Secara bawaan tak ada yang keberatan. Coba jadikan satu atau lebih kursi "keberatan", lalu ketuk palu untuk melihat akibatnya.</p>
                    </div>

                    <div class="subhead reveal">Empat tahap mencapai konsensus</div>
                    <ul class="flow reveal">
                        <li><span class="node">1</span><strong>Negosiasi informal berkelanjutan.</strong><p>Pimpinan sidang dan delegasi berkonsultasi untuk menjembatani perbedaan posisi.</p></li>
                        <li><span class="node">2</span><strong>Penyusunan naskah kompromi.</strong><p><em>Chairman's text</em> mengakomodasi sebanyak mungkin kepentingan peserta.</p></li>
                        <li><span class="node">3</span><strong>Pengetukan tanpa pemungutan suara.</strong><p>Naskah diadopsi "<em>without a vote</em>" bila tak ada keberatan formal.</p></li>
                        <li><span class="node">4</span><strong>Hak menyatakan posisi.</strong><p>Negara yang belum sepenuhnya setuju boleh menyampaikan interpretasi tanpa memblokir adopsi.</p></li>
                    </ul>

                    <div class="split reveal">
                        <div class="split__col split__col--good">
                            <h3>Kelebihan</h3>
                            <p>Legitimasi politik lebih luas karena tak ada negara yang "dikalahkan"; memperbesar peluang ratifikasi; cocok untuk isu yang menyentuh kedaulatan.</p>
                        </div>
                        <div class="split__col split__col--bad">
                            <h3>Kelemahan</h3>
                            <p>Prosesnya lambat dan rawan <em>deadlock</em> karena keberatan satu negara saja dapat menahan kesepakatan; hasil kerap berupa kompromi minimal.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 3B · VOTING -->
    <section class="section" id="voting">
        <div class="section__in">
            <div class="ed">
                <div class="ed__label reveal">
                    <span class="k">Bagian 3 · B</span>
                    <h2>Ketika Konsensus Gagal, Suara Dihitung</h2>
                </div>
                <div class="ed__body">
                    <p class="lead-p reveal" style="margin-top:0;">Bila konsensus tidak tercapai dalam konferensi, Pasal 9 ayat (2) menyediakan jalur voting dengan dukungan dua pertiga negara yang hadir dan memberikan suara. Ketentuan ini khusus berlaku untuk adopsi di konferensi internasional.</p>

                    <div class="subhead reveal">Ciri pokok prosedur voting</div>
                    <ol class="numlist reveal">
                        <li>
                            <span class="tag">Prinsip</span>
                            <h3>Satu Negara, Satu Suara</h3>
                            <p><em>One state, one vote</em>, yang mencerminkan kesetaraan kedaulatan terlepas dari besar-kecilnya kekuatan politik atau ekonomi negara.</p>
                        </li>
                        <li>
                            <span class="tag">Tiga kategori</span>
                            <h3>Setuju · Menolak · Abstain</h3>
                            <p>Suara dapat berupa <em>in favour</em>, <em>against</em>, atau <em>abstention</em>. Pelaksanaannya bisa lewat angkat tangan, pemanggilan nama (<em>roll-call</em>), atau elektronik.</p>
                        </li>
                    </ol>

                    <div class="subhead reveal">Siapa yang berhak memilih?</div>
                    <p class="lead-p reveal" style="margin-top:0;">Hak suara melekat pada delegasi negara yang sah secara prosedural, dibuktikan lewat surat kuasa penuh (<em>full powers</em>) dan surat kepercayaan (<em>credentials</em>), sejalan dengan Pasal 7 UU No. 24 Tahun 2000. Negara peninjau (<em>observer</em>) dan organisasi nonpemerintah umumnya hanya punya hak berbicara, bukan hak memilih.</p>

                    <div class="subhead reveal">Ilustrasi: Arms Trade Treaty (2013)</div>
                    <p class="lead-p reveal" style="margin-top:0;">Konferensi diplomatik ATT di New York gagal mengadopsi naskah secara konsensus setelah sembilan hari. Naskahnya lalu dibawa ke Majelis Umum PBB dan diadopsi lewat pemungutan suara pada 2 April 2013. Kegagalan konsensus memicu beralihnya proses ke jalur voting Pasal 9 ayat (2).</p>
                    <div class="statgrid reveal">
                        <div class="stat stat--yes"><div class="stat__num" data-count="154">0</div><div class="stat__lab">Mendukung</div></div>
                        <div class="stat stat--no"><div class="stat__num" data-count="3">0</div><div class="stat__lab">Menolak</div></div>
                        <div class="stat stat--abs"><div class="stat__num" data-count="23">0</div><div class="stat__lab">Abstain · termasuk Indonesia</div></div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 3C · DUA PERTIGA + SIMULASI UTAMA -->
    <section class="section" id="dua-pertiga">
        <div class="section__in read reveal">
            <span class="eyebrow"><span class="num">3 · C</span>Penghitungan dan Penerapan Aturan Dua Pertiga (2/3)</span>
            <h2>Rumus "Present and Voting"</h2>
            <p class="lead-p">Kunci penghitungan ada pada frasa <em>present and voting</em>. Hanya negara yang benar-benar memilih setuju atau menolak yang masuk penyebut. <strong style="color:var(--paper-light);">Abstain dan negara yang absen dikeluarkan sama sekali</strong>. Keduanya hanya mengurangi jumlah negara yang menentukan hasil, tanpa dihitung sebagai suara mendukung maupun menolak.</p>
            <p class="pull">Lolos ambang 2/3&nbsp; =&nbsp; Setuju&nbsp;&#247;&nbsp;(Setuju&nbsp;+&nbsp;Menolak)&nbsp;&#8805;&nbsp;&#8532;</p>
        </div>
        <div class="section__in reveal">
            <div class="sim" id="simVote">
                <div class="sim__head">
                    <span class="sim__title">Simulasi · Kalkulator Voting Dua Pertiga</span>
                    <span class="sim__hint">Atur suara di bawah, atau pilih kasus. Ambang dihitung otomatis.</span>
                </div>
                <div class="preset-row" id="votePresets">
                    <button class="chip active" data-preset="ambang" type="button">Ambang tipis</button>
                    <button class="chip" data-preset="hipotetis" type="button">Hipotetis 60&middot;20&middot;20</button>
                    <button class="chip" data-preset="att" type="button">Kasus ATT 2013 &middot; 154&middot;3&middot;23</button>
                    <button class="chip" data-preset="gagal" type="button">Contoh gagal</button>
                </div>
                <div class="vote-controls">
                    <div class="vote-ctrl vote-ctrl--yes">
                        <div class="vote-ctrl__label">Setuju</div>
                        <div class="vote-ctrl__val" id="valYes">6</div>
                        <div class="stepper-mini"><button data-cat="yes" data-d="-1" type="button">&#8722;</button><button data-cat="yes" data-d="1" type="button">+</button></div>
                        <div class="range-wrap"><input type="range" id="rangeYes" min="0" max="180" value="6" aria-label="Jumlah suara setuju"></div>
                    </div>
                    <div class="vote-ctrl vote-ctrl--no">
                        <div class="vote-ctrl__label">Menolak</div>
                        <div class="vote-ctrl__val" id="valNo">3</div>
                        <div class="stepper-mini"><button data-cat="no" data-d="-1" type="button">&#8722;</button><button data-cat="no" data-d="1" type="button">+</button></div>
                        <div class="range-wrap"><input type="range" id="rangeNo" min="0" max="180" value="3" aria-label="Jumlah suara menolak"></div>
                    </div>
                    <div class="vote-ctrl vote-ctrl--abs">
                        <div class="vote-ctrl__label">Abstain</div>
                        <div class="vote-ctrl__val" id="valAbs">2</div>
                        <div class="stepper-mini"><button data-cat="abs" data-d="-1" type="button">&#8722;</button><button data-cat="abs" data-d="1" type="button">+</button></div>
                        <div class="range-wrap"><input type="range" id="rangeAbs" min="0" max="180" value="2" aria-label="Jumlah suara abstain"></div>
                    </div>
                </div>
                <div class="hemicycle" id="hemicycle" aria-hidden="true"></div>
                <div class="gauge"><div class="gauge-threshold" style="left:66.667%"></div><div class="gauge-fill" id="gaugeFill"></div></div>
                <div class="gauge-note" id="gaugeNote"></div>
                <div class="calc" id="calcPanel"></div>
                <span class="verdict" id="voteVerdict"></span>
                <p class="sim__caption" id="voteCaption"></p>
            </div>
        </div>
    </section>

    <!-- 4 · PERBEDAAN + PROSES -->
    <section class="section" id="perbedaan">
        <div class="section__in">
            <div class="read reveal">
                <span class="eyebrow"><span class="num">4</span>Perbedaan Adopsi dengan Penandatanganan</span>
                <h2>Dua Tahap yang Kerap Tertukar</h2>
                <p class="lead-p">Singkatnya: adopsi berarti "ini teks finalnya, disepakati semua pihak", sedangkan penandatanganan berarti "negara saya menyetujui teks ini". Keduanya belum menimbulkan ikatan hukum penuh tanpa ratifikasi.</p>
            </div>
            <div class="paper-panel reveal" style="margin-top:2rem;">
                <div class="table-scroll">
                <table class="compare">
                    <caption>Perbandingan berdasarkan Konvensi Wina 1969</caption>
                    <thead><tr><th>Aspek</th><th>Adopsi Naskah</th><th>Penandatanganan</th></tr></thead>
                    <tbody>
                    <tr><td>Dasar hukum</td><td>Pasal 9 VCLT 1969</td><td>Pasal 10 sampai 12 VCLT 1969</td></tr>
                    <tr><td>Kapan terjadi</td><td>Di ujung tahap perundingan</td><td>Setelah adopsi &amp; otentikasi</td></tr>
                    <tr><td>Pelaku</td><td>Delegasi/wakil perunding</td><td>Pejabat berwenang (kepala negara, menlu, pemegang <em>full powers</em>)</td></tr>
                    <tr><td>Makna tindakan</td><td>Mengesahkan teks sebagai versi final</td><td>Menyatakan persetujuan atas teks</td></tr>
                    <tr><td>Akibat hukum</td><td>Belum mengikat</td><td>Umumnya belum mengikat penuh; masih perlu ratifikasi</td></tr>
                    </tbody>
                </table>
                </div>
            </div>
        </div>
    </section>

    <!-- PROSES horizontal -->
    <section class="section process-outer" id="proses">
        <div class="section__in">
            <div class="read reveal">
                <span class="eyebrow">Alur Pembentukan Perjanjian</span>
                <h2>Di Mana Posisi Adopsi?</h2>
                <p class="lead-p">Adopsi adalah tahap ketiga dari enam. Gulir untuk menyusuri alurnya dari perundingan hingga perjanjian berlaku.</p>
            </div>
            <div class="process-vp" style="margin-top:2.2rem;">
                <div class="process-track" id="processTrack">
                    <div class="pstep"><div class="pstep__art">01</div><div class="pstep__n">Tahap 1</div><h3>Perundingan</h3><p>Negosiasi substansi dan isu teknis antara para pihak.</p></div>
                    <div class="pstep"><div class="pstep__art">02</div><div class="pstep__n">Tahap 2</div><h3>Perumusan Naskah</h3><p>Hasil perundingan dituangkan menjadi teks perjanjian.</p></div>
                    <div class="pstep is-here"><div class="pstep__art" style="color:var(--teal-bright)">03</div><div class="pstep__n" style="color:var(--teal-bright)">Tahap 3 · Adopsi</div><h3>Adopsi Naskah</h3><p>Pasal 9: negara peserta mengunci bentuk akhir teks lewat konsensus atau suara dua pertiga.</p></div>
                    <div class="pstep"><div class="pstep__art">04</div><div class="pstep__n">Tahap 4</div><h3>Otentikasi</h3><p>Pasal 10: teks dinyatakan otentik dan definitif, umumnya lewat tanda tangan atau paraf.</p></div>
                    <div class="pstep"><div class="pstep__art">05</div><div class="pstep__n">Tahap 5</div><h3>Persetujuan Terikat</h3><p>Pasal 11 sampai 17: negara menyatakan kesediaan terikat lewat tanda tangan, ratifikasi, atau aksesi.</p></div>
                    <div class="pstep"><div class="pstep__art">06</div><div class="pstep__n">Tahap 6</div><h3>Berlaku (Entry into Force)</h3><p>Pasal 24: perjanjian mulai mengikat negara pihak sesuai syarat yang disepakati.</p></div>
                </div>
            </div>
            <div class="process-hint reveal">Gulir untuk menyusuri keenam tahap &#8594;</div>
        </div>
    </section>

    <!-- 5 · KONFERENSI + FORUM -->
    <section class="section" id="konferensi">
        <div class="section__in">
            <div class="read reveal">
                <span class="eyebrow"><span class="num">5</span>Konferensi Diplomatik &amp; Contoh</span>
                <h2>Di Forum Mana Naskah Diadopsi?</h2>
                <p class="lead-p">Konferensi diplomatik adalah forum resmi para wakil negara berwenang penuh untuk merundingkan dan mengadopsi teks perjanjian multilateral. Namun adopsi juga bisa terjadi di forum lain, baik organisasi internasional yang permanen maupun perundingan bilateral, masing-masing dengan mekanismenya sendiri.</p>
            </div>

            <div class="sim reveal" id="simForum">
                <div class="sim__head">
                    <span class="sim__title">Simulasi · Pilih Forum Adopsi</span>
                    <span class="sim__hint">Pilih satu forum untuk melihat mekanisme yang berlaku.</span>
                </div>
                <div class="forum-tabs" id="forumTabs">
                    <button class="forum-tab active" data-forum="bilateral" type="button">Forum Bilateral<small>2 negara</small></button>
                    <button class="forum-tab" data-forum="konferensi" type="button">Konferensi Diplomatik<small>Multilateral ad hoc</small></button>
                    <button class="forum-tab" data-forum="organisasi" type="button">Organisasi Internasional<small>PBB &middot; WHO &middot; ILO</small></button>
                </div>
                <div class="forum-out" id="forumOut"></div>
            </div>

            <div class="ed" style="margin-top:3rem;">
                <div class="ed__label reveal"><span class="k">Catatan Historis</span><h2>Dua Konferensi Wina</h2></div>
                <div class="ed__body">
                    <ol class="numlist reveal">
                        <li>
                            <span class="tag">Wina 1968 sampai 1969</span>
                            <h3>Lahirnya VCLT 1969</h3>
                            <p>Konferensi PBB tentang Hukum Perjanjian berlangsung dua sesi (1968 dan 1969), menghasilkan naskah konvensi yang ditandatangani 23 Mei 1969 dan mulai berlaku 27 Januari 1980.</p>
                        </li>
                        <li>
                            <span class="tag">Wina 1961</span>
                            <h3>Konvensi Hubungan Diplomatik</h3>
                            <p>Dihadiri delegasi 81 negara, konferensi ini mengadopsi Konvensi Wina tentang Hubungan Diplomatik (50 pasal), kerangka hukum hubungan diplomatik permanen antarnegara.</p>
                        </li>
                    </ol>
                </div>
            </div>

            <div class="ed" style="margin-top:3rem;">
                <div class="ed__label reveal"><span class="k">Lanjutan 5 · i</span><h2>Organisasi Internasional</h2></div>
                <div class="ed__body reveal">
                    <p class="lead-p" style="margin-top:0;">Selain konferensi ad hoc, adopsi juga dilakukan lewat organ internal organisasi internasional yang terlembaga permanen.</p>
                    <ul class="flow">
                        <li><span class="node">&#183;</span><strong>PBB.</strong><p>Majelis Umum dapat mengadopsi resolusi berisi konvensi, lalu membukanya untuk ditandatangani dan diratifikasi negara anggota.</p></li>
                        <li><span class="node">&#183;</span><strong>WHO.</strong><p><em>World Health Assembly</em>, organ tertinggi WHO, mengadopsi konvensi dan regulasi internasional di bidang kesehatan.</p></li>
                        <li><span class="node">&#183;</span><strong>ILO.</strong><p>Konferensi Perburuhan Internasional, dengan delegasi tripartit (pemerintah, pengusaha, pekerja), mengadopsi konvensi dan rekomendasi.</p></li>
                        <li><span class="node">!</span><strong>Catatan penting.</strong><p>VCLT 1969 hanya berlaku untuk perjanjian antarnegara. Perjanjian yang melibatkan organisasi internasional diatur Konvensi Wina 1986.</p></li>
                    </ul>
                </div>
            </div>

            <div class="ed" style="margin-top:3rem;">
                <div class="ed__label reveal"><span class="k">Lanjutan 5 · ii</span><h2>Forum Bilateral</h2></div>
                <div class="ed__body reveal">
                    <p class="lead-p" style="margin-top:0;">Berbeda dari forum multilateral, adopsi bilateral berlangsung lewat negosiasi langsung dua negara. Kesepakatan dicapai secara bulat (konsensus) tanpa voting, dan ditandai dengan pembubuhan paraf atau pertukaran nota diplomatik.</p>
                    <ol class="numlist">
                        <li>
                            <span class="tag">Kewenangan khusus</span>
                            <h3>Tanpa Full Powers Terpisah</h3>
                            <p>Pasal 7 VCLT 1969 memberi hak <em>ex officio</em> kepada Kepala Misi Diplomatik untuk mengadopsi teks perjanjian bilateral, tanpa surat kuasa penuh terpisah.</p>
                        </li>
                        <li>
                            <span class="tag">Contoh nyata</span>
                            <h3>Batas Laut RI dan Singapura</h3>
                            <p>Perjanjian penetapan garis batas laut wilayah Indonesia dan Singapura di bagian barat Selat Singapura, disahkan melalui UU No. 4 Tahun 2010.</p>
                        </li>
                    </ol>
                </div>
            </div>
        </div>
    </section>

    <!-- 6 · AKLAMASI + KUIS -->
    <section class="section" id="aklamasi">
        <div class="section__in">
            <div class="read reveal">
                <span class="eyebrow"><span class="num">6</span>Mekanisme Adopsi Melalui Aklamasi</span>
                <h2>Aklamasi dan Paraf</h2>
                <p class="lead-p">Selain konsensus dan voting, terdapat dua mekanisme pelengkap. Aklamasi adalah persetujuan seluruh peserta tanpa pemungutan suara. Paraf (<em>initialing</em>) adalah tanda singkat pada naskah sebagai bukti teknis bahwa isi telah disepakati, sebelum penandatanganan resmi.</p>
            </div>
            <div class="split reveal">
                <div class="split__col split__col--good">
                    <h3>Aklamasi</h3>
                    <p>Ketua sidang mengajukan rancangan; bila tak ada keberatan, keputusan disahkan secara aklamasi dan dicatat dalam berita acara. Mekanisme ini mempercepat proses dan mencerminkan persatuan, meski berpotensi menekan peserta yang berpendapat berbeda.</p>
                </div>
                <div class="split__col split__col--bad">
                    <h3>Paraf (Initialing)</h3>
                    <p>Inisial dibubuhkan ketua delegasi atau perunding utama setelah negosiasi selesai. Berfungsi mencegah perubahan sepihak dan mengamankan keaslian hasil perundingan sebelum penandatanganan resmi.</p>
                </div>
            </div>

            <div class="quiz reveal" id="quiz">
                <div class="sim__head" style="margin-bottom:1rem;">
                    <span class="sim__title">Uji Pemahaman · Mekanisme Mana yang Tepat?</span>
                </div>
                <div class="quiz__bar"><div class="quiz__bar-fill" id="quizBar"></div></div>
                <p class="quiz__scenario" id="quizScenario"></p>
                <div class="quiz__opts" id="quizOpts"></div>
                <p class="quiz__feedback" id="quizFeedback"></p>
                <div class="quiz__foot">
                    <span class="quiz__count" id="quizCount"></span>
                    <span class="quiz__score" id="quizScore"></span>
                    <button class="btn btn--ghost" id="quizNext" type="button" style="display:none;">Soal berikutnya &#8594;</button>
                </div>
                <div class="quiz__result" id="quizResult"></div>
                <button class="btn btn--primary quiz__restart" id="quizRestart" type="button">Ulangi dari awal</button>
            </div>
        </div>
    </section>

    <!-- RINGKASAN -->
    <section class="section" id="ringkasan">
        <div class="section__in read reveal">
            <span class="eyebrow">Ringkasan</span>
            <h2>Lima Hal untuk Diingat</h2>
            <ul class="checklist">
                <li><span class="mark">&#10003;</span><p><strong>Mengunci bentuk, bukan mengikat.</strong> Adopsi menetapkan teks final; kewajiban hukum baru lahir di tahap berikutnya.</p></li>
                <li><span class="mark">&#10003;</span><p><strong>Dua jalur utama.</strong> Konsensus (Pasal 9 ayat 1) dan suara dua pertiga di konferensi (Pasal 9 ayat 2), dengan aklamasi dan paraf sebagai pelengkap.</p></li>
                <li><span class="mark">&#10003;</span><p><strong>Abstain tidak dihitung.</strong> Dalam rumus 2/3, hanya suara setuju dan menolak yang masuk penyebut, sesuai prinsip <em>present and voting</em>.</p></li>
                <li><span class="mark">&#10003;</span><p><strong>Aturan 2/3 tidak mutlak.</strong> Konferensi boleh menyepakati ambang lain, asalkan disetujui dengan mayoritas yang sama.</p></li>
                <li><span class="mark">&#10003;</span><p><strong>Forum menentukan mekanisme.</strong> Bilateral lewat konsensus; konferensi multilateral bisa lewat voting; organisasi internasional lewat organ internalnya.</p></li>
            </ul>
        </div>
    </section>

    <!-- SUMBER -->
    <section class="section" id="sumber">
        <div class="section__in read reveal">
            <span class="eyebrow">Rujukan</span>
            <h2>Sumber Rujukan Utama</h2>
            <ul class="sources">
                <li><em>Vienna Convention on the Law of Treaties</em> 1969, Pasal 7 sampai 18.</li>
                <li>Parthiana, I Wayan. <em>Hukum Perjanjian Internasional Bagian 1</em>, Mandar Maju, Bandung, 2002.</li>
                <li>Boer Mauna. <em>Hukum Internasional: Pengertian, Peranan dan Fungsi dalam Era Dinamika Global</em>, Alumni, Bandung, 2011.</li>
                <li>Songko (2016); Mardiyanto (2023), kajian Pasal 9 VCLT 1969.</li>
                <li>Seniwati dkk. (2026); Laitupa, Kartika, &amp; J. (2022), tahapan pembentukan perjanjian dan hak suara.</li>
                <li>Undang-Undang Nomor 24 Tahun 2000 tentang Perjanjian Internasional; UU No. 4 Tahun 2010.</li>
                <li>Hukumonline (2013, 2024), kasus ATT dan praktik konsensus UNCLOS.</li>
            </ul>
        </div>
    </section>

    <footer>
        Materi pembelajaran Hukum Perjanjian Internasional. <em>Adopsi Naskah menurut Pasal 9 Konvensi Wina 1969.</em>
    </footer>

</div>

<script>
"use strict";
const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

/* ---------- Mobile nav ---------- */
const navToggle = document.querySelector('.nav-toggle');
const rail = document.querySelector('.rail');
navToggle.addEventListener('click', () => rail.classList.toggle('open'));
document.querySelectorAll('.rail nav a').forEach(a => a.addEventListener('click', () => rail.classList.remove('open')));

/* ---------- Active section highlight ---------- */
const navLinks = document.querySelectorAll('.rail nav a');
const secObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            navLinks.forEach(l => l.classList.toggle('active', l.getAttribute('href') === '#' + entry.target.id));
        }
    });
}, { rootMargin: '-35% 0px -60% 0px' });
document.querySelectorAll('section[id]').forEach(s => secObserver.observe(s));

/* ---------- Ahli slider ---------- */
(function () {
    const slides = [...document.querySelectorAll('.ahli-slide')];
    const total = slides.length;
    const dotsWrap = document.getElementById('ahliDots');
    const btnPrev = document.querySelector('.slider-arrow--left');
    const btnNext = document.querySelector('.slider-arrow--right');
    let idx = 0;

    slides.forEach((_, i) => {
        const dot = document.createElement('button');
        dot.type = 'button';
        dot.setAttribute('aria-label', 'Ke ahli ' + (i + 1));
        if (i === 0) dot.classList.add('active');
        dot.addEventListener('click', () => go(i));
        dotsWrap.appendChild(dot);
    });
    const dots = [...dotsWrap.children];

    function go(next) {
        idx = (next + total) % total;
        slides.forEach((s, i) => s.classList.toggle('active', i === idx));
        dots.forEach((d, i) => d.classList.toggle('active', i === idx));
    }

    btnPrev.addEventListener('click', () => go(idx - 1));
    btnNext.addEventListener('click', () => go(idx + 1));
})();

/* ---------- Simulation 1: Consensus gavel ---------- */
(function () {
    const N = 9;
    const floor = document.getElementById('consFloor');
    const verdict = document.getElementById('consVerdict');
    const caption = document.getElementById('consCaption');
    const gavel = document.getElementById('consGavel');
    const reset = document.getElementById('consReset');
    const seats = [];
    for (let i = 0; i < N; i++) {
        const s = document.createElement('button');
        s.className = 'seat agree'; s.type = 'button';
        s.setAttribute('aria-label', 'Delegasi ' + (i + 1));
        s.dataset.state = 'agree';
        s.addEventListener('click', () => {
            if (s.dataset.state === 'object') { s.dataset.state = 'agree'; s.className = 'seat agree'; }
            else { s.dataset.state = 'object'; s.className = 'seat object'; }
            verdict.classList.remove('show', 'pass', 'fail');
        });
        floor.appendChild(s); seats.push(s);
    }
    gavel.addEventListener('click', () => {
        const objectors = seats.filter(s => s.dataset.state === 'object').length;
        verdict.classList.remove('pass', 'fail'); void verdict.offsetWidth;
        if (objectors === 0) {
            verdict.textContent = 'Diadopsi \u00b7 Konsensus (Pasal 9 ayat 1)';
            verdict.classList.add('show', 'pass');
            caption.innerHTML = 'Tidak ada keberatan formal. Pimpinan mengetuk naskah "<em>without a vote</em>" dan naskah dianggap diterima secara konsensus. Ketiadaan keberatan sudah cukup sebagai persetujuan diam-diam.';
        } else {
            verdict.textContent = objectors + ' keberatan \u00b7 Tertahan (deadlock)';
            verdict.classList.add('show', 'fail');
            caption.innerHTML = 'Keberatan formal dari <b style="color:var(--paper-light)">' + objectors + ' negara</b> menahan kesepakatan. Inilah kelemahan konsensus: satu keberatan saja secara de facto dapat memblokir adopsi, sehingga sidang perlu kembali bernegosiasi.';
        }
    });
    reset.addEventListener('click', () => {
        seats.forEach(s => { s.dataset.state = 'agree'; s.className = 'seat agree'; });
        verdict.classList.remove('show', 'pass', 'fail');
        caption.innerHTML = 'Sembilan delegasi hadir. Secara bawaan tak ada yang keberatan. Coba jadikan satu atau lebih kursi "keberatan", lalu ketuk palu untuk melihat akibatnya.';
    });
})();

/* ---------- Simulation 2: Two-thirds voting calculator ---------- */
(function () {
    let yes = 6, no = 3, abs = 2;
    const MAXDOTS = 200;
    const valYes = document.getElementById('valYes'), valNo = document.getElementById('valNo'), valAbs = document.getElementById('valAbs');
    const rYes = document.getElementById('rangeYes'), rNo = document.getElementById('rangeNo'), rAbs = document.getElementById('rangeAbs');
    const hemi = document.getElementById('hemicycle'), gaugeFill = document.getElementById('gaugeFill'), gaugeNote = document.getElementById('gaugeNote');
    const calc = document.getElementById('calcPanel'), verdict = document.getElementById('voteVerdict'), caption = document.getElementById('voteCaption');
    const chips = document.querySelectorAll('#votePresets .chip');
    function threshold(pv) { return pv === 0 ? 0 : Math.ceil(pv * 2 / 3); }
    function render() {
        valYes.textContent = yes; valNo.textContent = no; valAbs.textContent = abs;
        rYes.value = yes; rNo.value = no; rAbs.value = abs;
        const pv = yes + no, total = yes + no + abs, th = threshold(pv);
        const pct = pv === 0 ? 0 : (yes / pv) * 100, adopted = pv > 0 && yes >= th;
        hemi.innerHTML = '';
        const shown = total > MAXDOTS ? MAXDOTS : total;
        const ry = Math.round(yes / total * shown) || (yes ? 1 : 0);
        const rn = Math.round(no / total * shown) || (no ? 1 : 0);
        const ra = shown - ry - rn;
        hemi.classList.toggle('small', total > 60);
        const frag = document.createDocumentFragment();
        for (let i = 0; i < ry; i++) { const d = document.createElement('div'); d.className = 'dot yes'; frag.appendChild(d); }
        for (let i = 0; i < rn; i++) { const d = document.createElement('div'); d.className = 'dot no'; frag.appendChild(d); }
        for (let i = 0; i < Math.max(ra, 0); i++) { const d = document.createElement('div'); d.className = 'dot abs'; frag.appendChild(d); }
        hemi.appendChild(frag);
        gaugeFill.style.width = Math.min(pct, 100) + '%';
        gaugeFill.style.background = adopted ? 'linear-gradient(90deg,var(--teal),var(--teal-bright))' : 'linear-gradient(90deg,var(--gold-soft),var(--gold))';
        gaugeNote.innerHTML = pv === 0 ? 'Belum ada suara sah (setuju/menolak).' : 'Dukungan setuju: <b style="color:var(--paper-light)">' + pct.toFixed(1) + '%</b> dari suara sah &middot; garis merah = ambang 2/3 (66,7%).';
        calc.innerHTML =
            '<div class="row"><span>Setuju</span><b>' + yes + '</b></div>' +
            '<div class="row"><span>Menolak</span><b>' + no + '</b></div>' +
            '<div class="row excl"><span>Abstain (dikeluarkan)</span><b>' + abs + '</b></div>' +
            '<div class="row"><span>Total hadir</span><b>' + total + '</b></div>' +
            '<div class="row key"><span>Hadir &amp; memberikan suara (penyebut)</span><b>' + yes + ' + ' + no + ' = ' + pv + '</b></div>' +
            '<div class="row key"><span>Ambang 2/3 &#8594; &#8968;' + pv + ' &#215; 2/3&#8969;</span><b>' + th + ' suara setuju</b></div>';
        verdict.classList.remove('pass', 'fail', 'show'); void verdict.offsetWidth;
        if (pv === 0) {
            verdict.textContent = 'Belum ada hasil'; verdict.classList.add('show');
            caption.innerHTML = 'Naikkan jumlah suara setuju atau menolak. Suara abstain saja tidak menghasilkan keputusan apa pun.';
        } else if (adopted) {
            verdict.textContent = 'Naskah DIADOPSI (Pasal 9 ayat 2)'; verdict.classList.add('show', 'pass');
            caption.innerHTML = '<b style="color:var(--paper-light)">' + yes + ' \u2265 ' + th + '</b>: dukungan setuju mencapai ambang dua pertiga dari ' + pv + ' negara yang hadir dan memberikan suara. Naskah dinyatakan diadopsi. Perhatikan, secara persentase dari <b style="color:var(--paper-light)">seluruh</b> ' + total + ' negara peserta, setuju hanya ' + (yes / total * 100).toFixed(1) + '%.';
        } else {
            verdict.textContent = 'Naskah TIDAK diadopsi'; verdict.classList.add('show', 'fail');
            caption.innerHTML = '<b style="color:var(--paper-light)">' + yes + ' &lt; ' + th + '</b>: dukungan setuju belum mencapai ambang dua pertiga dari ' + pv + ' suara sah. Naskah belum dapat diadopsi lewat jalur voting ini.';
        }
    }
    function clamp(v) { return Math.max(0, Math.min(180, v)); }
    function setActiveChip(name) { chips.forEach(c => c.classList.toggle('active', c.dataset.preset === name)); }
    function clearChip() { chips.forEach(c => c.classList.remove('active')); }
    document.querySelectorAll('#simVote .stepper-mini button').forEach(btn => {
        btn.addEventListener('click', () => {
            const d = parseInt(btn.dataset.d, 10);
            if (btn.dataset.cat === 'yes') yes = clamp(yes + d);
            if (btn.dataset.cat === 'no') no = clamp(no + d);
            if (btn.dataset.cat === 'abs') abs = clamp(abs + d);
            clearChip(); render();
        });
    });
    rYes.addEventListener('input', () => { yes = clamp(parseInt(rYes.value, 10)); clearChip(); render(); });
    rNo.addEventListener('input', () => { no = clamp(parseInt(rNo.value, 10)); clearChip(); render(); });
    rAbs.addEventListener('input', () => { abs = clamp(parseInt(rAbs.value, 10)); clearChip(); render(); });
    const presets = { ambang: [6, 3, 2], hipotetis: [60, 20, 20], att: [154, 3, 23], gagal: [9, 8, 5] };
    chips.forEach(c => c.addEventListener('click', () => { const p = presets[c.dataset.preset]; yes = p[0]; no = p[1]; abs = p[2]; setActiveChip(c.dataset.preset); render(); }));
    render();
})();

/* ---------- Simulation 3: Forum selector ---------- */
(function () {
    const data = {
        bilateral: { title: 'Adopsi Bilateral', basis: 'Pasal 7 &amp; 9 (1) VCLT 1969', items: [
            '<b>Mekanisme:</b> kesepakatan bulat (konsensus) dua negara, tanpa prosedur voting.',
            '<b>Penanda adopsi:</b> pembubuhan paraf atau pertukaran nota/surat diplomatik.',
            '<b>Kewenangan:</b> Kepala Misi Diplomatik dapat mengadopsi teks secara <em>ex officio</em>, tanpa <em>full powers</em> terpisah.',
            '<b>Contoh:</b> batas laut RI dan Singapura di Selat Singapura (UU No. 4/2010).' ] },
        konferensi: { title: 'Konferensi Diplomatik (Multilateral)', basis: 'Pasal 9 (2) VCLT 1969', items: [
            '<b>Mekanisme:</b> utamakan konsensus; bila gagal, voting dengan dukungan dua pertiga negara yang hadir dan memberikan suara.',
            '<b>Sifat forum:</b> ad hoc, dibentuk untuk tujuan tertentu, dihadiri wakil ber-<em>full powers</em>.',
            '<b>Contoh:</b> Konferensi Wina 1968 sampai 1969 (lahirnya VCLT 1969); Konferensi Hubungan Diplomatik 1961.',
            '<b>Catatan:</b> ambang 2/3 boleh diubah bila disepakati dengan mayoritas yang sama.' ] },
        organisasi: { title: 'Organisasi Internasional (PBB &middot; WHO &middot; ILO)', basis: 'Aturan internal organisasi &middot; VCLT 1986', items: [
            '<b>PBB:</b> Majelis Umum mengadopsi resolusi berisi konvensi, lalu membukanya untuk tanda tangan dan ratifikasi.',
            '<b>WHO:</b> adopsi lewat <em>World Health Assembly</em>.',
            '<b>ILO:</b> adopsi lewat Konferensi Perburuhan Internasional dengan delegasi tripartit.',
            '<b>Catatan:</b> perjanjian yang melibatkan organisasi internasional tunduk pada Konvensi Wina 1986, bukan VCLT 1969.' ] }
    };
    const tabs = document.querySelectorAll('#forumTabs .forum-tab');
    const out = document.getElementById('forumOut');
    out.style.transition = 'opacity .25s ease';
    function show(key) {
        const d = data[key]; out.style.opacity = 0;
        setTimeout(() => {
            out.innerHTML = '<span class="basis">' + d.basis + '</span><h3>' + d.title + '</h3><ul>' + d.items.map(i => '<li>' + i + '</li>').join('') + '</ul>';
            out.style.opacity = 1;
        }, reduced ? 0 : 130);
    }
    tabs.forEach(t => t.addEventListener('click', () => { tabs.forEach(x => x.classList.remove('active')); t.classList.add('active'); show(t.dataset.forum); }));
    show('bilateral');
})();

/* ---------- Quiz ---------- */
(function () {
    const questions = [
        { q: 'Sebuah konferensi diplomatik yang dihadiri 120 negara gagal mencapai kata sepakat setelah berhari-hari; beberapa negara menolak keras satu pasal. Naskah tetap perlu diadopsi. Mekanisme apa yang paling mungkin ditempuh?', opts: ['Voting dua pertiga (Pasal 9 ayat 2)', 'Konsensus tanpa pemungutan suara', 'Paraf oleh kepala delegasi'], correct: 0, why: 'Ketika konsensus gagal di konferensi multilateral, jalur voting dua pertiga negara yang hadir dan memberikan suara menjadi jalan keluarnya, persis seperti kasus ATT 2013.' },
        { q: 'Dua negara menyelesaikan perundingan batas laut. Kepala Misi Diplomatik ingin menandai bahwa isi naskah sudah final dan tidak boleh diubah sepihak, sebelum penandatanganan resmi. Apa yang dilakukan?', opts: ['Voting dua pertiga', 'Pembubuhan paraf (initialing)', 'Sidang World Health Assembly'], correct: 1, why: 'Dalam perundingan bilateral, paraf berfungsi sebagai bukti teknis bahwa isi telah disepakati dan mencegah perubahan sepihak sebelum penandatanganan resmi.' },
        { q: 'Dalam sidang pleno, ketua mengajukan rancangan resolusi dan bertanya apakah ada keberatan. Tidak seorang pun mengangkat keberatan, dan ketua langsung mengesahkannya tanpa menghitung suara. Mekanisme apa ini?', opts: ['Aklamasi', 'Voting roll-call', 'Ratifikasi'], correct: 0, why: 'Aklamasi adalah pengesahan tanpa pemungutan suara: bila tak ada keberatan, ketua langsung menyatakan keputusan disahkan dan mencatatnya dalam berita acara.' },
        { q: 'Pada sebuah voting, hasilnya 50 setuju, 20 menolak, dan 30 abstain. Berapa suara yang menjadi penyebut dalam rumus dua pertiga?', opts: ['100 (semua negara)', '70 (setuju + menolak)', '80 (setuju + abstain)'], correct: 1, why: 'Hanya negara yang "hadir dan memberikan suara" (setuju + menolak = 70) yang masuk penyebut. Abstain dikeluarkan sama sekali dari penghitungan.' },
        { q: 'Pimpinan sidang mengetuk naskah dan tidak ada satu pun delegasi yang mengajukan keberatan formal. Atas dasar apa naskah dianggap diterima secara konsensus?', opts: ['Semua delegasi menyatakan setuju satu per satu secara aktif', 'Ketiadaan keberatan formal dianggap sebagai persetujuan diam-diam', 'Sekurang-kurangnya dua pertiga delegasi mengangkat tangan'], correct: 1, why: 'Konsensus bukan pemungutan suara bulat. Keputusan dianggap diterima apabila tak ada keberatan formal; ketiadaan keberatan itu sudah cukup sebagai persetujuan diam-diam.' },
        { q: 'Sebuah perjanjian dibuat antara sebuah negara dan sebuah organisasi internasional, bukan antarnegara. Instrumen hukum mana yang mengaturnya?', opts: ['VCLT 1969', 'Konvensi Wina 1986', 'Piagam PBB 1945'], correct: 1, why: 'VCLT 1969 hanya berlaku untuk perjanjian antarnegara. Perjanjian yang melibatkan organisasi internasional diatur oleh Konvensi Wina 1986.' },
        { q: 'Dalam sebuah konferensi diplomatik hadir pula negara peninjau (observer) dan sejumlah organisasi nonpemerintah yang diundang. Hak apa yang umumnya mereka miliki?', opts: ['Hak memilih penuh setara dengan negara peserta', 'Hak berbicara, tetapi bukan hak memilih', 'Tidak diperbolehkan hadir dalam sidang'], correct: 1, why: 'Hak suara melekat pada delegasi negara yang sah secara prosedural. Negara peninjau dan organisasi nonpemerintah pada umumnya hanya memiliki hak berbicara, bukan hak memilih.' },
        { q: 'Konferensi Hukum Laut PBB ke-III (yang melahirkan UNCLOS 1982) sengaja menonjolkan satu mekanisme untuk mencegah satu kelompok kepentingan mendominasi hasil. Mekanisme apa itu?', opts: ['Konsensus', 'Voting mayoritas sederhana', 'Aklamasi terbuka'], correct: 0, why: 'Konferensi tersebut mengutamakan konsensus alih-alih pemungutan suara mayoritas, agar isu sensitif menyangkut kedaulatan dapat diakomodasi lewat kompromi bertahap.' },
        { q: 'Setelah sebuah naskah diadopsi dalam konferensi, apa akibat hukum yang tepat pada tahap tersebut?', opts: ['Negara peserta langsung terikat penuh dan wajib menjalankan isinya', 'Teks final disahkan, tetapi negara belum terikat secara hukum', 'Perjanjian otomatis berlaku (entry into force)'], correct: 1, why: 'Adopsi hanya menetapkan teks sebagai versi final yang tidak dapat diubah sepihak. Untuk benar-benar terikat, negara masih harus menandatangani, meratifikasi, atau melakukan aksesi.' },
        { q: 'Bagaimana sifat ambang dua pertiga dalam Pasal 9 ayat (2) Konvensi Wina 1969?', opts: ['Mutlak dan tidak dapat diubah dalam kondisi apa pun', 'Tidak mutlak, boleh diubah bila disepakati dengan mayoritas yang sama', 'Hanya berlaku untuk perjanjian bilateral'], correct: 1, why: 'Ambang 2/3 bersifat default rule. Konferensi boleh menyepakati ambang lain, misalnya mayoritas sederhana, sepanjang perubahan itu disetujui dengan mayoritas yang sama.' }
    ];
    let idx = 0, answered = false, score = 0;
    const scenario = document.getElementById('quizScenario'), optsEl = document.getElementById('quizOpts'), feedback = document.getElementById('quizFeedback');
    const countEl = document.getElementById('quizCount'), scoreEl = document.getElementById('quizScore'), nextBtn = document.getElementById('quizNext');
    const barFill = document.getElementById('quizBar'), resultEl = document.getElementById('quizResult'), restartBtn = document.getElementById('quizRestart');
    function load() {
        answered = false; const item = questions[idx];
        scenario.textContent = '\u201c' + item.q + '\u201d'; feedback.textContent = ''; nextBtn.style.display = 'none';
        countEl.textContent = 'Soal ' + (idx + 1) + ' / ' + questions.length;
        scoreEl.textContent = 'Skor: ' + score + ' / ' + questions.length;
        barFill.style.width = (idx / questions.length) * 100 + '%';
        optsEl.innerHTML = '';
        item.opts.forEach((o, i) => {
            const b = document.createElement('button'); b.className = 'quiz__opt'; b.type = 'button'; b.textContent = o;
            b.addEventListener('click', () => choose(i, b)); optsEl.appendChild(b);
        });
    }
    function choose(i, btn) {
        if (answered) return; answered = true; const item = questions[idx];
        [...optsEl.children].forEach(b => b.disabled = true);
        optsEl.children[item.correct].classList.add('correct');
        if (i === item.correct) { score++; feedback.innerHTML = '<b>Tepat.</b> ' + item.why; }
        else { btn.classList.add('wrong'); feedback.innerHTML = '<b>Kurang tepat.</b> ' + item.why; }
        scoreEl.textContent = 'Skor: ' + score + ' / ' + questions.length;
        barFill.style.width = ((idx + 1) / questions.length) * 100 + '%';
        if (idx < questions.length - 1) nextBtn.style.display = 'inline-block'; else finish();
    }
    function finish() {
        let v; if (score === questions.length) v = 'Sempurna! Pemahaman Anda sangat solid.';
        else if (score >= 8) v = 'Bagus sekali, tinggal sedikit penyempurnaan.';
        else if (score >= 6) v = 'Cukup baik, tinjau kembali bagian yang terlewat.';
        else v = 'Mari baca ulang materinya, lalu coba lagi.';
        resultEl.innerHTML = 'Skor akhir: <span>' + score + ' / ' + questions.length + '</span><br>' + v;
        resultEl.style.display = 'block'; restartBtn.style.display = 'inline-block';
    }
    nextBtn.addEventListener('click', () => { idx = Math.min(idx + 1, questions.length - 1); load(); });
    restartBtn.addEventListener('click', () => { idx = 0; score = 0; resultEl.style.display = 'none'; restartBtn.style.display = 'none'; load(); });
    load();
})();

/* ================= ENHANCEMENT LAYER: 3D + GSAP ================= */
function makeDiscTexture() {
    const c = document.createElement('canvas'); c.width = c.height = 64;
    const g = c.getContext('2d'); const grd = g.createRadialGradient(32, 32, 0, 32, 32, 32);
    grd.addColorStop(0, 'rgba(255,255,255,1)'); grd.addColorStop(.35, 'rgba(255,255,255,.9)');
    grd.addColorStop(1, 'rgba(255,255,255,0)');
    g.fillStyle = grd; g.beginPath(); g.arc(32, 32, 32, 0, Math.PI * 2); g.fill();
    const t = new THREE.Texture(c); t.needsUpdate = true; return t;
}
function initHero3D(reduced) {
    if (!window.THREE) return null;
    const canvas = document.getElementById('bg3d');
    const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true, powerPreference: 'high-performance' });
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.setSize(window.innerWidth, window.innerHeight);
    const scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x080f18, 0.055);
    const camera = new THREE.PerspectiveCamera(58, window.innerWidth / window.innerHeight, 0.1, 100);
    camera.position.set(0, 1.4, 9.2);

    const isMobile = window.innerWidth < 760;
    const count = isMobile ? 900 : 2000;
    const positions = new Float32Array(count * 3);
    const colors = new Float32Array(count * 3);
    const cTeal = new THREE.Color(0x3fb8a6), cGold = new THREE.Color(0xc8963a), cClaret = new THREE.Color(0xe0654e), cDim = new THREE.Color(0x24384c);
    const R = 4.6;
    for (let i = 0; i < count; i++) {
        // hemisphere dome shell + slight jitter -> "assembly dome"
        const u = Math.random(), v = Math.random();
        const theta = u * Math.PI * 2;
        const phi = Math.acos(v);                    // 0..PI/2 upper dome
        const rr = R * (0.75 + Math.random() * 0.28);
        const x = rr * Math.sin(phi) * Math.cos(theta);
        const y = rr * Math.cos(phi) * 0.9 - 1.4;    // flatten + drop
        const z = rr * Math.sin(phi) * Math.sin(theta);
        positions[i * 3] = x; positions[i * 3 + 1] = y; positions[i * 3 + 2] = z;
        let col = cTeal;
        const r = Math.random();
        if (r > 0.93) col = cClaret; else if (r > 0.80) col = cGold; else if (r > 0.62) col = cDim;
        colors[i * 3] = col.r; colors[i * 3 + 1] = col.g; colors[i * 3 + 2] = col.b;
    }
    const geo = new THREE.BufferGeometry();
    geo.setAttribute('position', new THREE.BufferAttribute(positions, 3));
    geo.setAttribute('color', new THREE.BufferAttribute(colors, 3));
    const mat = new THREE.PointsMaterial({
        size: isMobile ? 0.11 : 0.085, map: makeDiscTexture(), vertexColors: true,
        transparent: true, depthWrite: false, blending: THREE.AdditiveBlending, opacity: 0.95, sizeAttenuation: true
    });
    const points = new THREE.Points(geo, mat);
    const group = new THREE.Group(); group.add(points); scene.add(group);

    // faint ring accents
    const ringGeo = new THREE.RingGeometry(R * 0.92, R * 0.94, 96, 1, 0, Math.PI);
    const ringMat = new THREE.MeshBasicMaterial({ color: 0x3fb8a6, transparent: true, opacity: 0.09, side: THREE.DoubleSide });
    const ring = new THREE.Mesh(ringGeo, ringMat); ring.rotation.x = -Math.PI / 2; ring.position.y = -1.4; group.add(ring);

    let pointer = { x: 0, y: 0 }, target = { x: 0, y: 0 }, scrollY = 0;
    window.addEventListener('pointermove', e => {
        pointer.x = (e.clientX / window.innerWidth - 0.5);
        pointer.y = (e.clientY / window.innerHeight - 0.5);
    }, { passive: true });
    window.addEventListener('scroll', () => { scrollY = window.scrollY || window.pageYOffset; }, { passive: true });

    function resize() {
        camera.aspect = window.innerWidth / window.innerHeight; camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    }
    window.addEventListener('resize', resize);

    // intro: scale in
    let introT = 0;
    group.scale.setScalar(reduced ? 1 : 0.2);

    function frame() {
        target.x += (pointer.x - target.x) * 0.045;
        target.y += (pointer.y - target.y) * 0.045;
        const sp = Math.min(scrollY / 900, 1);
        group.rotation.y += reduced ? 0 : 0.0016;
        group.rotation.y += (target.x * 0.35 - (group.rotation.y % (Math.PI * 2)) * 0) * 0; // keep smooth base spin
        group.rotation.x = -0.12 + target.y * 0.18 + sp * 0.5;
        camera.position.x += (target.x * 2.2 - camera.position.x) * 0.05;
        camera.position.y = 1.4 - target.y * 1.0 + sp * 1.5;
        camera.position.z = 9.2 + sp * 3.2;
        camera.lookAt(0, -1.2 + sp * 0.6, 0);
        if (!reduced && introT < 1) { introT = Math.min(introT + 0.02, 1); const e = 1 - Math.pow(1 - introT, 3); group.scale.setScalar(0.2 + e * 0.8); }
        renderer.render(scene, camera);
    }
    let raf;
    function loop() { frame(); raf = requestAnimationFrame(loop); }
    if (reduced) { frame(); }
    else { loop(); }
    document.addEventListener('visibilitychange', () => {
        if (document.hidden) { cancelAnimationFrame(raf); }
        else if (!reduced) { loop(); }
    });
    return { renderer, scene, camera };
}

window.addEventListener('load', () => {
    const pre = document.getElementById('preloader');
    const hidePre = () => { if (pre) { pre.classList.add('hide'); setTimeout(() => pre.remove(), 800); } };
    setTimeout(hidePre, reduced ? 200 : 1100);

    // 3D (progressive enhancement)
    let three = null;
    try { three = initHero3D(reduced); } catch (e) { console.warn('3D unavailable:', e); }
    if (!three) { const c = document.getElementById('bg3d'); if (c) c.style.display = 'none'; }

    const hasGSAP = !!(window.gsap && window.ScrollTrigger);
    if (!hasGSAP || reduced) {
        document.querySelectorAll('.reveal').forEach(el => el.classList.add('in'));
        return;
    }

    gsap.registerPlugin(ScrollTrigger);
    document.documentElement.classList.add('gsap-ready');

    // scroll progress bar
    gsap.to('#progress', { scaleX: 1, ease: 'none', scrollTrigger: { trigger: document.body, start: 'top top', end: 'bottom bottom', scrub: 0.3 } });

    // fade 3D canvas after hero so text stays readable
    gsap.to('#bg3d', { opacity: 0.14, ease: 'none', scrollTrigger: { trigger: '#ahli', start: 'top bottom', end: 'top center', scrub: true } });

    // hero intro timeline
    const heroTl = gsap.timeline({ defaults: { ease: 'power3.out' } });
    heroTl.from('.hero .eyebrow', { y: 24, opacity: 0, duration: .7, delay: reduced ? 0 : .3 })
          .from('.hero h1 .word', { y: 60, opacity: 0, duration: 1, stagger: .12 }, '-=.3')
          .from('.hero__lede', { y: 24, opacity: 0, duration: .8 }, '-=.5')
          .from('.hero__meta span', { y: 18, opacity: 0, duration: .6, stagger: .1 }, '-=.4')
          .from('.scroll-cue', { opacity: 0, duration: .6 }, '-=.2');

    // generic reveals
    gsap.utils.toArray('.reveal').forEach(el => {
        el.classList.add('in');
        gsap.fromTo(el, { y: 40, opacity: 0 }, {
            y: 0, opacity: 1, duration: .9, ease: 'power3.out',
            scrollTrigger: { trigger: el, start: 'top 86%' }
        });
    });

    // stagger numlist / flow / checklist children
    gsap.utils.toArray('.numlist, .flow, .checklist').forEach(list => {
        gsap.from(list.children, {
            y: 26, opacity: 0, duration: .7, ease: 'power2.out', stagger: .12,
            scrollTrigger: { trigger: list, start: 'top 82%' }
        });
    });

    // animated counters
    gsap.utils.toArray('[data-count]').forEach(el => {
        const end = +el.dataset.count;
        const obj = { v: 0 };
        ScrollTrigger.create({
            trigger: el, start: 'top 88%', once: true,
            onEnter: () => gsap.to(obj, { v: end, duration: 1.4, ease: 'power2.out', onUpdate: () => { el.textContent = Math.round(obj.v); } })
        });
    });

    // horizontal pinned process (desktop only)
    const mm = gsap.matchMedia();
    mm.add('(min-width: 961px)', () => {
        const track = document.getElementById('processTrack');
        const vp = track.parentElement;
        const getAmt = () => Math.max(0, track.scrollWidth - vp.clientWidth);
        const tween = gsap.to(track, {
            x: () => -getAmt(), ease: 'none',
            scrollTrigger: {
                trigger: '#proses', start: 'top top', end: () => '+=' + getAmt(),
                pin: true, scrub: 1, invalidateOnRefresh: true, anticipatePin: 1
            }
        });
        return () => tween.kill();
    });

    ScrollTrigger.refresh();
});
</script>
</body>
</html>
