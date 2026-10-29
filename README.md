<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#0F1D17">
<link rel="manifest" href="manifest.webmanifest">
<link rel="apple-touch-icon" href="icon-192.png">
<meta name="mobile-web-app-capable" content="yes"><meta name="apple-mobile-web-app-capable" content="yes"><meta name="apple-mobile-web-app-title" content="Vertex"><meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<script>try{var t=localStorage.getItem("vertex_theme");if(t==="light"||t==="dark")document.documentElement.setAttribute("data-theme",t)}catch(e){}
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<title>Vertex — Ton compagnon trail</title>
<link rel="icon" href="data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%2064%2064%22%3E%3Crect%20width%3D%2264%22%20height%3D%2264%22%20rx%3D%2216%22%20fill%3D%22%23ff6a2b%22%2F%3E%3Cpath%20d%3D%22M12%2050%2028%2022l9%2013%207-9%2010%2024z%22%20fill%3D%22%2310140f%22%2F%3E%3C%2Fsvg%3E" type="image/svg+xml">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css">
<style>
:root{--bg:#0F1D17;--bg2:#14271E;--card:#16281F;--card2:#1D3328;--line:rgba(242,239,228,.14);--ink:#F2EFE4;--mut:#A8B8AB;--acc:#F27A2A;--acc2:#A9C79B;--ice:#8FBDB5;--bad:#FF8F80;--on-acc:#1A0F07;--on-acc2:#0F1D17;--inp:#0F1D17;--pane:#14271E;--sidebg:linear-gradient(180deg,#12241C,#0B1611);--navbg:rgba(11,22,17,.96);--vio:#B8A9DC;--yel:#E6B84A;--pink:#E89AAA;--goodbg:rgba(169,199,155,.10);--hero-end:#0F1D17;--sh:0 1px 0 rgba(242,239,228,.04) inset,0 14px 30px -22px rgba(0,0,0,.7);--topo:rgba(168,184,171,.075);color-scheme:dark;--font-head:"Bahnschrift","Barlow Condensed","Roboto Condensed","Arial Narrow","Helvetica Neue",system-ui,sans-serif;--font-body:system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",sans-serif;--r:16px;--side:232px}
@media(prefers-color-scheme:light){
 :root:not([data-theme="dark"]){--bg:#F3F0E6;--bg2:#ECE8DB;--card:#FBF9F2;--card2:#ECE8DB;--line:rgba(30,40,35,.16);--ink:#1E2823;--mut:#4F5C54;--acc:#A63F08;--acc2:#2D5A40;--ice:#2B6F69;--bad:#B3261E;--on-acc:#FFFFFF;--on-acc2:#FFFFFF;--inp:#FFFFFF;--pane:#FBF9F2;--sidebg:linear-gradient(180deg,#FBF9F2,#ECE8DB);--navbg:rgba(251,249,242,.96);--vio:#6A4FA3;--yel:#8A5A00;--pink:#A8325C;--goodbg:rgba(45,90,64,.10);--hero-end:rgba(15,29,23,.88);--sh:0 8px 24px -18px rgba(30,40,35,.45);--topo:rgba(30,40,35,.07);color-scheme:light}
}
:root[data-theme="light"]{--bg:#F3F0E6;--bg2:#ECE8DB;--card:#FBF9F2;--card2:#ECE8DB;--line:rgba(30,40,35,.16);--ink:#1E2823;--mut:#4F5C54;--acc:#A63F08;--acc2:#2D5A40;--ice:#2B6F69;--bad:#B3261E;--on-acc:#FFFFFF;--on-acc2:#FFFFFF;--inp:#FFFFFF;--pane:#FBF9F2;--sidebg:linear-gradient(180deg,#FBF9F2,#ECE8DB);--navbg:rgba(251,249,242,.96);--vio:#6A4FA3;--yel:#8A5A00;--pink:#A8325C;--goodbg:rgba(45,90,64,.10);--hero-end:rgba(15,29,23,.88);--sh:0 8px 24px -18px rgba(30,40,35,.45);--topo:rgba(30,40,35,.07);color-scheme:light}
:root[data-theme="dark"]{--bg:#0F1D17;--bg2:#14271E;--card:#16281F;--card2:#1D3328;--line:rgba(242,239,228,.14);--ink:#F2EFE4;--mut:#A8B8AB;--acc:#F27A2A;--acc2:#A9C79B;--ice:#8FBDB5;--bad:#FF8F80;--on-acc:#1A0F07;--on-acc2:#0F1D17;--inp:#0F1D17;--pane:#14271E;--sidebg:linear-gradient(180deg,#12241C,#0B1611);--navbg:rgba(11,22,17,.96);--vio:#B8A9DC;--yel:#E6B84A;--pink:#E89AAA;--goodbg:rgba(169,199,155,.10);--hero-end:#0F1D17;--sh:0 1px 0 rgba(242,239,228,.04) inset,0 14px 30px -22px rgba(0,0,0,.7);--topo:rgba(168,184,171,.075);color-scheme:dark}
.hero{--acc:#F27A2A;--acc2:#A9C79B;--on-acc:#1A0F07;--on-acc2:#0F1D17;--ink:#F2EFE4;--mut:#C3CEC4;--line:rgba(242,239,228,.24);color:#F2EFE4}
*{box-sizing:border-box;margin:0;padding:0}
html{-webkit-text-size-adjust:100%}
body{font:16px/1.5 var(--font-body);min-height:100vh;overflow-x:hidden}
button, input, select, textarea{font:inherit;color:inherit}
button{cursor:pointer;border:0;background:none}
.cond{font-family:var(--font-head);font-stretch:condensed;text-transform:uppercase}
.sm{font-size:.85rem}
.xs{font-size:.74rem}
.tc{text-align:center}
.hide{display:none!important}
/* layout */
.app{display:grid;grid-template-columns:var(--side) 1fr;min-height:100vh}
.side{position:sticky;top:0;height:100vh;padding:22px 14px;display:flex;flex-direction:column;gap:6px}
.brand{display:flex;gap:10px;align-items:center;padding:4px 8px 18px}
.logo{width:36px;height:36px;display:grid;place-items:center}
.nav button{display:flex;align-items:center;gap:12px;width:100%;padding:12px 14px;text-align:left;min-height:46px}
.nav button i{font-style:normal;font-size:1.25rem}
main{min-width:0;padding-bottom:40px}
.wrap{max-width:1080px;margin:0 auto;padding:22px 20px}
@media(max-width:899px){
 .app{display:block}
 .side{position:fixed;inset:auto 0 0 0;height:auto;flex-direction:row;padding:6px 6px calc(6px + env(safe-area-inset-bottom));z-index:60;background:var(--navbg);backdrop-filter:blur(14px);border-top:1px solid var(--line);border-right:0;gap:2px;overflow-x:auto}
 .brand{display:none}
 .nav{display:flex;gap:2px;width:100%}
 .nav button{flex-direction:column;gap:0;padding:6px 4px;font-size:.62rem;justify-content:center;text-align:center;min-width:56px;min-height:54px}
 .nav button.on{box-shadow:none;background:var(--acc);color:var(--on-acc)}
 main{padding-bottom:90px}
 .wrap{padding:16px 14px}
}
/* hero */
.hero{position:relative;display:flex;align-items:flex-end;overflow:hidden;isolation:isolate}
.hero-bg{position:absolute;inset:0;z-index:-2;background-size:cover;background-position:center}
.hero-bg svg{width:100%;height:100%;display:block}
.hero::after{content:"";position:absolute;inset:0;z-index:-1}
.hero-in{width:100%;max-width:1080px;margin:0 auto;padding:30px 20px 26px}
.hero h1{line-height:.95}
.hero p{max-width:560px;margin-top:8px}
.hero-tools{position:absolute;top:14px;right:14px;display:flex;gap:6px}
.next{display:flex;gap:12px;flex-wrap:wrap;margin-top:16px;align-items:center}
.cdn{display:flex;gap:8px}
.cdn div{padding:8px 12px;text-align:center}
.cdn b{display:block;line-height:1}
.cdn span{font-size:.65rem;text-transform:uppercase;letter-spacing:.06em}
/* cards */
.card{margin-bottom:16px}
.card h2, .sec h2{margin-bottom:10px}
.sec{display:flex;justify-content:space-between;align-items:baseline;gap:10px}
.sec h2{margin:0}
.grid{display:grid;gap:14px}
.g2{grid-template-columns:repeat(2,1fr)}
.g3{grid-template-columns:repeat(3,1fr)}
@media(max-width:760px){
 .g3{grid-template-columns:repeat(2,1fr)}
}
@media(max-width:520px){
 .g2{grid-template-columns:1fr}
}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;min-height:46px;padding:0 20px;text-decoration:none}
.btn.s{padding:0 14px;font-size:.85rem}
.row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
/* rings */
.rings{display:grid;position:relative;z-index:3;}
@media(max-width:899px){
 .rings{grid-template-columns:repeat(3,1fr)}
}
.ringc{width:100%;}
.ring{width:100%;max-width:104px;display:block;margin:0 auto}
.ring .t{fill:none;}
.ring .f{fill:none;stroke-linecap:round;transform:rotate(-90deg);transform-origin:50px 50px;animation:rin 1.1s cubic-bezier(.3,.9,.3,1) both;}
@keyframes rin{from{stroke-dashoffset:var(--c)}}
.ring text{fill:var(--ink);font-weight:800;font-size:17px;font-family:var(--font-head)}
.ring .u{font-size:8px;fill:var(--mut);font-weight:700}
.ringc small{display:block;margin-top:4px;font-size:.72rem;text-transform:uppercase;font-weight:800}
/* quick */
.quick{display:flex;gap:12px;align-items:center;text-align:left;width:100%;padding:16px}
.quick i{font-style:normal;font-size:1.8rem}
.quick b{display:block}
/* race cards */
.rc{display:flex;gap:14px;width:100%;text-align:left;padding:14px;margin-bottom:10px}
.dbox{flex:0 0 56px;height:62px;display:flex;flex-direction:column;align-items:center;justify-content:center;line-height:1.1}
.dbox b{font-size:1.4rem}
.dbox em{font-style:normal;font-size:.68rem;font-weight:800;text-transform:uppercase}
.tag{display:inline-block;font-size:.7rem;font-weight:800;padding:2px 9px;border-radius:999px;text-transform:uppercase}
.chips{display:flex;flex-wrap:wrap;gap:6px;margin-top:6px}
.chip{font-size:.78rem;padding:2px 10px;border-radius:999px}
/* forms */
.f{display:flex;flex-direction:column;gap:4px;font-size:.8rem;font-weight:700;color:var(--mut)}
.f input, .f select, .f textarea{min-height:44px;padding:8px 12px;border-radius:12px;background:var(--inp);border:1px solid var(--line);color:var(--ink);font-weight:500;width:100%}
.f textarea{min-height:80px}
.frm{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
@media(max-width:520px){
 .frm{grid-template-columns:1fr}
}
.frm .full{grid-column:1/-1}
/* tables / charts */
table{width:100%;border-collapse:collapse;font-size:.85rem}
th, td{padding:9px 6px;border-bottom:1px solid var(--line);text-align:left}
th{font-size:.72rem;text-transform:uppercase;letter-spacing:.05em}
.tscroll{overflow-x:auto}
.chart{width:100%;height:auto;display:block;min-width:300px}
.chart text{font-size:12px}
.chart .val{fill:var(--ink);font-weight:800;font-size:13px}
.chart .lab{fill:var(--ink);font-size:12px;font-weight:600}
.chart .gl{stroke-dasharray:3 4}
.prog .chart{min-width:0}
.prog .pt{cursor:pointer}
.prog .pt circle{transition:r .15s}
.prog .pt:hover circle, .prog .pt:focus-visible circle{r:8}
.prog .pt:focus-visible{outline:none}
.prog .pt:focus-visible circle{stroke:var(--ink);stroke-width:2}
.chartbox{overflow-x:auto;-webkit-overflow-scrolling:touch;margin:0 -4px;padding:0 4px}
.kv{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:10px}
.kv div{padding:10px 12px}
.kv b{display:block}
.kv span{font-size:.72rem;text-transform:uppercase}
.note{border-left:4px solid var(--acc);padding:10px 14px;font-size:.88rem;margin:10px 0}
.note.good{border-color:var(--acc2)}
.empty{text-align:center;padding:30px 16px;border:2px dashed var(--line);color:var(--mut)}
.wk{border-left:4px solid var(--line)}
.wk.cur{border-left-color:var(--acc)}
.ses{display:grid;grid-template-columns:54px 1fr;gap:10px;padding:10px 0;border-top:1px solid var(--line)}
.ses:first-of-type{border-top:0}
.ses.past{opacity:.5}
.ses .d{font-weight:800;font-size:.75rem;text-transform:uppercase;color:var(--acc)}
.dot{display:inline-block;width:9px;height:9px;border-radius:50%;margin-right:6px}
.sel{display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-bottom:14px}
.sel select{min-height:44px;padding:0 12px;border-radius:12px;background:var(--card2);border:1px solid var(--line);max-width:100%}
/* modal */
.mod{position:fixed;inset:0;z-index:200;display:flex;align-items:flex-end;justify-content:center}
.mp{position:relative;width:min(100%,640px);max-height:92vh;overflow:auto;padding:22px 18px calc(24px + env(safe-area-inset-bottom));animation:up .25s ease}
@media(min-width:760px){
 .mod{align-items:center}
 .mp{border-radius:26px}
}
@keyframes up{from{transform:translateY(30px);opacity:0}}
.mx{position:absolute;top:10px;right:10px;width:42px;height:42px;border-radius:50%}
.mp h2{padding-right:46px;margin-bottom:6px}
.toast{position:fixed;left:50%;transform:translateX(-50%);top:14px;z-index:300;padding:12px 18px;font-weight:700;max-width:92%;box-shadow:0 10px 30px rgba(0,0,0,.4)}
.toast.err{background:var(--bad);color:#fff}
@media(max-width:899px){

}
@media(max-width:760px){

}
.lvlname{font-size:2.3rem;line-height:1}
.bar{border-radius:99px;overflow:hidden;margin:10px 0 6px}
.bar i{display:block;height:100%;border-radius:99px}
.sc{border:1px solid var(--line);display:grid;gap:8px}
.sc.race{border-color:var(--acc);background:rgba(255,106,43,.12)}
.sc-h{display:flex;align-items:center;gap:10px}
.sc-day{font-size:.72rem;font-weight:700;color:var(--mut);text-transform:uppercase;letter-spacing:.05em;min-width:48px}
.sc-t{flex:1;line-height:1.25}
.sc input[type=checkbox]{width:28px;height:28px;accent-color:var(--acc);flex:none}
.sc-m{display:flex;flex-wrap:wrap;gap:6px}
.sc-m span{border-radius:999px;padding:3px 10px;font-size:.8rem;font-weight:700}
.sc-d summary{cursor:pointer;font-size:.78rem;color:var(--mut);padding:4px 0;min-height:32px}
.sc-d p{font-size:.85rem;line-height:1.5;margin-top:4px}
.sc.rest{background:transparent;border-style:dashed}
.sc.rest .sc-h{font-size:.85rem;color:var(--mut)}
@media(max-width:820px){
 .sessL{display:grid;gap:8px;margin:10px 0}
}
.nw td, .nw th{white-space:nowrap}
.apv input[type=date]{background:var(--inp);color:var(--ink);border:1px solid var(--line);border-radius:10px;padding:6px 8px;font:inherit;font-size:.85rem}
.apv-nav{display:flex;align-items:center;justify-content:space-between;gap:8px;margin:10px 0}
.apv-nav .tc{flex:1}
.apv-items{list-style:none;display:grid;gap:8px;margin:8px 0}
.apv-items>li{background:var(--card2);border:1px solid var(--line);border-radius:12px;padding:10px 12px}
.apv-items>li.dn{opacity:.55;text-decoration:line-through}
.apv-items label{display:flex;gap:10px;align-items:flex-start;cursor:pointer;line-height:1.45}
.apv-items input[type=checkbox]{width:24px;height:24px;flex:none;accent-color:var(--acc2);margin-top:1px}
.apv-items ul{margin:4px 0 0 18px;font-size:.88rem;color:var(--mut)}
.apv-note{background:var(--card);border-radius:10px;padding:8px 10px;margin-top:6px}
.apv-wk{display:grid;grid-template-columns:repeat(7,1fr);gap:6px}
.apv-wd{display:flex;flex-direction:column;gap:4px;text-align:left;background:var(--card2);border:1px solid var(--line);border-radius:12px;padding:8px;min-width:0;align-items:flex-start}
.apv-wd ul{list-style:none;font-size:.74rem;display:grid;gap:2px;color:var(--ink);width:100%}
.apv-wd li{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.apv-wd.today{border-color:var(--acc2)}
.apv-wd.full{background:rgba(169,199,155,.14)}
.apv-wd:disabled{opacity:.45;cursor:default}
.apv-cal{display:grid;grid-template-columns:repeat(7,1fr);gap:4px}
.apv-cal>i{font-style:normal;text-align:center;font-size:.72rem;color:var(--mut);font-weight:700}
.apv-c{min-height:52px;display:flex;flex-direction:column;align-items:flex-start;gap:2px;background:var(--card2);border:1px solid var(--line);border-radius:10px;padding:5px;min-width:0;text-align:left}
.apv-c b{font-size:.85rem}
.apv-c .apv-l{display:none;font-size:.68rem;color:var(--mut);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;width:100%}
.apv-c .apv-d{font-size:.66rem;color:var(--mut)}
.apv-c.today{border-color:var(--acc2);box-shadow:0 0 0 1px var(--acc2)}
.apv-c.full{background:rgba(169,199,155,.2)}
.apv-c.part{background:rgba(255,106,43,.14)}
.apv-c:disabled{opacity:.35;cursor:default}
@media(min-width:700px){
 .apv-c{min-height:74px}
 .apv-c .apv-l{display:block}
}
@media(max-width:699px){
 .apv-wk{grid-template-columns:1fr}
 .apv-wd ul{font-size:.82rem}
 .apv-wd li{white-space:normal}
}
.fiche table{font-size:.92rem}
.fiche td b{font-size:1.05rem}
.fiche tr.nx td{background:rgba(169,199,155,.18)}
.evo{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:14px}
.evo-c{padding:16px}
.evo-c h3{margin:0 0 2px;display:flex;justify-content:space-between;gap:8px;align-items:baseline}
.evo-svg{width:100%;height:auto;display:block;margin:4px 0}
.evo-svg text{fill:var(--mut);font-size:10px;font-weight:700}
.evo-v{font-size:.86rem;margin:2px 0 12px;line-height:1.45}
.evo-eds{display:flex;gap:8px;flex-wrap:wrap}
.evo-e{display:grid;gap:2px;text-align:left;padding:8px 12px;min-width:88px;border:1px solid var(--line);border-radius:12px;background:var(--card2);color:var(--ink);cursor:pointer}
.evo-e b{font-family:var(--font-head);font-size:1.02rem;letter-spacing:.02em}
.evo-e span{font-size:.8rem;font-variant-numeric:tabular-nums}
.evo-e.best{border-color:var(--acc)}
.evo-y{gap:8px;margin:16px 0 0;align-items:center}
.dev{font-weight:700}
.dev.up{color:var(--acc2)}
.dev.dn{color:var(--bad)}
@media print{
 body.printing>*:not(#modal){display:none!important}
 body.printing, body.printing #modal{background:#fff!important;overflow:visible!important}
 body.printing #modal{position:static!important;display:block!important;padding:0!important}
 body.printing .mp{max-height:none!important;overflow:visible!important;width:100%!important;max-width:none!important;border:0!important;border-radius:0!important;padding:0!important;animation:none!important}
 body.printing .mp, body.printing .mp *{background:transparent!important;color:#000!important;border-color:#999!important;box-shadow:none!important}
 body.printing .mx, body.printing .noprint{display:none!important}
 body.printing .fiche table{font-size:11pt}
 body.printing tr{break-inside:avoid}
}
@media(prefers-reduced-motion:reduce){
 *{animation:none!important;transition:none!important}
}
.savepill{position:fixed;right:12px;bottom:12px;z-index:90;font-size:.75rem;padding:6px 10px;border-radius:999px;border:1px solid var(--line);color:var(--mut)}
.savepill[data-s=saved]{color:var(--acc2)}
.savepill[data-s=error]{color:var(--bad)}
.savepill:empty{display:none}
@media(max-width:899px){
 .savepill{bottom:78px}
}
/* ===== v6 : design & nouveaux blocs ===== */
details.hist{padding:16px 18px}
details.hist>summary{cursor:pointer;list-style:none;display:flex;align-items:center;gap:10px;justify-content:space-between;flex-wrap:wrap}
details.hist>summary::-webkit-details-marker{display:none}
details.hist>summary::after{content:"▾";font-size:1.1rem;color:var(--mut);transition:transform .2s;margin-left:auto}
details.hist[open]>summary::after{transform:rotate(180deg)}
.mapcard{padding:16px}
#map{height:340px;overflow:hidden;background:var(--bg2);z-index:1}
.leaflet-container{font-family:inherit}
.leaflet-tooltip{border:1px solid var(--line);border-radius:10px;box-shadow:var(--sh);font-weight:700}
.leaflet-bar,.leaflet-control-layers{border:1px solid var(--line)!important;border-radius:12px!important;box-shadow:var(--sh)!important;overflow:hidden}
.leaflet-bar a,.leaflet-control-layers{background-color:var(--card)!important;color:var(--ink)!important;border-bottom-color:var(--line)!important}
.leaflet-bar a:hover{background-color:var(--card2)!important}
.leaflet-control-layers-toggle{background-image:none!important;width:34px!important;height:34px!important;display:grid;place-items:center}
.leaflet-control-layers-toggle::before{content:"🗺️";font-size:18px;line-height:1}
.leaflet-bar a.gp-fit{font-size:18px;font-weight:800;text-align:center;cursor:pointer}
.leaflet-control-layers-expanded{padding:8px 12px;font-weight:600;font-size:.85rem}
.leaflet-control-attribution{background:var(--navbg)!important;color:var(--mut)!important;font-size:10px}
.leaflet-control-attribution a{color:var(--acc2)!important}
.leaflet-control-scale-line{background:var(--navbg)!important;color:var(--ink)!important;border-color:var(--mut)!important;font-weight:700}
.gp-pin span{display:grid;place-items:center;width:100%;height:100%;border-radius:50%;border:3px solid #fff;box-shadow:0 2px 8px rgba(0,0,0,.5);font-size:15px;font-weight:800;box-sizing:border-box;background:var(--acc2);color:var(--on-acc2)}
.gp-pin span.up{background:var(--acc);color:var(--on-acc)}
.gp-km span{display:grid;place-items:center;width:100%;height:100%;border-radius:50%;background:var(--card);color:var(--ink);border:1.5px solid var(--ink);font:800 10px/1 var(--font-body);box-shadow:0 1px 4px rgba(0,0,0,.5);box-sizing:border-box}
:root[data-theme="dark"] .t-tint{filter:brightness(.8) saturate(.85) contrast(1.05)}
@media(prefers-color-scheme:dark){:root:not([data-theme="light"]) .t-tint{filter:brightness(.8) saturate(.85) contrast(1.05)}}
@media(max-width:600px){.gp-map{height:330px}}
.filt{align-items:flex-end}
.filt .f{min-width:120px;flex:1 1 120px}
.aiout{white-space:pre-wrap;word-break:break-word;background:var(--bg2);border:1px solid var(--line);border-radius:14px;padding:14px;font-size:.92rem;line-height:1.55;max-height:560px;overflow:auto;margin-top:10px}
.aiout-wrap{margin-top:8px}
.aiout-wrap summary{cursor:pointer}
.nav{backdrop-filter:blur(10px)}
.hero-tools .btn{border-radius:999px}
/* sélecteurs date & heure */
.pkf{position:relative}
.pkf .pklab{font-size:.8rem;font-weight:700;color:var(--mut)}
.pkbtn{min-height:44px;padding:8px 12px;border-radius:12px;background:var(--inp);border:1px solid var(--line);color:var(--ink);font-weight:600;text-align:left;width:100%;font-size:.95rem}
.pkbtn[aria-expanded="true"]{border-color:var(--acc2)}
.pkbtn:focus-visible, .pkd:focus-visible, .clk-n:focus-visible, .pkseg button:focus-visible{outline:2px solid var(--acc2);outline-offset:2px}
.pkpop{margin-top:8px;padding:12px;border-radius:16px;background:var(--card2);border:1px solid var(--line)}
.pkhead{display:flex;align-items:center;justify-content:space-between;gap:8px;margin-bottom:8px;flex-wrap:wrap}
.pkgrid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;text-align:center}
.pkwd span{font-size:.72rem;font-weight:700;color:var(--mut);padding:4px 0}
.pkd{min-height:40px;border-radius:10px;background:transparent;border:1px solid transparent;color:var(--ink);font-weight:600;font-size:.9rem;padding:0}
.pkd:hover{background:var(--card)}
.pkd.out{color:var(--mut);opacity:.5}
.pkd.tod{border-color:var(--acc2)}
.pkd.sel{background:var(--acc2);color:var(--on-acc2)}
.pkfoot{display:flex;justify-content:space-between;align-items:center;gap:8px;margin-top:10px;flex-wrap:wrap}
.pkseg{display:inline-flex;border-radius:999px;background:var(--card);border:1px solid var(--line);padding:3px;gap:2px}
.pkseg button{min-height:34px;padding:4px 12px;border-radius:999px;background:transparent;color:var(--ink);font-weight:700;font-size:.85rem;border:0}
.pkseg button.on{background:var(--acc2);color:var(--on-acc2)}
.clk{position:relative;width:min(240px,78vw);aspect-ratio:1;margin:14px auto 6px;border-radius:50%;background:var(--card);border:1px solid var(--line)}
.clk-c{position:absolute;left:50%;top:50%;width:10px;height:10px;margin:-5px 0 0 -5px;border-radius:50%;background:var(--acc2)}
.clk-hand{position:absolute;inset:0;width:100%;height:100%;pointer-events:none}
.clk-hand line{stroke:var(--acc2);stroke-width:2;stroke-linecap:round}
.clk-n{position:absolute;width:38px;height:38px;margin:-19px 0 0 -19px;border-radius:50%;border:0;background:transparent;color:var(--ink);font-weight:700;font-size:.9rem;padding:0}
.clk-n:hover{background:var(--card2)}
.clk-n.on{background:var(--acc2);color:var(--on-acc2)}
.lk{display:flex;flex-wrap:wrap}
.lk:empty{display:none}
/* cercles segmentés (une portion par course) */
.ring .seg{fill:none;transform:rotate(-90deg);transform-origin:50px 50px;}
/* lignes de course : même structure pour toutes */
.rc{min-height:92px;align-items:stretch}
.rc-main{flex:1;min-width:0;display:flex;flex-direction:column;justify-content:center;gap:6px}
.rc-name{display:block;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.rc-side{flex:0 0 auto;min-width:104px;display:flex;flex-direction:column;align-items:flex-end;justify-content:center;gap:6px}
.chip.empty{opacity:.45}
.rc-main .chips{align-items:center;align-content:flex-start;align-self:flex-start;flex:0 0 auto}
.rc-main .chip{line-height:1.5;padding:3px 10px;white-space:nowrap}
/* ===== v7 : visuel, jeu, landing dynamique ===== */
@keyframes drift{from{transform:translateX(-200px)}to{transform:translateX(1000px)}}
@keyframes tw{50%{opacity:.2}}
@keyframes dash{to{stroke-dashoffset:-22}}
@keyframes pulse{50%{transform:scale(1.08);opacity:.85}}
.rot{min-height:1.6em;transition:opacity .4s,transform .4s;display:block}
.rot.out{opacity:0;transform:translateY(6px)}
.rv{opacity:0}
.rv.in{opacity:1;transform:none}
.gam .bar i{animation:grow 1.2s cubic-bezier(.2,.9,.3,1) both}
@keyframes grow{from{width:0}}
.mbars rect{transform-box:fill-box;transform-origin:bottom;animation:bgrow .9s cubic-bezier(.2,.9,.3,1) both}
@keyframes bgrow{from{transform:scaleY(0)}}
.hs{display:flex;gap:12px;overflow-x:auto;scroll-snap-type:x mandatory;padding:4px 2px 14px;-webkit-overflow-scrolling:touch}
.tile{flex:0 0 min(260px,78vw);scroll-snap-align:start;text-align:left;border:1px solid var(--line);overflow:hidden;display:flex;flex-direction:column}
.tile-top{position:relative;background:linear-gradient(135deg,var(--tc1),var(--tc2));display:flex;align-items:flex-end}
.tile-top svg{width:100%;height:100%;position:absolute;inset:0}
.tile-d{position:relative;margin:0 0 8px 12px;font-size:2rem;line-height:1;text-shadow:0 2px 10px rgba(0,0,0,.5)}
.tile-b{padding:12px 14px 14px;display:grid;gap:6px}
.tile-b b{display:block;line-height:1.2}
/* plans : séances en cartes, bandeau de semaine, repas repliables */
.sessL{display:grid!important;grid-template-columns:repeat(auto-fill,minmax(290px,1fr));gap:10px;margin:12px 0}
.sc-ico{font-size:1.7rem;line-height:1;flex:none}
.sc-t{display:grid;gap:1px}
.sc-t small{font-size:.68rem}
.rpe{display:flex;gap:3px}
.rpe i{flex:1;height:7px;border-radius:4px;background:var(--line)}
.rpe i.on{background:linear-gradient(90deg,var(--acc2),var(--acc))}
.wstrip{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin:12px 0}
.wd{display:flex;flex-direction:column;align-items:center;gap:2px;padding:8px 2px;border:1px solid var(--line);border-bottom:3px solid var(--tc,var(--line));min-width:0}
.wd small{font-size:.62rem;text-transform:uppercase;color:var(--mut);font-weight:700}
.wd span{font-size:1.25rem}
.wd b{font-size:.66rem;white-space:nowrap}
.wd.done{background:var(--goodbg)}
.gam{margin:6px 0 14px}
.gam-top{display:flex;justify-content:space-between;align-items:center}
.chip2{display:inline-flex;gap:5px;align-items:center;background:var(--card2);border:1px solid var(--line);border-radius:999px;padding:2px 10px;font-size:.78rem;font-weight:700}
.nday{border:1px solid var(--line);padding:14px;margin-bottom:12px}
.nday.today{border-top-color:var(--acc);box-shadow:0 0 0 1px var(--acc) inset}
.meal{border:1px solid var(--line);margin:8px 0;overflow:hidden}
.meal>summary{list-style:none;cursor:pointer;display:flex;align-items:center;gap:10px;padding:11px 14px;position:relative;font-weight:700}
.meal>summary::-webkit-details-marker{display:none}
.meal>summary::after{content:'▾';margin-left:6px;color:var(--mut);transition:transform .2s}
.meal[open]>summary::after{transform:rotate(180deg)}
.meal-g{margin-left:auto;font-size:.8rem;color:var(--acc2);font-weight:800}
.meal>*:not(summary){padding:0 14px 12px}
.meal>ul.apv-items{margin:0;padding:0 12px 12px}
.meal.fin>summary{color:var(--acc2)}
details.hist>summary+*{margin-top:12px}
details.fold>summary{display:grid;grid-template-columns:40px minmax(0,1fr) auto;column-gap:12px;row-gap:0;align-items:center}
details.fold>summary::after{grid-column:3;grid-row:1/3;margin-left:0}
.fold-ic{grid-column:1;grid-row:1/3;display:grid;place-items:center;width:40px;height:40px;border-radius:12px;background:var(--card2);border:1px solid var(--line);font-size:1.2rem}
details.fold>summary h2{grid-column:2;grid-row:1;margin:0;font-size:1.12rem;line-height:1.2;align-self:end}
details.fold>summary small{grid-column:2;grid-row:2;font-size:.76rem;color:var(--mut);align-self:start;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.rcal-h{display:flex;align-items:center;gap:8px;flex-wrap:wrap;margin:0 0 12px}
.rcal-t{font-size:1.35rem;text-transform:capitalize;margin-left:8px}
.rcal-g{display:grid;grid-template-columns:repeat(7,minmax(0,1fr));border:1px solid var(--line);border-radius:14px;overflow:hidden}
.rcal-w{padding:7px 4px;text-align:center;font-size:.7rem;font-weight:800;text-transform:uppercase;letter-spacing:.05em;color:var(--mut);background:var(--card2);border-bottom:1px solid var(--line)}
.rcal-w .s{display:none}
.rcal-d{min-height:112px;padding:4px 4px 6px;display:flex;flex-direction:column;gap:3px;min-width:0;border-right:1px solid var(--line);border-bottom:1px solid var(--line)}
.rcal-d:nth-child(7n){border-right:0}
.rcal-d.we{background:rgba(127,127,127,.06)}
.rcal-d.out>.rcal-n{opacity:.45}
.rcal-d.out .rcal-e{opacity:.7}
.rcal-n{align-self:center;display:grid;place-items:center;min-width:24px;height:24px;padding:0 6px;border-radius:99px;font-size:.78rem;font-weight:700;white-space:nowrap}
.rcal-d.today>.rcal-n{background:var(--acc);color:var(--on-acc)}
.rcal-e{display:flex;flex-direction:column;align-items:flex-start;gap:1px;width:100%;min-width:0;text-align:left;padding:5px 8px;border-radius:8px;border-left:4px solid var(--cc);background:var(--card2);background:color-mix(in srgb,var(--cc) 40%,var(--card));color:var(--ink);font-size:.78rem;line-height:1.25;cursor:pointer;box-shadow:0 1px 0 rgba(0,0,0,.18)}
.rcal-e:hover{background:color-mix(in srgb,var(--cc) 58%,var(--card))}
.rcal-e b{display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;font-weight:800;overflow-wrap:anywhere}
.rcal-e small{font-size:.68rem;opacity:.85;font-weight:600}
.rcal-d.has{background:color-mix(in srgb,var(--cc) 11%,transparent)}
.rcal-d.has>.rcal-n{font-weight:900;box-shadow:inset 0 0 0 2px var(--cc)}
.rcal-d.today.has>.rcal-n{box-shadow:none}
.rcal-e.unc{background:transparent;border:1px dashed var(--cc);border-left:3px solid var(--cc)}
.rcal-e.dnf b{text-decoration:line-through}
.rcal-more{font-size:.68rem;color:var(--mut);padding:0 6px}
.rcal-ml{display:none;list-style:none;margin:12px 0 0;padding:0;gap:6px}
.rcal-ml button{display:grid;grid-template-columns:auto 1fr;gap:0 10px;align-items:center;width:100%;text-align:left;padding:9px 12px;border-radius:12px;border:1px solid var(--line);border-left:4px solid var(--cc);background:var(--card2);color:var(--ink);cursor:pointer}
.rcal-ml .d{grid-row:1/3;font-weight:800;font-size:.8rem;text-transform:capitalize;min-width:46px}
.rcal-ml b{font-size:.9rem;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.rcal-ml small{font-size:.74rem;color:var(--mut)}
.rcal-leg{display:flex;flex-wrap:wrap;gap:6px 14px;margin-top:10px;font-size:.74rem;color:var(--mut)}
.rcal-leg i{display:inline-block;width:12px;height:12px;border-radius:4px;margin-right:5px;vertical-align:-2px}
.dbox::before{background:var(--cc,var(--acc))!important}
@media(max-width:600px){.rcal-d{min-height:64px;padding:3px 2px 4px}.rcal-w .l{display:none}.rcal-w .s{display:inline}.rcal-d.has{background:color-mix(in srgb,var(--cc) 20%,transparent)}.rcal-e{flex-direction:row;height:10px;min-height:10px;padding:0;border:0;border-radius:99px;background:var(--cc);box-shadow:none}.rcal-e.unc{background:transparent;border:2px dashed var(--cc)}.rcal-e b,.rcal-e small{display:none}.rcal-more{font-size:.6rem;padding:0}.rcal-ml{display:grid}.rcal-n{min-width:20px;height:20px;font-size:.7rem;padding:0 3px}.rcal-t{font-size:1.15rem;margin-left:2px}}
details.nday{padding:0}
details.nday>summary{list-style:none;cursor:pointer;display:flex;align-items:center;gap:10px;flex-wrap:wrap;padding:14px}
details.nday>summary::-webkit-details-marker{display:none}
details.nday>summary::after{content:'▾';margin-left:auto;color:var(--mut);transition:transform .2s}
details.nday[open]>summary::after{transform:rotate(180deg)}
.nday.race{border-top-color:var(--yel,#f5c542)}
.stack{display:flex;height:16px;border-radius:999px;overflow:hidden;background:var(--line);margin:8px 0}
.stack i{display:block;height:100%}
.leg{display:flex;gap:10px;flex-wrap:wrap;font-size:.78rem;color:var(--mut)}
.leg b{color:var(--ink)}
.fsum{display:grid;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));gap:8px;margin:10px 0}
.fsum>div{background:var(--card2);border:1px solid var(--line);border-radius:16px;padding:10px;text-align:center}
.fsum i{font-style:normal;font-size:1.5rem;display:block}
.fsum b{font-size:1.15rem;display:block}
.fsum span{font-size:.7rem;color:var(--mut)}
.syncb{display:inline-flex;gap:6px;align-items:center;font-size:.75rem;color:var(--acc2);font-weight:700}
@media(prefers-reduced-motion:reduce){
 .gam .bar i, .mbars rect{animation:none!important}
 .rv{opacity:1!important;transform:none!important;transition:none!important}
 .rot{transition:none}
}
@media(max-width:560px){
 .hero{min-height:520px}
 .cdn{gap:6px}
 .cdn div{min-width:58px;padding:8px}
 .wd b{font-size:.58rem}
}
.sc{position:relative;padding:0}
.sc.rest{padding:8px 12px}
.sc-det>summary{list-style:none;cursor:pointer;display:grid;gap:8px;padding:12px 52px 12px 12px}
.sc-det>summary::-webkit-details-marker{display:none}
.sc-ck{position:absolute;top:12px;right:12px;width:28px;height:28px;accent-color:var(--acc2);z-index:2}
.sc-more{font-size:.74rem;color:var(--acc);font-weight:700}
.sc-det[open] .sc-more{display:none}
.sc-body{padding:12px 12px 14px;display:grid;gap:12px;border-top:1px dashed var(--line)}
.sc-info{display:grid;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));gap:8px}
.sc-info>div{background:var(--card);border:1px solid var(--line);border-radius:12px;padding:8px 10px;display:grid}
.sc-info i{font-style:normal}
.sc-info small{font-size:.66rem;color:var(--mut);text-transform:uppercase}
.sc-info b{font-size:.85rem;line-height:1.3}
.stps{list-style:none;display:grid;gap:6px;margin:0;padding:0}
.stp{display:flex;gap:10px;align-items:flex-start;background:var(--card);border:1px solid var(--line);border-radius:12px;padding:9px 10px;line-height:1.4}
.stp-n{flex:none;width:24px;height:24px;border-radius:50%;font-weight:800;font-size:.78rem;display:grid;place-items:center}
.stp.soft .stp-n{background:var(--line);color:var(--ink)}
.stp.soft{opacity:.85}
.ser{border-radius:6px;padding:0 5px;white-space:nowrap}
.sc.dn{opacity:.6}
.sc.dn .sc-t b{text-decoration:line-through}
.sessL{align-items:start}
.mealw{position:relative}
.mealw>.sc-ck{top:8px;right:10px;width:26px;height:26px}
.mealw .meal>summary{padding-right:48px}
.mealw.dn .meal{opacity:.55;border-color:var(--acc2)}
.mealw.dn .meal>summary span:first-child{text-decoration:line-through}
.nday.fin{border-top-color:var(--acc2);background:var(--goodbg)}
/* ===== v8 : refonte graphique « Sentier » — forêt, sauge, anthracite, orange trail ===== */
/* Jetons de design : tout est piloté par les variables de :root (couleurs, typographies, rayons, ombres). */
:root{--ease:cubic-bezier(.2,.7,.2,1)}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--ink);font-feature-settings:"tnum" 1,"lnum" 1}
.skip{text-decoration:none;transition:top .15s}
.skip:focus{top:12px}
.topo-bg{position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden}
.topo-bg svg{width:100%;height:100%;display:block}
.topo-bg path{fill:none;stroke:var(--topo);stroke-width:1.1;vector-effect:non-scaling-stroke;stroke-linejoin:round}
.app{position:relative;z-index:1}
:focus-visible{outline:3px solid var(--acc);outline-offset:2px;border-radius:10px}
.cond{font-weight:700;letter-spacing:.045em}
h2.cond{letter-spacing:.03em}
.mut{color:var(--mut)}
/* navigation */
.side{background:var(--sidebg);border-right:1px solid var(--line)}
.logo{background:var(--acc)}
.logo svg path{fill:#1A0F07}
.nav button{color:var(--mut);font-weight:700}
.nav button:hover{background:var(--card2);color:var(--ink)}
@media(max-width:899px){
 .nav button.on{background:var(--acc);color:var(--on-acc);box-shadow:none}
 .nav button:hover{background:transparent}
 .side{backdrop-filter:none}
}
/* cartes : surface pleine, filet fin, pas de flou */
.card{border:1px solid var(--line);box-shadow:var(--sh);backdrop-filter:none;transition:border-color .2s}
.card h2, .sec h2{font-size:1.1rem}
.sec h2{font-size:1.2rem;position:relative;padding-left:14px}
.sec h2::before{content:"";position:absolute;left:0;top:.18em;bottom:.18em;width:4px;border-radius:2px;background:var(--acc)}
.nav button, .btn{min-height:44px}
/* boutons : un seul langage — plein orange, secondaire contour, validation sauge */
.btn{background:var(--acc);color:var(--on-acc);border:1px solid transparent;font-weight:800}
.btn.ghost{background:transparent;color:var(--ink);border:1px solid var(--line)}
.btn.ghost:hover{background:var(--card2)}
.btn.lime{background:var(--acc2);color:var(--on-acc2)}
.btn.red{background:transparent;color:var(--bad);border:1px solid var(--bad)}
.btn.s{min-height:40px}
.tag{background:var(--card2);border:1px solid var(--line)}
.tag.up{background:var(--acc2);color:var(--on-acc2);border-color:transparent}
.tag.warn{background:transparent;color:var(--acc);border-color:var(--acc)}
.chip{background:var(--card2);border:1px solid var(--line)}
/* formulaires */
.f input, .f select, .f textarea, .sel select, .pkbtn{background:var(--inp);border:1px solid var(--line);border-radius:12px}
/* hero : relief topographique + tracé GPS, sans mouvement */
.hero::after{background:linear-gradient(180deg,rgba(15,29,23,0) 0%,rgba(15,29,23,.10) 40%,var(--hero-end) 100%)}
.hero h1 span{color:var(--acc)}
.hero p{color:#E3E8DD}
.cloud, .trail{animation:none!important}
.cdn div{background:rgba(15,29,23,.72);backdrop-filter:none;border:1px solid rgba(242,239,228,.24)}
.cdn b{font-variant-numeric:tabular-nums}
.cdn span{color:#C3CEC4}
/* statistiques : chiffres en avant */
.rings{margin-top:-30px}
.ringc{border:1px solid var(--line);box-shadow:var(--sh)}
.ring .t{stroke:var(--line)}
.ring text{font-variant-numeric:tabular-nums}
.ringc small{color:var(--mut);letter-spacing:.08em}
.kv div{border-left:3px solid var(--acc)}
.kv b{font-weight:700;font-size:1.35rem;letter-spacing:.02em;color:var(--ink);font-variant-numeric:tabular-nums}
.kv span{color:var(--mut);letter-spacing:.06em}
.fiche .kv b{font-size:1.5rem}
.lvlname{color:var(--acc2)}
.bar{background:var(--card2);border:1px solid var(--line)}
.bar i{background:linear-gradient(90deg,var(--acc2),var(--acc))}
.note{background:rgba(242,122,42,.10);border-left-color:var(--acc)}
.note.good{background:var(--goodbg);border-left-color:var(--acc2)}
/* listes de courses, tuiles, accès rapides */
.rc{border:1px solid var(--line)}
.rc:hover{border-color:var(--acc)}
.dbox{background:var(--card2);border-radius:12px}
.dbox em{color:var(--acc)}
.quick{border:1px solid var(--line);border-left:4px solid var(--acc)}
.quick:hover{transform:none}
.tile{background:var(--card)}
.tile:hover{border-color:var(--acc)}
.tile-top::before{content:"";position:absolute;inset:0;background:repeating-radial-gradient(ellipse at 70% 120%,transparent 0 11px,rgba(242,239,228,.10) 11px 12px)}
.tile-top svg{z-index:1}
.tile-d{z-index:2;color:#F2EFE4}
.today-card{border-color:var(--acc);border-left-width:4px}
.aicard{background:var(--card);border-color:var(--acc2)}
/* séances, repas, plans */
.sc{background:var(--card2);border-left:5px solid var(--tc,var(--line))}
.sc:hover{transform:none}
.sc-m span{background:var(--card);border:1px solid var(--line)}
.stp-n{background:var(--acc);color:var(--on-acc)}
.ser{background:rgba(242,122,42,.16);color:var(--acc)}
.wd{background:var(--card2);border-radius:12px}
.wd.today{outline:2px solid var(--acc)}
.nday{background:var(--card);border-top:4px solid var(--acc2);border-radius:var(--r)}
.meal{background:var(--card2);border-radius:12px}
table{font-variant-numeric:tabular-nums}
th{color:var(--mut)}
/* graphiques */
.chart text{fill:var(--mut)}
.chart .gl{stroke:var(--line)}
.mapcard{background:var(--card)}
#map{border:1px solid var(--line);border-radius:12px}
.leaflet-tooltip{background:var(--card2);color:var(--ink);border-color:var(--line)}
/* fenêtres */
.mp{background:var(--pane);border:1px solid var(--line)}
.mx{background:var(--card2);border:1px solid var(--line)}
.toast{background:var(--acc2);color:var(--on-acc2)}
.savepill{background:var(--card2)}
/* mouvement : réduit au strict utile */
.rv{transform:translateY(8px);transition:opacity .35s ease,transform .35s ease}
.rv.in{transition:opacity .35s ease,transform .2s ease,border-color .2s}
@media(prefers-reduced-motion:reduce){
 *, *::before, *::after{animation:none!important;transition:none!important;scroll-behavior:auto!important}
 .rv{opacity:1!important;transform:none!important}
}
@media(max-width:560px){
 .hero{min-height:500px}
 .kv b{font-size:1.2rem}
 .wrap{padding:14px 12px}
}
/* correctif mobile : les lignes de course ne doivent jamais dépasser l'écran */
.rc{max-width:100%;min-width:0;overflow:hidden}
.rc-main .chips{max-width:100%}
.rc-name{max-width:100%}
@media(max-width:560px){
 .rc{gap:10px;padding:12px}
 .rc-side{min-width:0}
 .dbox{flex-basis:52px}
}
/* semaine avant la course : calendrier de 7 jours */
.cw-cal{display:grid;grid-template-columns:repeat(auto-fit,minmax(0,1fr));grid-auto-flow:column}
.cw-c{display:flex;flex-direction:column;align-items:center;border:1px solid var(--line);color:var(--ink);text-align:center}
.cw-c small{text-transform:uppercase;color:var(--mut);font-weight:700}
.cw-c b{font-family:var(--font-head)}
.cw-c span{font-size:.66rem;color:var(--acc);font-weight:800;text-transform:uppercase}
.cw-c i{font-style:normal;font-size:.68rem;color:var(--mut);font-variant-numeric:tabular-nums}
.cw-c:hover:not(:disabled){border-color:var(--acc)}
.cw-c.today{border-color:var(--acc2);box-shadow:0 0 0 1px var(--acc2)}
.cw-c.sel{color:var(--on-acc2)}
.cw-c.sel small, .cw-c.sel i, .cw-c.sel span{color:var(--on-acc2)}
.cw-c:disabled{opacity:.4;cursor:default}
.cw-panel .meal{margin:8px 0}
@media(max-width:420px){
 .cw-cal{gap:4px}
 .cw-c{min-height:68px;padding:6px 0}
 .cw-c b{font-size:1.1rem}
}
/* v10 : calendrier de la semaine plus travaillé + repas bien distincts */
.cw-cal{gap:8px;padding:10px;border-radius:20px;background:var(--card2);border:1px solid var(--line)}
.cw-c{position:relative;min-height:98px;padding:10px 2px 8px;border-radius:16px;gap:3px;background:linear-gradient(180deg,var(--card),var(--card2));box-shadow:0 1px 0 rgba(255,255,255,.04) inset,0 6px 14px -10px rgba(0,0,0,.5)}
.cw-c b{font-size:1.65rem;font-weight:800;line-height:1}
.cw-c small{font-size:.64rem;letter-spacing:.1em}
.cw-c .cw-j{font-size:.6rem;padding:2px 8px;border-radius:999px;background:var(--bg2);border:1px solid var(--line);color:var(--acc);letter-spacing:.06em}
.cw-c.sel .cw-j{background:rgba(255,255,255,.22);border-color:transparent}
.cw-c .cw-dots{display:flex;gap:3px;justify-content:center;min-height:8px;margin-top:2px;font-style:normal}
.cw-c .cw-dots u{width:7px;height:7px;border-radius:50%;border:2px solid var(--sc);background:transparent;box-sizing:border-box;text-decoration:none}
.cw-c .cw-dots u.on{background:var(--sc)}
.cw-c.today::before{content:"";position:absolute;top:6px;right:6px;width:8px;height:8px;border-radius:50%;background:var(--acc);box-shadow:0 0 0 3px rgba(242,122,42,.25)}
.cw-c.full::after{content:"✓";position:absolute;top:5px;left:7px;font-size:.7rem;font-weight:800;color:var(--acc2)}
.cw-c.sel{background:linear-gradient(160deg,var(--acc2),var(--ice));border-color:transparent}
.cw-c.sel b, .cw-c.sel small, .cw-c.sel i{color:var(--on-acc2)}
.cw-c.sel .cw-dots u{border-color:var(--on-acc2)}
.cw-c.sel .cw-dots u.on{background:var(--on-acc2)}
.cw-c.sel.full::after{color:var(--on-acc2)}
.cw-c i{font-weight:700}
.cw-panel .mealw{margin:12px 0}
.cw-panel .mealw .meal{border-left:6px solid var(--sc);border-radius:16px;background:linear-gradient(90deg,color-mix(in srgb,var(--sc) 14%,var(--card2)),var(--card2) 55%)}
.cw-panel .meal>summary{padding:14px 52px 14px 14px;min-height:60px}
.meal-n{display:grid;gap:1px}
.meal-n b{font-size:1.05rem;font-family:var(--font-head);text-transform:uppercase;letter-spacing:.05em;color:var(--ink)}
.meal-h{font-size:.72rem;color:var(--mut);font-weight:600;text-transform:none;letter-spacing:0}
.cw-panel .meal-i{width:44px;height:44px;border-radius:14px;font-size:1.5rem;background:color-mix(in srgb,var(--sc) 30%,transparent);border:1px solid color-mix(in srgb,var(--sc) 55%,transparent)}
.cw-panel .mealw .meal-g{background:var(--card);border:1px solid var(--line);border-radius:999px;padding:2px 10px}
.cw-panel .meal[open]>summary{border-bottom:1px dashed var(--line);margin-bottom:6px}
.cw-panel .mealw .apv-items>li{background:var(--card);border-left:3px solid var(--sc)}
.cw-panel .meal>summary::after{content:'▾';transition:transform .2s}
.cw-panel .meal:not([open])>summary::after{transform:rotate(-90deg)}
.cw-panel .meal[open]>summary::after{transform:none}
@media(max-width:560px){
 .cw-cal{gap:4px;padding:6px}
 .cw-c{min-height:84px}
 .cw-c b{font-size:1.25rem}
 .cw-c .cw-j{font-size:.52rem;padding:1px 5px}
}
@media(forced-colors:active){
 .btn, .card, .rc, .quick, .tile{border:1px solid CanvasText}
}
/* ===== v9 : landing animée, sections par jour, analyse GPX ===== */
.hero.hv{min-height:640px}
.hv-blob{position:absolute;z-index:-1;border-radius:50%;filter:blur(70px);opacity:.32;pointer-events:none;animation:hvblob 16s ease-in-out infinite alternate}
.hv-blob.b1{width:340px;height:340px;left:-90px;top:18%;background:var(--acc)}
.hv-blob.b2{width:280px;height:280px;right:-70px;top:6%;background:var(--ice);animation-delay:-7s}
@keyframes hvblob{to{transform:translate3d(40px,30px,0) scale(1.15)}}
.hv-sun{animation:pulse 6s ease-in-out infinite;transform-box:fill-box;transform-origin:center}
.hv-star{animation:tw 3s ease-in-out infinite}
.hv-trail{stroke-dasharray:2 9;animation:dash 2.4s linear infinite}
.hv-cloud{animation:drift 85s linear infinite}
.hv-l1{transform:translate3d(calc(var(--mx,0)*-5px),calc(var(--sy,0)*10px),0)}
.hv-l2{transform:translate3d(calc(var(--mx,0)*-10px),calc(var(--sy,0)*22px),0)}
.hv-l3{transform:translate3d(calc(var(--mx,0)*-18px),calc(var(--sy,0)*36px),0)}
.hv-hello{display:inline-flex;align-items:center;gap:8px;padding:5px 14px 5px 10px;border-radius:999px;background:rgba(15,29,23,.6);border:1px solid rgba(242,239,228,.22);color:var(--acc2);font-size:.9rem}
.hv-dot{width:9px;height:9px;border-radius:50%;background:var(--acc);box-shadow:0 0 0 0 rgba(242,122,42,.7);animation:hvping 2s infinite}
@keyframes hvping{70%{box-shadow:0 0 0 10px rgba(242,122,42,0)}100%{box-shadow:0 0 0 0 rgba(242,122,42,0)}}
.hero h1 .hv-grad{background:linear-gradient(90deg,#F27A2A,#FFD08A,#F27A2A);background-size:200% 100%;-webkit-background-clip:text;background-clip:text;color:transparent;-webkit-text-fill-color:transparent;animation:hvshine 5s linear infinite}
@keyframes hvshine{to{background-position:-200% 0}}
.hero.hv h1{font-size:clamp(2.6rem,9vw,5rem)}
.hero-in>*{animation:hvin .8s cubic-bezier(.2,.7,.2,1) both}
.hero-in>*:nth-child(2){animation-delay:.08s}
.hero-in>*:nth-child(3){animation-delay:.16s}
.hero-in>*:nth-child(4){animation-delay:.24s}
.hero-in>*:nth-child(5){animation-delay:.32s}
@keyframes hvin{from{opacity:0;transform:translateY(24px)}}
.hv-chips{display:flex;flex-wrap:wrap;gap:10px;margin-top:20px}
.hv-chip{display:grid;grid-template-columns:auto auto;grid-template-rows:auto auto;column-gap:10px;align-items:center;padding:9px 16px 9px 12px;border-radius:18px;background:rgba(15,29,23,.62);border:1px solid rgba(242,239,228,.22);backdrop-filter:blur(8px);animation:hvfloat 5s ease-in-out infinite alternate}
.hv-chip:nth-child(2){animation-delay:-1.2s}
.hv-chip:nth-child(3){animation-delay:-2.4s}
.hv-chip:nth-child(4){animation-delay:-3.6s}
.hv-chip i{grid-row:1/3;font-style:normal;font-size:1.6rem}
.hv-chip b{font-size:1.35rem;line-height:1;color:#F2EFE4;font-variant-numeric:tabular-nums}
.hv-chip small{font-size:.68rem;color:#C3CEC4;text-transform:uppercase;letter-spacing:.07em}
@keyframes hvfloat{to{transform:translateY(-7px)}}
.cdn div{transition:transform .2s}
.cdn div:hover{transform:translateY(-3px) rotate(-1.5deg)}
.cdn div:last-child b{animation:hvtick 1s steps(1) infinite}
@keyframes hvtick{50%{color:var(--acc)}}
.mq{overflow:hidden;margin:26px -14px 4px;padding:11px 0;border-block:1px solid var(--line);background:var(--card);-webkit-mask-image:linear-gradient(90deg,transparent,#000 7%,#000 93%,transparent);mask-image:linear-gradient(90deg,transparent,#000 7%,#000 93%,transparent)}
.mq-in{display:flex;width:max-content;animation:mqs 55s linear infinite}
.mq:hover .mq-in{animation-play-state:paused}
.mq-g{display:flex;align-items:center;gap:18px;padding-right:18px;white-space:nowrap}
.mq-i{font-size:.9rem;color:var(--mut)}
.mq-i b{color:var(--ink)}
.mq-s{color:var(--acc);font-size:.7rem}
@keyframes mqs{to{transform:translateX(-50%)}}
.ringc{transition:transform .25s var(--ease),border-color .2s,box-shadow .25s}
.quick{overflow:hidden}
.quick::after{position:absolute;inset:0;background:linear-gradient(120deg,transparent 30%,rgba(242,122,42,.16) 50%,transparent 70%);transform:translateX(-100%)}
.quick i{display:inline-block}
.quick:hover i{animation:hop .55s}
@keyframes hop{40%{transform:translateY(-9px) rotate(-10deg)}}
.tile{transition:transform .25s var(--ease),border-color .2s,box-shadow .25s}
.tile:hover{transform:translateY(-5px);box-shadow:0 16px 30px -18px rgba(242,122,42,.6)}
.btn{position:relative;overflow:hidden}
.btn:not(.ghost):not(.red)::after{content:"";position:absolute;inset:0;background:linear-gradient(110deg,transparent 35%,rgba(255,255,255,.3) 50%,transparent 65%);transform:translateX(-120%);transition:transform .6s}
.btn:not(.ghost):not(.red):hover::after{transform:translateX(120%)}
/* sections par jour (nutrition + entraînement) */
.cw-nav{display:flex;align-items:center;justify-content:space-between;gap:8px;margin:10px 0}
.cw-nav .tc{flex:1}
.cw-c{transition:transform .15s,border-color .15s,background .15s,box-shadow .2s}
.cw-c:hover:not(:disabled){transform:translateY(-3px)}
.cw-c.sel{transform:translateY(-3px);box-shadow:0 12px 20px -12px var(--acc2)}
.cw-c span.ic{font-size:.95rem;letter-spacing:1px;text-transform:none;color:var(--ink)}
.mealw{--sc:var(--acc2);margin:10px 0}
.mealw .meal{margin:0;border-left:4px solid var(--sc);background:var(--card2);transition:transform .2s,box-shadow .2s}
.mealw .meal:hover{transform:translateY(-1px);box-shadow:0 12px 24px -18px var(--sc)}
.meal-i{display:grid;place-items:center;flex:none;width:36px;height:36px;border-radius:12px;font-size:1.2rem;background:color-mix(in srgb,var(--sc) 24%,transparent)}
.meal-n{flex:1;min-width:0}
.mealw .meal-g{margin-left:0;color:var(--mut);font-size:.75rem}
.mealw .meal[open]>summary{border-bottom:1px dashed var(--line);margin-bottom:8px}
.mealw.dn .meal{border-left-color:var(--acc2)}
.meal-i+.meal-n+.meal-g{white-space:nowrap}
.burst{position:fixed;z-index:500;pointer-events:none;width:0;height:0}
.burst i{position:absolute;left:0;top:0;width:8px;height:8px;border-radius:2px;background:var(--c);animation:bst .85s ease-out forwards}
@keyframes bst{to{transform:translate(var(--x),var(--y)) rotate(var(--r));opacity:0}}
/* analyse GPX */
.gp-h{margin:18px 0 6px}
.gp-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(138px,1fr));gap:10px;margin:12px 0}
.gp-st{position:relative;display:grid;gap:2px;background:var(--card2);border:1px solid var(--line);border-radius:16px;padding:12px 12px 10px 16px;overflow:hidden;animation:gpin .5s both}
.gp-st::before{content:"";position:absolute;left:0;top:0;bottom:0;width:4px;background:var(--c)}
.gp-st i{font-style:normal;font-size:1.3rem}
.gp-st b{font-family:var(--font-head);font-weight:700;font-size:1.45rem;letter-spacing:.02em;font-variant-numeric:tabular-nums}
.gp-st span{font-size:.7rem;color:var(--mut);text-transform:uppercase;letter-spacing:.06em}
@keyframes gpin{from{opacity:0;transform:translateY(10px)}}
.gp-tip{position:static;z-index:3;background:var(--card2);border:1px solid var(--acc);border-radius:12px;padding:9px 12px;font-size:.88rem;margin:8px 0;box-shadow:var(--sh)}
#gp-hit{touch-action:pan-y;cursor:crosshair}
.gp-leg{display:flex;flex-wrap:wrap;gap:6px 12px;font-size:.72rem;color:var(--mut);margin:6px 0 4px}
.gp-leg i{display:inline-block;width:12px;height:12px;border-radius:4px;margin-right:5px;vertical-align:-2px;font-style:normal}
.gp-leg i.gp-bd{width:16px;height:16px;border-radius:50%;background:var(--acc);color:#1A0F07;font-size:.62rem;font-weight:800;text-align:center;line-height:16px;vertical-align:-4px}
.gp-map{position:relative;z-index:1;height:400px;box-shadow:var(--sh);border-radius:14px;overflow:hidden;border:1px solid var(--line);margin:8px 0 6px;background:var(--bg2)}
.gp-hr{display:grid;grid-template-columns:128px 1fr 118px;gap:10px;align-items:center;margin:7px 0;font-size:.82rem}
.gp-hl i{display:inline-block;width:11px;height:11px;border-radius:3px;margin-right:7px}
.gp-hb{height:12px;background:var(--card2);border:1px solid var(--line);border-radius:99px;overflow:hidden}
.gp-hb b{display:block;height:100%;border-radius:99px;animation:grow 1s both}
.gp-hv{text-align:right;color:var(--mut);font-variant-numeric:tabular-nums}
@media(max-width:520px){
 .gp-hr{grid-template-columns:104px 1fr}
 .gp-hv{grid-column:1/-1;text-align:left}
}
.gp-n{display:inline-grid;place-items:center;width:24px;height:24px;border-radius:50%;background:var(--acc);color:var(--on-acc);font-size:.78rem}
/* barre de progression ludique */
/* vue mois */
.cm{border:1px solid var(--line);border-radius:20px;background:var(--card2);padding:10px}
.cm-h,.cm-g{display:contents}
.cm-h i{font-style:normal;text-align:center;font-size:.7rem;font-weight:800;color:var(--mut);padding:2px 0 6px;letter-spacing:.08em}
.cm{display:grid;grid-template-columns:repeat(7,minmax(0,1fr)) 40px;gap:5px}
.cm-d,.cm-e,.cm-w{min-width:0}
.cm-d{position:relative;display:flex;flex-direction:column;align-items:center;justify-content:space-between;gap:1px;min-height:84px;padding:6px 2px 7px;border-radius:14px;border:1px solid var(--line);border-bottom:4px solid var(--sc);background:linear-gradient(180deg,color-mix(in srgb,var(--sc) 16%,var(--card)),var(--card));color:var(--ink);transition:transform .15s,box-shadow .2s,border-color .15s}
.cm-d:hover:not(:disabled){transform:translateY(-3px);box-shadow:0 12px 20px -14px var(--sc)}
.cm-d.off{background:transparent;border-style:dashed;border-bottom-width:1px;opacity:.4;cursor:default}
.cm-n{font-family:var(--font-head);font-size:.95rem;line-height:1;align-self:flex-start;margin-left:6px;color:var(--mut)}
.cm-i{font-size:1.5rem;line-height:1}
.cm-k{font-size:.66rem;font-weight:800;font-variant-numeric:tabular-nums;color:var(--ink);min-height:1em}
.cm-st{font-style:normal;font-size:.62rem;font-weight:800;color:var(--mut)}
.cm-d.today{box-shadow:0 0 0 2px var(--acc)}
.cm-d.today .cm-n{color:var(--acc)}
.cm-d.sel{outline:3px solid var(--ink);outline-offset:1px}
.cm-d.race{background:linear-gradient(160deg,rgba(230,184,74,.35),var(--card))}
.cm-d.full{background:var(--acc2);border-color:var(--acc2);color:var(--on-acc2)}
.cm-d.full .cm-n,.cm-d.full .cm-k,.cm-d.full .cm-st{color:var(--on-acc2)}
.cm-w{display:flex;flex-direction:column;align-items:center;justify-content:center;border-radius:12px;background:var(--card);border:1px solid var(--line);font-variant-numeric:tabular-nums}
.cm-w b{font-family:var(--font-head);font-size:1.05rem;color:var(--acc)}
.cm-w small{font-size:.6rem;color:var(--mut)}
.cm-w.z{color:var(--mut);opacity:.6}
.cm-ms{display:flex;flex-wrap:wrap;justify-content:center;gap:1px 2px;font-size:.95rem;line-height:1.15;max-width:100%}
.cm-ms s{text-decoration:none;opacity:1;position:relative}.cm-ms s::after{content:"";position:absolute;left:15%;right:15%;bottom:-2px;height:2px;border-radius:2px;background:var(--line)}
.cm-ms s.on{opacity:1;filter:none;text-shadow:0 0 0 var(--acc2);position:relative}
.cm-ms s.on::after{content:"";position:absolute;left:15%;right:15%;bottom:-2px;height:2px;border-radius:2px;background:var(--acc2)}
.cm-d.full .cm-ms s.on::after{background:var(--on-acc2)}
@media(max-width:560px){.cm-ms{font-size:.7rem;gap:0 1px}}
@media(max-width:560px){.cm{padding:6px;gap:3px;grid-template-columns:repeat(7,minmax(0,1fr)) 30px}.cm-d{min-height:66px;border-radius:10px;padding:4px 1px 5px}.cm-i{font-size:1.15rem}.cm-k{font-size:.56rem}.cm-n{font-size:.78rem;margin-left:3px}.cm-st{font-size:.54rem}.cm-w b{font-size:.8rem}}
@media(max-width:560px){
 .hero.hv{min-height:600px}
 .hv-chip{padding:7px 12px 7px 9px}
 .hv-chip b{font-size:1.15rem}
}
/* v10b : blocs repas nettement distincts */
.cw-panel .mealw .meal{border:2px solid color-mix(in srgb,var(--sc) 60%,var(--line));border-left-width:8px;overflow:hidden}
.cw-panel .mealw .meal>summary{background:color-mix(in srgb,var(--sc) 22%,var(--card2));margin:0;cursor:pointer}
.cw-panel .mealw .meal>summary:hover{background:color-mix(in srgb,var(--sc) 32%,var(--card2))}
.cw-panel .mealw .meal[open]>summary{margin-bottom:8px}
.cw-panel .mealw .meal>.apv-items{padding:0 12px 12px}
.cw-panel .mealw>.sc-ck{top:17px;right:14px;width:26px;height:26px}
/* v14b : encadré « but de la séance », blocs repliables, barre de la semaine */
.trb-li{list-style:none;margin-left:-4px}
.trb{border:1px solid var(--line);border-radius:12px;background:var(--card);overflow:hidden;margin:2px 0}
.trb>summary{list-style:none;cursor:pointer;display:flex;align-items:center;gap:8px;padding:10px 12px;min-height:44px}
.trb>summary::-webkit-details-marker{display:none}
.trb>summary::after{content:'▾';margin-left:auto;color:var(--mut);transition:transform .2s}
.trb:not([open])>summary::after{transform:rotate(-90deg)}
.trb>summary small{font-size:.72rem;color:var(--mut);font-weight:700}
.trb>ul{margin:0;padding:0 12px 10px 30px;display:grid;gap:4px;border-top:1px dashed var(--line);padding-top:8px}
.wkg{margin:10px 0;padding:14px 16px 12px;border-radius:20px;border:1px solid var(--line);background:linear-gradient(120deg,rgba(242,122,42,.14),var(--card) 60%)}
.wkg-top{display:flex;justify-content:space-between;align-items:center;gap:8px;flex-wrap:wrap}
.wkg-svg{display:block;width:100%;height:auto;margin:8px 0 2px;overflow:visible}
.wkg-done{animation:wkdraw 1.2s var(--ease) both;transition:stroke-dasharray .7s var(--ease)}
@keyframes wkdraw{from{stroke-dasharray:0 100}}
.wkg-ping{transform-box:fill-box;transform-origin:center;animation:pulse 1.6s ease-in-out infinite}
.wkg.full{border-color:var(--acc2);background:linear-gradient(110deg,var(--goodbg) 30%,rgba(230,184,74,.28) 50%,var(--goodbg) 70%);background-size:220% 100%;animation:objshine 2.6s ease-in-out infinite}
@media(prefers-reduced-motion:reduce){.wkg-done,.wkg-ping,.wkg.full{animation:none!important}}
/* v11 : cases de la fiche course harmonisées (même gabarit partout) */
.mp .kv, .mp .gp-stats, .mp .fsum, .mp .sc-info{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:10px;margin:12px 0}
.mp .kv>div, .mp .gp-st, .mp .fsum>div, .mp .sc-info>div{position:relative;display:flex;flex-direction:column;justify-content:center;gap:3px;min-height:76px;padding:12px 14px;background:var(--card2);border:1px solid var(--line);border-left:4px solid var(--c,var(--acc));border-radius:14px;box-shadow:none;text-align:left;overflow:hidden}
.mp .gp-st::before{display:none}
.mp .kv b, .mp .gp-st b, .mp .fsum b{font-family:var(--font-head);font-weight:700;font-size:1.4rem;line-height:1.1;letter-spacing:.02em;color:var(--ink);font-variant-numeric:tabular-nums;display:block}
.mp .kv span, .mp .gp-st span, .mp .fsum span, .mp .sc-info small{font-size:.68rem;color:var(--mut);text-transform:uppercase;letter-spacing:.06em;line-height:1.3}
.mp .gp-st i, .mp .fsum i{font-style:normal;font-size:1.1rem;line-height:1;display:block;margin-bottom:2px}
.mp .card{padding:16px;border-radius:16px;margin-bottom:14px}
.mp .grid>.card{margin-bottom:0;display:flex;flex-direction:column;gap:4px}
.mp .chip{padding:3px 10px}
.mp .note{border-radius:14px}
.mp .tscroll{border:1px solid var(--line);border-radius:14px;padding:2px 8px;background:var(--card)}
@media(max-width:560px){
 .mp .kv, .mp .gp-stats, .mp .fsum{grid-template-columns:repeat(2,1fr)}
 .mp .kv b, .mp .gp-st b{font-size:1.2rem}
}
/* v12 : encadré objectif */
.objb{padding:14px 16px;border-radius:16px;margin:12px 0;overflow:hidden;position:relative}
.obj-h{display:flex;gap:12px;align-items:center}
.obj-ico{font-size:2rem;line-height:1;display:inline-block}
.obj-s{margin-top:8px;font-weight:800}
.obj-s.ok{color:var(--acc2)}
.obj-s.ko{color:var(--bad)}
.obj-sub{display:block;font-weight:700;color:var(--ink);margin-top:2px}
.objb.obj-win{border:2px solid var(--acc2);background:linear-gradient(110deg,var(--goodbg) 30%,rgba(230,184,74,.28) 50%,var(--goodbg) 70%);background-size:220% 100%;animation:objshine 2.6s ease-in-out infinite}
.objb.obj-win .obj-ico{animation:objbounce 1.1s ease-in-out infinite}
@keyframes objshine{0%{background-position:120% 0}100%{background-position:-120% 0}}
@keyframes objbounce{0%,100%{transform:translateY(0) rotate(0)}40%{transform:translateY(-10px) rotate(-12deg)}70%{transform:translateY(-3px) rotate(8deg)}}
/* v13 : bilan de saison */
.sb-hero{position:relative;border-radius:20px;margin-bottom:6px;color:#F2EFE4;background:linear-gradient(135deg,#1D3328,#0F1D17 60%),var(--card);overflow:hidden;border:1px solid var(--line)}
.sb-y{position:relative;display:block;line-height:1;background:linear-gradient(90deg,#F27A2A,#FFD08A,#F27A2A);background-size:200% 100%;-webkit-background-clip:text;background-clip:text;color:transparent;-webkit-text-fill-color:transparent;animation:hvshine 5s linear infinite}
.sb-sub{position:relative;margin-top:6px;font-size:.9rem}
.sb-kv>div{animation:gpin .5s both;transition:transform .2s,box-shadow .2s}
.sb-kv>div:nth-child(2){animation-delay:.07s}
.sb-kv>div:nth-child(3){animation-delay:.14s}
.sb-kv>div:nth-child(4){animation-delay:.21s}
.sb-kv>div:hover{transform:translateY(-3px);box-shadow:0 12px 22px -16px var(--c)}
.sb-d{display:inline-block;margin-top:4px;font-size:.72rem;font-weight:800;padding:1px 8px;border-radius:999px;width:fit-content}
.sb-d.up{background:var(--goodbg);color:var(--acc2)}
.sb-d.dn{background:rgba(255,143,128,.14);color:var(--bad)}
.sb-hls{display:grid;gap:8px}
.sb-hl{display:flex;align-items:center;gap:12px;width:100%;text-align:left;padding:12px 14px;border-radius:14px;background:var(--card2);border:1px solid var(--line);animation:gpin .5s both;transition:transform .2s,border-color .2s}
.sb-hl:hover{transform:translateX(4px);border-color:var(--acc)}
.sb-hi{font-size:1.6rem;width:46px;height:46px;border-radius:14px;display:grid;place-items:center;background:rgba(242,122,42,.16);flex:none}
.sb-hl span:nth-child(2){flex:1;min-width:0;display:grid}
.sb-hl small{font-size:.68rem;color:var(--mut);text-transform:uppercase;letter-spacing:.06em}
.sb-hl b{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.sb-hl em{font-style:normal;font-family:var(--font-head);font-weight:700;font-size:1.2rem;color:var(--acc);white-space:nowrap}
.sb-tl{position:relative;display:grid;gap:6px;padding-left:14px}
.sb-tl::before{content:"";position:absolute;left:4px;top:8px;bottom:8px;width:2px;background:var(--line)}
.sb-ev{position:relative;display:grid;grid-template-columns:62px 1fr auto;gap:10px;align-items:center;width:100%;text-align:left;padding:10px 12px;border-radius:12px;background:var(--card2);border:1px solid var(--line);transition:transform .2s,border-color .2s}
.sb-ev:hover{transform:translateX(3px);border-color:var(--acc)}
.sb-dot{position:absolute;left:-14px;top:50%;width:10px;height:10px;margin-top:-5px;border-radius:50%;background:var(--mut);border:2px solid var(--bg)}
.sb-ev.ok .sb-dot{background:var(--acc2)}
.sb-ev.dn .sb-dot{background:var(--bad)}
.sb-ev.up .sb-dot{background:var(--acc);box-shadow:0 0 0 4px rgba(242,122,42,.25)}
.sb-ed{font-size:.74rem;color:var(--mut);font-weight:700}
.sb-en{display:grid;min-width:0}
.sb-en b{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.sb-en small{color:var(--mut);font-size:.74rem}
.sb-er{font-weight:800;font-variant-numeric:tabular-nums;font-size:.85rem}
@media(max-width:520px){
 .sb-ev{grid-template-columns:1fr auto}
 .sb-ed{grid-column:1/-1}
 .sb-y{font-size:2.6rem}
}
.mp .sb-kv>div{padding:16px 16px;min-height:100px}
.mp .sb-kv span:not(.cu){font-size:.74rem}
@media(max-width:560px){
 .mp .sb-kv b{font-size:1.9rem}
}
.mp .sb-kv b{color:var(--c)}
@media(max-width:560px){
 .mp .sb-kv b{font-size:2.4rem}
}
.mp .sb-kv b{font-weight:900;line-height:1;letter-spacing:0}
@media(max-width:560px){
 .mp .sb-kv b{font-size:2.4rem}
}
.mp .sb-kv b .cu{font-size:inherit;font-weight:inherit;text-transform:none;letter-spacing:inherit;line-height:inherit;color:inherit;font-family:inherit;display:inline}
.mp .sb-kv{grid-template-columns:repeat(2,minmax(0,1fr))}
.mp .sb-kv b{font-size:clamp(1.5rem,6.4vw,2.2rem);white-space:nowrap}
@media(min-width:760px){
 .mp .sb-kv{grid-template-columns:repeat(4,minmax(0,1fr))}
 .mp .sb-kv b{font-size:clamp(1.4rem,3.4vw,1.9rem)}
}
.mp .sb-kv>div>span:not(.sb-d){text-transform:none;letter-spacing:.01em;font-size:.85rem;font-weight:600}
.sb-hero{min-height:190px;display:flex;flex-direction:column;justify-content:flex-end;gap:2px;padding:18px 18px 16px;border-color:rgba(242,239,228,.2)}
.sb-hero::before{display:none}
.sb-art{position:absolute;inset:0;width:100%;height:100%}
.sb-art .sb-trail{stroke-dasharray:3 9;animation:dash 2.4s linear infinite}
.sb-art .sb-sun{animation:pulse 5s ease-in-out infinite;transform-box:fill-box;transform-origin:center}
.sb-hero>:not(.sb-art){position:relative;z-index:1}
.sb-hero::after{display:block;content:"";position:absolute;inset:0;background:linear-gradient(180deg,rgba(8,14,11,.1),rgba(8,14,11,.6));width:auto;height:auto;border-radius:0;animation:none;right:0;top:0}
.sb-badge{align-self:flex-start;padding:4px 12px;border-radius:999px;background:rgba(15,29,23,.7);border:1px solid rgba(242,239,228,.25);font-size:.78rem;font-weight:800;color:#F2EFE4;margin-bottom:6px}
.sb-y{font-size:4.2rem;text-shadow:0 4px 24px rgba(0,0,0,.4)}
.sb-sub{display:inline-block;color:#E3E8DD;font-weight:600}
@media(max-width:520px){
 .sb-y{font-size:3.4rem}
 .sb-hero{min-height:170px}
}
/* ===== v12 : en-tête de course, liens, stats, logos UTMB ===== */
.mp .mx{z-index:5}
.rh{position:relative;isolation:isolate;overflow:hidden;margin:-22px -18px 14px;padding:20px 18px 16px;border-radius:26px 26px 22px 22px;background:linear-gradient(150deg,var(--tc1),var(--tc2));--ink:#F2EFE4;--mut:#D3DDD4;color:#F2EFE4;display:flex;flex-direction:column;gap:10px;min-height:200px}
.rh::after{content:"";position:absolute;inset:0;z-index:-1;background:linear-gradient(180deg,rgba(0,0,0,.04) 0%,rgba(6,13,10,.6) 100%)}
.rh-art{position:absolute;inset:0;width:100%;height:100%;z-index:-2}
.rh-top{display:flex;gap:6px;flex-wrap:wrap;padding-right:48px}
.rh-pill{display:inline-flex;align-items:center;min-height:24px;padding:0 10px;border-radius:999px;font-size:.68rem;font-weight:800;letter-spacing:.07em;text-transform:uppercase;background:rgba(255,255,255,.14);border:1px solid rgba(255,255,255,.24);backdrop-filter:blur(6px)}
.rh-pill.ok{background:#A9C79B;color:#0F1D17;border-color:transparent}
.rh-pill.bad{background:#FF8F80;color:#2A0D09;border-color:transparent}
.rh-pill.warn{background:#F27A2A;color:#1A0F07;border-color:transparent}
.rh-pill.mu{background:rgba(0,0,0,.4)}
.rh-name{font-size:clamp(1.8rem,7vw,2.6rem);line-height:.98;margin:auto 0 0;text-shadow:0 2px 14px rgba(0,0,0,.45)}
.rh-meta{display:flex;flex-wrap:wrap;gap:4px 14px;font-size:.85rem;font-weight:600;color:#E6EEE7;margin:0}
.rh-meta span{display:inline-flex;align-items:center;gap:6px}
.rh-meta svg{width:15px;height:15px;flex:none;opacity:.85}
.rh-foot{display:flex;align-items:flex-end;justify-content:space-between;gap:12px;margin-top:2px}
.rh-big b{display:block;font-size:2.1rem;line-height:1;color:#F6C79B}
.rh-big small{font-size:.75rem;color:#D3DDD4}
.rh-utmb{display:flex;align-items:center;gap:8px}
.rh-utmb .ulogo{width:44px;height:auto}
.rh-utmb small{font-size:.78rem;font-weight:800;color:#F2EFE4}
.lk{gap:6px}
.lkb{display:inline-flex;align-items:center;gap:6px;min-height:34px;padding:0 12px;border-radius:999px;font-size:.76rem;font-weight:700;text-decoration:none;color:#F2EFE4;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.22);backdrop-filter:blur(6px);transition:background .2s}
.lkb:hover{background:rgba(255,255,255,.24)}
.lkb svg{width:14px;height:14px;flex:none}
.rs{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--line);border:1px solid var(--line);border-radius:18px;overflow:hidden;margin:0 0 14px}
.rs>div{background:var(--card);padding:12px 10px;display:flex;flex-direction:column;gap:3px;min-width:0}
.rs b{font-family:var(--font-head);font-stretch:condensed;font-size:1.45rem;line-height:1.05;font-weight:800;color:var(--ink)}
.rs b small{font-size:.7rem;color:var(--mut);font-weight:700;margin-left:3px}
.rs span{display:flex;align-items:center;gap:5px;font-size:.68rem;text-transform:uppercase;letter-spacing:.06em;color:var(--mut);font-weight:700}
.rs i{font-style:normal;font-size:.85rem}
.ucats{display:flex;gap:10px;flex-wrap:wrap;margin-top:2px}
.ucat{width:68px;height:78px;padding:0;border-radius:14px;background:transparent;border:2px solid transparent;opacity:.55;transition:opacity .2s,transform .2s,border-color .2s;display:grid;place-items:center}
.ucat svg{width:52px;height:auto}
.ucat:hover{opacity:.9}
.ucat.on{opacity:1;border-color:var(--acc2);background:var(--card2);transform:translateY(-2px)}
.ulogo{display:block}
.chip .ulogo{width:auto;height:22px;display:inline-block;vertical-align:middle}
td .ulogo{width:34px;height:auto}
/* ===== v13 : refonte visuelle « Sommet » ===== */
:root{--topo-img:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 420 420'%3E%3Cg fill='none' stroke='%23A8B8AB' stroke-opacity='.10' stroke-width='1.3'%3E%3Cpath d='M200 40C290 30 360 90 365 170S330 330 230 350 60 320 45 230 110 50 200 40Z'/%3E%3Cpath d='M200 80C265 72 322 118 326 178S300 296 224 312 92 290 80 226 134 88 200 80Z'/%3E%3Cpath d='M200 120C245 114 284 146 288 188S268 262 218 274 124 258 116 214 156 124 200 120Z'/%3E%3Cpath d='M200 160C226 156 250 174 252 198S238 236 210 242 160 232 156 206 176 162 200 160Z'/%3E%3Cpath d='M0 400C60 360 120 390 180 380S330 396 420 360'/%3E%3Cpath d='M0 20C80 50 150 10 240 28S360 10 420 40'/%3E%3C/g%3E%3C/svg%3E");--glow:rgba(242,122,42,.32);}
@media(prefers-color-scheme:light){
 :root:not([data-theme="dark"]){--topo-img:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 420 420'%3E%3Cg fill='none' stroke='%231E2823' stroke-opacity='.09' stroke-width='1.3'%3E%3Cpath d='M200 40C290 30 360 90 365 170S330 330 230 350 60 320 45 230 110 50 200 40Z'/%3E%3Cpath d='M200 80C265 72 322 118 326 178S300 296 224 312 92 290 80 226 134 88 200 80Z'/%3E%3Cpath d='M200 120C245 114 284 146 288 188S268 262 218 274 124 258 116 214 156 124 200 120Z'/%3E%3Cpath d='M200 160C226 156 250 174 252 198S238 236 210 242 160 232 156 206 176 162 200 160Z'/%3E%3Cpath d='M0 400C60 360 120 390 180 380S330 396 420 360'/%3E%3Cpath d='M0 20C80 50 150 10 240 28S360 10 420 40'/%3E%3C/g%3E%3C/svg%3E");--glow:rgba(166,63,8,.28)}
}
:root[data-theme="light"]{--topo-img:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 420 420'%3E%3Cg fill='none' stroke='%231E2823' stroke-opacity='.09' stroke-width='1.3'%3E%3Cpath d='M200 40C290 30 360 90 365 170S330 330 230 350 60 320 45 230 110 50 200 40Z'/%3E%3Cpath d='M200 80C265 72 322 118 326 178S300 296 224 312 92 290 80 226 134 88 200 80Z'/%3E%3Cpath d='M200 120C245 114 284 146 288 188S268 262 218 274 124 258 116 214 156 124 200 120Z'/%3E%3Cpath d='M200 160C226 156 250 174 252 198S238 236 210 242 160 232 156 206 176 162 200 160Z'/%3E%3Cpath d='M0 400C60 360 120 390 180 380S330 396 420 360'/%3E%3Cpath d='M0 20C80 50 150 10 240 28S360 10 420 40'/%3E%3C/g%3E%3C/svg%3E");--glow:rgba(166,63,8,.28)}
*{scrollbar-width:thin;scrollbar-color:var(--line) transparent}
.skip{position:absolute;left:-999px;top:8px;z-index:999;background:var(--acc);color:var(--on-acc);padding:10px 16px;border-radius:12px;font-weight:800}
.skip:focus{left:12px}
body::before{content:"";position:fixed;inset:0;z-index:-1;pointer-events:none;background:var(--topo-img) 0 0/520px 520px;-webkit-mask-image:linear-gradient(180deg,#000 0%,rgba(0,0,0,.35) 100%);mask-image:linear-gradient(180deg,#000 0%,rgba(0,0,0,.35) 100%)}
.cdn b, .kv b, .rs b, .ring text, .dbox b{font-variant-numeric:tabular-nums}
/* navigation */
.brand b{letter-spacing:.14em;font-size:1.35rem}
.logo{border-radius:12px;box-shadow:0 8px 20px -8px var(--glow)}
.nav button{border-radius:14px;transition:background .2s,color .2s,transform .15s}
.nav button.on{background:linear-gradient(90deg,rgba(242,122,42,.20),transparent 85%);color:var(--ink);box-shadow:inset 3px 0 0 var(--acc)}
.nav button:active{transform:scale(.97)}
@media(max-width:899px){
 .side{width:auto;inset:auto 10px calc(10px + env(safe-area-inset-bottom)) 10px;border:1px solid var(--line);border-radius:24px;padding:6px;box-shadow:0 18px 40px -12px rgba(0,0,0,.65)}
 .nav button{border-radius:18px}
 .nav button.on{background:var(--acc);color:var(--on-acc);box-shadow:0 8px 18px -8px var(--glow)}
 main{padding-bottom:108px}
 .savepill{bottom:96px}
}
@media(min-width:900px){
 .wrap{max-width:1180px;padding:28px 28px}
}
/* accueil */
.hero{border-radius:0 0 36px 36px;min-height:460px}
.hero h1{text-transform:uppercase;letter-spacing:-.01em;font-size:clamp(2.6rem,9vw,5rem);text-shadow:0 4px 30px rgba(0,0,0,.4)}
.hero::before{content:"";position:absolute;left:0;right:0;bottom:0;height:4px;background:linear-gradient(90deg,var(--acc),var(--acc2) 55%,transparent)}
.cdn div{border-radius:12px;border-color:rgba(242,122,42,.5);min-width:66px}
.cdn b{color:#F6B07A;font-size:1.9rem}
.ringc{position:relative;overflow:hidden;}
/* titres */
.sec{margin:34px 0 14px}
.sec h2, .card>h2.cond{display:flex;align-items:center;gap:10px;letter-spacing:.03em}
.sec h2::before, .card>h2.cond::before{content:"";flex:none;width:18px;height:4px;border-radius:3px;background:var(--acc)}
/* cartes */
.card{border-radius:20px;background:linear-gradient(180deg,var(--card),var(--bg2));padding:20px}
.card:hover{border-color:rgba(242,122,42,.35)}
details.hist{border-radius:20px}
.today-card{border-left:4px solid var(--acc);background:linear-gradient(120deg,rgba(242,122,42,.12),var(--card) 45%)}
.aicard{border-left:4px solid var(--acc2)}
.kv div{border-radius:14px;border:1px solid var(--line);background:var(--card2)}
.kv b{font-family:var(--font-head);font-stretch:condensed}
.note{border-radius:14px}
.empty{border-radius:20px;background:var(--topo-img) center/320px,transparent;border-color:var(--line)}
/* boutons */
.btn{border-radius:14px;letter-spacing:.01em;box-shadow:0 10px 22px -14px var(--glow);transition:transform .15s,filter .15s,background .2s}
.btn:hover{filter:brightness(1.08);transform:translateY(-1px)}
.btn:active{transform:translateY(1px);filter:none}
.btn.ghost{box-shadow:none}
.btn.ghost:hover{border-color:var(--acc);filter:none}
.quick{position:relative;border-radius:18px;background:linear-gradient(135deg,rgba(242,122,42,.14),var(--card) 62%);transition:transform .2s,border-color .2s}
.quick::after{content:"→";margin-left:auto;font-weight:800;color:var(--acc);transition:transform .2s}
.quick:hover{border-color:var(--acc)}
.quick:hover::after{transform:translateX(4px)}
/* courses */
.rc{border-radius:18px;background:linear-gradient(90deg,var(--card),var(--bg2));transition:border-color .2s,transform .2s}
.rc:hover{transform:translateX(3px)}
.dbox{position:relative;overflow:hidden;border:1px solid var(--line);padding-top:4px}
.dbox::before{content:"";position:absolute;left:0;right:0;top:0;height:5px;background:var(--acc)}
.rc-name{font-size:1.02rem;letter-spacing:.01em}
.tag{letter-spacing:.06em}
.tag.up{box-shadow:0 6px 14px -8px var(--acc2)}
.chip{font-weight:600;font-variant-numeric:tabular-nums}
.tile{border-radius:24px;box-shadow:var(--sh)}
.tile-top{height:116px}
.tile-b b{font-size:1.05rem}
/* tableaux & formulaires */
table tbody tr:nth-child(even) td{background:rgba(127,127,127,.06)}
th{border-bottom:2px solid var(--line)}
.f input, .f select, .f textarea, .sel select{border-radius:12px;transition:border-color .2s,box-shadow .2s}
.f input:focus, .f select:focus, .f textarea:focus{outline:none;border-color:var(--acc);box-shadow:0 0 0 3px var(--glow)}
.f{letter-spacing:.01em}
.bar{height:12px}
/* séances */
.sc{border-radius:16px;transition:border-color .2s}
.sc.race{box-shadow:0 0 0 1px var(--acc) inset}
.apv-c, .apv-wd{border-radius:12px}
/* fenêtres */
.mod{background:rgba(5,10,8,.74);backdrop-filter:blur(6px)}
.mp{border-radius:28px 28px 0 0;box-shadow:0 -20px 60px -20px rgba(0,0,0,.7)}
@media(min-width:760px){
 .mp{border-radius:28px}
}
.mx{transition:transform .2s,background .2s}
.mx:hover{transform:rotate(90deg);background:var(--acc);color:var(--on-acc)}
.toast{border-radius:14px}
@media(prefers-reduced-motion:reduce){
 .rc:hover, .btn:hover, .mx:hover, .quick:hover::after{transform:none}
}
.cw-c.full{background:var(--acc2);border-color:var(--acc2);color:var(--on-acc2);box-shadow:0 10px 18px -12px var(--acc2)}
.cw-c.full b,.cw-c.full small,.cw-c.full i,.cw-c.full .ic,.cw-c.full::after{color:var(--on-acc2)}
.cw-c.full .cw-j{background:rgba(255,255,255,.25);border-color:transparent;color:var(--on-acc2)}
.cw-c.full .cw-dots u{border-color:var(--on-acc2)}.cw-c.full .cw-dots u.on{background:var(--on-acc2)}
.cw-c.full.sel{outline:3px solid var(--ink);outline-offset:2px}
.apv-wd.full,.apv-c.full{background:var(--acc2);border-color:var(--acc2);color:var(--on-acc2)}
.apv-wd.full *,.apv-c.full *{color:var(--on-acc2)}
.ring{overflow:visible}
.ring .t{stroke-width:16}
.ring .f{stroke-width:16}
.ring .seg{stroke-width:16;cursor:pointer;transition:stroke-width .18s var(--ease),opacity .18s,filter .18s;animation:segin .7s var(--ease) backwards}
@keyframes segin{from{stroke-width:0;opacity:0}}
.ring:has(.seg:hover) .seg:not(:hover){opacity:.4!important}
.ring .seg:hover{stroke-width:22;opacity:1!important;filter:brightness(1.12) drop-shadow(0 3px 6px rgba(0,0,0,.5))}
.ring .seg.on{stroke-width:21;opacity:1!important;filter:drop-shadow(0 2px 5px rgba(0,0,0,.45))}
.segtip{position:fixed;z-index:400;pointer-events:none;display:grid;gap:2px;padding:9px 13px;border-radius:14px;background:var(--card2);color:var(--ink);border:1px solid var(--line);border-left:6px solid var(--tc,var(--acc));box-shadow:0 14px 30px -10px rgba(0,0,0,.6);max-width:270px;font-size:.85rem;line-height:1.3}
.segtip b{font-size:.95rem}.segtip strong{font-family:var(--font-head);font-stretch:condensed;font-size:1.25rem;color:var(--tc,var(--acc))}
.ringpanel{border:1px solid var(--line);border-left:5px solid var(--rc,var(--acc));border-radius:20px;background:linear-gradient(180deg,var(--card),var(--bg2));padding:16px;margin-top:12px;animation:up .25s ease}
/* ===== v14 : cercles de l'accueil — anneau fin + légende ===== */
:root{--k0:#A593CC;--k1:#4C9A78;--k2:#D98E73;--k3:#D2AE5E}
@media(prefers-color-scheme:light){:root:not([data-theme="dark"]){--k0:#8A74B0;--k1:#346A52;--k2:#C77B63;--k3:#BE9A50}}
:root[data-theme="light"]{--k0:#8A74B0;--k1:#346A52;--k2:#C77B63;--k3:#BE9A50}
:root[data-theme="dark"]{--k0:#A593CC;--k1:#4C9A78;--k2:#D98E73;--k3:#D2AE5E}
.rings{grid-template-columns:repeat(6,1fr);gap:14px}
.ringc{grid-column:span 2;display:flex;flex-direction:column;align-items:stretch;padding:24px 16px 18px;text-align:left;border-radius:22px;background:var(--card)}
.ringc:nth-child(n+4){grid-column:span 3}
@media(max-width:899px){.rings{grid-template-columns:repeat(2,1fr)}.ringc,.ringc:nth-child(n+4){grid-column:auto}.ringc:last-child:nth-child(odd){grid-column:1/-1}}
@media(max-width:560px){.rings{grid-template-columns:1fr}.ringc:last-child:nth-child(odd){grid-column:auto}}
.ringc::before{display:none}
.ringc:hover{border-color:var(--acc);box-shadow:var(--sh)}
.rg-wrap{position:relative;width:100%;max-width:196px;margin:0 auto 20px}
.rg-wrap .ring{width:100%;max-width:none;margin:0}
.rg-open{position:absolute;left:21%;top:21%;width:58%;height:58%;border-radius:50%;background:transparent}
.rg-open:hover{background:rgba(127,127,127,.08)}
.ringc .ring .t{stroke:var(--line);stroke-width:18}
.ringc .ring .seg{stroke-width:18}
.ringc .ring .seg:hover{stroke-width:22.5}
.ringc .ring .seg.on,.ringc .ring .seg:focus-visible{stroke-width:22;outline:none;filter:brightness(1.1) drop-shadow(0 2px 4px rgba(0,0,0,.35))}
.ring text{pointer-events:none}
.ring .rg-l{font-family:var(--font-body);font-size:6.6px;font-weight:600;fill:var(--mut)}
.ring .rg-v{font-family:var(--font-body);font-weight:800;fill:var(--ink);letter-spacing:-.01em}
.ring .rg-s{font-family:var(--font-body);font-size:6.2px;font-weight:600;fill:var(--mut)}
.rg-leg{display:grid;gap:2px}
.lg-row{display:flex;align-items:center;gap:8px;min-width:0;width:100%;padding:6px;border-radius:10px;text-align:left;font-size:.88rem;background:transparent}
.lg-row:hover,.lg-row.on{background:var(--card2)}
.lg-d{flex:none;width:14px;height:14px;border-radius:5px}
.lg-n{flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;color:var(--ink);font-weight:600}
.lg-p{flex:none;min-width:3.2em;text-align:right;color:var(--mut);font-size:.84rem;font-variant-numeric:tabular-nums}
.lg-v{flex:none;min-width:3.6em;text-align:right;font-weight:800;color:var(--ink);font-variant-numeric:tabular-nums}
.rg-note{margin-top:8px;text-align:center;font-size:.72rem;color:var(--mut)}
.rings-note{margin-top:20px;padding-top:14px;border-top:1px solid var(--line);font-size:.9rem}
</style>
</head>
<body><a class="skip" href="#main">Aller au contenu</a>
<div class="topo-bg" id="topo" aria-hidden="true"></div>
<div class="app">
  <aside class="side" aria-label="Navigation">
    <div class="brand"><div class="logo" aria-hidden="true"><svg width="22" height="22" viewBox="0 0 24 24"><path d="M2 20 9 8l4 6 3-4 6 10z" fill="#10140f"/></svg></div><b class="cond">Vertex</b></div>
    <nav class="nav" id="nav"></nav>
  </aside>
  <main id="main" tabindex="-1"></main>
</div>
<div id="modal" class="mod hide" role="dialog" aria-modal="true"><div class="mp"><button class="mx" data-a="close" aria-label="Fermer">✕</button><div id="mbody"></div></div></div>
<div id="sv" class="savepill" aria-live="polite"></div>
<div id="segtip" class="segtip hide" role="tooltip"></div>
<div id="toast" class="toast hide" role="status"></div>
<input type="file" id="fGpx" accept=".gpx,application/gpx+xml,text/xml" hidden>
<input type="file" id="fBak" accept=".json,application/json" hidden>
<script>

'use strict';
/* ============================ DONNÉES ============================ */
const SEED={
 profile:{name:'Hugo',utmb:600,age:36,height:179,weight:70,weightTaper:68,vo2:57,hrRest:39,hrMax:177,shoes:'Hoka Speedgoat 7',watch:'Garmin Fenix 6 Pro',habit:'2 à 3 séances de course et 1 à 2 séances de musculation par semaine',terrain:'Plutôt plat, peu de dénivelé positif',gym:'Basic-Fit',sessionsRun:3,sessionsGym:2,weeklyKm:40,dplusAvail:300,treadmill:'oui',feel:5,nutriWater:500,nutriIso:500,nutriCarbs:75},
 races:[
{"id": "route-semi", "name": "Semi-marathon (route)", "date": "2026-05-17", "km": 21.14, "dplus": 65, "dminus": null, "goal": "", "status": "Finisher", "result": "1h35'40", "rank": "", "notes": "", "src": "seed", "kind": "route", "check": ""},
{"id": "route-15k", "name": "15 km (route)", "date": "2025-12-09", "km": 15, "dplus": 42, "dminus": null, "goal": "", "status": "Finisher", "result": "1h05'00", "rank": "", "notes": "", "src": "seed", "kind": "route", "check": ""},
{"id": "route-10k", "name": "10 km (route)", "date": "2025-12-09", "km": 10, "dplus": 21, "dminus": null, "goal": "", "status": "Finisher", "result": "42'42", "rank": "", "notes": "", "src": "seed", "kind": "route", "check": ""},
{"id": "route-5k", "name": "5 km (route)", "date": "2025-12-09", "km": 5, "dplus": 11, "dminus": null, "goal": "", "status": "Finisher", "result": "20'36", "rank": "", "notes": "", "src": "seed", "kind": "route", "check": ""},
{"id": "t24-mb", "name": "Marathon du Mont-Blanc — Duo étoilé", "date": "2024-06-29", "km": 21, "dplus": 1450, "dminus": 1450, "goal": "", "status": "Finisher", "result": "3h38'48", "rank": "129/556", "notes": "", "src": "", "kind": "trail", "check": "", "startTime": "20:00", "cond": "Nocturne", "condNote": "", "phys": "Bon", "pers": "", "srcNote": ""},
{"id": "t24-roses", "name": "Les Roses de l’Étang — Roller Coaster", "date": "2024-10-06", "km": 21.15, "dplus": 381, "dminus": 381, "goal": "", "status": "Finisher", "result": "1h55'51", "rank": "27/123", "notes": "", "src": "https://www.strava.com/activities/12588143359", "kind": "trail", "check": "", "startTime": "09:00", "cond": "Aucune particulière", "condNote": "", "phys": "Bon", "pers": "Chrono", "srcNote": ""},
{"id": "t24-sangliers", "name": "Trail des Sangliers du Grieffe", "date": "2024-11-17", "km": 18.58, "dplus": 364, "dminus": null, "goal": "", "status": "Finisher", "result": "1h46'26", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t24-saintelyon", "name": "SaintéLyon — relais à 4", "date": "2024-11-30", "km": 27.4, "dplus": 842, "dminus": null, "goal": "", "status": "Finisher", "result": "2h51'42", "rank": "", "notes": "Relais : distance et chrono de ton relais.", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-urban", "name": "Urban Trail de Montpellier", "date": "2025-01-11", "km": 12.21, "dplus": 144, "dminus": null, "goal": "", "status": "Finisher", "result": "1h02'11", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-linceuil", "name": "Trail de la Drôme — Tour du Linceuil", "date": "2025-04-13", "km": 21.18, "dplus": 1277, "dminus": null, "goal": "", "status": "Finisher", "result": "2h38'20", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-pistole", "name": "Trail de Saint-Jean-de-Védas — Ultra Pistole", "date": "2025-04-27", "km": 32.18, "dplus": 901, "dminus": null, "goal": "", "status": "Finisher", "result": "3h56'53", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-chevreuil", "name": "Trail du Sou de Tournon — La Chevreuil", "date": "2025-05-04", "km": 11.14, "dplus": 381, "dminus": null, "goal": "", "status": "Finisher", "result": "1h03'21", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-hortus", "name": "FestaTrail — Marathon de l’Hortus", "date": "2025-05-18", "km": 45.01, "dplus": 1465, "dminus": null, "goal": "", "status": "Finisher", "result": "6h10'44", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-falaises", "name": "Trail des Falaises — Donzère", "date": "2025-07-13", "km": 19.58, "dplus": 483, "dminus": null, "goal": "", "status": "Finisher", "result": "1h42'20", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-dolmens", "name": "Trail des Dolmens-Ardèche — Drailles du Dolmen", "date": "2025-09-14", "km": 24, "dplus": 520, "dminus": null, "goal": "", "status": "Finisher", "result": "2h26'29", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-nice", "name": "Nice Côte d’Azur by UTMB — Èze-Nice 50K", "date": "2025-09-27", "km": 54.56, "dplus": 2533, "dminus": null, "goal": "", "status": "Finisher", "result": "7h46'44", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-tiny", "name": "Les Roses de l’Étang — Tiny Coaster", "date": "2025-10-05", "km": 12.05, "dplus": 174, "dminus": null, "goal": "", "status": "Finisher", "result": "56'26", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-20collines", "name": "Le 20 des collines", "date": "2025-10-19", "km": 20.57, "dplus": 362, "dminus": null, "goal": "", "status": "Finisher", "result": "1h39'58", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-venivici", "name": "La Veni Vici", "date": "2025-11-08", "km": 27, "dplus": 683, "dminus": null, "goal": "", "status": "Finisher", "result": "2h26'52", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-saintexpress", "name": "SaintéLyon — SaintExpress", "date": "2025-11-29", "km": 46, "dplus": 1031, "dminus": null, "goal": "", "status": "Finisher", "result": "4h49'56", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t26-boeuf", "name": "Trail du Bœuf à Mèze", "date": "2026-02-08", "km": 15, "dplus": 215, "dminus": null, "goal": "", "status": "Finisher", "result": "1h05'27", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "ventoux", "name": "Trail du Ventoux — L’Origine", "date": "2026-03-28", "km": 48.14, "dplus": 2640, "dminus": null, "goal": "", "status": "Finisher", "result": "6h34'59", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t26-pistole", "name": "Trail de Saint-Jean-de-Védas — Ultra Pistole", "date": "2026-04-26", "km": 32, "dplus": 979, "dminus": null, "goal": "", "status": "Finisher", "result": "3h12'45", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "andorra", "name": "Trail100 Andorra — 80K", "date": "2026-06-12", "km": 79, "dplus": 4020, "dminus": null, "goal": "", "status": "Finisher", "result": "12h08'29", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "t25-falaises-b", "name": "Trail des Falaises — Donzère", "date": "2026-07-12", "km": 19.39, "dplus": 474, "dminus": null, "goal": "", "status": "Finisher", "result": "1h42'46", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "oisans", "name": "Oisans Trail Tour", "date": "2026-07-18", "km": 39.2, "dplus": 2055, "dminus": null, "goal": "", "status": "Finisher", "result": "4h37'02", "rank": "", "notes": "", "src": "seed", "kind": "trail", "check": ""},
{"id": "wild72", "name": "Wild 72 Kandersteg", "date": "2026-09-11", "km": 72, "dplus": 4600, "dminus": null, "goal": "11h", "status": "À confirmer", "result": "", "rank": "", "notes": "Kandersteg → Crans-Montana. Temps max 17 h 30.", "src": "seed", "kind": "trail", "check": ""},
{"id": "roses", "name": "Les Roses de l'Étang", "date": "2026-10-04", "km": 21.3, "dplus": 420, "dminus": null, "goal": "1h38", "status": "À confirmer", "result": "", "rank": "", "notes": "Pujaut (Gard).", "src": "seed", "kind": "trail", "check": ""},
{"id": "collines", "name": "Le 20 des Collines", "date": "2026-10-18", "km": 20, "dplus": 450, "dminus": null, "goal": "", "status": "À confirmer", "result": "", "rank": "", "notes": "Rural trail, Bourdic (Gard).", "src": "seed", "kind": "trail", "check": ""},
{"id": "rmvi0fk9zlto", "src": "", "name": "Les Roses de l'Etang", "date": "2023-10-08", "km": 14.8, "dplus": 370, "dminus": 370, "goal": "1h24", "status": "Finisher", "result": "1h24", "rank": "72ème / 246", "notes": "", "kind": "trail", "check": "", "startTime": "09:00", "cond": "Aucune particulière", "condNote": "", "phys": "Reprise", "pers": "Aucun", "srcNote": ""}
 ],
 v:2,plans:{},done:{},feedback:{}
};
function getTheme(){try{return localStorage.getItem('vertex_theme')||'auto'}catch(e){return 'auto'}}
function applyTheme(t){const h=document.documentElement;if(t==='light'||t==='dark')h.setAttribute('data-theme',t);else h.removeAttribute('data-theme');
  let dark=t==='dark';if(t==='auto')dark=!(window.matchMedia&&matchMedia('(prefers-color-scheme: light)').matches);
  const m=document.querySelector('meta[name=theme-color]');if(m)m.setAttribute('content',dark?'#0F1D17':'#F3F0E6')}
function cycleTheme(){const o=['auto','light','dark'],n=o[(o.indexOf(getTheme())+1)%3];try{localStorage.setItem('vertex_theme',n)}catch(e){}applyTheme(n);render();toast({auto:'Thème : automatique (suit ton appareil)',light:'Thème clair',dark:'Thème sombre'}[n])}
applyTheme(getTheme());
/* ============================ ÉTAT & SERVEUR ============================ */
let D=normalizeDoc(null),BOOTED=false;
let saveT=null,dirty=false;
function normalizeDoc(s){
  if(!s||typeof s!=='object')return JSON.parse(JSON.stringify(SEED));
  return{v:2,profile:Object.assign({},SEED.profile,s.profile||{}),races:(Array.isArray(s.races)?s.races:[]).map(r=>Object.assign({kind:'trail'},r)),
    plans:s.plans||{},feedback:s.feedback||{},done:s.done||{},ai:s.ai&&typeof s.ai==='object'?s.ai:{prompt:{},resp:{}}}}
const docOut=()=>({v:2,profile:D.profile,races:D.races,plans:D.plans||{},feedback:D.feedback,done:D.done,ai:D.ai||{prompt:{},resp:{}}});
function legacyDoc(){try{const s=JSON.parse(localStorage.getItem('vertex_v1'));return s&&Array.isArray(s.races)?s:null}catch(e){return null}}
/* Stockage : un seul document JSON dans localStorage (clé et format inchangés : tes données existantes restent valides). */
const KEY='vertex_v2';
const LS={get(k){try{return localStorage.getItem(k)}catch(e){return null}},set(k,v){try{localStorage.setItem(k,v)}catch(e){}}};
function loadDoc(){try{const o=JSON.parse(localStorage.getItem(KEY));return o&&o.doc?o.doc:null}catch(e){return null}}
function storeDoc(){let v=0;try{const c=JSON.parse(localStorage.getItem(KEY));v=(c&&+c.version)||0}catch(e){}localStorage.setItem(KEY,JSON.stringify({version:v+1,doc:docOut()}))}
const SAVE_MSG={idle:'',pending:'Modifications…',saved:'Enregistré ✓',error:'Non enregistré'};
function setSave(st,msg){const el=document.getElementById('sv');if(!el)return;el.dataset.s=st;el.textContent=msg||SAVE_MSG[st]||''}
function save(){if(!BOOTED)return;dirty=true;setSave('pending');clearTimeout(saveT);saveT=setTimeout(flush,400)}
function flush(){
  clearTimeout(saveT);if(!dirty||!BOOTED)return;
  try{storeDoc();dirty=false;setSave('saved');abSchedule()}
  catch(e){setSave('error','Non enregistré — stockage plein ou désactivé');toast('Sauvegarde impossible : le stockage du navigateur est plein ou désactivé. Exporte une sauvegarde (Profil → Données).',1)}
}
// Écriture aussi à la fermeture / mise en arrière-plan : une modification récente n'est jamais perdue.
window.addEventListener('pagehide',flush);
document.addEventListener('visibilitychange',()=>{if(document.visibilityState==='hidden')flush()});
function boot(){
  paintTopo();
  const stored=loadDoc();
  D=normalizeDoc(stored||legacyDoc());BOOTED=true;migrateData();
  if(!stored)save();
  if(!LS.get('vertex_first'))LS.set('vertex_first',today());
  abInit();
  try{if(navigator.storage&&navigator.storage.persist)navigator.storage.persist()}catch(e){} // demande au navigateur de ne pas purger ces données
  render();
}
const S={tab:'home',sel:null,filt:{from:'',to:'',y:'all'}};

/* ============================ OUTILS ============================ */
const $=(s,r=document)=>r.querySelector(s),$$=(s,r=document)=>[...r.querySelectorAll(s)];
const esc=s=>String(s==null?'':s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const pad=n=>String(n).padStart(2,'0');
const iso=d=>`${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}`;
const pISO=s=>{const [y,m,d]=s.split('-').map(Number);return new Date(y,m-1,d)};
const today=()=>iso(new Date());
const addD=(s,n)=>{const d=pISO(s);d.setDate(d.getDate()+n);return iso(d)};
const dBetween=(a,b)=>Math.round((pISO(b)-pISO(a))/864e5);
const dow=s=>(pISO(s).getDay()+6)%7;
const MONL=['janvier','février','mars','avril','mai','juin','juillet','août','septembre','octobre','novembre','décembre'],DAYS=['Lundi','Mardi','Mercredi','Jeudi','Vendredi','Samedi','Dimanche'],MON=['janv.','févr.','mars','avr.','mai','juin','juil.','août','sept.','oct.','nov.','déc.'];
const longD=s=>{const d=pISO(s);return `${DAYS[dow(s)]} ${d.getDate()} ${MONL[d.getMonth()]} ${d.getFullYear()}`};
const shortD=s=>{const d=pISO(s);return `${d.getDate()} ${MON[d.getMonth()]} ${String(d.getFullYear()).slice(2)}`};
const monday=s=>addD(s,-dow(s));
const fn=(n,d=1)=>(Math.round(n*10**d)/10**d).toLocaleString('fr-FR');
function parseT(v){ // texte → minutes (0 si illisible)
  if(v==null)return 0;
  const t=String(v).toLowerCase().replace(/[′’`]/g,"'").replace(/[″"]/g,'').replace(/\s+/g,'').replace(',','.');if(!t)return 0;
  let m=t.match(/^(\d+):(\d{1,2}):(\d{1,2}(?:\.\d+)?)$/);if(m)return +m[1]*60+ +m[2]+ +m[3]/60;          // 1:05:00
  m=t.match(/^(\d+)h(\d{1,2})?(?:['m:](\d{1,2}(?:\.\d+)?))?$/);if(m)return +m[1]*60+(m[2]?+m[2]:0)+(m[3]?+m[3]/60:0); // 6h34'59, 1h38, 1h35'40
  m=t.match(/^(\d+)['m:](\d{1,2}(?:\.\d+)?)$/);if(m)return +m[1]+ +m[2]/60;                              // 42'42, 20:36 (min'sec)
  m=t.match(/^(\d+(?:\.\d+)?)'?$/);if(m)return parseFloat(m[1]);                                           // 42 (minutes)
  return 0}
const fmtT=m=>{if(!m||!isFinite(m))return '—';let h=Math.floor(m/60),mm=Math.round(m%60);if(mm===60){h++;mm=0}return h?`${h} h ${pad(mm)}`:`${mm} min`};
const pace=m=>{if(!m||!isFinite(m))return '—';let a=Math.floor(m),b=Math.round((m-a)*60);if(b===60){a++;b=0}return `${a}'${pad(b)}"`};
function toast(m,err){const t=$('#toast');t.textContent=m;t.className='toast'+(err?' err':'');clearTimeout(toast.t);toast.t=setTimeout(()=>t.classList.add('hide'),4500)}
const uid=()=>'r'+Date.now().toString(36)+Math.random().toString(36).slice(2,5);

/* ============================ MODÈLE DE PERFORMANCE ============================ */
const vo2=v=>-4.6+0.182258*v+0.000104*v*v;
const pct=t=>0.8+0.1894393*Math.exp(-0.012778*t)+0.2989558*Math.exp(-0.1932605*t);
const vdotOf=(m,t)=>vo2(m/t)/pct(t);
function timeFor(m,vd){let lo=3,hi=900;for(let i=0;i<70;i++){const t=(lo+hi)/2;vdotOf(m,t)>vd?lo=t:hi=t}return (lo+hi)/2}
const isTrail=r=>r.kind!=='route';
const routeRaces=()=>D.races.filter(r=>r.kind==='route'&&parseT(r.result)>0);
function recFor(m){const c=routeRaces().filter(r=>Math.abs(r.km*1000-m)<m*.03).sort((a,b)=>parseT(a.result)-parseT(b.result))[0];return c?esc(c.result):'—'}
// Base de calcul unique : VO₂ max du profil, recalée par les courses route (moyenne pondérée, demi-vie 2 ans, facteur borné 0,8–1,1).
function vdBase(){
  const v=+D.profile.vo2,rs=routeRaces().map(r=>({x:vdotOf(r.km*1000,parseT(r.result)),w:Math.pow(.5,Math.max(0,dBetween(r.date,today()))/730)})).filter(o=>o.x>0&&isFinite(o.x));
  if(!(v>0))return rs.length?rs.reduce((a,o)=>a+o.x,0)/rs.length:45;
  if(!rs.length)return v;
  const sw=rs.reduce((a,o)=>a+o.w,0),f=Math.max(.8,Math.min(1.1,Math.exp(rs.reduce((a,o)=>a+o.w*Math.log(o.x/v),0)/sw)));
  return v*f}
const baseVdot=()=>vdBase();
const effKm=r=>(+r.km||0)+(+r.dplus||0)/100;
function flatMin(E,vd){const m=42.195;return E<=m?timeFor(E*1000,vd):timeFor(m*1000,vd)*Math.pow(E/m,1.15)}
function modelMin(r){return flatMin(effKm(r),baseVdot())}
function finished(){const t=today();return D.races.filter(r=>(r.date<=t||parseT(r.result)>0)&&isTrail(r)&&!['DNF','DNS'].includes(r.status))}
function timed(){return finished().filter(r=>parseT(r.result)>0&&effKm(r)>0)}
function calib(tg,excl){let L=timed().filter(r=>r.id!==excl).map(r=>({r,ratio:parseT(r.result)/modelMin(r),model:modelMin(r)}));
  if(tg){const E=effKm(tg),ra=(+tg.dplus||0)/Math.max(1,+tg.km||1);
    const sim=L.filter(x=>{const q=effKm(x.r)/E;return q>=.6&&q<=1.6});
    const prof=sim.filter(x=>{const rr=(+x.r.dplus||0)/Math.max(1,+x.r.km||1);return rr>=ra*.6&&rr<=ra*1.6+5});
    if(prof.length>=3)L=prof;else if(sim.length>=3)L=sim}
  if(!L.length)return{k:1.06,n:0,L,raw:null};
  const wts=L.map(x=>Math.pow(.5,Math.max(0,dBetween(x.r.date,today()))/365)),sw=wts.reduce((a,b)=>a+b,0);
  const raw=Math.exp(L.reduce((a,x,i)=>a+wts[i]*Math.log(x.ratio),0)/sw),w=L.length/(L.length+1);
  return{k:Math.max(.85,Math.min(1.3,1+(raw-1)*w)),n:L.length,L,raw}}
const QF={'Excellent':.98,'Bon':1,'Fatigue':1.03,'Reprise':1.05,'Blessure légère':1.05};
const CF={'Aucune particulière':1,'Roulant':1,'Terrain technique':1.04,'Terrain très technique / alpin':1.07,'Nocturne':1.03,'Nocturne + froid':1.05,'Chaleur (> 25 °C)':1.03,'Chaleur extrême (> 32 °C)':1.06,'Humidité élevée':1.02,'Pluie':1.03,'Pluie / boue':1.05,'Boue / terrain gras':1.05,'Vent fort':1.02,'Brouillard / faible visibilité':1.02,'Froid (< 5 °C)':1.03,'Froid / neige':1.04,'Neige / glace':1.06,'Altitude (> 2000 m)':1.05,'Très forte chaleur + altitude':1.08,'Autre':1.02};
function feelF(v){return 1+(5-(+v||5))*0.012}
function scenarios(r){const c=calib(r),qf=(QF[r.phys]||1)*(CF[r.cond]||1)*feelF(D.profile.feel),b=modelMin(r)*c.k*qf;return{amb:b*.94,real:b,mod:b*1.07,c,qf}}
function feelCard(){const v=+D.profile.feel||5;return `<div class="card"><h2 class="cond">Ressenti du moment</h2><p class="sm mut">Règle le curseur selon ta forme du jour : objectifs, plan de course, plan d'entraînement et nutrition sont recalculés immédiatement. 1 = très fatigué, 10 = en pleine forme.</p><div class="row" style="margin-top:10px;gap:12px;align-items:center"><input type="range" min="1" max="10" step="1" value="${v}" data-c="feel" aria-label="Ressenti du moment" style="flex:1"><b class="cond" style="font-size:1.6rem;min-width:2ch;text-align:center">${v}</b></div><p class="xs mut">Effet sur le temps estimé : ×${fn(feelF(v),3)} (5 = neutre ; chaque point modifie d'environ 1,2 %).</p></div>`}
function refCard(r,sc){const c=sc.c;return `<details class="card hist fold">${foldHead('📚','Courses de référence','Chronos proches utilisés pour recaler le modèle')}<p class="sm mut">Pour « ${esc(r.name)} » (${fn(effKm(r),0)} km-effort, ${fn((+r.dplus||0)/Math.max(1,+r.km||1),0)} m de D+ par km), le modèle est recalé sur tes courses chronométrées au profil proche. Les plus récentes comptent davantage. Ajouter ou corriger une course modifie cette liste et toutes les estimations.</p>${c.L.length?`<div class="tscroll" style="margin-top:10px"><table><thead><tr><th>Course</th><th>Date</th><th>Km-effort</th><th>Chrono</th><th>Écart au modèle</th></tr></thead><tbody>${c.L.map(x=>`<tr><td><button data-a="race" data-id="${x.r.id}" style="text-align:left;text-decoration:underline">${esc(x.r.name)}</button></td><td>${shortD(x.r.date)}</td><td>${fn(effKm(x.r),0)}</td><td>${esc(x.r.result)}</td><td>${x.ratio>1?'+':''}${fn((x.ratio-1)*100,0)} %</td></tr>`).join('')}</tbody></table></div>`:'<div class="empty">Aucune course chronométrée de profil proche : coefficient prudent.</div>'}</details>`}
function racePlan(r,sc){const E=effKm(r),vd=baseVdot(),g=parseT(r.goal),T=g||sc.real,tot=flatMin(E,vd),D0=+r.dplus||0;
  const tc=trailCost(r),rows=(tc?[0,.1,.2,.3,.4,.5,.6,.7,.8,.9,1]:[0,.2,.4,.6,.8,1]).map(f=>tc?{f,km:f*r.km,dp:tc.dp(f*tc.gk),t:f===0?0:T*tc.at(f*tc.gk)}:{f,km:f*r.km,dp:f*D0,t:f===0?0:T*flatMin(f*E,vd)/tot});
  return `<div class="card"><h2 class="cond">Plan de course</h2><p class="sm mut">Temps cible : <b>${fmtT(T)}</b> (${g?'ton objectif':'scénario réalisable'}). ${tc?`Le temps est réparti d'après les pentes de ton GPX (coût énergétique de chaque portion, plus une dérive de fatigue de +${fn(tc.drift*100,0)} % sur la durée) : les montées prennent davantage de temps, les descentes moins.`:'Le temps est réparti selon le coût réel du parcours (km-effort). Ajoute le GPX de la course pour un découpage fidèle au tracé.'} Repère-toi à chaque point et ajuste selon le terrain et ton ressenti du jour.</p><div class="tscroll" style="margin-top:10px"><table><thead><tr><th>Point</th><th>Distance</th><th>D+ cumulé</th><th>Temps cumulé</th><th>Allure moyenne</th></tr></thead><tbody>${rows.map((w,k)=>`<tr><td>${w.f===0?'Départ':w.f===1?'Arrivée':Math.round(w.f*100)+' %'}</td><td>${fn(w.km,1)} km</td><td>${fn(w.dp,0)} m</td><td><b>${k?fmtT(w.t):'0'}</b></td><td>${k&&w.km>0?pace(w.t/w.km)+'/km':'—'}</td></tr>`).join('')}</tbody></table></div></div>`}
function hypCard(r,sc){const c=sc.c,i=raceInfo(r),vd=baseVdot();
  return `<details class="card hist"><summary><h2 class="cond" style="display:inline-block;margin:0">Hypothèses utilisées</h2></summary><ul class="sm" style="padding-left:18px;line-height:1.7"><li>Niveau : base VDOT ${fn(vd,1)} (VO₂ max ${D.profile.vo2||'—'} recalée par ${routeRaces().length} performance(s) route).</li><li>Parcours : ${fn(i.E,0)} km-effort (${fn(r.km)} km + ${fn(r.dplus,0)} m de D+ / 100)${r.dminus!=null&&r.dminus!==''?`, D− ${fn(r.dminus,0)} m`:''}.</li><li>Calibrage trail : ×${fn(c.k,2)} d'après ${c.n} course(s) chronométrée(s).</li>${btLine()}${hypGpx(r)}<li>Facteurs : forme « ${esc(r.phys||'non renseignée')} », conditions « ${esc(r.cond||'non renseignées')} » → ×${fn(sc.qf,2)}.</li><li>Scénarios : ambitieux ×0,94 · réalisable ×1 · modeste ×1,07 (légère baisse de forme ou imprévus raisonnables).</li>${r.site&&/^https?:\/\//i.test(r.site)?`<li>Site de la course : <a href="${esc(r.site)}" target="_blank" rel="noopener">${esc(r.site)}</a></li>`:''}</ul></details>`}

const upcoming=()=>D.races.filter(r=>r.date>=today()&&!parseT(r.result)&&isTrail(r)).sort((a,b)=>a.date<b.date?-1:1);
const selRace=()=>{let r=D.races.find(x=>x.id===S.sel);if(!r){const u=upcoming();r=u[0]||D.races.slice().sort((a,b)=>a.date<b.date?1:-1)[0]}return r};
const zone=(a,b)=>{const p=D.profile,res=p.hrMax-p.hrRest;return [Math.round(p.hrRest+res*a),Math.round(p.hrRest+res*b)]};
const easyPace=()=>{const vd=baseVdot(),target=vd*.66;let lo=60,hi=400;for(let i=0;i<50;i++){const v=(lo+hi)/2;vo2(v)<target?lo=v:hi=v}return 1000/lo};

const ringW=(k,r)=>k==='n'?1:(k==='km'||k==='pace')?(+r.km||0):k==='dp'?(+r.dplus||0):parseT(r.result);
const RING_NOTE={n:'Pourcentage : part du nombre de courses',km:'Pourcentage : part de la distance cumulée',dp:'Pourcentage : part du dénivelé cumulé',time:'Pourcentage : part du temps de course',pace:'Valeur : allure moyenne du type · pourcentage : part des kilomètres chronométrés'};
// Une part par type de course (courts / moyens / longs / ultras) : valeur, pourcentage et courses concernées.
function ringCats(k){
  const m=metrics(),src=k==='n'?m.fin:(k==='time'||k==='pace')?m.tm:m.run,all=sumBy(src,r=>ringW(k,r));
  return [0,1,2,3].map(c=>{const a=src.filter(r=>catOf(r)===c),w=sumBy(a,r=>ringW(k,r)),km=sumBy(a,r=>+r.km||0),dp=sumBy(a,r=>+r.dplus||0),min=sumBy(a,r=>parseT(r.result));
    const v=k==='n'?fn(a.length,0):k==='km'?fn(km,0)+' km':k==='dp'?'+'+fn(dp,0)+' m':k==='time'?fn(min/60,1)+' h':(km>0?pace(min/km).replace('"','')+'/km':'—');
    return{c,name:CAT_N[c],col:CAT_C[c],w,v,races:a.slice().sort(byDateAsc),pct:all>0?w/all*100:0}}).filter(x=>x.w>0)}
function ring(val,unit,label,key){const R=40,C=2*Math.PI*R,cats=ringCats(key),tot=sumBy(cats,x=>x.w);
  let arcs='',off=0;
  cats.forEach(x=>{const len=C*x.w/tot,gap=cats.length>1?Math.min(len*.5,2.6):0,pc=fn(x.pct,1)+' %',lab=`${x.name} : ${pc}, ${x.v}. Voir le détail`;
    arcs+=`<circle class="seg" tabindex="0" role="button" data-a="seg" data-k="${key}" data-cat="${x.c}" data-n="${esc(x.name)}" data-m="${x.races.length} course${x.races.length>1?'s':''}" data-vt="${esc(x.v+' · '+pc)}" data-col="${x.col}" aria-label="${esc(lab)}" cx="50" cy="50" r="${R}" stroke-dasharray="${Math.max(.6,len-gap).toFixed(2)} ${C.toFixed(2)}" stroke-dashoffset="${(-off).toFixed(2)}" style="stroke:${x.col}"></circle>`;off+=len});
  const vs=String(val),fs=vs.length<=5?15:vs.length<=7?12.5:vs.length<=9?10:vs.length<=11?8.6:7.4;
  const leg=cats.map(x=>`<button type="button" class="lg-row" data-a="seg" data-k="${key}" data-cat="${x.c}" aria-label="${esc(`${x.name} : ${fn(x.pct,1)} %, ${x.v}. Voir le détail`)}"><i class="lg-d" style="background:${x.col}"></i><span class="lg-n">${esc(x.name)}</span><span class="lg-p">${fn(x.pct,1)} %</span><span class="lg-v">${esc(x.v)}</span></button>`).join('');
  return `<div class="ringc" role="group" aria-label="${esc(label)}"><div class="rg-wrap"><svg class="ring" viewBox="0 0 100 100" role="group" aria-label="${esc(label)} : répartition par type de course">${cats.length?'':`<circle class="t" cx="50" cy="50" r="${R}"/>`}${arcs}<text class="rg-l" aria-hidden="true" x="50" y="40.5" text-anchor="middle">${esc(label)}</text><text class="rg-v" aria-hidden="true" x="50" y="${(53+fs*.2).toFixed(1)}" text-anchor="middle" style="font-size:${fs}px">${esc(val)}</text><text class="rg-s" aria-hidden="true" x="50" y="64.5" text-anchor="middle">${esc(unit)}</text></svg><button type="button" class="rg-open" data-a="ring" data-k="${key}" aria-label="${esc(`${label} : ${val} ${unit} — détail complet par type de course`)}"></button></div><div class="rg-leg">${leg}</div><p class="rg-note">${esc(RING_NOTE[key]||'')}</p></div>`}
const RING_LAB={n:'du nombre de courses',km:'de ta distance cumulée',dp:'de ton dénivelé cumulé',time:'de ton temps de course',pace:'des kilomètres chronométrés'};
function ringPanelHTML(k,c){
  const d=metricDef(k),cd=ringCats(k).find(x=>x.c===c);if(!d||!cd)return '';
  const n=cd.races.length,pc=x=>fn(x,x<10?1:0)+' %';
  return `<div class="row" style="justify-content:space-between;align-items:flex-start"><div><b class="cond" style="font-size:1.2rem"><span class="dot" style="background:${cd.col}"></span>${esc(cd.name)}</b><div class="sm mut">${esc(d.t)} · ${n} course${n>1?'s':''}</div></div><button class="btn ghost s" data-a="segClose" aria-label="Fermer le détail">✕</button></div>
  <div class="kv" style="margin:10px 0"><div><b>${esc(cd.v)}</b><span>${k==='pace'?'allure moyenne':'total'}</span></div><div><b>${pc(cd.pct)}</b><span>part ${RING_LAB[k]}</span></div>${k==='n'?'':`<div><b>${n}</b><span>course${n>1?'s':''}</span></div>`}</div>
  <div class="tscroll"><table><thead><tr><th>Course</th><th>Date</th><th>Valeur</th>${k==='n'?'':'<th>Part</th>'}</tr></thead><tbody>${cd.races.slice().reverse().map(r=>`<tr><td><button data-a="race" data-id="${r.id}" style="text-align:left;text-decoration:underline">${esc(r.name)}</button></td><td>${shortD(r.date)}</td><td><b>${d.row(r)}</b></td>${k==='n'?'':`<td>${cd.w>0?pc(ringW(k,r)/cd.w*100):'—'}</td>`}</tr>`).join('')}</tbody></table></div>
  <div class="row" style="margin-top:8px"><button class="btn s" data-a="ring" data-k="${k}">Détail complet</button></div>`}
function ringSegs(k){const m=metrics();
  const mk=(r,v,d,vt)=>({v,l:r.name,d,c:CAT_C[catOf(r)],id:r.id,cat:CAT_N[catOf(r)],dt:shortD(r.date),vt});
  if(k==='n')return byCat(m.fin).map(r=>mk(r,1,0,fn(r.km)+' km'+(r.result?' · '+r.result:r.status==='DNF'?' · DNF':'')));
  if(k==='km')return byCat(m.run).map(r=>mk(r,+r.km||0,1,fn(r.km,1)+' km'));
  if(k==='dp')return byCat(m.run).map(r=>mk(r,+r.dplus||0,0,'+'+fn(r.dplus,0)+' m'));
  if(k==='time')return byCat(m.tm).map(r=>mk(r,parseT(r.result),0,fmtT(parseT(r.result))));
  if(k==='pace')return byCat(m.tm).map(r=>mk(r,+r.km||0,1,pace(parseT(r.result)/r.km)+'/km'));
  return null}

/* ============================ STATS ============================ */
const byDateAsc=(a,b)=>a.date<b.date?-1:a.date>b.date?1:0;
const sumBy=(a,f)=>a.reduce((x,r)=>x+f(r),0);
const isPast=r=>r.date<=today()||parseT(r.result)>0;                      // course déjà disputée (date passée ou chrono saisi)
const hasRun=r=>isPast(r)&&!['DNF','DNS'].includes(r.status);  // distance / D+ / temps réellement courus
/* Règle de décompte : « courses » = toutes les courses passées, abandons compris (seuls les non-partants et les courses à venir ne comptent pas) ;
   km, D+ et temps ne comptent que les courses menées à terme. Chaque course non comptée est listée avec sa raison. */
function metrics(){
  const fin=D.races.filter(r=>isPast(r)&&r.status!=='DNS').sort(byDateAsc),run=fin.filter(hasRun),tm=run.filter(r=>parseT(r.result)>0&&+r.km>0);
  const skipped=D.races.filter(r=>!fin.includes(r)).sort(byDateAsc).map(r=>({r,why:r.status==='DNS'?'DNS':'À venir'}));
  const sumT=sumBy(tm,r=>parseT(r.result)),sumK=sumBy(tm,r=>+r.km);
  return{fin,run,tm,skipped,n:fin.length,km:sumBy(run,r=>+r.km||0),dp:sumBy(run,r=>+r.dplus||0),min:sumT,pace:sumK?sumT/sumK:0}}
const CAT_N=['Courts < 21 km','Moyens 21–42 km','Longs 42–80 km','Ultras ≥ 80 km'],CAT_C=['var(--k0)','var(--k1)','var(--k2)','var(--k3)'],catOf=r=>r.km<21?0:r.km<42?1:r.km<80?2:3;
const byCat=a=>a.slice().sort((x,y)=>catOf(x)-catOf(y)||byDateAsc(x,y));
const catLegend=()=>`<div class="leg" style="justify-content:center;margin-top:10px">${CAT_N.map((n,k)=>`<span><i style="display:inline-block;width:12px;height:12px;border-radius:4px;background:${CAT_C[k]};margin-right:5px;vertical-align:-2px"></i>${n}</span>`).join('')}</div>`;
const lbl=r=>({l:r.name,s:shortD(r.date)});
function metricDef(k){
  const m=metrics(),p=D.profile;
  const defs={
   n:{t:'Courses',val:m.n,unit:'courses',col:'var(--acc2)',items:m.fin.map((r,i)=>({...lbl(r),v:i+1})),fmt:x=>fn(x,0),row:r=>fn(r.km)+' km'+(r.status==='DNF'?' · DNF':'')},
   km:{t:'Distance cumulée',val:fn(m.km,0),unit:'km',col:'var(--ice)',items:m.run.map(r=>({...lbl(r),v:+r.km})),fmt:x=>fn(x,0),row:r=>fn(r.km)+' km'},
   dp:{t:'Dénivelé positif cumulé',val:fn(m.dp,0),unit:'m D+',col:'var(--acc)',items:m.run.map(r=>({...lbl(r),v:+r.dplus})),fmt:x=>fn(x,0),row:r=>fn(r.dplus,0)+' m'},
   time:{t:"Temps de course",val:fn(m.min/60,1),unit:'heures',col:'var(--yel)',items:m.tm.map(r=>({...lbl(r),v:parseT(r.result)/60})),fmt:x=>fn(x,1)+' h',row:r=>fmtT(parseT(r.result))},
   pace:{t:'Allure moyenne',val:m.pace?pace(m.pace).replace('"',''):'—',unit:'min/km',col:'var(--acc2)',items:m.tm.map(r=>({...lbl(r),v:parseT(r.result)/r.km})),line:true,fmt:x=>pace(x),row:r=>pace(parseT(r.result)/r.km)+'/km',low:true},
   lvl:{t:'Niveau',val:levelInfo().band[2],unit:'VDOT '+fn(baseVdot(),1),col:'var(--acc)'}};
  return defs[k]}
function catBreak(k,rows){
  const g=[0,1,2,3].map(c=>{const a=rows.filter(r=>catOf(r)===c),km=sumBy(a,r=>+r.km||0),dp=sumBy(a,r=>+r.dplus||0),tm=a.filter(r=>parseT(r.result)>0&&+r.km>0),min=sumBy(tm,r=>parseT(r.result)),kmT=sumBy(tm,r=>+r.km),n=a.length;
    const v=k==='n'?n:k==='km'?km:k==='dp'?dp:k==='time'?min/60:(kmT?min/kmT:0);return{c,n,km,dp,v,w:k==='pace'?kmT:v}});
  const tot=sumBy(g,x=>x.w)||1,fmt=x=>k==='n'?fn(x,0):k==='km'?fn(x,0)+' km':k==='dp'?'+'+fn(x,0)+' m':k==='time'?fn(x,1)+' h':(x?pace(x)+'/km':'—');
  return `<h3 class="cond" style="margin:14px 0 6px">Par type de course</h3><div class="stack" role="img" aria-label="Répartition par type de course">${g.map(x=>x.w>0?`<i style="width:${(x.w/tot*100).toFixed(1)}%;background:${CAT_C[x.c]}" title="${CAT_N[x.c]}"></i>`:'').join('')}</div>
  <div class="tscroll"><table><thead><tr><th>Type</th><th>Courses</th><th>${k==='pace'?'Allure':'Total'}</th><th>Part</th></tr></thead><tbody>${g.map(x=>`<tr><td><span class="dot" style="background:${CAT_C[x.c]}"></span><b>${CAT_N[x.c]}</b>${x.n?`<br><span class="xs mut">moy. ${fn(x.km/x.n,0)} km · +${fn(x.dp/x.n,0)} m</span>`:''}</td><td>${x.n}</td><td><b>${x.n?fmt(x.v):'—'}</b></td><td>${x.w>0?fn(x.w/tot*100,0)+' %':'—'}</td></tr>`).join('')}</tbody></table></div>`}
function ringMark(k,c){$$('.ring .seg, .lg-row').forEach(x=>x.classList.toggle('on',k!=null&&x.dataset.k===k&&+x.dataset.cat===c))}
function segPick(el){
  const k=el.dataset.k,c=+el.dataset.cat,id=k+'|'+c,box=$('#ringpanel');if(!box)return;
  if(S.ringSel===id){segClose();return}
  const cd=ringCats(k).find(x=>x.c===c);if(!cd)return;
  S.ringSel=id;box.style.setProperty('--rc',cd.col);box.innerHTML=ringPanelHTML(k,c);box.classList.remove('hide');ringMark(k,c);
  try{box.scrollIntoView({block:'nearest',behavior:'smooth'})}catch(e){}}
function segClose(){S.ringSel=null;const box=$('#ringpanel');if(box){box.classList.add('hide');box.innerHTML=''}ringMark(null)}
function openMetric(k){
  const d=metricDef(k);if(!d)return;
  if(k==='lvl')return openLevel();
  const m=metrics(),rows=k==='n'?m.fin:(k==='time'||k==='pace')?m.tm:m.run,vs=d.items.map(i=>i.v),nAb=m.fin.filter(r=>r.status==='DNF').length;
  const kv=k==='n'?`<div><b>${m.n}</b><span>courses${nAb?` dont ${nAb} DNF`:''}</span></div><div><b>${fn(m.km,0)}</b><span>km parcourus</span></div><div><b>${m.skipped.length}</b><span>non comptée${m.skipped.length>1?'s':''}</span></div>`
    :`<div><b>${d.val}</b><span>${d.unit}</span></div><div><b>${rows.length}</b><span>courses prises en compte</span></div>${vs.length?`<div><b>${d.fmt(k==='pace'?Math.min(...vs):Math.max(...vs))}</b><span>${k==='pace'?'meilleure':'maximum'}</span></div>`:''}`;
  openModal(`<h2 class="cond">${d.t}</h2><div class="kv" style="margin:12px 0">${kv}</div>
   ${catBreak(k,rows)}<h3 class="cond" style="margin:14px 0 6px">Toutes les courses</h3><div class="tscroll"><table><thead><tr><th>Course</th><th>Date</th><th>Valeur</th></tr></thead><tbody>${rows.slice().reverse().map(r=>`<tr><td><span class="dot" style="background:${CAT_C[catOf(r)]}"></span><button data-a="race" data-id="${r.id}" style="text-align:left;text-decoration:underline">${esc(r.name)}</button></td><td>${shortD(r.date)}</td><td><b>${d.row(r)}</b></td></tr>`).join('')||'<tr><td colspan="3" class="mut">Aucune donnée.</td></tr>'}</tbody></table></div>${k==='n'&&m.skipped.length?`<h3 class="cond" style="margin:16px 0 6px">Non comptées (${m.skipped.length})</h3><p class="xs mut" style="margin-bottom:6px">Ces courses sont dans ta liste mais ne sont pas comptées. Si l'une est passée, saisis son chrono ou corrige son statut.</p><div class="tscroll"><table><tbody>${m.skipped.map(x=>`<tr><td><button data-a="race" data-id="${x.r.id}" style="text-align:left;text-decoration:underline">${esc(x.r.name)}</button></td><td>${shortD(x.r.date)}</td><td>${x.why}</td></tr>`).join('')}</tbody></table></div>`:''}`)}

const LV=[[0,35,'Débutant'],[35,42,'Intermédiaire'],[42,48,'Confirmé'],[48,54,'Avancé'],[54,60,'Expert'],[60,99,'Élite']];
function trailEq(r){const t=parseT(r.result),E=effKm(r);if(!(t>0&&E>=12&&E<=65))return null;let lo=25,hi=90;for(let i=0;i<50;i++){const m=(lo+hi)/2;flatMin(E,m)>t?lo=m:hi=m}return (lo+hi)/2}
function levelInfo(){
  const t=today(),vr=baseVdot(),age=d=>dBetween(d,t),tm=timed();
  const pts=tm.map(r=>({r,v:trailEq(r)})).filter(x=>x.v&&age(x.r.date)>=0).sort((a,b)=>a.r.date<b.r.date?-1:1);
  const rec=pts.filter(x=>age(x.r.date)<=180),old=pts.filter(x=>age(x.r.date)>180&&age(x.r.date)<=365);
  const wm=a=>{let s=0,w=0;a.forEach(x=>{const k=Math.pow(.5,age(x.r.date)/120);s+=x.v*k;w+=k});return w?s/w:null};
  const tNow=wm(rec.length?rec:pts.slice(-4)),tOld=wm(old),lv=vr;
  const band=LV.find(b=>lv>=b[0]&&lv<b[1])||LV[LV.length-1],hiB=Math.min(band[1],66),pos=Math.max(4,Math.min(100,(lv-band[0])/(hiB-band[0])*100));
  const y=tm.filter(r=>age(r.date)<=365&&age(r.date)>=0),all=finished().sort((a,b)=>a.date<b.date?1:-1),last=all.find(r=>r.date<=t);
  const route=routeRaces().sort((a,b)=>a.date<b.date?-1:1),rl=route.length?route[route.length-1].date:null;
  return{vr,tNow,tOld,trend:tNow&&tOld&&rec.length>=2&&old.length>=2?tNow-tOld:null,band,pos,lv,pts,hiB,n12:y.length,km12:y.reduce((s,r)=>s+(+r.km||0),0),dp12:y.reduce((s,r)=>s+(+r.dplus||0),0),longKm:y.reduce((m,r)=>Math.max(m,+r.km||0),0),longDp:y.reduce((m,r)=>Math.max(m,+r.dplus||0),0),last,lastAge:last?age(last.date):null,rl,nroute:route.length}}
function levelCard(){
  const L=levelInfo(),p=D.profile,f=feelF(p.feel);
  if(!routeRaces().length&&!(D.profile.vo2>0))return `<div class="card"><h2 class="cond">Niveau actuel</h2><div class="empty">Ajoute des chronos (route ou trail) pour estimer ton niveau.</div></div>`;
  const next=LV[LV.indexOf(L.band)+1],nx=upcoming()[0],vdP=baseVdot();
  const pred=[[5000,'5 km'],[10000,'10 km'],[21097.5,'21 km'],[42195,'42 km']].map(([m,l])=>`<div><b>${fmtC(timeFor(m,vdP)*f)}</b><span>${l} · prédit</span></div>`).join('');
  const nxT=nx?`<div><b>${fmtT(scenarios(nx).real)}</b><span>${esc(nx.name)} · réaliste</span></div>`:'';
  return `<div class="card"><div class="row" style="justify-content:space-between;margin-bottom:10px"><h2 class="cond" style="margin:0">Niveau actuel</h2><button class="btn ghost s" data-a="ring" data-k="lvl">Détail</button></div>
  <div class="cond lvlname">${L.band[2]}</div><div class="bar" role="img" aria-label="Progression dans le niveau ${L.band[2]}"><i style="width:${L.pos.toFixed(0)}%"></i></div><p class="xs mut" style="margin:6px 0 12px">${next?`encore ${fn(Math.max(0,next[0]-L.lv),1)} points avant « ${next[2]} »`:'Niveau maximal de l\'échelle'}</p>
  <h3 class="cond" style="margin:4px 0 8px">Prédicteur de course</h3><div class="kv">${pred}${nxT}</div>
  <p class="xs mut" style="margin-top:10px">Même base que les chronos cibles : VO₂ max (${p.vo2}) recalée par tes records route (VDOT ${fn(vdP,1)}), × ressenti du jour (×${fn(f,3)}). Mise à jour à chaque modification du profil ou d'une course.</p></div>`}
const fmtC=m=>{if(!m||!isFinite(m))return '—';const t=Math.round(m*60),h=Math.floor(t/3600),mi=Math.floor(t%3600/60),se=t%60;return h?`${h}:${pad(mi)}:${pad(se)}`:`${mi}:${pad(se)}`};
function openLevel(){
  const p=D.profile,L=levelInfo(),vd=baseVdot(),f=feelF(p.feel),dist=[[5000,'5 km'],[10000,'10 km'],[15000,'15 km'],[21097.5,'21 km'],[42195,'42 km']];
  openModal(`<h2 class="cond">Niveau & prédicteur</h2><div class="kv" style="margin:12px 0"><div><b>${L.band[2]}</b><span>niveau</span></div><div><b>${p.utmb}</b><span>Index UTMB</span></div><div><b>${p.hrRest}/${p.hrMax}</b><span>FC repos / max</span></div><div><b>×${fn(f,3)}</b><span>ressenti (${p.feel}/10)</span></div></div>
   <div class="note">Base de calcul : ta VO₂max de montre (${p.vo2}) recalée par tes ${L.nroute} performances route (VDOT ${fn(vd,1)}), corrigée de ton ressenti du jour.</div>
   <h3 class="cond" style="margin:14px 0 6px">Échelle des niveaux</h3><div class="tscroll"><table><tbody>${LV.map(b=>`<tr${b===L.band?' style="font-weight:800"':''}><td>${b[2]}</td><td>${b[0]?b[0]:'<35'}${b[1]<99?'–'+b[1]:'+'}</td><td>${b===L.band?'◀ toi':''}</td></tr>`).join('')}</tbody></table></div>
   <h3 class="cond" style="margin:14px 0 6px">Chronos prédits</h3><div class="tscroll"><table><thead><tr><th>Distance</th><th>Record route</th><th>Prédit</th></tr></thead><tbody>${dist.map(([m,l])=>`<tr><td>${l}</td><td>${recFor(m)}</td><td>${fmtC(timeFor(m,vd)*f)}</td></tr>`).join('')}</tbody></table></div>
   <p class="xs mut" style="margin-top:8px">12 derniers mois : ${L.n12} trails · ${fn(L.km12,0)} km · ${fn(L.dp12,0)} m D+ · plus long D+ ${fn(L.longDp,0)} m. Les paliers sont des repères indicatifs, pas une classification officielle.</p>
   <div class="row" style="margin-top:14px"><button class="btn s" data-a="goProfile">Modifier mon profil</button></div>`)}


/* ============================ MODALE ============================ */
function openModal(h){$('#mbody').innerHTML=h;$('#modal').classList.remove('hide');document.body.style.overflow='hidden';$('.mp').scrollTop=0}
function closeModal(){S.pendProf=null;S.pendTrk=null;if(GPM){try{GPM.remove()}catch(e){}GPM=null}$('#modal').classList.add('hide');$('#mbody').innerHTML='';document.body.style.overflow=''}

/* ============================ PROGRESSION (allure par km-effort) ============================ */
// Allure en min par km-effort (km + D+/100) : comparable d'une course à l'autre, quel que soit le dénivelé.
// Droite des moindres carrés v = a + b·x (b en min par km-effort et par jour) ; null si l'ajustement n'a pas de sens.
function trendLine(P){
  const n=P.length;if(n<4)return null;
  const mx=P.reduce((a,p)=>a+p.x,0)/n,my=P.reduce((a,p)=>a+p.v,0)/n,sxx=P.reduce((a,p)=>a+(p.x-mx)**2,0);
  if(sxx<90*90)return null; // moins de ~3 mois d'écart : pas de tendance
  const b=P.reduce((a,p)=>a+(p.x-mx)*(p.v-my),0)/sxx;return{a:my-b*mx,b}}
// Indice de performance : VDOT « plat » qui donnerait ce chrono sur ce parcours (distance + D+/100). Comparable d'une course à l'autre.
function perfIdx(r){const t=parseT(r.result),E=effKm(r);if(!(t>0&&E>=8))return null;let lo=25,hi=95;for(let i=0;i<50;i++){const m=(lo+hi)/2;flatMin(E,m)>t?lo=m:hi=m}return (lo+hi)/2}
function progressCard(){
  const t0=today(),P=timed().sort(byDateAsc).map(r=>({r,x:pISO(r.date).getTime()/864e5,v:perfIdx(r),age:dBetween(r.date,t0)})).filter(p=>p.v&&isFinite(p.v)&&p.age>=0);
  if(P.length<3)return `<div class="card"><h2 class="cond">Progression</h2><div class="empty">Ajoute au moins trois trails chronométrés pour suivre l'évolution de ton niveau.</div></div>`;
  const narrow=window.innerWidth<600,W=narrow?340:640,H=narrow?260:280,L=narrow?40:46,R=14,T=16,B=32,iw=W-L-R,ih=H-T-B,base=baseVdot();
  const xs=P.map(p=>p.x),vs=P.map(p=>p.v).concat([base]),tr=trendLine(P);
  const x0=Math.min(...xs),x1=Math.max(...xs),sp=Math.max(1,x1-x0),lo0=Math.min(...vs),hi0=Math.max(...vs),pd=Math.max(1,(hi0-lo0)*.12),lo=lo0-pd,hi=hi0+pd;
  const X=x=>L+(x-x0)/sp*iw,Y=v=>T+(hi-v)/(hi-lo)*ih;
  const gl=[0,1,2,3].map(i=>{const v=lo+(hi-lo)*i/3,y=Y(v);return `<line class="gl" x1="${L}" x2="${W-R}" y1="${y.toFixed(1)}" y2="${y.toFixed(1)}"/><text x="${L-8}" y="${(y+4).toFixed(1)}" text-anchor="end">${fn(v,0)}</text>`}).join('');
  const nt=Math.min(narrow?4:5,Math.max(2,Math.floor(sp/60)+1)),xt=Array.from({length:nt},(_,i)=>x0+sp*i/(nt-1)).map((x,i)=>{const d=new Date(Math.round(x)*864e5),dd=new Date(d.getUTCFullYear(),d.getUTCMonth(),d.getUTCDate());return `<text x="${X(x).toFixed(1)}" y="${H-10}" text-anchor="${i===0?'start':i===nt-1?'end':'middle'}">${MON[dd.getMonth()]} ${String(dd.getFullYear()).slice(2)}</text>`}).join('');
  const baseL=`<line x1="${L}" x2="${W-R}" y1="${Y(base).toFixed(1)}" y2="${Y(base).toFixed(1)}" stroke="var(--ice)" stroke-width="1.5" stroke-dasharray="2 5"/><text x="${W-R}" y="${(Y(base)-5).toFixed(1)}" text-anchor="end" style="fill:var(--ice);font-weight:700">niveau actuel ${fn(base,1)}</text>`;
  const trend=tr?`<line x1="${X(x0).toFixed(1)}" y1="${Y(tr.a+tr.b*x0).toFixed(1)}" x2="${X(x1).toFixed(1)}" y2="${Y(tr.a+tr.b*x1).toFixed(1)}" stroke="var(--acc)" stroke-width="2.5" stroke-dasharray="7 5" stroke-linecap="round"/>`:'';
  const best=P.reduce((m,p)=>p.v>m.v?p:m,P[0]);
  const pts=P.map(p=>{const E=effKm(p.r),rad=Math.max(5,Math.min(12,3+Math.sqrt(E)*.75)),tip=`${p.r.name} · ${shortD(p.r.date)} · ${p.r.result} · indice ${fn(p.v,1)} · ${fn(E,0)} km-effort`;
    return `<g class="pt" data-a="race" data-id="${p.r.id}" tabindex="0" role="button" aria-label="${esc(tip)}"><title>${esc(tip)}</title><circle cx="${X(p.x).toFixed(1)}" cy="${Y(p.v).toFixed(1)}" r="${rad.toFixed(1)}" fill="${CAT_C[catOf(p.r)]}" fill-opacity=".85" stroke="${p===best?'var(--ink)':'var(--bg)'}" stroke-width="${p===best?3:2}"/></g>`}).join('');
  const wm=a=>{let s=0,w=0;a.forEach(p=>{const k=Math.pow(.5,p.age/90);s+=p.v*k;w+=k});return w?s/w:null};
  const rec=P.filter(p=>p.age<=180),old=P.filter(p=>p.age>180&&p.age<=365),cur=wm(rec.length?rec:P.slice(-3)),prev=wm(old),delta=cur!=null&&prev!=null&&rec.length>=2&&old.length>=2?cur-prev:null,perYear=tr?tr.b*365:null;
  const kv=`<div><b>${fn(cur,1)}</b><span>niveau récent (6 mois)</span></div>${delta!=null?`<div><b>${delta>=0?'+':'−'}${fn(Math.abs(delta),1)}</b><span>vs les 6 mois d'avant</span></div>`:''}<div><b>${fn(best.v,1)}</b><span>meilleure perf · ${esc(best.r.name.split(' — ')[0])}</span></div>${perYear!=null?`<div><b>${perYear>=0?'+':'−'}${fn(Math.abs(perYear),1)}</b><span>points / an (tendance)</span></div>`:''}`;
  const msg=delta==null?'Pas encore assez de courses sur deux périodes de 6 mois pour mesurer ta progression.':delta>=.5?`Sur les 6 derniers mois, tes performances valent ${fn(cur,1)} contre ${fn(prev,1)} avant : +${fn(delta,1)} point${delta>=1.5?'s':''}. Ton entraînement porte ses fruits, à chiffrer en temps gagné sur une même course.`:delta<=-.5?`Tes performances récentes (${fn(cur,1)}) sont en retrait de ${fn(-delta,1)} par rapport aux 6 mois d'avant (${fn(prev,1)}) : fatigue, blessure, courses très exigeantes ou terrain plus difficile peuvent l'expliquer.`:`Niveau stable : ${fn(cur,1)} contre ${fn(prev,1)} sur les 6 mois d'avant.`;
  const rows=[0,1,2,3].map(c=>{const a=P.filter(p=>catOf(p.r)===c);return a.length?`<tr><td><span class="dot" style="background:${CAT_C[c]}"></span><b>${CAT_N[c]}</b></td><td>${a.length}</td><td>${fn(sumBy(a,p=>p.v)/a.length,1)}</td><td>${fn(Math.max(...a.map(p=>p.v)),1)}</td><td>${fn(a[a.length-1].v,1)}</td></tr>`:''}).join('');
  return `<div class="card prog"><h2 class="cond">Progression</h2><p class="sm mut">Chaque course a un <b>indice de performance</b> : le niveau (VDOT) qui expliquerait ton chrono compte tenu de la distance et du dénivelé. Plus il est haut, plus tu étais en forme ; les courses de profils différents deviennent comparables. Taille du point = ampleur de la course, couleur = type.</p>
  <div class="kv" style="margin:12px 0">${kv}</div>
  <div class="chartbox"><svg class="chart" viewBox="0 0 ${W} ${H}" role="group" aria-label="Indice de performance de chaque course, du ${shortD(P[0].r.date)} au ${shortD(P[P.length-1].r.date)}">${gl}${xt}${baseL}${trend}${pts}</svg></div>
  ${catLegend()}
  <div class="note ${delta!=null&&delta>=.5?'good':''}">${msg}</div>
  <div class="tscroll" style="margin-top:8px"><table><thead><tr><th>Type</th><th>Courses</th><th>Moyenne</th><th>Meilleur</th><th>Dernier</th></tr></thead><tbody>${rows}</tbody></table></div>
  <p class="xs mut" style="margin-top:6px">Contour épais : ton meilleur indice. Tirets orange : tendance. Touche un point pour ouvrir la course. L'indice dépend du modèle de dénivelé : pour les courses très techniques, il est un peu sous-estimé.</p></div>`}

/* ============================ ANALYSES : classiques · fiabilité · index UTMB ============================ */
// --- Mes classiques : une même course courue plusieurs années (le nom, avant « — format », sert de clé) ---
const stripAcc=x=>String(x).normalize('NFD').replace(/[̀-ͯ]/g,'');
function raceKey(name){
  const n=String(name||'').split(/\s[—–-]\s/)[0];
  return stripAcc(n).toLowerCase().replace(/[’`´]/g,"'").replace(/\(.*?\)/g,'').replace(/^(?:(?:le|la|les)\s+|l')/,'').replace(/[^a-z0-9' ]+/g,' ').replace(/\s+/g,' ').trim()}
const effPace=r=>{const t=parseT(r.result),e=effKm(r);return t>0&&e>0&&hasRun(r)?t/e:null}; // min par km-effort
const KM_TOL=5; // deux éditions ne sont comparées que si elles portent le même nom ET une distance à ± 5 km
function classics(list=D.races){
  const g={};list.forEach(r=>{const k=raceKey(r.name);if(k)(g[k]=g[k]||[]).push(r)});
  const groups=[];
  Object.values(g).forEach(a=>{let cur=[];a.slice().sort((x,y)=>(+x.km||0)-(+y.km||0)).forEach(r=>{if(cur.length&&(+r.km||0)-(+cur[0].km||0)>KM_TOL){groups.push(cur);cur=[]}cur.push(r)});if(cur.length)groups.push(cur)});
  return groups.filter(a=>a.length>=2).map(a=>{
    const eds=a.slice().sort(byDateAsc).map(r=>({r,eff:effPace(r)}));
    const tms=eds.filter(e=>e.eff!=null);
    eds.forEach((e,i)=>{const p=eds.slice(0,i).reverse().find(x=>x.eff!=null);e.prev=e.eff!=null&&p?p:null;e.d=e.prev?(e.eff-e.prev.eff)/e.prev.eff:null;
      e.dT=e.prev&&Math.abs(e.r.km/e.prev.r.km-1)<=.08?parseT(e.r.result)-parseT(e.prev.r.result):null});
    const best=tms.length?tms.reduce((m,e)=>e.eff<m.eff?e:m,tms[0]):null,last=tms[tms.length-1]||null;
    return{key:raceKey(a[0].name),name:a.slice().sort(byDateAsc).pop().name.split(/\s[—–-]\s/)[0],km:+eds[eds.length-1].r.km||0,eds,best,last,n:a.length,nTimed:tms.length}}
  ).sort((a,b)=>b.n-a.n||(b.eds[b.eds.length-1].r.date<a.eds[a.eds.length-1].r.date?-1:1))}
const devTxt=d=>d==null?'—':`<span class="dev ${d<0?'up':'dn'}">${d<0?'−':'+'}${fn(Math.abs(d)*100,1)} %</span>`;
function classicsSummary(){const c=classics();if(!c.length)return "Aucune course courue plusieurs fois pour l'instant";
  const up=c.filter(x=>x.last&&x.last.d!=null);return `${c.length} course${c.length>1?'s':''} courue${c.length>1?'s':''} plusieurs fois${up.length?` · ${up.filter(x=>x.last.d<0).length}/${up.length} plus rapide${up.length>1?'s':''} à la dernière édition`:''}`}
function openClassics(){
  const c=classics();
  openModal(`<h2 class="cond">Mes classiques</h2><p class="sm mut" style="margin:6px 0 12px">Les courses de même nom ET de distance proche (à ± 5 km), courues plusieurs fois (ex. une même épreuve courue plusieurs années). La comparaison se fait à l'allure par km-effort, ce qui reste juste si le dénivelé a changé ; l'écart en temps n'apparaît que si la distance est quasi identique (±8 %). Vert = plus rapide que l'édition précédente.</p>
  ${c.length?c.map(g=>`<div class="card" style="margin:0 0 12px"><h3 class="cond" style="margin:0 0 8px">${esc(g.name)} <span class="xs mut">· ≈ ${fn(g.km,0)} km · ${g.n} éditions</span></h3><div class="tscroll"><table><thead><tr><th>Édition</th><th>Chrono</th><th>Vs précédente</th></tr></thead><tbody>${g.eds.map(e=>`<tr><td><button data-a="race" data-id="${e.r.id}" style="text-align:left;text-decoration:underline">${e.r.date.slice(0,4)}</button>${g.best&&e===g.best&&g.nTimed>1?' 🏆':''}<br><span class="xs mut">${fn(e.r.km)} km · +${fn(e.r.dplus,0)} m</span></td><td style="white-space:nowrap"><b>${e.r.result?esc(e.r.result):`<span class="mut">${esc(e.r.status||'—')}</span>`}</b><br><span class="xs mut">${e.eff!=null?pace(e.eff)+'/km-effort':'—'}</span></td><td style="white-space:nowrap">${devTxt(e.d)}${e.dT!=null?`<br><span class="xs mut">${e.dT<0?'−':'+'}${fmtT(Math.abs(e.dT))}</span>`:''}</td></tr>`).join('')}</tbody></table></div></div>`).join(''):'<div class="empty">Aucune course ne revient encore. Dès que tu cours une même épreuve une 2ᵉ fois (même nom, distance à ± 5 km), elle apparaît ici.</div>'}`)}

// --- Fiabilité des prédictions : chaque trail chronométré est prédit SANS lui-même (validation croisée) ---
function backtest(){
  const rows=timed().sort(byDateAsc).map(r=>{const real=parseT(r.result),k=calib(r,r.id),pred=modelMin(r)*k.k;
    return{r,real,pred,err:(pred-real)/real,band:real>=pred*.94&&real<=pred*1.07,n:k.n}}).filter(x=>x.real>0&&isFinite(x.pred)&&x.pred>0);
  const n=rows.length;if(!n)return{rows,n:0};
  const share=f=>rows.filter(f).length/n;
  return{rows,n,mae:sumBy(rows,x=>Math.abs(x.err))/n,bias:sumBy(rows,x=>x.err)/n,w5:share(x=>Math.abs(x.err)<=.05),w10:share(x=>Math.abs(x.err)<=.1),inBand:share(x=>x.band)}}
const btLine=()=>{const b=backtest();return b.n?`<li>Fiabilité : sur tes ${b.n} trails chronométrés, le modèle se trompe de ±${fn(b.mae*100,1)} % en moyenne (chaque course prédite sans elle-même).</li>`:''};
function reliabSummary(){const b=backtest();return b.n>=3?`Erreur moyenne ±${fn(b.mae*100,1)} % · ${b.n} trails testés`:'Pas assez de trails chronométrés'}
function openReliab(){
  const b=backtest();
  if(b.n<3)return openModal(`<h2 class="cond">Fiabilité des prédictions</h2><div class="empty">Il faut au moins 3 trails chronométrés pour tester le modèle.</div>`);
  const W=600,H=150,mid=H/2,mx=Math.max(.1,...b.rows.map(x=>Math.abs(x.err))),bw=W/b.rows.length;
  const bars=b.rows.map((x,i)=>{const h=Math.abs(x.err)/mx*(mid-14),y=x.err>=0?mid-h:mid;return `<rect x="${(i*bw+1.5).toFixed(1)}" y="${y.toFixed(1)}" width="${Math.max(2,bw-3).toFixed(1)}" height="${Math.max(1,h).toFixed(1)}" rx="2" fill="${x.err>=0?'var(--ice)':'var(--acc)'}"><title>${esc(x.r.name)} · ${shortD(x.r.date)} : ${x.err>=0?'+':'−'}${fn(Math.abs(x.err)*100,1)} %</title></rect>`}).join('');
  const bias=Math.abs(b.bias)<.02?'Pas de biais net : le modèle ne penche ni d\'un côté ni de l\'autre.':b.bias<0?`Le modèle est en moyenne <b>trop optimiste</b> de ${fn(-b.bias*100,1)} % (il prédit plus rapide que le réel).`:`Le modèle est en moyenne <b>trop prudent</b> de ${fn(b.bias*100,1)} % (il prédit plus lent que le réel).`;
  openModal(`<h2 class="cond">Fiabilité des prédictions</h2>
  <p class="sm mut" style="margin:6px 0 12px">Méthode : pour chacun de tes ${b.n} trails chronométrés, le modèle refait sa prédiction sans connaître cette course (validation croisée), puis on compare au vrai chrono. C'est le meilleur test honnête avec tes données.</p>
  <div class="kv"><div><b>±${fn(b.mae*100,1)} %</b><span>erreur moyenne</span></div><div><b>${fn(b.w5*100,0)} %</b><span>des courses à ±5 %</span></div><div><b>${fn(b.w10*100,0)} %</b><span>des courses à ±10 %</span></div><div><b>${fn(b.inBand*100,0)} %</b><span>dans la fourchette ambitieux–modeste</span></div></div>
  <p class="sm" style="margin:12px 0">${bias}</p>
  <h3 class="cond" style="margin:10px 0 6px">Écart par course (ancienne → récente)</h3><div class="chartbox"><svg class="chart" viewBox="0 0 ${W} ${H}" style="min-width:0" role="img" aria-label="Écart entre chrono prédit et chrono réel pour chaque course"><line class="gl" x1="0" x2="${W}" y1="${mid}" y2="${mid}"/>${bars}</svg></div>
  <p class="xs mut">Bleu au-dessus : prédit plus lent que le réel. Orange en dessous : prédit plus rapide (trop optimiste).</p>
  <h3 class="cond" style="margin:14px 0 6px">Détail</h3><div class="tscroll"><table><thead><tr><th>Course</th><th>Réel</th><th>Prédit</th><th>Écart</th></tr></thead><tbody>${b.rows.slice().reverse().map(x=>`<tr><td><button data-a="race" data-id="${x.r.id}" style="text-align:left;text-decoration:underline">${esc(x.r.name)}</button><br><span class="xs mut">${shortD(x.r.date)}</span></td><td style="white-space:nowrap">${fmtT(x.real)}</td><td style="white-space:nowrap">${fmtT(x.pred)}</td><td style="white-space:nowrap"><span class="dev ${Math.abs(x.err)<=.05?'up':Math.abs(x.err)>.1?'dn':''}">${x.err>=0?'+':'−'}${fn(Math.abs(x.err)*100,1)} %</span></td></tr>`).join('')}</tbody></table></div>`)}

// --- Index UTMB : historique saisi, objectif, courses classées ---
// L'index est calculé par UTMB (formule non publique) : on le suit tel que tu le lis sur ton profil UTMB, sans le recalculer.
const byD=(a,b)=>a.d<b.d?-1:a.d>b.d?1:0;
function utmbHist(){return (Array.isArray(D.profile.utmbHist)?D.profile.utmbHist:[]).filter(e=>e&&e.d&&+e.v>0).map(e=>({d:e.d,v:+e.v})).sort(byD)}
function utmbNote(v,d=today()){v=+v;if(!(v>0)||!/^\d{4}-\d{2}-\d{2}$/.test(d))return false;
  const h=utmbHist().filter(e=>e.d!==d);h.push({d,v});h.sort(byD);D.profile.utmbHist=h;D.profile.utmb=h[h.length-1].v;save();return true}
function utmbSummary(){const h=utmbHist(),p=D.profile;if(!h.length)return p.utmb>0?`Index ${p.utmb}`:'Note ton index pour suivre sa courbe';
  const l=h[h.length-1],f=h.length>1?h[h.length-2]:null,dl=f?l.v-f.v:null;
  return `Index ${l.v}${dl!=null?` (${dl>=0?'+':'−'}${Math.abs(dl)} depuis le ${shortD(f.d)})`:''}${+p.utmbGoal>0?` · objectif ${p.utmbGoal}`:''}`}
function utmbChart(h,goal){
  const narrow=window.innerWidth<600,W=narrow?340:640,H=220,L=narrow?40:48,R=14,T=14,B=30,iw=W-L-R,ih=H-T-B;
  const xs=h.map(e=>pISO(e.d).getTime()/864e5),vs=h.map(e=>e.v).concat(goal>0?[goal]:[]);
  const x0=Math.min(...xs),x1=Math.max(...xs),sp=Math.max(1,x1-x0),lo0=Math.min(...vs),hi0=Math.max(...vs),pd=Math.max(8,(hi0-lo0)*.18),lo=lo0-pd,hi=hi0+pd;
  const X=x=>L+(x-x0)/sp*iw,Y=v=>T+(hi-v)/(hi-lo)*ih;
  const gl=[0,1,2,3].map(i=>{const v=lo+(hi-lo)*i/3,y=Y(v);return `<line class="gl" x1="${L}" x2="${W-R}" y1="${y.toFixed(1)}" y2="${y.toFixed(1)}"/><text x="${L-6}" y="${(y+4).toFixed(1)}" text-anchor="end">${Math.round(v)}</text>`}).join('');
  const goalL=goal>0?`<line x1="${L}" x2="${W-R}" y1="${Y(goal).toFixed(1)}" y2="${Y(goal).toFixed(1)}" stroke="var(--acc)" stroke-width="2" stroke-dasharray="7 5"/><text x="${W-R}" y="${(Y(goal)-6).toFixed(1)}" text-anchor="end" style="fill:var(--acc)">objectif ${goal}</text>`:'';
  const line=`<polyline points="${h.map(e=>`${X(pISO(e.d).getTime()/864e5).toFixed(1)},${Y(e.v).toFixed(1)}`).join(' ')}" fill="none" stroke="var(--ice)" stroke-width="2.5" stroke-linejoin="round"/>`;
  const pts=h.map(e=>`<circle cx="${X(pISO(e.d).getTime()/864e5).toFixed(1)}" cy="${Y(e.v).toFixed(1)}" r="5" fill="var(--ice)" stroke="var(--bg)" stroke-width="2"><title>${shortD(e.d)} : ${e.v}</title></circle>`).join('');
  return `<div class="chartbox"><svg class="chart" viewBox="0 0 ${W} ${H}" style="min-width:0" role="img" aria-label="Évolution de l'index UTMB">${gl}${goalL}${line}${pts}<text x="${L}" y="${H-8}">${shortD(h[0].d)}</text><text x="${W-R}" y="${H-8}" text-anchor="end">${shortD(h[h.length-1].d)}</text></svg></div>`}
function openUtmb(){
  const h=utmbHist(),p=D.profile,goal=+p.utmbGoal||0,cur=h.length?h[h.length-1].v:(+p.utmb||0);
  const rs=D.races.filter(r=>r.utmbCat||r.utmbPts).sort(byDateAsc).reverse();
  openModal(`<h2 class="cond">Index UTMB</h2>
  <div class="kv" style="margin:12px 0"><div><b>${cur||'—'}</b><span>index actuel</span></div>${goal?`<div><b>${goal}</b><span>objectif</span></div><div><b>${cur>=goal?'atteint ✅':'−'+(goal-cur)}</b><span>${cur>=goal?'objectif':'écart à combler'}</span></div>`:''}</div>
  ${h.length>=2?utmbChart(h,goal):`<div class="note">Note ton index à chaque mise à jour de ton profil UTMB (environ une fois par mois) : la courbe apparaît dès le 2ᵉ relevé.</div>`}
  <h3 class="cond" style="margin:14px 0 6px">Noter mon index</h3>
  <div class="frm"><label class="f">Index<input id="u-v" type="number" inputmode="numeric" placeholder="ex. 600" value="${cur||''}"></label><label class="f">Date<input id="u-d" type="date" value="${today()}"></label></div>
  <div class="row" style="margin-top:10px"><button class="btn s" data-a="utmbAdd">💾 Enregistrer ce relevé</button></div>
  <h3 class="cond" style="margin:16px 0 6px">Mon objectif</h3>
  <div class="frm"><label class="f">Index visé<input id="u-g" type="number" inputmode="numeric" placeholder="ex. 650" value="${goal||''}"></label></div>
  <div class="row" style="margin-top:10px"><button class="btn ghost s" data-a="utmbGoal">🎯 Enregistrer l'objectif</button></div>
  ${h.length?`<h3 class="cond" style="margin:16px 0 6px">Relevés</h3><div class="tscroll"><table><tbody>${h.slice().reverse().map(e=>`<tr><td>${longD(e.d)}</td><td><b>${e.v}</b></td><td><button data-a="utmbDel" data-d="${e.d}" aria-label="Supprimer le relevé du ${e.d}">✕</button></td></tr>`).join('')}</tbody></table></div>`:''}
  <h3 class="cond" style="margin:16px 0 6px">Courses comptant pour l'UTMB</h3>
  ${rs.length?`<div class="tscroll"><table><thead><tr><th>Course</th><th>Catégorie</th><th>Points</th></tr></thead><tbody>${rs.map(r=>`<tr><td><button data-a="race" data-id="${r.id}" style="text-align:left;text-decoration:underline">${esc(r.name)}</button><br><span class="xs mut">${shortD(r.date)}</span></td><td>${r.utmbCat?utmbLogo(r.utmbCat):'—'}</td><td>${esc(r.utmbPts||'—')}</td></tr>`).join('')}</tbody></table></div>`:'<p class="sm mut">Renseigne la catégorie et les points UTMB dans la fiche d\'une course pour la voir ici.</p>'}
  <p class="xs mut" style="margin-top:12px">L'index est calculé par UTMB avec une formule non publique : Vertex ne le recalcule pas, il garde l'historique que tu y saisis.</p>`)}
function utmbAddFromForm(){const v=+$('#u-v').value,d=$('#u-d').value;if(!utmbNote(v,d))return toast('Saisis un index valide et une date.',1);toast('Relevé enregistré.');render();openUtmb()}
function utmbGoalFromForm(){const g=+$('#u-g').value;D.profile.utmbGoal=g>0?g:'';save();toast(g>0?'Objectif enregistré.':'Objectif retiré.');render();openUtmb()}
function utmbDelete(d){D.profile.utmbHist=utmbHist().filter(e=>e.d!==d);const h=utmbHist();if(h.length)D.profile.utmb=h[h.length-1].v;save();render();openUtmb()}

function analysesRow(){
  return `<div class="sec"><h2 class="cond">Analyses</h2></div><div class="grid g3">
  <button class="quick" data-a="seasonPlan"><i>📅</i><span><b>Ma saison</b><small class="mut">${seasonSummary()}</small></span></button>
  <button class="quick" data-a="classics"><i>🏁</i><span><b>Mes classiques</b><small class="mut">${classicsSummary()}</small></span></button>
  <button class="quick" data-a="reliab"><i>🎯</i><span><b>Fiabilité des prédictions</b><small class="mut">${reliabSummary()}</small></span></button>
  <button class="quick" data-a="utmb"><i>📈</i><span><b>Index UTMB</b><small class="mut">${utmbSummary()}</small></span></button></div>`}

/* ============================ FICHE JOUR J ============================ */
// Temps de passage : le temps cible est réparti selon le coût réel du parcours (km-effort), comme le plan de course ; la fourchette est × 0,94 / × 1,07.
function passageTable(r,T){
  const km=+r.km||0;if(!(km>0&&T>0))return [];
  const E=effKm(r),vd=baseVdot(),tot=flatMin(E,vd),D0=+r.dplus||0,F=fuel(T),tc=trailCost(r),PL=fuelPlan(T),step=km<=50?5:km<=100?10:20,xs=[];
  for(let x=step;x<km-step*.25;x+=step)xs.push(x);xs.push(km);
  const start=/^\d{1,2}:\d{2}$/.test(r.startTime||'')?r.startTime.split(':').map(Number):null;
  let px=0,pt=0;
  return xs.map((x,i)=>{const t=i===xs.length-1?T:tc?T*tc.at(x/km*tc.gk):T*flatMin(x/km*E,vd)/tot,o={km:x,dp:tc?tc.dp(x/km*tc.gk):x/km*D0,t,lo:t*.94,hi:t*1.07,seg:(t-pt)/(x-px),
      gels:F.cph?PL.ev.filter(e=>e.t<=t+.01).length:0,carb:Math.round(F.cph*t/60),finish:i===xs.length-1};
    if(start){const m=start[0]*60+start[1]+t;o.clock=`${pad(Math.floor(m/60)%24)}:${pad(Math.floor(m%60))}`;o.day=Math.floor(m/1440)}
    px=x;pt=t;return o})}
function openFiche(id){
  const r=D.races.find(x=>x.id===id);if(!r)return;
  const sc=scenarios(r),g=parseT(r.goal),T=g||sc.real,F=fuel(T),rows=passageTable(r,T),i=raceInfo(r);
  let nx=-1;if(r.date===today()&&/^\d{1,2}:\d{2}$/.test(r.startTime||'')){const [h,m]=r.startTime.split(':').map(Number),n=new Date(),el=n.getHours()*60+n.getMinutes()-(h*60+m);nx=rows.findIndex(x=>x.t>=el)}
  const hasClock=rows.some(x=>x.clock);
  openModal(`<div class="fiche"><h2 class="cond">${esc(r.name)}</h2><p class="mut sm">${longD(r.date)}${r.startTime?` · départ ${esc(r.startTime)}`:''} · ${fn(r.km)} km · +${fn(r.dplus,0)} m</p>
  <div class="kv" style="margin:12px 0"><div><b>${fmtT(T)}</b><span>temps cible (${g?'ton objectif':'réalisable'})</span></div><div><b>${pace(T/r.km)}/km</b><span>allure moyenne</span></div>${F.cph?`<div><b>${F.cph} g/h</b><span>glucides · iso+ compris</span></div>`:'<div><b>À la soif</b><span>pas de gel nécessaire</span></div>'}<div><b>${F.water} ml/h</b><span>eau</span></div>${F.iso?`<div><b>${F.iso} ml/h</b><span>iso+</span></div>`:''}${F.na?`<div><b>${F.na} mg/h</b><span>sodium</span></div>`:''}</div>
  <div class="tscroll"><table><thead><tr><th>Km</th><th>${hasClock?'Heure':'Temps'}</th><th>Allure</th><th>Nutrition</th></tr></thead><tbody>${rows.map((x,k)=>`<tr class="${k===nx?'nx':''}"><td><b>${fn(x.km,x.km%1?1:0)}</b>${x.finish?' 🏁':''}<br><span class="xs mut">+${fn(x.dp,0)} m</span></td><td style="white-space:nowrap"><b>${hasClock?x.clock+(x.day?` (+${x.day} j)`:''):fmtT(x.t)}</b>${hasClock?`<br><span class="xs mut">${fmtT(x.t)}</span>`:''}<br><span class="xs mut">${fmtT(x.lo)} – ${fmtT(x.hi)}</span></td><td style="white-space:nowrap">${pace(x.seg)}<br><span class="xs mut">/km</span></td><td style="white-space:nowrap">${F.cph?`<b>${x.gels} prise${x.gels>1?'s':''}</b><br><span class="xs mut">${x.carb} g cumulés</span>`:'—'}</td></tr>`).join('')}</tbody></table></div>
  <p class="xs mut" style="margin-top:8px">Lignes grises : temps écoulé (si l'heure est affichée) et fourchette ambitieux (×0,94) – modeste (×1,07). Nutrition = cumul depuis le départ. ${hasClock?'':"Renseigne l'heure de départ dans la fiche de la course pour afficher les heures de passage. "}${nx>=0?'Ligne verte : prochain point de passage.':''}</p>
  ${F.cph?`<h3 class="cond" style="margin:16px 0 6px">Plan de ravitaillement</h3>${fuelPlanHTML(r,T)}`:''}
  ${r.prof?profileBlock(r,T,true):''}
  ${r.notes?`<p class="sm" style="margin-top:6px"><b>Notes :</b> ${esc(r.notes)}</p>`:''}
  <div class="row noprint" style="margin-top:14px"><button class="btn s" data-a="printFiche">🖨️ Imprimer / PDF</button><button class="btn ghost s" data-a="wake">📱 Garder l'écran allumé</button></div></div>`)}
function printFiche(){document.body.classList.add('printing');try{window.print()}finally{setTimeout(()=>document.body.classList.remove('printing'),500)}}
window.addEventListener('afterprint',()=>document.body.classList.remove('printing'));
let WAKE=null;
async function toggleWake(){try{if(WAKE){await WAKE.release();WAKE=null;toast('Écran : veille normale.')}else{WAKE=await navigator.wakeLock.request('screen');WAKE.addEventListener('release',()=>{WAKE=null});toast('Écran maintenu allumé tant que cette fiche est ouverte.')}}catch(e){toast("Impossible de garder l'écran allumé sur cet appareil.",1)}}

/* ============================ BILAN DE SAISON ============================ */
function seasonStats(y,list=D.races){
  const rs=list.filter(r=>String(r.date).slice(0,4)===String(y)).sort(byDateAsc);
  const fin=rs.filter(r=>isPast(r)&&r.status!=='DNS'),run=fin.filter(hasRun),tm=run.filter(r=>parseT(r.result)>0&&+r.km>0);
  const eff=r=>parseT(r.result)/effKm(r),tt=tm.filter(r=>isTrail(r)&&effKm(r)>0);
  const pick=(a,f,better)=>a.reduce((m,r)=>m==null||better(f(r),f(m))?r:m,null);
  const byMonth=Array(12).fill(0);run.forEach(r=>{byMonth[+r.date.slice(5,7)-1]+=+r.km||0});
  return{y:String(y),races:rs,n:fin.length,ab:fin.filter(r=>r.status==='DNF').length,pending:rs.length-fin.length,
    km:sumBy(run,r=>+r.km||0),dp:sumBy(run,r=>+r.dplus||0),min:sumBy(tm,r=>parseT(r.result)),
    best:pick(tt,eff,(a,b)=>a<b),longest:pick(run,r=>+r.km||0,(a,b)=>a>b),hiDp:pick(run,r=>+r.dplus||0,(a,b)=>a>b),byMonth,eff}}
function countIn(root){
  if(!root||(window.matchMedia&&matchMedia('(prefers-reduced-motion: reduce)').matches))return;
  root.querySelectorAll('.cu').forEach(el=>{const v=+el.dataset.v,d=+el.dataset.d||0;if(!(v>0))return;const t0=performance.now(),st=t=>{const k=Math.min(1,(t-t0)/1100),e=1-Math.pow(1-k,3);el.textContent=fn(v*e,d);if(k<1)requestAnimationFrame(st)};requestAnimationFrame(st)})}
function openSeason(y){
  const a=seasonStats(y),b=seasonStats(+y-1),cur=String(y)===today().slice(0,4),prev=b.n>0;
  const mx=Math.max(1,...a.byMonth),W=600,H=176,bw=W/12,LT='JFMAMJJASOND',bm=Math.max(...a.byMonth)>0?a.byMonth.indexOf(Math.max(...a.byMonth)):-1;
  const dl=(x,z,abs)=>prev&&z>0?`<span class="sb-d ${x>=z?'up':'dn'}">${x>=z?'▲':'▼'} ${abs?Math.abs(x-z):Math.round(Math.abs(x-z)/z*100)+' %'}</span>`:'';
  const run=a.races.filter(r=>isPast(r)&&hasRun(r)),cat=r=>r.km<21?0:r.km<42?1:r.km<80?2:3,CN=['Courts < 21 km','Moyens 21–42 km','Longs 42–80 km','Ultras ≥ 80 km'],CC=['var(--k0)','var(--k1)','var(--k2)','var(--k3)'],cc=[0,0,0,0];run.forEach(r=>cc[cat(r)]++);
  const mc=Array.from({length:12},()=>[0,0,0,0]);run.forEach(r=>{mc[+r.date.slice(5,7)-1][cat(r)]+=+r.km||0});
  const bars=a.byMonth.map((v,i)=>{const x=i*bw+6,w=bw-12,cx=(x+w/2).toFixed(1),full=v/mx*(H-56);let yy=H-24;
    const segs=mc[i].map((km,k)=>{if(!(km>0))return '';const h=Math.max(2,km/mx*(H-56));yy-=h;return `<rect x="${x.toFixed(1)}" y="${yy.toFixed(1)}" width="${w.toFixed(1)}" height="${h.toFixed(1)}" rx="4" fill="${CC[k]}" style="animation-delay:${i*70}ms"><title>${MONL[i]} · ${CN[k]} : ${fn(km,0)} km</title></rect>`}).join('');
    return `<g><title>${MONL[i]} : ${fn(v,0)} km</title>${segs}${i===bm&&v>0?`<rect x="${(x-3).toFixed(1)}" y="${(H-24-full-3).toFixed(1)}" width="${(w+6).toFixed(1)}" height="${(full+6).toFixed(1)}" rx="8" fill="none" stroke="var(--ink)" stroke-width="2"/>`:''}${v>0?`<text x="${cx}" y="${(H-30-full).toFixed(1)}" text-anchor="middle" style="font-weight:800;fill:var(--ink)">${fn(v,0)}</text>`:''}<text x="${cx}" y="${H-7}" text-anchor="middle">${LT[i]}</text></g>`}).join('');
  const hl=[a.longest&&['📏','Plus longue',`${esc(a.longest.name)}`,`${fn(a.longest.km)} km`,a.longest.id],a.hiDp&&['🏔️','Plus gros dénivelé',`${esc(a.hiDp.name)}`,`+${fn(a.hiDp.dplus,0)} m`,a.hiDp.id],a.best&&['⚡','Meilleure allure / km-effort',`${esc(a.best.name)}`,pace(a.eff(a.best)),a.best.id]].filter(Boolean);
  const tl=a.races.map(r=>{const res=parseT(r.result)>0,up=!isPast(r),st=r.status==='DNF'?'dn':up?'up':res?'ok':'';
    return `<button class="sb-ev ${st}" data-a="race" data-id="${r.id}"><span class="sb-dot"></span><span class="sb-ed">${shortD(r.date)}</span><span class="sb-en"><b>${esc(r.name)}</b><small>${fn(r.km)} km · +${fn(r.dplus,0)} m</small></span><span class="sb-er">${r.result?esc(r.result):esc(r.status||(up?'À venir':'—'))}</span></button>`}).join('');
  openModal(`<div class="sb-hero"><svg class="sb-art" viewBox="0 0 600 200" preserveAspectRatio="xMidYMax slice" aria-hidden="true"><defs><linearGradient id="sbg1" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2C5240"/><stop offset="1" stop-color="#0E1D16"/></linearGradient><linearGradient id="sbg2" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#1D3D2D"/><stop offset="1" stop-color="#0A140F"/></linearGradient></defs><circle class="sb-sun" cx="470" cy="62" r="26" fill="#F27A2A" opacity=".9"/><circle cx="470" cy="62" r="52" fill="#F27A2A" opacity=".18"/><path d="M0 150 L70 104 L120 128 L210 56 L270 100 L340 70 L420 120 L500 84 L600 130 V200 H0Z" fill="url(#sbg1)"/><path d="M210 56 l-14 18 l10 -4 l8 10 l8 -10 l10 4z" fill="#F2EFE4" opacity=".8"/><path d="M0 176 C100 156 200 170 300 158 S500 168 600 152 V200 H0Z" fill="url(#sbg2)"/><path class="sb-trail" d="M20 190 C120 168 170 150 250 134 S380 110 440 92 S530 80 575 72" fill="none" stroke="#F27A2A" stroke-width="3" stroke-linecap="round"/><circle cx="575" cy="72" r="6" fill="#F2EFE4" stroke="#F27A2A" stroke-width="3"/></svg>
   <span class="sb-badge">${cur?'🔥 Saison en cours':'🏁 Saison terminée'}</span><span class="sb-y cond">${y}</span>
   <span class="sb-sub">${a.n} course${a.n>1?'s':''}${a.ab?` dont ${a.ab} DNF`:''}${a.races.length?` · du ${shortD(a.races[0].date)} au ${shortD(a.races[a.races.length-1].date)}`:''}</span></div>
   <div class="kv sb-kv"><div style="--c:${CC[0]}"><b><span class="cu" data-v="${a.n}" data-d="0">${a.n}</span></b><span>Courses</span>${dl(a.n,b.n,true)}</div><div style="--c:${CC[1]}"><b><span class="cu" data-v="${a.km}" data-d="0">${fn(a.km,0)}</span> km</b><span>Distance</span>${dl(a.km,b.km)}</div><div style="--c:${CC[2]}"><b>+<span class="cu" data-v="${a.dp}" data-d="0">${fn(a.dp,0)}</span> m</b><span>Dénivelé positif</span>${dl(a.dp,b.dp)}</div><div style="--c:${CC[3]}"><b><span class="cu" data-v="${a.min/60}" data-d="1">${fn(a.min/60,1)}</span> h</b><span>Temps</span>${dl(a.min,b.min)}</div></div>
   ${prev?`<p class="xs mut">Flèches : évolution par rapport à ${b.y}.</p>`:''}
   ${a.pending?`<p class="sm mut">${a.pending} course${a.pending>1?'s':''} à venir ou DNS, non comptée${a.pending>1?'s':''}.</p>`:''}
   ${hl.length?`<h3 class="cond gp-h">Temps forts</h3><div class="sb-hls">${hl.map(([ic,k,n,v,id],i)=>`<button class="sb-hl" style="animation-delay:${i*90}ms" data-a="race" data-id="${id}"><span class="sb-hi">${ic}</span><span><small>${k}</small><b>${n}</b></span><em>${v}</em></button>`).join('')}</div>`:''}
   <h3 class="cond gp-h">Kilomètres par mois</h3><div class="chartbox"><svg class="chart mbars" viewBox="0 0 ${W} ${H}" style="min-width:0" role="img" aria-label="Kilomètres courus par mois en ${y}">${bars}</svg></div>${run.length?`<div class="leg" style="margin-top:6px">${CN.map((n,k)=>`<span><i style="display:inline-block;width:12px;height:12px;border-radius:4px;background:${CC[k]};margin-right:5px;vertical-align:-2px"></i>${n}</span>`).join('')}</div>`:''}${bm>=0?`<p class="xs mut">🔥 Meilleur mois : ${MONL[bm]} (${fn(a.byMonth[bm],0)} km)</p>`:''}
   ${run.length?`<h3 class="cond gp-h">Types de courses</h3>${cc.map((c,k)=>`<div class="gp-hr"><span class="gp-hl"><i style="background:${CC[k]}"></i>${CN[k]}</span><span class="gp-hb"><b style="width:${(c/run.length*100).toFixed(0)}%;background:${CC[k]}"></b></span><span class="gp-hv">${c} course${c>1?'s':''}</span></div>`).join('')}`:''}
   <h3 class="cond gp-h">Courses de la saison</h3><div class="sb-tl">${tl||'<p class="sm mut">Aucune course.</p>'}</div>`);
  countIn($('#mbody'))}

/* ============================ AUTO-TESTS ============================ */
// Exécutés sur une copie des données de départ : aucune écriture dans tes vraies données.
function runSelfTests(){
  const out=[],keep={D,BOOTED};
  const t=(name,fn)=>{try{fn();out.push({name,ok:true})}catch(e){out.push({name,ok:false,msg:String(e&&e.message||e)})}};
  const ok=(c,m)=>{if(!c)throw new Error(m||'condition fausse')};
  const eq=(a,b,e=1e-6)=>{if(!(Math.abs(a-b)<=e))throw new Error(`attendu ${b}, obtenu ${a}`)};
  D=normalizeDoc(null);BOOTED=false;
  try{
    t('parseT : formats de chrono',()=>{
      eq(parseT("1:05:00"),65);eq(parseT("6h34'59"),394+59/60);eq(parseT("1h38"),98);eq(parseT("1h35'40"),95+40/60);
      eq(parseT("42'42"),42+42/60);eq(parseT("42"),42);eq(parseT("1h"),60);eq(parseT(" 2H05 "),125)});
    t('parseT : valeurs illisibles → 0',()=>{eq(parseT(''),0);eq(parseT(null),0);eq(parseT(undefined),0);eq(parseT('abc'),0)});
    t('fmtT / pace : formats',()=>{ok(fmtT(65)==='1 h 05',fmtT(65));ok(fmtT(59.6)==='1 h 00',fmtT(59.6));ok(pace(4.5)==='4\'30"',pace(4.5));ok(fmtT(0)==='—')});
    t('effKm = km + D+/100',()=>{eq(effKm({km:20,dplus:500}),25);eq(effKm({km:10}),10)});
    const race=(o={})=>Object.assign({id:'t-race',name:'Test',date:addD(today(),112),km:42,dplus:1800,dminus:1800,goal:'',kind:'trail',status:'',result:'',rank:'',notes:''},o);
    t('scenarios : ambitieux < réaliste < modeste',()=>{const s=scenarios(race());ok(s.amb<s.real&&s.real<s.mod,'ordre');eq(s.amb,s.real*.94,1e-6);eq(s.mod,s.real*1.07,1e-6);ok(isFinite(s.real)&&s.real>0)});
    t('scenarios : plus de D+ → plus lent',()=>{ok(scenarios(race({dplus:3000})).real>scenarios(race({dplus:500})).real)});
    t('scenarios : ressenti faible → plus lent',()=>{D.profile.feel=9;const a=scenarios(race()).real;D.profile.feel=2;const b=scenarios(race()).real;D.profile.feel=5;ok(b>a)});
    t('genPlan : structure du plan',()=>{
      const r=race(),pl=genPlan(r);
      ok(pl.weeks.length===pl.W&&pl.W>=2,'nombre de semaines');
      ok(pl.weeks.every((w,i)=>w.i===i&&w.sess.length>0&&isFinite(w.km)&&isFinite(w.dp)&&isFinite(w.dur)&&w.km>=0),'semaines valides');
      ok(dow(pl.weeks[0].ws)===0,'chaque semaine commence un lundi');
      ok(pl.weeks[pl.W-1].sess.some(s=>s.ty==='race'),'la dernière semaine contient la course');
      const peak=Math.max(...pl.weeks.map(w=>w.km));ok(pl.weeks[pl.W-1].km<peak,"l'affûtage allège la dernière semaine")});
    t('genPlan : même résultat à chaque appel',()=>{const r=race(),a=genPlan(r),b=genPlan(r);ok(JSON.stringify(a.weeks.map(w=>w.km))===JSON.stringify(b.weeks.map(w=>w.km)))});
    t('décompte : chaque course est comptée ou listée avec sa raison',()=>{
      D.races.push(race({id:'x-ab',date:'2025-01-01',status:'DNF'}),race({id:'x-dns',date:'2025-01-02',status:'DNS'}),race({id:'x-fut',date:addD(today(),30)}));
      const m=metrics();ok(m.n+m.skipped.length===D.races.length,`${m.n}+${m.skipped.length}≠${D.races.length}`);
      ok(m.fin.some(r=>r.id==='x-ab'),"un DNF compte comme une course");ok(!m.run.some(r=>r.id==='x-ab'),"un DNF n'ajoute pas de km");
      ok(m.skipped.some(x=>x.r.id==='x-dns')&&m.skipped.some(x=>x.r.id==='x-fut'),'DNS et course à venir listés');
      ok(ringSegs('n').length===m.n,'segments du cercle = nombre de courses')});
    t('cercles : parts par type de course',()=>{['n','km','dp','time','pace'].forEach(k=>{const c=ringCats(k);ok(c.length>0&&c.length<=4,k+' : parts');eq(c.reduce((a,x)=>a+x.pct,0),100,1e-6)});eq(ringCats('n').reduce((a,x)=>a+x.races.length,0),metrics().n);ok(!/NaN|undefined/.test(ring('1','x','Test','n')),'rendu sans NaN')});
    t('bilan de saison : la somme des années = le total',()=>{
      const ys=[...new Set(D.races.map(r=>r.date.slice(0,4)))];eq(ys.reduce((a,y)=>a+seasonStats(y).n,0),metrics().n);
      eq(ys.reduce((a,y)=>a+seasonStats(y).km,0),metrics().km,1e-6)});
    t('tendance de progression',()=>{
      const mk=(n,f)=>Array.from({length:n},(_,i)=>({x:i*60,v:f(i)}));
      ok(trendLine(mk(3,i=>5))===null,'moins de 4 points');ok(trendLine(mk(5,i=>5-i*.1)).b<0,'amélioration → pente négative');eq(trendLine(mk(5,i=>5)).b,0,1e-9)});
    t('rappel de sauvegarde',()=>{
      const T='2026-10-23';ok(backupDue(T,null,null).never===true,'jamais exporté');ok(backupDue(T,'2026-10-01',null)===null,'récent');
      ok(backupDue(T,'2026-09-01',null).age===52,'ancien');ok(backupDue(T,null,'2026-10-30')===null,'reporté')});
    t('données : dates corrigées dans le jeu de départ',()=>{
      ok(D.races.find(r=>r.id==='t25-saintexpress').date==='2025-11-29');ok(D.races.find(r=>r.id==='t25-falaises-b').date==='2026-07-12')});

    t('classiques : clé de regroupement',()=>{
      ok(raceKey("Les Roses de l’Étang — Roller Coaster")===raceKey("Les Roses de l'Etang"),'apostrophes et accents');
      ok(raceKey('Le 20 des Collines')===raceKey('Le 20 des collines'),'casse');ok(raceKey('SaintéLyon — SaintExpress')===raceKey('SaintéLyon — relais à 4'),'format');
      ok(raceKey('Trail du Ventoux — L’Origine')!==raceKey('Trail du Bœuf à Mèze'),'courses différentes');ok(raceKey('')==='')});
    t('classiques : regroupement et écarts',()=>{
      const c=classics(),fal=c.find(x=>x.key==='trail des falaises');ok(fal&&fal.n===2,'Falaises ×2');
      const roses=c.filter(x=>x.key==="roses de l'etang");ok(roses.length===2&&roses.every(g=>g.n===2),'Roses : deux distances (12 et 21 km) = deux comparaisons séparées');
      ok(c.every(g=>g.n>=2&&g.eds.every((e,i,a)=>i===0||a[i-1].r.date<=e.r.date)),'≥2 éditions, ordre chronologique');
      const mk=(n,km,d)=>({id:'x'+n+km,name:'Trail Test'+(km>40?' — long':''),date:d,km,dplus:km*30,kind:'trail',status:'Finisher',result:'0'+Math.round(km/8)+':00:00'}),tc=classics([mk(1,25,'2023-05-01'),mk(2,27,'2024-05-01'),mk(3,50,'2023-06-01'),mk(4,54,'2024-06-01'),mk(5,80,'2024-07-01'),mk(6,56,'2025-06-01')]);
      ok(tc.length===2&&tc.every(g=>g.eds.every(e=>Math.abs(e.r.km-g.eds[0].r.km)<=KM_TOL)),'classiques : même nom ET distance à ± 5 km');ok(tc.every(g=>g.km>0),'distance de référence du classique');
      const m0=D.races[0].date.slice(0,7),sv=S.rcMon;S.rcMon=m0;const ch=raceCalHTML();S.rcMon=sv;
      ok(/rcal-g/.test(ch)&&racesFiltered().filter(r=>r.date.slice(0,7)===m0).every(r=>racesFiltered().filter(q=>q.date===r.date).length>3||ch.includes('data-id="'+r.id+'"')),'calendrier des courses : chaque course du mois a sa pastille');
      const e=fal.eds[1];ok(e.d!=null&&Math.abs(e.d-(e.eff-fal.eds[0].eff)/fal.eds[0].eff)<1e-12,'écart calculé vs édition précédente');ok(fal.eds[0].d===null,'première édition sans écart')});
    t('fiabilité : validation croisée sans fuite',()=>{
      const r=timed()[0];ok(calib(r,r.id).L.every(x=>x.r.id!==r.id),'la course testée est exclue');ok(calib(r).L.some(x=>x.r.id===r.id),'sans exclusion elle est incluse');
      const b=backtest();eq(b.n,timed().length);ok(isFinite(b.mae)&&b.mae>=0&&b.mae<.5,'erreur moyenne plausible : '+b.mae);ok(b.w5<=b.w10&&b.w10<=1,'parts cohérentes')});
    t('index UTMB : relevés',()=>{
      D.profile.utmbHist=[];ok(utmbNote(600,'2026-01-01')&&utmbNote(620,'2026-06-01'),'ajout');ok(utmbHist().length===2&&D.profile.utmb===620,'index courant = dernier relevé');
      utmbNote(630,'2026-06-01');ok(utmbHist().length===2&&utmbHist()[1].v===630,'même jour : remplacé');
      ok(!utmbNote(0)&&!utmbNote('abc')&&!utmbNote(600,'pas-une-date'),'valeurs invalides refusées');ok(utmbSummary().includes('630'))});
    t('fiche jour J : temps de passage',()=>{
      const r=race({startTime:'09:00'}),T=parseT('5h00'),rows=passageTable(r,T);
      ok(rows.length>=5,'plusieurs points');ok(rows.every((x,i)=>i===0||(x.t>rows[i-1].t&&x.km>rows[i-1].km&&x.dp>=rows[i-1].dp)),'croissant');
      const f=rows[rows.length-1];ok(f.finish&&f.km===42&&Math.abs(f.t-T)<1e-9,'arrivée = temps cible');eq(f.dp,1800,1e-9);ok(f.clock==='14:00','heure d\'arrivée '+f.clock);
      ok(rows.every(x=>x.lo<x.t&&x.t<x.hi),'fourchette autour du temps');ok(passageTable(race({km:0}),T).length===0&&passageTable(r,0).length===0,'entrées invalides');
      eq(passageTable(race({startTime:'22:00'}),T).pop().day,1);ok(passageTable(race({startTime:'22:00'}),T).pop().clock==='03:00','passage après minuit')});

    const synth=()=>{const pts=[];for(let i=0;i<=100;i++){const k=i/4;pts.push([k,k<=10?100+30*k:k<=15?400-60*(k-10):k<=25?100+30*(k-15):400])}return pts}; // 10 km +300 · 5 km −300 · 10 km +300
    t('sections : montées / descentes du profil',()=>{
      const sc=profSections(synth());ok(sc.length>=3,'au moins 3 sections');
      ok(sc[0].type==='montée'&&sc[1].type==='descente'&&sc[2].type==='montée',sc.map(x=>x.type).join(','));
      ok(Math.abs(sc[0].up-300)<=20,`D+ section 1 : ${sc[0].up}`);ok(Math.abs(sc[0].d-10)<=.6,`distance : ${sc[0].d}`);
      ok(profSections(null).length===0&&profSections([[0,1]]).length===0,'profils vides')});
    t('sections : le temps réparti = le temps cible',()=>{
      const T=300,r=sectionTimes(profSections(synth()),T);eq(r[r.length-1].cum,T,1e-6);ok(r.every(x=>x.t>0&&isFinite(x.pace)),'allures valides');
      ok(r[0].pace>r[1].pace,'la montée est plus lente que la descente')});
    t('analyse GPX : pentes, répartition et panneau',()=>{const prof=synth(),rc={id:'z',name:'Z',km:25,dplus:600,dminus:600,prof,kind:'trail',date:addD(today(),30),result:'',goal:''},A=gpxAnalysis(rc);
      eq(A.dist.reduce((a,b)=>a+b,0),25,1e-6);ok(A.gmax>2.9&&A.gmin<-5.9,'pentes extrêmes '+A.gmax+' / '+A.gmin);ok(A.dU>17&&A.dU<22,'distance en montée '+A.dU);
      const h=gpxPanel(rc);ok(h.includes('id="gp-svg"')&&h.includes('Montées marquantes')&&!/NaN|undefined/.test(h),'panneau sans NaN');ok(gBin(-20)===0&&gBin(0)===3&&gBin(9)===5&&gBin(30)===6,'classes de pente')});
    t('GPX : lecture, distance, D+ et profil',()=>{
      const pt=i=>`<trkpt lat="${(45+i*.001).toFixed(5)}" lon="6"><ele>${100+i*5}</ele><time>2026-05-02T08:${pad(i)}:00Z</time></trkpt>`,
        g=parseGPX(`<?xml version="1.0"?><gpx><trk><name>Test GPX</name><trkseg>${Array.from({length:40},(_,i)=>pt(i)).join('')}</trkseg></trk></gpx>`,'x.gpx');
      eq(g.km,39*.001*6371*Math.PI/180,.01);ok(g.dplus>150&&g.dplus<=195,'D+ '+g.dplus);ok(g.name==='Test GPX'&&g.date==='2026-05-02');
      ok(g.prof&&g.prof.length===161&&g.prof[0][0]===0,'profil 161 points');ok(g.trk&&g.trk.length===161&&g.trk[0].length===2,'trace GPS alignée sur le profil');ok(parseGPX('<gpx><trk><trkseg><trkpt lat="1" lon="1"/><trkpt lat="1.1" lon="1"/></trkseg></trk></gpx>','n.gpx').prof===null,'sans altitude → pas de profil')});
    t('saison : alerte quand deux courses sont trop rapprochées',()=>{
      const mk=(id,dt,km,dp,prio)=>({id,name:id,date:dt,km,dplus:dp,dminus:0,kind:'trail',status:'',result:'',prio});
      const a=mk('ultra',addD(today(),30),80,4000,'B'),b=mk('cible',addD(today(),40),30,800,'A'),c=mk('loin',addD(today(),130),30,800,'C');
      const y=b.date.slice(0,4),p=seasonPlan(y,[a,b,c]);const g=p.gaps.find(x=>x.b.id==='cible');
      ok(g&&g.short&&g.days===10&&g.need>=30,'écart court détecté');ok(p.alerts.some(x=>/cible/.test(x.txt)),'alerte générée');
      ok(!seasonPlan(c.date.slice(0,4),[a,b,c]).gaps.some(x=>x.b.id==='loin'&&x.short),"écart suffisant : pas d'alerte");
      ok(recoveryDays(a)>recoveryDays(b),'plus long = plus de récupération')});
    t('sauvegarde auto : contenu du fichier',()=>{const p=backupPayload();ok(p.app==='vertex'&&p.data.races.length===D.races.length&&!isNaN(Date.parse(p.exportedAt)));ok(typeof abStatus()==='string'&&typeof pwaStatus()==='string')});

    t('plan de ravitaillement : iso+ obligatoire, complément alterné',()=>{
      const P=fuelPlan(360);ok(P.F.water===500&&P.F.iso===500,'eau / iso+');eq(P.isoC,33);eq(P.comp,42);
      ok(P.ev.length>=6,'prises : '+P.ev.length);ok(Math.abs(P.planned/6-42)<=15,'complément ≈ 42 g/h : '+P.planned/6);
      ok(new Set(P.ev.map(e=>e.f.name)).size>=4,'alternance');ok(P.ev.every(e=>e.t<=345),'rien dans les 15 dernières min');
      ok(P.ev.filter(e=>/caf/i.test(e.f.name)).every(e=>e.t>=360*.55),'caféine en seconde moitié');ok(fuelPlan(40).ev.length===0,'course courte : rien')});
    t('GPX : temps réparti selon les pentes',()=>{
      const prof=[];for(let i=0;i<=100;i++){const k=i*.4;prof.push([k,k<=20?k*50:1000-(k-20)*50])}
      const r=race({km:40,dplus:1000,prof}),tc=trailCost(r);ok(tc&&Math.abs(tc.at(40)-1)<1e-9,'cumul = 1');
      ok(tc.at(20)>.6,'la montée prend plus de la moitié du temps : '+tc.at(20));eq(tc.dp(40),1000,15);ok(trailCost(race())===null,'sans GPX')});
    const L_=(...a)=>a.join('\n');
    t('plan IA : jours datés (Markdown, listes, sous-listes)',()=>{
      const d=parseAIPlan(L_('### Semaine 1','**Jour 1 — lundi 3 novembre**',"- Petit-déjeuner : flocons d'avoine, banane",'- Déjeuner : riz, poulet','Total : 2800 kcal','**Jour 2 — mardi 4 novembre**','Petit-déjeuner :','- pain','- confiture','- Dîner : pâtes'));
      eq(d.length,2);eq(d[0].items.length,2);ok(d[0].notes[0]==='Total : 2800 kcal'&&d[0].items[0].l==='Petit-déjeuner');
      ok(d[1].items.length===2&&d[1].items[0].sub.length===2&&d[1].items[1].l==='Dîner','groupe « Petit-déjeuner : » + liste');
      const p=resolvePlan(d,{raceDate:'2026-12-05'});ok(p.explicit&&p.first==='2026-11-03'&&p.last==='2026-11-04',p.first+' '+p.last)});
    t('plan IA : jours de semaine + « Semaine N » + date de début',()=>{
      const p=resolvePlan(parseAIPlan(L_('Semaine 1','Lundi : Repos','Mardi : Footing 45 min Z2','Semaine 2','Lundi : Fractionné 8x400')),{start:'2026-11-02'});
      ok(p.days.map(x=>x.date).join()==='2026-11-02,2026-11-03,2026-11-09',p.days.map(x=>x.date).join());ok(p.days[1].items[0].t.startsWith('Footing'))});
    t('plan IA : « J-N » et « Jour J » depuis la date de la course',()=>{
      const p=resolvePlan(parseAIPlan(L_('J-3 : Charge glucidique','- pâtes','J-2','- riz','Jour J : Course','- gel toutes les 20 min')),{raceDate:'2026-12-05'});
      ok(p.days.map(x=>x.date).join()==='2026-12-02,2026-12-03,2026-12-05',p.days.map(x=>x.date).join());ok(p.days[0].title==='Charge glucidique')});
    t('plan IA : « Jour N » depuis la date de début choisie',()=>{
      const p=resolvePlan(parseAIPlan(L_('Jour 1','- a','Jour 2','- b','Jour 3','- c')),{start:'2026-11-10'});ok(!p.explicit&&p.first==='2026-11-10'&&p.last==='2026-11-12')});
    t('plan IA : tableau Markdown (jours × repas)',()=>{
      const d=parseAIPlan(L_('| Jour | Petit-déj | Déjeuner |','|---|---|---|','| Lundi 3 novembre | flocons | riz |','| Mardi 4 novembre | pain | pâtes<br>fruit |'));
      eq(d.length,2);ok(d[0].items[0].l==='Petit-déj'&&d[0].items[0].t==='flocons'&&d[1].items[1].sub[0]==='fruit')});
    t('plan IA : texte sans jours → rien à suivre ; « 1.5 litres » n’est pas une date',()=>{
      ok(resolvePlan(parseAIPlan("Bonjour, voici quelques conseils.\nBois beaucoup d'eau."))===null,'texte libre');
      const d=parseAIPlan(L_('Jour 1',"1.5 litres d'eau par jour"));ok(d.length===1&&d[0].items.length===1,'pas de faux jour')});
    t('plan IA : suivi (cases cochées) et vues sans erreur',()=>{
      const txt=L_('### Semaine 1','**Jour 1 — lundi 3 novembre**','- Déjeuner : riz','- Dîner : pâtes','**Jour 2 — mardi 4 novembre**','- Déjeuner : quinoa');
      const p=resolvePlan(parseAIPlan(txt),{raceDate:'2026-12-05'});const K=sk('nutri');D.ai={resp:{[K]:txt},start:{},done:{[K]:{'2026-11-03|m1':1}}};
      const pr=apvProg('nutri',p.days);ok(pr.n===3&&pr.f===1,JSON.stringify(pr));
      const k=S.apv;S.apv={nutri:{v:'day',d:'2026-11-03',m:''}};
      for(const v of ['day','week','cal']){S.apv.nutri.v=v;const h=aiPlanView('nutri');ok(h.includes('apv-nutri')&&!/NaN|undefined/.test(h),v+' : '+h.slice(0,80))}
      S.apv=k});
    t('plan du coach : semaine avant la course et programme alimentés uniquement par le texte',()=>{
      const k0=S.sel;D.races.push({id:'tc',name:'Course coach',date:'2026-12-05',km:42,dplus:1800,kind:'trail',status:'',result:'',goal:''});S.sel='tc';
      try{const txt=L_('Semaine 1','Jour 1 — lundi 23 novembre 2026','- Séance : footing 45 min','Jour 2 — samedi 28 novembre 2026','- Petit-déjeuner : riz au lait','Jour 3 — vendredi 4 décembre 2026','- Dîner : pâtes','- Hydratation : 3 L');
        D.ai={resp:{[sk('nutri')]:txt,[sk('train')]:txt},start:{},done:{}};const r=D.races.find(x=>x.id==='tc');
        S.cwView={[sk('nutri')]:'week',[sk('train')]:'week'};S.cwSel={};S.cwSel[sk('train')]='2026-11-23';const n=coachSection('nutri',r),tr=coachSection('train',r);
        ok((n.match(/class="cw-c[ "]/g)||[]).length===8&&n.includes('J-7')&&n.includes('Veille')&&n.includes('pâtes')&&!n.includes('footing'),'nutrition : calendrier de 7 jours, jour choisi = veille');ok(!/undefined|NaN/.test(n+tr),'pas de undefined/NaN');
        ok((tr.match(/class="cw-c[ "]/g)||[]).length===7&&tr.includes('footing')&&tr.includes('Semaine 1')&&tr.includes('mealw')&&!/Autre/.test(n+tr),'entraînement : semaine de 7 jours rangée par sections, sans « Autre »');
        D.ai={resp:{},start:{},done:{}};ok(coachSection('train',r).includes('Aucun plan du coach'),'vide : invitation à coller le plan');
        D.ai={resp:{[sk('train')]:txt},start:{},done:{}};D.races.push({id:'tc2',name:'Autre',date:'2027-01-10',km:10,dplus:0,kind:'trail',status:'',result:'',goal:''});S.sel='tc2';
        ok(aiPlan('train')===null,'le plan d\'une course n\'apparaît pas pour une autre')
      }finally{S.sel=k0}});
    t('profil du coureur : bouton cliquable comme le site et Strava',()=>{
      const h=linkBtns('https://site.test','','https://profil.test/moi');ok(h.includes('href="https://profil.test/moi"')&&h.includes('Mon profil sur la course'));ok(!linkBtns('','','javascript:alert(1)').includes('href'),'liens non http refusés')});
  }finally{D=keep.D;BOOTED=keep.BOOTED}
  return{pass:out.filter(x=>x.ok).length,fail:out.filter(x=>!x.ok).length,results:out}}
function openSelfTests(){
  const r=runSelfTests();
  openModal(`<h2 class="cond">Auto-tests</h2><p class="sm ${r.fail?'':'mut'}" style="margin:8px 0">${r.fail?`⚠️ ${r.fail} test${r.fail>1?'s':''} en échec`:'✅ Tout est bon'} · ${r.pass}/${r.pass+r.fail} réussis. Ils s'exécutent sur une copie des données de départ, sans toucher aux tiennes.</p>
  <div class="tscroll"><table><tbody>${r.results.map(x=>`<tr><td>${x.ok?'✅':'❌'}</td><td>${esc(x.name)}${x.ok?'':`<br><span class="xs" style="color:var(--bad)">${esc(x.msg)}</span>`}</td></tr>`).join('')}</tbody></table></div>`)}

/* ============================ SAUVEGARDE AUTO & INSTALLATION ============================ */
// Sauvegarde automatique : à chaque enregistrement, le fichier choisi est réécrit (Chrome / Edge sur ordinateur et Android ; pas Safari / Firefox).
const AB={ok:typeof window.showSaveFilePicker==='function'&&typeof indexedDB!=='undefined',handle:null,perm:'none',last:null,err:'',t:null};
const backupPayload=()=>({app:'vertex',version:1,exportedAt:new Date().toISOString(),data:D});
function idb(mode,fn){return new Promise((ok,ko)=>{const q=indexedDB.open('vertex_fs',1);q.onupgradeneeded=()=>q.result.createObjectStore('h');q.onerror=()=>ko(q.error);
  q.onsuccess=()=>{const db=q.result,tx=db.transaction('h',mode),rq=fn(tx.objectStore('h'));tx.oncomplete=()=>{db.close();ok(rq&&rq.result)};tx.onerror=tx.onabort=()=>{db.close();ko(tx.error)}}})}
async function abInit(){if(!AB.ok)return;try{const h=await idb('readonly',st=>st.get('file'));if(h){AB.handle=h;AB.perm=await h.queryPermission({mode:'readwrite'});if(S.tab==='home'||S.tab==='profile')render()}}catch(e){}}
function abStatus(){
  if(!AB.ok)return `Sauvegarde automatique : indisponible sur ce navigateur (Chrome ou Edge sur ordinateur ou Android). Ailleurs, exporte régulièrement.`;
  if(!AB.handle)return `Sauvegarde automatique : désactivée. Choisis un fichier (de préférence dans un dossier synchronisé : Drive, iCloud, OneDrive) et il sera mis à jour à chaque modification.<div class="row" style="margin-top:8px"><button class="btn lime s" data-a="abChoose">🔄 Choisir le fichier</button></div>`;
  const ok=AB.perm==='granted';
  return `Sauvegarde automatique vers <b>${esc(AB.handle.name)}</b> : ${ok?(AB.last?`dernière écriture à ${pad(AB.last.getHours())}:${pad(AB.last.getMinutes())} ✅`:'active ✅'):'⚠️ autorisation à renouveler'}${AB.err?`<br><span style="color:var(--bad)">${esc(AB.err)}</span>`:''}<div class="row" style="margin-top:8px">${ok?'':'<button class="btn lime s" data-a="abReconnect">Reconnecter</button>'}<button class="btn ghost s" data-a="abChoose">Changer de fichier</button><button class="btn ghost s" data-a="abStop">Arrêter</button></div>`}
const refreshAB=()=>{const el=$('#ab');if(el)el.innerHTML=abStatus()};
async function abWrite(){
  if(!AB.handle||AB.perm!=='granted')return false;
  try{const w=await AB.handle.createWritable();await w.write(JSON.stringify(backupPayload(),null,2));await w.close();AB.last=new Date();AB.err='';LS.set('vertex_lastexport',today());return true}
  catch(e){if(e&&e.name==='NotAllowedError'){AB.perm='prompt';AB.err='Autorisation perdue : reconnecte le fichier.'}else AB.err='Écriture impossible ('+((e&&e.message)||e)+').';return false}
  finally{refreshAB()}}
function abSchedule(){if(!AB.handle||AB.perm!=='granted')return;clearTimeout(AB.t);AB.t=setTimeout(abWrite,3000)}
async function abChoose(){
  try{const h=await window.showSaveFilePicker({suggestedName:'vertex-sauvegarde.json',types:[{description:'Sauvegarde Vertex (JSON)',accept:{'application/json':['.json']}}]});
    AB.handle=h;AB.perm='granted';AB.err='';
    try{await idb('readwrite',st=>st.put(h,'file'))}catch(e){AB.err="Fichier choisi, mais le navigateur ne peut pas s'en souvenir après fermeture."}
    const ok=await abWrite();toast(ok?`Sauvegarde automatique activée : ${h.name}`:'Fichier choisi, mais écriture impossible.',!ok);render()}
  catch(e){if(!e||e.name!=='AbortError')toast('Impossible de choisir le fichier.',1)}}
async function abReconnect(){
  try{AB.perm=await AB.handle.requestPermission({mode:'readwrite'});if(AB.perm==='granted'){AB.err='';await abWrite();toast('Sauvegarde automatique reconnectée.')}}catch(e){toast('Autorisation refusée.',1)}render()}
async function abStop(){AB.handle=null;AB.perm='none';clearTimeout(AB.t);try{await idb('readwrite',st=>st.delete('file'))}catch(e){}toast('Sauvegarde automatique arrêtée (le fichier déjà écrit est conservé).');render()}
// Installation / hors ligne : nécessite la page hébergée en https avec sw.js et manifest.webmanifest à côté (impossible depuis un fichier local).
let INSTALL=null;
window.addEventListener('beforeinstallprompt',e=>{e.preventDefault();INSTALL=e;const el=$('#pwa');if(el)el.innerHTML=pwaStatus()});
window.addEventListener('appinstalled',()=>{INSTALL=null;const el=$('#pwa');if(el)el.innerHTML=pwaStatus()});
if('serviceWorker' in navigator&&/^https?:$/.test(location.protocol))navigator.serviceWorker.register('sw.js?p='+encodeURIComponent(location.pathname)).then(()=>{const el=$('#pwa');if(el)setTimeout(()=>{el.innerHTML=pwaStatus()},1500)}).catch(()=>{});
function pwaStatus(){
  const http=/^https?:$/.test(location.protocol),sw=!!(navigator.serviceWorker&&navigator.serviceWorker.controller),standalone=!!(window.matchMedia&&matchMedia('(display-mode: standalone)').matches);
  return `${standalone?'✅ Application installée.':sw?'✅ Fonctionne hors ligne.':http?"Hors ligne : sera actif au prochain chargement (sw.js doit être hébergé à côté de la page).":"Hors ligne : nécessite d'héberger la page en https avec sw.js et manifest.webmanifest à côté."}${INSTALL?`<div class="row" style="margin-top:8px"><button class="btn lime s" data-a="install">📲 Installer l'application</button></div>`:''}${!INSTALL&&!standalone&&/iphone|ipad/i.test(navigator.userAgent)?'<br><span class="xs">iPhone / iPad : Partager → « Sur l\'écran d\'accueil ».</span>':''}`}

/* ============================ RAPPEL DE SAUVEGARDE ============================ */
const BACKUP_DAYS=30;
// Les données vivent uniquement dans ce navigateur : on rappelle d'exporter une sauvegarde si aucune n'existe ou si elle date de 30 jours ou plus.
function backupDue(t=today(),last=LS.get('vertex_lastexport'),snooze=LS.get('vertex_snooze')){
  if(!D.races.length)return null;
  if(snooze&&snooze>t)return null;
  if(!last)return{never:true,age:null};
  const age=dBetween(last,t);return age>=BACKUP_DAYS?{never:false,age}:null}
function backupNote(){
  if(AB.handle&&AB.perm==='granted')return '';   // sauvegarde automatique active : pas de rappel
  if(AB.handle)return `<div class="note" style="margin-top:14px">💾 La sauvegarde automatique vers « ${esc(AB.handle.name)} » attend ton autorisation après la réouverture du navigateur.<div class="row" style="margin-top:8px"><button class="btn lime s" data-a="abReconnect">Reconnecter</button></div></div>`;
  const b=backupDue();if(!b)return '';
  return `<div class="note" style="margin-top:14px">💾 ${b.never?"Tu n'as encore jamais exporté de sauvegarde.":`Ta dernière sauvegarde date de ${b.age} jours.`} Tes courses et ton profil ne sont enregistrés que dans ce navigateur : vider ses données les efface.<div class="row" style="margin-top:8px"><button class="btn lime s" data-a="export">⬇️ Exporter maintenant</button>${AB.ok?'<button class="btn ghost s" data-a="abChoose">🔄 Sauvegarde auto</button>':''}<button class="btn ghost s" data-a="snoozeBackup">Plus tard (7 jours)</button></div></div>`}

/* ============================ PROFIL D'ALTITUDE & SECTIONS ============================ */
// Découpe le profil en montées / descentes / plats : un changement de sens compte à partir d'un écart d'altitude significatif (hystérésis).
function profSections(prof){
  if(!Array.isArray(prof)||prof.length<4)return [];
  const ys=prof.map(p=>p[1]),range=Math.max(...ys)-Math.min(...ys);
  const turns=th=>{const idx=[0];let dir=0,ext=0;
    for(let i=1;i<prof.length;i++){const y=prof[i][1];
      if(dir===0){const b=prof[0][1];if(y-b>=th){dir=1;ext=i}else if(b-y>=th){dir=-1;ext=i}}
      else if(dir===1){if(y>=prof[ext][1])ext=i;else if(prof[ext][1]-y>=th){idx.push(ext);dir=-1;ext=i}}
      else{if(y<=prof[ext][1])ext=i;else if(y-prof[ext][1]>=th){idx.push(ext);dir=1;ext=i}}}
    if(dir&&ext!==idx[idx.length-1])idx.push(ext);
    if(idx[idx.length-1]!==prof.length-1)idx.push(prof.length-1);
    return idx};
  let th=Math.max(15,Math.min(150,range*.06)),idx=turns(th);
  while(idx.length>17&&th<2000){th*=1.35;idx=turns(th)}   // pas plus de 16 sections : reste lisible
  return idx.slice(1).map((b,k)=>{const a=idx[k];let up=0,dn=0;
    for(let i=a+1;i<=b;i++){const d=prof[i][1]-prof[i-1][1];if(d>0)up+=d;else dn-=d}
    const d=prof[b][0]-prof[a][0],net=prof[b][1]-prof[a][1],grade=d>0?net/(d*1000)*100:0;
    return{a:prof[a][0],b:prof[b][0],d,up:Math.round(up),dn:Math.round(dn),net:Math.round(net),grade,type:grade>=3?'montée':grade<=-3?'descente':'plat'}}).filter(x=>x.d>0)}
// Répartit le temps cible T selon le coût de chaque section : km + D+/100 (même base que le reste du site), descentes un peu moins coûteuses (jusqu'à −25 %).
function sectionTimes(secs,T,tc){
  const cost=secs.map(x=>tc?Math.max(1e-9,tc.at(x.b)-tc.at(x.a)):x.d*(x.type==='descente'?1-Math.min(.25,Math.abs(x.grade)/100*2.5):1)+x.up/100),tot=cost.reduce((a,b)=>a+b,0);let cum=0;
  return secs.map((x,i)=>{const t=tot>0?T*cost[i]/tot:0;cum+=t;return{...x,t,cum,pace:x.d>0?t/x.d:0}})}
const SEC_COL={'montée':'var(--acc)','descente':'var(--ice)','plat':'var(--mut)'},SEC_ICO={'montée':'▲','descente':'▼','plat':'▶'};
function secTable(secs){return `<div class="tscroll"><table class="nw"><thead><tr><th>#</th><th>Section</th><th>Km</th><th>D+ / D−</th><th>Pente</th><th>Temps</th><th>Allure</th><th>Cumul</th></tr></thead><tbody>${secs.map((x,i)=>`<tr><td>${i+1}</td><td style="color:${SEC_COL[x.type]};font-weight:700">${SEC_ICO[x.type]} ${x.type}</td><td>${fn(x.a,1)} → ${fn(x.b,1)}</td><td>${x.type==='descente'?'−'+x.dn:x.type==='montée'?'+'+x.up:`+${x.up} / −${x.dn}`} m</td><td>${x.grade>0?'+':''}${fn(x.grade,1)} %</td><td><b>${fmtT(x.t)}</b></td><td>${pace(x.pace)}/km</td><td>${fmtT(x.cum)}</td></tr>`).join('')}</tbody></table></div>`}
function profChart(prof,secs,compact){
  const nr=window.innerWidth<600,W=nr?340:640,H=nr?190:compact?170:200,L=52,R=10,T=14,B=26,iw=W-L-R,ih=H-T-B,x1=prof[prof.length-1][0]||1,ys=prof.map(p=>p[1]),lo=Math.min(...ys),hi=Math.max(...ys),pd=Math.max(10,(hi-lo)*.08),y0=lo-pd,y1=hi+pd;
  const X=k=>L+k/x1*iw,Y=m=>T+(y1-m)/(y1-y0)*ih,f=v=>v.toFixed(1);
  const line=prof.map(p=>`${f(X(p[0]))},${f(Y(p[1]))}`).join(' ');
  const bands=secs.map((x,i)=>{const w=X(x.b)-X(x.a);return `<g><title>${i+1}. ${x.type} · ${fn(x.d,1)} km · +${x.up} / −${x.dn} m${x.t?` · ${fmtT(x.t)}`:''}</title><rect x="${f(X(x.a))}" y="${T}" width="${f(w)}" height="${ih}" fill="${SEC_COL[x.type]}" opacity=".17"/>${w>16?`<text x="${f(X(x.a)+w/2)}" y="${T+11}" text-anchor="middle" style="font-size:11px;font-weight:800">${i+1}</text>`:''}</g>`}).join('');
  const ky=x1<=25?5:x1<=60?10:x1<=120?20:25,kt=[];for(let k=0;k<=x1+.01;k+=ky)kt.push(k);
  const yt=[0,1,2].map(i=>lo+(hi-lo)*i/2);
  return `<div class="chartbox"><svg class="chart" viewBox="0 0 ${W} ${H}" style="min-width:0" role="img" aria-label="Profil d'altitude de ${fn(x1,1)} km, de ${Math.round(lo)} à ${Math.round(hi)} m, ${secs.length} sections">
   ${yt.map(m=>`<line class="gl" x1="${L}" x2="${W-R}" y1="${f(Y(m))}" y2="${f(Y(m))}"/><text x="${L-6}" y="${f(Y(m)+4)}" text-anchor="end">${Math.round(m)} m</text>`).join('')}
   ${bands}<polygon points="${f(X(0))},${f(Y(y0))} ${line} ${f(X(x1))},${f(Y(y0))}" fill="var(--card2)" opacity=".85"/><polyline points="${line}" fill="none" stroke="var(--ink)" stroke-width="2" stroke-linejoin="round"/>
   ${kt.map(k=>`<text x="${f(X(k))}" y="${H-8}" text-anchor="middle">${fn(k,0)}${k===kt[kt.length-1]?' km':''}</text>`).join('')}</svg></div>`}
function profileBlock(r,T0,compact){
  if(!r.prof)return compact?'':`<div class="card"><h2 class="cond">Profil d'altitude</h2><p class="sm mut">Ajoute le GPX de la course : tu verras le profil, les montées et descentes, et un temps cible pour chaque section.</p><div class="row" style="margin-top:8px"><button class="btn ghost s" data-a="gpxFor" data-id="${r.id}">📈 Ajouter le GPX</button></div></div>`;
  if(!compact)return gpxPanel(r);
  const res=parseT(r.result),T=T0||res||parseT(r.goal)||scenarios(r).real,secs=sectionTimes(profSections(r.prof),T,trailCost(r)),gk=r.prof[r.prof.length-1][0];
  const gap=r.km>0&&Math.abs(gk/r.km-1)>.03?`<p class="xs mut" style="margin-top:6px">⚠️ Le GPX mesure ${fn(gk,1)} km, la course est enregistrée à ${fn(r.km,1)} km : les sections suivent le GPX.</p>`:'';
  const tbl=secTable(secs);
  const note=`<p class="xs mut" style="margin-top:6px">Temps cible ${fmtT(T)} (${res?'ton chrono réel':parseT(r.goal)?'ton objectif':'scénario réalisable'}) réparti selon la pente de chaque portion du GPX (descentes moins coûteuses, dérive de fatigue incluse). Estimation : ajuste au terrain réel.</p>`;
  if(compact)return `<h3 class="cond" style="margin:16px 0 6px">Profil et sections</h3>${profChart(r.prof,secs,true)}${tbl}${note}`;
  return `<details class="card hist" open><summary><h2 class="cond" style="display:inline-block;margin:0">Infos GPX</h2><span class="xs mut"> · ${fn(gk,1)} km · réduire / développer</span></summary><div style="margin-top:12px">${gpxStats(r)}</div><div style="margin-top:12px">${profChart(r.prof,secs)}</div><details class="hist" style="padding:10px 0 0" open><summary><b class="cond">Sections</b></summary><div style="margin-top:8px">${tbl}</div></details>${note}${gap}<div class="row noprint" style="margin-top:8px"><button class="btn ghost s" data-a="gpxFor" data-id="${r.id}">📈 Remplacer le GPX</button><button class="btn red s" data-a="profDel" data-id="${r.id}">Retirer le profil</button></div></details>`}

/* ============================ MA SAISON (A / B / C) ============================ */
const PRIO={A:'Objectif principal',B:'Objectif secondaire',C:'Préparation / plaisir'};
const PRIO_COL={A:'var(--acc)',B:'var(--ice)',C:'var(--mut)','':'var(--yel)'};
// Repères de récupération et d'affûtage selon le coût de la course (km-effort). Indicatifs : à ajuster selon ton ressenti.
const recoveryDays=r=>{const E=effKm(r);return E<20?3:E<35?6:E<55?12:E<85?21:30};
const taperDays=r=>{const E=effKm(r);return E<20?2:E<35?5:E<55?10:E<85?14:21};
function seasonPlan(y,list=D.races,t=today()){
  const all=list.filter(r=>r.status!=='DNS').sort(byDateAsc),inY=r=>r.date.slice(0,4)===String(y),gaps=[];
  for(let i=1;i<all.length;i++){const a=all[i-1],b=all[i];if(!inY(b))continue;
    const days=dBetween(a.date,b.date),need=recoveryDays(a)+(b.prio==='A'?Math.ceil(taperDays(b)/2):0);
    gaps.push({a,b,days,need,short:days<need,upcoming:b.date>=t,high:days<need*.6})}
  const rs=all.filter(inY),A=rs.filter(r=>r.prio==='A'),up=rs.filter(r=>r.date>=t),alerts=[];
  gaps.filter(g=>g.short&&g.upcoming).forEach(g=>alerts.push({high:g.high,txt:`${g.a.name} → ${g.b.name} : seulement ${g.days} j d'écart (récupération conseillée : ${g.need} j). ${g.b.prio==='A'?"Ton objectif A risque d'en pâtir : cours la première en sortie tranquille ou saute-la.":g.a.prio==='A'?"Laisse ton corps récupérer de l'objectif A avant de repartir à fond.":'Cours l’une des deux en sortie tranquille.'}`}));
  for(let i=1;i<A.length;i++){const d=dBetween(A[i-1].date,A[i].date);if(d<56&&A[i].date>=t)alerts.push({high:false,txt:`${A[i-1].name} et ${A[i].name} sont deux objectifs A à ${d} j d'intervalle : il en faut ~8 semaines pour préparer chacun à fond.`})}
  if(A.length>2)alerts.push({high:false,txt:`${A.length} objectifs A cette année : au-delà de 2, la préparation devient difficile. Passe certains en B.`});
  if(up.length&&!A.length)alerts.push({high:false,txt:`Aucun objectif A défini pour ${y} : choisis ta course principale pour orienter la préparation.`});
  return{y:String(y),rs,gaps,alerts,count:{A:A.length,B:rs.filter(r=>r.prio==='B').length,C:rs.filter(r=>r.prio==='C').length,X:rs.filter(r=>!r.prio).length}}}
function seasonSummary(){const p=seasonPlan(today().slice(0,4)),n=p.alerts.length;
  return `${p.count.A} objectif${p.count.A>1?'s':''} A · ${p.rs.length} course${p.rs.length>1?'s':''} en ${p.y}${n?` · ⚠️ ${n} alerte${n>1?'s':''}`:''}`}
function openSeasonPlan(y){
  const cy=+today().slice(0,4),ys=[...new Set([cy,cy+1,...D.races.map(r=>+r.date.slice(0,4))])].sort(),Y=String(y||S.spY||cy);S.spY=Y;
  const p=seasonPlan(Y),leap=(+Y%4===0&&+Y%100!==0)||+Y%400===0,nd=leap?366:365,t=today();
  const W=window.innerWidth<600?340:640,H=170,L=26,R=8,TT=14,lanes=['A','B','C',''],ih=H-TT-22,lh=ih/4,X=d=>L+d/nd*(W-L-R),LY=k=>TT+lh*(lanes.indexOf(k)+.5);
  const mo=Array.from({length:12},(_,i)=>{const d=dBetween(`${Y}-01-01`,`${Y}-${pad(i+1)}-01`);return `<line class="gl" x1="${X(d).toFixed(1)}" x2="${X(d).toFixed(1)}" y1="${TT}" y2="${H-22}"/><text x="${(X(d)+(X(d+30)-X(d))/2).toFixed(1)}" y="${H-6}" text-anchor="middle">${'JFMAMJJASOND'[i]}</text>`}).join('');
  const bands=p.gaps.filter(g=>g.short&&g.upcoming&&g.a.date.slice(0,4)===Y).map(g=>{const a=dBetween(`${Y}-01-01`,g.a.date),b=dBetween(`${Y}-01-01`,g.b.date);return `<rect x="${X(a).toFixed(1)}" y="${TT}" width="${Math.max(3,X(b)-X(a)).toFixed(1)}" height="${ih}" fill="var(--bad)" opacity=".18"><title>${esc(g.a.name)} → ${esc(g.b.name)} : ${g.days} j (conseillé ${g.need} j)</title></rect>`}).join('');
  const dots=p.rs.map(r=>{const d=dBetween(`${Y}-01-01`,r.date),past=r.date<t,k=r.prio||'';return `<g class="pt" data-a="race" data-id="${r.id}" tabindex="0" role="button" aria-label="${esc(r.name)}, ${shortD(r.date)}, ${k?'objectif '+k:'priorité non définie'}"><title>${esc(r.name)} · ${shortD(r.date)}${k?' · '+k:''}</title><circle cx="${X(d).toFixed(1)}" cy="${LY(k).toFixed(1)}" r="${past?5:7}" fill="${past?'none':PRIO_COL[k]}" stroke="${PRIO_COL[k]}" stroke-width="2.5" opacity="${past?.75:1}"/></g>`}).join('');
  const todayX=t.slice(0,4)===Y?`<line x1="${X(dBetween(`${Y}-01-01`,t)).toFixed(1)}" x2="${X(dBetween(`${Y}-01-01`,t)).toFixed(1)}" y1="${TT-4}" y2="${H-22}" stroke="var(--acc2)" stroke-width="2" stroke-dasharray="4 3"><title>Aujourd'hui</title></line>`:'';
  const lab=lanes.map(k=>`<text x="${L-8}" y="${(LY(k)+4).toFixed(1)}" text-anchor="end" style="font-weight:800;fill:${PRIO_COL[k]}">${k||'?'}</text>`).join('');
  openModal(`<h2 class="cond">Ma saison ${Y}</h2>
   <div class="row" style="margin:8px 0;flex-wrap:wrap">${ys.map(v=>`<button class="btn ${String(v)===Y?'':'ghost'} s" data-a="spYear" data-y="${v}">${v}</button>`).join('')}</div>
   <div class="kv" style="margin:10px 0"><div><b>${p.count.A}</b><span>objectif${p.count.A>1?'s':''} A</span></div><div><b>${p.count.B}</b><span>B</span></div><div><b>${p.count.C}</b><span>C</span></div><div><b>${p.rs.length}</b><span>course${p.rs.length>1?'s':''} au total</span></div></div>
   ${p.alerts.length?p.alerts.map(a=>`<div class="note"${a.high?' style="border-color:var(--bad);background:rgba(255,107,107,.12)"':''}>⚠️ ${esc(a.txt)}</div>`).join(''):(p.rs.length?'<div class="note good">✅ Aucune alerte : tes courses sont bien espacées.</div>':'')}
   <div class="chartbox"><svg class="chart" viewBox="0 0 ${W} ${H}" style="min-width:0" role="group" aria-label="Calendrier des courses ${Y} par priorité">${mo}${bands}${lab}${todayX}${dots}</svg></div>
   <p class="xs mut" style="margin:4px 0 12px">Point plein : à venir · contour : déjà courue · bande rouge : écart trop court avant une course à venir · tirets verts : aujourd'hui.</p>
   <div class="tscroll"><table><thead><tr><th>Date</th><th>Course</th><th>Priorité</th><th>Récup.</th></tr></thead><tbody>${p.rs.map(r=>`<tr><td>${shortD(r.date)}</td><td><button data-a="race" data-id="${r.id}" style="text-align:left;text-decoration:underline">${esc(r.name)}</button><br><span class="xs mut">${fn(r.km)} km · +${fn(r.dplus,0)} m</span></td><td><select data-c="prio" data-id="${r.id}" aria-label="Priorité de ${esc(r.name)}">${['','A','B','C'].map(k=>`<option value="${k}" ${(r.prio||'')===k?'selected':''}>${k?k+' · '+PRIO[k]:'—'}</option>`).join('')}</select></td><td>${recoveryDays(r)} j</td></tr>`).join('')||'<tr><td colspan="4" class="mut">Aucune course cette année.</td></tr>'}</tbody></table></div>
   <p class="xs mut" style="margin-top:8px">Récupération conseillée avant la course suivante : 3 j (court) à 30 j (ultra), +½ affûtage si la suivante est un objectif A. Ce sont des repères, pas une règle.</p>`)}

/* ============================ ACCUEIL ============================ */
/* Courbes de niveau générées (relief fictif, 800×440) : réutilisées par le hero et par le fond de page. */
const TOPO={minor:"M61 0 57 5 52 10 45 15 40 19 35 22 30 25 23 30 15 35 10 38 5 41M147 0 141 4 136 8 131 11 125 15 118 20 111 25 106 29 101 33 96 37 91 41 84 46 79 51 73 56 68 61 63 66 58 71 53 76 48 81 43 86 37 91 30 96 25 100 20 103 14 106 6 111 0 114M248 0 244 5 241 10 242 18 252 18 258 15 267 11 272 9 279 5 287 1M428 0 423 4 418 8 413 12 408 17 403 21 397 27 394 35 403 37 410 35 418 33 423 30 433 26 438 23 444 20 453 15 458 12 463 9 470 5 477 0M684 0 681 5 679 10 682 15 689 19 694 20 704 24 709 26 719 28 730 29 740 27 745 25 755 21 760 19 766 15 775 10 780 7 785 4 791 0M0 19 7 15 15 12 20 9 30 5 35 3 43 0M800 33 795 36 788 40 780 46 775 49 770 53 765 58 760 65 760 71 764 76 770 80 775 83 780 88 784 96 783 106 785 112 795 111 800 108M0 81 7 76 14 71 20 67 25 62 30 58 35 54 40 49 45 43 50 37 55 31 60 25 63 20 67 15 72 10 78 5 86 0M0 145 12 137 25 127 35 118 45 109 55 99 65 91 78 81 91 72 101 65 115 56 126 48 138 40 151 31 161 24 172 15 185 5M800 386 791 389 785 392 780 395 770 400 765 402 760 405 752 410 745 414 740 417 735 420 727 425 720 430 714 434 709 437M23 440 28 435 33 430 30 424 24 425 15 428 8 430 0 434M225 440 229 435 232 430 231 423 221 424 216 427 209 430 201 434 196 437M676 440 680 435 684 425 684 423 679 419 674 420 664 424 659 426 651 430 644 434 639 437 634 440M764 440 770 436 775 432 780 429 785 425 792 420 798 415M129 0 124 5 117 10 111 15 106 18 101 22 96 25 88 30 81 34 75 36 75 32 80 25 84 20 90 15 96 10 101 7 106 4 113 0M235 0 231 5 226 13 223 20 220 25 217 35 226 39 235 35 242 32 247 30 255 25 262 22 267 19 274 15 282 11 287 9 295 5 302 2M328 0 327 7 323 15 320 20 317 25 317 33 327 32 332 30 342 26 347 23 352 20 359 15 366 10 372 5 377 2M414 0 408 4 403 8 397 12 392 16 387 20 381 25 376 30 372 35 367 44 366 51 372 56 372 56 382 54 392 51 397 49 407 46 413 43 418 40 428 36 433 33 438 30 448 25 453 23 458 20 466 15 473 11 478 8 483 5 491 0M556 0 563 5 569 7 579 7 588 5 594 3 602 0M659 0 652 15 657 30 669 37 688 40 704 45 719 50 725 59 725 74 734 86 745 95 746 111 743 126 755 136 770 139 790 137M800 21 793 25 785 29 780 31 770 35 770 27 775 22 780 18 785 14 790 10 797 5M0 92 5 89 10 86 18 81 25 77 30 74 30 79 25 84 20 89 15 93 10 96 2 101M0 153 11 147 25 138 35 131 46 121 56 111 66 101 77 91 89 81 101 72 111 64 123 56 136 47 146 40 160 30 171 23 182 15 196 5M800 327 795 331 790 334 783 339 775 344 770 348 765 351 760 354 753 359 745 364 740 368 735 371 729 374 720 379 714 383 709 385 702 389 694 394 689 396 684 400 676 405 669 409 664 412 659 415 653 420 645 425 639 429 634 432 629 435 622 440M783 369 790 368 797 369 792 374 785 379 780 382 775 386 769 389 761 394 755 398 750 401 743 405 735 409 730 411 719 410 719 410 725 401 730 396 735 391 740 388 745 384 755 380 760 377 768 374 775 372 783 369M53 440 57 435 62 430 67 425 72 420 75 415 76 405 70 403 60 402 50 404 45 405 35 407 25 410 20 411 10 414 5 416M140 440 136 435 131 428 121 427 115 430 106 434 101 437 95 440M244 440 247 435 252 426 254 420 257 412 257 405 252 401 242 404 236 406 229 410 221 414 216 416 210 420 201 425 196 427 191 430 181 435 176 437 170 440M577 440 589 431 599 424 614 415 624 410 639 402 653 394 664 388 676 379 685 369 674 363 659 368 646 374 634 380 619 388 606 394 594 401 579 409 569 416 556 425 543 435M775 440 780 437 785 433 790 430 799 425M172 35 181 32 187 35 185 40 181 47 176 52 171 57 166 62 161 66 154 71 147 76 141 79 136 82 128 86 121 89 114 91 106 91 105 86 109 81 114 76 119 71 125 66 131 62 136 58 141 54 146 51 154 46 161 41 166 39 172 35M413 70 408 72 403 76 397 81 391 86 387 91 382 97 378 106 387 110 397 106 403 103 408 100 414 96 420 91 426 86 431 81 434 76 433 71 423 68 413 70M433 141 428 142 418 146 413 149 408 152 400 157 393 162 387 166 382 170 377 175 374 182 379 182 387 179 393 177 403 172 408 169 413 166 419 162 425 157 430 152 434 147 433 141M800 243 790 254 780 263 769 273 759 283 749 293 739 303 727 314 714 323 704 329 689 338 679 344 664 352 649 359 638 364 624 370 607 369 614 359 624 348 634 339 645 329 656 319 664 309 659 298 644 303 632 309 619 315 605 324 594 332 584 340 574 350 564 360 553 369 542 379 528 389 518 396 504 405 493 410 478 417 463 422 448 425 433 420 428 410 416 415 403 421 387 427 372 432 352 435 355 420 364 410 373 400 382 385 377 377 362 381 347 388 332 394 321 400 307 405 288 405 292 388 301 374 309 364 318 354 322 343 307 344 292 349 277 356 262 364 252 370 239 379 226 388 216 395 212 389 225 379 236 369 244 359 231 351 211 354 196 356 176 357 171 344 181 337 195 329 206 321 218 314 231 304 242 296 252 287 262 277 271 263 257 264 242 272 231 278 216 288 206 295 195 303 184 314 175 324 166 337 157 349 146 355 131 362 116 368 101 372 86 376 65 379 55 379 45 373 55 361 65 352 75 343 81 329 60 334 45 336 30 332 20 319 10 313M553 257 548 258 540 263 533 268 528 272 528 275 538 273 543 270 548 268 554 263 559 258 553 257M0 279 8 268 16 258 27 248 40 238 50 231 63 223 75 215 87 207 101 198 111 190 121 182 131 172 141 160 147 147 131 147 119 152 106 158 91 165 75 171 72 162 81 152 94 142 106 134 118 126 131 119 146 112 157 106 171 100 186 93 201 86 213 81 231 76 247 74 262 71 281 66 297 62 312 60 324 66 320 81 312 93 317 101 330 96 342 91 357 85 372 79 387 74 403 69 418 63 428 55 442 46 453 39 468 31 479 25 493 20 510 20 518 32 517 46 523 61 538 56 553 49 569 42 584 35 599 31 610 30 624 39 632 51 639 63 652 71 664 76 676 86 689 96 699 106 700 121 694 132 684 145 678 157 694 159 714 157 735 161 745 169 750 182 752 202 758 217 770 226 785 228M800 309 794 314 787 319 780 323 775 326 770 329 760 334 755 335 745 334 744 329 747 324 751 319 756 314 762 309 770 304 775 301 780 298 790 294 795 292M523 334 518 336 513 339 505 344 498 348 493 352 488 355 483 359 477 364 471 369 465 374 460 379 456 384 452 389 458 389 463 386 468 384 476 379 483 375 488 372 493 369 500 364 507 359 513 355 518 350 523 346 528 340 532 334 523 334M579 46 599 41 614 47 621 61 624 80 634 86 654 91 664 96 679 106 686 116 682 131 674 142 664 154 654 166 647 177 664 178 679 173 694 169 714 168 726 177 722 192 714 204 714 218 730 223 741 233 755 239 771 243 770 258 760 269 750 278 740 288 729 298 718 309 706 319 694 327 684 334 669 342 655 349 639 353 644 341 654 331 664 321 674 311 684 300 690 288 679 283 664 287 649 293 638 298 624 306 610 314 599 320 586 329 574 338 564 347 553 358 543 368 533 377 523 385 508 394 498 400 483 406 465 405 473 394 485 384 498 375 508 368 522 359 533 351 543 343 553 334 564 319 564 305 547 309 533 316 521 324 508 333 498 340 485 349 473 358 463 365 451 374 438 384 428 392 417 400 403 408 388 415 377 415 382 403 392 389 399 379 404 364 387 364 374 369 362 375 347 382 332 388 317 394 307 394 308 379 317 367 327 357 337 348 347 338 357 328 347 321 332 325 315 329 297 330 282 327 267 329 250 334 231 339 216 340 211 331 221 321 231 312 242 303 254 293 265 283 275 273 285 263 293 253 302 238 292 237 281 243 267 251 254 258 242 266 230 273 216 282 206 288 192 298 181 306 171 314 160 324 148 334 136 343 126 349 111 356 96 359 91 353 101 340 110 329 118 319 126 304 121 296 106 302 92 309 81 314 65 319 49 319 50 303 60 293 73 283 86 275 98 268 111 261 126 254 138 248 151 239 158 228 151 223 136 229 121 236 106 243 94 248 81 254 65 260 50 265 33 263 40 251 50 241 61 233 74 223 86 215 96 207 109 197 121 188 131 179 141 170 151 159 161 147 168 137 176 126 186 116 200 106 211 99 226 92 240 86 254 81 269 76 287 72 302 71 307 78 300 91 291 101 281 111 270 121 260 131 251 142 262 141 277 133 290 126 302 120 317 113 331 106 347 101 357 106 356 126 372 127 387 121 397 116 413 107 423 101 438 92 448 86 463 77 473 76 482 91 493 88 507 81 518 75 533 67 545 61 558 54 574 47M453 116 443 121 428 130 417 137 403 146 392 153 379 162 367 171 357 179 347 187 337 198 327 212 333 212 347 206 362 200 377 193 389 187 403 180 417 172 428 165 438 156 448 146 458 131 463 119 453 116M508 201 503 203 493 207 488 209 481 212 473 217 468 221 463 226 458 232 454 238 451 243 448 249 445 258 453 260 458 258 468 253 473 250 478 247 484 243 491 238 498 233 503 228 508 224 513 219 518 214 523 207 523 202 518 200 508 201M423 212 418 215 411 217 403 222 397 226 392 229 387 233 380 238 373 243 367 247 362 252 357 257 352 262 352 267 362 265 367 262 376 258 382 255 387 252 395 248 403 243 408 240 413 237 419 233 426 228 431 223 435 217 433 211 423 212M579 232 567 238 553 245 540 253 528 260 517 268 503 278 493 286 484 298 501 298 518 293 533 288 545 283 558 276 569 268 579 258 589 244 589 229M571 61 589 59 598 71 593 86 584 101 584 115 604 113 624 112 644 115 654 121 654 142 647 152 638 162 628 172 617 182 607 192 595 202 584 211 574 219 560 228 548 235 535 243 523 250 508 258 498 263 483 268 488 259 498 250 508 240 518 231 528 222 539 212 548 201 555 187 543 177 523 179 503 178 494 167 478 166 463 167 463 154 470 142 478 129 487 116 496 106 508 96 518 88 529 81 543 73 557 66 571 61M264 91 274 96 267 107 257 117 246 126 234 137 222 147 211 155 201 163 190 172 177 182 166 190 156 197 141 206 129 212 116 218 111 212 121 202 132 192 143 182 154 172 164 162 173 152 182 142 192 131 203 121 216 112 226 106 242 98 257 93M297 137 317 132 322 142 317 157 309 172 305 187 299 202 292 212 282 223 271 233 258 243 247 250 236 258 221 267 211 273 196 282 182 288 174 283 181 272 191 262 202 253 215 243 226 234 236 226 247 217 252 207 236 208 219 207 216 194 226 182 236 173 247 166 260 157 272 150 286 142 297 137M673 192 679 191 687 192 684 202 680 207 674 212 669 216 664 220 659 223 652 228 644 231 639 233 631 233 631 223 635 217 639 212 645 207 652 202 659 198 664 196 673 192M381 207 387 206 387 211 382 216 377 221 372 225 367 229 362 233 356 238 349 243 342 247 337 251 332 254 326 258 318 263 312 265 312 260 317 253 321 248 325 243 330 238 336 233 342 228 347 225 352 221 359 217 367 213 372 211 381 207M379 278 387 275 387 279 381 283 372 285 372 283 379 278M406 319 413 316 420 319 417 324 412 329 406 334 400 339 392 344 387 347 382 350 375 354 367 358 362 360 352 364 352 355 357 350 362 346 367 342 372 339 380 334 387 329 392 326 397 323 406 319M463 339 468 337 468 340 463 344 457 344 463 339M558 71 574 67 587 76 580 91 572 101 562 111 551 121 538 131 528 137 513 143 498 147 483 145 486 131 493 119 503 107 513 98 523 90 538 81 548 75M240 106 255 106 247 118 236 127 225 137 212 147 201 154 190 162 176 170 171 167 179 157 187 147 196 136 207 126 220 116 231 110M594 126 614 124 634 126 643 137 636 152 627 162 617 172 606 182 595 192 584 201 574 209 561 217 548 225 546 217 555 207 564 197 571 182 564 167 548 164 538 157 547 147 558 140 574 133 589 128M293 147 302 146 303 152 301 157 297 163 292 168 287 173 281 177 273 182 267 185 262 188 252 191 247 192 238 192 236 187 239 182 243 177 249 172 256 167 262 163 267 160 272 156 280 152 287 149 293 147M545 91 553 90 554 96 549 101 543 106 538 109 533 112 523 114 523 107 528 102 533 98 538 94 545 91",major:"M161 3 156 5 147 10 141 14 136 17 130 20 123 25 116 30 111 34 106 38 101 43 96 48 91 53 86 61 86 61 93 61 101 57 106 54 112 51 121 46 126 42 131 38 136 35 142 30 149 25 155 20 161 15 166 10 170 5 161 3M736 0 734 5 736 10 745 12 755 10 760 9 768 5 775 2M0 71 5 67 10 62 15 57 20 51 20 51 10 50 5 53M753 440 760 435 765 432 770 428 775 424 780 419 785 414 790 405 781 405 775 407 768 410 760 414 755 416 749 420 741 425 735 429 730 433 725 436M519 0 533 7 543 20 551 30 564 30 579 25 594 18 609 12 624 9 632 20 639 35 647 46 659 52 674 57 688 66 694 76 704 88 714 96 721 111 714 126 709 137 719 145 735 147 751 152 770 156 785 160 785 177 780 187 776 207 790 216M195 15 211 15 205 30 196 44 187 56 176 66 166 75 156 83 143 91 131 99 116 105 101 110 86 114 75 111 83 96 93 86 104 76 116 66 126 59 138 51 151 42 161 35 176 26 186 20M0 235 10 227 25 223 40 223 55 217 66 212 81 204 91 197 105 187 116 177 123 167 109 167 96 173 81 181 70 187 55 196 45 202 30 210 31 197 38 182 45 170 55 159 65 150 76 142 90 131 101 124 113 116 126 108 138 101 151 94 166 87 179 81 191 74 205 66 216 58 228 51 242 43 253 35 267 28 282 21 297 19 292 30 283 40 282 54 302 52 317 48 332 45 344 51 342 70 352 74 367 70 382 64 397 58 413 51 423 46 438 38 452 30 463 24 478 16 489 10 503 4M800 319 790 326 777 334 765 341 750 349 739 354 719 357 714 340 704 340 689 346 674 353 662 359 649 366 634 373 620 379 609 384 594 390 579 395 573 384 581 374 592 364 604 355 614 346 624 338 634 329 639 316 624 321 611 329 599 338 589 347 579 357 569 368 558 378 548 386 536 394 523 403 511 410 498 416 483 423 468 429 453 434 438 439M0 386 5 380 10 374 14 369 18 364 20 354 15 347 10 342 5 338M324 440 332 429 342 419 352 409 360 394 347 396 332 402 317 409 305 415 292 421 272 421 272 410 277 394 282 379 267 378 256 384 242 393 231 400 216 408 204 415 191 421 176 426 163 420 171 407 181 397 191 387 200 374 181 372 166 376 151 380 131 384 116 384 96 386 75 388 60 391 43 394 25 398 10 401M587 51 599 51 609 62 608 76 603 91 614 100 634 100 649 104 664 111 672 121 668 137 659 148 649 160 639 170 629 181 619 192 609 201 599 209 587 217 574 226 563 233 548 242 538 248 523 257 513 263 498 273 488 279 476 288 463 298 453 309 444 319 435 329 423 337 411 344 397 351 382 358 371 364 357 371 342 377 327 381 323 374 332 362 342 353 352 344 365 334 377 325 387 318 401 309 413 301 424 293 438 284 448 277 461 268 473 259 483 252 495 243 507 233 518 223 528 214 538 202 538 190 518 189 503 193 488 197 473 197 458 187 448 189 433 195 419 202 408 209 396 217 382 227 372 234 361 243 348 253 337 262 327 271 317 280 307 290 297 298 282 308 272 314 257 320 240 319 248 309 259 298 270 288 280 278 290 268 299 258 308 248 318 238 329 228 342 219 353 212 367 205 382 197 394 192 408 186 423 177 433 170 443 162 453 151 463 138 471 126 479 116 488 105 498 96 512 86 523 79 537 71 548 65 564 58 579 52M276 81 288 81 286 96 277 106 266 116 255 126 243 137 231 146 221 155 211 164 201 174 191 182 178 192 166 201 155 207 141 215 127 223 116 228 101 235 86 240 75 233 85 223 96 214 106 206 117 197 129 187 140 177 151 167 160 157 169 147 178 137 188 126 200 116 211 108 223 101 236 94 252 88 267 83M316 121 332 118 338 131 347 146 365 142 377 136 392 129 408 122 419 121 408 131 397 139 387 147 372 157 362 164 352 172 339 182 328 192 317 202 307 212 297 221 287 229 275 238 262 247 252 254 237 263 226 270 213 278 201 286 189 293 176 302 165 309 151 316 145 303 151 293 161 279 171 268 181 259 191 250 201 241 209 228 196 222 191 212 198 197 207 187 219 177 231 168 242 162 257 152 267 146 282 138 294 131 307 125M676 182 694 178 708 187 699 202 689 212 679 222 669 232 674 241 694 239 710 243 704 258 694 264 679 271 665 278 654 283 639 291 624 298 612 303 594 305 597 293 604 283 613 268 603 258 605 243 613 228 620 217 630 207 644 197 654 192 669 185M414 248 429 248 423 263 415 273 404 283 392 291 379 298 367 303 352 309 332 312 327 303 337 293 350 283 362 276 375 268 387 261 403 253 414 248M503 309 518 307 513 319 503 327 493 335 481 344 468 354 458 361 445 369 433 377 418 384 419 369 427 354 433 344 443 334 458 325 473 319 486 314 503 309M563 76 569 76 574 79 574 83 570 91 566 96 562 101 556 106 550 111 543 116 538 120 533 123 526 126 518 130 513 131 503 132 500 126 503 118 508 111 512 106 518 101 523 96 528 93 533 89 539 86 548 81 553 79 563 76M596 147 604 144 614 144 617 152 614 157 608 162 599 163 595 157 596 147"};
function paintTopo(){const el=document.getElementById('topo');if(!el||el.firstChild)return;
  el.innerHTML=`<svg viewBox="0 0 800 440" preserveAspectRatio="xMidYMid slice" focusable="false"><path d="${TOPO.major}"/></svg>`}
function palette(h){
  // Dégradés forêt selon l'heure ; seule la lueur de l'horizon change (aube / jour / crépuscule / nuit).
  if(h>=5&&h<8)return{bg:['#0B1812','#16301F','#27472F'],ridge:['#1F3D2D','#0F2118'],ridge2:['#16301F','#0A140F'],glow:'#F2A25E',ga:.55,orb:'#F7D9A8',line:'#C3D6BE'};
  if(h>=8&&h<17)return{bg:['#0E1F18','#1B3A2A','#33583F'],ridge:['#2C5240','#13291F'],ridge2:['#1D3D2D','#0B1A13'],glow:'#E9E4C8',ga:.30,orb:'#F2EFE4',line:'#C9DAC4'};
  if(h>=17&&h<20)return{bg:['#0A1510','#1A2E22','#3A4A30'],ridge:['#27453A','#10231A'],ridge2:['#183024','#09130E'],glow:'#F27A2A',ga:.50,orb:'#F5C08A',line:'#C3D6BE'};
  return{bg:['#07100C','#0D1D16','#15291F'],ridge:['#173028','#0A1511'],ridge2:['#0F2119','#060D0A'],glow:'#8FBDB5',ga:.14,orb:'#DDE6E0',line:'#9FB8AA'}}
function heroChips(m){const lv=levelInfo();
  return `<div class="hv-chips"><span class="hv-chip"><i>🏃</i><b class="cu cond" data-v="${m.km}" data-d="0">${fn(m.km,0)}</b><small>km courus</small></span><span class="hv-chip"><i>⛰️</i><b class="cu cond" data-v="${m.dp}" data-d="0">${fn(m.dp,0)}</b><small>m de D+</small></span><span class="hv-chip"><i>🏁</i><b class="cu cond" data-v="${m.n}" data-d="0">${m.n}</b><small>courses</small></span><span class="hv-chip"><i>⚡</i><b class="cond">${esc(lv.band[2])}</b><small>VDOT ${fn(baseVdot(),1)}</small></span></div>`}
function marqueeHTML(){const rs=metrics().run.slice(-10).reverse();if(rs.length<3)return '';
  const it=rs.map(r=>`<span class="mq-i"><b>${esc(r.name.split(' — ')[0])}</b> · ${fn(r.km)} km · +${fn(r.dplus,0)} m${r.result?` · ${esc(r.result)}`:''}</span>`).join('<span class="mq-s" aria-hidden="true">▲</span>');
  return `<div class="mq" role="marquee" aria-label="Mes dernières courses"><div class="mq-in"><div class="mq-g">${it}<span class="mq-s" aria-hidden="true">▲</span></div><div class="mq-g" aria-hidden="true">${it}<span class="mq-s">▲</span></div></div></div>`}
function sceneSVG(){
  const n=new Date(),hr=n.getHours()+n.getMinutes()/60,P=palette(Math.floor(hr)),night=hr>=20||hr<5,u=Math.max(0,Math.min(1,(hr-6)/14)),sx=140+520*u,sy=250-150*Math.sin(Math.PI*u);
  const pine=(x,sc)=>`<g transform="translate(${x},440) scale(${sc})"><path d="M0 0 L9 -26 L4 -26 L13 -48 L7 -48 L16 -70 L-16 -70 L-7 -48 L-13 -48 L-4 -26 L-9 -26Z"/></g>`;
  const stars=night?Array.from({length:30},(_,i)=>{const x=(i*97+31)%800,y=(i*53+17)%190,r=.8+(i%3)*.5;return `<circle class="hv-star" cx="${x}" cy="${y}" r="${r}" fill="#F2EFE4" style="animation-delay:${-(i%7)*.5}s"/>`}).join(''):'';
  const cloud=(y,sc,dl)=>`<g class="hv-cloud" style="animation-delay:${dl}s"><g transform="translate(0,${y}) scale(${sc})" fill="#fff" opacity="${night?.05:.12}"><ellipse cx="0" cy="0" rx="62" ry="12"/><ellipse cx="26" cy="-10" rx="34" ry="12"/><ellipse cx="-24" cy="-6" rx="28" ry="10"/></g></g>`;
  const TR="M232 408 C300 388 322 336 372 330 S452 350 500 314 S566 262 612 236 S676 214 708 186";
  const cap=(x,y,w)=>`<path d="M${x-w} ${y+w*1.1} L${x} ${y} L${x+w} ${y+w*1.15} L${x+w*.45} ${y+w*.8} L${x} ${y+w*1.25} L${x-w*.5} ${y+w*.8}Z" fill="#F2EFE4" opacity=".82"/>`;
  return `<svg viewBox="0 0 800 440" preserveAspectRatio="xMidYMid slice" aria-hidden="true" focusable="false"><defs>
  <linearGradient id="sk" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="${P.bg[0]}"/><stop offset=".55" stop-color="${P.bg[1]}"/><stop offset="1" stop-color="${P.bg[2]}"/></linearGradient>
  <radialGradient id="sun" cx=".5" cy=".5" r=".5"><stop offset="0" stop-color="${P.glow}" stop-opacity="${P.ga}"/><stop offset="1" stop-color="${P.glow}" stop-opacity="0"/></radialGradient>
  <linearGradient id="m1" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="${P.ridge[0]}"/><stop offset="1" stop-color="${P.ridge[1]}"/></linearGradient>
  <linearGradient id="m2" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="${P.ridge2[0]}"/><stop offset="1" stop-color="${P.ridge2[1]}"/></linearGradient></defs>
  <rect width="800" height="440" fill="url(#sk)"/>${stars}
  <g class="hv-sun"><circle cx="${sx.toFixed(0)}" cy="${sy.toFixed(0)}" r="190" fill="url(#sun)"/><circle cx="${sx.toFixed(0)}" cy="${sy.toFixed(0)}" r="16" fill="${P.orb}" opacity=".9"/></g>
  <g class="hv-l1" fill="none" stroke="${P.line}" stroke-linejoin="round"><path d="${TOPO.minor}" stroke-width=".8" opacity=".16" vector-effect="non-scaling-stroke"/><path d="${TOPO.major}" stroke-width="1.3" opacity=".34" vector-effect="non-scaling-stroke"/></g>
  ${cloud(80,1.2,0)}${cloud(130,.8,-35)}${cloud(50,1,-60)}
  <g class="hv-l2"><path d="M0 318 L80 282 L150 300 L262 196 L338 252 L428 214 L520 270 L628 176 L712 240 L800 214 V440 H0Z" fill="url(#m1)" opacity=".96"/>${cap(262,196,16)}${cap(628,176,18)}${cap(428,214,12)}</g>
  <g class="hv-l3"><path d="M0 366 C90 340 170 352 260 338 S430 352 520 334 S700 350 800 330 V440 H0Z" fill="url(#m2)"/></g>
  <path d="${TR}" fill="none" stroke="#F27A2A" stroke-width="3" stroke-linecap="round" class="hv-trail" opacity=".95"/>
  <circle cx="232" cy="408" r="6" fill="#F2EFE4" stroke="#F27A2A" stroke-width="3"/>
  <g><circle cx="708" cy="186" r="8" fill="#F27A2A" stroke="#F2EFE4" stroke-width="2.5"/><circle cx="708" cy="186" r="8" fill="none" stroke="#F27A2A" stroke-width="2"><animate attributeName="r" values="8;24" dur="2.4s" repeatCount="indefinite"/><animate attributeName="opacity" values=".8;0" dur="2.4s" repeatCount="indefinite"/></circle></g>
  <g class="hv-run"><circle r="16" fill="#F27A2A" opacity=".28"><animate attributeName="r" values="10;20;10" dur="1.6s" repeatCount="indefinite"/></circle><circle r="6.5" fill="#F2EFE4" stroke="#F27A2A" stroke-width="3.5"/><animateMotion dur="14s" repeatCount="indefinite" path="${TR}" calcMode="linear"/></g>
  <g fill="#060D0A" opacity=".92">${pine(34,1)}${pine(84,.7)}${pine(662,.62)}${pine(712,1.1)}${pine(764,.78)}</g></svg>`}
function bgHTML(){return `<div class="hero-bg">${sceneSVG()}</div>`}
function raceRow(r){const t=today(),d=dBetween(t,r.date),res=parseT(r.result),up=d>=0&&!res,dd=pISO(r.date);
  const hasD=r.dminus!=null&&r.dminus!=='';
  const chips=[`${fn(r.km)} km`,`+${fn(r.dplus,0)} m`,hasD?`−${fn(r.dminus,0)} m`:'−',res?`⏱️ ${esc(r.result)}`:(r.goal?`🎯 ${esc(r.goal)}`:'⏱️ —'),r.utmbCat?utmbLogo(r.utmbCat):'UTMB —',r.utmbPts?`${esc(r.utmbPts)} pts`:'pts —',...(r.prio?[`Objectif ${r.prio}`]:[])];
  return `<button class="rc" data-a="race" data-id="${r.id}" style="--cc:${CAT_C[catOf(r)]}"><span class="dbox"><em>${MON[dd.getMonth()]}</em><b>${dd.getDate()}</b><small class="xs mut">${dd.getFullYear()}</small></span><span class="rc-main"><b class="rc-name">${esc(r.name)}</b><span class="chips">${chips.map(c=>`<span class="chip${/ — |—$|^−$/.test(c)?' empty':''}">${c}</span>`).join('')}</span></span><span class="rc-side">${up?`<span class="tag up">${d===0?'Jour J':'J-'+d}</span>`:`<span class="tag ${r.status==='À confirmer'?'warn':''}">${esc(r.status||'Passée')}</span>`}${r.kind==='route'?'<span class="tag">route</span>':''}</span></button>`}
function evoCard(g){
  const E=g.eds,n=E.length,tm=E.filter(e=>e.eff!=null),W=260,H=70,PL=16,PR=16,PT=14,PB=22,iw=W-PL-PR,ih=H-PT-PB;
  const lo=tm.length?Math.min(...tm.map(e=>e.eff)):0,sp=tm.length>1?Math.max(1e-6,Math.max(...tm.map(e=>e.eff))-lo):1;
  const X=i=>PL+(n>1?i/(n-1)*iw:iw/2),Y=v=>tm.length>1?PT+(v-lo)/sp*ih:PT+ih/2; // plus rapide = plus haut
  const pts=E.map((e,i)=>e.eff!=null?{e,x:X(i),y:Y(e.eff)}:null).filter(Boolean),best=g.nTimed>1?g.best:null;
  const line=pts.length>1?`<polyline points="${pts.map(q=>`${q.x.toFixed(1)},${q.y.toFixed(1)}`).join(' ')}" fill="none" stroke="var(--ice)" stroke-width="2.2" stroke-linejoin="round" stroke-linecap="round"/>`:'';
  const dots=pts.map(q=>`<circle cx="${q.x.toFixed(1)}" cy="${q.y.toFixed(1)}" r="${q.e===best?6:4.5}" fill="${q.e===best?'var(--acc)':'var(--ice)'}" stroke="var(--card)" stroke-width="2"><title>${q.e.r.date.slice(0,4)} · ${esc(q.e.r.result)} · ${pace(q.e.eff)}/km-effort</title></circle>`).join('');
  const yrs=E.map((e,i)=>`<text x="${X(i).toFixed(1)}" y="${H-6}" text-anchor="middle">${e.r.date.slice(0,4)}</text>`).join('');
  const first=tm[0],last=g.last;
  let verdict='Un seul chrono pour l\'instant : la comparaison démarre à la prochaine édition chronométrée.';
  if(last&&last.d!=null){const tot=first&&first!==last?(last.eff-first.eff)/first.eff:null;
    verdict=`Dernière édition (${last.r.date.slice(0,4)}) : ${devTxt(last.d)} ${last.d<0?'plus rapide':'plus lente'} que la précédente${tot!=null&&tm.length>2?` · depuis ${first.r.date.slice(0,4)} : ${devTxt(tot)}`:''}.`}
  return `<div class="card evo-c"><h3 class="cond">${esc(g.name)} <span class="xs mut">≈ ${fn(g.km,0)} km · ${g.n} éditions</span></h3>
  <svg class="evo-svg" viewBox="0 0 ${W} ${H}" role="img" aria-label="Évolution de l'allure par km-effort sur ${esc(g.name)}, éditions ${E.map(e=>e.r.date.slice(0,4)).join(', ')}">${line}${dots}${yrs}</svg>
  <p class="evo-v">${verdict}</p>
  <div class="evo-eds">${E.map(e=>`<button type="button" class="evo-e${e===best?' best':''}" data-a="race" data-id="${e.r.id}" aria-label="Ouvrir l'édition ${e.r.date.slice(0,4)}"><b>${e.r.date.slice(0,4)}${e===best?' 🏆':''}</b><span>${e.r.result?esc(e.r.result):esc(e.r.status||'—')}</span><span class="xs">${e.d!=null?devTxt(e.d):'<span class="mut">—</span>'}</span></button>`).join('')}</div></div>`}
function evolBlock(){
  const c=classics(),ys=[...new Set(D.races.filter(r=>r.date).map(r=>r.date.slice(0,4)))].sort().reverse();
  const bilan=ys.length?`<div class="row evo-y"><span class="xs mut">Bilan par année :</span>${ys.map(y=>`<button class="btn ghost s" data-a="seasonOpen" data-y="${y}">📊 ${y}</button>`).join('')}</div>`:'';
  const head=`<div class="sec"><h2 class="cond">Évolution sur les mêmes courses</h2>${c.length?'<button class="btn ghost s" data-a="classics">Détail</button>':''}</div>`;
  if(!c.length)return head+`<div class="empty">Aucune course courue plusieurs fois pour l'instant.<br>Dès que tu cours une même épreuve une 2ᵉ fois (même nom, distance à ± 5 km), son évolution apparaît ici.</div>${bilan}`;
  return head+`<p class="xs mut" style="margin:-4px 0 12px">Même nom et même distance (à ± 5 km). Allure par km-effort d'une édition à l'autre : plus haut = plus rapide. 🏆 = meilleure édition.</p><div class="evo">${c.slice(0,6).map(evoCard).join('')}</div>${c.length>6?`<div class="row" style="margin-top:10px"><button class="btn ghost s" data-a="classics">Voir les ${c.length} courses</button></div>`:''}${bilan}`}
const HFX={t:null,r:null,io:null};
function weekStripSafe(w){return typeof weekStrip==='function'?weekStrip(w):''}
function todayCard(nx,pl){
  if(!nx)return `<div class="card today-card"><h2 class="cond">Aujourd'hui</h2><div class="empty">Ajoute ta prochaine course : ton plan du jour apparaîtra ici.<br><br><button class="btn" data-a="newRace">➕ Ajouter une course</button></div></div>`;
  if(!planReady(nx))return `<div class="card today-card"><h2 class="cond">Aujourd'hui</h2><p class="sm">Le plan pour ${esc(nx.name)} apparaîtra dès que tu auras renseigné les infos de la course.</p><div class="row" style="margin-top:8px"><button class="btn s" data-a="race" data-id="${nx.id}">✏️ Renseigner la course</button></div></div>`;
  const w=pl&&pl.weeks.find(x=>x.cur);
  if(!w)return `<div class="card today-card"><h2 class="cond">Aujourd'hui</h2><p class="sm">${pl&&pl.start>today()?`Ton plan pour ${esc(nx.name)} démarre le ${longD(pl.start)}.`:"Pas de séance prévue aujourd'hui."}</p><div class="row" style="margin-top:8px"><button class="btn s" data-a="plan" data-id="${nx.id}" data-t="train">🏃 Voir le plan</button></div></div>`;
  const s=w.sess.find(x=>x.d===today());
  return `<div class="card today-card"><div class="row" style="justify-content:space-between"><h2 class="cond" style="margin:0">Aujourd'hui · semaine ${w.i+1}/${pl.W}</h2><span class="tag up">${esc(w.phase)}</span></div>${weekStripSafe(w)}<div class="sessL" style="grid-template-columns:1fr">${s?sessCard(s):''}</div><div class="row" style="margin-top:6px"><button class="btn s" data-a="plan" data-id="${nx.id}" data-t="train">🏃 Ouvrir mon plan</button><button class="btn ghost s" data-a="plan" data-id="${nx.id}" data-t="nutri">🍌 Ma nutrition</button></div></div>`}
function raceTile(r){
  const d=dBetween(today(),r.date),i=raceInfo(r),pal={'Roulant':['#4C7F5F','#17342A'],'Vallonné':['#36694F','#12281F'],'Montagneux':['#2A5240','#0E1D16'],'Très technique / alpin':['#B8531C','#2A1810']}[i.diff]||['#4C7F5F','#17342A'];
  let svg;
  if(Array.isArray(r.prof)&&r.prof.length>3){const ys=r.prof.map(q=>q[1]),lo=Math.min(...ys),hi=Math.max(...ys),gk=r.prof[r.prof.length-1][0]||1,pts=r.prof.map(q=>`${(q[0]/gk*200).toFixed(1)},${(56-(q[1]-lo)/Math.max(1,hi-lo)*46).toFixed(1)}`).join(' ');
    svg=`<svg viewBox="0 0 200 60" preserveAspectRatio="none" aria-hidden="true"><polygon points="0,60 ${pts} 200,60" fill="rgba(255,255,255,.22)"/><polyline points="${pts}" fill="none" stroke="#fff" stroke-width="1.6"/></svg>`}
  else svg=`<svg viewBox="0 0 200 60" preserveAspectRatio="none" aria-hidden="true"><path d="M0 60 L0 44 L30 30 L50 40 L90 12 L120 36 L150 22 L200 40 L200 60Z" fill="rgba(255,255,255,.2)"/></svg>`;
  return `<button class="tile" data-a="race" data-id="${r.id}" style="--tc1:${pal[0]};--tc2:${pal[1]}"><span class="tile-top">${svg}<span class="tile-d cond">${d===0?'Jour J':'J-'+d}</span></span><span class="tile-b"><b>${esc(r.name)}</b><span class="xs mut">${longD(r.date)}</span><span class="chips"><span class="chip">${fn(r.km)} km</span><span class="chip">+${fn(r.dplus,0)} m</span><span class="chip">${i.diff}</span></span></span></button>`}
function homeFxStop(){clearInterval(HFX.t);clearInterval(HFX.r);HFX.t=HFX.r=null;if(HFX.io){HFX.io.disconnect();HFX.io=null}}
function countUp(){
  if(window.matchMedia&&matchMedia('(prefers-reduced-motion: reduce)').matches)return;
  $$('.cu').forEach(el=>{const v=+el.dataset.v,d=+el.dataset.d||0;if(!(v>0))return;const t0=performance.now(),step=t=>{const k=Math.min(1,(t-t0)/1000),e=1-Math.pow(1-k,3);el.textContent=fn(v*e,d);if(k<1)requestAnimationFrame(step)};requestAnimationFrame(step)})}
function homeFx(){
  homeFxStop();if(S.tab!=='home')return;countUp();
  if(window.matchMedia&&matchMedia('(prefers-reduced-motion: reduce)').matches){const sv=document.querySelector('.hero-bg svg');if(sv&&sv.pauseAnimations)sv.pauseAnimations()}
  const items=$$('#main .card, #main .rc, #main .quick, #main .tile, #main .ringc');
  if('IntersectionObserver' in window){HFX.io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');HFX.io.unobserve(e.target)}}),{threshold:.06});items.forEach(el=>{el.classList.add('rv');HFX.io.observe(el)})}
  const tick=()=>{const c=$('#cdn');if(!c)return;let ms=new Date(c.dataset.t)-new Date();if(!(ms>0))ms=0;const s=Math.floor(ms/1000),v={d:Math.floor(s/86400),h:Math.floor(s%86400/3600),m:Math.floor(s%3600/60),s:s%60};$$('[data-u]',c).forEach(e=>{const x=v[e.dataset.u];e.textContent=e.dataset.u==='d'?x:pad(x)})};
  if($('#cdn')){tick();HFX.t=setInterval(()=>{if(!$('#cdn')){homeFxStop();return}tick()},1000)}
  const rot=$('#rot');if(rot){let L=[];try{L=JSON.parse(rot.dataset.l)}catch(e){}
    if(L.length>1){let i=0;HFX.r=setInterval(()=>{const el=$('#rot');if(!el)return;el.classList.add('out');setTimeout(()=>{i=(i+1)%L.length;el.textContent=L[i];el.classList.remove('out')},400)},4500)}}}
(function(){
  window.addEventListener('scroll',()=>{const el=document.querySelector('.hero');if(el)el.style.setProperty('--sy',Math.min(1,window.scrollY/420).toFixed(3))},{passive:true});
  document.addEventListener('pointermove',e=>{const el=document.querySelector('.hero');if(el)el.style.setProperty('--mx',((e.clientX/window.innerWidth-.5)*2).toFixed(3))},{passive:true})})();
/* Un plan n'est généré que lorsque les infos de la course sont saisies (conditions + état physique). */
const planReady=r=>!!(r&&r.cond&&r.phys);
const planWait=r=>`<div class="empty">Le plan d'entraînement de <b>${esc(r.name)}</b> apparaîtra ici dès que tu auras renseigné les infos de la course : <b>conditions particulières</b> et <b>état physique actuel</b>.<br><br><button class="btn" data-a="race" data-id="${r.id}">✏️ Renseigner la course</button></div>`;
function renderHome(){
  S.ringSel=null;
  const p=D.profile,m=metrics(),up=upcoming(),nx=up[0],hr=new Date().getHours(),hello=hr<6||hr>=19?'Bonsoir':hr<12?'Bonjour':'Bon après-midi';
  let pl=null;if(nx&&planReady(nx)){try{pl=genPlan(nx)}catch(e){pl=null}}
  const lines=[];
  if(nx){const d=dBetween(today(),nx.date);lines.push(d===0?`C'est le jour J : ${nx.name} !`:`${nx.name} dans ${d} jour${d>1?'s':''}.`)}
  const tw=pl&&pl.weeks.find(w=>w.cur),ts=tw&&tw.sess.find(s=>s.d===today());
  if(ts)lines.push(ts.ty==='rest'?"Aujourd'hui : repos, c'est là que tu progresses.":`Aujourd'hui : ${ts.title}.`);
  lines.push(`${fn(m.km,0)} km et ${fn(m.dp,0)} m de D+ au compteur.`,`Niveau ${levelInfo().band[2]} · VDOT ${fn(baseVdot(),1)}.`,"Vertex centralise tes courses, tes plans d'entraînement et ta nutrition.");
  let next;
  if(nx){const tm=/^\d{1,2}:\d{2}$/.test(nx.startTime||'')?nx.startTime:'08:00',tg=`${nx.date}T${tm.length<5?'0'+tm:tm}`;
    next=`<div class="next"><div class="cdn" id="cdn" data-t="${tg}">${[['d','jours'],['h','heures'],['m','min'],['s','sec']].map(([u,l])=>`<div><b class="cond" data-u="${u}">0</b><span>${l}</span></div>`).join('')}</div><div><b>${esc(nx.name)}</b><div class="sm" style="color:#dfe9e0">${longD(nx.date)} · ${fn(nx.km)} km · +${fn(nx.dplus,0)} m</div></div><button class="btn lime s" data-a="race" data-id="${nx.id}">Voir la fiche</button></div>`}
  else next=`<div class="next"><button class="btn" data-a="newRace">➕ Ajouter ma prochaine course</button></div>`;
  const unconf=D.races.filter(r=>r.status==='À confirmer'&&r.date<=today());
    const rings=[['n',m.n,'au total','Courses'],['km',fn(m.km,0),'km','Distance'],['dp',fn(m.dp,0),'m D+','Dénivelé'],['time',fn(m.min/60,1),'heures','Temps'],['pace',m.pace?pace(m.pace).replace('"',''):'—','min/km','Allure']].map(([k,v,u,l])=>ring(v,u,l,k)).join('');
  return `<section class="hero hv">${bgHTML()}<span class="hv-blob b1"></span><span class="hv-blob b2"></span><div class="hero-tools"><button class="btn ghost s" style="background:rgba(10,18,15,.6);color:#f2f6ef;border-color:rgba(255,255,255,.35);backdrop-filter:blur(6px)" data-a="theme" aria-label="Changer de thème (actuel : ${({auto:'automatique',light:'clair',dark:'sombre'})[getTheme()]})">${({auto:'🌓',light:'☀️',dark:'🌙'})[getTheme()]} Thème</button></div><div class="hero-in"><p class="hv-hello cond"><span class="hv-dot"></span>${hello} ${esc(p.name||'')}</p><h1 class="cond">Chaque sommet<br>commence <span class="hv-grad">ici.</span></h1><p class="rot" id="rot" data-l="${esc(JSON.stringify(lines))}">${esc(lines[0])}</p>${next}${heroChips(m)}</div></section>
  <div class="wrap"><div class="rings">${rings}</div><div id="ringpanel" class="ringpanel hide" aria-live="polite"></div><p class="xs mut tc rings-note">Touche une part d'un cercle (ou une ligne de sa légende) pour voir les courses de ce type juste en dessous, ou le centre du cercle pour le détail complet.${m.skipped.length?` <button class="xs" style="text-decoration:underline;color:var(--mut)" data-a="ring" data-k="n">${m.skipped.length} course${m.skipped.length>1?'s':''} de ta liste non comptée${m.skipped.length>1?'s':''} : voir</button>`:''}</p>
  ${unconf.length?`<div class="note" style="margin-top:14px">⚠️ ${unconf.length} course${unconf.length>1?'s':''} passée${unconf.length>1?'s':''} à confirmer (${unconf.map(r=>esc(r.name)).join(', ')}). Saisis le statut et le chrono pour compléter tes statistiques.</div>`:''}
  ${marqueeHTML()}<div style="margin-top:18px">${todayCard(nx,pl)}</div>
  <div class="sec"><h2 class="cond">Prochains trails</h2><button class="btn ghost s" data-a="newRace">➕ Ajouter</button></div>${up.length?`<div class="hs">${up.map(raceTile).join('')}</div>`:'<div class="empty">Aucune course à venir pour le moment.<br>Ajoute ton prochain objectif pour générer plan d\'entraînement, nutrition et chronos cibles.</div>'}
  ${backupNote()}${levelCard()}${progressCard()}${analysesRow()}
  ${evolBlock()}
  </div>`}

/* ============================ PROFIL ============================ */
const PF=[['Identité',[['name','Prénom','text'],['age','Âge','number','ans'],['height','Taille','number','cm'],['weight','Poids habituel','number','kg'],['weightTaper',"Poids en affûtage",'number','kg']]],
 ['Physiologie',[['utmb','Index UTMB','number'],['vo2','VO₂ max (montre)','number'],['hrRest','FC repos','number','bpm'],['hrMax','FC max','number','bpm'],['feel','Ressenti du moment (1 très fatigué → 10 en pleine forme)','number']]],
 ['Entraînement',[['sessionsRun','Séances de course / sem.','number'],['sessionsGym','Séances de muscu / sem.','number'],['weeklyKm','Volume de course actuel (km/sem.)','number'],['dplusAvail','D+ naturel disponible à l\'entraînement (m/sem.)','number'],['treadmill','Tapis incliné disponible (oui / non)','text'],['terrain','Terrain habituel','text','','full'],['habit','Habitudes','text','','full'],['gym','Salle de sport','text']]],
 ['Nutrition de course',[['nutriWater','Eau en course','number','ml/h'],['nutriIso','Iso+ en course','number','ml/h'],['nutriCarbs','Glucides en course','number','g/h']]],
 ['Matériel',[['shoes','Chaussures','text'],['watch','Montre','text']]]];
function renderProfile(){
  const p=D.profile,tm=timed().sort((a,b)=>a.date<b.date?-1:1),all=D.races.slice().sort((a,b)=>a.date<b.date?1:-1);
  const form=PF.map(([t,fs])=>`<details class="card hist"><summary><h2 class="cond" style="display:inline-block;margin:0">${t}</h2></summary><div class="frm" style="margin-top:12px">${fs.map(([k,l,ty,u,full])=>`<label class="f ${full||''}">${l}${u?' ('+u+')':''}<input id="p-${k}" type="${ty}" ${ty==='number'?'step="any" inputmode="decimal"':''} value="${esc(p[k])}"></label>`).join('')}</div>${t==='Nutrition de course'?foodsEditor():''}</details>`).join('');
  const bmi=p.weight/((p.height/100)**2);
  return `<div class="wrap"><div class="sec" style="margin-top:0"><h2 class="cond">Profil du coureur</h2><button class="btn s" data-a="saveProfile">💾 Enregistrer</button></div>
  <div class="card"><div class="kv"><div><b>${p.age} ans</b><span>${p.height} cm · ${p.weight} kg</span></div><div><b>${fn(bmi)}</b><span>IMC</span></div><div><b>${p.vo2}</b><span>VO₂ max (montre)</span></div></div></div>
  <details class="card hist"><summary><h2 class="cond" style="display:inline-block;margin:0">Historique complet</h2> <span class="xs mut">· réduire / développer</span></summary><div class="sec" style="margin:12px 0 8px"><button class="btn ghost s" data-a="newRace">➕ Ajouter une course</button></div><div class="tscroll"><table><thead><tr><th>Course</th><th>Date</th><th>Km</th><th>D+</th><th>Chrono</th><th>Allure</th><th>min/km-eff.</th></tr></thead><tbody>${all.map(r=>{const t=parseT(r.result);return `<tr><td><button data-a="race" data-id="${r.id}" style="text-align:left;text-decoration:underline">${esc(r.name)}</button>${r.kind==='route'?' <span class="tag">route</span>':''}${r.site&&/^https?:/.test(r.site)?` <a href="${esc(r.site)}" target="_blank" rel="noopener noreferrer" aria-label="Site de la course">🌐</a>`:''}</td><td>${shortD(r.date)}</td><td>${fn(r.km)}</td><td>${fn(r.dplus,0)}</td><td>${t?esc(r.result):'—'}</td><td>${t?pace(t/r.km):'—'}</td><td>${t?pace(t/effKm(r)):'—'}</td></tr>`}).join('')}</tbody></table></div><p class="xs mut" style="margin-top:8px">Compare la colonne « min/km-effort » : c'est la plus juste pour comparer des courses de profils différents.</p></details>
  ${form}<details class="card hist"><summary><h2 class="cond" style="display:inline-block;margin:0">Données</h2></summary><div class="row" style="margin-top:12px"><button class="btn ghost s" data-a="export">⬇️ Exporter une sauvegarde</button><button class="btn ghost s" data-a="import">⬆️ Restaurer / importer (Vertex ou Trail Prep)</button><button class="btn red s" data-a="reset">Réinitialiser</button><button class="btn ghost s" data-a="tests">🧪 Auto-tests</button></div><p class="xs mut" style="margin-top:8px">${LS.get('vertex_lastexport')?`Dernière sauvegarde exportée : ${longD(LS.get('vertex_lastexport'))}.`:"Aucune sauvegarde exportée pour l'instant."} Tes données restent dans ce navigateur : exporte-les régulièrement.</p><div id="ab" class="sm" style="margin-top:12px">${abStatus()}</div><div id="pwa" class="sm" style="margin-top:12px">${pwaStatus()}</div></details></div>`}
function migrateData(){let ch=false;const p=D.profile;
  if(!p._c75){p._c75=1;if(+p.nutriCarbs===70||p.nutriCarbs===''||p.nutriCarbs==null)p.nutriCarbs=75;ch=true}
  // Records route : une seule source (les courses route). Les anciens champs du profil sont retirés.
  ['rec5','rec10','rec15','recHalf','gRaces','gKm','gDp','gHours'].forEach(k=>{if(k in p){delete p[k];ch=true}});
  // Corrections de dates : appliquées uniquement si l'ancienne valeur erronée est encore là (une date que tu as modifiée toi-même est respectée).
  [['t25-saintexpress','2026-11-29','2025-11-29'],['t25-falaises-b','2025-07-12','2026-07-12']].forEach(([id,bad,ok])=>{
    const r=D.races.find(x=>x.id===id);if(r&&r.date===bad){r.date=ok;ch=true}});
  if(!Array.isArray(p.utmbHist)){p.utmbHist=+p.utmb>0?[{d:today(),v:+p.utmb}]:[];ch=true}
  D.races.forEach(r=>{
    if(r.status==='Abandon'){r.status='DNF';ch=true}else if(r.status==='Non-partant'){r.status='DNS';ch=true}
    if(r.id==='route-10k'&&r.result==="42'55"){r.result="42'42";ch=true}
    if(r.id==='route-semi'&&r.result==="1h35'55"){r.result="1h35'40";ch=true}
    if(r.noJ7===undefined){r.noJ7=/saint.?ly[oô]n/i.test(r.name||'')&&/^2026/.test(r.date||'');ch=true}
    if('srcNote' in r){delete r.srcNote;ch=true}
    if('check' in r){delete r.check;ch=true}
  });
  // Plan du coach rattaché à chaque course : un ancien plan unique est rangé sous la prochaine course (ou la plus récente).
  if(D.ai&&typeof D.ai==='object'){const tgt=upcoming()[0]||D.races.slice().sort((a,b)=>a.date<b.date?1:-1)[0];
    if(tgt)['resp','done','start'].forEach(f=>{const o=D.ai[f];if(!o||typeof o!=='object')return;['train','nutri'].forEach(k=>{if(k in o){const nk=k+'@'+tgt.id;if(!(nk in o))o[nk]=o[k];delete o[k];ch=true}})})}
  if(!p._gpxSync1){p._gpxSync1=1;D.races.forEach(r=>{if(r.prof&&r.gx&&r.gx.dp!=null&&syncGpx(r))ch=true});ch=true}
  if(ch)save()}
function saveProfile(){const p=D.profile,u0=+p.utmb;PF.forEach(([,fs])=>fs.forEach(([k,,ty])=>{const el=$('#p-'+k);if(!el)return;p[k]=ty==='number'?(el.value===''?p[k]:parseFloat(el.value)):el.value.trim()}));if(+p.utmb>0&&+p.utmb!==u0)utmbNote(p.utmb);save();toast('Profil enregistré : tous les calculs sont mis à jour.');render()}

/* ============================ SÉLECTEURS DATE & HEURE ============================ */
const PKS={};
const pkEl=id=>document.getElementById(id);
const pkText=(mode,v)=>!v?(mode==='date'?'Choisir une date':'Choisir l\'heure'):(mode==='date'?longD(v):v);
function pkField(id,mode,val,key,label){
  return `<div class="f pkf">${label?`<span class="pklab">${esc(label)}</span>`:''}<button type="button" class="pkbtn" id="b-${id}" data-a="pkOpen" data-f="${id}" aria-expanded="false" aria-controls="p-${id}">${esc(pkText(mode,val))}</button><input type="hidden" id="${id}" data-mode="${mode}" ${key?`data-c="filt" data-k="${key}"`:''} value="${esc(val||'')}"><div class="pkpop hide" id="p-${id}" role="dialog" aria-label="${mode==='date'?'Choisir la date':'Choisir l\'heure'}"></div></div>`}
function pkOpen(id){const inp=pkEl(id),pop=$('#p-'+id),btn=$('#b-'+id);if(!inp||!pop)return;
  if(!pop.classList.contains('hide')){pkDone(id,true);return}
  const mode=inp.dataset.mode,v=inp.value,st={mode,view:(v&&mode==='date'?v:today()).slice(0,7),step:'h',ap:'AM',h:null,m:null};
  if(mode==='time'&&v){const [hh,mm]=v.split(':').map(Number);st.ap=hh>=12?'PM':'AM';st.h=hh%12||12;st.m=mm}
  PKS[id]=st;pop.classList.remove('hide');btn.setAttribute('aria-expanded','true');pkPaint(id)}
function pkSet(id,fn,commit){const st=PKS[id];if(!st)return;fn(st);
  if(commit&&st.h!=null&&st.m!=null)pkCommit(id,false);else pkPaint(id)}
function pkMinute(id,m){const st=PKS[id];if(!st)return;st.m=m;if(st.h!=null)pkCommit(id,true);else pkPaint(id)}
function pkCommit(id,close){const st=PKS[id],inp=pkEl(id);
  const h24=st.ap==='PM'?(st.h%12)+12:st.h%12;inp.value=`${pad(h24)}:${pad(st.m)}`;pkDone(id,close)}
function pkDone(id,close){const inp=pkEl(id),pop=$('#p-'+id),btn=$('#b-'+id);if(!inp)return;
  if(close&&pop){pop.classList.add('hide');btn.setAttribute('aria-expanded','false')}
  btn.textContent=pkText(inp.dataset.mode,inp.value);
  if(!close&&PKS[id])pkPaint(id);
  inp.dispatchEvent(new Event('change',{bubbles:true}))}
function pkPick(id,v){const inp=pkEl(id);if(!inp)return;inp.value=v;pkDone(id,true)}
function pkNav(id,s){const st=PKS[id];if(!st)return;const d=pISO(st.view+'-01');d.setMonth(d.getMonth()+s);st.view=iso(d).slice(0,7);pkPaint(id)}
function pkPaint(id){const pop=$('#p-'+id),st=PKS[id],inp=pkEl(id);if(!pop||!st||!inp)return;
  if(st.mode==='date'){
    const [y,m]=st.view.split('-').map(Number),f=iso(new Date(y,m-1,1)),start=addD(f,-dow(f));let cells='';
    for(let i=0;i<42;i++){const d=addD(start,i),dd=pISO(d);
      cells+=`<button type="button" class="pkd${dd.getMonth()!==m-1?' out':''}${d===inp.value?' sel':''}${d===today()?' tod':''}" data-a="pkDay" data-f="${id}" data-v="${d}" aria-label="${longD(d)}">${dd.getDate()}</button>`}
    pop.innerHTML=`<div class="pkhead"><button type="button" class="btn ghost s" data-a="pkNav" data-f="${id}" data-s="-1" aria-label="Mois précédent">◀</button><b class="cond">${MONL[m-1]} ${y}</b><button type="button" class="btn ghost s" data-a="pkNav" data-f="${id}" data-s="1" aria-label="Mois suivant">▶</button></div>
    <div class="pkgrid pkwd">${['L','M','M','J','V','S','D'].map(x=>`<span>${x}</span>`).join('')}</div><div class="pkgrid">${cells}</div>
    <div class="pkfoot"><button type="button" class="btn ghost s" data-a="pkDay" data-f="${id}" data-v="${today()}">Aujourd'hui</button><button type="button" class="btn ghost s" data-a="pkClr" data-f="${id}">Effacer</button></div>`;
    return}
  const isH=st.step==='h',cur=isH?(st.h!=null?st.h%12:null):(st.m!=null?st.m/60:null);
  let nums='';
  if(isH){for(let i=1;i<=12;i++){const a=i/12*2*Math.PI;nums+=`<button type="button" class="clk-n${st.h===i?' on':''}" style="left:${(50+37*Math.sin(a)).toFixed(2)}%;top:${(50-37*Math.cos(a)).toFixed(2)}%" data-a="pkHour" data-f="${id}" data-h="${i}" aria-label="${i} heures">${i}</button>`}}
  else{for(let i=0;i<12;i++){const mn=i*5,a=mn/60*2*Math.PI;nums+=`<button type="button" class="clk-n${st.m===mn?' on':''}" style="left:${(50+37*Math.sin(a)).toFixed(2)}%;top:${(50-37*Math.cos(a)).toFixed(2)}%" data-a="pkMin" data-f="${id}" data-m="${mn}" aria-label="${mn} minutes">${pad(mn)}</button>`}}
  const hand=cur==null?'':`<svg class="clk-hand" viewBox="0 0 100 100" aria-hidden="true"><line x1="50" y1="50" x2="${(50+36*Math.sin(cur/12*2*Math.PI)).toFixed(2)}" y2="${(50-36*Math.cos(cur/12*2*Math.PI)).toFixed(2)}"/></svg>`;
  pop.innerHTML=`<div class="pkhead"><div class="pkseg"><button type="button" class="${isH?'on':''}" data-a="pkStep" data-f="${id}" data-s="h" aria-pressed="${isH}">Heure ${st.h!=null?pad(st.h):'--'}</button><button type="button" class="${isH?'':'on'}" data-a="pkStep" data-f="${id}" data-s="m" aria-pressed="${!isH}">Minutes ${st.m!=null?pad(st.m):'--'}</button></div><div class="pkseg"><button type="button" class="${st.ap==='AM'?'on':''}" data-a="pkAp" data-f="${id}" data-p="AM">AM</button><button type="button" class="${st.ap==='PM'?'on':''}" data-a="pkAp" data-f="${id}" data-p="PM">PM</button></div></div>
  <div class="clk">${hand}<span class="clk-c"></span>${nums}</div>
  <div class="pkfoot"><span class="xs mut">${inp.value?'Actuel : '+esc(inp.value):(isH?'Choisis d\'abord l\'heure':'Puis les minutes')}</span><button type="button" class="btn ghost s" data-a="pkClr" data-f="${id}">Effacer</button></div>`}

/* ============================ COURSES ============================ */
function filtOf(){return S.filt||(S.filt={q:'',kmMin:'',kmMax:'',dpMin:'',dpMax:'',from:'',to:'',y:'all'})}
const hasXY=r=>r.lat!=null&&r.lat!==''&&isFinite(r.lat)&&r.lon!=null&&r.lon!==''&&isFinite(r.lon);
function racesFiltered(){const f=filtOf(),t=today(),isUp=r=>r.date>=t&&!parseT(r.result),num=v=>v===''||v==null?null:+v,q=(f.q||'').trim().toLowerCase(),a=num(f.kmMin),b=num(f.kmMax),c=num(f.dpMin),d=num(f.dpMax);
  return D.races.filter(r=>{if(f.y==='up'&&!isUp(r))return false;if(f.y!=='all'&&f.y!=='up'&&r.date.slice(0,4)!==f.y)return false;
    if(q&&!(r.name||'').toLowerCase().includes(q)&&!(r.place||'').toLowerCase().includes(q))return false;
    if(a!=null&&!(+r.km>=a))return false;if(b!=null&&!(+r.km<=b))return false;if(c!=null&&!(+r.dplus>=c))return false;if(d!=null&&!(+r.dplus<=d))return false;
    if(f.from&&r.date<f.from)return false;if(f.to&&r.date>f.to)return false;return true}).sort((x,y)=>x.date<y.date?1:-1)}
/* Blocs repliables harmonisés (Mes courses + fiche course) : pastille, titre, sous-titre, chevron. */
const foldHead=(ic,t,sub)=>`<summary><span class="fold-ic" aria-hidden="true">${ic}</span><h2 class="cond">${t}</h2><small>${sub||'&nbsp;'}</small></summary>`;
/* Calendrier des courses façon Google Agenda : une pastille colorée par course (couleur = type de course). */
function rcMonthKey(){return S.rcMon||today().slice(0,7)}
function raceCalHTML(){
  const m=rcMonthKey(),[Y,M]=m.split('-').map(Number),first=`${m}-01`,nd=new Date(Y,M,0).getDate(),lead=dow(first),t=today(),list=racesFiltered(),by={};
  list.forEach(r=>{(by[r.date]=by[r.date]||[]).push(r)});
  const inM=list.filter(r=>r.date.slice(0,7)===m),start=addD(first,-lead),total=Math.ceil((lead+nd)/7)*7,MAXE=3;
  const pill=r=>{const st=r.status,res=parseT(r.result),ic=st==='DNF'?'✕ ':st==='DNS'?'⊘ ':res?'✓ ':st==='À confirmer'?'? ':'',nm=String(r.name).split(/\s[—–-]\s/)[0];
    return `<button type="button" class="rcal-e${res?' fin':''}${st==='À confirmer'?' unc':''}${st==='DNF'||st==='DNS'?' dnf':''}" style="--cc:${CAT_C[catOf(r)]}" data-a="race" data-id="${r.id}" title="${esc(r.name)} · ${fn(r.km)} km · +${fn(r.dplus,0)} m" aria-label="${esc(r.name)}, ${fn(r.km)} km, ${longD(r.date)}"><b>${ic}${esc(nm)}</b><small>${fn(r.km,0)} km</small></button>`};
  let cells='';
  for(let i=0;i<total;i++){const x=addD(start,i),inMon=x.slice(0,7)===m,dn=+x.slice(8),ev=(by[x]||[]).slice().sort((a,b)=>(+b.km||0)-(+a.km||0)),shown=ev.slice(0,ev.length>MAXE?MAXE-1:MAXE),more=ev.length-shown.length;
    cells+=`<div class="rcal-d${inMon?'':' out'}${x===t?' today':''}${dow(x)>=5?' we':''}${ev.length?' has':''}"${ev.length?` style="--cc:${CAT_C[catOf(ev[0])]}"`:''} role="gridcell"${x===t?' aria-current="date"':''}><span class="rcal-n">${dn===1?dn+' '+MON[pISO(x).getMonth()]:dn}</span>${shown.map(pill).join('')}${more?`<span class="rcal-more" title="${esc(ev.slice(shown.length).map(r=>r.name).join(', '))}">+${more} autre${more>1?'s':''}</span>`:''}</div>`}
  const wd=[['lun.','L'],['mar.','M'],['mer.','M'],['jeu.','J'],['ven.','V'],['sam.','S'],['dim.','D']].map(([a,b])=>`<div class="rcal-w"><span class="l">${a}</span><span class="s">${b}</span></div>`).join('');
  const ml=inM.length?`<ul class="rcal-ml" aria-label="Courses de ${MONL[M-1]}">${inM.slice().sort((a,b)=>a.date<b.date?-1:1).map(r=>`<li><button type="button" data-a="race" data-id="${r.id}" style="--cc:${CAT_C[catOf(r)]}"><span class="d">${DAYS[dow(r.date)].slice(0,3).toLowerCase()}. ${+r.date.slice(8)}</span><b>${esc(String(r.name).split(/\s[—–-]\s/)[0])}</b><small>${fn(r.km,0)} km · +${fn(r.dplus,0)} m</small></button></li>`).join('')}</ul>`:'';
  const leg=CAT_N.map((n,k)=>`<span><i style="background:${CAT_C[k]}"></i>${n}</span>`).join('')+'<span class="xs">✓ terminée · ✕ abandon · ? à confirmer</span>';
  return `<details class="card hist fold" id="racecal">${foldHead('🗓️','Calendrier des courses',inM.length?`${inM.length} course${inM.length>1?'s':''} en ${MONL[M-1]}`:`Aucune course en ${MONL[M-1]}`)}
  <div class="rcal"><div class="rcal-h"><button type="button" class="btn ghost s" data-a="rcMonth" data-s="0">Aujourd'hui</button><button type="button" class="btn ghost s" data-a="rcMonth" data-s="-1" aria-label="Mois précédent">‹</button><button type="button" class="btn ghost s" data-a="rcMonth" data-s="1" aria-label="Mois suivant">›</button><b class="cond rcal-t" aria-live="polite">${MONL[M-1]} ${Y}</b></div>
  <div class="rcal-g" role="grid" aria-label="Calendrier des courses, ${MONL[M-1]} ${Y}">${wd}${cells}</div>${ml}<div class="rcal-leg">${leg}</div></div></details>`}
function refreshRaceCal(focusS){const e=$('#racecal');if(!e)return;const open=e.open;e.outerHTML=raceCalHTML();const n=$('#racecal');if(n)n.open=open;
  const b=focusS!=null&&document.querySelector(`#racecal [data-a="rcMonth"][data-s="${focusS}"]`);if(b)b.focus()}
function renderRaces(){
  const f=filtOf(),all=D.races,list=racesFiltered(),isUp=r=>r.date>=today()&&!parseT(r.result),up=list.filter(isUp),past=list.filter(r=>!isUp(r));
  const inp=(k,l,ty,ph)=>`<label class="f">${l}<input type="${ty}" ${ty==='number'?'step="any" inputmode="decimal"':''} placeholder="${ph||''}" value="${esc(f[k]||'')}" data-c="filt" data-k="${k}"></label>`;
  const nLoc=all.filter(hasXY).length;
  return `<div class="wrap"><div class="sec" style="margin-top:0"><h2 class="cond">Mes courses</h2><div class="row"><button class="btn ghost s" data-a="gpxSyncAll">🔄 Recalculer d'après les GPX</button><button class="btn s" data-a="newRace">➕ Nouvelle course</button></div></div>
  ${raceCalHTML()}
  <details class="card hist fold mapcard" id="mapfold" open>${foldHead('🗺️','Carte des courses',`${nLoc} placée${nLoc>1?'s':''} sur ${all.length}`)}<div id="map" role="region" aria-label="Carte des courses"></div><p class="xs mut" style="margin-top:8px">Touche un repère pour ouvrir la course. Renseigne le lieu (ville, pays) dans la fiche pour la placer.</p></details>
  <details class="card filterbar hist fold">${foldHead('🔎','Filtres',`${list.length} / ${all.length} course(s)`)}<div class="frm2 filt">${inp('q','Nom ou lieu','text','ex. Ventoux')}${inp('kmMin','Km min','number','0')}${inp('kmMax','Km max','number','')}${inp('dpMin','D+ min (m)','number','0')}${inp('dpMax','D+ max (m)','number','')}${pkField('f-from','date',f.from||'','from','Du')}${pkField('f-to','date',f.to||'','to','Au')}<button class="btn ghost s" data-a="filtClr">Effacer</button></div>
  <p class="xs mut">${list.length} course(s) affichée(s) sur ${all.length} · plus récente en premier</p></details>
  ${up.length?`<h3 class="cond mut" style="margin:10px 0 8px">À venir</h3>${up.map(raceRow).join('')}`:''}${past.length?`<h3 class="cond mut" style="margin:14px 0 8px">Passées</h3>${past.map(raceRow).join('')}`:''}${!list.length?'<div class="empty">Aucune course pour ces filtres.</div>':''}</div>`}
let MAP=null;
function mountMap(){const el=document.getElementById('map');if(!el)return;
  if(MAP){MAP.remove();MAP=null}
  if(typeof L==='undefined'){el.innerHTML='<div class="empty">Carte indisponible (hors connexion).</div>';return}
  MAP=L.map(el,{scrollWheelZoom:false}).setView([46.5,2.5],4);mapBase(MAP);
  const pts=racesFiltered().filter(hasXY);
  if(!pts.length)return;
  const g=L.featureGroup(pts.map(r=>L.marker([+r.lat,+r.lon],{icon:r.date>=today()?mapPin('up','🏁',32):mapPin('pa','✓',28)}).bindTooltip(`${esc(r.name)} · ${shortD(r.date)}`).on('click',()=>openRace(r.id)))).addTo(MAP);
  MAP.fitBounds(g.getBounds().pad(.25),{maxZoom:8,animate:false})}
async function geocodeRace(id){const r=D.races.find(x=>x.id===id),q=((r&&r.place)||'').trim();if(!q)return false;
  try{const res=await fetch('https://nominatim.openstreetmap.org/search?format=json&limit=1&q='+encodeURIComponent(q),{headers:{'Accept-Language':'fr'}});if(!res.ok)throw new Error('http');
    const j=await res.json();if(!j[0]){toast(`Lieu introuvable : « ${q} ». Essaie « ville, pays ».`,1);return false}
    r.lat=+(+j[0].lat).toFixed(5);r.lon=+(+j[0].lon).toFixed(5);r.geoFor=q;save();return true}
  catch(e){toast('Localisation impossible (réseau).',1);return false}}
function raceInfo(r){const E=effKm(r),ratio=r.km?r.dplus/r.km:0,cat=r.km<21?'Court':r.km<42?'Moyen':r.km<80?'Long':'Ultra';
  return{E,ratio,cat,diff:ratio<15?'Roulant':ratio<35?'Vallonné':ratio<60?'Montagneux':'Très technique / alpin'}}
const LK_ICO={
  site:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M3 12h18M12 3c2.6 2.7 3.9 5.7 3.9 9S14.600 18.300 12 21c-2.600-2.700-3.900-5.700-3.900-9S9.400 5.700 12 3z"/></svg>',
  src:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 17l5-6 4 4 4-7 5 9"/></svg>',
  bib:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="4" y="4" width="16" height="16" rx="3"/><path d="M8 10h8M8 14h5"/></svg>',
  rank:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M8 21h8M12 17v4M7 4h10v5a5 5 0 0 1-10 0zM7 6H4v1a3 3 0 0 0 3 3M17 6h3v1a3 3 0 0 1-3 3"/></svg>',
  runner:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="8" r="4"/><path d="M4 21c1-4 4-6 8-6s7 2 8 6"/></svg>'};
function linkBtns(site,src,runner,rank,bib){return extLink(site,'site','Site officiel','Site de la course')+extLink(src,'src','Strava','Ouvrir sur Strava')+extLink(bib,'bib','Dossard','Voir le dossard')+extLink(rank,'rank','Classement','Voir le classement')+extLink(runner,'runner','Mes résultats','Mon profil sur la course')}
function extLink(url,k,label,full){return url&&/^https?:\/\//i.test(url)?`<a class="lkb" href="${esc(url)}" target="_blank" rel="noopener noreferrer" title="${full}" aria-label="${full}">${LK_ICO[k]}<span>${label}</span></a>`:''}
function objBox(r,t,g,i){
  const info=`${pace(t/r.km)}/km · ${pace(t/i.E)}/km-effort${r.rank?` · classement ${esc(r.rank)}`:''}`;
  if(!g)return `<div class="note good objb"><div class="obj-h"><span class="obj-ico">⏱️</span><div><b>Temps réalisé : ${esc(r.result)}</b><br><span class="xs">${info}</span><br><span class="xs mut">Aucun objectif saisi pour cette course.</span></div></div></div>`;
  const diff=t-g,MARGE=10,ok=diff<=MARGE,near=Math.abs(diff)<=MARGE,cls=ok&&near?' obj-win':'';
  const msg=!ok?`Objectif manqué de ${fmtT(diff)}`:diff===0?'Objectif atteint pile à la minute !':diff<0?`Objectif atteint : ${fmtT(-diff)} d'avance`:`Objectif validé : ${fmtT(diff)} au-dessus, dans la marge de ${MARGE} min`;
  const ico=ok?(near?'🏆':'✅'):'🎯',sub=ok&&near?'🎉 Bravo, tu l\'as fait !':'';
  return `<div class="note ${ok?'good':''} objb${cls}"><div class="obj-h"><span class="obj-ico">${ico}</span><div><b>Objectif : ${esc(r.goal)}</b> · réalisé <b>${esc(r.result)}</b><br><span class="xs">${info}</span></div></div><div class="obj-s ${ok?'ok':'ko'}">${ok?'✅':'❌'} ${msg}${sub?` <span class="obj-sub">${sub}</span>`:''}</div></div>`}
const RH_PAL={'Roulant':['#4C7F5F','#17342A'],'Vallonné':['#36694F','#12281F'],'Montagneux':['#2A5240','#0E1D16'],'Très technique / alpin':['#B8531C','#2A1810']};
const RH_ICO={cal:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="5" width="18" height="16" rx="3"/><path d="M8 3v4M16 3v4M3 10h18"/></svg>',pin:'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 21s7-6.200 7-11.500A7 7 0 0 0 5 9.500C5 14.800 12 21 12 21z"/><circle cx="12" cy="9.500" r="2.500"/></svg>'};
function raceHeader(r,i,t,up){
  const d=dBetween(today(),r.date),pal=RH_PAL[i.diff]||RH_PAL['Roulant'],place=(r.place||'').trim();
  let art;
  if(Array.isArray(r.prof)&&r.prof.length>3){const ys=r.prof.map(q=>q[1]),lo=Math.min(...ys),hi=Math.max(...ys),gk=r.prof[r.prof.length-1][0]||1,pts=r.prof.map(q=>`${(q[0]/gk*400).toFixed(1)},${(112-(q[1]-lo)/Math.max(1,hi-lo)*70).toFixed(1)}`).join(' ');
    art=`<svg class="rh-art" viewBox="0 0 400 120" preserveAspectRatio="none" aria-hidden="true"><polygon points="0,120 ${pts} 400,120" fill="rgba(255,255,255,.16)"/><polyline points="${pts}" fill="none" stroke="rgba(255,255,255,.75)" stroke-width="1.6" vector-effect="non-scaling-stroke"/></svg>`}
  else art=`<svg class="rh-art" viewBox="0 0 400 120" preserveAspectRatio="none" aria-hidden="true"><path d="M0 120V84L60 54L96 74L170 22L226 64L290 38L352 72L400 56V120Z" fill="rgba(255,255,255,.14)"/><path d="M0 120V100L80 80L150 96L230 66L310 92L400 74V120Z" fill="rgba(255,255,255,.10)"/></svg>`;
  const st=r.status||(up?'Inscrit':'Passée'),stc=st==='DNF'?'bad':st==='DNS'?'mu':st==='Finisher'?'ok':st==='À confirmer'?'warn':'';
  const big=up?`<b class="cond">${d===0?'Jour J':'J-'+d}</b><small>avant le départ${r.startTime?` · ${esc(r.startTime)}`:''}</small>`:t?`<b class="cond">${esc(r.result)}</b><small>chrono${r.rank?` · classement ${esc(r.rank)}`:''}</small>`:'';
  const lk=linkBtns(r.site,r.src,r.runner,r.rankUrl,r.bibUrl);
  return `<header class="rh" style="--tc1:${pal[0]};--tc2:${pal[1]}">${art}
  <div class="rh-top"><span class="rh-pill ${stc}">${esc(st)}</span><span class="rh-pill">${r.kind==='route'?'Route':'Trail'}</span>${r.prio?`<span class="rh-pill">Objectif ${esc(r.prio)}</span>`:''}</div>
  <h2 class="cond rh-name">${esc(r.name)}</h2>
  <p class="rh-meta"><span>${RH_ICO.cal}${longD(r.date)}</span>${place?`<span>${RH_ICO.pin}${esc(place)}</span>`:''}</p>
  ${big||r.utmbCat?`<div class="rh-foot"><div class="rh-big">${big}</div>${r.utmbCat?`<div class="rh-utmb">${utmbLogo(r.utmbCat)}${r.utmbPts?`<small>${esc(r.utmbPts)} pts</small>`:''}</div>`:''}</div>`:''}
  ${lk?`<div class="lk rh-lk">${lk}</div>`:''}</header>`}
function raceStats(r,i){
  const hasD=r.dminus!=null&&r.dminus!=='';
  const c=[['📏','Distance',`${fn(r.km)}<small>km</small>`],['⛰️','Dénivelé +',`+${fn(r.dplus,0)}<small>m</small>`],['↘️','Dénivelé −',hasD?`−${fn(r.dminus,0)}<small>m</small>`:'—'],['⚡','Km-effort',`${fn(i.E,0)}`],['📐',i.diff,`${fn(i.ratio,0)}<small>m/km</small>`],['🏷️','Format',i.cat],['⏱️','Chrono',r.result?esc(r.result):'—'],['🎯','Objectif',r.goal?esc(r.goal):'—'],['🏆','Classement',r.rank?esc(r.rank):'—']];
  return `<div class="rs">${c.map(([ic,l,v])=>`<div><b>${v}</b><span><i aria-hidden="true">${ic}</i>${l}</span></div>`).join('')}</div>`}
function openRace(id){
  const r=D.races.find(x=>x.id===id);if(!r)return;S.goalsId=id;const i=raceInfo(r),t=parseT(r.result),g=parseT(r.goal),up=r.date>=today()&&!t;
  openModal(`${raceHeader(r,i,t,up)}${raceStats(r,i)}
  ${t?objBox(r,t,g,i):''}
  <div class="grid g2" style="margin:12px 0"><button class="quick" data-a="plan" data-id="${r.id}" data-t="nutri"><i>🍌</i><span><b>Nutrition de cette course</b><small class="mut">Plan du coach · semaine avant la course</small></span></button><button class="quick" data-a="plan" data-id="${r.id}" data-t="train"><i>🏃</i><span><b>Plan d'entraînement de cette course</b><small class="mut">Plan du coach · semaine par semaine</small></span></button></div>
  ${up?`<div class="row" style="margin:10px 0"><button class="btn lime s" data-a="fiche" data-id="${r.id}">🏁 Fiche jour J</button></div>`:''}
  ${profileBlock(r)}
  ${goalsBlock(r)}
  ${filesBlock(r)}<details class="card hist fold editrace">${foldHead('✏️','Modifier la course','Infos, objectif, statut, GPX')}<div style="margin-top:12px">${raceForm(r)}</div></details>`);initGpx(r.id);loadFiles(r.id);const _w=$('.objb.obj-win');if(_w)setTimeout(()=>burstAt($('.objb.obj-win .obj-ico')),350)}
/* Dossard & classement : liens validés (boutons en haut de la course). */
const filesBlock=r=>`<details class="card hist fold" id="rfiles">${foldHead('🎽','Dossard & classement',[r.bibUrl&&'Dossard',r.rankUrl&&'Classement'].filter(Boolean).join(' · ')||'Ajoute tes liens')}<div id="rf-body" class="sm mut">Chargement…</div></details>`;
async function loadFiles(id){
  if(!$('#rf-body'))return;
  const rc=D.races.find(x=>x.id===id)||{},box=$('#rf-body'),
    lnk=(k,t,ph)=>{const u=rc[k+'Url']||'';return `<h3 class="cond" style="margin:18px 0 6px">${t}</h3><label class="f"><input id="lk-${k}" type="url" inputmode="url" placeholder="${ph}" value="${esc(u)}"></label><div class="row" style="margin-top:8px"><button type="button" class="btn s" data-a="rankSave" data-k="${k}" data-id="${esc(id)}">✅ Valider le lien</button>${u?`<a class="btn ghost s" href="${esc(u)}" target="_blank" rel="noopener noreferrer">Ouvrir</a><button type="button" class="btn red s" data-a="rankDel" data-k="${k}" data-id="${esc(id)}">Retirer</button>`:''}</div>`};
  if(!box||S.goalsId!==id)return;
  box.className='';
  box.innerHTML=`${lnk('bib','Lien du dossard','https://… (page du dossard)')}${lnk('rank','Lien du classement','https://… (page des résultats)')}
  <p class="xs mut" style="margin-top:10px">Une fois validé, chaque lien devient un bouton (« Dossard », « Classement ») en haut de la course.</p>`}
function goalsBlock(r){return `<div id="goalsbox"><details class="card hist fold">${foldHead('🎯','Objectifs de course','Chronos cibles calculés pour cette course')}<p class="xs mut" style="margin-bottom:10px">Calculés automatiquement d'après ton profil, tes courses passées, le tracé GPX et les réglages de la course : ils se mettent à jour dès que tu enregistres la course ou que tu bouges le ressenti du moment.</p>${goalsHTML(r)}</details></div>`}
function refreshGoals(){const gb=$('#goalsbox'),gr=gb&&D.races.find(x=>x.id===S.goalsId);if(!gr)return;const st=[...gb.querySelectorAll('details')].map(d=>d.open);gb.outerHTML=goalsBlock(gr);[...$('#goalsbox').querySelectorAll('details')].forEach((d,i)=>{d.open=!!st[i]})}
function syncAll(){save();refreshGoals();S.keep=true;if(S.tab!=='profile')render()}
// Coût relatif de chaque portion du tracé GPX (modèle énergétique pente / coût de Minetti, descentes plafonnées car techniques) + dérive de fatigue.
function gradeCost(g){const x=Math.max(-.4,Math.min(.4,g)),c=((((155.4*x-30.4)*x-43.3)*x+46.3)*x+19.5)*x+3.6,f=c/3.6;return x<0?Math.max(.75,f):f}
function trailCost(r){
  const p=r.prof;if(!Array.isArray(p)||p.length<4)return null;const gk=p[p.length-1][0];if(!(gk>0))return null;
  const E=effKm(r),Lr=timed().filter(x=>dBetween(x.date,today())<=730).reduce((m,x)=>Math.max(m,effKm(x)),0)||30,drift=Math.min(.2,.04+.1*Math.max(0,E/Lr-1));
  let u0=0;for(let i=1;i<p.length;i++)u0+=Math.max(0,p[i][1]-p[i-1][1]);
  const sc=(+r.dplus>0&&u0>0)?Math.max(1,Math.min(2,r.dplus/u0)):1,cum=[0],up=[0];let tot=0,u=0;
  for(let i=1;i<p.length;i++){const d=p[i][0]-p[i-1][0],dz=p[i][1]-p[i-1][1];
    if(d>0){tot+=d*gradeCost(dz*sc/(d*1000))*(1+drift*((p[i][0]+p[i-1][0])/2/gk));if(dz>0)u+=dz}
    cum.push(tot);up.push(u)}
  const k=(+r.dplus>0&&u>0)?r.dplus/u:1,lerp=(arr,km)=>{if(km<=0)return 0;if(km>=gk)return arr[arr.length-1];let i=1;while(i<p.length-1&&p[i][0]<km)i++;const a=p[i-1][0],b=p[i][0],w=b>a?(km-a)/(b-a):1;return arr[i-1]+(arr[i]-arr[i-1])*w};
  return{gk,drift,total:tot,at:km=>tot>0?lerp(cum,km)/tot:km/gk,dp:km=>lerp(up,km)*k}}
const hypGpx=r=>{const tc=trailCost(r);return tc?`<li>Tracé GPX : temps réparti d'après la pente de chaque portion (${r.prof.length} points), dérive de fatigue de +${fn(tc.drift*100,0)} % sur la durée (selon ta plus longue course récente).</li>`:'<li>Pas de GPX : temps réparti selon le km-effort (ajoute le GPX pour un découpage fidèle au tracé).</li>'};
// Infos GPX (départ / arrivée, km-effort, plus longue montée / descente, altitudes, qualité du tracé)
function gpxStats(r){
  const p=r.prof,secs=profSections(p),gk=p[p.length-1][0],ys=p.map(q=>q[1]),gx=r.gx||{};
  const dp=gx.dp!=null?gx.dp:Math.round(+r.dplus||0),dm=gx.dm!=null?gx.dm:(r.dminus!==''&&r.dminus!=null?Math.round(+r.dminus):null);
  const big=a=>a.reduce((m,x)=>!m||x.d>m.d?x:m,null),lu=big(secs.filter(x=>x.type==='montée')),ld=big(secs.filter(x=>x.type==='descente'));
  const kv=[[fn(gk+dp/100,0),'km-effort'],lu?[`+${lu.up} m`,`plus longue montée · ${fn(lu.d,1)} km`]:null,ld?[`−${ld.dn} m`,`plus longue descente · ${fn(ld.d,1)} km`]:null,[`${Math.max(...ys)} m`,'altitude max'],[`${Math.min(...ys)} m`,'altitude min'],[gx.q?`1 pt / ${gx.q} m`:'—','qualité du tracé']].filter(Boolean);
  return `<div class="kv">${kv.map(([b,l])=>`<div><b>${b}</b><span>${l}</span></div>`).join('')}</div>
  <div class="tscroll" style="margin-top:10px"><table class="nw"><thead><tr><th></th><th>Distance</th><th>Altitude</th><th>D+</th><th>D−</th></tr></thead><tbody><tr><td><b>Départ</b></td><td>0 km</td><td>${ys[0]} m</td><td>0 m</td><td>0 m</td></tr><tr><td><b>Arrivée</b></td><td>${fn(gk,1)} km</td><td>${ys[ys.length-1]} m</td><td>${fn(dp,0)} m</td><td>${dm==null?'—':fn(dm,0)+' m'}</td></tr></tbody></table></div>`}
const UTMB_CATS=['20K','50K','100K','100M'];
/* Pastilles de catégorie UTMB (SVG intégré). Pour utiliser les fichiers officiels, remplace simplement le contenu de utmbLogo(). */
function utmbLogo(c){
  if(!UTMB_CATS.includes(c))return c?`<span>UTMB ${esc(c)}</span>`:'';
  return `<svg class="ulogo" viewBox="0 0 64 72" role="img" aria-label="UTMB ${c}"><path d="M6 8Q6 4 10 4H54Q58 4 58 8V46Q58 58 32 68Q6 58 6 46Z" fill="#101A15" stroke="#F2EFE4" stroke-width="2"/><text x="32" y="17" text-anchor="middle" font-size="8" font-weight="800" letter-spacing="1.6" fill="#F2EFE4" font-family="system-ui,sans-serif">UTMB</text><path d="M13 38L23 25L28 31L36 21L51 38Z" fill="#F27A2A"/><text x="32" y="53" text-anchor="middle" font-size="14" font-weight="900" fill="#F2EFE4" font-family="system-ui,sans-serif">${c}</text></svg>`}
function utmbPicker(cur){return `<div class="f full"><span>Catégorie UTMB <span class="xs" style="font-weight:500">(touche à nouveau pour désélectionner)</span></span><div class="ucats" role="radiogroup" aria-label="Catégorie UTMB">${UTMB_CATS.map(c=>`<button type="button" class="ucat${cur===c?' on':''}" role="radio" aria-checked="${cur===c}" data-a="utmbPick" data-v="${c}" aria-label="UTMB ${c}">${utmbLogo(c)}</button>`).join('')}</div><input type="hidden" id="r-utmbcat" value="${esc(cur||'')}"></div>`}
function raceForm(r){const v=k=>esc(r[k]==null?'':r[k]),sel=(id,opts,val,lab=o=>o||'—')=>`<select id="${id}">${opts.map(o=>`<option value="${esc(o)}" ${o===val?'selected':''}>${esc(lab(o))}</option>`).join('')}</select>`;
  const ST=['Inscrit / à venir','À confirmer','Finisher','DNF','DNS'];
  return `<div class="frm"><label class="f full">Nom<input id="r-name" value="${v('name')}"></label><label class="f full">Lieu (ville, pays) — pour la carte<input id="r-place" placeholder="ex. Chamonix, France" value="${v('place')}"></label>
  ${pkField('r-date','date',r.date||'','','Date')}
  <label class="f">Type<select id="r-kind"><option value="trail" ${(r.kind||'trail')==='trail'?'selected':''}>Trail</option><option value="route" ${r.kind==='route'?'selected':''}>Route</option></select></label>
  <label class="f">Priorité (saison)<select id="r-prio">${['','A','B','C'].map(k=>`<option value="${k}" ${(r.prio||'')===k?'selected':''}>${k?k+' · '+PRIO[k]:'—'}</option>`).join('')}</select></label>
  <label class="f">Statut<select id="r-status">${ST.map(o=>`<option ${((r.status||'Inscrit / à venir')===o)?'selected':''}>${o}</option>`).join('')}</select></label>
  <label class="f">Distance (km)<input id="r-km" type="number" step="any" inputmode="decimal" value="${v('km')}"></label><label class="f">D+ (m)<input id="r-dplus" type="number" step="any" inputmode="decimal" value="${v('dplus')}"></label><label class="f">D− (m)<input id="r-dminus" type="number" step="any" inputmode="decimal" value="${v('dminus')}"></label><label class="f">Objectif chrono<input id="r-goal" placeholder="ex. 11h ou 1h38" value="${v('goal')}"></label>
  <label class="f">Chrono réel<input id="r-result" placeholder="ex. 6h34'59" value="${v('result')}"></label>  <label class="f full">Site de la course (lien)<input id="r-site" type="url" inputmode="url" placeholder="https://…" value="${v('site')}"></label>
  <label class="f full">Lien Strava (activité)<input id="r-src" type="url" inputmode="url" placeholder="https://www.strava.com/activities/…" value="${v('src')}"></label>
  <label class="f full">Profil du coureur (lien vers ta page / tes résultats sur cette course)<input id="r-runner" type="url" inputmode="url" placeholder="https://…" value="${v('runner')}"></label>
  ${utmbPicker(r.utmbCat||'')}<label class="f">Points UTMB (libre)<input id="r-utmbpts" placeholder="ex. 2 ou 1,5 + 0,5" value="${v('utmbPts')}"></label>
  <p class="full cond" style="margin-top:10px;color:var(--acc2)">Questionnaire objectif</p>
  ${pkField('r-time','time',r.startTime||'','','Heure de départ')}<label class="f">Conditions particulières${sel('r-cond',['',...Object.keys(CF)],r.cond||'')}</label><label class="f">État physique actuel${sel('r-phys',['',...Object.keys(QF)],r.phys||'')}</label></div>
  <div class="row" style="margin-top:14px"><button class="btn" data-a="saveRace" data-id="${r.id||''}">💾 Enregistrer</button>${r.id&&D.races.some(x=>x.id===r.id)?`<button class="btn red" data-a="delRace" data-id="${r.id}">🗑️ Supprimer</button>`:''}</div><div id="r-err" class="sm" style="color:var(--bad);margin-top:8px" role="alert"></div>`}
function newRace(pre){openModal(`<h2 class="cond">Ajouter une course</h2><p class="mut sm" style="margin-bottom:10px">Passée ou à venir : les statistiques, plans et chronos cibles se mettent à jour.</p>${raceForm(Object.assign({id:'',name:'',date:'',km:'',dplus:'',dminus:'',goal:'',status:'',result:'',rank:'',notes:'',startTime:'',cond:'',condNote:'',phys:'',site:'',src:'',utmbCat:'',utmbPts:''},pre||{}))}`)}
function saveRace(id){
  const g=k=>($('#r-'+k).value||'').trim(),err=m=>{$('#r-err').textContent=m};
  const name=g('name'),date=g('date'),km=parseFloat(g('km')),dp=parseFloat(g('dplus'));
  if(!name)return err('Donne un nom à la course.');if(!/^\d{4}-\d{2}-\d{2}$/.test(date))return err('Choisis la date.');if(!(km>0))return err('Indique la distance.');if(!(dp>=0))return err('Indique le D+ (0 si plat).');
  if(g('time')&&!/^\d{2}:\d{2}$/.test(g('time')))return err('Heure de départ illisible.');
  if(g('site')&&!/^https?:\/\//i.test(g('site')))return err('Le lien du site doit commencer par https://');
  if(g('src')&&!/^https?:\/\//i.test(g('src')))return err('Le lien Strava doit commencer par https://');
  if(g('runner')&&!/^https?:\/\//i.test(g('runner')))return err('Le lien du profil coureur doit commencer par https://');
  if(g('result')&&!parseT(g('result')))return err("Chrono illisible : écris par exemple 6h34'59 ou 1h38.");
  if(g('goal')&&!parseT(g('goal')))return err("Objectif illisible : écris par exemple 11h30.");
  const dm=g('dminus'),o={name,place:g('place'),noJ7:!!(id&&(D.races.find(x=>x.id===id)||{}).noJ7),date,km,dplus:dp,dminus:dm===''?null:parseFloat(dm),goal:g('goal'),status:g('status')==='Inscrit / à venir'?'':g('status'),result:g('result'),kind:g('kind')||'trail',startTime:g('time'),cond:g('cond'),phys:g('phys'),site:g('site'),src:g('src'),runner:g('runner'),utmbCat:g('utmbcat'),utmbPts:g('utmbpts'),prio:g('prio')};
  if(id){Object.assign(D.races.find(x=>x.id===id),o)}else{const r=Object.assign({id:uid()},o,S.pendProf?{prof:S.pendProf,trk:S.pendTrk||undefined}:{});S.pendProf=null;S.pendTrk=null;D.races.push(r);S.sel=r.id}
  const rr=D.races.find(x=>x.id===(id||S.sel));save();closeModal();toast('Course enregistrée : objectifs, plans et prédicteur sont recalculés.');if(rr&&(rr.place||'').trim()&&rr.geoFor!==rr.place.trim()){geocodeRace(rr.id).then(ok=>{if(ok)render()})}render()}

/* ============================ ENTRAÎNEMENT ============================ */
const ZN=[['Z1','Récupération',.50,.60,.50,.59,'Très facile, conversation fluide'],['Z2','Endurance fondamentale',.60,.70,.59,.70,'Facile, phrases complètes'],['Z3','Tempo / allure ultra',.70,.80,.72,.82,'Soutenu, phrases courtes'],['Z4','Seuil',.80,.90,.83,.89,'Dur, quelques mots'],['Z5','VMA / puissance',.90,1,.90,1,'Très dur, aucun mot']];
const zr=z=>ZN.find(x=>x[0]===z);
function zhr(z){const p=D.profile,res=p.hrMax-p.hrRest,r=zr(z);return[Math.round(p.hrRest+res*r[2]),Math.round(p.hrRest+res*r[3])]}
const hrS=z=>{const a=zhr(z);return `${z} · ${a[0]}–${a[1]} bpm`};
const hrR=(a,b)=>`${a}–${b} · ${zhr(a)[0]}–${zhr(b)[1]} bpm`;
function pAt(f){const target=baseVdot()*f;let lo=40,hi=520;for(let i=0;i<50;i++){const v=(lo+hi)/2;vo2(v)<target?lo=v:hi=v}return 1000/((lo+hi)/2)}
const prs=(a,b)=>`${pace(a).replace('"','')}–${pace(b).replace('"','')}/km`;
function zps(z){const r=zr(z);return prs(pAt(r[5]),pAt(r[4]))}
const rr=(x,s=1)=>Math.round(x/s)*s,k1=x=>Math.round(x*10)/10,ceilDur=m=>Math.max(5,Math.round(m/5)*5);
const PAIN=[['none','Aucune douleur'],['light','Gêne légère (disparaît à l\'échauffement)'],['moderate','Douleur modérée (modifie ma foulée)'],['strong','Douleur forte (j\'ai dû m\'arrêter)']];
const PZONES=['Genou','Tendon d\'Achille','Mollet','Tibia','Hanche / fessier','Bande ilio-tibiale','Pied / voûte','Dos','Autre'];
const PZT={'Genou':'renforce quadriceps et fessiers (step-down lent 3×8, abducteurs 3×15), évite les descentes appuyées.','Tendon d\'Achille':'montées de mollets excentriques 3×15 lentes, évite les côtes raides et le travail de vitesse.','Mollet':'mobilité de cheville, auto-massage doux, montées de mollets légères ; pas de sprint.','Tibia':'réduis l\'impact (terrain souple), renforce le tibial antérieur 3×15, vérifie tes chaussures.','Hanche / fessier':'pont unijambiste 3×12, abduction élastique 3×15, mobilité de hanche 10\'.','Bande ilio-tibiale':'renforce le moyen fessier (abductions, clam shells), rouleau sur le fascia latéral, évite les dévers prolongés.','Pied / voûte':'renforcement du pied court 2×10, marche pieds nus sur terrain souple, vérifie l\'usure des chaussures.','Dos':'gainage 3×40", mobilité thoracique, évite de te pencher en côte (regard loin, buste gainé).','Autre':'note précisément où et quand ça fait mal, et consulte un professionnel si ça persiste.'};

function raceSelect(){const rs=D.races.slice().sort((a,b)=>a.date<b.date?1:-1),cur=selRace();return `<div class="sel"><label class="mut sm" for="selR">Course :</label><select id="selR" data-c="sel">${rs.map(r=>`<option value="${r.id}" ${cur&&cur.id===r.id?'selected':''}>${esc(r.name)} — ${shortD(r.date)}${r.date<today()?' (passée)':''}</option>`).join('')}</select></div>`}
function ensurePlan(r){D.plans=D.plans||{};let p=D.plans[r.id];if(!p){const mR=monday(r.date);let st=monday(today());const lim=addD(mR,-29*7);if(st<lim)st=lim;p=D.plans[r.id]={start:st,created:today()};save()}
  return{start:p.start,created:p.created,base:Math.round(Math.max(10,+D.profile.weeklyKm||30)),src:'ton profil'}}

function fbEffect(b,b0){
  const o={f:1,rec:false,noInt:0,noDown:0,stop:false,run:null,gym:null,long:0,notes:[]};
  const fat=+b.fatigue||3,sen=+b.sens||3,sl=+b.sleep||3,dn=(b.done===''||b.done==null)?100:+b.done,pain=b.pain||'none',fat0=b0?(+b0.fatigue||3):3,z=b.zone?` (${b.zone})`:'';
  if(pain==='strong'){o.f=.65;o.stop=true;o.noInt=2;o.noDown=3;o.notes.push(`Douleur forte${z} : course remplacée par du cross-training sans impact cette semaine. Consulte un kiné ou un médecin du sport avant de reprendre l'intensité.`)}
  else if(pain==='moderate'){o.f=.8;o.noInt=2;o.noDown=2;o.notes.push(`Douleur modérée${z} : aucune intensité ni descente appuyée pendant 2 semaines, volume −20 %.`)}
  else if(pain==='light'){o.noDown=1;o.notes.push(`Gêne légère${z} : pas de descente appuyée cette semaine, prévention ciblée ajoutée.`)}
  if(!o.stop){
    if(fat>=5||(fat>=4&&fat0>=4)){o.rec=true;o.f=Math.min(o.f,.85);o.notes.push(`Fatigue élevée (${fat}/5${fat0>=4&&fat<5?', 2e semaine de suite':''}) : semaine de récupération (−35 % de volume), puis reprise progressive.`)}
    else if(fat>=4||sen<=2||dn<70){o.f=Math.min(o.f,.88);o.notes.push(`${fat>=4?'Fatigue '+fat+'/5':sen<=2?'Mauvaises sensations':'Séances manquées ('+dn+' % réalisées)'} : charge −12 %.`)}
    else if(fat<=2&&sen>=4&&dn>=90&&sl>=3&&pain==='none'){o.f=1.05;o.notes.push('Très bonne assimilation : charge +5 % (plafonnée à +10 % par semaine).')}
    else if(pain==='none')o.notes.push('Bonne assimilation : progression prévue maintenue.')}
  if(sl<=2)o.notes.push('Sommeil insuffisant : vise 8 h cette semaine, c\'est ton premier levier de récupération.');
  if(b.availRun)o.run=+b.availRun;if(b.availGym!==''&&b.availGym!=null)o.gym=+b.availGym;if(b.availLong)o.long=+b.availLong;
  if(b.constraints)o.notes.push('Contrainte notée : '+b.constraints);
  return o}

function mkGym(c,kind,o){const g=D.profile.gym||'Salle';
  const K={
   force:['Renfo jambes — force maximale',55,'7–8/10',`${g} · échauffement 8' (vélo + mobilité). Presse à cuisses (ou squat goblet) 4×6 · Soulevé de terre roumain 3×8 · Fentes bulgares 3×8/jambe · Hip thrust 4×8 · Mollets debout 4×8 (montée 2 s, descente 3 s) · Gainage latéral + planche 3×35". Repos 1'30–2'.`],
   fe:['Renfo trail — force-endurance',55,'7/10',`${g} · échauffement 8'. Step-up sur box haute lesté 4×10/jambe · Fentes marchées 3×12 · Leg curl 3×12 · Hip thrust unijambiste 3×10 · Mollets assis (soléaire) 3×15 · Planche dynamique + Pallof press 3×12. Repos 1'15.`],
   ecc:['Renfo trail — excentrique & descente',50,'7/10',`${g} · échauffement 8'. Step-down excentrique (descente 4 s) 4×8/jambe · Presse excentrique 3×8 (descente 4 s) · Fentes arrière 3×10 · Nordic curl assisté 3×6 · Tibial antérieur 3×15 · Mollets excentriques 3×12 · Proprioception sur plateau instable 5'. Repos 1'30.`],
   ent:['Renfo d\'entretien',30,'5/10',`${g} · Presse 2×8 légère · Hip thrust 2×8 · Fentes 2×8 · Gainage 2×30". Reste très loin de l'échec : tu dois sortir plus frais qu'en entrant.`],
   prev:['Prévention, gainage & proprioception',40,'4–5/10',`${g} · Gainage (planche, latéral, bird-dog) 3×40" · Pallof press 3×12 · Abducteurs/adducteurs machine 3×15 · Pont unijambiste 3×12 · Proprio sur plateau instable 2×1' par pied · Mobilité hanches-chevilles 8'.`]}[kind];
  return{ty:'gym',o,title:a0(K),focus:'Renfo',dur:c.deload?ceilDur(K[1]*.8):K[1],km:0,dp:0,hr:'—',pace:'—',rpe:K[2],desc:K[3]}}
const a0=K=>K[0];
function mkEasy(km,o,dp,title,extra){const ep=easyPace();
  return{ty:'run',o,title:title||'Footing endurance',focus:dp>60?'Plat + relief':'Plat',dur:ceilDur(km*ep*1.03+dp/12),km:k1(km),dp:rr(dp,10),hr:hrS('Z2'),pace:zps('Z2'),rpe:'3–4/10',desc:`Footing en aisance respiratoire, Z2 stricte (ne dépasse pas ${zhr('Z2')[1]} bpm, même en côte : marche si besoin). ${extra||'Termine par 4–6 lignes droites de 20" progressives et quelques éducatifs (montées de genoux, talons-fesses).'}`}}
function mkLong(c,kmRaw,dp,o){
  const ep=easyPace(),f=dp>0?1.15:1.06;let km=kmRaw,dur=(km+dp/100)*ep*f;
  const cap=Math.min(c.longMax||999,c.E>=100?300:c.E>=55?270:c.E>=30?210:c.E>=15?150:120);
  if(dur>cap){dur=cap;km=Math.max(5,dur/(ep*f)-dp/100)}
  const ph=c.phase;let body;
  if(c.tp)body=`Sortie allégée en Z2, sensations avant tout : tu dois finir en voulant continuer.`;
  else if(ph==='Base'||c.deload||c.rec)body=`Z2 continue sur terrain roulant, allure régulière. Hydratation 400–500 ml/h, 1 gel ou ~30 g de glucides par 45'.`;
  else if(ph==='Développement')body=`Z2 avec 3 × 10' de montée soutenue en Z3 au milieu, dernières 20' en Z2 stable. Alimentation 50–60 g de glucides/h.`;
  else body=c.ultra?`Allure ultra : Z2 haute / Z3 bas, marche rapide dans les montées raides, relance contrôlée en descente. Teste ta stratégie de course (${c.fuelTxt}), ton sac, tes ${D.profile.shoes||'chaussures'}.`:`Allure d'endurance avec 2 × 20' à effort course (Z3). Teste nutrition (${c.fuelTxt}) et matériel.`;
  if(c.steep&&!c.noDown&&!c.tp&&(ph==='Développement'||ph==='Spécifique'))body+=` Descente : 4 × 3' contrôlées (cadence haute, genoux souples, regard 3 m devant).`;
  if(dp>0)body+=` D+ ≈ ${rr(dp,50)} m : sentier vallonné, escaliers, ponts ou blocs sur tapis incliné (10–12 %) si ton terrain est plat.`;
  if(!c.noDown&&!c.tp&&(ph==='Développement'||ph==='Spécifique')&&c.i%2===0)body+=` Une fois sur deux, vise un sentier technique (racines, cailloux) sur ~30 % du parcours ; sinon travaille la proprioception en salle.`;
  const key=ph==='Spécifique'&&c.i===c.keyLong&&!c.deload&&!c.rec;
  return{ty:'run',o,title:key?'Sortie longue clé — répétition générale':'Sortie longue',focus:dp>0?'Endurance + D+':'Endurance',dur:ceilDur(dur),km:k1(km),dp:rr(dp,50),hr:hrS('Z2')+' (Z3 en côte)',pace:zps('Z2')+' sur plat ; à l\'effort en côte',rpe:'4–5/10',desc:body}}
function qualSession(c,type){
  const ep=easyPace(),w=15,cd=10,easyKm=m=>m/(ep*1.03),dpT=Math.max(40,c.T*.4);
  const wu=`Échauffement ${w}' en Z1–Z2 + 3 lignes droites`,cdn=`retour au calme ${cd}' en Z1`,B={ty:'run',o:1,dp:0};
  if(type==='hillshort'){const per=9,reps=Math.max(6,Math.min(12,Math.round(dpT/per)));
    return Object.assign(B,{title:'Côtes courtes — puissance',focus:'Montée',dur:ceilDur(w+cd+reps*2.25),km:k1(easyKm(w+cd)+reps*.25),dp:rr(reps*per,10),hr:hrR('Z4','Z5'),pace:'À l\'effort (pas d\'allure)',rpe:'8/10',desc:`${wu} · ${reps} × 45" en côte raide (8–10 %) ou sur tapis incliné 10–12 % (8–9 km/h), effort 8/10 · récupération 1'30 en descente trottinée · ${cdn}. Foulée courte et active, buste droit, bras puissants.`})}
  if(type==='hilllong'){const rd=c.prog<.5?6:c.prog<.8?8:10,per=rd*10,reps=Math.max(3,Math.min(8,Math.round(dpT/per)));
    return Object.assign(B,{title:'Montées longues — spécifique',focus:'Montée',dur:ceilDur(w+cd+reps*(rd+3)),km:k1(easyKm(w+cd)+reps*(rd/60*6+.3)),dp:rr(reps*per,10),hr:hrR('Z3','Z4'),pace:'Marche rapide / trot lent (≈ 6 km/h en pente)',rpe:'6–7/10',desc:`${wu} · ${reps} × ${rd}' de montée soutenue (tapis 10–12 % à 5,5–6,5 km/h, escaliers ou côte), effort 6–7/10 régulier, bâtons si tu en prévois en course · récupération 3' en descente marchée · ${cdn}. Objectif : cadence stable du début à la fin.`})}
  if(type==='tempo'){const nb=c.prog<.4?2:3,d=rr(6+4*c.prog,1)+(c.ultra?4:0),z=c.ultra?'Z3':'Z4';
    return Object.assign(B,{title:c.ultra?'Allure ultra — blocs soutenus':'Tempo / seuil',focus:'Plat',dur:ceilDur(w+cd+nb*(d+3)),km:k1(easyKm(w+cd+nb*3)+nb*d/pAt(z==='Z3'?.77:.86)),hr:hrS(z),pace:zps(z),rpe:z==='Z3'?'6/10':'7–8/10',desc:`${wu} · ${nb} × ${d}' en ${z} (${zps(z)}), récupération 3' de trot en Z1 · ${cdn}. Régularité avant vitesse : le dernier bloc doit être aussi fluide que le premier.`})}
  if(type==='vma'){const reps=8+Math.round(c.prog*2);
    return Object.assign(B,{title:'VMA courte',focus:'Plat',dur:ceilDur(w+cd+reps*2),km:k1(easyKm(w+cd)+reps*(1/pAt(.97)+1/(ep*1.3))),hr:hrR('Z4','Z5'),pace:zps('Z5'),rpe:'8–9/10',desc:`${wu} · ${reps} × 1' en Z5 (${zps('Z5')}) / 1' de trot lent · ${cdn}. Reste relâché : les répétitions doivent toutes être identiques.`})}
  if(type==='racepace'){const nb=3,d=rr(10+5*c.prog,1),pe=`${pace(c.raceMin/c.E).replace('"','')}/km-effort`;
    return Object.assign(B,{title:'Allure course — simulation',focus:c.steep?'Montée + plat':'Plat',dur:ceilDur(w+cd+nb*(d+4)),km:k1(easyKm(w+cd+nb*4)+nb*d/pAt(.77)),dp:c.steep?rr(dpT,10):0,hr:hrS('Z3'),pace:`≈ ${pe} (Z3 : ${zps('Z3')})`,rpe:'6/10',desc:`${wu} · ${nb} × ${d}' à l'effort course (≈ ${pe}), ${c.steep?'dont 40 % en montée (tapis 6–8 % ou côte), ':''}récupération 4' de trot · ${cdn}. Mange et bois comme en course (${c.fuelTxt}).`})}
  if(type==='rappel')return Object.assign(B,{title:'Rappel d\'allure (affûtage)',focus:'Plat',dur:40,km:k1(40/(ep*1.03)),hr:hrR('Z2','Z3'),pace:zps('Z3'),rpe:'5–6/10',desc:`15' en Z2 · 3 × 3' à l'effort course (Z3), récupération 2' · 8' en Z1–Z2. Court et vif : tu gardes la fraîcheur.`});
  return Object.assign(B,{title:'Footing + vivacité',focus:'Plat',dur:40,km:k1(40/(ep*1.03)),hr:hrS('Z2'),pace:zps('Z2'),rpe:'3–4/10',desc:`30' en Z2 + 6 lignes droites de 20" souples (sans forcer). Une touche de vivacité sans fatigue, pour garder la mécanique.`})}
function pickQual(c){const i=c.i,ph=c.phase;let t;
  if(c.rec||c.deload)t='strides';else if(c.tp)t='rappel';else if(c.noInt)t='easyonly';
  else if(ph==='Base')t=c.steep?(i%2?'tempo':'hillshort'):(i%2?'vma':'tempo');
  else if(ph==='Développement')t=c.steep?['hillshort','tempo','hilllong'][i%3]:(i%2?'tempo':'vma');
  else t=c.steep?(i%2?'racepace':'hilllong'):'racepace';
  if(c.ultra&&t==='vma')t='tempo';return t}

function raceWeek(c,add){
  const r=c.r,ro=dow(r.date),ep=easyPace(),z2=zps('Z2'),act=(o,title,dur,desc,ty,hr)=>{if(o>=0&&o<ro)add({ty:ty||'run',o,title,focus:ty==='gym'?'Renfo':'Plat',dur,km:ty==='gym'?0:k1(dur/(ep*1.03)),dp:0,hr:hr||hrS('Z2'),pace:ty==='gym'?'—':z2,rpe:'3/10',desc})};
  act(ro-5,'Footing facile + lignes droites',35,`35' en Z2 + 5 lignes droites de 20". Teste ton sac, tes flasques et ta tenue complète.`);
  act(ro-4,'Mobilité & gainage léger',20,`20' de gainage et mobilité hanches-chevilles. Aucune série lourde.`,'gym','—');
  act(ro-3,'Rappel d\'allure',35,`10' en Z2 · 3 × 2' à l'allure course (effort 6/10), récupération 2' · 8' en Z2.`,'run',hrR('Z2','Z3'));
  act(ro-1,'Veille : décrassage',20,`15–20' très faciles + 3 lignes droites. Prépare dossard, nutrition, vêtements. Dîner tôt, riche en glucides, peu de fibres.`);
  const pe=`${pace(c.raceMin/c.E).replace('"','')}/km-effort`;
  add({ty:'race',o:ro,race:true,title:'🏁 '+r.name,focus:'Course',dur:Math.round(c.raceMin),km:+r.km,dp:+r.dplus,hr:hrR('Z2','Z3'),pace:`≈ ${pe}`,rpe:'6/10',desc:`Premier tiers en Z2 (aucun regret en partant trop vite), marche rapide dans les montées raides, alimentation dès 30' (${c.fuelTxt}), relance dans le dernier tiers.`})}

function buildWeek(c){
  const S2=[],add=s=>{s.d=addD(c.ws,s.o);s.key=s.d+'|'+s.ty+'|'+s.o;S2.push(s)};
  if(c.race)raceWeek(c,add);
  else if(c.stop){
    add({ty:'cross',o:1,title:'Cross-training sans impact',focus:'Récup',dur:40,km:0,dp:0,hr:hrS('Z2'),pace:'—',rpe:'3/10',desc:'Vélo, elliptique ou natation 40\' en Z2, sans douleur. Si ça fait mal : stop.'});
    add(mkGym(c,'prev',3));S2[S2.length-1].dur=30;S2[S2.length-1].desc+=' (Évite tout exercice qui réveille la douleur.)';
    add({ty:'cross',o:5,title:'Cross-training doux',focus:'Récup',dur:30,km:0,dp:0,hr:hrS('Z1'),pace:'—',rpe:'2/10',desc:'30\' vélo ou natation très facile.'});
    add({ty:'cross',o:6,title:'Marche active',focus:'Récup',dur:45,km:0,dp:0,hr:hrS('Z1'),pace:'—',rpe:'2/10',desc:'45\' de marche sur terrain souple. Reprise de la course seulement sans douleur au quotidien.'})}
  else{
    const nRun=Math.max(2,Math.min(4,c.runN)),nGym=Math.max(0,Math.min(2,c.gymN)),share=nRun>=4?.36:nRun===3?.40:.5;
    const type=pickQual(c);
    const q=type==='easyonly'?Object.assign(mkEasy(Math.max(5,c.vol*.25),1,0,'Footing Z2 (intensité suspendue)','Pas de séance intense cette semaine : reste en Z2 + 4 lignes droites très souples.')):qualSession(c,type);q.o=1;
    const rem=Math.max(8,c.vol-q.km-(nRun>=4?Math.min(6,c.vol*.12):0)),L=mkLong(c,nRun>=3?rem*.58:rem,rr(c.T*.45,50),6);
    add(q);
    if(nRun>=3){let satKm=0;const sat=nRun>=4;if(sat)satKm=c.ultra&&c.phase==='Spécifique'&&!c.deload&&!c.rec?Math.min(c.vol*.2,12):Math.min(6,c.vol*.12);
      const easyKm=Math.max(4,Math.min(c.vol-q.km-L.km-satKm,L.km*.7));
      add(mkEasy(easyKm,2,rr(c.T*(q.dp>0?.15:.4),10)));
      if(sat)add(mkEasy(Math.max(3,satKm),5,0,c.ultra&&c.phase==='Spécifique'?'Footing J1 — fatigue cumulée':'Footing d\'activation',c.ultra&&c.phase==='Spécifique'?'À enchaîner la veille de la longue : jambes déjà fatiguées, allure très facile.':'Court et facile : tu veux des jambes fraîches pour demain.'))}
    add(L);
    if(nGym>=1&&!(c.tp&&c.k===c.taperN-1&&c.taperN>=1&&c.k>0)){
      const heavy=c.rec?'prev':(c.deload||c.tp)?'ent':c.phase==='Base'?'force':c.phase==='Développement'?'fe':(c.steep?'ecc':'fe');
      add(mkGym(c,heavy,3));
      if(nGym>=2&&!c.rec&&!c.tp)add(mkGym(c,'prev',4))}}
  const ro=c.race?dow(c.r.date):7;
  for(let o=0;o<7;o++){if(S2.some(s=>s.o===o))continue;
    let t='Repos',d='Repos complet : marche, sommeil ≥ 8 h, hydratation, repas riches en glucides.';
    if(c.race&&o>ro){t='Récupération post-course';d='Repos 2–3 jours, marche, mobilité douce, alimentation riche. Reprise légère ensuite.'}
    else if(o===0){t='Repos / mobilité';d='Après la sortie longue : 15\' de mobilité douce (hanches, chevilles, mollets), rouleau 5\'.'}
    else if(o===5&&!c.race){t='Repos';d='Repos complet : jambes fraîches pour la sortie longue de demain.'}
    S2.push({ty:'rest',o,d:addD(c.ws,o),key:addD(c.ws,o)+'|rest',title:t,focus:'Repos',dur:0,km:0,dp:0,desc:d})}
  S2.sort((a,b)=>a.o-b.o);return S2}

const PHT={
 'Base':(c,v)=>`Installer la routine et la base aérobie : ≈ ${v} km, 1 séance de qualité courte, renfo de force. Chaque séance doit te laisser frais pour la suivante.`,
 'Développement':(c,v)=>`Monter en charge de façon contrôlée (+8 % maximum) : endurance, travail ${c.steep?'de côte':'de seuil'}, renfo force-endurance. ≈ ${v} km.`,
 'Spécifique':(c,v,d)=>`Se rapprocher du profil de la course : ≈ ${v} km${d?` et ${d} m de D+`:''}, descentes contrôlées, nutrition testée (${c.fuelTxt}).`,
 'Allègement':(c,v)=>`Semaine d'assimilation : −25 % de volume (≈ ${v} km). Garde une touche de vivacité, dors, mange bien : c'est maintenant que tu progresses.`,
 'Récupération (adaptée)':(c,v)=>`Semaine de récupération décidée d'après ton bilan : volume très réduit, aucune intensité, priorité au sommeil et à la mobilité.`,
 'Affûtage':(c,v,d,pc)=>`Garder les jambes vives : volume −${pc} % (≈ ${v} km), un peu d'intensité courte, sommeil ≥ 8 h, glucides en hausse en fin de semaine.`,
 'Course':(c)=>`Arriver frais et prêt pour ${c.r.name} : une seule vraie séance d'activation, stratégie et matériel validés.`};
const VIG={'Base':'Reste patient en Z2 : aller trop vite dès le début est l\'erreur n°1.','Développement':'Surveille Achille, mollets et genoux au début des côtes ; stop à la moindre douleur qui persiste le lendemain.','Spécifique':'Charge maximale du plan : ne cumule jamais 2 jours durs d\'affilée, travaille ta nutrition à l\'entraînement.','Allègement':'Ne rajoute pas de séance « parce que tu te sens bien ».','Récupération (adaptée)':'Si la fatigue ou la douleur ne baisse pas en 5 jours, parles-en à un professionnel de santé.','Affûtage':'Les jambes lourdes sont normales ; ne compense pas avec des séances en plus.','Course':'Aucun aliment, aucune chaussure, aucun matériel nouveau.'};
function prevLines(c){const L=['Sommeil : 7 h 30–8 h 30 par nuit, c\'est là que la charge est assimilée.','Mobilité 10\' par jour (hanches, chevilles, ischios) + rouleau 5\' sur mollets et quadriceps après les séances.'];
  if(c.rec||c.stop)L.push('Aucune séance intense, marche et étirements doux, 8–9 h de sommeil.');
  else if(c.tp||c.race)L.push('Pas de nouveau renfo ni de nouveau matériel ; hydratation 2,5–3 L par jour ; 8–9 h de sommeil.');
  else if(c.phase==='Base')L.push('Pied et cheville : marche sur pointes/talons 2×30 m et renfort du pied court 2×10, 3 fois dans la semaine.');
  else if(c.phase==='Développement')L.push('Mollets/Achille : montées de mollets excentriques 3×15 (2 fois) + abductions de hanche 3×15.');
  else L.push('Après chaque sortie avec dénivelé : 5\' de marche lente et étirements doux ; surveille genoux et quadriceps.');
  if(c.zone&&PZT[c.zone])L.push(`Zone « ${c.zone} » : ${PZT[c.zone]}`);return L}

function genPlan(r){
  const p=D.profile,pl=ensurePlan(r),mR=monday(r.date);if(pl.start>mR)pl.start=mR;
  const W=dBetween(pl.start,mR)/7+1,E=effKm(r),ratio=r.dplus/Math.max(1,r.km),ultra=r.km>=60||E>=70,steep=ratio>=22,flatRace=ratio<12;
  const taperN=E>=50?2:E>=25?1:0,B=Math.max(0,W-1-taperN),raceMin=parseT(r.goal)||scenarios(r).real,base=pl.base;
  let peak=r.km>=42?Math.max(55,Math.min(95,r.km*.95)):Math.max(30,Math.min(65,r.km*2.4));peak=Math.round(Math.max(base,peak));
  let Tp=steep?Math.min(2600,Math.max(600,r.dplus*.42)):Math.max(150,Math.min(900,r.dplus*.4));
  Tp=Math.min(Tp,(+p.dplusAvail||300)+(/^n/i.test(p.treadmill||'')?0:1500));
  const F=fuel(raceMin),fuelTxt=F.cph?`${F.cph} g de glucides/h`:'hydratation à la soif',t=today();
  const weeks=[],st={noInt:0,noDown:0,runN:+p.sessionsRun||3,gymN:+p.sessionsGym||2,longMax:0,zone:''};
  let level=base,full=base,maxVol=base,prevVol=0,lastFull=0;
  for(let i=0;i<W;i++){
    const ws=addD(pl.start,i*7),race=i===W-1,tp=!race&&i>=B,k=i-B;let notes=[],rec=false,stop=false;
    const fb=i>0?D.feedback[addD(pl.start,(i-1)*7)]:null;
    if(fb){const e=fbEffect(fb,i>1?D.feedback[addD(pl.start,(i-2)*7)]:null);notes=e.notes;rec=e.rec;stop=e.stop;
      if(e.f<1)level*=e.f;else if(e.f>1)level*=1.03;
      st.noInt=Math.max(st.noInt,e.noInt);st.noDown=Math.max(st.noDown,e.noDown);if(e.run)st.runN=e.run;if(e.gym!=null)st.gymN=e.gym;st.longMax=e.long||0;st.zone=(fb.pain&&fb.pain!=='none'&&fb.zone)?fb.zone:''}
    let vol,phase,deload=false;
    if(race){vol=maxVol*.38;phase='Course'}
    else if(tp){vol=maxVol*(taperN===2?(k===0?.75:.55):.65);phase='Affûtage'}
    else if(stop){vol=0;phase='Récupération (adaptée)'}
    else if(rec){vol=level*.65;phase='Récupération (adaptée)';level*=.95}
    else if(i<B-1&&i%4===3){deload=true;vol=level*.74;phase='Allègement'}
    else{if(i>0)level=Math.min(peak,level*1.08);else level=Math.min(peak,level);vol=Math.min(level,full*1.1);level=Math.max(level,vol);full=vol;phase=B>0?(i/B<.35?'Base':i/B<.7?'Développement':'Spécifique'):'Base';maxVol=Math.max(maxVol,vol)}
    vol=Math.round(vol);
    const prog=peak>base?Math.min(1,Math.max(0,(level-base)/(peak-base))):1;
    let T=Tp*(.3+.7*prog);if(deload)T*=.7;if(rec)T*=.4;if(stop)T=0;if(tp)T=Tp*(taperN===2?(k===0?.55:.35):.4);if(race)T=Tp*.1;
    const c={i,ws,vol,T,phase,race,tp,k,deload,rec,stop,runN:st.runN,gymN:st.gymN,longMax:st.longMax,noInt:st.noInt>0,noDown:st.noDown>0,steep,flatRace,ultra,E,r,raceMin,fuelTxt,B,W,peak,prog,zone:st.zone,keyLong:B-1,taperN};
    const sess=buildWeek(c);
    if(st.noInt>0)st.noInt--;if(st.noDown>0)st.noDown--;
    const prep=sess.filter(s=>!s.race),km=k1(prep.reduce((a,s)=>a+(s.km||0),0)),dur=prep.reduce((a,s)=>a+(s.dur||0),0),dp=prep.reduce((a,s)=>a+(s.dp||0),0);
    const pc=maxVol>0?Math.round((1-vol/maxVol)*100):0,obj=(PHT[phase]||PHT.Base)(c,km,rr(dp,50),pc);
    weeks.push({i,ws,phase,sess,km,dur,dp:rr(dp,10),delta:(()=>{if(race)return null;const ref=(deload||rec||stop||tp)?prevVol:(lastFull||prevVol);return ref>0?(km/ref-1)*100:null})(),cur:t>=ws&&t<=addD(ws,6),past:addD(ws,6)<t,notes,obj,vig:VIG[phase]||'',prev:prevLines(c),nRun:sess.filter(s=>s.ty==='run').length,nGym:sess.filter(s=>s.ty==='gym').length});
    if(!race){prevVol=km||prevVol;if(!deload&&!rec&&!stop&&!tp)lastFull=km}}
  return{r,weeks,base,peak,Tp,src:pl.src,start:pl.start,raceMin,E,steep,ultra,W,B,taperN,fuelTxt,days:dBetween(t,r.date)}}

const TYI={run:['🏃🏼‍♂️','var(--acc)'],gym:['🏋🏼','var(--vio)'],cross:['🚴','var(--ice)'],race:['🏁','var(--yel)'],rest:['🍋','var(--mut)']};
const PHC={'Base':'var(--ice)','Développement':'var(--acc2)','Spécifique':'var(--acc)','Allègement':'var(--mut)','Récupération (adaptée)':'var(--mut)','Affûtage':'var(--vio)','Course':'var(--yel)'};
const rpeNum=x=>{const m=String(x||'').match(/(\d+)(?:\s*[–-]\s*(\d+))?\s*\/\s*10/);return m?+(m[2]||m[1]):0};
function weekStrip(w){const t=today();return `<div class="wstrip">${w.sess.map(s=>{const [ico,col]=TYI[s.ty]||TYI.rest,dn=s.ty!=='rest'&&D.done[s.key];return `<div class="wd${s.d===t?' today':''}${dn?' done':''}" style="--tc:${col}" title="${esc(s.title)}"><small>${DAYS[s.o].slice(0,3)}</small><span>${dn?'✅':ico}</span><b>${s.ty==='rest'?'&nbsp;':(s.km>0?fn(s.km,0)+' km':fmtT(s.dur))}</b></div>`}).join('')}</div>`}
const SERIES=/(\d+\s?[×x]\s?\d+(?:['’]\d*|&quot;|&#39;)?(?:\/jambe)?(?:\s?(?:s|min))?)/g;
function stepsOf(txt){return String(txt||'').split(' · ').flatMap(p=>p.split(/(?<=[.!?"'’])\s+(?=[A-ZÉÈÀÂÎÔ])/)).map(x=>x.trim().replace(/\.$/,'')).filter(Boolean).map(x=>x[0].toUpperCase()+x.slice(1))}
function stepHTML(t,i){const e=esc(t).replace(SERIES,'<b class="ser">$1</b>'),m=/^(échauffement|retour au calme|récupération|repos)/i.test(t);
  return `<li class="stp${m?' soft':''}"><span class="stp-n">${i+1}</span><span class="stp-t">${e}</span></li>`}
function sessCard(s){
  const [ico,col]=TYI[s.ty]||TYI.rest,day=`${DAYS[s.o].slice(0,3)} ${pISO(s.d).getDate()}`;
  if(s.ty==='rest')return `<div class="sc rest" style="--tc:${col}"><div class="sc-h"><span class="sc-ico">${ico}</span><span class="sc-t"><small class="sc-day">${day}</small><b>${esc(s.title)}</b><span class="xs mut">${esc(s.desc)}</span></span></div></div>`;
  const done=!!D.done[s.key],n=rpeNum(s.rpe),chips=[['⏱️',fmtT(s.dur)],s.km>0?['📏',fn(s.km)+' km']:null,s.dp>0?['⛰️','+'+fn(s.dp,0)+' m']:null].filter(Boolean),st=stepsOf(s.desc);
  const info=[s.hr&&s.hr!=='—'?['❤️','Fréquence cardiaque',s.hr]:null,s.pace&&s.pace!=='—'?['💨','Allure',s.pace]:null,s.rpe?['🔥','Effort',s.rpe]:null].filter(Boolean);
  return `<div class="sc${done?' dn':''}${s.ty==='race'?' race':''}" style="--tc:${col}"><input class="sc-ck" type="checkbox" data-c="done" data-k="${esc(s.key)}" ${done?'checked':''} aria-label="Séance faite : ${esc(s.title)}">
  <details class="sc-det" open><summary><span class="sc-h"><span class="sc-ico">${ico}</span><span class="sc-t"><small class="sc-day">${day}</small><b>${esc(s.title)}</b></span></span>
  <span><span class="tag">${esc(s.focus)}</span></span><span class="sc-m">${chips.map(c=>`<span>${c[0]} ${c[1]}</span>`).join('')}</span>
  ${n?`<span class="rpe" role="img" aria-label="Intensité ${n} sur 10">${Array.from({length:10},(_,i)=>`<i class="${i<n?'on':''}"></i>`).join('')}</span>`:''}<span class="sc-more">Voir la séance ▾</span></summary>
  <div class="sc-body"><div class="sc-info">${info.map(x=>`<div><i>${x[0]}</i><small>${x[1]}</small><b>${esc(x[2])}</b></div>`).join('')}</div><ol class="stps">${st.map(stepHTML).join('')}</ol></div></details></div>`}
function trainProgress(pl){let n=0,f=0;pl.weeks.forEach(w=>w.sess.forEach(s=>{if(s.ty!=='rest'&&s.ty!=='race'){n++;if(D.done[s.key])f++}}));
  const p=n?Math.round(f/n*100):0,badge=p<10?'🌱 Départ lancé':p<35?'🔥 Tu prends le rythme':p<65?'⛰️ En pleine ascension':p<90?'🚀 Sprint final':'🏆 Prêt pour le jour J';
  return `<div class="gam"><div class="gam-top"><b class="cond">${f}/${n} séances cochées</b><span class="tag up">${p} %</span></div><div class="bar"><i style="width:${p}%"></i></div><p class="xs mut">${pl.weeks.filter(w=>w.past).length}/${pl.W} semaines passées · ${badge}</p></div>`}
function volChart(pl){const n=pl.weeks.length,W=Math.max(300,Math.min(700,n*22)),H=150,mx=Math.max(1,...pl.weeks.map(w=>w.km)),bw=W/n;
  const bars=pl.weeks.map((w,i)=>{const h=w.km/mx*(H-34),x=i*bw+2;return `<g><title>Sem. ${w.i+1} · ${esc(w.phase)} · ${fn(w.km,0)} km · +${fn(w.dp,0)} m</title><rect x="${x.toFixed(1)}" y="${(H-18-h).toFixed(1)}" width="${Math.max(3,bw-4).toFixed(1)}" height="${Math.max(2,h).toFixed(1)}" rx="4" fill="${PHC[w.phase]||'var(--ice)'}" ${w.cur?'stroke="var(--ink)" stroke-width="2"':''} opacity="${w.past?.45:1}"/>${n<=26?`<text x="${(x+(bw-4)/2).toFixed(1)}" y="${H-4}" text-anchor="middle" style="font-size:9px">${w.i+1}</text>`:''}</g>`}).join('');
  const leg=[...new Set(pl.weeks.map(w=>w.phase))].map(p=>`<span class="chip2"><i style="width:10px;height:10px;border-radius:3px;background:${PHC[p]||'var(--ice)'};display:inline-block"></i>${esc(p)}</span>`).join('');
  return `<div class="chartbox"><svg class="chart mbars" viewBox="0 0 ${W} ${H}" style="min-width:0" role="img" aria-label="Volume hebdomadaire en km, par phase">${bars}</svg></div><div class="row" style="gap:6px;margin:4px 0 12px">${leg}</div>`}
/* ============================ PLANS IA : LECTURE ET SUIVI JOUR PAR JOUR ============================ */
const MOIS_RE='janv(?:ier)?|f[eé]vr(?:ier)?|mars|avr(?:il)?|mai|juin|juil(?:let)?|ao[uû]t|sept(?:embre)?|oct(?:obre)?|nov(?:embre)?|d[eé]c(?:embre)?',WD_RE='lundi|mardi|mercredi|jeudi|vendredi|samedi|dimanche',JOURS_FR=['lundi','mardi','mercredi','jeudi','vendredi','samedi','dimanche'];
const fold=w=>String(w).toLowerCase().normalize('NFD').replace(/[̀-ͯ]/g,'');
const monthIdx=w=>{const n=fold(w);return ['janv','fevr','mars','avr','mai','juin','juil','aout','sept','oct','nov','dec'].findIndex(p=>n.startsWith(p))};
// Reconnaît un titre de jour : « Jour 3 », « J-5 », « Jour J », « Lundi », « Lundi 3 novembre », « 03/11 », « 3 novembre »…
function dayHead(t){
  const clean=r=>(r||'').replace(/^[\s:–—\-·|(\/]+/,'').replace(/[)\s]+$/,''),ok=d=>d.dd>=1&&d.dd<=31&&d.mm>=1&&d.mm<=12;let m;
  // « Jour 3 — lundi 3 novembre » : le numéro ET la date / le jour de la semaine du reste sont conservés
  const wd2=o=>{const q=o.rest?dayHead(o.rest):null;if(q&&(q.dm||q.wd!=null)){if(q.dm)o.dm=q.dm;if(q.wd!=null)o.wd=q.wd;o.rest=q.rest}return o};
  if(m=t.match(/^jour\s*j\b\s*(.*)$/i))return wd2({off:0,rest:clean(m[1])});
  if(m=t.match(/^(?:jour|day)\s*(\d{1,3})\b(?![\/.]\d)\s*(.*)$/i))return wd2({n:+m[1],rest:clean(m[2])});
  if(m=t.match(/^J\s*([+\-−–])\s*(\d{1,3})\b\s*(.*)$/))return wd2({off:(m[1]==='+'?1:-1)*+m[2],rest:clean(m[3])});
  if(m=t.match(/^J0\b\s*(.*)$/))return wd2({off:0,rest:clean(m[1])});
  m=t.match(new RegExp(`^(${WD_RE})\\b\\.?\\s*(?:(\\d{1,2})(?:er)?\\s+(${MOIS_RE})\\.?(?:\\s+(\\d{4}))?|(\\d{1,2})[\\/.](\\d{1,2})(?:[\\/.](\\d{2,4}))?)?\\s*(.*)$`,'i'));
  if(m){const o={wd:JOURS_FR.indexOf(fold(m[1])),rest:clean(m[8])};
    const dm=m[2]?{dd:+m[2],mm:monthIdx(m[3])+1,yy:m[4]?+m[4]:0}:m[5]?{dd:+m[5],mm:+m[6],yy:m[7]?+m[7]:0}:null;if(dm&&ok(dm))o.dm=dm;return o}
  m=t.match(/^(\d{1,2})\/(\d{1,2})(?:\/(\d{2,4}))?\b\s*(.*)$/)||t.match(/^(\d{1,2})\.(\d{1,2})\.(\d{2,4})\b\s*(.*)$/);
  if(m){const dm={dd:+m[1],mm:+m[2],yy:m[3]?+m[3]:0};if(ok(dm))return{dm,rest:clean(m[4])}}
  m=t.match(new RegExp(`^(\\d{1,2})(?:er)?\\s+(${MOIS_RE})\\.?(?:\\s+(\\d{4}))?\\b\\s*(.*)$`,'i'));
  if(m){const dm={dd:+m[1],mm:monthIdx(m[2])+1,yy:m[3]?+m[3]:0};if(ok(dm))return{dm,rest:clean(m[4])}}
  return null}
// Texte libre (réponse d'une IA) → liste de jours {n, off, wd, dm, week, title, items:[{l,t,sub}], notes}. Sans date : voir resolvePlan.
const cleanLab=x=>fold(x||'').replace(/[^a-z0-9' ]+/g,' ').replace(/\s+/g,' ').trim(),BARE_MEAL=/^(petit dej\w*|dejeuner|collation\w*|diner|souper|gouter|hydratation)( [\d h]{1,8})?$/,MEAL_START=/^(petit dej\w*|collation\w*|dejeuner|gouter|diner|souper|hydratation)\b/,
  isMealHead=txt=>{const c=cleanLab(txt);return BARE_MEAL.test(c)||(MEAL_START.test(c)&&txt.length<=100&&/[:：]\s*$/.test(txt))};   // « 🍌 Collation (seulement si faim) : » = titre
function parseAIPlan(text){
  const days=[],strip=x=>x.replace(/\*\*|__|`/g,'').replace(/\s+/g,' ').trim().replace(/^["“”]+\s*/,'').replace(/(?<=[^\d\s])["“”]+$/,'').trim();
  let cur=null,week=null,last=null,tbl=null;
  const label=txt=>{const m=txt.match(/^([^:：]{2,34}?)\s*[:：]\s*(.*)$/)||(MEAL_START.test(cleanLab(txt))&&txt.match(/^([^:：]{2,80}?)\s*[:：]\s*(.*)$/));return m?{l:m[1].trim(),t:m[2].trim(),sub:[]}:{l:'',t:txt,sub:[]}};
  const startDay=h=>{cur={n:h.n,off:h.off,wd:h.wd,dm:h.dm,week,title:'',items:[],notes:[]};days.push(cur);last=null;
    if(h.rest){if(h.rest.length<=50)cur.title=h.rest;else addItem(h.rest,0,false)}};
  const push=(it,indent,grp)=>{cur.items.push(it);last={it,indent,grp:grp||(!!it.l&&!it.t)}};
  function addItem(txt,indent,bullet,asLabel){
    if(!cur||!txt)return;
    if(/^(total|totaux|macros?|apports?|bilan|r[eé]sum[eé]|calories|kcal)\b/i.test(txt)){cur.notes.push(txt.replace(/\s*:\s*$/,''));return}
    // Une puce « Dîner : … » sous « Petit-déjeuner : » est un nouveau repas / une nouvelle séance, pas un détail du précédent.
    const newMeal=/^(petit[- ]?d[eé]j|collation|d[eé]jeuner|go[uû]ter|d[iî]ner|souper|hydratation|snack|r[eé]cup|s[eé]ance|repos|renfo|footing|matin|midi|soir|avant|pendant|apr[eè]s)[^:：]{0,24}[:：]\s*\S/i.test(txt);
    const ctxt=cleanLab(txt),mealHead=isMealHead(txt)||(MEAL_START.test(ctxt)&&/[:：]/.test(txt.slice(0,80)));   // titre de repas, même avec emoji ou sans « : »
    if(bullet&&last&&!mealHead&&(last.grp?indent>last.indent&&!(last.indent<0&&newMeal):indent>=last.indent+2)){last.it.sub.push(txt);return}
    if(asLabel){push({l:txt.replace(/\s*[:：]\s*$/,''),t:'',sub:[]},bullet?indent:-1,true);return}
    push(label(txt),bullet?indent:-1)}
  for(const raw of String(text).replace(/\r/g,'').split('\n')){
    if(!raw.trim())continue;
    if(/^\s*\|/.test(raw)){                                     // tableau Markdown : 1re colonne = jour, en-têtes = repas / séances
      const cells=raw.trim().replace(/^\||\|$/g,'').split('|').map(c=>strip(c));
      if(cells.every(c=>/^:?-{2,}:?$/.test(c)||c===''))continue;
      if(!tbl){tbl={head:cells};continue}
      const h=dayHead(cells[0]);
      if(h){startDay(h);cells.slice(1).forEach((c,j)=>{if(!c||/^[-–—]$/.test(c))return;const parts=c.split(/<br\s*\/?>/i).map(strip).filter(Boolean);
        const it={l:tbl.head[j+1]||'',t:parts[0]||'',sub:parts.slice(1)};cur.items.push(it)})}
      else if(cur)cur.items.push({l:'',t:cells.filter(Boolean).join(' · '),sub:[]});
      continue}
    tbl=null;
    const m=raw.match(/^(\s*)(?:(#{1,6})\s+)?(?:([-*•·–+]|\d+[.)])\s+)?(.*)$/),indent=m[1].replace(/\t/g,'    ').length,heading=!!m[2],bullet=!!m[3],body=m[4],text=strip(body);
    if(!text)continue;
    const w=text.match(/^(?:semaine|week)\s*(\d{1,2})\b/i);if(w){week=+w[1];continue}
    const h=text.length<=90?dayHead(text):null;if(h){startDay(h);continue}
    if(!cur)continue;
    const bold=!bullet&&/^(\*\*[^*]+\*\*|__[^_]+__):?$/.test(body.trim());
    addItem(text,indent,bullet,heading||bold||isMealHead(text))}
  days.forEach(d=>{if(!d.items.length&&d.title){d.items.push({l:'',t:d.title,sub:[]});d.title=''}});
  return days.filter(d=>d.items.length||d.notes.length)}
// Donne une date à chaque jour : date écrite > « Jour N » (depuis la date de début) > « J-N » (depuis la course) > jour de la semaine > ordre.
function resolvePlan(days,{start='',raceDate=''}={}){
  if(!days.length)return null;
  const t0=today(),anchor=raceDate||t0,ay=+anchor.slice(0,4);
  const year=(mm,dd,yy)=>{if(yy)return yy<100?2000+yy:yy;let b=null;for(const y of [ay-1,ay,ay+1]){const dist=Math.abs(dBetween(anchor,`${y}-${pad(mm)}-${pad(dd)}`));if(!b||dist<b.dist)b={y,dist}}return b.y};
  days.forEach(d=>{d.date=null;if(d.dm){const y=year(d.dm.mm,d.dm.dd,d.dm.yy),dt=new Date(y,d.dm.mm-1,d.dm.dd);if(dt.getMonth()===d.dm.mm-1)d.date=iso(dt)}});
  const dated=days.filter(d=>d.date).map(d=>d.date).sort(),explicit=dated.length>0,st=start||(explicit?dated[0]:t0);let prev=null;
  days.forEach(d=>{
    if(!d.date){
      if(d.n!=null)d.date=addD(st,d.n-1);
      else if(d.off!=null&&raceDate)d.date=addD(raceDate,d.off);
      else if(d.wd!=null&&d.week!=null&&!explicit)d.date=addD(monday(st),(d.week-1)*7+d.wd);
      else if(d.wd!=null){let c=prev?addD(prev,1):st;for(let k=0;k<7&&dow(c)!==d.wd;k++)c=addD(c,1);d.date=c}
      else d.date=prev?addD(prev,1):st}
    prev=d.date});
  const by={};days.forEach(d=>{if(by[d.date]){by[d.date].items.push(...d.items);by[d.date].notes.push(...d.notes);if(!by[d.date].title)by[d.date].title=d.title}else by[d.date]=d});
  const out=Object.values(by).sort((a,b)=>a.date<b.date?-1:1);
  return{days:out,start:st,explicit,first:out[0].date,last:out[out.length-1].date}}
// Plan du coach : chaque course a le sien (clé « train@id » ou « nutri@id »).
const sk=k=>k+'@'+((selRace()||{}).id||'');
let _apc=null;
function aiPlan(kind){
  const ai=D.ai||{},text=(ai.resp&&ai.resp[sk(kind)])||'';if(!text.trim())return null;
  const r=selRace(),rd=r?r.date:'',st=(ai.start&&ai.start[sk(kind)])||'',key=[kind,text,rd,st,today()].join('\u0001');
  if(_apc&&_apc.key===key)return _apc.v;
  const v=resolvePlan(parseAIPlan(text),{start:st,raceDate:rd});_apc={key,v};return v}

const apvS=k=>{S.apv=S.apv||{};return S.apv[k]=S.apv[k]||{v:'day',d:'',m:''}};
const apvIsDone=(k,id)=>!!(D.ai&&D.ai.done&&D.ai.done[sk(k)]&&D.ai.done[sk(k)][id]);
// Unité de suivi : en nutrition, un REPAS entier (petit-déjeuner, déjeuner…) ; pour l'entraînement, une séance (une ligne).
function apvUnits(k,d){if(k==='train')return [{id:`${d.date}|m0`,seg:trainSeg(d),its:apvOrd(k,d)}];const g={};apvOrd(k,d).forEach(x=>{(g[x.s]=g[x.s]||[]).push(x)});return Object.keys(g).map(Number).sort((a,b)=>a-b).map(sg=>({id:`${d.date}|m${sg}`,seg:sg,its:g[sg]}))}
function apvDP(k,d){const u=apvUnits(k,d);return{n:u.length,f:u.filter(x=>apvIsDone(k,x.id)).length}}
function apvProg(k,days){let n=0,f=0;days.forEach(d=>{const p=apvDP(k,d);n+=p.n;f+=p.f});return{n,f}}
function apvSel(k,pl){const s=apvS(k),t=today();if(!s.d||s.d<pl.first||s.d>pl.last)s.d=t>=pl.first&&t<=pl.last?t:t<pl.first?pl.first:pl.last;return s}
const apvShort=it=>{const x=(it.l?it.l+' : ':'')+it.t;return x.length>40?x.slice(0,38)+'…':x};
function apvDayHTML(k,pl,s,by){
  const d=by[s.d],isT=s.d===today(),nav=n=>`<button class="btn ghost s" data-a="apvNav" data-k="${k}" data-s="${n}" ${(n<0?s.d<=pl.first:s.d>=pl.last)?'disabled':''} aria-label="${n<0?'Jour précédent':'Jour suivant'}">${n<0?'‹':'›'}</button>`;
  return `<div class="apv-nav">${nav(-1)}<div class="tc"><b class="cond">${esc(longD(s.d))}</b>${isT?' <span class="tag up">Aujourd\'hui</span>':''}${d&&d.title?`<div class="sm mut">${esc(d.title)}</div>`:''}</div>${nav(1)}</div>
  ${d?`${apvGroups(k,d,s.d)}${d.notes.map(n=>`<p class="sm apv-note">📊 ${esc(n)}</p>`).join('')}`:'<p class="sm mut tc" style="margin:14px 0">Rien de prévu ce jour-là.</p>'}
  ${!isT&&today()>=pl.first&&today()<=pl.last?`<div class="row" style="margin-top:8px"><button class="btn ghost s" data-a="apvToday" data-k="${k}">Aller à aujourd'hui</button></div>`:''}`}
function apvWeekHTML(k,pl,s,by){
  const mon=monday(s.d),ds=Array.from({length:7},(_,i)=>addD(mon,i)),wp=apvProg(k,ds.map(x=>by[x]).filter(Boolean)),t=today();
  const nav=n=>`<button class="btn ghost s" data-a="apvNav" data-k="${k}" data-s="${n}" ${(n<0?mon<=monday(pl.first):addD(mon,7)>pl.last)?'disabled':''} aria-label="${n<0?'Semaine précédente':'Semaine suivante'}">${n<0?'‹':'›'}</button>`;
  return `<div class="apv-nav">${nav(-1)}<div class="tc"><b class="cond">Semaine du ${shortD(mon)}</b><div class="sm mut">${wp.n?`${wp.f}/${wp.n} faits`:'Rien de prévu'}</div></div>${nav(1)}</div>
  <div class="apv-wk">${ds.map(x=>{const d=by[x],dp=d?apvDP(k,d):{n:0,f:0},n=dp.n,f=dp.f;
    return `<button class="apv-wd${x===t?' today':''}${n&&f===n?' full':''}" data-a="apvDay" data-k="${k}" data-d="${x}" ${d?'':'disabled'}><b>${DAYS[dow(x)].slice(0,3)} ${pISO(x).getDate()}</b>${d?`${d.title?`<span class="xs mut">${esc(d.title)}</span>`:''}<ul>${apvOrd(k,d).slice(0,5).map(x=>`<li>${esc(apvShort(x.it))}</li>`).join('')}</ul>${n>5?`<span class="xs mut">+${n-5} autres</span>`:''}<span class="tag ${f===n?'up':''}">${f}/${n}</span>`:'<span class="xs mut">—</span>'}</button>`}).join('')}</div>`}
function apvCalHTML(k,pl,s,by){
  const m=s.m||s.d.slice(0,7);s.m=m;const [Y,M]=m.split('-').map(Number),lead=dow(`${m}-01`),nd=new Date(Y,M,0).getDate(),t=today();
  const nav=n=>`<button class="btn ghost s" data-a="apvNav" data-k="${k}" data-s="${n}" ${(n<0?m<=pl.first.slice(0,7):m>=pl.last.slice(0,7))?'disabled':''} aria-label="${n<0?'Mois précédent':'Mois suivant'}">${n<0?'‹':'›'}</button>`;
  let cells='';for(let i=0;i<lead;i++)cells+='<span></span>';
  for(let d=1;d<=nd;d++){const x=`${m}-${pad(d)}`,p=by[x],dp=p?apvDP(k,p):{n:0,f:0},n=dp.n,f=dp.f;
    cells+=`<button class="apv-c${x===t?' today':''}${n?(f===n?' full':f?' part':' todo'):''}" data-a="apvDay" data-k="${k}" data-d="${x}" ${p?'':'disabled'} aria-label="${esc(longD(x))}${n?`, ${f} sur ${n} faits`:', rien de prévu'}"><b>${d}</b>${p?`<span class="apv-l">${esc(apvShort(p.items[0]))}</span><span class="apv-d">${f}/${n}</span>`:''}</button>`}
  return `<div class="apv-nav">${nav(-1)}<div class="tc"><b class="cond">${MONL[M-1]} ${Y}</b></div>${nav(1)}</div>
  <div class="apv-cal">${['L','M','M','J','V','S','D'].map(x=>`<i>${x}</i>`).join('')}${cells}</div>`}
const SEGS_N=[[`☀️ Petit-déjeuner`,/(petit|breakfast|^matin)/,'var(--yel)'],[`🍽️ Déjeuner`,/(dejeuner|\bmidi\b|lunch)/,'var(--acc)'],[`🍎 Collation`,/^(collation|snack|en-cas|encas|gouter)/,'var(--pink)'],[`🌙 Dîner`,/(diner|souper|dinner|^soir)/,'var(--vio)']];
// Entraînement : UNE seule section par jour. Son type (donc son logo) vient du premier mot écrit pour la journée dans le plan du coach :
// « Course » 🏃 · « Renfo » 🏋🏼 · « Repos » 🍋 · « Jour de course » 🏁 (le logo lui-même, écrit en premier, est aussi reconnu).
const SEGS_T=[[`🏃 Course`,/^(course|footing|seance|entrainement|sortie)/,'var(--acc)'],[`🏋🏼 Renfo`,/^(renfo|renforcement|muscu)/,'var(--vio)'],[`🍋 Repos`,/^(repos|recup)/,'var(--mut)'],[`🏁 Jour de course`,/^jour de course/,'var(--yel)'],[`🧘🏼‍♂️ Mobilité`,/^(mobilite|etirement|stretching|yoga)/,'var(--ice)']];
const TR_EMO=[[3,/\u{1F3C1}/u],[2,/\u{1F34B}/u],[1,/\u{1F3CB}/u],[0,/\u{1F3C3}/u],[4,/\u{1F9D8}/u]],TR_ICO=['🏃','🏋🏼','🍋','🏁','🧘🏼‍♂️'];
function trainSeg(d){
  const it0=d.items[0]||{},first=[d.title,it0.l,it0.t].find(x=>x&&String(x).trim())||'';
  const lead=(String(first).match(/^[^\p{L}\p{N}]*/u)||[''])[0],e=TR_EMO.find(([,re])=>re.test(lead));if(e)return e[0];
  const w=fold(String(first)).replace(/^[^a-z]+/,'');
  if(/^jour de course|^jour j\b/.test(w))return 3;
  if(/^(mobilite|etirement|stretching|yoga)/.test(w))return 4;
  if(/^(repos|recup)/.test(w))return 2;
  if(/^(renfo|renforcement|muscu)/.test(w))return 1;
  if(/^(course|footing|sortie|seance|entrainement)/.test(w))return 0;
  const txt=[d.title||''].concat(d.items.map(i=>[i.l,i.t].concat(i.sub||[]).join(' '))).join('\n'),x=TR_EMO.find(([,re])=>re.test(txt));if(x)return x[0];
  if(d.date&&(selRace()||{}).date===d.date)return 3;
  return /renfo|muscu|gainage/.test(fold(txt))?1:0}
const segDefs=k=>k==='nutri'?SEGS_N:SEGS_T,priOf=k=>k==='train'?[0,1,4,2,3]:[2,0,1,3];
// Chaque élément est rangé dans une section ; un libellé inconnu rejoint la section de l'élément précédent (jamais de section « Autre »).
const nMeal=x=>{const c=cleanLab(x);if(!c)return -1;const f=priOf('nutri').find(i=>SEGS_N[i][1].test(c));return f==null?-1:f};
const segOf=(k,it,prev)=>{
  if(k==='nutri'){const l=cleanLab(it.l),t=cleanLab(it.t);
    if(/^hydrat/.test(l)||(!l&&MEAL_START.test(t)&&/^hydrat/.test(t)&&isMealHead(it.t)))return -1;
    let x=nMeal(it.l);if(x<0&&!l&&isMealHead(it.t))x=nMeal(it.t);
    return x>=0?x:(prev==null?0:prev)}
  const D=segDefs(k),P=priOf(k),l=fold(it.l||''),t=fold(it.t||''),gen=k==='train'&&(!l||/^(seance|entrainement|training|activite|programme)/.test(l)),hit=x=>{const f=P.find(i=>D[i][1].test(x));return f==null?-1:f};
  let x=gen?(hit(t)>=0?hit(t):hit(l)):hit(l);if(x<0&&!gen&&!l)x=hit(t);if(x<0&&k==='nutri')x=hit(t.slice(0,30));if(x<0&&gen&&l)x=0;return x<0?(prev==null?0:prev):x};
const segName=(k,s)=>segDefs(k)[s][0],segCol=(k,s)=>segDefs(k)[s][2];
function apvOrd(k,d){let prev=null,out=[];
  if(k==='train'){const sg=trainSeg(d);return d.items.map((it,i)=>({it,i,s:sg}))}
  d.items.forEach((it,i)=>{const s=segOf(k,it,prev);prev=s;
    if(k!=='nutri'){out.push({it,i,s});return}
    if(s<0)return;
    if(!it.t&&nMeal(it.l)>=0){it.sub.forEach((z,j)=>out.push({it:{l:'',t:z,sub:[]},i:i+j/100,s}));return}   // titre de repas : on ne garde que son contenu
    out.push({it,i,s})});
  return out.sort((p,q)=>p.s-q.s||p.i-q.i)}
function apvNote(d,seg){let prev=null,out=[];d.items.forEach(it=>{const s=segOf('nutri',it,prev);prev=s;if(s===seg&&nMeal(it.l)===seg){const m=String(it.l).match(/\(([^)]*)\)/);if(m&&m[1].trim())out.push(m[1].trim())}});return out}
function apvHydr(d){let prev=null,out=[];
  d.items.forEach(it=>{const s=segOf('nutri',it,prev);prev=s;if(s>=0)return;if(it.t)out.push(it.t);it.sub.forEach(z=>out.push(z))});
  return out}
function apvGroups(k,d,date){
  const hide=(it,sg)=>{const l=k==='nutri'?cleanLab(it.l):fold(it.l||'');return !l||(k==='nutri'?nMeal(it.l)===sg:segDefs(k)[sg][1].test(l))||(k==='train'&&/^(seance|entrainement|training|activite|programme)/.test(l))},
   line=x=>{const it=x.it,sh=hide(it,x.s);return `<li>${!sh?`<b>${esc(it.l)}</b>${it.t?' : ':''}`:''}${it.t?esc(it.t):(sh&&it.l?`<b>${esc(it.l)}</b>`:'')}${it.sub.length?`<ul>${it.sub.map(z=>`<li>${esc(z)}</li>`).join('')}</ul>`:''}</li>`};
  // Séance de renfo : seuls « Échauffement », « Circuit » et « Finish » sont repliables, repliés par défaut (les lignes qui les suivent sans en être des sous-puces y sont rattachées jusqu'au titre suivant).
  const blk=it=>/^(echauffement|circuit|finish)\b/.test(cleanLab(it.l||it.t||'')),endH=it=>/^(bloc\b|bas du corps|haut du corps|posture|echauffement|circuit|finish)\b/.test(cleanLab(it.l||it.t||'')),
   isC=it=>/^circuit\b/.test(cleanLab(it.l||it.t||'')),grp=a=>{const o=[];let cur=null,circ=false;a.forEach(x=>{if(blk(x.it)){const nd={...x,kids:[]};o.push(nd);circ=isC(x.it);cur=(x.it.sub.length&&!circ)?null:nd}else if(circ&&cur)cur.kids.push(x);else if(endH(x.it)){o.push(x);cur=null}else if(cur)cur.kids.push(x);else o.push(x)});return o},
   blockLine=x=>{const it=x.it,n=it.sub.length+x.kids.length;return `<li class="trb-li"><details class="trb"><summary><b>${esc(it.l||it.t)}</b>${it.l&&it.t?` : ${esc(it.t)}`:''}<small>${n} ligne${n>1?'s':''}</small></summary><ul>${it.sub.map(z=>`<li>${esc(z)}</li>`).join('')}${x.kids.map(line).join('')}</ul></details></li>`},
   rowOf=x=>x.kids&&(x.kids.length||x.it.sub.length)?blockLine(x):line(x);
  let h=apvUnits(k,d).map(u=>{const dn=apvIsDone(k,u.id),n=u.its.length,nm=segName(k,u.seg),sp=nm.indexOf(' '),ico=nm.slice(0,sp),lab=nm.slice(sp+1);
    const hint=k==='nutri'?((['Le matin','Le midi','Dans l\'après-midi','Le soir'][u.seg]||'')+apvNote(d,u.seg).map(x=>' · '+esc(x)).join('')):'';
    return `<div class="mealw mw${u.seg}${dn?' dn':''}" style="--sc:${segCol(k,u.seg)}"><input class="sc-ck" type="checkbox" data-c="apvdone" data-k="${k}" data-id="${esc(u.id)}" ${dn?'checked':''} aria-label="${esc(lab)} : terminé"><details class="meal${dn?' fin':''}"${k==='train'?' open':''}><summary>${k==='train'?'':`<span class="meal-i" aria-hidden="true">${ico}</span>`}<span class="meal-n"><b>${esc(lab)}</b>${hint?`<small class="meal-h">${hint}</small>`:''}</span><span class="meal-g">${dn?'✅ ':''}${n} élément${n>1?'s':''}</span></summary><ul class="apv-items">${(k==='train'&&u.seg===1?grp(u.its):u.its).map(rowOf).join('')}</ul></details></div>`}).join('');
  if(k==='nutri'){const hy=apvHydr(d);if(hy.length)h+=`<p class="sm apv-note">💧 Hydratation : ${hy.map(esc).join(' · ')}</p>`}
  return h}
function aiPlanView(kind){
  const resp=((D.ai||{}).resp||{})[sk(kind)]||'';if(!resp.trim())return '';
  const pl=aiPlan(kind);
  if(!pl)return `<div id="apv-${kind}" class="note" style="margin-top:12px">Je n'ai pas reconnu de jours dans cette réponse. Demande à ton IA un plan présenté jour par jour (« Jour 1 — lundi 3 novembre », puis une ligne par repas ou séance) : le bouton « Copier prompt + données » le lui demande déjà.</div>`;
  const s=apvSel(kind,pl),by={};pl.days.forEach(d=>{by[d.date]=d});const pr=apvProg(kind,pl.days),pct=pr.n?Math.round(pr.f/pr.n*100):0;
  return `<div id="apv-${kind}" class="apv"><h3 class="cond" style="margin:16px 0 4px">Mon plan jour par jour</h3>
  <p class="xs mut">${pl.days.length} jours · du ${shortD(pl.first)} au ${shortD(pl.last)} · ${pr.f}/${pr.n} faits (${pct} %)</p><div class="bar" role="img" aria-label="Avancement ${pct} %"><i style="width:${pct}%"></i></div>
  <div class="row" style="margin:10px 0;flex-wrap:wrap">${[['day','Jour'],['week','Semaine'],['cal','Calendrier']].map(([v,l])=>`<button class="btn ${s.v===v?'':'ghost'} s" data-a="apvV" data-k="${kind}" data-v="${v}">${l}</button>`).join('')}
    ${pl.explicit?'':`<label class="xs mut" style="display:flex;gap:6px;align-items:center;margin-left:auto">Jour 1 =<input type="date" data-c="apvstart" data-k="${kind}" value="${pl.start}"></label>`}</div>
  ${s.v==='week'?apvWeekHTML(kind,pl,s,by):s.v==='cal'?apvCalHTML(kind,pl,s,by):apvDayHTML(kind,pl,s,by)}</div>`}
const apvRefresh=k=>{const el=$('#apv-'+k);if(!el)return;const st=[...el.querySelectorAll('details.meal')].map(d=>d.open);el.outerHTML=aiPlanView(k);const n=$('#apv-'+k);if(n)[...n.querySelectorAll('details.meal')].forEach((d,i)=>{if(i<st.length)d.open=st[i]})};
function aiBlock(kind,r){const resp=((D.ai||{}).resp||{})[sk(kind)]||'',lab=kind==='train'?"plan d'entraînement":'plan nutritionnel',pl=resp.trim()?aiPlan(kind):null;
  const inner=`<label class="f full" style="margin-top:4px">Plan du coach<textarea id="ai-r-${kind}" rows="${resp?6:4}" placeholder="Colle ici le plan de ton coach">${esc(resp)}</textarea></label>
  <div class="row" style="margin-top:8px"><button class="btn s" data-a="aiSave" data-k="${kind}">💾 Enregistrer le plan du coach</button>${resp?`<button class="btn red s" data-a="aiClear" data-k="${kind}">Effacer le plan</button>`:''}${pl&&!pl.explicit?`<label class="xs mut" style="display:flex;gap:6px;align-items:center;margin-left:auto">Jour 1 du plan =<input type="date" data-c="apvstart" data-k="${kind}" value="${pl.start}"></label>`:''}</div>
  ${resp?`<details class="aiout-wrap"><summary class="xs mut">Afficher le plan du coach enregistré</summary><div class="aiout">${esc(resp)}</div></details>`:''}`;
  return kind==='train'?`<details class="card aicard hist"${resp?'':' open'}><summary><h2 class="cond" style="display:inline-block;margin:0">Plan du coach · ${lab}</h2></summary><div style="margin-top:12px">${inner}</div></details>`:`<div class="card aicard"><h2 class="cond">Plan du coach · ${lab}</h2>${inner}</div>`}
/* Sections alimentées uniquement par le plan du coach : « Programme semaine par semaine » (entraînement) et « Semaine avant la course » (nutrition). */
// Un seul logo par jour. 1) un logo écrit dans le plan du coach (🍋 repos, 🏃 course à pied, 🏋 renfo, 🏁 course) l'emporte : le premier rencontré dans le jour ; 2) sinon déduit des séances (🏁 si c'est le jour de la course).
function trainIcons(d,isRace){
  if(!d)return '';
  return TR_ICO[trainSeg(d)]}
// Barre de la semaine : un tracé GPX de montagne à petits sommets ; le coureur avance sur le tracé à mesure que les journées sont cochées (un repère par journée, le dernier au sommet).
const MT_N=60,MT_W=600,MT_H=100,MT_PTS=Array.from({length:MT_N},(_,i)=>{const t=i/(MT_N-1);return Math.max(8,Math.min(86,78-50*t+9*Math.sin(t*Math.PI*2*3.5+.6)+5*Math.sin(t*Math.PI*2*9+1.3)+3*Math.sin(t*Math.PI*2*17)))});
const mtX=t=>10+t*(MT_W-20),mtY=t=>{const f=Math.max(0,Math.min(1,t))*(MT_N-1),i=Math.min(MT_N-2,Math.floor(f)),w=f-i;return MT_PTS[i]+(MT_PTS[i+1]-MT_PTS[i])*w};
function weekGam(wp,all,cur,mo,nu){
  const n=wp.n,pct=n?Math.round(wp.f/n*100):0,full=n>0&&wp.f===n,left=n-wp.f,t=n?wp.f/n:0,
    badge=full?(nu?'🏆 Prêt pour le jour J !':mo?'🏆 Mois validé !':'🏆 Semaine validée !'):pct>=70?'🚀 Dernière ligne droite':pct>=35?'⛰️ En pleine ascension':pct>0?'🔥 Tu prends le rythme':cur?(nu?'🍽️ À table !':'🌱 À toi de jouer'):mo?'🗓️ Mois à venir':'🗓️ Semaine à venir',
    hint=nu?(full?'Tous les repas sont cochés : tu arrives affûté.':n?`Encore ${left} repas à cocher pour atteindre le sommet.`:'Rien de prévu.'):full?(mo?'Toutes les journées du mois sont cochées : bravo, récupère bien.':'Toutes les journées sont cochées : bravo, récupère bien.'):n?`Encore ${left} journée${left>1?'s':''} à cocher pour atteindre le sommet.`:(mo?'Rien de prévu ce mois-ci.':'Rien de prévu cette semaine.'),
    line=MT_PTS.map((y,i)=>`${mtX(i/(MT_N-1)).toFixed(1)},${y.toFixed(1)}`).join(' '),
    marks=Array.from({length:n},(_,i)=>{const q=(i+1)/n,x=mtX(q),y=mtY(q),dn=i<wp.f,last=i===n-1;
      return last&&!full?`<text x="${x.toFixed(1)}" y="${(y-8).toFixed(1)}" text-anchor="middle" style="font-size:16px">🏁</text>`:`<circle cx="${x.toFixed(1)}" cy="${y.toFixed(1)}" r="4.5" fill="${dn?'var(--acc2)':'var(--card)'}" stroke="${dn?'var(--bg)':'var(--mut)'}" stroke-width="2"/>`}).join(''),
    rx=mtX(t),ry=mtY(t);
  return `<div class="wkg${full?' full':''}" data-full="${full?1:0}"><div class="wkg-top"><b class="cond">${esc(badge)}</b><span class="tag up">${wp.f}/${n} · ${pct} %</span></div>
  <svg class="wkg-svg" viewBox="0 0 ${MT_W} ${MT_H}" role="img" aria-label="Avancement de la semaine sur un tracé de montagne : ${pct} %"><defs><clipPath id="wkclip"><rect x="0" y="0" width="${rx.toFixed(1)}" height="${MT_H}"/></clipPath></defs>
  <polygon points="${mtX(0)},${MT_H} ${line} ${mtX(1)},${MT_H}" fill="var(--line)" opacity=".35"/><polygon points="${mtX(0)},${MT_H} ${line} ${mtX(1)},${MT_H}" fill="var(--acc)" opacity=".22" clip-path="url(#wkclip)"/>
  <path d="M${line.replace(/ /g,' L')}" fill="none" stroke="var(--mut)" stroke-width="2" stroke-linejoin="round" stroke-linecap="round" stroke-dasharray="3 6" opacity=".8"/>
  <path class="wkg-done" pathLength="100" d="M${line.replace(/ /g,' L')}" fill="none" stroke="${full?'var(--acc2)':'var(--acc)'}" stroke-width="3.5" stroke-linejoin="round" stroke-linecap="round" stroke-dasharray="${(t*100).toFixed(2)} 100" style="--d:${(t*100).toFixed(2)}"/>
  ${marks}<g class="wkg-run" transform="translate(${rx.toFixed(1)} ${ry.toFixed(1)})"><circle class="wkg-ping" r="8" fill="${full?'var(--acc2)':'var(--acc)'}" opacity=".35"/><circle r="5.5" fill="var(--ink)" stroke="${full?'var(--acc2)':'var(--acc)'}" stroke-width="3"/><text y="-12" text-anchor="middle" style="font-size:17px">${full?'🏆':'🏃'}</text></g></svg>
  <p class="xs mut">${hint}</p></div>`}
// Distance d'une journée « Course », calculée d'après le contenu de la séance : durées × allure de la zone (Z1–Z5, Z2 par défaut), répétitions « N × durée » ou « N × distance », km écrits.
const trZone=z=>{const r=ZN.find(x=>x[0]===z)||ZN[1];return pAt((r[4]+r[5])/2)};
function trainKm(d){
  if(!d)return 0;
  const num=v=>parseFloat(String(v).replace(',','.')),dayZ=((d.items.map(i=>[i.l,i.t].concat(i.sub||[]).join(' ')).join(' ').match(/\bZ([1-5])\b/)||[])[1]),SK=/^(distance|allure|fc|frequence|rpe|ressenti|objectif|but|zone|intensite|duree|total)/;
  const calc=(txt,pz)=>{
    let km=0,N=0,s=' '+txt.replace(/\d+['’]\d*\s*\/\s*km/gi,' ').replace(/\d+\s*bpm/gi,' ').replace(/\d+(?:[.,]\d+)?\s*km\s*\/\s*h/gi,' ')+' ';
    const zm=s.match(/\bZ([1-5])\b/),z=zm?'Z'+zm[1]:pz||(dayZ?'Z'+dayZ:'Z2'),p=trZone(z),pr=trZone('Z1');
    s=s.replace(/(\d+)\s*[×x]\s*(\d+(?:[.,]\d+)?)\s*(km|min|mn|m|'|’|″|"|”|sec|s)(?![a-zA-Zéèêàû])/gi,(_,n,v,u)=>{n=+n;v=num(v);u=u.toLowerCase();N=Math.max(N,n);
      if(u==='km')km+=n*v;else if(u==='m')km+=n*v/1000;else if(u==='min'||u==='mn'||u==="'"||u==='’')km+=n*v/p;else km+=n*v/60/p;return ' '});
    s=s.replace(/(\d+(?:[.,]\d+)?)\s*h\s*(\d{1,2})?(?![\d])/gi,(m,h,mm,i)=>{km+=(num(h)*60+(mm?+mm:0))/p;return ' '});
    s=s.replace(/(\d+)\s*['’]\s*(\d{2})(?!\d)/g,(m,mn,sc,i,str)=>{const rcp=str.search(/r[ée]cup|trot|repos/i),rec=rcp>=0&&i>=rcp;km+=(+mn+ +sc/60)*(rec&&N>1?N:1)/(rec?pr:p);return ' '});
    s=s.replace(/(\d+(?:[.,]\d+)?)\s*(?:min|mn|['’])(?!\d)/gi,(m,v,i,str)=>{const rcp=str.search(/r[ée]cup|trot|repos/i),rec=rcp>=0&&i>=rcp;km+=num(v)*(rec&&N>1?N:1)/(rec?pr:p);return ' '});
    s=s.replace(/(\d+(?:[.,]\d+)?)\s*km\b/gi,(m,v)=>{km+=num(v);return ' '});
    return{km,z}};
  let tot=0;const dur=[];
  d.items.forEach(it=>{const lab=cleanLab(it.l||'');
    if(SK.test(lab)){if(/^(duree|total)/.test(lab))dur.push(it.t||'');return}
    const r0=calc([it.l,it.t].filter(Boolean).join(' '),null);tot+=r0.km;
    (it.sub||[]).forEach(z=>{tot+=calc(z,r0.z).km})});
  if(!(tot>0))dur.forEach(t=>{tot+=calc(t,null).km});
  return tot}
function dayKmTxt(d,r){
  if(!d||!r)return '';const sg=trainSeg(d);
  if(sg===3&&d.date===r.date&&+r.km>0)return `${fn(r.km,1)} km`;
  if(sg!==0&&sg!==3)return '';const km=trainKm(d);return km>=1?`≈ ${fn(km,1)} km`:''}
const dayKmN=(d,r)=>{if(!d)return 0;const sg=trainSeg(d);if(sg===3&&d.date===r.date&&+r.km>0)return +r.km;return sg===0||sg===3?trainKm(d):0};
function monthHTML(kind,r,by,days,sel,t,K){
  const N=kind==='nutri';S.cwMon=S.cwMon||{};let m=S.cwMon[K]||sel.slice(0,7);const fm=days[0].date.slice(0,7),lm=days[days.length-1].date.slice(0,7);if(m<fm)m=fm;if(m>lm)m=lm;S.cwMon[K]=m;
  const [Y,M]=m.split('-').map(Number),nd=new Date(Y,M,0).getDate(),lead=dow(m+'-01'),trail=(7-(lead+nd)%7)%7,inM=days.filter(d=>d.date.slice(0,7)===m);
  const mp=apvProg(kind,inM),mk=N?0:inM.reduce((a,d)=>a+dayKmN(d,r),0),cnt=[0,0,0,0,0];if(!N)inM.forEach(d=>{cnt[trainSeg(d)]++});
  const nav=n=>`<button type="button" class="btn ghost s" data-a="cwMonth" data-k="${kind}" data-s="${n}" ${(n<0?m<=fm:m>=lm)?'disabled':''} aria-label="${n<0?'Mois précédent':'Mois suivant'}">${n<0?'‹':'›'}</button>`;
  let rows='',wk=0,wf=0,wn=0,cells='';
  const flush=()=>{rows+=cells+(N?`<div class="cm-w${wn?'':' z'}">${wn?`<b>${wf}/${wn}</b><small>repas</small>`:'—'}</div>`:`<div class="cm-w${wk>0?'':' z'}">${wk>0?`<b>${fn(wk,0)}</b><small>km</small>`:'—'}</div>`);cells='';wk=0;wf=0;wn=0};
  for(let i=0;i<lead;i++)cells+='<span class="cm-e"></span>';
  for(let d=1;d<=nd;d++){const x=`${m}-${pad(d)}`,p=by[x],dp=p?apvDP(kind,p):{n:0,f:0},n=dp.n,f=dp.f,o=dBetween(r.date,x),isR=N?x===r.date:(p&&trainSeg(p)===3),sg=N?-1:(p?trainSeg(p):-1),km=N?0:dayKmN(p,r);wk+=km;wf+=f;wn+=n;
    const sc=N?(x===r.date?'var(--yel)':'var(--acc2)'):(sg>=0?segCol('train',sg):'var(--line)'),ico=N?(p?(()=>{const us=apvUnits('nutri',p);return us.length?`<span class="cm-ms">${us.map(u=>`<s class="${apvIsDone('nutri',u.id)?'on':''}" title="${esc(SEGS_N[u.seg][0].replace(/^\S+\s/,''))}">${SEGS_N[u.seg][0].split(' ')[0]}</s>`).join('')}</span>`:'🍽️'})():''):(sg>=0?TR_ICO[sg]:''),
      lab=N?(o===0?'🏁 Jour J':o===-1?'Veille':'J'+o):(km>=1?fn(km,0)+' km':sg===2?'repos':'&nbsp;'),
      what=N?(o===0?'jour J':o===-1?'veille':'J'+o):(sg>=0?SEGS_T[sg][0].replace(/^\S+\s/,''):'');
    cells+=`<button type="button" class="cm-d${x===t?' today':''}${x===sel?' sel':''}${n&&f===n?' full':''}${p?'':' off'}${isR?' race':''}" style="--sc:${sc}" data-a="cwDay" data-k="${kind}" data-d="${x}" ${p?'':'disabled'} aria-pressed="${x===sel}" aria-label="${esc(longD(x))}${p?`, ${esc(what)}${km>=1?', environ '+fn(km,0)+' km':''}, ${f} sur ${n} faits`:', rien de prévu'}"><b class="cm-n">${d}</b>${p?`<span class="cm-i">${ico}</span><span class="cm-k">${lab}</span><em class="cm-st">${n&&f===n?'✓':n?`${f}/${n}`:''}</em>`:''}</button>`;
    if(dow(x)===6)flush()}
  if(trail){for(let i=0;i<trail;i++)cells+='<span class="cm-e"></span>';flush()}
  const leg=N?SEGS_N.map(z=>`<span class="chip2"><i style="width:10px;height:10px;border-radius:3px;background:${z[2]};display:inline-block"></i>${esc(z[0])}</span>`).join(''):SEGS_T.map((z,i)=>cnt[i]||i<3?`<span class="chip2"><i style="width:10px;height:10px;border-radius:3px;background:${z[2]};display:inline-block"></i>${esc(z[0])}${cnt[i]?` · <b>${cnt[i]}</b>`:''}</span>`:'').join('');
  const sub=mp.n?(N?`${mp.f}/${mp.n} repas cochés`:`${mp.f}/${mp.n} séances cochées · ≈ ${fn(mk,0)} km prévus`):'Rien de prévu ce mois-ci';
  return `<div class="cw-nav"><button type="button" class="btn ghost s" style="visibility:hidden" aria-hidden="true" tabindex="-1">‹</button>${nav(-1)}<div class="tc"><b class="cond" style="font-size:1.25rem">${MONL[M-1]} ${Y}</b><div class="sm mut">${sub}</div></div>${nav(1)}<button type="button" class="btn ghost s" style="visibility:hidden" aria-hidden="true" tabindex="-1">›</button></div>
  ${weekGam(mp,null,t.slice(0,7)===m,!N,N)}
  <div class="cm" role="group" aria-label="Calendrier du mois de ${MONL[M-1]} ${Y}"><div class="cm-h">${['L','M','M','J','V','S','D'].map(x=>`<i>${x}</i>`).join('')}<i>${N?'✓':'Σ'}</i></div><div class="cm-g">${rows}</div></div>
  <div class="row" style="gap:6px;margin:10px 0">${leg}</div>`}
function coachSection(kind,r){
  const isN=kind==='nutri',pl=aiPlan(kind),t=today(),K=sk(kind);
  const head=false?`<div class="sec"><h2 class="cond">${isN?'Semaine avant la course':'Programme semaine par semaine'}</h2><span class="xs mut">d'après le plan du coach</span></div>`:'';
  let body;
  if(!pl)body=`<div class="empty">Aucun plan du coach enregistré pour « ${esc(r.name)} ».<br>Colle-le dans « Plan du coach » ci-dessus puis enregistre : ${isN?'les 7 jours avant la course':'le programme semaine par semaine'} s'affichera ici, uniquement d'après ce que tu y as écrit.</div>`;
  else{
    let days=pl.days;
    if(isN){const a=addD(r.date,-7),b=r.date;days=days.filter(d=>d.date>=a&&d.date<=b)}
    if(!days.length)body=`<div class="empty">Ton plan du coach ne contient aucun jour entre le ${shortD(addD(r.date,-7))} et le ${shortD(r.date)} (les 7 jours avant la course et le jour J).</div>`;
    else{
      const by={};days.forEach(d=>{by[d.date]=d});S.cwSel=S.cwSel||{};
      let sel=S.cwSel[K];
      if(!sel||!by[sel])sel=by[t]?t:isN?(by[addD(r.date,-1)]?addD(r.date,-1):days[0].date):(days.find(d=>d.date>=t)||days[days.length-1]).date;
      const mon=isN?addD(r.date,-7):monday(sel),dates=Array.from({length:isN?8:7},(_,i)=>addD(mon,i)),wd=dates.map(x=>by[x]).filter(Boolean),wp=apvProg(kind,wd),all=apvProg(kind,days),first=days[0].date,last=days[days.length-1].date,wn=(wd.find(x=>x.week)||{}).week,cur=t>=mon&&t<=addD(mon,6);
      const nav=isN?'':`<div class="cw-nav"><button type="button" class="btn ghost s" data-a="cwWeek" data-k="${kind}" data-s="-1" ${monday(first)>=mon?'disabled':''} aria-label="Semaine précédente">‹</button><div class="tc"><b class="cond">${wn?`Semaine ${wn} · `:''}du ${shortD(mon)} au ${shortD(addD(mon,6))}</b><div class="sm mut">${cur?'Semaine en cours':'&nbsp;'}</div></div><button type="button" class="btn ghost s" data-a="cwWeek" data-k="${kind}" data-s="1" ${addD(mon,7)>last?'disabled':''} aria-label="Semaine suivante">›</button></div>`;
      const cells=dates.map(date=>{const d=by[date],o=dBetween(r.date,date),dp=d?apvDP(kind,d):{n:0,f:0},n=dp.n,f=dp.f,lab=isN?(o===0?'Jour J':o===-1?'Veille':'J'+o):trainIcons(d,date===r.date);
        return `<button type="button" class="cw-c${date===t?' today':''}${date===sel?' sel':''}${n&&f===n?' full':''}" data-a="cwDay" data-k="${kind}" data-d="${date}" ${d?'':'disabled'} aria-pressed="${date===sel}" aria-label="${esc(longD(date))}${isN?(o===0?', jour J':', J'+o):''}${d?`, ${f} sur ${n} faits`:', rien de prévu'}"><small>${DAYS[dow(date)].slice(0,3)}</small><b>${pISO(date).getDate()}</b>${lab?`<span class="${isN?'cw-j':'ic'}">${lab}</span>`:''}<em class="cw-dots" aria-hidden="true">${d?apvUnits(kind,d).map(u=>`<u style="--sc:${segCol(kind,u.seg)}" class="${apvIsDone(kind,u.id)?'on':''}"></u>`).join(''):''}</em><i>${d?`${f}/${n}`:'—'}</i></button>`}).join('');
      const sd=by[sel],o=dBetween(r.date,sel),dp2=apvDP(kind,sd),sn=dp2.n,sf=dp2.f,pct=sn?Math.round(sf/sn*100):0,pg=all.n?Math.round(all.f/all.n*100):0,
        sub=(isN?[o===0?'Jour J':o===-1?'Veille':'J'+o,sd.title||'',`${sf}/${sn} repas faits`]:[sd.title||'',dayKmTxt(sd,r)]).filter(Boolean).map(esc).join(' · '),
        gamN=isN&&(S.cwView||{})[K]==='week'?weekGam(all,null,true,false,true):'',
        wkG=isN?'':weekGam(wp,all,cur);
      S.cwView=S.cwView||{};const mv=S.cwView[K]!=='week',
        sw=`<div class="row" style="margin:4px 0 10px"><button type="button" class="btn ${mv?'ghost':''} s" data-a="cwView" data-k="${kind}" data-v="week">📆 ${isN?'7 jours':'Semaine'}</button><button type="button" class="btn ${mv?'':'ghost'} s" data-a="cwView" data-k="${kind}" data-v="month">🗓️ Mois</button></div>`;
      body=`
      ${sw}${gamN}${mv?monthHTML(kind,r,by,days,sel,t,K):`${nav}${wkG}<div class="cw-cal" role="group" aria-label="${isN?'Calendrier de la semaine avant la course':'Calendrier de la semaine'}">${cells}</div>`}
      <div class="card cw-panel" style="margin-top:12px"><div class="row" style="justify-content:space-between;align-items:center"><div><b class="cond" style="font-size:1.15rem">${esc(longD(sel))}</b><div class="sm mut">${sub}</div></div><div class="row" style="gap:6px"><button type="button" class="btn ghost s" data-a="cwAll" data-k="${kind}" data-o="0">Tout réduire</button><button type="button" class="btn ghost s" data-a="cwAll" data-k="${kind}" data-o="1">Tout déplier</button></div></div>
      ${sn&&sf===sn?'<div class="note good">🎉 Journée validée, bravo !</div>':''}${apvGroups(kind,sd,sel)}${sd.notes.map(x=>`<p class="sm apv-note">📊 ${esc(x)}</p>`).join('')}</div>`}
  }
  return `<div id="cwk-${kind}">${head}${body}</div>`}
function burstAt(el){if(!el||(window.matchMedia&&matchMedia('(prefers-reduced-motion: reduce)').matches))return;const b=el.getBoundingClientRect(),w=document.createElement('div');w.className='burst';w.style.left=(b.left+b.width/2)+'px';w.style.top=(b.top+b.height/2)+'px';
  const C=['#F27A2A','#A9C79B','#E6B84A','#8FBDB5','#E89AAA','#B8A9DC'];
  w.innerHTML=Array.from({length:16},(_,i)=>{const a=i/16*6.283+Math.random()*.4,d=36+Math.random()*44;return `<i style="--c:${C[i%C.length]};--x:${(Math.cos(a)*d).toFixed(0)}px;--y:${(Math.sin(a)*d).toFixed(0)}px;--r:${Math.round(Math.random()*360)}deg"></i>`}).join('');
  document.body.appendChild(w);setTimeout(()=>w.remove(),900)}
function burstFor(k,id){const c=$$('#cwk-'+k+' input[data-c=apvdone]').find(x=>x.dataset.id===id);if(c)burstAt(c)}
function coachRefresh(k,focusId,keep=true){const el=$('#cwk-'+k),r=selRace();if(!el||!r)return;const st=keep?[...el.querySelectorAll('details')].map(d=>d.open):[];
  el.outerHTML=coachSection(k,r);const n=$('#cwk-'+k);if(!n)return;[...n.querySelectorAll('details')].forEach((d,i)=>{if(i<st.length)d.open=st[i]});
  if(focusId){const c=[...n.querySelectorAll('input[data-c=apvdone]')].find(x=>x.dataset.id===focusId);if(c)c.focus()}}
function aiSave(kind){
  D.ai=D.ai||{};D.ai.resp=D.ai.resp||{};D.ai.done=D.ai.done||{};D.ai.start=D.ai.start||{};const K=sk(kind);
  const txt=($('#ai-r-'+kind).value||'').trim();
  if(txt!==(D.ai.resp[K]||'')){D.ai.done[K]={};S.apv&&delete S.apv[kind]}   // nouveau texte : on repart d'un suivi vierge
  D.ai.resp[K]=txt;save();S.keep=true;
  const pl=aiPlan(kind);
  if(!txt)toast('Plan du coach effacé.');
  else if(pl)toast(`Plan du coach enregistré : ${pl.days.length} jours, du ${shortD(pl.first)} au ${shortD(pl.last)}.`);
  else toast("Plan du coach enregistré, mais je n'ai pas reconnu de jours. Présente-le jour par jour (« Jour 1 — lundi 3 novembre », puis une ligne par séance ou repas).",1);
  render()}
function aiClear(kind){if(!confirm('Effacer le plan du coach de cette course et son suivi ?'))return;D.ai=D.ai||{};const K=sk(kind);['resp','done','start'].forEach(x=>{D.ai[x]=D.ai[x]||{};delete D.ai[x][K]});S.apv&&delete S.apv[kind];save();S.keep=true;toast('Plan du coach effacé.');render()}
function renderTrain(){
  const r=selRace();let h=`<div class="wrap"><div class="sec" style="margin-top:0"><h2 class="cond">Plan d'entraînement</h2></div>`;
  if(!r)return h+`<div class="empty">Ajoute ta prochaine course pour générer un plan personnalisé jusqu'au jour J.<br><br><button class="btn" data-a="newRace">➕ Nouvelle course</button></div></div>`;
  h+=raceSelect();
  const _past=r.date<today()||parseT(r.result)>0;
  if(!_past&&!planReady(r))return h+planWait(r)+'</div>';
  h+=aiBlock('train',r);
  if(_past)return h+coachSection('train',r)+'</div>';
  const pl=genPlan(r);S.plan=pl;const cur=pl.weeks.find(w=>w.cur),p=D.profile,ci=cur?cur.i:-1;
  const peakW=pl.weeks.reduce((a,w)=>w.km>a.km?w:a,pl.weeks[0]);
  h+=`<div class="card"><h2 class="cond">${esc(r.name)} · ${pl.days>0?'J-'+pl.days:'Jour J'}</h2><div class="kv"><div><b>${pl.W}</b><span>semaines de plan</span></div><div><b>${pl.base} → ${fn(peakW.km,0)} km</b><span>volume hebdo (départ → pic)</span></div><div><b>+${fn(peakW.dp,0)} m</b><span>D+ hebdo au pic</span></div><div><b>${fmtT(pl.raceMin)}</b><span>durée de course visée</span></div></div>
  <p class="sm mut" style="margin-top:10px">Calculé selon ton niveau (VDOT ${fn(baseVdot(),1)}), tes ${timed().length} chronos, ta base actuelle de <b>${pl.base} km/sem.</b> (source : ${esc(pl.src)}), ${p.sessionsRun} sorties + ${p.sessionsGym} renfos/sem., ton terrain « ${esc(p.terrain)} » (D+ naturel ≈ ${p.dplusAvail||300} m/sem., tapis incliné : ${esc(p.treadmill||'oui')}) et les ${pl.W} semaines restantes. Progression de +8 % maximum par semaine, allègement toutes les 4 semaines, affûtage de ${pl.taperN} semaine${pl.taperN>1?'s':''}.${pl.start>today()?` Le plan démarre le ${longD(pl.start)}.`:''}</p>
  <div class="row" style="margin-top:10px"><button class="btn ghost s" data-a="planReset" data-id="${r.id}">🔄 Régénérer depuis aujourd'hui</button></div></div>`;
  h+=`<div class="card"><h2 class="cond">Zones cardiaques & allures</h2><div class="tscroll"><table><thead><tr><th>Zone</th><th>Ressenti</th><th>FC (bpm)</th><th>Allure sur plat</th></tr></thead><tbody>${ZN.map(z=>`<tr><td><b>${z[0]}</b> · ${z[1]}</td><td>${z[6]}</td><td>${zhr(z[0])[0]}–${zhr(z[0])[1]}</td><td>${zps(z[0])}</td></tr>`).join('')}</tbody></table></div><p class="xs mut" style="margin-top:8px">FC calculées avec la méthode de Karvonen (FC repos ${p.hrRest}, FC max ${p.hrMax}). En côte ou sur sentier, pilote à la FC et à l'effort, pas à l'allure.</p></div>`;
  const wk=cur||pl.weeks[0],prevW=pl.weeks[wk.i-1],missing=cur&&!D.feedback[wk.ws]&&dow(today())>=4,prevMissing=prevW&&!D.feedback[prevW.ws]&&!prevW.sess.every(s=>s.ty==='rest');
  if(missing||prevMissing)h+=`<div class="card" style="border-color:var(--acc)"><h2 class="cond">📝 Bilan de fin de semaine</h2><p class="sm">${missing?`C'est bientôt la fin de la semaine ${wk.i+1} :`:`Le bilan de la semaine ${prevW.i+1} manque :`} réponds à 6 questions (fatigue, sensations, douleurs, disponibilité…) pour que je recalcule les semaines suivantes.</p><div class="row" style="margin-top:10px"><button class="btn s" data-a="bilan" data-k="${missing?wk.ws:prevW.ws}">Remplir le bilan</button></div></div>`;
  h+=`<div class="card"><h2 class="cond">Vue d'ensemble</h2>${trainProgress(pl)}${volChart(pl)}<details class="sc-d"><summary>Voir le tableau semaine par semaine</summary><div class="tscroll"><table><thead><tr><th>Sem.</th><th>Début</th><th>Phase</th><th>Km</th><th>Durée</th><th>D+</th><th>Charge</th></tr></thead><tbody>${pl.weeks.map(w=>`<tr${w.cur?' style="font-weight:800"':''}><td>${w.i+1}${w.cur?' ◀':''}</td><td>${shortD(w.ws)}</td><td>${esc(w.phase)}</td><td>${fn(w.km,0)}</td><td>${fmtT(w.dur)}</td><td>+${fn(w.dp,0)} m</td><td>${w.delta==null?'—':(w.delta>=0?'+':'')+fn(w.delta,0)+' %'}</td></tr>`).join('')}</tbody></table></div></details><p class="xs mut" style="margin-top:8px">Les chiffres de la semaine de course excluent la course elle-même.</p></div>`;
  h+=coachSection('train',r)+'</div>';
  return h}
function openBilan(ws){
  const pl=S.plan,w=pl&&pl.weeks.find(x=>x.ws===ws);if(!w)return;const b=D.feedback[ws]||{},plan=w.sess.filter(s=>s.ty!=='rest'&&s.ty!=='race'),dn=plan.filter(s=>D.done[s.key]).length;
  const sel=(id,opts,val)=>`<select id="${id}">${opts.map(([v,l])=>`<option value="${v}" ${String(v)===String(val)?'selected':''}>${esc(l)}</option>`).join('')}</select>`;
  const f5=l=>l.map((t,i)=>[i+1,`${i+1} · ${t}`]);
  openModal(`<h2 class="cond">Bilan · semaine du ${shortD(ws)}</h2><p class="mut sm">Tes réponses modifient la charge, l'intensité et le nombre de séances dès la semaine suivante.</p><div class="note good">Séances réalisées : <b>${dn} / ${plan.length}</b> (coche-les dans le tableau avant de valider).</div>
  <div class="frm"><label class="f">1 · Fatigue générale${sel('b-fat',f5(['Frais','Plutôt frais','Normale','Fatigué','Épuisé']),b.fatigue||3)}</label><label class="f">2 · Sensations à l'entraînement${sel('b-sen',f5(['Très mauvaises','Mauvaises','Correctes','Bonnes','Excellentes']),b.sens||3)}</label><label class="f">3 · Qualité du sommeil${sel('b-sle',f5(['Très mauvaise','Mauvaise','Moyenne','Bonne','Excellente']),b.sleep||3)}</label><label class="f">4 · Douleurs${sel('b-pain',PAIN,b.pain||'none')}</label><label class="f full">Zone concernée (si douleur)${sel('b-zone',PZONES.map(z=>[z,z]),b.zone||'Genou')}</label>
  <label class="f">5 · Séances de course possibles la semaine prochaine${sel('b-run',[[2,'2 séances'],[3,'3 séances'],[4,'4 séances']],b.availRun||D.profile.sessionsRun||3)}</label><label class="f">Séances de renfo possibles${sel('b-gym',[[0,'Aucune'],[1,'1 séance'],[2,'2 séances']],b.availGym==null||b.availGym===''?D.profile.sessionsGym:b.availGym)}</label><label class="f full">Temps maximum pour la sortie longue${sel('b-long',[['','Pas de limite'],[90,'1 h 30'],[120,'2 h'],[150,'2 h 30'],[180,'3 h'],[210,'3 h 30'],[240,'4 h'],[270,'4 h 30'],[300,'5 h']],b.availLong||'')}</label>
  <label class="f full">6 · Contraintes (travail, voyage, famille, météo…)<input id="b-con" value="${esc(b.constraints||'')}"></label><label class="f full">Notes libres<textarea id="b-not">${esc(b.notes||'')}</textarea></label></div>
  <div class="row" style="margin-top:14px"><button class="btn" data-a="saveBilan" data-k="${ws}">💾 Enregistrer & adapter le plan</button></div>`)}
function saveBilan(ws){
  const pl=S.plan,w=pl&&pl.weeks.find(x=>x.ws===ws),plan=w?w.sess.filter(s=>s.ty!=='rest'&&s.ty!=='race'):[],dn=plan.filter(s=>D.done[s.key]).length,g=id=>$('#'+id).value;
  const pain=g('b-pain');
  D.feedback[ws]={fatigue:+g('b-fat'),sens:+g('b-sen'),sleep:+g('b-sle'),pain,zone:pain==='none'?'':g('b-zone'),availRun:+g('b-run'),availGym:+g('b-gym'),availLong:g('b-long')?+g('b-long'):0,constraints:g('b-con').trim(),notes:g('b-not').trim(),done:plan.length?Math.round(dn/plan.length*100):'',planned:plan.length,saved:today()};
  save();closeModal();S.keep=true;toast('Bilan enregistré : les semaines suivantes sont recalculées.');render()}

/* ============================ NUTRITION ============================ */
const DEFAULT_FOODS=[{id:'f-iso',name:'ISO+ Decathlon',carbs:33,kind:'drink'},{id:'f-gb',name:'Gels Baouw',carbs:30,kind:'food'},{id:'f-pb',name:'Purée Baouw',carbs:15,kind:'food'},{id:'f-gd',name:'Gels Decathlon 1:0.8',carbs:40,kind:'food'},{id:'f-pf',name:'Pâte de fruits Decathlon',carbs:21,kind:'food'},{id:'f-gl',name:'Gels Long Nutripure',carbs:30,kind:'food'},{id:'f-cola',name:'Hydrogel caféine cola Decathlon',carbs:23,kind:'food'}];
function foodsList(){const p=D.profile;if(!Array.isArray(p.foods))p.foods=JSON.parse(JSON.stringify(DEFAULT_FOODS));return p.foods}
// Plan de ravitaillement : eau + iso+ obligatoires chaque heure ; le complément de glucides est réparti en alternant les aliments de la liste.
function fuelPlan(T){
  const F=fuel(T),foods=foodsList(),drink=foods.find(f=>f.kind==='drink'),solids=foods.filter(f=>f.kind!=='drink'&&+f.carbs>0);
  const isoC=drink&&F.iso?Math.round((+drink.carbs||0)*F.iso/500):0,comp=Math.max(0,F.cph-isoC),ev=[];let planned=0,ptr=0,caf=0;
  if(F.cph&&comp>0&&solids.length){
    for(let t=15;t<=T-15;t+=5){const target=comp*t/60;
      for(let k=0;k<solids.length;k++){const f=solids[ptr%solids.length],isCaf=/caf[eé]ine/i.test(f.name);
        if(isCaf&&(t<T*.55||caf>=3)){ptr++;continue}
        if(target-planned>=(+f.carbs)*.55){ev.push({t,f});planned+=+f.carbs;ptr++;if(isCaf)caf++}
        break}}}
  return{F,drink,isoC,comp,ev,planned}}
function fuelPlanHTML(r,T){
  const P=fuelPlan(T),F=P.F;if(!F.cph)return '';
  const st=/^\d{1,2}:\d{2}$/.test(r.startTime||'')?r.startTime.split(':').map(Number):null,clk=t=>{if(!st)return '';const m=st[0]*60+st[1]+t;return ` (${pad(Math.floor(m/60)%24)}:${pad(Math.floor(m%60))})`},fm=t=>`${Math.floor(t/60)}:${pad(Math.round(t%60)%60)}`;
  const nh=Math.ceil(T/60),rows=[];
  for(let h=0;h<nh;h++){const frac=Math.min(1,(T-h*60)/60),evs=P.ev.filter(e=>Math.floor(e.t/60)===h),sol=evs.reduce((a,e)=>a+ +e.f.carbs,0),ig=Math.round(P.isoC*frac);
    rows.push(`<tr><td><b>H${h+1}</b><br><span class="xs mut">${fm(h*60)}–${fm(Math.min(T,(h+1)*60))}</span></td><td>💧 ${Math.round(F.water*frac)} ml d'eau${F.iso?`<br>🥤 ${Math.round(F.iso*frac)} ml d'iso+ (${ig} g)`:''}${evs.map(e=>`<br>⏱️ ${fm(e.t)}${clk(e.t)} · ${esc(e.f.name)} (${fn(+e.f.carbs,0)} g)`).join('')}</td><td style="white-space:nowrap"><b>${ig+sol} g</b></td></tr>`)}
  const cnt={};P.ev.forEach(e=>{cnt[e.f.name]=(cnt[e.f.name]||0)+1});
  const pack=Object.entries(cnt).map(([n,c])=>`${c} × ${esc(n)}`).join(' · '),tot=Math.round(P.isoC*T/60+P.planned);
  return `<div class="kv" style="margin:6px 0"><div><b>${F.cph} g/h</b><span>objectif glucides</span></div><div><b>${P.isoC} g/h</b><span>via l'iso+ (${F.iso} ml/h)</span></div><div><b>${P.comp} g/h</b><span>à compléter avec tes aliments</span></div><div><b>${tot} g</b><span>glucides prévus au total</span></div></div>
  <div class="tscroll" style="margin-top:10px"><table><thead><tr><th>Heure</th><th>Plan</th><th>Glucides</th></tr></thead><tbody>${rows.join('')}</tbody></table></div>
  <p class="sm" style="margin-top:10px"><b>À emporter :</b> ${pack||'—'} · eau ≈ ${fn(F.water*T/60000,1)} L · iso+ ≈ ${fn(F.iso*T/60000,1)} L. Prévois environ 20 % de marge (au moins une prise de rechange par type).</p>
  <p class="xs mut">Les aliments sont alternés dans l'ordre de ta liste. Les prises commencent après ~15 min et s'arrêtent 15 min avant l'arrivée ; les produits à la caféine ne sont proposés qu'en seconde moitié (3 au maximum).</p>`}
function foodsEditor(){const fl=foodsList();
  return `<h3 class="cond" style="margin:18px 0 6px">Aliments de course</h3><p class="xs mut" style="margin-bottom:10px">Eau et iso+ sont pris à chaque heure (valeurs ci-dessus). Le complément de glucides est réparti en alternant les aliments de type « Aliment » ; le type « Boisson » indique les glucides de 500 ml d'iso+. Les modifications sont enregistrées immédiatement.</p>${fl.map(f=>`<div class="row" style="gap:8px;align-items:flex-end;margin-bottom:8px"><label class="f" style="flex:1 1 180px">Nom<input data-c="food" data-f="name" data-id="${esc(f.id)}" value="${esc(f.name)}"></label><label class="f" style="flex:0 0 96px">Glucides (g)<input type="number" step="any" inputmode="decimal" data-c="food" data-f="carbs" data-id="${esc(f.id)}" value="${esc(f.carbs)}"></label><label class="f" style="flex:0 0 170px">Type<select data-c="food" data-f="kind" data-id="${esc(f.id)}"><option value="food" ${f.kind!=='drink'?'selected':''}>Aliment (par prise)</option><option value="drink" ${f.kind==='drink'?'selected':''}>Boisson (par 500 ml)</option></select></label><button class="btn red s" data-a="foodDel" data-id="${esc(f.id)}" aria-label="Supprimer ${esc(f.name)}">✕</button></div>`).join('')}<div class="row" style="margin-top:6px"><button class="btn ghost s" data-a="foodAdd">➕ Ajouter un aliment</button><button class="btn ghost s" data-a="foodReset">Remettre ma liste d'origine</button></div>`}
function fuel(min){const h=min/60,pf=D.profile,cMax=+pf.nutriCarbs>0?+pf.nutriCarbs:75,wa=pf.nutriWater===''||pf.nutriWater==null||!(+pf.nutriWater>=0)?500:+pf.nutriWater,isoP=pf.nutriIso===''||pf.nutriIso==null||!(+pf.nutriIso>=0)?500:+pf.nutriIso;
  const cph=h<.75?0:h<1.5?Math.min(30,cMax):cMax,water=h<1?Math.min(wa,300):wa,iso=h<1?0:isoP;return{h,cph,water,iso,fl:water+iso,na:h<2?0:h<6?500:600,every:cph?Math.round(25/cph*60):0,tot:Math.round(cph*h),gels:Math.ceil(cph*h/25)}}
function renderNutri(){
  const r=selRace();let h=`<div class="wrap"><div class="sec" style="margin-top:0"><h2 class="cond">Plan nutritionnel</h2></div>`;
  if(!r)return h+'<div class="empty">Ajoute une course pour créer ta stratégie.<br><br><button class="btn" data-a="newRace">➕ Nouvelle course</button></div></div>';
  h+=raceSelect();h+=aiBlock('nutri',r);const d0=dBetween(today(),r.date);
  if(d0<0)return h+coachSection('nutri',r)+'</div>';
  const sc=scenarios(r),gm=parseT(r.goal)||sc.real,F=fuel(gm),w=D.profile.weightTaper,long=gm>=90;
  const P=fuelPlan(gm),pf=D.profile,ex=(F.cph?Math.round(F.cph*gm/60):0),isoT=Math.round(P.isoC*gm/60),solT=Math.round(P.planned),mx=Math.max(1,isoT+solT);
  const num=(k,l,u,v)=>`<label class="f">${l} (${u})<input type="number" step="any" inputmode="decimal" data-c="nset" data-k="${k}" value="${esc(pf[k]===''||pf[k]==null?v:pf[k])}"></label>`;
  h+=`<div class="card today-card"><div class="row" style="justify-content:space-between"><h2 class="cond" style="margin:0">🏁 Ma stratégie · ${esc(r.name)}</h2><span class="syncb">🔗 Synchronisée avec ton profil</span></div>
  <div class="fsum"><div><i>⏱️</i><b>${fmtT(gm)}</b><span>durée${parseT(r.goal)?' visée':' estimée'}</span></div><div><i>🍬</i><b>${F.cph} g/h</b><span>glucides</span></div><div><i>💧</i><b>${F.water} ml/h</b><span>eau</span></div>${F.iso?`<div><i>🥤</i><b>${F.iso} ml/h</b><span>iso+</span></div>`:''}<div><i>⚖️</i><b>${w} kg</b><span>poids d'affûtage</span></div></div>
  ${F.cph?`<p class="xs mut" style="margin-top:8px">D'où viennent tes ${ex} g de glucides prévus :</p><div class="stack" role="img" aria-label="Iso+ ${isoT} g, aliments ${solT} g"><i style="width:${isoT/mx*100}%;background:var(--ice)"></i><i style="width:${solT/mx*100}%;background:var(--acc)"></i></div><div class="leg"><span>🥤 Iso+ <b>${isoT} g</b></span><span>🍌 Aliments <b>${solT} g</b> (${P.ev.length} prises)</span></div>`:''}
  <details class="meal" style="margin-top:12px"><summary><span>⚙️ Ajuster mes quantités et mes aliments</span></summary><div><p class="xs mut" style="margin-bottom:8px">Tout est lié : modifie une valeur et le plan de course, les repas, la fiche jour J et les objectifs de chaque course se recalculent aussitôt.</p><div class="frm">${num('nutriWater','Eau','ml/h',500)}${num('nutriIso','Iso+','ml/h',500)}${num('nutriCarbs','Glucides','g/h',75)}</div>${foodsEditor()}</div></details></div>`;
  h+=coachSection('nutri',r);
  return h}

/* ============================ OBJECTIFS ============================ */
function goalsHTML(r){
  let h='';
    const sc=scenarios(r),i=raceInfo(r),c=sc.c,vd=baseVdot(),g=parseT(r.goal);
  const card=(t,m,col,txt)=>`<div class="card" style="border-top:4px solid ${col}"><span class="tag">${t}</span><div class="cond" style="font-size:2.1rem;margin:8px 0 2px;color:${col}">${fmtT(m)}</div><p class="sm">${pace(m/r.km)}/km · ${fn(r.km/(m/60),1)} km/h · ${pace(m/i.E)}/km-effort</p><p class="sm mut" style="margin-top:6px">${txt}</p></div>`;
  h+=`<div class="card"><h2 class="cond">Objectif chrono</h2>${g?`<p class="sm" style="margin-top:10px">Ton objectif actuel : <b>${esc(r.goal)}</b> — ${g<sc.amb*.99?'plus ambitieux que le scénario ambitieux ci-dessous : très risqué.':g<sc.real?'entre ambitieux et réalisable.':g<sc.mod?'entre réalisable et modeste.':'plus prudent que le scénario modeste.'}</p>`:'<p class="sm mut">Aucun objectif chrono saisi : les trois scénarios ci-dessous servent de repère. Renseigne « Objectif chrono » dans le formulaire plus bas, puis régénère.</p>'}</div>
  ${feelCard()}
  <div class="grid" style="grid-template-columns:repeat(auto-fit,minmax(170px,1fr))">${card('Ambitieux',sc.amb,'var(--acc)','Conditions idéales et forme au niveau de tes meilleures sorties. ≈ −6 % sur le réalisable.')}${card('Réalisable',sc.real,'var(--acc2)','Course bien gérée, au niveau de tes chronos récents et de ton indice trail.')}${card('Modeste',sc.mod,'var(--ice)','Légère baisse de forme ou imprévus raisonnables. ≈ +7 %.')}</div>
  ${racePlan(r,sc)}
  ${r.date>=today()&&!parseT(r.result)?`<div class="card"><h2 class="cond">Jour J</h2><p class="sm mut">Une fiche lisible sur téléphone, imprimable ou exportable en PDF : temps de passage avec fourchette, heures de passage et nutrition.</p><div class="row" style="margin-top:10px"><button class="btn lime s" data-a="fiche" data-id="${r.id}">🏁 Ouvrir la fiche jour J</button></div></div>`:''}
  ${refCard(r,sc)}
  ${hypCard(r,sc)}
  <details class="card hist"><summary><h2 class="cond" style="display:inline-block;margin:0">Comment c'est calculé</h2></summary><ol class="sm" style="padding-left:18px;line-height:1.7"><li><b>Niveau :</b> ${vd?`tes ${routeRaces().length} performances route (5, 10, 15 km et semi) donnent un VDOT de <b>${fn(vd,1)}</b> (modèle de Daniels). Base : ta VO₂max montre (${D.profile.vo2}) recalée par tes records route (facteur borné entre 0,8 et 1,1).`:'VO₂max de la montre (aucun record route saisi).'}</li><li><b>Parcours :</b> distance + D+/100 = <b>${fn(i.E,0)} km-effort</b>. Le temps croît plus vite que la distance au-delà de 42 km (exposant 1,15).</li><li><b>Calibrage trail :</b> ${c.n?`comparé aux ${c.n} courses chronométrées les plus proches de ce parcours, le modèle brut est ajusté de <b>×${fn(c.k,2)}</b> (moyenne pondérée par la récence, atténuée par prudence).`:'aucune course chronométrée : coefficient prudent ×1,06 (terrain d\'entraînement plat).'}</li><li><b>Scénarios :</b> ambitieux ×0,94 · réalisable ×1 · modeste ×1,07.</li></ol>
  
  <div class="note" style="margin-top:12px">Une estimation n'est pas une promesse : la météo, la technicité du terrain (le D− et les sections techniques ne sont pas modélisés finement), ton état de forme et ton poids d'affûtage (${D.profile.weightTaper} kg) peuvent la faire bouger de plusieurs %. Plus tu enregistres de courses chronométrées, plus elle devient précise.</div></details>`;
  return h}

// Profil [[km, altitude]…] (≈160 points) : assez léger pour être stocké avec la course.
function downProf(cum,ele,n=160){
  const tot=cum[cum.length-1];if(!(tot>0)||cum.length<4||ele.filter(isFinite).length<ele.length*.5)return null;
  let last=ele.find(isFinite);const fe=ele.map(v=>isFinite(v)?(last=v):last),out=[];let j=0;
  for(let k=0;k<=n;k++){const x=tot*k/n;while(j<cum.length-1&&cum[j]<x)j++;out.push([+x.toFixed(2),Math.round(fe[j])])}
  return out}
/* ============================ ANALYSE DU PARCOURS (GPX) ============================ */
// Profil interactif coloré par pente, carte synchronisée, montées / descentes marquantes, répartition des pentes.
const GCOL=['#3F6FA8','#5B93C7','#8FBDB5','#A9C79B','#E6B84A','#F27A2A','#D8452B'],GBIN=[[-99,-15],[-15,-8],[-8,-3],[-3,3],[3,8],[8,15],[15,99]],GLAB=['< −15 %','−15 à −8 %','−8 à −3 %','−3 à +3 %','+3 à +8 %','+8 à +15 %','> +15 %'];
const gBin=g=>{const i=GBIN.findIndex(b=>g>=b[0]&&g<b[1]);return i<0?3:i};
let GPM=null,GPC=null;
const kmStep=gk=>gk<=12?1:gk<=30?5:gk<=90?10:gk<=180?20:25;
function mapBase(map){
  const T={'⛰️ Relief':L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png',{maxZoom:17,className:'t-tint',attribution:'© OpenTopoMap · © OpenStreetMap'}),
    '🗺️ Plan':L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{maxZoom:19,className:'t-tint',attribution:'© OpenStreetMap'}),
    '🛰️ Satellite':L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}',{maxZoom:18,attribution:'© Esri'})};
  T['⛰️ Relief'].addTo(map);
  L.control.layers(T,null,{position:'topright',collapsed:true}).addTo(map);
  L.control.scale({imperial:false,position:'bottomleft'}).addTo(map);
  return T}
const mapPin=(cls,txt,sz)=>L.divIcon({className:'gp-pin',html:`<span class="${cls}">${txt}</span>`,iconSize:[sz,sz],iconAnchor:[sz/2,sz/2]});
function gpxSteps(prof){
  const n=prof.length,st=[];
  for(let i=1;i<n;i++){const d=prof[i][0]-prof[i-1][0];if(!(d>0))continue;
    const a=Math.max(0,i-2),b=Math.min(n-1,i+1),dd=prof[b][0]-prof[a][0],g=dd>0?(prof[b][1]-prof[a][1])/(dd*1000)*100:0;
    st.push({i,a:prof[i-1][0],b:prof[i][0],za:prof[i-1][1],zb:prof[i][1],d,dz:prof[i][1]-prof[i-1][1],g})}
  return st}
function gpxAnalysis(r){
  const prof=r.prof,st=gpxSteps(prof),gk=prof[prof.length-1][0],ys=prof.map(q=>q[1]),dist=Array(7).fill(0),up=Array(7).fill(0);
  let dU=0,dD=0,dF=0,zU=0,zD=0,gmax=-99,gmin=99;
  st.forEach(s=>{const k=gBin(s.g);dist[k]+=s.d;if(s.dz>0)up[k]+=s.dz;
    if(s.g>=3){dU+=s.d;if(s.dz>0)zU+=s.dz}else if(s.g<=-3){dD+=s.d;zD+=Math.max(0,-s.dz)}else dF+=s.d;
    if(s.g>gmax)gmax=s.g;if(s.g<gmin)gmin=s.g});
  if(!st.length){gmax=0;gmin=0}
  return{st,gk,dist,up,dU,dD,dF,zU,zD,gmax,gmin,hi:Math.max(...ys),lo:Math.min(...ys),avgUp:dU>0?zU/(dU*1000)*100:0,avgDn:dD>0?zD/(dD*1000)*100:0}}
const climbDiff=x=>x.up>=800||(x.up>=500&&x.grade>=12)?['🔴','Très dure']:x.up>=400||(x.up>=250&&x.grade>=10)?['🟠','Dure']:x.up>=200?['🟡','Soutenue']:['🟢','Courte'];
const descDiff=x=>x.grade<=-12?['⚠️','Très raide']:x.grade<=-8?['🟠','Raide']:x.grade<=-5?['🟡','Soutenue']:['🟢','Roulante'];
function gpxPanel(r){
  const prof=r.prof,res=parseT(r.result),T=res||parseT(r.goal)||scenarios(r).real,tc=trailCost(r),A=gpxAnalysis(r),gk=A.gk,secs=sectionTimes(profSections(prof),T,tc),gx=r.gx||{},
    dp=gx.dp!=null?gx.dp:Math.round(+r.dplus||0),dm=gx.dm!=null?gx.dm:(r.dminus!==''&&r.dminus!=null?Math.round(+r.dminus):null);
  const nr=window.innerWidth<600,W=nr?340:700,H=nr?230:270,PL=46,PR=10,PT=26,PB=26,iw=W-PL-PR,ih=H-PT-PB,pd=Math.max(10,(A.hi-A.lo)*.1),y0=A.lo-pd,y1=A.hi+pd,X=k=>PL+k/gk*iw,Y=m=>PT+(y1-m)/(y1-y0)*ih,f=v=>v.toFixed(1),base=Y(y0);
  const inSec=(x,q)=>A.st.filter(z=>z.a>=x.a-1e-6&&z.b<=x.b+1e-6).map(z=>z.g);
  const climbs=secs.filter(x=>x.type==='montée'&&x.up>=80).map((x,j)=>{const g=inSec(x);return{...x,n:j+1,gmax:g.length?Math.max(...g):x.grade}});
  const desc=secs.filter(x=>x.type==='descente'&&x.dn>=100).sort((a,b)=>b.dn-a.dn).slice(0,5).map(x=>{const g=inSec(x);return{...x,gmin:g.length?Math.min(...g):x.grade}});
  const quads=A.st.map(s=>`<polygon points="${f(X(s.a))},${f(Y(s.za))} ${f(X(s.b))},${f(Y(s.zb))} ${f(X(s.b))},${f(base)} ${f(X(s.a))},${f(base)}" fill="${GCOL[gBin(s.g)]}" opacity=".8"/>`).join('');
  const line=`<polyline points="${prof.map(q=>`${f(X(q[0]))},${f(Y(q[1]))}`).join(' ')}" fill="none" stroke="var(--ink)" stroke-width="1.8" stroke-linejoin="round"/>`;
  const badges=climbs.map(c=>{const q=prof.find(z=>z[0]===c.b)||prof[prof.length-1];return `<g><title>Montée ${c.n} · +${c.up} m · ${fn(c.d,1)} km</title><circle cx="${f(X(c.b))}" cy="${f(Y(q[1])-13)}" r="9" fill="var(--acc)"/><text x="${f(X(c.b))}" y="${f(Y(q[1])-9.5)}" text-anchor="middle" style="fill:#1A0F07;font-size:10px;font-weight:800">${c.n}</text></g>`}).join('');
  const yt=[0,1,2,3].map(i=>A.lo+(A.hi-A.lo)*i/3),ky=gk<=25?5:gk<=60?10:gk<=120?20:25,kt=[];for(let k=0;k<=gk+.01;k+=ky)kt.push(k);
  const axes=yt.map(m=>`<line class="gl" x1="${PL}" x2="${W-PR}" y1="${f(Y(m))}" y2="${f(Y(m))}"/><text x="${PL-6}" y="${f(Y(m)+4)}" text-anchor="end">${Math.round(m)} m</text>`).join('')+kt.map(k=>`<text x="${f(X(k))}" y="${H-8}" text-anchor="middle">${fn(k,0)}${k===kt[kt.length-1]?' km':''}</text>`).join('');
  const gi=Array(prof.length).fill(0);A.st.forEach(s=>{gi[s.i]=s.g;if(s.i>0&&!gi[s.i-1])gi[s.i-1]=s.g});
  GPC={W,PL,iw,gk,prof,gi,X,Y,T,tc,trk:r.trk,mk:null};
  const tt={'montée':0,'plat':0,'descente':0};secs.forEach(x=>{tt[x.type]+=x.t});
  const tsum=tt['montée']+tt['plat']+tt['descente']||1,dsum=A.dU+A.dF+A.dD||1,pc=(a,b)=>fn(a/b*100,0),
    stack=(a,b,c)=>`<div class="stack"><i style="width:${a}%;background:#F27A2A" title="Montée"></i><i style="width:${b}%;background:#A9C79B" title="Plat"></i><i style="width:${c}%;background:#5B93C7" title="Descente"></i></div>`;
  const totD=A.dist.reduce((a,b)=>a+b,0)||1;
  const hist=A.dist.map((d,k)=>`<div class="gp-hr"><span class="gp-hl"><i style="background:${GCOL[k]}"></i>${GLAB[k]}</span><span class="gp-hb"><b style="width:${(d/totD*100).toFixed(1)}%;background:${GCOL[k]}"></b></span><span class="gp-hv">${fn(d,1)} km · ${fn(d/totD*100,0)} %</span></div>`).join('');
  const cards=[['📏',fn(gk,1)+' km','distance GPX','var(--ice)'],['⛰️','+'+fn(dp,0)+' m','dénivelé positif','var(--acc)'],['📉',dm==null?'—':'−'+fn(dm,0)+' m','dénivelé négatif','var(--ice)'],['⚡',fn(gk+dp/100,0),'km-effort','var(--acc2)'],['🔝',A.hi+' m','altitude max','var(--vio)'],['🕳️',A.lo+' m','altitude min','var(--mut)'],['📈','+'+fn(A.avgUp,1)+' %','pente moy. en montée','var(--yel)'],['🧗','+'+fn(Math.max(0,A.gmax),0)+' %','pente max (lissée)','var(--bad)']];
  const crow=climbs.map(c=>{const [ic,lb]=climbDiff(c);return `<tr><td><b class="gp-n">${c.n}</b></td><td>${fn(c.a,1)} → ${fn(c.b,1)}</td><td>${fn(c.d,1)} km</td><td>+${c.up} m</td><td>${fn(c.grade,1)} %<br><span class="xs mut">max ${fn(c.gmax,0)} %</span></td><td>${ic} ${lb}</td><td><b>${fmtT(c.t)}</b></td></tr>`}).join('');
  const drow=desc.map(x=>{const [ic,lb]=descDiff(x);return `<tr><td>${fn(x.a,1)} → ${fn(x.b,1)}</td><td>${fn(x.d,1)} km</td><td>−${x.dn} m</td><td>${fn(x.grade,1)} %<br><span class="xs mut">max ${fn(x.gmin,0)} %</span></td><td>${ic} ${lb}</td><td><b>${fmtT(x.t)}</b></td></tr>`}).join('');
  const tbl=secTable(secs);
  const gap=r.km>0&&Math.abs(gk/r.km-1)>.03?`<p class="xs mut" style="margin-top:6px">⚠️ Le GPX mesure ${fn(gk,1)} km, la course est enregistrée à ${fn(r.km,1)} km : l'analyse suit le GPX.</p>`:'';
  const hasMap=Array.isArray(r.trk)&&r.trk.length===prof.length;
  return `<details class="card hist fold gpxp">${foldHead('🛰️','Analyse du parcours',`${fn(gk,1)} km · ${climbs.length} montée${climbs.length>1?'s':''}`)}
  <div class="gp-stats">${cards.map((c,i)=>`<div class="gp-st" style="--c:${c[3]};animation-delay:${i*45}ms"><i>${c[0]}</i><b>${c[1]}</b><span>${c[2]}</span></div>`).join('')}</div>
  <h3 class="cond gp-h">Profil interactif</h3><div class="gp-tip" id="gp-tip">👆 Survole ou glisse sur le profil : km, altitude, pente et temps estimé s'affichent ici.</div>
  <div class="chartbox"><svg id="gp-svg" class="chart" viewBox="0 0 ${W} ${H}" style="min-width:0" role="img" aria-label="Profil d'altitude coloré par pente, ${fn(gk,1)} km, de ${A.lo} à ${A.hi} m">${axes}${quads}${line}${badges}<line id="gp-cur" x1="0" x2="0" y1="${PT}" y2="${f(base)}" stroke="var(--ink)" stroke-width="1.5" stroke-dasharray="4 3" visibility="hidden"/><circle id="gp-dot" r="5.5" fill="var(--acc)" stroke="var(--ink)" stroke-width="2" visibility="hidden"/><rect id="gp-hit" x="${PL}" y="${PT}" width="${iw}" height="${ih}" fill="transparent"/></svg></div>
  <div class="gp-leg">${GLAB.map((l,k)=>`<span><i style="background:${GCOL[k]}"></i>${l}</span>`).join('')}<span><i class="gp-bd">1</i>montée marquante</span></div>
  ${hasMap?`<h3 class="cond gp-h">Trace sur la carte</h3><div id="gp-map" class="gp-map" role="region" aria-label="Carte de la trace"></div><p class="xs mut" style="margin:0 0 6px">Trace colorée selon la pente (mêmes couleurs que le profil) · repère tous les ${kmStep(gk)} km · bouton en haut à droite pour changer de fond (relief, plan, satellite).</p>`:`<p class="sm mut" style="margin:8px 0">Pour afficher la trace sur la carte, réimporte le GPX de cette course (bouton « Remplacer le GPX » en bas de ce bloc).</p>`}
  <h3 class="cond gp-h">Répartition des pentes</h3>${hist}
  <h3 class="cond gp-h">Terrain</h3>
  <p class="xs mut">Distance</p>${stack(pc(A.dU,dsum),pc(A.dF,dsum),pc(A.dD,dsum))}<div class="leg"><span>▲ montée <b>${pc(A.dU,dsum)} %</b></span><span>▶ plat <b>${pc(A.dF,dsum)} %</b></span><span>▼ descente <b>${pc(A.dD,dsum)} %</b></span></div>
  <p class="xs mut" style="margin-top:8px">Temps estimé (${fmtT(T)})</p>${stack(pc(tt['montée'],tsum),pc(tt['plat'],tsum),pc(tt['descente'],tsum))}<div class="leg"><span>▲ montée <b>${fmtT(tt['montée'])}</b></span><span>▶ plat <b>${fmtT(tt['plat'])}</b></span><span>▼ descente <b>${fmtT(tt['descente'])}</b></span></div>
  <h3 class="cond gp-h">Montées marquantes</h3>${climbs.length?`<div class="tscroll"><table class="nw"><thead><tr><th>#</th><th>Km</th><th>Longueur</th><th>D+</th><th>Pente</th><th>Difficulté</th><th>Temps</th></tr></thead><tbody>${crow}</tbody></table></div>`:'<p class="sm mut">Aucune montée de plus de 80 m de D+ détectée.</p>'}
  <h3 class="cond gp-h">Descentes marquantes</h3>${desc.length?`<div class="tscroll"><table class="nw"><thead><tr><th>Km</th><th>Longueur</th><th>D−</th><th>Pente</th><th>Profil</th><th>Temps</th></tr></thead><tbody>${drow}</tbody></table></div>`:'<p class="sm mut">Aucune descente de plus de 100 m de D− détectée.</p>'}
  <details class="hist" style="padding:12px 0 0"><summary><b class="cond">Toutes les sections (${secs.length})</b></summary><div style="margin-top:8px">${tbl}</div></details>
  <p class="xs mut" style="margin-top:10px">Temps cible ${fmtT(T)} (${res?'ton chrono réel':parseT(r.goal)?'ton objectif':'scénario réalisable'}) réparti selon la pente de chaque portion (descentes moins coûteuses, dérive de fatigue incluse). Pentes lissées sur ~3 points du profil : estimation, à ajuster au terrain réel.</p>${gap}
  <div class="row noprint" style="margin-top:8px"><button class="btn ghost s" data-a="gpxFor" data-id="${r.id}">📈 Remplacer le GPX</button><button class="btn lime s" data-a="gpxSync" data-id="${r.id}">🔄 Recalculer km / D+ / D− d'après le GPX</button><button class="btn red s" data-a="profDel" data-id="${r.id}">Retirer le profil</button></div></details>`}
function gpCursor(km){
  const C=GPC;if(!C)return;const cur=$('#gp-cur'),dot=$('#gp-dot'),tip=$('#gp-tip');if(!cur||!dot)return;
  if(km==null){cur.setAttribute('visibility','hidden');dot.setAttribute('visibility','hidden');if(C.mk&&GPM)GPM.removeLayer(C.mk);return}
  const n=C.prof.length,fi=km/C.gk*(n-1),i0=Math.max(0,Math.min(n-1,Math.floor(fi))),i1=Math.min(n-1,i0+1),w=fi-i0,z=C.prof[i0][1]+(C.prof[i1][1]-C.prof[i0][1])*w,g=C.gi[Math.round(fi)]||0,x=C.X(km),tm=C.tc?C.T*C.tc.at(km):C.T*km/C.gk;
  cur.setAttribute('x1',x);cur.setAttribute('x2',x);cur.setAttribute('visibility','visible');dot.setAttribute('cx',x);dot.setAttribute('cy',C.Y(z));dot.setAttribute('visibility','visible');
  if(tip)tip.innerHTML=`<b>km ${fn(km,1)}</b> · ${Math.round(z)} m · pente <b style="color:${GCOL[gBin(g)]}">${g>0?'+':''}${fn(g,1)} %</b> · ⏱️ ${fmtT(tm)} écoulées`;
  if(C.mk&&GPM&&C.trk){const q=C.trk[Math.round(fi)];if(q){C.mk.setLatLng(q);if(!GPM.hasLayer(C.mk))C.mk.addTo(GPM)}}}
function initGpx(id){
  const r=D.races.find(x=>x.id===id),hit=$('#gp-hit');if(!r||!GPC||!hit)return;
  const C=GPC,mv=e=>{const svg=$('#gp-svg');if(!svg)return;const bb=svg.getBoundingClientRect(),x=(e.clientX-bb.left)/bb.width*C.W;gpCursor(Math.max(0,Math.min(C.gk,(x-C.PL)/C.iw*C.gk)))};
  hit.addEventListener('pointermove',mv);hit.addEventListener('pointerdown',mv);hit.addEventListener('pointerleave',e=>{if(e.pointerType==='mouse')gpCursor(null)});
  const el=$('#gp-map');
  if(el&&typeof L!=='undefined'&&Array.isArray(r.trk)){
    try{GPM=L.map(el,{scrollWheelZoom:false,zoomSnap:.25});mapBase(GPM);
      const tk=r.trk,n=tk.length,gi=C.gi,gk=C.gk,ks=kmStep(gk);
      L.polyline(tk,{color:'#fff',weight:10,opacity:.92,lineJoin:'round',lineCap:'round',interactive:false}).addTo(GPM);
      for(let i=0;i<n-1;i++)L.polyline([tk[i],tk[i+1]],{color:GCOL[gBin(gi[i+1]||gi[i]||0)],weight:5.5,opacity:1,lineJoin:'round',lineCap:'round',interactive:false}).addTo(GPM);
      for(let k=ks;k<gk-ks*.35;k+=ks)L.marker(tk[Math.round(k/gk*(n-1))],{icon:L.divIcon({className:'gp-km',html:`<span>${k}</span>`,iconSize:[22,22],iconAnchor:[11,11]}),interactive:false,keyboard:false}).addTo(GPM);
      const bd=L.latLngBounds(tk.map(p=>L.latLng(p[0],p[1]))).pad(.12);GPM.fitBounds(bd,{animate:false});
      if(L.latLng(tk[0]).distanceTo(L.latLng(tk[n-1]))<150)L.marker(tk[0],{icon:mapPin('up big','🏁',38)}).addTo(GPM).bindTooltip('Départ / Arrivée');
      else{L.marker(tk[0],{icon:mapPin('pa','▶',32)}).addTo(GPM).bindTooltip('Départ');L.marker(tk[n-1],{icon:mapPin('up','🏁',34)}).addTo(GPM).bindTooltip('Arrivée')}
      C.mk=L.circleMarker(tk[0],{radius:9,color:'#1A0F07',weight:3,fillColor:'#fff',fillOpacity:1});
      const Fit=L.Control.extend({options:{position:'topleft'},onAdd(){const w=L.DomUtil.create('div','leaflet-bar'),x=L.DomUtil.create('a','gp-fit',w);x.href='#';x.title='Recentrer sur la trace';x.setAttribute('role','button');x.setAttribute('aria-label','Recentrer sur la trace');x.innerHTML='⤢';L.DomEvent.disableClickPropagation(w);L.DomEvent.on(x,'click',ev=>{L.DomEvent.preventDefault(ev);if(GPM)GPM.fitBounds(bd)});return w}});
      new Fit().addTo(GPM);
      setTimeout(()=>{if(GPM)GPM.invalidateSize()},300)}catch(e){el.innerHTML='<div class="empty">Carte indisponible.</div>'}}}
// Distance, D+ et D− d'une course = ceux de son GPX importé (D+/D− mesurés sur le GPX complet ; à défaut, estimés d'après le profil).
function syncGpx(r){
  if(!r||!Array.isArray(r.prof)||r.prof.length<4)return false;
  const gk=r.prof[r.prof.length-1][0],gx=r.gx||{};let dp,dm;
  if(gx.dp!=null){dp=gx.dp;dm=gx.dm}
  else{let u=0,d=0,ref=r.prof[0][1];r.prof.forEach(q=>{const v=q[1];if(v-ref>=3){u+=v-ref;ref=v}else if(ref-v>=3){d+=ref-v;ref=v}});dp=Math.round(u);dm=Math.round(d)}
  const km=+gk.toFixed(2),ch=r.km!==km||r.dplus!==dp||(dm!=null&&r.dminus!==dm);
  r.km=km;r.dplus=dp;if(dm!=null)r.dminus=dm;return ch}
function downTrk(cum,pts,n=160){const tot=cum[cum.length-1];if(!(tot>0))return null;const out=[];let j=0;for(let k=0;k<=n;k++){const x=tot*k/n;while(j<cum.length-1&&cum[j]<x)j++;out.push([+pts[j].la.toFixed(5),+pts[j].lo.toFixed(5)])}return out}
function parseGPX(text,name){
  const doc=new DOMParser().parseFromString(text,'application/xml');if(doc.getElementsByTagName('parsererror').length)throw new Error('xml');
  const pts=[...doc.getElementsByTagName('trkpt')].map(p=>{const e=p.getElementsByTagName('ele')[0],t=p.getElementsByTagName('time')[0];return{la:+p.getAttribute('lat'),lo:+p.getAttribute('lon'),e:e?+e.textContent:NaN,t:t?Date.parse(t.textContent):NaN}}).filter(p=>isFinite(p.la)&&isFinite(p.lo));
  if(pts.length<2)throw new Error('empty');const rad=Math.PI/180;let d=0;const cum=[0];
  for(let i=1;i<pts.length;i++){const x=(pts[i].lo-pts[i-1].lo)*rad*Math.cos((pts[i].la+pts[i-1].la)/2*rad),y=(pts[i].la-pts[i-1].la)*rad;d+=Math.sqrt(x*x+y*y)*6371;cum.push(d)}
  const el=pts.map(p=>p.e),sm=el.map((v,i)=>{let s=0,c=0;for(let j=Math.max(0,i-2);j<=Math.min(el.length-1,i+2);j++)if(isFinite(el[j])){s+=el[j];c++}return c?s/c:NaN});
  let up=0,dn=0,ref=sm.find(isFinite);sm.forEach(v=>{if(!isFinite(v))return;if(v-ref>=3){up+=v-ref;ref=v}else if(ref-v>=3){dn+=ref-v;ref=v}});
  const t0=pts.find(p=>isFinite(p.t)),t1=[...pts].reverse().find(p=>isFinite(p.t)),nm=doc.getElementsByTagName('name')[0];
  return{km:d,q:Math.max(1,Math.round(d*1000/pts.length)),dplus:Math.round(up),dminus:Math.round(dn),min:t0&&t1?(t1.t-t0.t)/60000:0,date:t0?iso(new Date(t0.t)):today(),prof:downProf(cum,sm),trk:downTrk(cum,pts),name:(nm?nm.textContent.trim():'')||name.replace(/\.gpx$/i,'')}}
function hms(m){const s=Math.round(m*60);return `${Math.floor(s/3600)}h${pad(Math.floor(s%3600/60))}'${pad(s%60)}`}

/* ============================ SAUVEGARDE ============================ */
function exportBak(){LS.set('vertex_lastexport',today());LS.set('vertex_snooze','');setTimeout(()=>{if(S.tab==='home'||S.tab==='profile')render()},900);const b=new Blob([JSON.stringify(backupPayload(),null,2)],{type:'application/json'}),a=document.createElement('a');a.href=URL.createObjectURL(b);a.download=`vertex-sauvegarde-${today()}.json`;document.body.appendChild(a);a.click();a.remove();setTimeout(()=>URL.revokeObjectURL(a.href),800)}
function importBak(file){const rd=new FileReader();rd.onload=e=>{try{const p=JSON.parse(e.target.result);
  if(p.app==='vertex'&&p.data&&p.data.races){if(!confirm('Remplacer les données actuelles par cette sauvegarde ?'))return;D=normalizeDoc(p.data);save();toast('Sauvegarde restaurée.');render();return}
  if(p.app==='trail-prep'&&p.data){let n=0;const d=p.data,J=k=>{try{return JSON.parse(d[k])}catch(x){return null}};
    (J('tp_races_custom')||[]).forEach(c=>{if(!D.races.some(r=>r.name===c.name&&r.date===c.date)){D.races.push({id:uid(),name:c.name,date:c.date,km:c.distance,dplus:c.dplus,dminus:null,goal:(c.goalLabel||'').replace('Objectif ',''),status:'À confirmer',result:'',rank:'',notes:c.info||''});n++}});
    [['wild72','wild72'],['roses','roses']].forEach(([old,id])=>{const b=J('tp_bilan_'+old),r=D.races.find(x=>x.id===id);if(b&&r){if(b.time&&!r.result){r.result=b.time;n++}if(b.rank&&!r.rank)r.rank=b.rank;if(b.status&&/Finisher/.test(b.status))r.status='Finisher'}});
    const pr=J('tp_profile');if(pr){if(pr.weight)D.profile.weight=pr.weight;if(pr.hrRest)D.profile.hrRest=pr.hrRest;if(pr.hrMax)D.profile.hrMax=pr.hrMax}
    save();toast(`Import Trail Prep : ${n} élément(s) repris.`);render();return}
  throw 0}catch(x){toast('Fichier non reconnu.',1)}};rd.readAsText(file)}

/* ============================ RENDU & ÉVÉNEMENTS ============================ */
const TABS=[['home','Accueil','🏔️'],['profile','Profil','👤'],['races','Courses','🏁'],['train','Entraînement','🏃'],['nutri','Nutrition','🍌']];
const VIEWS={home:renderHome,profile:renderProfile,races:renderRaces,train:renderTrain,nutri:renderNutri};
function render(){if(!BOOTED)return;const th=getTheme(),TI={auto:['🌓','Auto'],light:['☀️','Clair'],dark:['🌙','Sombre']}[th];$('#nav').innerHTML=TABS.map(([k,l,i])=>`<button class="${S.tab===k?'on':''}" data-a="tab" data-t="${k}" ${S.tab===k?'aria-current="page"':''}><i aria-hidden="true">${i}</i><span>${l}</span></button>`).join('');
  const y=window.scrollY;$('#main').innerHTML=VIEWS[S.tab]();if(S.tab==='home')homeFx();else homeFxStop();if(S.tab==='races')mountMap();if(S.keep){window.scrollTo(0,y);S.keep=false}}
function go(t){S.tab=t;closeModal();render();window.scrollTo(0,0)}
const A={
 cwView:el=>{S.cwView=S.cwView||{};S.cwView[sk(el.dataset.k)]=el.dataset.v;coachRefresh(el.dataset.k,null,false)},cwMonth:el=>{const k=el.dataset.k,K=sk(k),pl0=aiPlan(k),rc=selRace();if(!pl0||!rc)return;const pl={days:k==='nutri'?pl0.days.filter(d=>d.date>=addD(rc.date,-7)&&d.date<=rc.date):pl0.days};S.cwMon=S.cwMon||{};const cur=S.cwMon[K]||(S.cwSel&&S.cwSel[K]||today()).slice(0,7),[Y,M]=cur.split('-').map(Number),d=new Date(Y,M-1+ +el.dataset.s,1),m=`${d.getFullYear()}-${pad(d.getMonth()+1)}`,f=pl.days.find(x=>x.date.slice(0,7)===m);if(!f)return;S.cwMon[K]=m;S.cwSel=S.cwSel||{};S.cwSel[K]=(f.date<=today()&&pl.days.filter(x=>x.date.slice(0,7)===m).some(x=>x.date===today())?today():f.date);coachRefresh(k,null,false)},
 cwDay:el=>{S.cwSel=S.cwSel||{};S.cwSel[sk(el.dataset.k)]=el.dataset.d;coachRefresh(el.dataset.k,null,false);const b=document.querySelector('.cw-c.sel, .cm-d.sel');if(b)b.focus()},cwAll:el=>{$$('#cwk-'+el.dataset.k+' details.meal, #cwk-'+el.dataset.k+' details.trb').forEach(d=>{d.open=el.dataset.o==='1'})},cwWeek:el=>{const k=el.dataset.k,K=sk(k),pl=aiPlan(k);if(!pl)return;const b=$('#cwk-'+k+' .cw-c.sel'),m=addD(monday(b?b.dataset.d:today()),7*+el.dataset.s),inW=pl.days.filter(d=>monday(d.date)===m);if(!inW.length)return;S.cwSel=S.cwSel||{};S.cwSel[K]=(inW.find(d=>d.date===today())||inW[0]).date;coachRefresh(k,null,false)},
 pkOpen:el=>pkOpen(el.dataset.f),pkNav:el=>pkNav(el.dataset.f,+el.dataset.s),pkDay:el=>pkPick(el.dataset.f,el.dataset.v),pkClr:el=>pkPick(el.dataset.f,''),
 pkStep:el=>pkSet(el.dataset.f,st=>{st.step=el.dataset.s}),pkHour:el=>pkSet(el.dataset.f,st=>{st.h=+el.dataset.h;st.step='m'}),pkMin:el=>pkMinute(el.dataset.f,+el.dataset.m),pkAp:el=>pkSet(el.dataset.f,st=>{st.ap=el.dataset.p},true),
 theme:()=>cycleTheme(),foodAdd:()=>{foodsList().push({id:uid(),name:'Nouvel aliment',carbs:20,kind:'food'});syncAll();if(S.tab==='profile')render()},foodDel:el=>{D.profile.foods=foodsList().filter(f=>f.id!==el.dataset.id);syncAll();if(S.tab==='profile')render()},foodReset:()=>{if(confirm('Remettre la liste d\'aliments d\'origine ?')){D.profile.foods=JSON.parse(JSON.stringify(DEFAULT_FOODS));syncAll();if(S.tab==='profile')render()}},
 rcMonth:el=>{const s=+el.dataset.s;let m=s===0?today().slice(0,7):rcMonthKey();if(s){let [y,mo]=m.split('-').map(Number);mo+=s;if(mo<1){mo=12;y--}if(mo>12){mo=1;y++}m=`${y}-${pad(mo)}`}S.rcMon=m;refreshRaceCal(s)},tab:el=>go(el.dataset.t),filtClr:()=>{S.filt={q:'',kmMin:'',kmMax:'',dpMin:'',dpMax:'',from:'',to:'',y:'all'};render()},aiSave:el=>aiSave(el.dataset.k),aiClear:el=>aiClear(el.dataset.k),apvV:el=>{apvS(el.dataset.k).v=el.dataset.v;apvRefresh(el.dataset.k)},apvDay:el=>{const k=el.dataset.k,x=apvS(k);x.d=el.dataset.d;x.v='day';x.m='';apvRefresh(k)},apvToday:el=>{const k=el.dataset.k,x=apvS(k);x.d=today();x.m='';apvRefresh(k)},apvNav:el=>{const k=el.dataset.k,x=apvS(k),n=+el.dataset.s;if(x.v==='day')x.d=addD(x.d,n);else if(x.v==='week')x.d=addD(x.d,7*n);else{const [Y,M]=(x.m||x.d.slice(0,7)).split('-').map(Number),d=new Date(Y,M-1+n,1);x.m=`${d.getFullYear()}-${pad(d.getMonth()+1)}`}apvRefresh(k)},close:()=>closeModal(),ring:el=>openMetric(el.dataset.k),race:el=>openRace(el.dataset.id),
 newRace:()=>newRace(),saveRace:el=>saveRace(el.dataset.id),
 delRace:el=>{if(confirm('Supprimer cette course ?')){D.races=D.races.filter(r=>r.id!==el.dataset.id);if(S.sel===el.dataset.id)S.sel=null;save();closeModal();toast('Course supprimée.');render()}},
 plan:el=>{S.sel=el.dataset.id;go(el.dataset.t)},saveProfile:()=>saveProfile(),goProfile:()=>go('profile'),
 bilan:el=>openBilan(el.dataset.k),saveBilan:el=>saveBilan(el.dataset.k),planReset:el=>{if(confirm('Régénérer le plan depuis aujourd\'hui ? Les bilans déjà saisis des semaines passées ne seront plus appliqués.')){delete D.plans[el.dataset.id];save();S.keep=false;toast('Plan régénéré.');render()}},
 export:()=>exportBak(),snoozeBackup:()=>{LS.set('vertex_snooze',addD(today(),7));render()},seasonOpen:el=>openSeason(el.dataset.y),tests:()=>openSelfTests(),import:()=>$('#fBak').click(),reset:()=>{if(confirm('Tout réinitialiser (courses, profil, retours) ?')){D=normalizeDoc(null);save();toast('Données réinitialisées.');render()}},

 gpxSync:el=>{const r=D.races.find(q=>q.id===el.dataset.id);if(!r)return;syncGpx(r);save();toast(`Course recalculée d'après le GPX : ${fn(r.km)} km · +${fn(r.dplus,0)} m · −${fn(r.dminus,0)} m.`);render();openRace(r.id)},gpxSyncAll:()=>{let n=0,t=0;D.races.forEach(r=>{if(Array.isArray(r.prof)&&r.prof.length>3){t++;if(syncGpx(r))n++}});save();toast(t?`${t} course(s) avec GPX : ${n} mise(s) à jour (km, D+, D−).`:'Aucune course n\'a de GPX importé.',!t);render()},
 gpxFor:el=>{S.gpxFor=el.dataset.id;$('#fGpx').click()},profDel:el=>{const r=D.races.find(q=>q.id===el.dataset.id);if(r&&confirm('Retirer le profil d\'altitude de cette course ?')){delete r.prof;delete r.gx;delete r.trk;save();openRace(r.id)}},
 seg:el=>segPick(el),segClose:()=>segClose(),classics:()=>openClassics(),abChoose:()=>abChoose(),abReconnect:()=>abReconnect(),abStop:()=>abStop(),install:async()=>{if(!INSTALL)return;INSTALL.prompt();try{await INSTALL.userChoice}catch(e){}INSTALL=null;refreshAB();const el=$('#pwa');if(el)el.innerHTML=pwaStatus()},seasonPlan:()=>openSeasonPlan(),spYear:el=>openSeasonPlan(el.dataset.y),reliab:()=>openReliab(),utmb:()=>openUtmb(),utmbAdd:()=>utmbAddFromForm(),utmbGoal:()=>utmbGoalFromForm(),utmbDel:el=>utmbDelete(el.dataset.d),
 utmbPick:el=>{const h=$('#r-utmbcat');if(!h)return;const v=el.dataset.v,same=h.value===v;h.value=same?'':v;$$('.ucat').forEach(b=>{const on=!same&&b.dataset.v===v;b.classList.toggle('on',on);b.setAttribute('aria-checked',on)})},
 fiche:el=>openFiche(el.dataset.id),rankSave:el=>{const k=el.dataset.k,r=D.races.find(x=>x.id===el.dataset.id),v=(($('#lk-'+k)||{}).value||'').trim();if(!r)return;if(!/^https?:\/\/\S+$/i.test(v))return toast('Le lien doit commencer par https://',1);r[k+'Url']=v;save();toast(`Lien validé : bouton « ${k==='bib'?'Dossard':'Classement'} » ajouté en haut de la course.`);render();openRace(r.id)},rankDel:el=>{const r=D.races.find(x=>x.id===el.dataset.id);if(!r)return;delete r[el.dataset.k+'Url'];save();render();openRace(r.id)},printFiche:()=>printFiche(),wake:()=>toggleWake(),
};
document.addEventListener('click',e=>{if(e.target.classList&&e.target.id==='modal'){closeModal();return}const el=e.target.closest('[data-a]');if(el&&A[el.dataset.a])A[el.dataset.a](el)});
document.addEventListener('change',e=>{if(e.target.dataset&&e.target.dataset.c==='food'){const f=foodsList().find(x=>x.id===e.target.dataset.id);if(f){const k=e.target.dataset.f;f[k]=k==='carbs'?(parseFloat(e.target.value)||0):e.target.value;syncAll()}return}
  if(e.target.dataset&&e.target.dataset.c==='nset'){D.profile[e.target.dataset.k]=e.target.value===''?'':Math.max(0,+e.target.value||0);syncAll();return}
  if(/^p-nutri(Water|Iso|Carbs)$/.test(e.target.id||'')){D.profile[e.target.id.slice(2)]=e.target.value===''?'':Math.max(0,+e.target.value||0);syncAll();return}
  if(e.target.dataset&&e.target.dataset.c==='feel'){D.profile.feel=+e.target.value;save();refreshGoals();render();return}
  if(e.target.dataset&&e.target.dataset.c==='filt'){S.filt=S.filt||{};S.filt[e.target.dataset.k]=e.target.value;setTimeout(render,0);return}
  if(e.target.dataset&&e.target.dataset.c==='done'){const k=e.target.dataset.k;if(e.target.checked)D.done[k]=1;else delete D.done[k];save();const tr=e.target.closest('tr,.sc');if(tr)tr.classList.toggle('dn',e.target.checked);return}
  if(e.target.dataset&&e.target.dataset.c==='ndone'){const k=e.target.dataset.k;if(e.target.checked)D.done[k]=1;else delete D.done[k];save();const m=e.target.closest('.mealw');if(m)m.classList.toggle('dn',e.target.checked);const dy=e.target.closest('.nday');if(dy){const c=dy.querySelectorAll('input[data-c=ndone]'),f=[...c].filter(x=>x.checked).length,b=dy.querySelector('.ncount');if(b)b.textContent=(f===c.length?'✅ ':'')+f+'/'+c.length;dy.classList.toggle('fin',f===c.length)}return}
  if(e.target.dataset&&e.target.dataset.c==='prio'){const r=D.races.find(x=>x.id===e.target.dataset.id);if(r){r.prio=e.target.value;save();render();openSeasonPlan(S.spY)}return}
  if(e.target.dataset&&e.target.dataset.c==='apvdone'){const k=e.target.dataset.k;D.ai=D.ai||{};D.ai.done=D.ai.done||{};const K=sk(k),o=D.ai.done[K]=D.ai.done[K]||{};if(e.target.checked)o[e.target.dataset.id]=1;else delete o[e.target.dataset.id];save();const _id=e.target.dataset.id,_on=e.target.checked,_was=!!$('#cwk-'+k+' .wkg.full');apvRefresh(k);coachRefresh(k,_id);if(_on)burstFor(k,_id);if(_on&&!_was){const g=$('#cwk-'+k+' .wkg.full .wkg-run');if(g){setTimeout(()=>burstAt(g),150);setTimeout(()=>burstAt(g),450)}}return}
  if(e.target.dataset&&e.target.dataset.c==='apvstart'){const k=e.target.dataset.k;D.ai=D.ai||{};D.ai.start=D.ai.start||{};D.ai.start[sk(k)]=/^\d{4}-\d{2}-\d{2}$/.test(e.target.value)?e.target.value:'';save();S.apv&&delete S.apv[k];S.keep=true;render();return}
  if(e.target.dataset&&e.target.dataset.c==='sel'){S.sel=e.target.value;render()}});
document.addEventListener('toggle',e=>{const t=e.target;if(t&&t.id==='mapfold'&&t.open&&MAP)setTimeout(()=>{try{MAP.invalidateSize()}catch(x){}},60)},true);
document.addEventListener('keydown',e=>{if(e.key==='Escape'&&!$('#modal').classList.contains('hide'))closeModal();
  if((e.key==='Enter'||e.key===' ')&&e.target.matches&&e.target.matches('g[data-a],circle.seg')){e.preventDefault();const el=e.target;if(A[el.dataset.a])A[el.dataset.a](el)}});
$('#fGpx').addEventListener('change',e=>{const f=e.target.files[0];e.target.value='';const tg=S.gpxFor;S.gpxFor=null;if(!f)return;const rd=new FileReader();
  rd.onload=x=>{try{const g=parseGPX(x.target.result,f.name);
    if(tg){const r=D.races.find(q=>q.id===tg);if(!r)return;if(!g.prof)return toast("Ce GPX n'a pas d'altitude : profil impossible.",1);
      r.prof=g.prof;r.gx={dp:g.dplus,dm:g.dminus,q:g.q};if(g.trk)r.trk=g.trk;else delete r.trk;syncGpx(r);save();toast(`GPX importé : la course passe à ${fn(r.km)} km · +${fn(r.dplus,0)} m · −${fn(r.dminus,0)} m (mesurés sur le GPX).`);render();openRace(tg);return}
    S.pendProf=g.prof||null;S.pendTrk=g.prof&&g.trk?g.trk:null;newRace({name:g.name,date:g.date,km:+g.km.toFixed(2),dplus:g.dplus,dminus:g.dminus,result:g.min?hms(g.min):'',status:'Finisher'});toast(`GPX lu : ${fn(g.km)} km · +${g.dplus} m · −${g.dminus} m${g.prof?' · profil conservé':''}`)}
  catch(err){toast('GPX illisible (points GPS requis).',1)}};
  rd.readAsText(f)});
$('#fBak').addEventListener('change',e=>{const f=e.target.files[0];e.target.value='';if(f)importBak(f)});


(function(){
  const tip=()=>document.getElementById('segtip'),seg=e=>e.target&&e.target.closest?e.target.closest('circle.seg'):null;
  const show=e=>{const c=seg(e),t=tip();if(!t)return;if(!c){t.classList.add('hide');return}
    t.style.setProperty('--tc',c.dataset.col||'var(--acc)');
    t.innerHTML=`<b>${esc(c.dataset.n)}</b><span class="mut">${esc(c.dataset.m)}</span><strong>${esc(c.dataset.vt)}</strong>`;t.classList.remove('hide');
    const w=t.offsetWidth,h=t.offsetHeight;let x=e.clientX+16,y=e.clientY-h-14;if(x+w>window.innerWidth-8)x=e.clientX-w-16;if(y<8)y=e.clientY+20;t.style.left=Math.max(8,x)+'px';t.style.top=y+'px'};
  document.addEventListener('mouseover',show);document.addEventListener('mousemove',e=>{if(seg(e))show(e)});
  document.addEventListener('mouseout',e=>{if(seg(e)){const t=tip();if(t)t.classList.add('hide')}});
  document.addEventListener('scroll',()=>{const t=tip();if(t)t.classList.add('hide')},{passive:true});
})();
boot();
if(location.hash==='#tests')setTimeout(openSelfTests,0);
</script>
</body>
</html># Vertex.github.io
