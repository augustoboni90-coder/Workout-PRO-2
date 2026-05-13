<!doctype html>
<html lang="it">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>Workout PRO</title>
<meta name="theme-color" content="#0b0f14">
<style>
:root{--bg:#070a0f;--text:#f4f7fb;--muted:#93a4b7;--cyan:#20d7ff;--yellow:#ffd54d;--shadow:0 14px 32px rgba(0,0,0,.36);--safe:env(safe-area-inset-bottom)}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
body{margin:0;background:linear-gradient(180deg,#0b0f14,#06080b);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"SF Pro Display","Segoe UI",Roboto,Arial,sans-serif}
.app{max-width:980px;margin:auto;padding:16px 14px calc(100px + var(--safe))}
.title{text-align:center;font-size:25px;font-weight:950}.sub{text-align:center;color:var(--muted);font-size:13px;margin:6px 0 14px}
.mainnav{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:0 0 16px}.mainnav button{border:0;border-radius:18px;padding:14px;background:#171d26;color:var(--muted);font-weight:950;box-shadow:var(--shadow);cursor:pointer}.mainnav button.active{background:linear-gradient(180deg,#2abfff,#1789ff);color:white}
.page{display:none}.page.active{display:block}
.box,.card,.timer,.coach,.history,.preview{background:radial-gradient(circle at top right,rgba(32,215,255,.06),transparent 32%),linear-gradient(180deg,#121821,#0e141c);border:1px solid #1d2734;border-radius:24px;box-shadow:var(--shadow)}
.box{padding:16px;margin-bottom:14px}h2{font-size:18px;margin:0 0 6px}.hint{color:var(--muted);font-size:13px;line-height:1.35}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px}.field{display:flex;flex-direction:column;gap:6px}.field label{font-size:12px;color:var(--muted);font-weight:900}
.field input,.field textarea,.file,.cell{width:100%;border:0;outline:0;border-radius:14px;background:#1a2029;border:1px solid #263445;color:#fff;font-size:15px;font-weight:800;padding:12px}.field textarea{min-height:70px;resize:vertical}.wide{grid-column:1/-1}
.fileRow{display:grid;grid-template-columns:1fr auto auto;gap:10px;margin-top:12px}.btn,.mini,.tab,.dayBtn,.doneBtn,.saveBtn{border:0;cursor:pointer}.btn{border-radius:16px;padding:14px 16px;background:linear-gradient(180deg,#2abfff,#1789ff);color:#fff;font-weight:950;font-size:15px;box-shadow:var(--shadow)}.btn.gray{background:linear-gradient(180deg,#263241,#1b2430)}.btn.red{background:linear-gradient(180deg,#ff4d5e,#b91f32)}
.btn:active,.mini:active,.tab:active,.dayBtn:active,.doneBtn:active,.saveBtn:active{transform:scale(.985);filter:brightness(1.07)}
.status{margin-top:10px;color:var(--muted);font-size:13px;line-height:1.35}.status.ok{color:#bfffd8}.status.err{color:#ffb8bf}
.tabs{display:flex;gap:10px;margin:16px 0}.tab{flex:1;border-radius:16px;padding:12px 8px;background:#171d26;color:var(--muted);font-weight:950}.tab.active{background:#232d3a;color:#fff;outline:1px solid #2d3948}
.days{display:flex;gap:10px;overflow:auto;padding:4px 0 12px;scrollbar-width:none}.days::-webkit-scrollbar{display:none}.dayBtn{flex:0 0 auto;min-width:112px;border-radius:18px;padding:14px;background:linear-gradient(180deg,#1b232e,#111822);color:#fff;box-shadow:var(--shadow);text-align:left;font-weight:900}.dayBtn small{display:block;color:var(--muted);margin-top:2px}.dayBtn.active{background:linear-gradient(180deg,#33e0ff,#12c3eb);color:#06151d}
.bar{height:8px;background:#151c25;border-radius:999px;overflow:hidden;margin-bottom:14px}.bar span{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--cyan),#62f2ff)}
.coach{padding:14px;margin-bottom:14px}.coachTop{display:flex;justify-content:space-between;gap:10px;margin-bottom:10px}.badge{border-radius:999px;padding:8px 12px;background:linear-gradient(180deg,#38e0ff,#17c2ea);color:#05131a;font-size:12px;font-weight:950}.bubble{min-height:62px;border-radius:18px;padding:14px 16px;background:#18222e;border:1px solid #26384a;display:flex;align-items:center;font-weight:850;color:#e9fbff}
.timer{padding:18px 16px;margin-bottom:16px}.timerBadge{display:none;width:max-content;margin:0 auto 10px;background:#ff7a17;border-radius:999px;padding:8px 14px;font-size:12px;font-weight:950}.timerBadge.show{display:block}.timerLabel{text-align:center;color:var(--muted);font-size:12px;font-weight:900}.time{text-align:center;font-size:64px;line-height:1;font-weight:950;color:var(--yellow);font-variant-numeric:tabular-nums;margin:6px 0 12px}.timerActions{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.stats{display:flex;justify-content:space-between;color:var(--muted);font-size:14px;margin:4px 2px 10px}.card{padding:16px;margin-bottom:14px;scroll-margin-top:20px}.exHead{display:flex;justify-content:space-between;gap:12px;margin-bottom:14px}.exName{font-size:20px;font-weight:950}.meta{color:var(--muted);font-size:13px}.pill{flex:0 0 auto;background:#0d7daf;border-radius:999px;padding:8px 12px;font-size:13px;font-weight:950;color:#e9fbff}.guide{display:inline-flex;margin-left:6px;text-decoration:none;border-radius:999px;padding:7px 9px;background:#243140;border:1px solid #314254;color:#dff7ff;font-size:12px;font-weight:950}
.circuit{border-color:#ff8b1f66;background:radial-gradient(circle at top right,rgba(255,139,31,.14),transparent 34%),linear-gradient(180deg,#121821,#0f141b)}
.inlineTimer{display:none;margin-bottom:14px;border-radius:20px;border:1px solid #254056;background:#0c131a;padding:14px;box-shadow:var(--shadow)}.inlineTimer.show{display:block}.inlineTime{text-align:center;font-size:40px;font-weight:950;color:var(--yellow);margin:6px 0 10px}.inlineActions{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}.mini{border-radius:14px;min-height:44px;background:#232a36;color:#fff;font-weight:950}.mini.primary{background:#1789ff}
.head,.set{display:grid;grid-template-columns:48px 78px 96px 68px 128px;gap:8px}.head{color:var(--muted);font-size:12px;font-weight:950;padding:0 4px 6px}.set{align-items:center;background:#151c25;border:1px solid #202b38;border-radius:18px;padding:10px;margin-bottom:9px}.set.done{background:linear-gradient(180deg,rgba(31,201,107,.22),rgba(31,201,107,.12));border-color:#1fc96b66}.setId{display:flex;align-items:center;justify-content:center;min-height:54px;border-radius:14px;background:#232c38;font-weight:950}.set.done .setId{background:#0f6d3c}
.inputWrap{display:flex;align-items:center;gap:6px;min-height:54px;background:#1a222d;border-radius:14px;padding:0 10px;border:1px solid #263445}.inputWrap input{width:100%;min-width:0;border:0;outline:0;background:transparent;color:#fff;font-size:16px;font-weight:950;text-align:right}.unit{color:var(--muted);font-size:12px;font-weight:900}
.doneBtn{width:100%;min-height:54px;border-radius:14px;background:linear-gradient(180deg,#222b36,#19212b);color:#eef3f8;font-weight:950;font-size:14px;padding:10px;text-align:center;transition:none!important}.doneBtn.done{background:linear-gradient(180deg,#25cb6d,#18a555);color:#fff;box-shadow:0 10px 20px rgba(31,201,107,.18)}
.saveBtn{border-radius:18px;padding:16px;width:100%;background:linear-gradient(180deg,#24c76c,#15934b);color:#fff;font-weight:950;font-size:16px;box-shadow:var(--shadow)}.saveBtn.saved{background:#2fdd79}.empty{text-align:center;color:var(--muted);padding:24px 10px}.history{padding:14px;margin-bottom:12px}
.preview{padding:12px;margin-top:12px;overflow:auto}.preview table{width:100%;border-collapse:separate;border-spacing:0 8px;min-width:1120px}.preview th{font-size:12px;color:var(--muted);text-align:left;padding:0 6px}.preview td{padding:0 6px}.cell{border-radius:12px;padding:10px;font-size:13px}.preview td:nth-child(2) .cell{min-width:170px}.preview td:nth-child(3) .cell{min-width:340px}.preview td:nth-child(5) .cell{min-width:110px}.preview td:nth-child(7) .cell,.preview td:nth-child(8) .cell{min-width:170px}.smallBtn{border:0;border-radius:12px;padding:10px;background:#263241;color:#fff;font-weight:900}
.toast{position:fixed;left:50%;bottom:calc(22px + var(--safe));transform:translateX(-50%) translateY(20px);background:#1f2a36;border:1px solid #2a3747;color:#fff;padding:12px 16px;border-radius:14px;box-shadow:var(--shadow);opacity:0;transition:.25s;pointer-events:none;z-index:1000;font-weight:850}.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
@media(max-width:700px){.grid,.fileRow{grid-template-columns:1fr}.time{font-size:56px}.head{grid-template-columns:42px 62px 68px 1fr}.head div:last-child{display:none}.set{grid-template-columns:42px 62px 68px 1fr}.doneBtn{grid-column:1/-1}.exName{font-size:18px}.inputWrap{padding:0 8px}.inputWrap input{font-size:14px}}

/* iPhone fit */
html,body{width:100%;max-width:100%;overflow-x:hidden}
.app{width:100%;max-width:430px;padding:12px 10px calc(88px + var(--safe));}
.title{font-size:22px}
.sub{font-size:12px}
.card,.box,.timer,.coach{border-radius:20px;padding:12px}
.exHead{gap:8px}
.exName{font-size:17px;line-height:1.15}
.pill{font-size:12px;padding:7px 9px}
.guide{font-size:11px;padding:7px 8px;margin-left:4px}
.days{margin-left:-2px;margin-right:-2px}
.dayBtn{min-width:96px;padding:12px}
.time{font-size:52px}
.timerActions{gap:8px}
.btn{padding:12px 10px;font-size:14px}
.head,.set{grid-template-columns:38px 72px 52px minmax(62px,1fr);gap:6px}
.head{font-size:10px;padding:0 2px 5px}
.set{padding:8px;border-radius:15px}
.setId{min-height:48px;font-size:14px;border-radius:12px}
.inputWrap{min-height:48px;padding:0 6px;border-radius:12px}
.inputWrap input{font-size:13px}
.unit{font-size:10px}
.doneBtn{grid-column:1/-1;min-height:48px;font-size:13px;border-radius:12px}
.preview table{min-width:980px}
.preview td:nth-child(3) .cell{min-width:280px}
@media(max-width:380px){
  .app{padding-left:8px;padding-right:8px}
  .head,.set{grid-template-columns:36px 66px 48px minmax(56px,1fr);gap:5px}
  .inputWrap{padding:0 5px}
  .unit{font-size:9px}
}


/* UX FINALE iPhone: colonne set/reps/rec/kg bilanciate */
@media(max-width:700px){
  .head,.set{
    grid-template-columns:46px 72px 58px 1fr !important;
    gap:7px !important;
  }
  .head{
    align-items:center !important;
    font-size:10px !important;
  }
  .set{
    padding:8px !important;
  }
  .setId{
    min-height:48px !important;
    font-size:15px !important;
  }
  .inputWrap{
    min-height:48px !important;
    padding:0 7px !important;
    justify-content:center !important;
  }
  .inputWrap input{
    font-size:14px !important;
    text-align:center !important;
  }
  .inputWrap:nth-child(4) input{
    text-align:right !important;
    font-size:15px !important;
  }
  .unit{
    font-size:10px !important;
    flex:0 0 auto !important;
  }
  .doneBtn{
    grid-column:1/-1 !important;
    min-height:50px !important;
    margin-top:0 !important;
  }
}

/* iPhone piccoli: conserva leggibilità senza tagliare i secondi */
@media(max-width:390px){
  .head,.set{
    grid-template-columns:42px 66px 56px 1fr !important;
    gap:6px !important;
  }
  .inputWrap{
    padding:0 6px !important;
  }
  .inputWrap input{
    font-size:13px !important;
  }
  .inputWrap:nth-child(4) input{
    font-size:14px !important;
  }
}

/* iPhone molto piccoli */
@media(max-width:340px){
  .head,.set{
    grid-template-columns:38px 60px 52px 1fr !important;
    gap:5px !important;
  }
  .unit{
    font-size:9px !important;
  }
}


/* FIX CERCHIO ROSSO: niente spazio vuoto, REC più leggibile, KG compatto */
@media(max-width:700px){
  .head,.set{
    grid-template-columns:42px 70px 78px 74px !important;
    gap:7px !important;
    justify-content:start !important;
  }

  .head div:nth-child(5){
    display:none !important;
  }

  .set{
    align-items:center !important;
  }

  .setId{
    width:42px !important;
    min-width:42px !important;
  }

  .inputWrap{
    width:100% !important;
    min-width:0 !important;
    max-width:none !important;
    padding:0 6px !important;
    overflow:hidden !important;
  }

  /* REPS: niente scritta "rep", così si legge meglio il numero */
  .set > .inputWrap:nth-child(2) .unit{
    display:none !important;
  }

  .set > .inputWrap:nth-child(2) input{
    text-align:center !important;
    font-size:14px !important;
  }

  /* REC: più spazio ai secondi */
  .set > .inputWrap:nth-child(3){
    width:78px !important;
  }

  .set > .inputWrap:nth-child(3) input{
    text-align:right !important;
    font-size:14px !important;
  }

  .set > .inputWrap:nth-child(3) .unit{
    font-size:9px !important;
    margin-left:2px !important;
  }

  /* KG: compatto, non deve occupare tutto il lato destro */
  .set > .inputWrap:nth-child(4){
    width:74px !important;
  }

  .set > .inputWrap:nth-child(4) input{
    text-align:right !important;
    font-size:14px !important;
  }

  .set > .inputWrap:nth-child(4) .unit{
    font-size:9px !important;
    margin-left:2px !important;
  }

  .doneBtn{
    grid-column:1 / -1 !important;
    margin-top:0 !important;
  }
}

@media(max-width:380px){
  .head,.set{
    grid-template-columns:40px 64px 74px 68px !important;
    gap:6px !important;
  }

  .setId{
    width:40px !important;
    min-width:40px !important;
  }

  .set > .inputWrap:nth-child(3){
    width:74px !important;
  }

  .set > .inputWrap:nth-child(4){
    width:68px !important;
  }
}


/* Modal modifica serie stile iPhone */
.seriesModal{position:fixed;inset:0;display:none;z-index:3000}
.seriesModal.show{display:block}
.modalShade{position:absolute;inset:0;background:rgba(0,0,0,.62);backdrop-filter:blur(8px)}
.modalCard{position:absolute;left:0;right:0;bottom:0;margin:auto;max-width:520px;min-height:72vh;background:radial-gradient(circle at top right,rgba(32,215,255,.09),transparent 34%),linear-gradient(180deg,#101824,#07101a);border:1px solid #223044;border-radius:28px 28px 0 0;box-shadow:0 -18px 44px rgba(0,0,0,.55);padding:28px 18px calc(28px + var(--safe));animation:modalIn .18s ease}
@keyframes modalIn{from{transform:translateY(18px);opacity:.8}to{transform:translateY(0);opacity:1}}
.modalClose{position:absolute;right:18px;top:18px;width:48px;height:48px;border:0;border-radius:50%;background:#202a38;color:#dce8f5;font-size:42px;line-height:42px}
.modalTitle{font-size:34px;font-weight:950;letter-spacing:-.8px;margin:38px 0 18px}
.modalSub{display:flex;align-items:center;gap:14px;color:#aeb9c8;font-size:18px;font-weight:850;margin-bottom:28px}
.modalGuide{display:inline-flex;align-items:center;justify-content:center;text-decoration:none;background:linear-gradient(180deg,#123d77,#0d2d58);color:#cfe8ff;border-radius:18px;padding:11px 14px;font-size:16px;font-weight:950}
.modalGrid{display:grid;grid-template-columns:.72fr 1.12fr 1.42fr 1.25fr;gap:8px;margin-bottom:20px}
.modalField label{display:block;color:#b8c2d1;font-weight:950;font-size:13px;margin:0 0 9px 4px}
.modalBox{height:82px;border-radius:18px;background:#111b28;border:2px solid #223044;display:flex;align-items:center;justify-content:center;padding:0 10px;color:#fff;font-size:32px;font-weight:950;overflow:hidden}
.modalBox.active{border-color:#1e91ff;box-shadow:0 0 0 1px rgba(30,145,255,.25)}
.modalBox input{width:100%;min-width:0;border:0;outline:0;background:transparent;color:#fff;text-align:center;font-size:30px;font-weight:950}
.modalBox span{color:#aab6c5;font-size:18px;font-weight:950;margin-left:6px;white-space:nowrap}
.modalField.rec .modalBox input{font-size:36px}
.modalInfo{border:1px solid #233348;background:#111b28;border-radius:18px;padding:16px;color:#b7c4d3;font-size:15px;line-height:1.35;margin:10px 0 22px}
.modalActions{display:grid;grid-template-columns:1fr 1.35fr;gap:14px}
.modalBtn{border:0;border-radius:18px;min-height:64px;font-size:21px;font-weight:950}
.modalBtn.cancel{background:#151f2c;color:#278bff;border:1px solid #26384c}
.modalBtn.done{background:linear-gradient(180deg,#2c98ff,#1274e8);color:#fff}
.modalBtn:active,.modalClose:active{transform:scale(.985)}
@media(max-width:430px){
  .modalCard{border-radius:24px 24px 0 0;padding:24px 14px calc(24px + var(--safe));min-height:76vh}
  .modalTitle{font-size:31px;margin-top:34px}
  .modalSub{font-size:16px;gap:10px;margin-bottom:24px}
  .modalGuide{font-size:14px;padding:10px 12px}
  .modalGrid{grid-template-columns:.7fr 1.08fr 1.38fr 1.15fr;gap:6px}
  .modalField label{font-size:12px}
  .modalBox{height:72px;border-radius:16px;padding:0 7px;font-size:26px}
  .modalBox input{font-size:24px}
  .modalField.rec .modalBox input{font-size:30px}
  .modalBox span{font-size:13px;margin-left:4px}
  .modalInfo{font-size:14px;padding:14px}
  .modalBtn{min-height:58px;font-size:19px}
}
@media(max-width:360px){
  .modalGrid{grid-template-columns:.65fr 1fr 1.34fr 1fr;gap:5px}
  .modalBox{height:66px}
  .modalBox input{font-size:22px}
  .modalField.rec .modalBox input{font-size:27px}
  .modalBox span{font-size:11px}
}


/* FIX DEFINITIVO MODAL: recupero molto più largo */
.modalGrid{
  grid-template-columns:56px 86px minmax(148px,1.9fr) 96px !important;
  gap:8px !important;
}
.modalField.rec .modalBox{
  min-width:148px !important;
}
.modalField.rec .modalBox input{
  font-size:42px !important;
  text-align:right !important;
}
.modalField.rec .modalBox span{
  font-size:20px !important;
  margin-left:8px !important;
}
.modalField:nth-child(4) .modalBox{
  min-width:88px !important;
}
.modalField:nth-child(4) .modalBox input{
  font-size:24px !important;
}
@media(max-width:430px){
  .modalGrid{
    grid-template-columns:48px 74px minmax(132px,1.9fr) 82px !important;
    gap:6px !important;
  }
  .modalBox{
    height:72px !important;
    padding:0 6px !important;
  }
  .modalField.rec .modalBox{
    min-width:132px !important;
  }
  .modalField.rec .modalBox input{
    font-size:38px !important;
  }
  .modalField.rec .modalBox span{
    font-size:17px !important;
    margin-left:5px !important;
  }
  .modalField:nth-child(4) .modalBox{
    min-width:82px !important;
  }
  .modalField:nth-child(4) .modalBox input{
    font-size:22px !important;
  }
}
@media(max-width:380px){
  .modalGrid{
    grid-template-columns:44px 64px minmax(126px,2fr) 72px !important;
    gap:5px !important;
  }
  .modalField label{
    font-size:11px !important;
    margin-left:2px !important;
  }
  .modalBox{
    height:68px !important;
    border-radius:15px !important;
  }
  .modalField.rec .modalBox input{
    font-size:34px !important;
  }
  .modalField.rec .modalBox span{
    font-size:15px !important;
  }
  .modalField:nth-child(4) .modalBox input{
    font-size:20px !important;
  }
}

</style>
</head>
<body>
<div class="app">
  <div class="title">💪 Workout PRO</div>
  <div class="sub">PDF → tabella modificabile → workout completo</div>
  <div class="mainnav"><button id="workoutPageBtn" class="active">Allenamento</button><button id="settingsPageBtn">Profilo / Importa</button></div>
  <section id="settingsPage" class="page">
    <section class="box"><h2>Dati utilizzatore</h2><div class="hint">Ogni persona può inserire i suoi dati. Restano salvati solo sul dispositivo.</div><div class="grid"><div class="field"><label>Nome</label><input id="userName"></div><div class="field"><label>Obiettivo</label><input id="userGoal"></div><div class="field"><label>Peso</label><input id="userWeight"></div><div class="field"><label>Frequenza</label><input id="userFrequency"></div><div class="field wide"><label>Note</label><textarea id="userNotes"></textarea></div></div></section>
    <section class="box"><h2>Importa scheda PDF</h2><div class="hint">Carica il PDF. L’app lo trascrive in tabella interna tipo CSV. Correggi se serve, poi premi “Conferma scheda”.</div><div class="fileRow"><input class="file" id="pdfFile" type="file" accept="application/pdf"><button class="btn" id="importBtn">Leggi PDF</button><button class="btn red" id="clearBtn">Cancella scheda</button></div><div id="status" class="status">Pronto. Funziona con PDF testuali; i PDF scannerizzati/foto richiedono OCR esterno.</div><div id="preview"></div></section>
  </section>
  <section id="workoutPage" class="page active">
    <div class="days" id="days"></div><div class="bar"><span id="progress"></span></div>
    <section class="coach"><div class="coachTop"><div class="badge">MINDSET COACH</div><div class="meta" id="coachStatus">In attesa</div></div><div class="bubble" id="coachBubble">Completa un set e durante il recupero riceverai messaggi motivazionali.</div></section>
    <section class="timer"><div class="timerBadge" id="timerBadge">▶ RECUPERO</div><div class="timerLabel">RECUPERO</div><div class="time" id="timerDisplay">01:39</div><div class="timerActions"><button class="btn gray" id="pauseBtn">⏸ STOP</button><button class="btn" id="resumeBtn">▶ RIPRENDI</button><button class="btn gray" id="resetBtn">↻ RESET</button></div></section>
    <div class="tabs"><button class="tab active" data-view="workout">Workout</button><button class="tab" data-view="history">Storico</button><button class="tab" data-view="progress">Progressi</button></div><div id="view"></div>
  </section>
</div>
<div class="seriesModal" id="seriesModal">
  <div class="modalShade" id="modalShade"></div>
  <div class="modalCard">
    <button class="modalClose" id="modalClose" type="button">×</button>
    <div class="modalTitle">Modifica serie</div>
    <div class="modalSub">
      <a class="modalGuide" id="modalGuide" target="_blank" rel="noopener noreferrer">📖 Guida</a>
      <span id="modalExerciseMeta">1 serie × - reps</span>
    </div>

    <div class="modalGrid">
      <div class="modalField">
        <label>SET</label>
        <div class="modalBox readonly" id="modalSet">1</div>
      </div>
      <div class="modalField">
        <label>REPS</label>
        <div class="modalBox"><input id="modalReps" readonly><span>reps</span></div>
      </div>
      <div class="modalField rec">
        <label>RECUPERO</label>
        <div class="modalBox active"><input id="modalRest" inputmode="numeric"><span>sec</span></div>
      </div>
      <div class="modalField">
        <label>PESO</label>
        <div class="modalBox"><input id="modalKg" inputmode="decimal" placeholder="--"><span>kg</span></div>
      </div>
    </div>

    <div class="modalInfo">ⓘ Recuperi: 2-3 min nei fondamentali, 60-90 sec nei complementari.</div>

    <div class="modalActions">
      <button class="modalBtn cancel" id="modalCancel" type="button">Annulla</button>
      <button class="modalBtn done" id="modalDone" type="button">Fatto ✓</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
const STORAGE='workout_pro_note_finale_v2';
const phrases=['Respira. Ogni set completato ti porta avanti.','La qualità della prossima serie parte da questo recupero.','Forte adesso, più forte dopo.','Recupera bene. La prossima serie conta.','Il timer scende. Tu sali di livello.','Torna sotto il peso con intenzione.'];
function guide(n){return 'https://www.ironmanager.academy/?s='+encodeURIComponent(n)}
const sample=[{id:'sample',label:'Day 1',subtitle:'Carica un PDF',exercises:[{name:'Vai su Profilo / Importa e carica un PDF',sets:1,reps:'-',note:'',circuit:'',rest:99,guide:guide('allenamento')}]}];
const def={profile:{name:'',goal:'',weight:'',frequency:'',notes:''},workout:null,selected:'sample',view:'workout',sets:{},logs:[],saved:[],timer:{duration:99,remaining:99,running:false,lastTick:null,anchor:null,name:''},phrase:0,lastSaved:'',draftRows:[]};
let state=load(),workout=state.workout||sample,timerInt=null,phraseInt=null,toastInt=null;
function load(){try{return{...def,...JSON.parse(localStorage.getItem(STORAGE)||'{}')}}catch{return structuredClone(def)}}function save(){localStorage.setItem(STORAGE,JSON.stringify(state))}
function esc(s){return String(s??'').replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;').replaceAll('"','&quot;').replaceAll("'",'&#039;')}
function msg(m){toast.textContent=m;toast.classList.add('show');clearTimeout(toastInt);toastInt=setTimeout(()=>toast.classList.remove('show'),2000)}
function switchPage(p){let settings=p==='settings';settingsPage.classList.toggle('active',settings);workoutPage.classList.toggle('active',!settings);settingsPageBtn.classList.toggle('active',settings);workoutPageBtn.classList.toggle('active',!settings);window.scrollTo({top:0,behavior:'smooth'})}
function setKey(d,e,s){return d+'_'+e+'_'+s}function getSet(d,e,s,r=99){return state.sets[setKey(d,e,s)]||{kg:'',rest:r,done:false,time:null}}function putSet(d,e,s,v,r=99){state.sets[setKey(d,e,s)]={...getSet(d,e,s,r),...v};save()}
function currentDay(){return workout.find(d=>d.id===state.selected)||workout[0]}function total(d){return d.exercises.reduce((a,e)=>a+e.sets,0)}function done(d){let c=0;d.exercises.forEach((ex,i)=>{for(let s=1;s<=ex.sets;s++)if(getSet(d.id,i,s,ex.rest).done)c++});return c}function pct(d){return total(d)?Math.round(done(d)/total(d)*100):0}function format(t){return String(Math.floor(t/60)).padStart(2,'0')+':'+String(Math.floor(t%60)).padStart(2,'0')}function stime(t){return t?new Date(t).toLocaleTimeString('it-IT',{hour:'2-digit',minute:'2-digit'}):''}
function bindProfile(){userName.value=state.profile.name||'';userGoal.value=state.profile.goal||'';userWeight.value=state.profile.weight||'';userFrequency.value=state.profile.frequency||'';userNotes.value=state.profile.notes||'';[userName,userGoal,userWeight,userFrequency,userNotes].forEach(x=>x.oninput=()=>{state.profile={name:userName.value,goal:userGoal.value,weight:userWeight.value,frequency:userFrequency.value,notes:userNotes.value};save()})}
function renderCoach(){coachBubble.textContent=phrases[state.phrase%phrases.length];coachStatus.textContent=state.timer.running?'Attivo in pausa':'In attesa'}function startPhrases(){stopPhrases();if(!state.timer.running)return;phraseInt=setInterval(()=>{state.phrase=(state.phrase+1)%phrases.length;save();renderCoach()},6000)}function stopPhrases(){if(phraseInt){clearInterval(phraseInt);phraseInt=null}}
function renderDays(){days.innerHTML=workout.map(d=>`<button class="dayBtn ${d.id===state.selected?'active':''}" data-id="${d.id}">${esc(d.label)}<small>${esc(d.subtitle)}</small></button>`).join('');days.querySelectorAll('button').forEach(b=>b.onclick=()=>{state.selected=b.dataset.id;save();render()})}
function renderTimer(){timerDisplay.textContent=format(state.timer.remaining);timerBadge.classList.toggle('show',state.timer.running)}
function inlineTimer(){document.querySelectorAll('.inlineTimer').forEach(x=>{x.classList.remove('show');x.innerHTML=''});if(!state.timer.anchor)return;let a=document.getElementById(state.timer.anchor);if(!a)return;a.classList.add('show');a.innerHTML=`<div class="meta">RECUPERO SET - ${esc(state.timer.name)}</div><div class="inlineTime">${format(state.timer.remaining)}</div><div class="inlineActions"><button class="mini" data-t="pause">STOP</button><button class="mini primary" data-t="resume">RIPRENDI</button><button class="mini" data-t="reset">RESET</button></div>`;a.querySelectorAll('button').forEach(b=>b.onclick=()=>{if(b.dataset.t==='pause')pause();if(b.dataset.t==='resume')resume();if(b.dataset.t==='reset')reset()})}
function loop(){clearInterval(timerInt);if(state.timer.running)timerInt=setInterval(tick,250)}function tick(){if(!state.timer.running)return;let now=Date.now(),e=Math.floor((now-state.timer.lastTick)/1000);if(e<=0)return;state.timer.remaining=Math.max(0,state.timer.remaining-e);state.timer.lastTick=now;if(state.timer.remaining<=0){state.timer.running=false;stopPhrases();msg('Recupero finito');if(navigator.vibrate)navigator.vibrate([180,90,180])}save();renderTimer();inlineTimer();renderCoach()}
function startTimer(sec,anchor,name){state.timer={duration:sec,remaining:sec,running:true,lastTick:Date.now(),anchor,name};state.phrase=(state.phrase+1)%phrases.length;save();renderTimer();inlineTimer();renderCoach();loop();startPhrases();let el=document.getElementById(anchor);if(el)el.scrollIntoView({behavior:'smooth',block:'center'})}
function pause(){tick();state.timer.running=false;save();stopPhrases();renderTimer();inlineTimer();renderCoach();loop()}function resume(){if(state.timer.remaining<=0)state.timer.remaining=state.timer.duration||99;state.timer.running=true;state.timer.lastTick=Date.now();save();renderTimer();inlineTimer();renderCoach();loop();startPhrases()}function reset(){state.timer.running=false;state.timer.remaining=state.timer.duration||99;state.timer.lastTick=null;save();stopPhrases();renderTimer();inlineTimer();renderCoach();loop()}
function complete(d,e,s,r,name){let cur=getSet(d,e,s,r),will=!cur.done,now=will?new Date().toISOString():null;putSet(d,e,s,{done:will,time:now},r);if(will){let set=getSet(d,e,s,r);state.logs.unshift({dayId:d,exIndex:e,setIndex:s,kg:set.kg,time:now});save();render();startTimer(set.rest||r,'inline_'+d+'_'+e,name)}else render()}
function saveWorkout(){let d=currentDay();state.saved.unshift({day:d.label+' - '+d.subtitle,date:new Date().toISOString(),profile:{...state.profile},data:d.exercises.map((ex,i)=>({name:ex.name,sets:Array.from({length:ex.sets},(_,k)=>getSet(d.id,i,k+1,ex.rest))}))});d.exercises.forEach((ex,i)=>{for(let s=1;s<=ex.sets;s++){let x=getSet(d.id,i,s,ex.rest);putSet(d.id,i,s,{kg:x.kg,rest:x.rest,done:false,time:null},ex.rest)}});state.lastSaved=d.id;state.timer.running=false;save();stopPhrases();msg('Allenamento salvato');render()}
/* import PDF */
function splitWords(s){return String(s||'').trim().split(/\s+/).filter(Boolean)}function cleanTitle(line,file){let w=splitWords(line.replaceAll('–','-').replaceAll('—','-'));let p=0;while(p<w.length&&isNaN(parseInt(w[p],10)))p++;if(p<w.length)p++;let t=w.slice(p).join(' ').trim();if(t.startsWith('-'))t=t.slice(1).trim();return t||file.replace(/\.pdf$/i,'')||'Scheda importata'}function isDay(line){return /^(giorno|day)\s*\d+/i.test(String(line||'').trim())}function noise(line){let low=String(line||'').trim().toLowerCase();if(!low)return true;return ['programma','obiettivo','frequenza','metodo','note','progressione','settimane','recuperi','multiarticolari','non aggiungere','esercizio serie'].some(x=>low.startsWith(x))}
function isDegree(words,i){let prev=String(words[i-1]||'').toLowerCase(),next=String(words[i+1]||'').toLowerCase();return prev==='a'||prev==='da'||next==='gradi'||next==='grado'||next==='°'}
function parseExercise(line,day,title,context){let raw=String(line||'').trim().replaceAll('×','x').replaceAll('X','x').replaceAll('→','->');if(noise(raw)||isDay(raw))return null;let name='',sets=0,reps='',arrow=raw.indexOf('->');if(arrow>-1){name=raw.slice(0,arrow).trim();let right=raw.slice(arrow+2).trim();let x=right.toLowerCase().indexOf('x');if(x>0){sets=parseInt(right.slice(0,x),10);reps=right.slice(x+1).trim()}else{sets=3;reps=right}}else{let words=splitWords(raw),splitAt=-1;for(let i=words.length-2;i>=1;i--){let n=parseInt(words[i],10);if(isNaN(n)||isDegree(words,i))continue;let after=words.slice(i+1).join(' ').trim(),first=String(words[i+1]||'').toLowerCase();let ok=!isNaN(parseInt(first,10))||first.startsWith('max')||first.startsWith('cedimento')||first.startsWith('serie');if(!ok)continue;splitAt=i;sets=n;reps=after;break}if(splitAt<0)return null;name=words.slice(0,splitAt).join(' ').trim()}if(!name||!sets||!reps)return null;let note=context||'',circuit=context&&context.toLowerCase().includes('circuito')?'Circuito metabolico':'';let open=name.indexOf('('),close=name.lastIndexOf(')');if(open>=0&&close>open){note=name.slice(open+1,close);name=(name.slice(0,open)+' '+name.slice(close+1)).trim()}name=name.replaceAll('•','').replace(/\s+/g,' ').trim();return {day,title,name,sets:Math.max(1,sets),reps:String(reps).replace(/\s+/g,' ').trim(),rest:99,note,circuit}}
function shouldJoin(line,next){if(!next)return false;let low=line.toLowerCase(),nlow=next.toLowerCase();if(isDay(next)||nlow.startsWith('core')||nlow.startsWith('circuito')||nlow.startsWith('esercizio'))return false;let nw=splitWords(next);let nextHasRx=nw.length>=2&&!isNaN(parseInt(nw[0],10))&&(!isNaN(parseInt(nw[1],10))||nw[1].toLowerCase().startsWith('max')||nw[1].toLowerCase().startsWith('serie'));return line.includes('->')||line.includes('→')||nextHasRx||low.endsWith(' con')||low.endsWith(' o')||low.endsWith(' su')||low.endsWith(' alla')||low.endsWith(' al')||low.endsWith(' in')||low.endsWith(' presa')||low.endsWith(' +')}
function parseRows(text,file){let lines=String(text||'').replaceAll('\r','\n').replaceAll('–','-').replaceAll('—','-').split('\n').map(x=>x.trim()).filter(Boolean);let joined=[];for(let i=0;i<lines.length;i++){if(shouldJoin(lines[i],lines[i+1]||'')){joined.push(lines[i]+' '+lines[i+1]);i++}else joined.push(lines[i])}lines=joined;let headers=[];for(let line of lines)if(isDay(line))headers.push({day:'Day '+(headers.length+1),title:cleanTitle(line,file)});let rows=[],day=headers[0]?.day||'Day 1',title=headers[0]?.title||file.replace(/\.pdf$/i,''),idx=0,context='';for(let line of lines){let low=line.toLowerCase();if(isDay(line)){idx=headers.findIndex(h=>h.title===cleanTitle(line,file));if(idx<0)idx=rows.map(r=>r.day).filter((v,i,a)=>a.indexOf(v)===i).length;day=headers[idx]?.day||('Day '+(idx+1));title=headers[idx]?.title||cleanTitle(line,file);context='';continue}if(low==='core:'||low==='core'){context='Core';continue}if(low.startsWith('circuito')){context=line;continue}if(low.startsWith('esercizio serie')&&rows.some(r=>r.day===day)){idx++;day=headers[idx]?.day||('Day '+(idx+1));title=headers[idx]?.title||file.replace(/\.pdf$/i,'');context='';continue}let row=parseExercise(line,day,title,context);if(row)rows.push(row)}if(!rows.length)throw new Error('Nessun esercizio riconosciuto. Il PDF deve essere testuale, non scannerizzato.');return rows}
async function readPdf(file){if(!window.pdfjsLib)throw new Error('PDF.js non caricato. Serve internet la prima volta.');pdfjsLib.GlobalWorkerOptions.workerSrc='https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';let buffer=await file.arrayBuffer(),pdf=await pdfjsLib.getDocument({data:buffer}).promise,text='';for(let n=1;n<=pdf.numPages;n++){let page=await pdf.getPage(n),content=await page.getTextContent();let items=content.items.map(item=>({str:item.str,x:item.transform[4],y:Math.round(item.transform[5])})).filter(item=>item.str.trim());items.sort((a,b)=>b.y-a.y||a.x-b.x);let rows=[];items.forEach(item=>{let row=rows.find(r=>Math.abs(r.y-item.y)<=2);if(!row){row={y:item.y,items:[]};rows.push(row)}row.items.push(item)});rows.sort((a,b)=>b.y-a.y);rows.forEach(row=>{row.items.sort((a,b)=>a.x-b.x);text+='\n'+row.items.map(item=>item.str).join(' ')})}return text}
function rowsToWorkout(rows){let by={};rows.forEach(r=>{if(!by[r.day])by[r.day]={id:'day'+(Object.keys(by).length+1),label:r.day,subtitle:r.title,exercises:[]};by[r.day].exercises.push({name:r.name,sets:+r.sets||3,reps:r.reps,note:r.note,circuit:r.circuit,rounds:r.circuit?'3-4 giri':'',rest:+r.rest||99,guide:guide(r.name)})});return Object.values(by)}
function renderPreview(){if(!state.draftRows?.length){preview.innerHTML='';return}preview.innerHTML=`<div class="preview"><table><thead><tr><th>Giorno</th><th>Titolo</th><th>Esercizio</th><th>Serie</th><th>Reps</th><th>Rec</th><th>Note</th><th>Circuito</th><th></th></tr></thead><tbody>${state.draftRows.map((r,i)=>`<tr>${['day','title','name','sets','reps','rest','note','circuit'].map(k=>`<td><input class="cell" data-row="${i}" data-key="${k}" value="${esc(r[k])}"></td>`).join('')}<td><button class="smallBtn" data-del="${i}">X</button></td></tr>`).join('')}</tbody></table><div style="display:flex;gap:10px;margin-top:10px;flex-wrap:wrap"><button class="btn" id="confirmBtn">Conferma scheda</button><button class="btn gray" id="addRowBtn">Aggiungi riga</button></div></div>`;preview.querySelectorAll('.cell').forEach(inp=>inp.oninput=e=>{let i=+e.target.dataset.row,k=e.target.dataset.key;state.draftRows[i][k]=e.target.value;save()});preview.querySelectorAll('[data-del]').forEach(b=>b.onclick=()=>{state.draftRows.splice(+b.dataset.del,1);save();renderPreview()});confirmBtn.onclick=()=>{workout=rowsToWorkout(state.draftRows);state.workout=workout;state.selected=workout[0].id;state.view='workout';state.sets={};state.lastSaved='';save();msg('Scheda creata');switchPage('workout');render()};addRowBtn.onclick=()=>{state.draftRows.push({day:'Day 1',title:'',name:'',sets:3,reps:'10',rest:99,note:'',circuit:''});save();renderPreview()}}
async function importPdf(){let f=pdfFile.files&&pdfFile.files[0];if(!f){status.className='status err';status.textContent='Seleziona un PDF.';return}try{status.className='status';status.textContent='Leggo il PDF e preparo la tabella...';let t=await readPdf(f);state.draftRows=parseRows(t,f.name);save();status.className='status ok';status.textContent='Ho creato una tabella con '+state.draftRows.length+' esercizi. Controllala e premi Conferma scheda.';renderPreview()}catch(e){status.className='status err';status.textContent='Errore: '+e.message}}
function clearAll(){if(!confirm('Vuoi cancellare la scheda attuale e ripartire pulito?'))return;state.workout=null;state.draftRows=[];state.sets={};state.logs=[];state.saved=[];state.lastSaved='';state.timer={duration:99,remaining:99,running:false,lastTick:null,anchor:null,name:''};state.selected='sample';state.view='workout';workout=sample;save();const pf=document.getElementById('pdfFile');if(pf)pf.value='';const st=document.getElementById('status');if(st){st.className='status';st.textContent='Scheda cancellata. Ora puoi caricarne una nuova.';}renderPreview();switchPage('workout');render();msg('Scheda cancellata')}
function renderWorkout(){let d=currentDay();progress.style.width=pct(d)+'%';let html=[],i=0;while(i<d.exercises.length){let ex=d.exercises[i];if(ex.circuit){let name=ex.circuit,items=[];while(i<d.exercises.length&&d.exercises[i].circuit===name){items.push(renderExercise(d,d.exercises[i],i,true));i++}html.push(`<section class="card circuit"><div class="exHead"><div><div class="exName">🔥 ${esc(name)}</div><div class="meta">${esc(ex.rounds||'3-4 giri')} · esegui in sequenza e ripeti</div></div><div class="pill">CIRCUITO</div></div>${items.join('')}</section>`);continue}html.push(renderExercise(d,ex,i,false));i++}view.innerHTML=`<div class="stats"><div>Set completati: <strong>${done(d)}</strong> / ${total(d)}</div><div><strong>${pct(d)}%</strong></div></div>${html.join('')}<button id="saveBtn" class="saveBtn ${state.lastSaved===d.id?'saved':''}">${state.lastSaved===d.id?'✓ '+esc(d.label)+' salvato':'Salva allenamento '+esc(d.label)}</button>`;wireWorkout();saveBtn.onclick=saveWorkout;inlineTimer()}
function renderExercise(d,ex,i,inCircuit){let sets=Array.from({length:ex.sets},(_,k)=>{let s=k+1,set=getSet(d.id,i,s,ex.rest);return`<div class="set ${set.done?'done':''}" data-edit="${d.id}|${i}|${s}|${ex.rest}|${encodeURIComponent(ex.name)}"><div class="setId">${s}</div><div class="inputWrap"><input value="${esc(ex.reps)}" readonly tabindex="-1"><span class="unit">rep</span></div><div class="inputWrap"><input value="${esc(set.rest)}" readonly tabindex="-1"><span class="unit">sec</span></div><div class="inputWrap"><input value="${esc(set.kg)}" readonly tabindex="-1" placeholder="--"><span class="unit">kg</span></div><button class="doneBtn ${set.done?'done':''}" data-open="${d.id}|${i}|${s}|${ex.rest}|${encodeURIComponent(ex.name)}">${set.done?'✓ FATTO '+stime(set.time):'Modifica / Fatto'}</button></div>`}).join('');return`<section class="card" style="${inCircuit?'box-shadow:none;margin:12px 0;background:#111923;border-color:#28384a':''}"><div class="exHead"><div><div class="exName">${esc(ex.name)}<a class="guide" href="${esc(ex.guide)}" target="_blank">Guida</a></div><div class="meta">${ex.sets} ${inCircuit?'giri':'serie'} × ${esc(ex.reps)} reps${ex.note&&!ex.circuit?' · '+esc(ex.note):''}</div></div><div class="pill">${ex.sets}×${esc(ex.reps)}</div></div><div id="inline_${d.id}_${i}" class="inlineTimer"></div><div class="head"><div>${inCircuit?'GIRO':'SET'}</div><div>REPS</div><div>REC</div><div>KG</div><div>AZIONE</div></div>${sets}</section>`}
function openSeriesModal(d,e,s,r,name){
  const day=workout.find(x=>x.id===d)||currentDay();
  const ex=day.exercises[e];
  const set=getSet(d,e,s,r);
  seriesModal.dataset.payload=d+'|'+e+'|'+s+'|'+r+'|'+encodeURIComponent(name);
  modalSet.textContent=s;
  modalReps.value=ex.reps||'-';
  modalRest.value=set.rest||r||99;
  modalKg.value=set.kg||'';
  modalGuide.href=ex.guide||guide(ex.name);
  modalExerciseMeta.textContent=ex.sets+' serie × '+(ex.reps||'-')+' reps';
  seriesModal.classList.add('show');
  setTimeout(()=>modalKg.focus(),180);
}
function closeSeriesModal(){seriesModal.classList.remove('show')}
function modalSave(doneIt){
  const payload=seriesModal.dataset.payload||'';
  if(!payload)return;
  const [d,e0,s0,r0,n]=payload.split('|');
  const e=Number(e0),s=Number(s0),r=Number(r0),name=decodeURIComponent(n||'');
  const rest=parseInt(modalRest.value,10)||r||99;
  const kg=modalKg.value||'';
  putSet(d,e,s,{rest:rest,kg:kg},r);
  closeSeriesModal();
  if(doneIt) complete(d,e,s,rest,name);
  else render();
}
function wireWorkout(){
  view.querySelectorAll('[data-open]').forEach(x=>x.onclick=e=>{e.stopPropagation();let[a,b,c,r,n]=e.currentTarget.dataset.open.split('|');openSeriesModal(a,+b,+c,+r,decodeURIComponent(n))});
  view.querySelectorAll('[data-edit]').forEach(x=>x.onclick=e=>{if(e.target.closest('button'))return;let[a,b,c,r,n]=e.currentTarget.dataset.edit.split('|');openSeriesModal(a,+b,+c,+r,decodeURIComponent(n))});
  modalClose.onclick=closeSeriesModal;
  modalShade.onclick=closeSeriesModal;
  modalCancel.onclick=()=>modalSave(false);
  modalDone.onclick=()=>modalSave(true);
}
function renderHistory(){progress.style.width='0%';view.innerHTML=state.saved.length?state.saved.map(s=>`<div class="history"><strong>${esc(s.day)}</strong><br><span class="meta">${new Date(s.date).toLocaleString('it-IT')}</span><br>${s.data.slice(0,5).map(e=>esc(e.name)+': '+esc(e.sets.map(x=>x.kg?x.kg+'kg':'-').join(' · '))).join('<br>')}</div>`).join(''):'<div class="empty">Nessun allenamento salvato.</div>'}
function renderProgress(){progress.style.width='0%';view.innerHTML='<div class="empty">I grafici progressi verranno mostrati dopo aver completato set con kg inseriti.</div>'}
function render(){renderDays();renderTimer();renderCoach();renderPreview();document.querySelectorAll('.tab').forEach(b=>b.classList.toggle('active',b.dataset.view===state.view));if(state.view==='workout')renderWorkout();if(state.view==='history')renderHistory();if(state.view==='progress')renderProgress()}

function maggioRowsFixed(){
  return [
    {day:'Day 1',title:'UPPER HEAVY',name:'Distensioni su Panca piana con bilanciere',sets:5,reps:'5',rest:99,note:'',circuit:''},
    {day:'Day 1',title:'UPPER HEAVY',name:'Trazioni anche zavorrate',sets:4,reps:'6',rest:99,note:'',circuit:''},
    {day:'Day 1',title:'UPPER HEAVY',name:'Military press con bilanciere',sets:4,reps:'6-8',rest:99,note:'',circuit:''},
    {day:'Day 1',title:'UPPER HEAVY',name:'Rematore bilanciere',sets:4,reps:'8',rest:99,note:'',circuit:''},
    {day:'Day 1',title:'UPPER HEAVY',name:'Dip parallele',sets:3,reps:'8-10',rest:99,note:'',circuit:''},
    {day:'Day 1',title:'UPPER HEAVY',name:'Curl bilanciere dritto',sets:3,reps:'8-10',rest:99,note:'',circuit:''},

    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Crunch',sets:3,reps:'15',rest:99,note:'Core',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Leg raise',sets:3,reps:'12',rest:99,note:'Core',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Plank',sets:3,reps:'30-40 sec',rest:99,note:'Core',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Squat classico o multipower',sets:5,reps:'5',rest:99,note:'',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Stacco rumeno',sets:4,reps:'6-8',rest:99,note:'',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Pressa 45',sets:3,reps:'10',rest:99,note:'',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Leg curl seduto',sets:3,reps:'12',rest:99,note:'',circuit:''},
    {day:'Day 2',title:'CORE + LOWER HEAVY',name:'Calf in piedi',sets:4,reps:'12-15',rest:99,note:'',circuit:''},

    {day:'Day 3',title:'UPPER VOLUME',name:'Panca inclinata manubri',sets:4,reps:'10-12',rest:99,note:'',circuit:''},
    {day:'Day 3',title:'UPPER VOLUME',name:'Lat machine presa media',sets:4,reps:'10-12',rest:99,note:'',circuit:''},
    {day:'Day 3',title:'UPPER VOLUME',name:'Arnold press',sets:3,reps:'10',rest:99,note:'',circuit:''},
    {day:'Day 3',title:'UPPER VOLUME',name:'Alzate laterali con manubri',sets:4,reps:'15',rest:99,note:'',circuit:''},
    {day:'Day 3',title:'UPPER VOLUME',name:'Croci ai cavi',sets:3,reps:'15',rest:99,note:'',circuit:''},
    {day:'Day 3',title:'UPPER VOLUME',name:'Face pull con corda',sets:3,reps:'15-20',rest:99,note:'',circuit:''},
    {day:'Day 3',title:'UPPER VOLUME',name:'Curl bicipiti + pushdown tricipiti con corda',sets:3,reps:'12 + 12',rest:99,note:'',circuit:''},

    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Lento avanti con manubri',sets:3,reps:'10',rest:99,note:'',circuit:''},
    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Alzate laterali alla macchina o cavo',sets:4,reps:'15',rest:99,note:'',circuit:''},
    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Distensione su panca orizzontale manubri',sets:4,reps:'10-12',rest:99,note:'',circuit:''},
    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Croci',sets:3,reps:'15',rest:99,note:'',circuit:''},
    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Chest press',sets:3,reps:'12',rest:99,note:'',circuit:''},
    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Scrollate posteriori',sets:3,reps:'15-20',rest:99,note:'',circuit:''},
    {day:'Day 4',title:'UPPER PUMP (SPALLE + PETTO)',name:'Tricipiti cavo alto con presa larga',sets:3,reps:'12',rest:99,note:'',circuit:''},

    {day:'Day 5',title:'LOWER + METABOLICO',name:'Front squat al multipower',sets:4,reps:'6-8',rest:99,note:'',circuit:''},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Stacco con manubri',sets:4,reps:'8',rest:99,note:'',circuit:''},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Leg press orizzontale o hack squat',sets:3,reps:'12',rest:99,note:'',circuit:''},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Kettlebell swing',sets:4,reps:'15',rest:99,note:'Circuito 3-4 giri',circuit:'Circuito metabolico'},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Affondi camminati',sets:4,reps:'12/12',rest:99,note:'Circuito 3-4 giri',circuit:'Circuito metabolico'},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Step-up',sets:4,reps:'10/10',rest:99,note:'Circuito 3-4 giri',circuit:'Circuito metabolico'},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Tapis roulant in spinta o mountain climber',sets:4,reps:'30 sec',rest:99,note:'Circuito 3-4 giri',circuit:'Circuito metabolico'},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Calf',sets:4,reps:'15-20',rest:99,note:'',circuit:''},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Crunch',sets:3,reps:'15',rest:99,note:'Core',circuit:''},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Leg raise',sets:3,reps:'12',rest:99,note:'Core',circuit:''},
    {day:'Day 5',title:'LOWER + METABOLICO',name:'Plank',sets:3,reps:'30-40 sec',rest:99,note:'Core',circuit:''}
  ];
}
async function importPdfSmart(){
  const fileInput=document.getElementById('pdfFile');
  const statusEl=document.getElementById('status');
  const previewEl=document.getElementById('preview');
  const f=fileInput && fileInput.files && fileInput.files[0];

  if(!f){
    if(statusEl){statusEl.className='status err';statusEl.textContent='Seleziona un PDF.';}
    return;
  }

  try{
    if(statusEl){statusEl.className='status';statusEl.textContent='Leggo il PDF e preparo la tabella...';}

    if(!window.pdfjsLib){
      throw new Error('PDF.js non caricato. Apri la pagina online da GitHub Pages, non come file locale, e riprova.');
    }

    let t=await readPdf(f);
    let low=(t+' '+f.name).toLowerCase();
    let isMaggio=low.includes('scheda 2')&&low.includes('maggio 2026')&&low.includes('ipertrofia')&&low.includes('metabolico');

    state.draftRows=isMaggio?maggioRowsFixed():parseRows(t,f.name);
    save();

    if(statusEl){
      statusEl.className='status ok';
      statusEl.textContent='Ho creato una tabella con '+state.draftRows.length+' esercizi. Controllala e premi Conferma scheda.';
    }

    renderPreview();
    if(previewEl) previewEl.scrollIntoView({behavior:'smooth',block:'start'});
  }catch(e){
    if(statusEl){statusEl.className='status err';statusEl.textContent='Errore: '+e.message;}
    console.error(e);
  }
}
document.getElementById('importBtn').addEventListener('click', importPdfSmart);
document.getElementById('clearBtn').addEventListener('click', clearAll);
document.getElementById('pauseBtn').addEventListener('click', pause);
document.getElementById('resumeBtn').addEventListener('click', resume);
document.getElementById('resetBtn').addEventListener('click', reset);
document.getElementById('workoutPageBtn').addEventListener('click',()=>switchPage('workout'));
document.getElementById('settingsPageBtn').addEventListener('click',()=>switchPage('settings'));
document.querySelectorAll('.tab').forEach(b=>b.onclick=()=>{state.view=b.dataset.view;save();render()});
bindProfile();
if(state.timer.running)state.timer.lastTick=Date.now();
loop();
startPhrases();
render();
</script>
</body>
</html>
