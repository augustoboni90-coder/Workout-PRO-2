<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <title>Workout PRO</title>
  <meta name="theme-color" content="#0b0f14" />
  <style>
    :root{
      --bg:#0b0f14;
      --panel:#121821;
      --panel2:#171f29;
      --line:#273241;
      --text:#f4f7fb;
      --muted:#95a3b5;
      --cyan:#20d7ff;
      --cyan2:#1498ff;
      --green:#23c96d;
      --green2:#15934b;
      --yellow:#ffd54d;
      --orange:#ff8b1f;
      --shadow:0 12px 28px rgba(0,0,0,.34);
      --safe-top: env(safe-area-inset-top);
      --safe-bottom: env(safe-area-inset-bottom);
    }

    *{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
    html,body{
      margin:0;
      padding:0;
      background:linear-gradient(180deg,#0b0f14 0%, #070a0d 100%);
      color:var(--text);
      font-family:-apple-system,BlinkMacSystemFont,"SF Pro Display","Segoe UI",Roboto,Helvetica,Arial,sans-serif;
    }
    body{min-height:100vh}
    .app{max-width:980px;margin:0 auto;padding:calc(14px + var(--safe-top)) 14px calc(110px + var(--safe-bottom));}
    .topbar{text-align:center;font-size:24px;font-weight:900;letter-spacing:.2px;margin-bottom:14px}

    .days{display:flex;gap:10px;overflow:auto;padding:4px 0 12px;scrollbar-width:none}
    .days::-webkit-scrollbar{display:none}
    .day-btn{flex:0 0 auto;min-width:112px;border:none;border-radius:18px;padding:14px 14px 12px;background:linear-gradient(180deg,#1b212b 0%,#121923 100%);color:var(--text);box-shadow:var(--shadow);text-align:left;cursor:pointer;transition:.18s ease}
    .day-btn .d1{font-size:14px;font-weight:900}
    .day-btn .d2{font-size:12px;color:var(--muted);margin-top:2px}
    .day-btn.active{background:linear-gradient(180deg,#27dcff 0%,#11c1e8 100%);color:#05131a}
    .day-btn.active .d2{color:#0c4253}

    .progress-wrap{margin:0 2px 14px;height:8px;background:#161c24;border-radius:999px;overflow:hidden}
    .progress-bar{height:100%;width:0%;background:linear-gradient(90deg,var(--cyan),#57efff);transition:width .25s ease}

    .motivator{background:radial-gradient(circle at left center, rgba(32,215,255,.10), transparent 28%),linear-gradient(180deg,#151c25 0%,#0f151d 100%);border:1px solid #233041;border-radius:22px;box-shadow:var(--shadow);margin-bottom:16px;padding:14px}
    .motivator-top{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-bottom:10px}
    .motivator-badge{border-radius:999px;padding:8px 12px;background:linear-gradient(180deg,#38e0ff 0%,#17c2ea 100%);color:#05131a;font-size:12px;font-weight:900;letter-spacing:.8px;flex:0 0 auto}
    .motivator-status{color:var(--muted);font-size:13px;font-weight:800;text-align:right}
    .motivator-bubble{min-height:74px;border-radius:18px;padding:14px 16px;background:linear-gradient(180deg,#18212c 0%,#121923 100%);border:1px solid #263445;display:flex;align-items:center;font-size:18px;line-height:1.35;font-weight:800;color:#e9fbff}

    .top-timer-card{background:radial-gradient(circle at top right, rgba(255,213,77,.08), transparent 30%),linear-gradient(180deg,#121821 0%,#0d1219 100%);border:1px solid #1e2632;border-radius:26px;padding:18px 16px 16px;box-shadow:var(--shadow);margin-bottom:16px}
    .timer-badge{width:max-content;margin:0 auto 10px;background:linear-gradient(180deg,#ff9028 0%,#ff7a17 100%);color:white;border-radius:999px;padding:8px 14px;font-weight:900;font-size:12px;display:none}
    .timer-badge.show{display:block}
    .timer-title{text-align:center;font-size:12px;font-weight:800;letter-spacing:.9px;color:var(--muted);margin-bottom:4px}
    .timer-main{text-align:center;font-size:68px;line-height:1;font-weight:900;color:var(--yellow);font-variant-numeric:tabular-nums;margin:4px 0 8px}
    .timer-sub{text-align:center;color:var(--muted);font-size:15px;margin-bottom:14px}
    .timer-actions{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:12px}
    .btn{border:none;border-radius:16px;padding:14px 10px;cursor:pointer;font-weight:900;font-size:15px;background:linear-gradient(180deg,#232a36 0%,#1a212b 100%);color:var(--text);box-shadow:var(--shadow);transition:transform .08s ease, filter .15s ease}
    .btn:active{transform:scale(.985);filter:brightness(1.05)}
    .btn.primary{background:linear-gradient(180deg,#2abfff 0%,#1789ff 100%);color:white}
    .tip{border:1px solid #115870;background:linear-gradient(180deg,rgba(32,215,255,.13),rgba(32,215,255,.05));color:#c9f7ff;border-radius:14px;padding:12px 14px;font-size:14px;line-height:1.35}

    .segmented{display:flex;gap:10px;margin:16px 0}
    .seg-btn{flex:1;border:none;border-radius:16px;padding:12px 10px;background:#171c24;color:var(--muted);font-weight:900;cursor:pointer}
    .seg-btn.active{background:linear-gradient(180deg,#232d3a 0%,#1a222e 100%);color:var(--text);outline:1px solid #2d3948}

    .stats{display:flex;justify-content:space-between;align-items:center;color:var(--muted);font-size:14px;margin:4px 2px 10px;gap:10px}
    .card{background:radial-gradient(circle at top right, rgba(32,215,255,.05), transparent 30%),linear-gradient(180deg,#121821 0%,#0f141b 100%);border:1px solid #1d2530;border-radius:24px;padding:16px;box-shadow:var(--shadow);margin-bottom:14px;scroll-margin-top:20px}
    .exercise-head{display:flex;justify-content:space-between;gap:12px;align-items:flex-start;margin-bottom:14px}
    .exercise-left{flex:1;min-width:0}
    .exercise-top{display:flex;align-items:center;gap:8px;flex-wrap:wrap;margin-bottom:4px}
    .exercise-name{font-size:21px;font-weight:900;line-height:1.12}
    .guide-link{display:inline-flex;align-items:center;justify-content:center;text-decoration:none;border-radius:999px;padding:8px 10px;background:linear-gradient(180deg,#243140 0%,#1a2430 100%);border:1px solid #314254;color:#dff7ff;font-size:12px;font-weight:900;white-space:nowrap}
    .exercise-meta{color:var(--muted);font-size:13px;line-height:1.25}
    .pill{flex:0 0 auto;background:linear-gradient(180deg,#0d7daf 0%,#095e92 100%);color:#e9fbff;border-radius:999px;padding:8px 12px;font-size:13px;font-weight:900;white-space:nowrap}

    .inline-timer{display:none;margin:0 0 14px;border-radius:20px;border:1px solid #254056;background:radial-gradient(circle at top right, rgba(255,213,77,.08), transparent 35%),linear-gradient(180deg,#111922 0%,#0c131a 100%);padding:14px;box-shadow:var(--shadow)}
    .inline-timer.show{display:block}
    .inline-timer-top{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:10px}
    .inline-timer-label{font-size:13px;color:var(--muted);font-weight:800}
    .inline-timer-ex{font-size:14px;font-weight:900;color:#dff8ff;text-align:right}
    .inline-timer-time{text-align:center;font-size:42px;line-height:1;font-weight:900;color:var(--yellow);font-variant-numeric:tabular-nums;margin:6px 0 10px}
    .inline-timer-actions{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
    .mini-btn{border:none;border-radius:14px;min-height:46px;font-weight:900;font-size:14px;cursor:pointer;color:var(--text);background:linear-gradient(180deg,#232a36 0%,#1a212b 100%);transition:transform .08s ease, filter .15s ease}
    .mini-btn:active{transform:scale(.985);filter:brightness(1.05)}
    .mini-btn.primary{background:linear-gradient(180deg,#2abfff 0%,#1789ff 100%);color:white}

    .grid-head{display:grid;grid-template-columns:64px 100px 1fr 132px;gap:10px;color:var(--muted);font-weight:900;font-size:12px;padding:0 4px 6px}
    .set-row{display:grid;grid-template-columns:64px 100px 1fr 132px;gap:10px;align-items:center;background:linear-gradient(180deg,#151b24 0%,#111721 100%);border:1px solid #202734;border-radius:18px;padding:12px;margin-bottom:10px;transition:.18s ease}
    .set-row.done{background:linear-gradient(180deg,rgba(31,201,107,.22),rgba(31,201,107,.12));border-color:#1fc96b66}
    .set-id{display:flex;align-items:center;justify-content:center;border-radius:14px;background:#232a36;min-height:58px;font-weight:900;font-size:17px;color:#f0f4f8}
    .set-row.done .set-id{background:#0f6d3c}
    .rest-wrap,.load-wrap{display:flex;align-items:center;gap:8px;min-height:58px;background:#1a2029;border-radius:14px;padding:0 12px;border:1px solid #262f3d;overflow:hidden;min-width:0}
    .rest-input,.load-input{width:100%;min-width:0;border:none;outline:none;background:transparent;color:var(--text);font-size:18px;font-weight:900;padding:0;appearance:textfield;text-align:right}
    .rest-input::-webkit-outer-spin-button,.rest-input::-webkit-inner-spin-button,.load-input::-webkit-outer-spin-button,.load-input::-webkit-inner-spin-button{-webkit-appearance:none;margin:0}
    .unit{color:var(--muted);font-size:14px;font-weight:800;white-space:nowrap}
    .action-btn{border:none;width:100%;min-height:58px;border-radius:14px;background:linear-gradient(180deg,#222934 0%,#1a202a 100%);color:#eef3f8;font-weight:900;font-size:14px;cursor:pointer;padding:10px 12px;line-height:1.15;transition:transform .08s ease, filter .15s ease, background .18s ease, box-shadow .18s ease}
    .action-btn:active{transform:scale(.98);filter:brightness(1.05)}
    .action-btn.done{background:linear-gradient(180deg,#25cb6d 0%,#18a555 100%);color:white;box-shadow:0 0 0 1px rgba(255,255,255,.04), 0 10px 20px rgba(31,201,107,.18)}
    .action-time{display:block;font-size:12px;font-weight:800;opacity:.9;margin-top:4px}
    .mini-note{margin-top:10px;color:var(--muted);font-size:13px;line-height:1.35}

    .day-save{margin-top:12px;display:flex;justify-content:center}
    .save-day-btn{border:none;border-radius:18px;padding:16px 18px;width:100%;background:linear-gradient(180deg,#24c76c 0%,#15934b 100%);color:white;font-weight:900;font-size:16px;cursor:pointer;box-shadow:var(--shadow);transition:transform .08s ease, filter .15s ease, box-shadow .18s ease, background .18s ease}
    .save-day-btn:active{transform:scale(.985);filter:brightness(1.05)}
    .save-day-btn.saved{background:linear-gradient(180deg,#2fdd79 0%,#1aa85a 100%);box-shadow:0 0 0 1px rgba(255,255,255,.05), 0 12px 24px rgba(31,201,107,.2)}

    .profile-box,.import-box{background:radial-gradient(circle at top right, rgba(32,215,255,.05), transparent 30%),linear-gradient(180deg,#121821 0%,#0f141b 100%);border:1px solid #1d2530;border-radius:24px;padding:16px;box-shadow:var(--shadow);margin-bottom:14px}
    .box-title{font-size:18px;font-weight:900;margin-bottom:6px}
    .box-sub{color:var(--muted);font-size:13px;line-height:1.35;margin-bottom:12px}
    .profile-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
    .field{display:flex;flex-direction:column;gap:6px}
    .field label{font-size:12px;color:var(--muted);font-weight:900}
    .field input,.field textarea,.file-input{width:100%;border:none;outline:none;border-radius:14px;background:#1a2029;border:1px solid #262f3d;color:var(--text);font-size:15px;font-weight:800;padding:13px}
    .field textarea{min-height:70px;resize:vertical}.wide{grid-column:1/-1}
    .import-actions{display:grid;grid-template-columns:1fr auto;gap:10px;align-items:center}
    .import-btn{border:none;border-radius:16px;padding:14px 16px;background:linear-gradient(180deg,#2abfff 0%,#1789ff 100%);color:white;font-weight:900;font-size:15px;cursor:pointer;box-shadow:var(--shadow)}
    .import-status{margin-top:10px;color:var(--muted);font-size:13px;line-height:1.35}.import-status.ok{color:#bfffd8}.import-status.err{color:#ffb8bf}

    .history-item,.chart-card{background:linear-gradient(180deg,#121821 0%,#0f141b 100%);border:1px solid #1f2734;border-radius:20px;padding:14px;margin-bottom:12px}
    .history-top{display:flex;justify-content:space-between;gap:10px;margin-bottom:8px;font-weight:900}
    .history-sub,.chart-sub{color:var(--muted);font-size:13px;line-height:1.35}
    .chart-title{font-size:18px;font-weight:900;margin-bottom:4px}
    canvas{width:100%;height:220px;display:block;background:linear-gradient(180deg,#0f141b 0%,#0b1017 100%);border-radius:18px;border:1px solid #1b2330;margin-top:10px}
    .empty{text-align:center;color:var(--muted);padding:24px 10px;line-height:1.4}

    .toast{position:fixed;left:50%;bottom:calc(22px + var(--safe-bottom));transform:translateX(-50%) translateY(20px);background:linear-gradient(180deg,#1f2a36 0%,#151d27 100%);border:1px solid #2a3747;color:#fff;padding:12px 16px;border-radius:14px;box-shadow:var(--shadow);opacity:0;transition:.25s ease;pointer-events:none;z-index:1000;font-weight:800;font-size:14px}
    .toast.show{opacity:1;transform:translateX(-50%) translateY(0)}

    @media (max-width:700px){
      .profile-grid,.import-actions{grid-template-columns:1fr}
      .timer-main{font-size:56px}
      .inline-timer-time{font-size:36px}
      .exercise-name{font-size:18px}
      .guide-link{font-size:11px;padding:7px 9px}
      .grid-head{grid-template-columns:56px 82px 1fr}
      .grid-head div:last-child{display:none}
      .set-row{grid-template-columns:56px 82px 1fr;gap:8px}
      .action-btn{grid-column:1 / -1}
      .rest-wrap,.load-wrap,.action-btn,.set-id{min-height:56px}
      .rest-input,.load-input{font-size:16px}
      .unit{font-size:12px}
      .motivator-bubble{font-size:16px;min-height:66px}
    }
  </style>
</head>
<body>
  <div class="app">
    <div class="topbar">💪 Workout PRO</div>

    <div class="days" id="days"></div>
    <div class="progress-wrap"><div class="progress-bar" id="dayProgress"></div></div>

    <div class="motivator">
      <div class="motivator-top">
        <div class="motivator-badge">MINDSET COACH</div>
        <div class="motivator-status" id="motivatorStatus">In attesa della pausa</div>
      </div>
      <div class="motivator-bubble" id="motivatorBubble">Completa un set e durante il recupero inizieranno i messaggi motivazionali.</div>
    </div>

    <section class="top-timer-card">
      <div class="timer-badge" id="timerBadge">▶ RECUPERO IN CORSO</div>
      <div class="timer-title">RECUPERO</div>
      <div class="timer-main" id="timerDisplay">01:39</div>
      <div class="timer-sub" id="timerSub">Tocca “Fatto” su un set per avviare il timer del set</div>

      <div class="timer-actions">
        <button class="btn" id="stopBtn">⏸ STOP</button>
        <button class="btn primary" id="resumeBtn">▶ RIPRENDI</button>
        <button class="btn" id="resetBtn">↻ RESET</button>
      </div>

      <div class="tip">Il timer si sposta vicino al set completato. Quando salvi il day, le spunte vengono tolte ma i pesi restano memorizzati.</div>
    </section>

    <div class="segmented">
      <button class="seg-btn active" data-view="workout">Workout</button>
      <button class="seg-btn" data-view="history">Storico</button>
      <button class="seg-btn" data-view="progress">Progressi</button>
    </div>

    <div id="view"></div>
  </div>

  <div class="toast" id="toast"></div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
  <script>
    const STORAGE_KEY = "workout_pro_maggio_2026_fisso_v1";

    function ironSearch(name){
      return "https://www.ironmanager.academy/?s=" + encodeURIComponent(name);
    }

    let workoutData = [
      {
        id: "day1",
        label: "Day 1",
        subtitle: "Upper Heavy",
        exercises: [
          { name: "Distensioni su panca piana con bilanciere", sets: 5, reps: "5", rest: 99, guide: ironSearch("distensioni panca piana bilanciere") },
          { name: "Trazioni anche zavorrate", sets: 4, reps: "6", rest: 99, guide: ironSearch("trazioni zavorrate") },
          { name: "Military press con bilanciere", sets: 4, reps: "6-8", rest: 99, guide: ironSearch("military press bilanciere") },
          { name: "Rematore bilanciere", sets: 4, reps: "8", rest: 99, guide: ironSearch("rematore bilanciere") },
          { name: "Dip parallele", sets: 3, reps: "8-10", rest: 99, guide: ironSearch("dip parallele") },
          { name: "Curl bilanciere dritto", sets: 3, reps: "8-10", rest: 99, guide: ironSearch("curl bilanciere dritto") }
        ]
      },
      {
        id: "day2",
        label: "Day 2",
        subtitle: "Core + Lower Heavy",
        exercises: [
          { name: "Crunch", sets: 3, reps: "15", note: "Core", rest: 99, guide: ironSearch("crunch addominali") },
          { name: "Leg raise", sets: 3, reps: "12", note: "Core", rest: 99, guide: ironSearch("leg raise") },
          { name: "Plank", sets: 3, reps: "30-40 sec", note: "Core", rest: 99, guide: ironSearch("plank") },
          { name: "Squat classico o multipower", sets: 5, reps: "5", rest: 99, guide: ironSearch("squat multipower") },
          { name: "Stacco rumeno", sets: 4, reps: "6-8", rest: 99, guide: ironSearch("stacco rumeno") },
          { name: "Pressa 45", sets: 3, reps: "10", rest: 99, guide: ironSearch("pressa 45") },
          { name: "Leg curl seduto", sets: 3, reps: "12", rest: 99, guide: ironSearch("leg curl seduto") },
          { name: "Calf in piedi", sets: 4, reps: "12-15", rest: 99, guide: ironSearch("calf in piedi") }
        ]
      },
      {
        id: "day3",
        label: "Day 3",
        subtitle: "Upper Volume",
        exercises: [
          { name: "Panca inclinata manubri", sets: 4, reps: "10-12", rest: 99, guide: ironSearch("panca inclinata manubri") },
          { name: "Lat machine presa media", sets: 4, reps: "10-12", rest: 99, guide: ironSearch("lat machine presa media") },
          { name: "Arnold press", sets: 3, reps: "10", rest: 99, guide: ironSearch("arnold press") },
          { name: "Alzate laterali con manubri", sets: 4, reps: "15", rest: 99, guide: ironSearch("alzate laterali manubri") },
          { name: "Croci ai cavi", sets: 3, reps: "15", rest: 99, guide: ironSearch("croci ai cavi") },
          { name: "Face pull con corda", sets: 3, reps: "15-20", rest: 99, guide: ironSearch("face pull corda") },
          { name: "Curl bicipiti + pushdown tricipiti con corda", sets: 3, reps: "12 + 12", rest: 99, guide: ironSearch("curl bicipiti pushdown tricipiti corda") }
        ]
      },
      {
        id: "day4",
        label: "Day 4",
        subtitle: "Upper Pump Spalle + Petto",
        exercises: [
          { name: "Lento avanti con manubri", sets: 3, reps: "10", rest: 99, guide: ironSearch("lento avanti manubri") },
          { name: "Alzate laterali alla macchina o cavo", sets: 4, reps: "15", rest: 99, guide: ironSearch("alzate laterali macchina cavo") },
          { name: "Distensione su panca orizzontale manubri", sets: 4, reps: "10-12", rest: 99, guide: ironSearch("distensione panca orizzontale manubri") },
          { name: "Croci", sets: 3, reps: "15", rest: 99, guide: ironSearch("croci petto") },
          { name: "Chest press", sets: 3, reps: "12", rest: 99, guide: ironSearch("chest press") },
          { name: "Scrollate posteriori", sets: 3, reps: "15-20", rest: 99, guide: ironSearch("scrollate posteriori") },
          { name: "Tricipiti cavo alto con presa larga", sets: 3, reps: "12", rest: 99, guide: ironSearch("tricipiti cavo alto presa larga") }
        ]
      },
      {
        id: "day5",
        label: "Day 5",
        subtitle: "Lower + Metabolico",
        exercises: [
          { name: "Front squat al multipower", sets: 4, reps: "6-8", rest: 99, guide: ironSearch("front squat multipower") },
          { name: "Stacco con manubri", sets: 4, reps: "8", rest: 99, guide: ironSearch("stacco manubri") },
          { name: "Leg press orizzontale o hack squat", sets: 3, reps: "12", rest: 99, guide: ironSearch("leg press orizzontale hack squat") },
          { name: "Kettlebell swing", sets: 4, reps: "15", note: "Circuito metabolico", circuit: "Circuito metabolico", rounds: "3-4 giri", rest: 99, guide: ironSearch("kettlebell swing") },
          { name: "Affondi camminati", sets: 4, reps: "12/12", note: "Circuito metabolico", circuit: "Circuito metabolico", rounds: "3-4 giri", rest: 99, guide: ironSearch("affondi camminati") },
          { name: "Step-up", sets: 4, reps: "10/10", note: "Circuito metabolico", circuit: "Circuito metabolico", rounds: "3-4 giri", rest: 99, guide: ironSearch("step up") },
          { name: "Tapis roulant in spinta o mountain climber", sets: 4, reps: "30 sec", note: "Circuito metabolico", circuit: "Circuito metabolico", rounds: "3-4 giri", rest: 99, guide: ironSearch("tapis roulant in spinta mountain climber") },
          { name: "Calf", sets: 4, reps: "15-20", rest: 99, guide: ironSearch("calf") },
          { name: "Crunch", sets: 3, reps: "15", note: "Core", rest: 99, guide: ironSearch("crunch addominali") },
          { name: "Leg raise", sets: 3, reps: "12", note: "Core", rest: 99, guide: ironSearch("leg raise") },
          { name: "Plank", sets: 3, reps: "30-40 sec", note: "Core", rest: 99, guide: ironSearch("plank") }
        ]
      }
    ];

    const motivationPhrases = [
      "Respira. Ogni set completato ti porta avanti.",
      "Non stai improvvisando: stai costruendo disciplina.",
      "La qualità della prossima serie parte da questo recupero.",
      "Forte adesso, più forte dopo.",
      "Usa il recupero per ricaricare, non per distrarti.",
      "Ogni volta che torni sotto il peso diventi più solido.",
      "Stai facendo il lavoro che molti rimandano.",
      "Tecnica pulita, mente lucida, focus totale.",
      "Recupera bene. La prossima serie conta.",
      "La costanza trasforma più della motivazione.",
      "Non serve essere perfetto, serve esserci davvero.",
      "Hai già fatto la parte difficile: iniziare.",
      "Un set alla volta. Un giorno alla volta.",
      "Rimani presente. Il progresso è qui.",
      "Respira profondo e prepara la prossima rep.",
      "Più controllo, più risultato.",
      "Il timer scende. Tu sali di livello.",
      "Questo è il momento in cui costruisci abitudine.",
      "Stai facendo qualcosa di buono per te.",
      "Torna sotto il bilanciere con intenzione."
    ];

    const defaultState = {
      selectedDay: "day1",
      currentView: "workout",
      timer: { duration: 99, remaining: 99, running: false, lastTick: null, anchorId: null, exerciseName: "" },
      savedDays: [],
      logs: [],
      setData: {},
      motivatorIndex: 0,
      lastSavedDayId: "",
      importedWorkoutData: null,
      userProfile: { name: "", goal: "", weight: "", frequency: "", notes: "" }
    };

    let state = loadState();
    state.importedWorkoutData = null;
    if (!workoutData.find(d => d.id === state.selectedDay)) state.selectedDay = workoutData[0].id;
    let timerInterval = null;
    let motivatorInterval = null;
    let toastTimeout = null;

    function loadState() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        if (!raw) return structuredClone(defaultState);
        const parsed = JSON.parse(raw);
        return {
          ...structuredClone(defaultState),
          ...parsed,
          timer: { ...defaultState.timer, ...(parsed.timer || {}) },
          savedDays: parsed.savedDays || [],
          logs: parsed.logs || [],
          setData: parsed.setData || {},
          motivatorIndex: Number.isInteger(parsed.motivatorIndex) ? parsed.motivatorIndex : 0,
          lastSavedDayId: parsed.lastSavedDayId || "",
          importedWorkoutData: parsed.importedWorkoutData || null,
          userProfile: parsed.userProfile || { name: "", goal: "", weight: "", frequency: "", notes: "" }
        };
      } catch {
        return structuredClone(defaultState);
      }
    }

    function saveState() { localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); }

    function bindProfileForm(){
      const p = state.userProfile || {};
      document.getElementById("userName").value = p.name || "";
      document.getElementById("userGoal").value = p.goal || "";
      document.getElementById("userWeight").value = p.weight || "";
      document.getElementById("userFrequency").value = p.frequency || "";
      document.getElementById("userNotes").value = p.notes || "";
      ["userName","userGoal","userWeight","userFrequency","userNotes"].forEach(id => {
        document.getElementById(id).addEventListener("input", () => {
          state.userProfile = {
            name: document.getElementById("userName").value,
            goal: document.getElementById("userGoal").value,
            weight: document.getElementById("userWeight").value,
            frequency: document.getElementById("userFrequency").value,
            notes: document.getElementById("userNotes").value
          };
          saveState();
        });
      });
    }

    function showToast(message){
      const toast = document.getElementById("toast");
      toast.textContent = message;
      toast.classList.add("show");
      if (toastTimeout) clearTimeout(toastTimeout);
      toastTimeout = setTimeout(() => toast.classList.remove("show"), 2200);
    }

    function escapeHtml(str) {
      return String(str ?? "")
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;")
        .replaceAll('"', "&quot;")
        .replaceAll("'", "&#039;");
    }

    function setKey(dayId, exIndex, setIndex) { return `${dayId}__${exIndex}__${setIndex}`; }

    function getSetData(dayId, exIndex, setIndex, exRest=99) {
      return state.setData[setKey(dayId, exIndex, setIndex)] || { load: "", rest: exRest, done: false, time: null };
    }

    function updateSetData(dayId, exIndex, setIndex, patch, exRest=99) {
      const key = setKey(dayId, exIndex, setIndex);
      state.setData[key] = { ...getSetData(dayId, exIndex, setIndex, exRest), ...patch };
      saveState();
    }

    function getDay() { return workoutData.find(d => d.id === state.selectedDay) || workoutData[0]; }
    function totalSetsForDay(day) { return day.exercises.reduce((sum, ex) => sum + ex.sets, 0); }
    function completedSetsForDay(day) {
      let count = 0;
      day.exercises.forEach((ex, exIndex) => {
        for (let s = 1; s <= ex.sets; s++) if (getSetData(day.id, exIndex, s, ex.rest).done) count++;
      });
      return count;
    }
    function progressPercent(day) {
      const total = totalSetsForDay(day);
      const done = completedSetsForDay(day);
      return total ? Math.round((done / total) * 100) : 0;
    }
    function formatTimer(sec) {
      const m = Math.floor(sec / 60).toString().padStart(2, "0");
      const s = Math.floor(sec % 60).toString().padStart(2, "0");
      return `${m}:${s}`;
    }
    function formatTimeShort(iso) {
      if (!iso) return "";
      return new Date(iso).toLocaleTimeString("it-IT", { hour:"2-digit", minute:"2-digit" });
    }
    function formatDateTime(iso) {
      if (!iso) return "";
      return new Date(iso).toLocaleString("it-IT", { day:"2-digit", month:"2-digit", year:"numeric", hour:"2-digit", minute:"2-digit" });
    }

    function renderMotivator() {
      const bubble = document.getElementById("motivatorBubble");
      const status = document.getElementById("motivatorStatus");
      bubble.textContent = motivationPhrases[state.motivatorIndex % motivationPhrases.length];
      if (state.timer.running) status.textContent = "Messaggi attivi durante la pausa";
      else if (state.timer.remaining !== state.timer.duration) status.textContent = "Pausa in stop";
      else status.textContent = "In attesa della pausa";
    }

    function startMotivatorLoop() {
      stopMotivatorLoop();
      if (!state.timer.running) return;
      motivatorInterval = setInterval(() => {
        state.motivatorIndex = (state.motivatorIndex + 1) % motivationPhrases.length;
        saveState();
        renderMotivator();
      }, 6000);
    }
    function stopMotivatorLoop() {
      if (motivatorInterval) { clearInterval(motivatorInterval); motivatorInterval = null; }
    }

    function renderDays() {
      const daysEl = document.getElementById("days");
      daysEl.innerHTML = workoutData.map(day => `
        <button class="day-btn ${day.id === state.selectedDay ? "active" : ""}" data-day="${day.id}">
          <div class="d1">${day.label}</div>
          <div class="d2">${day.subtitle}</div>
        </button>
      `).join("");
      daysEl.querySelectorAll(".day-btn").forEach(btn => {
        btn.addEventListener("click", () => { state.selectedDay = btn.dataset.day; saveState(); renderApp(); });
      });
    }

    function renderTopTimer() {
      const display = document.getElementById("timerDisplay");
      const sub = document.getElementById("timerSub");
      const badge = document.getElementById("timerBadge");
      display.textContent = formatTimer(state.timer.remaining);
      badge.classList.toggle("show", state.timer.running);
      if (state.timer.running) sub.textContent = "Timer attivo anche vicino al set completato";
      else if (state.timer.remaining !== state.timer.duration) sub.textContent = "Timer in pausa";
      else sub.textContent = "Tocca “Fatto” su un set per avviare il timer del set";
    }

    function renderInlineTimer() {
      document.querySelectorAll(".inline-timer").forEach(el => { el.classList.remove("show"); el.innerHTML = ""; });
      if (!state.timer.anchorId) return;
      const anchor = document.getElementById(state.timer.anchorId);
      if (!anchor) return;
      anchor.classList.add("show");
      anchor.innerHTML = `
        <div class="inline-timer-top">
          <div class="inline-timer-label">RECUPERO SET</div>
          <div class="inline-timer-ex">${escapeHtml(state.timer.exerciseName || "")}</div>
        </div>
        <div class="inline-timer-time">${formatTimer(state.timer.remaining)}</div>
        <div class="inline-timer-actions">
          <button class="mini-btn" data-inline="pause">⏸ STOP</button>
          <button class="mini-btn primary" data-inline="resume">▶ RIPRENDI</button>
          <button class="mini-btn" data-inline="reset">↻ RESET</button>
        </div>
      `;
      anchor.querySelectorAll("[data-inline]").forEach(btn => {
        btn.addEventListener("click", () => {
          const action = btn.dataset.inline;
          if (action === "pause") pauseTimer();
          if (action === "resume") resumeTimer();
          if (action === "reset") resetTimer();
        });
      });
    }

    function vibrate(pattern=[180,90,180]) { if (navigator.vibrate) navigator.vibrate(pattern); }
    function beep() {
      try {
        const ctx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = "sine";
        osc.frequency.value = 880;
        gain.gain.value = 0.03;
        osc.connect(gain);
        gain.connect(ctx.destination);
        osc.start();
        setTimeout(() => { osc.stop(); ctx.close(); }, 220);
      } catch {}
    }

    function stopTimerLoop() { if (timerInterval) { clearInterval(timerInterval); timerInterval = null; } }

    function tickTimer() {
      if (!state.timer.running) return;
      const now = Date.now();
      const elapsed = Math.floor((now - state.timer.lastTick) / 1000);
      if (elapsed <= 0) return;
      state.timer.remaining = Math.max(0, state.timer.remaining - elapsed);
      state.timer.lastTick = now;
      if (state.timer.remaining <= 0) {
        state.timer.running = false;
        state.timer.remaining = 0;
        stopTimerLoop();
        stopMotivatorLoop();
        beep();
        vibrate();
        showToast("Recupero finito");
      }
      saveState();
      renderTopTimer();
      renderInlineTimer();
      renderMotivator();
    }

    function ensureTimerLoop() {
      stopTimerLoop();
      if (state.timer.running) timerInterval = setInterval(tickTimer, 250);
    }

    function startTimer(duration=99, anchorId=null, exerciseName="") {
      state.timer.duration = Math.max(1, Number(duration) || 99);
      state.timer.remaining = state.timer.duration;
      state.timer.running = true;
      state.timer.lastTick = Date.now();
      if (anchorId) state.timer.anchorId = anchorId;
      if (exerciseName) state.timer.exerciseName = exerciseName;
      state.motivatorIndex = (state.motivatorIndex + 1) % motivationPhrases.length;
      saveState();
      renderTopTimer();
      renderInlineTimer();
      renderMotivator();
      ensureTimerLoop();
      startMotivatorLoop();
      if (anchorId) {
        const el = document.getElementById(anchorId);
        if (el) el.scrollIntoView({ behavior: "smooth", block: "center" });
      }
    }
    function pauseTimer() {
      tickTimer();
      state.timer.running = false;
      saveState();
      stopMotivatorLoop();
      renderTopTimer();
      renderInlineTimer();
      renderMotivator();
      ensureTimerLoop();
    }
    function resumeTimer() {
      if (state.timer.remaining <= 0) state.timer.remaining = state.timer.duration || 99;
      state.timer.running = true;
      state.timer.lastTick = Date.now();
      saveState();
      renderTopTimer();
      renderInlineTimer();
      renderMotivator();
      ensureTimerLoop();
      startMotivatorLoop();
    }
    function resetTimer() {
      state.timer.running = false;
      state.timer.remaining = state.timer.duration || 99;
      state.timer.lastTick = null;
      saveState();
      stopMotivatorLoop();
      renderTopTimer();
      renderInlineTimer();
      renderMotivator();
      ensureTimerLoop();
    }

    function toggleSetDone(dayId, exIndex, setIndex, fallbackRest=99, exerciseName="") {
      const current = getSetData(dayId, exIndex, setIndex, fallbackRest);
      const willBeDone = !current.done;
      const nowIso = willBeDone ? new Date().toISOString() : null;
      const anchorId = `inline_timer_${dayId}_${exIndex}`;
      updateSetData(dayId, exIndex, setIndex, { done: willBeDone, time: nowIso }, fallbackRest);
      if (willBeDone) {
        const setNow = getSetData(dayId, exIndex, setIndex, fallbackRest);
        state.logs.unshift({
          id: `${Date.now()}_${Math.random().toString(36).slice(2,8)}`,
          dayId, exIndex, setIndex,
          load: setNow.load || "",
          rest: setNow.rest || fallbackRest,
          time: nowIso
        });
        saveState();
        startTimer(setNow.rest || fallbackRest || 99, anchorId, exerciseName);
      } else {
        state.logs = state.logs.filter(log => !(log.dayId === dayId && log.exIndex === exIndex && log.setIndex === setIndex));
        saveState();
        renderApp();
      }
    }

    function updateLoad(dayId, exIndex, setIndex, value, fallbackRest=99) {
      updateSetData(dayId, exIndex, setIndex, { load: value }, fallbackRest);
      if (state.currentView === "progress") renderProgressView();
    }

    function updateRest(dayId, exIndex, setIndex, value, fallbackRest=99) {
      let rest = parseInt(value, 10);
      if (Number.isNaN(rest) || rest < 1) rest = fallbackRest;
      updateSetData(dayId, exIndex, setIndex, { rest }, fallbackRest);
    }

    function clearDoneFlagsForDay(day) {
      day.exercises.forEach((ex, exIndex) => {
        for (let s = 1; s <= ex.sets; s++) {
          const current = getSetData(day.id, exIndex, s, ex.rest);
          updateSetData(day.id, exIndex, s, { done: false, time: null, load: current.load, rest: current.rest }, ex.rest);
        }
      });
    }

    function saveCurrentDayWorkout() {
      const day = getDay();
      const snapshot = {
        id: `${day.id}_${Date.now()}`,
        dayId: day.id,
        dayLabel: `${day.label} - ${day.subtitle}`,
        savedAt: new Date().toISOString(),
        exercises: day.exercises.map((ex, exIndex) => ({
          name: ex.name,
          reps: ex.reps,
          sets: Array.from({ length: ex.sets }, (_, i) => {
            const setNumber = i + 1;
            return { set: setNumber, ...getSetData(day.id, exIndex, setNumber, ex.rest) };
          })
        }))
      };
      state.savedDays.unshift(snapshot);
      clearDoneFlagsForDay(day);
      state.timer.running = false;
      state.timer.remaining = state.timer.duration || 99;
      state.timer.lastTick = null;
      state.timer.anchorId = null;
      state.timer.exerciseName = "";
      state.lastSavedDayId = day.id;
      saveState();
      stopTimerLoop();
      stopMotivatorLoop();
      showToast("Allenamento salvato");
      renderApp();
    }

    function importedExercise(name, sets, reps, note){
      const cleanName = String(name || "").replaceAll("•", "").replaceAll("-", " ").replaceAll("  ", " ").trim();
      return { name: cleanName, sets: Math.max(1, parseInt(sets,10) || 3), reps: String(reps || "-").trim(), note: String(note || "").trim(), rest: 99, guide: ironSearch(cleanName) };
    }

    function parseExerciseSimple(line){
      let raw = String(line || "").trim();
      if (!raw) return null;
      const low = raw.toLowerCase();
      if (low.startsWith("programma") || low.startsWith("obiettivo") || low.startsWith("frequenza") || low.startsWith("metodo") || low.startsWith("note") || low.startsWith("progressione") || low.startsWith("settimane")) return null;
      if (low.startsWith("day ") || low.startsWith("giorno ") || low === "core:" || low === "core") return null;
      raw = raw.replaceAll("→", " -> ").replaceAll("➜", " -> ");
      let arrow = raw.indexOf("->");
      if (arrow > -1) {
        const name = raw.slice(0, arrow).trim();
        const rest = raw.slice(arrow + 2).trim();
        const x = rest.toLowerCase().indexOf("x");
        if (x > 0) return importedExercise(name, rest.slice(0,x).trim().split("-")[0], rest.slice(x+1).trim(), "");
        return importedExercise(name, 3, rest, "");
      }
      const parts = raw.split(" ").filter(Boolean);
      for (let i = parts.length - 1; i >= 1; i--) {
        const token = parts[i];
        const x = token.toLowerCase().indexOf("x");
        if (x > 0) return importedExercise(parts.slice(0,i).join(" "), token.slice(0,x), token.slice(x+1) + " " + parts.slice(i+1).join(" "), "");
      }
      if (parts.length >= 3 && !isNaN(parseInt(parts[parts.length-2],10))) {
        return importedExercise(parts.slice(0,parts.length-2).join(" "), parts[parts.length-2], parts[parts.length-1], "");
      }
      return null;
    }

    function parseWorkoutFromText(text, fileName){
      const lines = String(text || "").replaceAll(String.fromCharCode(13), String.fromCharCode(10)).split(String.fromCharCode(10)).map(x => x.trim()).filter(Boolean);
      const days = [];
      let current = null;
      let context = "";
      for (const line of lines) {
        const lower = line.toLowerCase();
        let dayNumber = "";
        let subtitle = "";
        if (lower.startsWith("giorno ") || lower.startsWith("day ")) {
          const words = line.replaceAll("–","-").replaceAll("—","-").split(" ").filter(Boolean);
          dayNumber = words[1] || String(days.length + 1);
          subtitle = line.includes("-") ? line.split("-").slice(1).join("-").trim() : words.slice(2).join(" ");
          current = { id: `import_day_${days.length+1}`, label: `Day ${days.length+1}`, subtitle: subtitle || fileName.replace(".pdf",""), exercises: [] };
          days.push(current);
          context = "";
          continue;
        }
        if (!current) continue;
        if (lower === "core:" || lower === "core") { context = "Core"; continue; }
        if (lower.startsWith("circuito")) { context = line; continue; }
        const ex = parseExerciseSimple(line);
        if (ex) { if (context && !ex.note) ex.note = context; current.exercises.push(ex); }
      }
      const valid = days.filter(d => d.exercises.length);
      if (!valid.length) throw new Error("Non ho trovato giorni ed esercizi leggibili nel PDF.");
      return valid;
    }

    async function readPdfText(file){
      if (!window.pdfjsLib) throw new Error("PDF.js non caricato. Serve internet la prima volta.");
      pdfjsLib.GlobalWorkerOptions.workerSrc = "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";
      const buffer = await file.arrayBuffer();
      const pdf = await pdfjsLib.getDocument({data: buffer}).promise;
      let text = "";
      for (let n = 1; n <= pdf.numPages; n++) {
        const page = await pdf.getPage(n);
        const content = await page.getTextContent();
        text += String.fromCharCode(10) + content.items.map(i => i.str).join(String.fromCharCode(10));
      }
      return text;
    }

    async function importPdfWorkout(){
      const file = document.getElementById("pdfFile").files && document.getElementById("pdfFile").files[0];
      const status = document.getElementById("importStatus");
      if (!file) { status.className = "import-status err"; status.textContent = "Seleziona prima un PDF."; return; }
      try {
        status.className = "import-status";
        status.textContent = "Sto leggendo e strutturando la scheda...";
        const text = await readPdfText(file);
        const parsed = parseWorkoutFromText(text, file.name);
        workoutData = parsed;
        state.importedWorkoutData = parsed;
        state.selectedDay = parsed[0].id;
        state.currentView = "workout";
        state.setData = {};
        state.lastSavedDayId = "";
        saveState();
        status.className = "import-status ok";
        status.textContent = `Scheda importata: ${parsed.length} giorni e ${parsed.reduce((a,d)=>a+d.exercises.length,0)} esercizi.`;
        showToast("Scheda PDF importata");
        renderApp();
      } catch (err) {
        status.className = "import-status err";
        status.textContent = "Errore: " + err.message;
      }
    }

    function renderWorkoutView() {
      const day = getDay();
      document.getElementById("dayProgress").style.width = `${progressPercent(day)}%`;

      const total = totalSetsForDay(day);
      const done = completedSetsForDay(day);

      function renderSetRows(ex, exIndex) {
        return Array.from({ length: ex.sets }, (_, i) => {
          const setNumber = i + 1;
          const set = getSetData(day.id, exIndex, setNumber, ex.rest);

          return `
            <div class="set-row ${set.done ? "done" : ""}">
              <div class="set-id">${setNumber}</div>

              <div class="rest-wrap">
                <input class="rest-input" inputmode="numeric" value="${escapeHtml(set.rest)}"
                  data-rest="${day.id}|${exIndex}|${setNumber}|${ex.rest}">
                <div class="unit">sec</div>
              </div>

              <div class="load-wrap">
                <input class="load-input" inputmode="decimal" placeholder="kg"
                  value="${escapeHtml(set.load)}"
                  data-load="${day.id}|${exIndex}|${setNumber}|${ex.rest}">
                <div class="unit">kg</div>
              </div>

              <button class="action-btn ${set.done ? "done" : ""}"
                data-toggle="${day.id}|${exIndex}|${setNumber}|${ex.rest}|${encodeURIComponent(ex.name)}">
                ${set.done ? `✓ FATTO <span class="action-time">${formatTimeShort(set.time)}</span>` : `Fatto / Annulla`}
              </button>
            </div>
          `;
        }).join("");
      }

      const chunks = [];
      for (let exIndex = 0; exIndex < day.exercises.length; exIndex++) {
        const ex = day.exercises[exIndex];

        if (ex.circuit) {
          const circuitName = ex.circuit;
          const startIndex = exIndex;
          const items = [];

          while (exIndex < day.exercises.length && day.exercises[exIndex].circuit === circuitName) {
            const circuitEx = day.exercises[exIndex];
            const circuitExIndex = exIndex;
            items.push(`
              <div class="card" style="margin:12px 0;background:linear-gradient(180deg,#151c25 0%,#101720 100%);box-shadow:none;border-color:#28384a;">
                <div class="exercise-head">
                  <div class="exercise-left">
                    <div class="exercise-top">
                      <div class="exercise-name">${escapeHtml(circuitEx.name)}</div>
                      <a class="guide-link" href="${escapeHtml(circuitEx.guide)}" target="_blank" rel="noopener noreferrer">Guida</a>
                    </div>
                    <div class="exercise-meta">
                      ${circuitEx.sets} giri × ${escapeHtml(circuitEx.reps)} reps
                    </div>
                  </div>
                  <div class="pill">${circuitEx.sets} × ${escapeHtml(circuitEx.reps)}</div>
                </div>

                <div id="inline_timer_${day.id}_${circuitExIndex}" class="inline-timer"></div>

                <div class="grid-head">
                  <div>GIRO</div>
                  <div>REC</div>
                  <div>KG</div>
                  <div>AZIONE</div>
                </div>

                ${renderSetRows(circuitEx, circuitExIndex)}
              </div>
            `);
            exIndex++;
          }
          exIndex--;

          chunks.push(`
            <section class="card" style="border-color:#ff8b1f55;background:radial-gradient(circle at top right,rgba(255,139,31,.12),transparent 32%),linear-gradient(180deg,#121821 0%,#0f141b 100%);">
              <div class="exercise-head">
                <div class="exercise-left">
                  <div class="exercise-top">
                    <div class="exercise-name">🔥 ${escapeHtml(circuitName)}</div>
                  </div>
                  <div class="exercise-meta">${escapeHtml(day.exercises[startIndex].rounds || "3-4 giri")} · esegui gli esercizi in sequenza, poi recupera e ripeti il giro.</div>
                </div>
                <div class="pill">CIRCUITO</div>
              </div>
              ${items.join("")}
            </section>
          `);
          continue;
        }

        chunks.push(`
          <section class="card">
            <div class="exercise-head">
              <div class="exercise-left">
                <div class="exercise-top">
                  <div class="exercise-name">${escapeHtml(ex.name)}</div>
                  <a class="guide-link" href="${escapeHtml(ex.guide)}" target="_blank" rel="noopener noreferrer">Guida</a>
                </div>
                <div class="exercise-meta">
                  ${ex.sets} serie × ${escapeHtml(ex.reps)} reps
                  ${ex.note ? ` · ${escapeHtml(ex.note)}` : ""}
                </div>
              </div>
              <div class="pill">${ex.sets} × ${escapeHtml(ex.reps)}</div>
            </div>

            <div id="inline_timer_${day.id}_${exIndex}" class="inline-timer"></div>

            <div class="grid-head">
              <div>SET</div>
              <div>REC</div>
              <div>KG</div>
              <div>AZIONE</div>
            </div>

            ${renderSetRows(ex, exIndex)}
            ${ex.note ? `<div class="mini-note">Nota: ${escapeHtml(ex.note)}</div>` : ""}
          </section>
        `);
      }

      const view = document.getElementById("view");
      view.innerHTML = `
        <div class="stats">
          <div>Set completati: <strong>${done}</strong> / ${total}</div>
          <div><strong>${progressPercent(day)}%</strong></div>
        </div>
        ${chunks.join("")}
        <div class="day-save">
          <button class="save-day-btn ${state.lastSavedDayId === day.id ? "saved" : ""}" id="saveDayBtn">${state.lastSavedDayId === day.id ? `✓ ${escapeHtml(day.label)} salvato` : `Salva allenamento ${escapeHtml(day.label)}`}</button>
        </div>
      `;

      view.querySelectorAll("[data-load]").forEach(input => {
        input.addEventListener("input", e => {
          const [dayId, exIndex, setIndex, fallbackRest] = e.currentTarget.dataset.load.split("|");
          updateLoad(dayId, Number(exIndex), Number(setIndex), e.currentTarget.value, Number(fallbackRest));
        });
      });

      view.querySelectorAll("[data-rest]").forEach(input => {
        input.addEventListener("change", e => {
          const [dayId, exIndex, setIndex, fallbackRest] = e.currentTarget.dataset.rest.split("|");
          updateRest(dayId, Number(exIndex), Number(setIndex), e.currentTarget.value, Number(fallbackRest));
          renderApp();
        });
      });

      view.querySelectorAll("[data-toggle]").forEach(btn => {
        btn.addEventListener("click", e => {
          const [dayId, exIndex, setIndex, fallbackRest, exerciseNameEnc] = e.currentTarget.dataset.toggle.split("|");
          toggleSetDone(dayId, Number(exIndex), Number(setIndex), Number(fallbackRest), decodeURIComponent(exerciseNameEnc));
        });
      });

      document.getElementById("saveDayBtn").addEventListener("click", saveCurrentDayWorkout);

      renderInlineTimer();
    }

    function renderHistoryView() {
      document.getElementById("dayProgress").style.width = "0%";
      const view = document.getElementById("view");
      if (!state.savedDays.length) {
        view.innerHTML = `<div class="empty">Nessun allenamento salvato ancora.</div>`;
        return;
      }
      view.innerHTML = state.savedDays.map(day => {
        const completed = day.exercises.reduce((acc, ex) => acc + ex.sets.filter(s => s.done).length, 0);
        const total = day.exercises.reduce((acc, ex) => acc + ex.sets.length, 0);
        return `
          <div class="history-item">
            <div class="history-top">
              <div>${escapeHtml(day.dayLabel)}</div>
              <div>${formatDateTime(day.savedAt)}</div>
            </div>
            <div class="history-sub">
              Set completati: <strong>${completed}/${total}</strong><br>
              ${day.exercises.slice(0,4).map(ex => {
                const loads = ex.sets.map(s => s.load ? `${s.load}kg` : "-").join(" · ");
                return `${escapeHtml(ex.name)}: ${escapeHtml(loads)}`;
              }).join("<br>")}
              ${day.exercises.length > 4 ? "<br>..." : ""}
            </div>
          </div>
        `;
      }).join("");
    }

    function getExerciseHistoryPoints() {
      const byExercise = {};
      state.logs.forEach(log => {
        const day = workoutData.find(d => d.id === log.dayId);
        const ex = day?.exercises?.[log.exIndex];
        const name = ex?.name;
        const load = parseFloat(String(log.load).replace(",", "."));
        if (!name || Number.isNaN(load)) return;
        if (!byExercise[name]) byExercise[name] = [];
        byExercise[name].push({ x: new Date(log.time), y: load });
      });
      Object.keys(byExercise).forEach(name => {
        byExercise[name].sort((a,b) => a.x - b.x);
        byExercise[name] = byExercise[name].slice(-12);
      });
      return byExercise;
    }

    function renderProgressView() {
      document.getElementById("dayProgress").style.width = "0%";
      const view = document.getElementById("view");
      const groups = getExerciseHistoryPoints();
      const names = Object.keys(groups);
      if (!names.length) {
        view.innerHTML = `<div class="empty">Nessun dato sufficiente per i grafici. Inserisci i carichi e completa qualche set.</div>`;
        return;
      }
      view.innerHTML = names.map((name, idx) => `
        <div class="chart-card">
          <div class="chart-title">${escapeHtml(name)}</div>
          <div class="chart-sub">Ultimi carichi registrati</div>
          <canvas id="chart_${idx}" width="800" height="220"></canvas>
        </div>
      `).join("");
      names.forEach((name, idx) => drawChart(`chart_${idx}`, groups[name]));
    }

    function drawChart(id, points) {
      const canvas = document.getElementById(id);
      if (!canvas || !points.length) return;
      const ctx = canvas.getContext("2d");
      const w = canvas.width;
      const h = canvas.height;
      ctx.clearRect(0,0,w,h);
      const pad = { top:22, right:20, bottom:34, left:42 };
      const minY = Math.min(...points.map(p => p.y));
      const maxY = Math.max(...points.map(p => p.y));
      const ySpan = Math.max(1, maxY - minY);
      const xStep = points.length > 1 ? (w - pad.left - pad.right) / (points.length - 1) : 0;

      ctx.strokeStyle = "#223044";
      ctx.lineWidth = 1;
      for (let i = 0; i < 4; i++) {
        const y = pad.top + ((h - pad.top - pad.bottom) / 3) * i;
        ctx.beginPath();
        ctx.moveTo(pad.left, y);
        ctx.lineTo(w - pad.right, y);
        ctx.stroke();
      }

      const coords = points.map((p, i) => {
        const x = pad.left + xStep * i;
        const y = pad.top + (1 - ((p.y - minY) / ySpan)) * (h - pad.top - pad.bottom);
        return { x, y };
      });

      const grad = ctx.createLinearGradient(0, pad.top, 0, h - pad.bottom);
      grad.addColorStop(0, "rgba(32,215,255,0.28)");
      grad.addColorStop(1, "rgba(32,215,255,0)");
      ctx.beginPath();
      coords.forEach((p, i) => i === 0 ? ctx.moveTo(p.x, p.y) : ctx.lineTo(p.x, p.y));
      ctx.lineTo(coords[coords.length - 1].x, h - pad.bottom);
      ctx.lineTo(coords[0].x, h - pad.bottom);
      ctx.closePath();
      ctx.fillStyle = grad;
      ctx.fill();

      ctx.beginPath();
      coords.forEach((p, i) => i === 0 ? ctx.moveTo(p.x, p.y) : ctx.lineTo(p.x, p.y));
      ctx.strokeStyle = "#20d7ff";
      ctx.lineWidth = 3;
      ctx.stroke();

      coords.forEach(p => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, 5, 0, Math.PI * 2);
        ctx.fillStyle = "#20d7ff";
        ctx.fill();
      });
    }

    function renderSegmentButtons() {
      document.querySelectorAll(".seg-btn").forEach(btn => {
        btn.classList.toggle("active", btn.dataset.view === state.currentView);
      });
    }

    function renderView() {
      if (state.currentView === "workout") renderWorkoutView();
      if (state.currentView === "history") renderHistoryView();
      if (state.currentView === "progress") renderProgressView();
    }

    function renderApp() {
      renderDays();
      renderTopTimer();
      renderMotivator();
      renderSegmentButtons();
      renderView();
    }

    document.getElementById("stopBtn").addEventListener("click", pauseTimer);
    document.getElementById("resumeBtn").addEventListener("click", resumeTimer);
    document.getElementById("resetBtn").addEventListener("click", resetTimer);
    document.querySelectorAll(".seg-btn").forEach(btn => {
      btn.addEventListener("click", () => {
        state.currentView = btn.dataset.view;
        saveState();
        renderApp();
      });
    });

    if (state.timer.running) state.timer.lastTick = Date.now();
    ensureTimerLoop();
    startMotivatorLoop();
    renderApp();
  </script>
</body>
</html>
