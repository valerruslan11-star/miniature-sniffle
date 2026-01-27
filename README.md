<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <meta name="theme-color" content="#ffffff" />
  <title>iPay.ua — Demo</title>

  <!-- ASSISTANT PATCH: single-file demo UI based on provided iPay.ua screenshots; NO real payments -->
  <style>
    :root{
      --bg:#f3f6fb;
      --card:#ffffff;
      --text:#0d1220;
      --muted:#5a6a7f;
      --line:#e4ebf4;
      --line2:#d7e1ee;
      --brand:#ff5a3c;
      --brand2:#ff7a52;
      --info:#d8ecff;
      --infoText:#2a5c8a;
      --btn:#dfe7f2;
      --btnText:#7b8aa2;
      --shadow: 0 14px 30px rgba(9,23,45,.08);
      --shadow2: 0 10px 22px rgba(9,23,45,.10);
      --radius:18px;
      --radius2:22px;
      --safeTop: env(safe-area-inset-top, 0px);
      --safeBottom: env(safe-area-inset-bottom, 0px);
    }

    *{ box-sizing:border-box; }
    html,body{ height:100%; }
    body{
      margin:0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Liberation Sans", sans-serif;
      background: var(--bg);
      color:var(--text);
      overflow-x:hidden;
    }

    /* Top promo banner (PSM Awards) */
    .topPromo{
      padding: calc(8px + var(--safeTop)) 12px 10px;
      background: linear-gradient(90deg, #1c1b4b, #2a2662);
      color:#fff;
    }
    .topPromoInner{
      max-width: 920px;
      margin:0 auto;
      display:flex;
      gap:12px;
      align-items:center;
      justify-content:space-between;
    }
    .promoText{
      min-width:0;
    }
    .promoTitle{
      font-weight:800;
      letter-spacing:.2px;
      font-size:12px;
      opacity:.9;
      margin:0 0 4px;
    }
    .promoMain{
      margin:0;
      font-weight:800;
      font-size:14px;
      line-height:1.2;
    }
    .promoBtn{
      border:0;
      background: linear-gradient(180deg, var(--brand2), var(--brand));
      color:#fff;
      font-weight:800;
      border-radius:12px;
      padding:10px 12px;
      cursor:pointer;
      box-shadow: 0 10px 18px rgba(0,0,0,.18);
      white-space:nowrap;
    }
    .promoBtn:active{ transform: translateY(1px); }

    /* Header */
    .header{
      background:#fff;
      border-bottom:1px solid var(--line);
      position: sticky;
      top:0;
      z-index:10;
    }
    .headerInner{
      max-width: 920px;
      margin:0 auto;
      padding:10px 12px;
      display:flex;
      align-items:center;
      gap:10px;
    }
    .logo{
      display:flex;
      align-items:center;
      gap:8px;
      font-weight:950;
      letter-spacing:.2px;
      font-size:22px;
      color:#2a2f3d;
    }
    .logo .dot{
      color: var(--brand);
      margin-left:2px;
    }
    .searchIcon{
      width:22px; height:22px;
      opacity:.55;
      cursor:pointer;
      border-radius:10px;
      padding:6px;
    }
    .searchIcon:active{ background: rgba(0,0,0,.04); }
    .spacer{ flex:1; }
    .loginBtn{
      border:0;
      background: linear-gradient(180deg, #ff6a4f, #ff4c35);
      color:#fff;
      font-weight:900;
      border-radius:12px;
      padding:10px 12px;
      cursor:pointer;
      display:flex;
      align-items:center;
      gap:8px;
      box-shadow: 0 10px 18px rgba(255,76,53,.22);
    }
    .loginBtn:active{ transform: translateY(1px); }
    .burger{
      border:0;
      background: transparent;
      padding:10px 10px;
      cursor:pointer;
      border-radius:12px;
    }
    .burger:active{ background: rgba(0,0,0,.04); }
    .burgerLines{
      width:22px; height:18px;
      display:grid;
      gap:4px;
    }
    .burgerLines span{
      height:2px;
      background: #2d3446;
      border-radius:999px;
      opacity:.85;
    }

    /* Language/info bar */
    .infoBar{
      background: #cfe8ff;
      color: var(--infoText);
      font-weight:700;
      padding:10px 12px;
      border-bottom: 1px solid rgba(42,92,138,.12);
    }
    .infoBarInner{
      max-width: 920px;
      margin:0 auto;
      display:flex;
      align-items:center;
      gap:10px;
      justify-content:center;
      text-align:center;
    }
    .infoBar a{
      color: #1f4f7a;
      text-decoration: underline;
      font-weight:900;
    }

    /* Main page */
    .wrap{
      max-width: 920px;
      margin:0 auto;
      padding: 14px 12px calc(36px + var(--safeBottom));
    }
    .crumbs{
      display:flex;
      align-items:center;
      gap:10px;
      color: #96a5bb;
      font-weight:700;
      margin: 6px 0 10px;
    }
    .crumbs .back{
      width:34px; height:34px;
      border-radius:12px;
      border:1px solid var(--line);
      background:#fff;
      cursor:pointer;
      display:grid;
      place-items:center;
      box-shadow: 0 8px 18px rgba(9,23,45,.06);
    }
    .crumbs .back:active{ transform: translateY(1px); }

    h1{
      margin: 10px 0 6px;
      font-size: 28px;
      letter-spacing:.1px;
    }
    .subtitle{
      margin:0 0 14px;
      color: var(--muted);
      font-weight:650;
      line-height:1.35;
    }

    .sectionTitle{
      margin: 16px 0 10px;
      font-size: 16px;
      font-weight:900;
      letter-spacing:.1px;
    }

    /* Method tabs */
    .tabs{
      display:grid;
      grid-template-columns: repeat(3, minmax(0,1fr));
      gap:10px;
      margin: 10px 0 12px;
    }
    .tab{
      background:#fff;
      border:1px solid var(--line2);
      border-radius: 14px;
      padding:10px 10px;
      display:flex;
      align-items:center;
      justify-content:center;
      gap:10px;
      cursor:pointer;
      box-shadow: 0 10px 22px rgba(9,23,45,.06);
      font-weight:850;
      color:#334059;
      min-height: 56px;
      user-select:none;
      -webkit-tap-highlight-color: transparent;
    }
    .tab[aria-selected="true"]{
      background:#1f3548;
      border-color:#1f3548;
      color:#fff;
      box-shadow: 0 14px 26px rgba(31,53,72,.18);
    }
    .tabIcon{
      width:20px; height:20px;
      display:block;
      opacity:.95;
    }
    .tab[aria-selected="true"] .tabIcon{ filter: brightness(6); opacity:1; }

    /* Cards */
    .card{
      background: var(--card);
      border: 1px solid var(--line);
      border-radius: var(--radius2);
      box-shadow: var(--shadow);
      padding: 14px;
      margin: 12px 0;
    }
    .card h3{
      margin:0 0 10px;
      font-size: 18px;
      font-weight:950;
      letter-spacing:.1px;
    }
    .grid2{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap:10px;
    }
    .field{
      display:flex;
      flex-direction:column;
      gap:8px;
      margin: 10px 0;
    }
    .input{
      width:100%;
      border: 2px solid var(--line2);
      border-radius: 14px;
      padding: 14px 14px;
      font-size: 16px;
      outline:none;
      transition: border-color .12s ease, box-shadow .12s ease;
      background:#fff;
    }
    .input:focus{
      border-color: rgba(42,92,138,.35);
      box-shadow: 0 0 0 4px rgba(42,92,138,.10);
    }
    .input::placeholder{
      color:#9aa8bd;
      font-weight:650;
    }
    .suffixRow{
      display:flex;
      gap:10px;
    }

    .selectWrap{
      position:relative;
    }
    select.input{
      appearance:none;
      padding-right: 38px;
    }
    .chev{
      position:absolute;
      right:14px; top:50%;
      transform: translateY(-50%);
      opacity:.45;
      pointer-events:none;
    }

    .sumRow{
      display:grid;
      grid-template-columns: 1fr auto;
      align-items:center;
      gap:12px;
    }
    .commission{
      text-align:left;
      color: var(--text);
      font-weight:900;
      line-height:1.2;
      white-space:nowrap;
    }
    .commission small{
      display:block;
      color: var(--muted);
      font-weight:800;
    }

    .checkboxRow{
      display:flex;
      gap:10px;
      align-items:center;
      color: var(--muted);
      font-weight:750;
      margin: 8px 0 6px;
    }
    .checkboxRow input{
      width:20px; height:20px;
      accent-color: #2a5c8a;
    }

    .payRow{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:12px;
      margin: 8px 0 6px;
    }
    .payRow .toPay{
      color: var(--text);
      font-weight:900;
    }
    .payRow .amount{
      font-size: 26px;
      font-weight:950;
      letter-spacing:.2px;
    }
    .payBtn{
      width:100%;
      border:0;
      background: #dfe7f2;
      color:#7b8aa2;
      font-weight:950;
      padding:16px 14px;
      border-radius: 14px;
      cursor:not-allowed;
      box-shadow: 0 12px 22px rgba(9,23,45,.06);
      font-size: 16px;
    }
    .payBtn.enabled{
      background: linear-gradient(180deg, #4e8dff, #2f6bff);
      color:#fff;
      cursor:pointer;
      box-shadow: 0 14px 26px rgba(47,107,255,.22);
    }
    .payBtn.enabled:active{ transform: translateY(1px); }

    .legal{
      margin: 10px 0 0;
      color: #9aa8bd;
      font-weight:650;
      font-size: 12.5px;
      line-height:1.35;
      text-align:center;
    }
    .legal a{ color:#d05a5a; text-decoration: underline; font-weight:900; }

    .logosRow{
      display:flex;
      gap:16px;
      align-items:center;
      justify-content:flex-start;
      padding: 10px 0 0;
      flex-wrap:wrap;
    }
    .logoChip{
      display:flex;
      align-items:center;
      gap:10px;
      color:#3b4b63;
      font-weight:950;
    }
    .logoChip svg{ width:64px; height:24px; }

    /* Limits */
    .limitsTitle{
      margin: 0 0 10px;
      font-size: 22px;
      font-weight:950;
    }
    .limitItem{
      padding: 10px 0;
      border-top: 1px solid var(--line);
    }
    .limitItem:first-child{ border-top:0; }
    .limitItem .val{
      font-weight:950;
      font-size: 22px;
      margin:0 0 4px;
    }
    .limitItem .desc{
      margin:0;
      color: var(--muted);
      font-weight:650;
      line-height:1.35;
    }

    /* Rating block */
    .ratingWrap{
      background: #1f3548;
      border-radius: var(--radius2);
      padding: 16px;
      color:#fff;
      box-shadow: 0 18px 30px rgba(31,53,72,.18);
      margin: 14px 0;
    }
    .ratingTitle{
      margin:0 0 10px;
      font-weight:950;
      text-align:center;
      opacity:.95;
    }
    .stars{
      display:flex;
      gap:6px;
      justify-content:center;
      margin: 6px 0 10px;
    }
    .stars svg{ width:24px; height:24px; }
    .ratingMeta{
      text-align:center;
      opacity:.92;
      font-weight:850;
    }
    .ratingCard{
      background:#fff;
      border-radius: 16px;
      color: var(--text);
      padding: 14px;
      margin-top: 12px;
      box-shadow: 0 14px 26px rgba(0,0,0,.18);
      text-align:center;
      font-weight:900;
    }
    .ratingCard .big{
      font-size: 30px;
      letter-spacing:.2px;
      margin: 4px 0;
    }
    .ratingCard small{
      color: var(--muted);
      font-weight:800;
    }

    /* Content blocks (info sections) */
    .content{
      background:#fff;
      border:1px solid var(--line);
      border-radius: var(--radius2);
      box-shadow: var(--shadow);
      padding: 14px;
      margin: 12px 0;
    }
    .content h2{
      margin: 0 0 10px;
      font-size: 22px;
      font-weight:950;
      line-height:1.2;
    }
    .content p{
      margin: 10px 0;
      color: var(--muted);
      font-weight:650;
      line-height:1.55;
    }
    .quote{
      margin: 12px 0;
      padding: 10px 12px;
      border-left: 4px solid #ef6a5b;
      background: #fbfbfe;
      color: #6b7b92;
      border-radius: 12px;
      font-weight:700;
    }
    .stats{
      display:grid;
      grid-template-columns: 1fr;
      gap:10px;
      margin-top: 12px;
    }
    .stat{
      border:1px solid var(--line);
      border-radius: 16px;
      padding: 14px;
      background:#fff;
      box-shadow: 0 10px 20px rgba(9,23,45,.06);
      text-align:center;
      font-weight:950;
    }
    .stat .n{
      color:#ef6a5b;
      font-size: 26px;
      margin: 0 0 6px;
    }
    .stat .t{
      margin:0;
      color: var(--muted);
      font-weight:700;
    }

    /* Drawer */
    .drawerBack{
      position:fixed;
      inset:0;
      background: rgba(0,0,0,.35);
      display:none;
      z-index: 30;
    }
    .drawerBack.open{ display:block; }
    .drawer{
      position:fixed;
      top:0; right:0;
      height:100%;
      width: min(340px, 90vw);
      background:#fff;
      box-shadow: -18px 0 40px rgba(0,0,0,.18);
      transform: translateX(102%);
      transition: transform .18s ease;
      z-index: 31;
      display:flex;
      flex-direction:column;
    }
    .drawer.open{ transform: translateX(0); }
    .drawerHead{
      padding: calc(14px + var(--safeTop)) 14px 12px;
      border-bottom: 1px solid var(--line);
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:10px;
    }
    .drawerHead b{ font-weight:950; }
    .drawerClose{
      border:1px solid var(--line);
      background:#fff;
      border-radius: 12px;
      padding:10px 12px;
      cursor:pointer;
      font-weight:900;
    }
    .drawerClose:active{ transform: translateY(1px); }
    .drawerBody{
      padding: 12px 14px;
      overflow:auto;
    }
    .drawerItem{
      padding: 12px 10px;
      border-radius: 14px;
      border:1px solid var(--line);
      background:#fff;
      box-shadow: 0 10px 20px rgba(9,23,45,.06);
      margin: 10px 0;
      cursor:pointer;
      font-weight:900;
      color:#2d3a52;
      user-select:none;
      -webkit-tap-highlight-color: transparent;
    }
    .drawerItem:active{ transform: translateY(1px); }

    /* Modal (login) */
    .modalBack{
      position:fixed;
      inset:0;
      background: rgba(0,0,0,.35);
      display:none;
      z-index: 40;
      padding: 14px 12px;
      align-items:flex-end;
      justify-content:center;
    }
    .modalBack.open{ display:flex; }
    .modal{
      width: min(520px, 100%);
      background:#fff;
      border-radius: 22px;
      box-shadow: 0 22px 55px rgba(0,0,0,.18);
      border: 1px solid var(--line);
      overflow:hidden;
    }
    .modalHead{
      padding: 12px 14px;
      border-bottom: 1px solid var(--line);
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:10px;
    }
    .modalHead b{ font-weight:950; }
    .modalClose{
      border:1px solid var(--line);
      background:#fff;
      border-radius: 12px;
      padding:10px 12px;
      cursor:pointer;
      font-weight:900;
    }
    .modalBody{
      padding: 14px;
    }
    .hint{
      background:#fbfbfe;
      border:1px solid var(--line);
      border-radius: 16px;
      padding: 12px;
      color: var(--muted);
      font-weight:650;
      line-height:1.5;
    }

    /* Mobile tweaks */
    @media (max-width: 520px){
      h1{ font-size: 26px; }
      .tabs{ grid-template-columns: 1fr; }
      .grid2{ grid-template-columns: 1fr 1fr; }
    }
    @media (max-width: 390px){
      .grid2{ grid-template-columns: 1fr; }
      .promoBtn{ display:none; }
    }
  
/* === ASSISTANT PATCH: page continuation sections (screens 12:57) === */
.section{ margin:22px 0; }
.section h2{ margin:0 0 10px; font-size:20px; letter-spacing:.1px; }
.section p{ margin:10px 0; color:var(--muted); line-height:1.45; }
.redBullets{ list-style:none; padding:0; margin:12px 0 0; }
.redBullets li{ position:relative; padding-left:18px; margin:10px 0; color:var(--muted); }
.redBullets li:before{
  content:"";
  position:absolute; left:0; top:.6em;
  width:8px; height:8px; border-radius:50%;
  background:var(--accent);
  transform:translateY(-50%);
}
.bankList{ margin:10px 0 0; padding-left:0; list-style:none; }
.bankList li{ position:relative; padding-left:18px; margin:10px 0; color:var(--muted); }
.bankList li:before{ content:""; position:absolute; left:0; top:.6em; width:8px; height:8px; border-radius:50%; background:var(--accent); transform:translateY(-50%); }
.numSteps{ margin:10px 0 0; padding-left:0; list-style:none; counter-reset: st; }
.numSteps li{ counter-increment: st; margin:12px 0; color:var(--muted); line-height:1.45; }
.numSteps li b{ color:var(--accent); margin-right:6px; font-weight:800; }
.numSteps li:before{ content: counter(st) "."; color:var(--accent); font-weight:800; display:inline-block; width:22px; }
.helpBlock{
  margin:18px 0 0;
  background:#0f2b3a;
  color:#d9e6ee;
  border-radius:18px;
  padding:18px;
  box-shadow:0 14px 38px rgba(15,43,58,.18);
}
.helpBlock h3{ margin:0 0 12px; font-size:18px; color:#ffffff; }
.helpItem{ display:flex; gap:12px; align-items:flex-start; padding:12px 0; border-top:1px solid rgba(255,255,255,.10); }
.helpItem:first-of-type{ border-top:0; padding-top:0; }
.helpIcon{
  width:34px; height:34px; border-radius:10px;
  background:rgba(255,255,255,.08);
  display:flex; align-items:center; justify-content:center;
  flex:0 0 34px;
}
.helpMain{ font-weight:700; color:#ffffff; }
.helpSub{ color:rgba(255,255,255,.75); font-size:13px; margin-top:2px; }
.footerWrap{
  background:#0f2b3a;
  color:#d9e6ee;
  padding:28px 0 20px;
  margin-top:18px;
}
.footerInner{ width:min(920px, 100%); margin:0 auto; padding:0 16px; }
.footerGrid{
  display:grid;
  grid-template-columns: 1fr;
  gap:22px;
}
.footerCol h4{ margin:0 0 12px; color:#ffffff; font-size:18px; }
.footerLinks{ list-style:none; padding:0; margin:0; }
.footerLinks li{ padding:10px 0; color:#d9e6ee; }
.footerLinks li span{ opacity:.9; }
.socialRow{ display:flex; gap:14px; align-items:center; }
.socialBtn{
  width:44px; height:44px; border-radius:14px;
  background:rgba(255,255,255,.08);
  display:flex; align-items:center; justify-content:center;
}
.payRow{ display:flex; gap:18px; flex-wrap:wrap; align-items:center; opacity:.9; margin-top:18px; }
.legalSmall{ margin-top:18px; color:rgba(255,255,255,.6); font-size:12px; line-height:1.4; }
@media (min-width: 860px){
  .footerGrid{ grid-template-columns: 1.2fr 1fr 1fr; }
}
/* === /ASSISTANT PATCH === */


    /* ASSISTANT PATCH: drawer menu like screenshot (13:14) */
    .drawer{ width: min(420px, 92vw); }
    .drawerBody{ padding: 0; }
    .drawerHead{ display:none; } /* keep in DOM, hide visually */
    .drawerBody::-webkit-scrollbar{ width: 8px; }
    .drawerBody::-webkit-scrollbar-thumb{ background: rgba(0,0,0,.12); border-radius: 999px; }

    .menuPanel{
      padding: 14px 14px calc(18px + var(--safeBottom));
      overflow:auto;
      height: 100%;
    }
    .menuTop{
      display:flex;
      align-items:center;
      justify-content:space-between;
      padding: calc(10px + var(--safeTop)) 4px 10px;
      margin: -14px -14px 10px;
      background:#fff;
      border-bottom: 1px solid var(--line);
      position: sticky;
      top: 0;
      z-index: 1;
    }
    .menuTop .logoMini{
      display:flex;
      align-items:baseline;
      gap:2px;
      font-weight:1000;
      letter-spacing:-.2px;
      font-size: 24px;
      color:#ff4c35;
      padding-left:10px;
    }
    .menuTop .logoMini .dot{ color:#7f93ad; font-weight:1000; }
    .menuX{
      border:0;
      background: transparent;
      width: 44px;
      height: 44px;
      border-radius: 14px;
      display:grid;
      place-items:center;
      cursor:pointer;
      margin-right: 6px;
    }
    .menuX:active{ background: rgba(0,0,0,.04); }
    .menuX svg{ width: 22px; height: 22px; color:#2d3446; }

    .menuCatalogBtn{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:12px;
      background: #18b07d;
      color:#fff;
      border-radius: 16px;
      padding: 14px 14px;
      font-weight: 1000;
      box-shadow: 0 16px 26px rgba(24,176,125,.18);
      border: 1px solid rgba(0,0,0,.05);
    }
    .menuCatalogBtn .left{
      display:flex;
      align-items:center;
      gap:10px;
    }
    .menuCatalogBtn .grid{
      width: 22px; height: 22px;
      display:grid;
      grid-template-columns: repeat(2, 1fr);
      gap:3px;
    }
    .menuCatalogBtn .grid span{
      background: rgba(255,255,255,.92);
      border-radius: 4px;
    }
    .menuCatalogBtn .chev{
 
