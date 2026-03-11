<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta
    name="viewport"
    content="width=device-width, initial-scale=1, viewport-fit=cover, user-scalable=no"
  />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="theme-color" content="#f3c969" />
  <link rel="apple-touch-icon" href="icon-180.png" />
  <title>🍺🍹🥃 Counter Deluxe</title>

  <style>
    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }

    :root {
      --bg1: #f7e7a9;
      --bg2: #f3c969;
      --card: rgba(255, 255, 255, 0.95);
      --text: #2a2a2a;
      --accent: #8b5a00;
      --danger: #8b0000;
      --warning: #b35c00;
      --muted: #6b6b6b;
      --shadow: 0 14px 35px rgba(0, 0, 0, 0.18);
      --radius: 24px;
    }

    html {
      height: 100%;
      -webkit-text-size-adjust: 100%;
    }

    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
      background: linear-gradient(180deg, var(--bg1), var(--bg2));
      min-height: 100vh;
      color: var(--text);
      padding: 14px;
      overflow-x: hidden;
      -webkit-text-size-adjust: 100%;
    }

    .app {
      width: 100%;
      max-width: 430px;
      margin: 0 auto;
      position: relative;
    }

    .title {
      text-align: center;
      margin: 6px 0 14px;
      font-size: 27px;
      color: #5a3b00;
      line-height: 1.2;
    }

    .panel {
      background: var(--card);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 14px;
      margin-bottom: 14px;
    }

    .totals {
      display: grid;
      grid-template-columns: 1fr;
      gap: 10px;
    }

    @media (min-width: 390px) {
      .totals {
        grid-template-columns: 1fr 1fr;
      }
    }

    .total-box {
      background: #fff7df;
      border: 2px solid #f0d17a;
      border-radius: 18px;
      padding: 12px;
      text-align: center;
    }

    .total-label {
      font-size: 13px;
      color: #7a5a00;
      margin-bottom: 4px;
    }

    .total-value {
      font-size: 22px;
      font-weight: 800;
      word-break: break-word;
    }

    .date-line {
      margin-top: 10px;
      text-align: center;
      font-size: 13px;
      color: var(--muted);
    }

    .card-wrap {
      position: relative;
      min-height: 1420px;
      overflow: visible;
      touch-action: pan-y;
    }

    .profile-card {
      position: absolute;
      inset: 0;
      background: linear-gradient(180deg, #fffef8, #fff6da);
      border-radius: 26px;
      border: 2px solid #f1d998;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,0.6);
      padding: 16px 12px 14px;
      text-align: center;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      will-change: transform, opacity;
      transition: transform 0.28s ease, opacity 0.28s ease;
    }

    .profile-name {
      font-size: 30px;
      font-weight: 800;
      color: #4a2f00;
      margin-top: 2px;
      margin-bottom: 8px;
    }

    .profile-meta {
      font-size: 13px;
      color: #7a5a00;
      margin-bottom: 12px;
      font-weight: 700;
    }

    .drink-section {
      margin-bottom: 12px;
      background: rgba(255,255,255,0.55);
      border: 1px solid #ecd28f;
      border-radius: 18px;
      padding: 12px;
    }

    .drink-title {
      font-size: 18px;
      font-weight: 800;
      color: #5a3b00;
      margin-bottom: 10px;
    }

    .counter-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 10px;
    }

    .mini-box {
      background: rgba(255,255,255,0.85);
      border-radius: 16px;
      padding: 10px;
      border: 1px solid #edd38f;
    }

    .mini-label {
      font-size: 12px;
      color: #7a5a00;
      margin-bottom: 4px;
    }

    .mini-value {
      font-size: 25px;
      font-weight: 800;
      word-break: break-word;
    }

    .action-row {
      display: flex;
      gap: 8px;
      justify-content: center;
      flex-wrap: wrap;
    }

    button.drink-btn {
      border: none;
      border-radius: 16px;
      padding: 10px 12px;
      font-size: 14px;
      cursor: pointer;
      font-weight: 800;
      background: #f2e0a3;
      color: #5a3b00;
      width: calc(50% - 6px);
      min-width: 0;
    }

    button.drink-btn:active {
      transform: scale(0.97);
    }

    .gauge-wrap {
      background: rgba(255,255,255,0.55);
      border: 1px solid #ecd28f;
      border-radius: 18px;
      padding: 12px;
      margin-bottom: 12px;
    }

    .gauge-title {
      font-size: 18px;
      font-weight: 800;
      color: #5a3b00;
      margin-bottom: 6px;
    }

    .gauge-subtitle {
      font-size: 12px;
      color: #8a6a15;
      margin-bottom: 8px;
      line-height: 1.35;
    }

    .gauge {
      position: relative;
      width: 100%;
      max-width: 250px;
      height: 145px;
      margin: 0 auto 6px;
    }

    .gauge-svg {
      width: 100%;
      height: 100%;
      display: block;
    }

    .gauge-needle {
      transform-origin: 50% 85%;
      transition: transform 0.35s ease;
    }

    .gauge-value {
      position: absolute;
      left: 50%;
      bottom: 16px;
      transform: translateX(-50%);
      font-size: 28px;
      font-weight: 900;
      color: #4a2f00;
      line-height: 1;
    }

    .gauge-unit {
      font-size: 13px;
      color: #7a5a00;
      margin-top: 2px;
      font-weight: 700;
    }

    .gauge-scale {
      display: flex;
      justify-content: space-between;
      font-size: 11px;
      color: #8a6a15;
      max-width: 250px;
      margin: 0 auto;
      padding: 0 4px;
    }

    .gauge-extra {
      margin-top: 10px;
      font-size: 13px;
      color: #6b6b6b;
      line-height: 1.45;
      text-align: center;
    }

    .metabolism-box {
      margin-top: 10px;
      background: rgba(255,255,255,0.85);
      border-radius: 14px;
      border: 1px solid #edd38f;
      padding: 10px;
      font-size: 13px;
      line-height: 1.45;
      color: #6b6b6b;
    }

    .status {
      min-height: 40px;
      font-size: 13px;
      line-height: 1.35;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 0 6px;
      color: #8a5b00;
      font-weight: 700;
    }

    .swipe-hint {
      font-size: 12px;
      color: var(--muted);
      margin-top: 4px;
      text-align: center;
      line-height: 1.3;
    }

    .nav-row,
    .button-row {
      display: flex;
      gap: 8px;
      justify-content: center;
      flex-wrap: wrap;
      margin-top: 12px;
    }

    button.control,
    button.nav {
      border: none;
      border-radius: 14px;
      padding: 10px 12px;
      font-size: 14px;
      cursor: pointer;
      font-weight: 700;
    }

    button.nav {
      background: #f2e0a3;
      color: #5a3b00;
      width: calc(50% - 6px);
      min-width: 0;
    }

    .finish-btn {
      background: var(--warning);
      color: white;
      flex: 1 1 140px;
      min-width: 0;
    }

    .reset-btn {
      background: var(--danger);
      color: white;
      flex: 1 1 140px;
      min-width: 0;
    }

    .dots {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin-top: 14px;
    }

    .dot {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      background: #d1c7a8;
      transition: transform 0.22s ease, background 0.22s ease;
    }

    .dot.active {
      background: var(--accent);
      transform: scale(1.25);
    }

    .section-title {
      font-size: 18px;
      font-weight: 800;
      margin-bottom: 10px;
      color: #5a3b00;
    }

    .leaderboard-list,
    .history-list {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .leaderboard-item,
    .history-item {
      background: #fff8e6;
      border: 1px solid #ecd28f;
      border-radius: 16px;
      padding: 10px 12px;
    }

    .leaderboard-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
      font-weight: 700;
      flex-wrap: wrap;
    }

    .rank-name {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .rank-badge {
      width: 28px;
      height: 28px;
      border-radius: 999px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      background: #f3d27f;
      color: #5a3b00;
      font-size: 14px;
      font-weight: 800;
      flex-shrink: 0;
    }

    .leaderboard-sub {
      margin-top: 6px;
      font-size: 13px;
      color: var(--muted);
      line-height: 1.45;
    }

    .history-date {
      font-weight: 800;
      margin-bottom: 4px;
      color: #5a3b00;
    }

    .history-total {
      font-size: 14px;
      margin-bottom: 6px;
      line-height: 1.5;
    }

    .history-breakdown {
      font-size: 13px;
      color: var(--muted);
      line-height: 1.5;
    }

    .empty {
      text-align: center;
      color: var(--muted);
      font-size: 14px;
      padding: 8px 0;
    }

    canvas#confetti {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 999;
    }

    @media (max-width: 430px) {
      .title {
        font-size: 24px;
      }

      .profile-name {
        font-size: 26px;
      }

      .drink-title,
      .gauge-title {
        font-size: 17px;
      }

      .mini-value {
        font-size: 23px;
      }

      .total-value {
        font-size: 20px;
      }

      .card-wrap {
        min-height: 1460px;
      }
    }
  </style>
</head>
<body>
  <canvas id="confetti"></canvas>

  <div class="app">
    <h1 class="title">🍺🍹🥃 Counter Deluxe</h1>

    <div class="panel">
      <div class="totals">
        <div class="total-box">
          <div class="total-label">пиво gesamt / heute</div>
          <div id="beerTotals" class="total-value">0 / 0</div>
        </div>
        <div class="total-box">
          <div class="total-label">Drinks gesamt / heute</div>
          <div id="drinkTotals" class="total-value">0 / 0</div>
        </div>
        <div class="total-box">
          <div class="total-label">стопки gesamt / heute</div>
          <div id="shotTotals" class="total-value">0 / 0</div>
        </div>
        <div class="total-box">
          <div class="total-label">Liter gesamt / heute</div>
          <div id="alcoholTotals" class="total-value">0,00 L / 0,00 L</div>
        </div>
        <div class="total-box">
          <div class="total-label">Reiner Alkohol gesamt / heute</div>
          <div id="pureAlcoholTotals" class="total-value">0,00 L / 0,00 L</div>
        </div>
      </div>
      <div id="dateLine" class="date-line"></div>
    </div>

    <div class="panel">
      <div id="cardWrap" class="card-wrap">
        <div id="profileCard" class="profile-card">
          <div>
            <div id="profileName" class="profile-name">Dr. Alex</div>
            <div id="profileMeta" class="profile-meta">95 kg · 186 cm</div>

            <div class="gauge-wrap">
              <div class="gauge-title">🚗 Promille-Tacho</div>
              <div class="gauge-subtitle">
                Schätzung mit Gewicht, Größe, Zeitstempeln und laufendem Alkoholabbau.
              </div>

              <div class="gauge">
                <svg class="gauge-svg" viewBox="0 0 220 140" aria-hidden="true">
                  <path
                    d="M20 120 A90 90 0 0 1 200 120"
                    fill="none"
                    stroke="#f0d17a"
                    stroke-width="18"
                    stroke-linecap="round"
                  ></path>

                  <path
                    d="M20 120 A90 90 0 0 1 80 42"
                    fill="none"
                    stroke="#7bc96f"
                    stroke-width="18"
                    stroke-linecap="round"
                  ></path>
                  <path
                    d="M80 42 A90 90 0 0 1 140 42"
                    fill="none"
                    stroke="#f2c94c"
                    stroke-width="18"
                    stroke-linecap="round"
                  ></path>
                  <path
                    d="M140 42 A90 90 0 0 1 176 70"
                    fill="none"
                    stroke="#f2994a"
                    stroke-width="18"
                    stroke-linecap="round"
                  ></path>
                  <path
                    d="M176 70 A90 90 0 0 1 200 120"
                    fill="none"
                    stroke="#eb5757"
                    stroke-width="18"
                    stroke-linecap="round"
                  ></path>

                  <line
                    id="gaugeNeedle"
                    class="gauge-needle"
                    x1="110"
                    y1="120"
                    x2="110"
                    y2="38"
                    stroke="#4a2f00"
                    stroke-width="6"
                    stroke-linecap="round"
                  ></line>
                  <circle cx="110" cy="120" r="10" fill="#4a2f00"></circle>
                </svg>

                <div id="gaugeValue" class="gauge-value">0,00
                  <div class="gauge-unit">‰</div>
                </div>
              </div>

              <div class="gauge-scale">
                <span>0,0</span>
                <span>0,5</span>
                <span>1,0</span>
                <span>1,5</span>
                <span>2,0+</span>
              </div>

              <div id="gaugeExtra" class="gauge-extra">
                Aktiv: 0,00 L reiner Alkohol
              </div>

              <div id="metabolismBox" class="metabolism-box">
                Abbau läuft...
              </div>
            </div>

            <div class="drink-section">
              <div class="drink-title">🍺 пиво</div>
              <div class="counter-grid">
                <div class="mini-box">
                  <div class="mini-label">Gesamt</div>
                  <div id="profileBeerAllTime" class="mini-value">0</div>
                </div>
                <div class="mini-box">
                  <div class="mini-label">Heute</div>
                  <div id="profileBeerToday" class="mini-value">0</div>
                </div>
              </div>
              <div class="action-row">
                <button id="addBeerBtn" class="drink-btn">+1 пиво</button>
                <button id="removeBeerBtn" class="drink-btn">-1 пиво</button>
              </div>
            </div>

            <div class="drink-section">
              <div class="drink-title">🍹 Drinks</div>
              <div class="counter-grid">
                <div class="mini-box">
                  <div class="mini-label">Gesamt</div>
                  <div id="profileDrinksAllTime" class="mini-value">0</div>
                </div>
                <div class="mini-box">
                  <div class="mini-label">Heute</div>
                  <div id="profileDrinksToday" class="mini-value">0</div>
                </div>
              </div>
              <div class="action-row">
                <button id="addDrinkBtn" class="drink-btn">+1 Drink</button>
                <button id="removeDrinkBtn" class="drink-btn">-1 Drink</button>
              </div>
            </div>

            <div class="drink-section">
              <div class="drink-title">🥃 стопки</div>
              <div class="counter-grid">
                <div class="mini-box">
                  <div class="mini-label">Gesamt</div>
                  <div id="profileShotsAllTime" class="mini-value">0</div>
                </div>
                <div class="mini-box">
                  <div class="mini-label">Heute</div>
                  <div id="profileShotsToday" class="mini-value">0</div>
                </div>
              </div>
              <div class="action-row">
                <button id="addShotBtn" class="drink-btn">+1 стопка</button>
                <button id="removeShotBtn" class="drink-btn">-1 стопка</button>
              </div>
            </div>

            <div class="drink-section">
              <div class="drink-title">📏 Liter gesamt</div>
              <div class="counter-grid">
                <div class="mini-box">
                  <div class="mini-label">Gesamt</div>
                  <div id="profileAlcoholAllTime" class="mini-value">0,00 L</div>
                </div>
                <div class="mini-box">
                  <div class="mini-label">Heute</div>
                  <div id="profileAlcoholToday" class="mini-value">0,00 L</div>
                </div>
              </div>
            </div>

            <div class="drink-section">
              <div class="drink-title">🧪 Reiner Alkohol</div>
              <div class="counter-grid">
                <div class="mini-box">
                  <div class="mini-label">Gesamt</div>
                  <div id="profilePureAlcoholAllTime" class="mini-value">0,00 L</div>
                </div>
                <div class="mini-box">
                  <div class="mini-label">Heute brutto</div>
                  <div id="profilePureAlcoholToday" class="mini-value">0,00 L</div>
                </div>
              </div>
            </div>
          </div>

          <div>
            <div id="statusText" class="status"></div>
            <div class="swipe-hint">Nach links/rechts swipen oder Buttons nutzen</div>
          </div>
        </div>
      </div>

      <div id="dots" class="dots"></div>

      <div class="nav-row">
        <button id="prevBtn" class="nav">← Zurück</button>
        <button id="nextBtn" class="nav">Weiter →</button>
      </div>

      <div class="button-row">
        <button id="finishEveningBtn" class="control finish-btn">Abend abschließen</button>
        <button id="resetAllBtn" class="control reset-btn">Alles reset</button>
      </div>
    </div>

    <div class="panel">
      <div class="section-title">🏆 Leaderboard</div>
      <div id="leaderboard" class="leaderboard-list"></div>
    </div>

    <div class="panel">
      <div class="section-title">📊 Statistik pro Abend</div>
      <div id="historyList" class="history-list"></div>
    </div>
  </div>

  <script>
    const profiles = ["Dr. Alex", "Agurchik", "Micha", "leon4ikki", "Eric"];
    const STORAGE_KEY = "bierCounterDeluxeV6";

    const NAME_MIGRATION = {
      "Alex": "Dr. Alex",
      "Arthur": "Agurchik",
      "Leon": "leon4ikki",
      "Micha": "Micha",
      "Eric": "Eric"
    };

    const PEOPLE = {
      "Dr. Alex": { weight: 95, height: 186 },
      "Agurchik": { weight: 105, height: 190 },
      "Micha": { weight: 78, height: 186 },
      "leon4ikki": { weight: 85, height: 180 },
      "Eric": { weight: 87, height: 186 }
    };

    const BEER_LITERS = 0.5;
    const DRINK_LITERS = 0.33;
    const SHOT_LITERS = 0.02;

    const BEER_ALC = 0.052;
    const SHOT_ALC = 0.40;
    const DRINK_ALC_MIN = 0.10;
    const DRINK_ALC_MAX = 0.30;

    const ALCOHOL_DENSITY = 0.789;
    const ELIMINATION_PROMILLE_PER_HOUR = 0.15;

    function defaultCounts() {
      return Object.fromEntries(
        profiles.map(name => [
          name,
          {
            beer: 0,
            drinks: 0,
            shots: 0,
            drinkAlcoholValues: []
          }
        ])
      );
    }

    function defaultEvents() {
      return Object.fromEntries(
        profiles.map(name => [name, []])
      );
    }

    function getTodayKey() {
      const now = new Date();
      const year = now.getFullYear();
      const month = String(now.getMonth() + 1).padStart(2, "0");
      const day = String(now.getDate()).padStart(2, "0");
      return `${year}-${month}-${day}`;
    }

    function formatDateGerman(dateKey) {
      const [y, m, d] = dateKey.split("-");
      return `${d}.${m}.${y}`;
    }

    function getGermanWeekday() {
      return new Date().toLocaleDateString("de-DE", { weekday: "long" });
    }

    function litersForCounts(beerCount, drinkCount, shotCount) {
      return (beerCount * BEER_LITERS) + (drinkCount * DRINK_LITERS) + (shotCount * SHOT_LITERS);
    }

    function pureAlcoholForEntry(entry) {
      const beerAlcohol = entry.beer * BEER_LITERS * BEER_ALC;
      const shotAlcohol = entry.shots * SHOT_LITERS * SHOT_ALC;
      const drinkAlcohol = (entry.drinkAlcoholValues || []).reduce((sum, value) => sum + value, 0);
      return beerAlcohol + shotAlcohol + drinkAlcohol;
    }

    function formatLiters(value) {
      return `${value.toFixed(2).replace(".", ",")} L`;
    }

    function formatPromille(value) {
      return value.toFixed(2).replace(".", ",");
    }

    function formatTime(ts) {
      return new Date(ts).toLocaleTimeString("de-DE", {
        hour: "2-digit",
        minute: "2-digit"
      });
    }

    function formatMinutes(mins) {
      if (!isFinite(mins) || mins <= 0) return "0 Min.";
      if (mins < 60) return `${Math.ceil(mins)} Min.`;
      const hours = Math.floor(mins / 60);
      const rest = Math.ceil(mins % 60);
      return rest === 60 ? `${hours + 1} Std.` : `${hours} Std. ${rest} Min.`;
    }

    function randomDrinkAlcoholLiters() {
      const percent = DRINK_ALC_MIN + Math.random() * (DRINK_ALC_MAX - DRINK_ALC_MIN);
      return DRINK_LITERS * percent;
    }

    function safeLoad() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        if (raw) return JSON.parse(raw);

        const oldRaw = localStorage.getItem("bierCounterDeluxeV5");
        if (oldRaw) return JSON.parse(oldRaw);

        return null;
      } catch {
        return null;
      }
    }

    function getFreshState() {
      return {
        currentIndex: 0,
        allTime: defaultCounts(),
        daily: {
          dateKey: getTodayKey(),
          counts: defaultCounts(),
          events: defaultEvents()
        },
        history: []
      };
    }

    function renameKeys(obj) {
      const out = {};
      for (const key in obj || {}) {
        const newKey = NAME_MIGRATION[key] || key;
        out[newKey] = obj[key];
      }
      return out;
    }

    function migrateStateNames(rawState) {
      if (!rawState) return null;

      if (rawState.allTime) rawState.allTime = renameKeys(rawState.allTime);

      if (rawState.daily?.counts) {
        rawState.daily.counts = renameKeys(rawState.daily.counts);
      }

      if (rawState.daily?.events) {
        rawState.daily.events = renameKeys(rawState.daily.events);
      }

      if (Array.isArray(rawState.history)) {
        rawState.history = rawState.history.map(entry => {
          if (entry.counts) entry.counts = renameKeys(entry.counts);
          if (entry.events) entry.events = renameKeys(entry.events);
          return entry;
        });
      }

      return rawState;
    }

    let state = migrateStateNames(safeLoad()) || getFreshState();

    if (!state.allTime) state.allTime = defaultCounts();
    if (!state.daily) {
      state.daily = {
        dateKey: getTodayKey(),
        counts: defaultCounts(),
        events: defaultEvents()
      };
    }
    if (!state.daily.counts) state.daily.counts = defaultCounts();
    if (!state.daily.events) state.daily.events = defaultEvents();
    if (!Array.isArray(state.history)) state.history = [];
    if (typeof state.currentIndex !== "number") state.currentIndex = 0;

    for (const name of profiles) {
      if (!state.allTime[name] || typeof state.allTime[name] !== "object") {
        state.allTime[name] = { beer: 0, drinks: 0, shots: 0, drinkAlcoholValues: [] };
      }
      if (!state.daily.counts[name] || typeof state.daily.counts[name] !== "object") {
        state.daily.counts[name] = { beer: 0, drinks: 0, shots: 0, drinkAlcoholValues: [] };
      }
      if (!Array.isArray(state.daily.events[name])) {
        state.daily.events[name] = [];
      }

      if (typeof state.allTime[name].beer !== "number") state.allTime[name].beer = 0;
      if (typeof state.allTime[name].drinks !== "number") state.allTime[name].drinks = 0;
      if (typeof state.allTime[name].shots !== "number") state.allTime[name].shots = 0;
      if (!Array.isArray(state.allTime[name].drinkAlcoholValues)) state.allTime[name].drinkAlcoholValues = [];

      if (typeof state.daily.counts[name].beer !== "number") state.daily.counts[name].beer = 0;
      if (typeof state.daily.counts[name].drinks !== "number") state.daily.counts[name].drinks = 0;
      if (typeof state.daily.counts[name].shots !== "number") state.daily.counts[name].shots = 0;
      if (!Array.isArray(state.daily.counts[name].drinkAlcoholValues)) state.daily.counts[name].drinkAlcoholValues = [];

      while (state.allTime[name].drinkAlcoholValues.length < state.allTime[name].drinks) {
        state.allTime[name].drinkAlcoholValues.push(DRINK_LITERS * 0.20);
      }
      while (state.daily.counts[name].drinkAlcoholValues.length < state.daily.counts[name].drinks) {
        state.daily.counts[name].drinkAlcoholValues.push(DRINK_LITERS * 0.20);
      }

      if (state.allTime[name].drinkAlcoholValues.length > state.allTime[name].drinks) {
        state.allTime[name].drinkAlcoholValues = state.allTime[name].drinkAlcoholValues.slice(0, state.allTime[name].drinks);
      }
      if (state.daily.counts[name].drinkAlcoholValues.length > state.daily.counts[name].drinks) {
        state.daily.counts[name].drinkAlcoholValues = state.daily.counts[name].drinkAlcoholValues.slice(0, state.daily.counts[name].drinks);
      }

      for (const evt of state.daily.events[name]) {
        if (!evt.timestamp) evt.timestamp = Date.now();
      }
    }

    if (state.currentIndex < 0 || state.currentIndex >= profiles.length) {
      state.currentIndex = 0;
    }

    function getDailyTotal(type) {
      return profiles.reduce((sum, name) => sum + state.daily.counts[name][type], 0);
    }

    function getGrandTotal(type) {
      return profiles.reduce((sum, name) => sum + state.allTime[name][type], 0);
    }

    function getCombinedAllTimeForProfile(name) {
      return state.allTime[name].beer + state.allTime[name].drinks + state.allTime[name].shots;
    }

    function getDailyAlcoholLiters() {
      return profiles.reduce((sum, name) => {
        return sum + litersForCounts(
          state.daily.counts[name].beer,
          state.daily.counts[name].drinks,
          state.daily.counts[name].shots
        );
      }, 0);
    }

    function getGrandAlcoholLiters() {
      return profiles.reduce((sum, name) => {
        return sum + litersForCounts(
          state.allTime[name].beer,
          state.allTime[name].drinks,
          state.allTime[name].shots
        );
      }, 0);
    }

    function getProfileAlcoholToday(name) {
      return litersForCounts(
        state.daily.counts[name].beer,
        state.daily.counts[name].drinks,
        state.daily.counts[name].shots
      );
    }

    function getProfileAlcoholAllTime(name) {
      return litersForCounts(
        state.allTime[name].beer,
        state.allTime[name].drinks,
        state.allTime[name].shots
      );
    }

    function getProfilePureAlcoholToday(name) {
      return pureAlcoholForEntry(state.daily.counts[name]);
    }

    function getProfilePureAlcoholAllTime(name) {
      return pureAlcoholForEntry(state.allTime[name]);
    }

    function getDailyPureAlcohol() {
      return profiles.reduce((sum, name) => sum + getProfilePureAlcoholToday(name), 0);
    }

    function getGrandPureAlcohol() {
      return profiles.reduce((sum, name) => sum + getProfilePureAlcoholAllTime(name), 0);
    }

    function clamp(value, min, max) {
      return Math.min(max, Math.max(min, value));
    }

    function estimateDistributionFactor(weightKg, heightCm) {
      const heightM = heightCm / 100;
      const bmi = weightKg / (heightM * heightM);

      let factor = 0.68;
      factor -= Math.max(0, bmi - 25) * 0.004;
      factor += Math.max(0, heightCm - 180) * 0.001;
      factor -= Math.max(0, 175 - heightCm) * 0.001;

      return clamp(factor, 0.58, 0.73);
    }

    function getEliminationGramsPerHour(name) {
      const person = PEOPLE[name];
      const r = estimateDistributionFactor(person.weight, person.height);
      return ELIMINATION_PROMILLE_PER_HOUR * person.weight * r;
    }

    function getEventTypeLabel(type) {
      if (type === "beer") return "пиво";
      if (type === "drink") return "Drink";
      if (type === "shot") return "стопка";
      return type;
    }

    function getActiveAlcoholStats(name) {
      const events = state.daily.events[name] || [];
      const eliminationPerHour = getEliminationGramsPerHour(name);
      const now = Date.now();

      let activeGrams = 0;
      let nextZeroMinutes = 0;
      let lastDrinkTime = null;
      let activeCount = 0;

      for (const evt of events) {
        const grams = evt.pureAlcoholLiters * 1000 * ALCOHOL_DENSITY;
        const hoursPassed = Math.max(0, (now - evt.timestamp) / 3600000);
        const remainingGrams = Math.max(0, grams - (eliminationPerHour * hoursPassed));

        if (remainingGrams > 0) {
          activeGrams += remainingGrams;
          activeCount += 1;

          const hoursUntilZero = remainingGrams / eliminationPerHour;
          const minutesUntilZero = hoursUntilZero * 60;
          if (minutesUntilZero > nextZeroMinutes) nextZeroMinutes = minutesUntilZero;
        }

        if (!lastDrinkTime || evt.timestamp > lastDrinkTime) {
          lastDrinkTime = evt.timestamp;
        }
      }

      return {
        activeGrams,
        activePureAlcoholLiters: activeGrams / (1000 * ALCOHOL_DENSITY),
        timeUntilZeroMinutes: nextZeroMinutes,
        lastDrinkTime,
        activeCount
      };
    }

    function calculatePromille(name) {
      const person = PEOPLE[name];
      const active = getActiveAlcoholStats(name);
      const distributionFactor = estimateDistributionFactor(person.weight, person.height);
      const promille = active.activeGrams / (person.weight * distributionFactor);
      return Math.max(0, promille);
    }

    function gaugeRotationFromPromille(promille) {
      const maxPromille = 2.0;
      const normalized = clamp(promille / maxPromille, 0, 1);
      return -90 + (normalized * 180);
    }

    function getPromilleStatusText(promille) {
      if (promille < 0.3) return "Locker unterwegs.";
      if (promille < 0.8) return "Schon deutlich was drin.";
      if (promille < 1.3) return "Jetzt wird's ordentlich.";
      if (promille < 2.0) return "Sehr stabil unterwegs.";
      return "Komplett Endgegner-Modus.";
    }

    function archiveCurrentEvening(reason = "automatic") {
      const totalBeer = getDailyTotal("beer");
      const totalDrinks = getDailyTotal("drinks");
      const totalShots = getDailyTotal("shots");
      const totalLiters = getDailyAlcoholLiters();
      const totalPureAlcohol = getDailyPureAlcohol();
      const total = totalBeer + totalDrinks + totalShots;

      if (total <= 0) {
        state.daily = {
          dateKey: getTodayKey(),
          counts: defaultCounts(),
          events: defaultEvents()
        };
        return;
      }

      state.history.unshift({
        id: Date.now(),
        dateKey: state.daily.dateKey,
        label: `${formatDateGerman(state.daily.dateKey)} · ${reason === "manual" ? "manuell abgeschlossen" : "automatisch gespeichert"}`,
        counts: JSON.parse(JSON.stringify(state.daily.counts)),
        events: JSON.parse(JSON.stringify(state.daily.events)),
        totalBeer,
        totalDrinks,
        totalShots,
        totalLiters,
        totalPureAlcohol,
        total
      });

      state.history = state.history.slice(0, 20);

      state.daily = {
        dateKey: getTodayKey(),
        counts: defaultCounts(),
        events: defaultEvents()
      };
    }

    if (state.daily.dateKey !== getTodayKey()) {
      archiveCurrentEvening("automatic");
    }

    function saveState() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    }

    const beerTotalsEl = document.getElementById("beerTotals");
    const drinkTotalsEl = document.getElementById("drinkTotals");
    const shotTotalsEl = document.getElementById("shotTotals");
    const alcoholTotalsEl = document.getElementById("alcoholTotals");
    const pureAlcoholTotalsEl = document.getElementById("pureAlcoholTotals");
    const dateLineEl = document.getElementById("dateLine");

    const profileNameEl = document.getElementById("profileName");
    const profileMetaEl = document.getElementById("profileMeta");

    const profileBeerAllTimeEl = document.getElementById("profileBeerAllTime");
    const profileBeerTodayEl = document.getElementById("profileBeerToday");

    const profileDrinksAllTimeEl = document.getElementById("profileDrinksAllTime");
    const profileDrinksTodayEl = document.getElementById("profileDrinksToday");

    const profileShotsAllTimeEl = document.getElementById("profileShotsAllTime");
    const profileShotsTodayEl = document.getElementById("profileShotsToday");

    const profileAlcoholAllTimeEl = document.getElementById("profileAlcoholAllTime");
    const profileAlcoholTodayEl = document.getElementById("profileAlcoholToday");

    const profilePureAlcoholAllTimeEl = document.getElementById("profilePureAlcoholAllTime");
    const profilePureAlcoholTodayEl = document.getElementById("profilePureAlcoholToday");

    const gaugeNeedleEl = document.getElementById("gaugeNeedle");
    const gaugeValueEl = document.getElementById("gaugeValue");
    const gaugeExtraEl = document.getElementById("gaugeExtra");
    const metabolismBoxEl = document.getElementById("metabolismBox");

    const statusTextEl = document.getElementById("statusText");
    const dotsEl = document.getElementById("dots");
    const leaderboardEl = document.getElementById("leaderboard");
    const historyListEl = document.getElementById("historyList");

    const addBeerBtn = document.getElementById("addBeerBtn");
    const removeBeerBtn = document.getElementById("removeBeerBtn");
    const addDrinkBtn = document.getElementById("addDrinkBtn");
    const removeDrinkBtn = document.getElementById("removeDrinkBtn");
    const addShotBtn = document.getElementById("addShotBtn");
    const removeShotBtn = document.getElementById("removeShotBtn");

    const prevBtn = document.getElementById("prevBtn");
    const nextBtn = document.getElementById("nextBtn");
    const resetAllBtn = document.getElementById("resetAllBtn");
    const finishEveningBtn = document.getElementById("finishEveningBtn");
    const profileCard = document.getElementById("profileCard");
    const cardWrap = document.getElementById("cardWrap");

    function currentProfile() {
      return profiles[state.currentIndex];
    }

    function updateGauge() {
      const name = currentProfile();
      const promille = calculatePromille(name);
      const rotation = gaugeRotationFromPromille(promille);
      const activeStats = getActiveAlcoholStats(name);

      gaugeNeedleEl.style.transform = `rotate(${rotation}deg)`;
      gaugeValueEl.innerHTML = `${formatPromille(promille)}<div class="gauge-unit">‰</div>`;
      gaugeExtraEl.innerHTML = `Aktiv: ${formatLiters(activeStats.activePureAlcoholLiters)} reiner Alkohol<br>${getPromilleStatusText(promille)}`;

      const eliminationPerHour = getEliminationGramsPerHour(name);
      const eliminationLitersPerHour = eliminationPerHour / (1000 * ALCOHOL_DENSITY);

      if (activeStats.activeGrams <= 0) {
        metabolismBoxEl.innerHTML = `
          <strong>Abbau-Timer</strong><br>
          Kein aktiver Alkohol mehr im Rechner.
        `;
      } else {
        metabolismBoxEl.innerHTML = `
          <strong>Abbau-Timer</strong><br>
          Letztes Getränk: ${activeStats.lastDrinkTime ? formatTime(activeStats.lastDrinkTime) : "--:--"}<br>
          Noch aktiv im Körper: ${formatLiters(activeStats.activePureAlcoholLiters)}<br>
          Abbaugeschwindigkeit: ca. ${formatLiters(eliminationLitersPerHour)}/h<br>
          Voraussichtlich auf 0,00‰ in: ${formatMinutes(activeStats.timeUntilZeroMinutes)}
        `;
      }
    }

    function updateStatus() {
      const name = currentProfile();
      const beerToday = state.daily.counts[name].beer;
      const drinksToday = state.daily.counts[name].drinks;
      const shotsToday = state.daily.counts[name].shots;
      const litersToday = getProfileAlcoholToday(name);
      const pureToday = getProfilePureAlcoholToday(name);
      const promille = calculatePromille(name);
      const totalToday = beerToday + drinksToday + shotsToday;

      if (totalToday === 0) {
        statusTextEl.textContent = "Noch nüchtern heute.";
      } else {
        statusTextEl.textContent =
          `${name}: ${beerToday} пиво · ${drinksToday} Drinks · ${shotsToday} стопки · ${formatLiters(litersToday)} · ${formatLiters(pureToday)} brutto · ca. ${formatPromille(promille)}‰`;
      }
    }

    function renderDots() {
      dotsEl.innerHTML = "";
      profiles.forEach((_, i) => {
        const dot = document.createElement("div");
        dot.className = "dot" + (i === state.currentIndex ? " active" : "");
        dotsEl.appendChild(dot);
      });
    }

    function renderLeaderboard() {
      const sorted = [...profiles].sort((a, b) => {
        return getCombinedAllTimeForProfile(b) - getCombinedAllTimeForProfile(a) || a.localeCompare(b);
      });

      leaderboardEl.innerHTML = "";

      sorted.forEach((name, index) => {
        const item = document.createElement("div");
        item.className = "leaderboard-item";

        const icon =
          index === 0 ? "👑" :
          index === 1 ? "🥈" :
          index === 2 ? "🥉" : "🍻";

        const activeStats = getActiveAlcoholStats(name);

        item.innerHTML = `
          <div class="leaderboard-top">
            <div class="rank-name">
              <span class="rank-badge">${index + 1}</span>
              <span>${icon} ${name}</span>
            </div>
            <div>${getCombinedAllTimeForProfile(name)} gesamt</div>
          </div>
          <div class="leaderboard-sub">
            🍺 пиво: ${state.allTime[name].beer} gesamt / ${state.daily.counts[name].beer} heute<br>
            🍹 Drinks: ${state.allTime[name].drinks} gesamt / ${state.daily.counts[name].drinks} heute<br>
            🥃 стопки: ${state.allTime[name].shots} gesamt / ${state.daily.counts[name].shots} heute<br>
            📏 Liter: ${formatLiters(getProfileAlcoholAllTime(name))} gesamt / ${formatLiters(getProfileAlcoholToday(name))} heute<br>
            🧪 Reiner Alkohol: ${formatLiters(getProfilePureAlcoholAllTime(name))} gesamt / ${formatLiters(getProfilePureAlcoholToday(name))} heute<br>
            ⚡ Aktiv im Körper: ${formatLiters(activeStats.activePureAlcoholLiters)}<br>
            🚗 Promille jetzt: ca. ${formatPromille(calculatePromille(name))}‰
          </div>
        `;

        leaderboardEl.appendChild(item);
      });
    }

    function renderHistory() {
      historyListEl.innerHTML = "";

      if (!state.history.length) {
        historyListEl.innerHTML = `<div class="empty">Noch kein abgeschlossener Abend gespeichert.</div>`;
        return;
      }

      state.history.forEach(entry => {
        const item = document.createElement("div");
        item.className = "history-item";

        const breakdown = profiles
          .map(name => {
            const beer = entry.counts[name]?.beer || 0;
            const drinks = entry.counts[name]?.drinks || 0;
            const shots = entry.counts[name]?.shots || 0;
            const liters = litersForCounts(beer, drinks, shots);

            const entryPureAlcohol =
              (beer * BEER_LITERS * BEER_ALC) +
              (shots * SHOT_LITERS * SHOT_ALC) +
              ((entry.counts[name]?.drinkAlcoholValues || []).reduce((sum, value) => sum + value, 0));

            return `${name}: 🍺 ${beer} пиво · 🍹 ${drinks} Drinks · 🥃 ${shots} стопки · 📏 ${formatLiters(liters)} · 🧪 ${formatLiters(entryPureAlcohol)}`;
          })
          .join("<br>");

        item.innerHTML = `
          <div class="history-date">${entry.label}</div>
          <div class="history-total">
            Gesamt an diesem Abend: <strong>${entry.total}</strong><br>
            🍺 пиво: <strong>${entry.totalBeer}</strong> · 🍹 Drinks: <strong>${entry.totalDrinks}</strong> · 🥃 стопки: <strong>${entry.totalShots}</strong><br>
            📏 Liter: <strong>${formatLiters(entry.totalLiters || 0)}</strong><br>
            🧪 Reiner Alkohol: <strong>${formatLiters(entry.totalPureAlcohol || 0)}</strong>
          </div>
          <div class="history-breakdown">${breakdown}</div>
        `;

        historyListEl.appendChild(item);
      });
    }

    function updateUI() {
      const name = currentProfile();
      const person = PEOPLE[name];

      beerTotalsEl.textContent = `${getGrandTotal("beer")} / ${getDailyTotal("beer")}`;
      drinkTotalsEl.textContent = `${getGrandTotal("drinks")} / ${getDailyTotal("drinks")}`;
      shotTotalsEl.textContent = `${getGrandTotal("shots")} / ${getDailyTotal("shots")}`;
      alcoholTotalsEl.textContent = `${formatLiters(getGrandAlcoholLiters())} / ${formatLiters(getDailyAlcoholLiters())}`;
      pureAlcoholTotalsEl.textContent = `${formatLiters(getGrandPureAlcohol())} / ${formatLiters(getDailyPureAlcohol())}`;
      dateLineEl.textContent = `${getGermanWeekday()} · ${formatDateGerman(getTodayKey())}`;

      profileNameEl.textContent = name;
      profileMetaEl.textContent = `${person.weight} kg · ${person.height} cm`;

      profileBeerAllTimeEl.textContent = state.allTime[name].beer;
      profileBeerTodayEl.textContent = state.daily.counts[name].beer;

      profileDrinksAllTimeEl.textContent = state.allTime[name].drinks;
      profileDrinksTodayEl.textContent = state.daily.counts[name].drinks;

      profileShotsAllTimeEl.textContent = state.allTime[name].shots;
      profileShotsTodayEl.textContent = state.daily.counts[name].shots;

      profileAlcoholAllTimeEl.textContent = formatLiters(getProfileAlcoholAllTime(name));
      profileAlcoholTodayEl.textContent = formatLiters(getProfileAlcoholToday(name));

      profilePureAlcoholAllTimeEl.textContent = formatLiters(getProfilePureAlcoholAllTime(name));
      profilePureAlcoholTodayEl.textContent = formatLiters(getProfilePureAlcoholToday(name));

      updateGauge();
      updateStatus();
      renderDots();
      renderLeaderboard();
      renderHistory();
      saveState();
    }

    function setIndex(newIndex) {
      const len = profiles.length;
      state.currentIndex = (newIndex + len) % len;
      updateUI();
    }

    function nextProfile() {
      animateCardOut(-1, () => setIndex(state.currentIndex + 1));
    }

    function prevProfile() {
      animateCardOut(1, () => setIndex(state.currentIndex - 1));
    }

    function createEvent(type, pureAlcoholLiters) {
      return {
        type,
        pureAlcoholLiters,
        timestamp: Date.now()
      };
    }

    function addCount(type) {
      const name = currentProfile();

      state.allTime[name][type] += 1;
      state.daily.counts[name][type] += 1;

      if (type === "drinks") {
        const alcoholValue = randomDrinkAlcoholLiters();
        state.allTime[name].drinkAlcoholValues.push(alcoholValue);
        state.daily.counts[name].drinkAlcoholValues.push(alcoholValue);
        state.daily.events[name].push(createEvent("drink", alcoholValue));
      }

      if (type === "beer") {
        state.daily.events[name].push(createEvent("beer", BEER_LITERS * BEER_ALC));
      }

      if (type === "shots") {
        state.daily.events[name].push(createEvent("shot", SHOT_LITERS * SHOT_ALC));
      }

      updateUI();
      fireConfetti();
    }

    function removeLastEventByType(name, eventType) {
      const events = state.daily.events[name];
      for (let i = events.length - 1; i >= 0; i--) {
        if (events[i].type === eventType) {
          events.splice(i, 1);
          return true;
        }
      }
      return false;
    }

    function removeCount(type) {
      const name = currentProfile();

      if (state.daily.counts[name][type] <= 0 || state.allTime[name][type] <= 0) {
        return;
      }

      state.daily.counts[name][type] -= 1;
      state.allTime[name][type] -= 1;

      if (type === "drinks") {
        state.daily.counts[name].drinkAlcoholValues.pop();
        state.allTime[name].drinkAlcoholValues.pop();
        removeLastEventByType(name, "drink");
      }

      if (type === "beer") {
        removeLastEventByType(name, "beer");
      }

      if (type === "shots") {
        removeLastEventByType(name, "shot");
      }

      updateUI();
    }

    function finishEvening() {
      const total = getDailyTotal("beer") + getDailyTotal("drinks") + getDailyTotal("shots");

      if (total === 0) {
        alert("Für heute gibt es noch keinen Eintrag.");
        return;
      }

      archiveCurrentEvening("manual");
      updateUI();
    }

    function resetAll() {
      const ok = confirm("Wirklich alles zurücksetzen? Gesamtstände, Tagesstände und Abend-Statistik werden gelöscht.");
      if (!ok) return;
      state = getFreshState();
      updateUI();
    }

    addBeerBtn.addEventListener("click", () => addCount("beer"));
    removeBeerBtn.addEventListener("click", () => removeCount("beer"));

    addDrinkBtn.addEventListener("click", () => addCount("drinks"));
    removeDrinkBtn.addEventListener("click", () => removeCount("drinks"));

    addShotBtn.addEventListener("click", () => addCount("shots"));
    removeShotBtn.addEventListener("click", () => removeCount("shots"));

    prevBtn.addEventListener("click", prevProfile);
    nextBtn.addEventListener("click", nextProfile);
    finishEveningBtn.addEventListener("click", finishEvening);
    resetAllBtn.addEventListener("click", resetAll);

    let startX = 0;
    let currentX = 0;
    let dragging = false;

    function onTouchStart(e) {
      dragging = true;
      startX = e.touches[0].clientX;
      currentX = startX;
      profileCard.style.transition = "none";
    }

    function onTouchMove(e) {
      if (!dragging) return;
      currentX = e.touches[0].clientX;
      const deltaX = currentX - startX;
      const rotate = deltaX * 0.04;
      profileCard.style.transform = `translateX(${deltaX}px) rotate(${rotate}deg)`;
      profileCard.style.opacity = String(Math.max(0.72, 1 - Math.abs(deltaX) / 320));
    }

    function onTouchEnd() {
      if (!dragging) return;
      dragging = false;

      const deltaX = currentX - startX;
      const threshold = 80;

      profileCard.style.transition = "transform 0.28s ease, opacity 0.28s ease";

      if (deltaX <= -threshold) {
        animateCardOut(-1, () => setIndex(state.currentIndex + 1));
      } else if (deltaX >= threshold) {
        animateCardOut(1, () => setIndex(state.currentIndex - 1));
      } else {
        profileCard.style.transform = "translateX(0px) rotate(0deg)";
        profileCard.style.opacity = "1";
      }
    }

    cardWrap.addEventListener("touchstart", onTouchStart, { passive: true });
    cardWrap.addEventListener("touchmove", onTouchMove, { passive: true });
    cardWrap.addEventListener("touchend", onTouchEnd, { passive: true });

    function animateCardOut(direction, callback) {
      profileCard.style.transition = "transform 0.25s ease, opacity 0.25s ease";
      profileCard.style.transform = `translateX(${direction * 380}px) rotate(${direction * 16}deg)`;
      profileCard.style.opacity = "0";

      setTimeout(() => {
        callback();
        profileCard.style.transition = "none";
        profileCard.style.transform = `translateX(${direction * -380}px) rotate(${direction * -16}deg)`;
        profileCard.style.opacity = "0";

        requestAnimationFrame(() => {
          requestAnimationFrame(() => {
            profileCard.style.transition = "transform 0.25s ease, opacity 0.25s ease";
            profileCard.style.transform = "translateX(0px) rotate(0deg)";
            profileCard.style.opacity = "1";
          });
        });
      }, 250);
    }

    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");
    let particles = [];
    let animationFrame = null;

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    function random(min, max) {
      return Math.random() * (max - min) + min;
    }

    function fireConfetti() {
      const originX = window.innerWidth / 2;
      const originY = window.innerHeight * 0.45;
      const colors = ["#f2c94c", "#f2994a", "#eb5757", "#6fcf97", "#56ccf2", "#bb6bd9"];

      for (let i = 0; i < 45; i++) {
        particles.push({
          x: originX,
          y: originY,
          vx: random(-4.2, 4.2),
          vy: random(-8.5, -3.5),
          size: random(5, 10),
          color: colors[Math.floor(Math.random() * colors.length)],
          life: 0,
          maxLife: random(40, 65),
          rotation: random(0, Math.PI * 2),
          vr: random(-0.25, 0.25)
        });
      }

      if (!animationFrame) {
        animateConfetti();
      }
    }

    function animateConfetti() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      particles.forEach(p => {
        p.life += 1;
        p.x += p.vx;
        p.y += p.vy;
        p.vy += 0.18;
        p.rotation += p.vr;

        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate(p.rotation);
        ctx.globalAlpha = Math.max(0, 1 - p.life / p.maxLife);
        ctx.fillStyle = p.color;
        ctx.fillRect(-p.size / 2, -p.size / 2, p.size, p.size * 0.6);
        ctx.restore();
      });

      particles = particles.filter(p => p.life < p.maxLife && p.y < canvas.height + 30);

      if (particles.length > 0) {
        animationFrame = requestAnimationFrame(animateConfetti);
      } else {
        animationFrame = null;
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      }
    }

    updateUI();

    setInterval(() => {
      updateGauge();
      updateStatus();
      renderLeaderboard();
    }, 30000);
  </script>
</body>
</html>
