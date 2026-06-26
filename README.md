# gabrielluimeme.github.io
The final answer to the war beetwen men and women
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Life Path Dashboard</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
      background: #f5f4f0;
      color: #1a1a18;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 2rem 1rem;
    }

    .card {
      background: #fff;
      border-radius: 16px;
      border: 0.5px solid #d3d1c7;
      padding: 2rem 2rem 2.5rem;
      max-width: 680px;
      width: 100%;
    }

    h1 {
      font-size: 18px;
      font-weight: 500;
      color: #1a1a18;
      margin-bottom: 0.25rem;
    }

    .subtitle {
      font-size: 13px;
      color: #888780;
      margin-bottom: 2rem;
    }

    .slider-labels {
      display: flex;
      justify-content: space-between;
      margin-bottom: 0.5rem;
    }

    .slider-label {
      font-size: 13px;
      font-weight: 500;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .label-left { color: #c87941; }
    .label-right { color: #3b7dd8; }

    input[type=range] {
      width: 100%;
      height: 6px;
      appearance: none;
      background: linear-gradient(to right, #c87941 0%, #3b7dd8 100%);
      border-radius: 3px;
      outline: none;
      cursor: pointer;
    }

    input[type=range]::-webkit-slider-thumb {
      appearance: none;
      width: 22px;
      height: 22px;
      border-radius: 50%;
      background: #fff;
      border: 2px solid #888780;
      box-shadow: 0 1px 4px rgba(0,0,0,0.15);
      cursor: grab;
      transition: border-color 0.15s;
    }

    input[type=range]::-webkit-slider-thumb:hover {
      border-color: #1a1a18;
    }

    input[type=range]::-moz-range-thumb {
      width: 22px;
      height: 22px;
      border-radius: 50%;
      background: #fff;
      border: 2px solid #888780;
      cursor: grab;
    }

    .pos-label {
      text-align: center;
      font-size: 13px;
      color: #888780;
      margin-top: 8px;
    }

    .section-title {
      font-size: 11px;
      font-weight: 500;
      letter-spacing: 0.07em;
      text-transform: uppercase;
      color: #b4b2a9;
      margin: 1.75rem 0 0.75rem;
    }

    .gauges {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 12px;
    }

    .gauge-card {
      background: #f5f4f0;
      border: 0.5px solid #d3d1c7;
      border-radius: 12px;
      padding: 1rem 1.25rem;
    }

    .gauge-header {
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 10px;
    }

    .gauge-icon {
      font-size: 18px;
      color: #888780;
    }

    .gauge-label {
      font-size: 13px;
      font-weight: 500;
      color: #1a1a18;
    }

    .gauge-bar-bg {
      height: 8px;
      background: #d3d1c7;
      border-radius: 4px;
      overflow: hidden;
    }

    .gauge-bar {
      height: 100%;
      border-radius: 4px;
      transition: width 0.3s ease, background 0.3s ease;
    }

    .gauge-values {
      display: flex;
      justify-content: space-between;
      margin-top: 6px;
    }

    .gauge-val {
      font-size: 11px;
      color: #b4b2a9;
      transition: color 0.2s, font-weight 0.2s;
    }

    .gauge-val.active {
      font-weight: 500;
      color: #1a1a18;
    }

    .summary {
      background: #f5f4f0;
      border: 0.5px solid #d3d1c7;
      border-radius: 12px;
      padding: 1rem 1.25rem;
      margin-top: 1.5rem;
    }

    .summary-title {
      font-size: 11px;
      font-weight: 500;
      letter-spacing: 0.07em;
      text-transform: uppercase;
      color: #b4b2a9;
      margin-bottom: 8px;
    }

    .summary-text {
      font-size: 14px;
      color: #1a1a18;
      line-height: 1.65;
    }

    @media (max-width: 480px) {
      .card { padding: 1.5rem 1.25rem 2rem; }
      .gauges { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<div class="card">
  <h1>Life path dashboard</h1>
  <p class="subtitle">Move the slider to explore the trade-offs between each lifestyle.</p>

  <div class="slider-labels">
    <span class="slider-label label-left">
      <i class="ti ti-home" aria-hidden="true"></i> Stay-at-home
    </span>
    <span class="slider-label label-right">
      Working woman <i class="ti ti-briefcase" aria-hidden="true"></i>
    </span>
  </div>

  <input type="range" id="main-slider" min="0" max="100" value="50" step="1" aria-label="Life path slider" />
  <p class="pos-label" id="pos-label">Balanced — 50/50</p>

  <p class="section-title">Lifestyle metrics</p>
  <div class="gauges" id="gauges"></div>

  <div class="summary">
    <p class="summary-title">Profile at a glance</p>
    <p class="summary-text" id="summary-text"></p>
  </div>
</div>

<script>
  const metrics = [
    {
      id: "income",
      label: "Monthly income",
      icon: "ti-coin",
      leftLabel: "Lower",
      rightLabel: "Higher",
      leftColor: "#c87941",
      rightColor: "#3b7dd8",
      direction: "right"
    },
    {
      id: "freetime",
      label: "Free time",
      icon: "ti-clock",
      leftLabel: "More",
      rightLabel: "Less",
      leftColor: "#3b7dd8",
      rightColor: "#c87941",
      direction: "left"
    },
    {
      id: "chores",
      label: "Household tasks",
      icon: "ti-tools-kitchen-2",
      leftLabel: "Full load (100%)",
      rightLabel: "Half load (50%)",
      leftColor: "#c87941",
      rightColor: "#3b7dd8",
      direction: "left"
    },
    {
      id: "spouse",
      label: "Time with spouse",
      icon: "ti-heart",
      leftLabel: "More",
      rightLabel: "Less",
      leftColor: "#3b7dd8",
      rightColor: "#c87941",
      direction: "left"
    },
    {
      id: "work",
      label: "Work demands",
      icon: "ti-chart-line",
      leftLabel: "None",
      rightLabel: "High",
      leftColor: "#3b9441",
      rightColor: "#c87941",
      direction: "right"
    },
    {
      id: "independence",
      label: "Financial independence",
      icon: "ti-shield-check",
      leftLabel: "Lower",
      rightLabel: "Higher",
      leftColor: "#c87941",
      rightColor: "#3b7dd8",
      direction: "right"
    }
  ];

  function buildGauges() {
    const container = document.getElementById("gauges");
    container.innerHTML = metrics.map(m => `
      <div class="gauge-card">
        <div class="gauge-header">
          <i class="ti ${m.icon} gauge-icon" aria-hidden="true"></i>
          <span class="gauge-label">${m.label}</span>
        </div>
        <div class="gauge-bar-bg">
          <div class="gauge-bar" id="bar-${m.id}" style="background: ${m.leftColor}; width: 50%;"></div>
        </div>
        <div class="gauge-values">
          <span class="gauge-val active" id="val-left-${m.id}">${m.leftLabel}</span>
          <span class="gauge-val" id="val-right-${m.id}">${m.rightLabel}</span>
        </div>
      </div>
    `).join("");
  }

  function getSummary(v) {
    if (v <= 15) return "A life centered on home and family — full domestic responsibility, deep involvement with your spouse, and more personal time, with a lower individual income.";
    if (v <= 35) return "Leaning toward the home, with perhaps some part-time activity. Low work stress, high family presence, but limited financial independence.";
    if (v <= 65) return "A balanced path — some professional activity alongside significant home responsibilities. Trade-offs on both sides.";
    if (v <= 85) return "Career-focused, with home responsibilities shared or reduced. Higher income and independence, but less free time and domestic presence.";
    return "Fully career-oriented — maximum income and independence, minimal household duties, but the least free time and domestic involvement.";
  }

  function update(v) {
    document.getElementById("pos-label").textContent =
      v < 20 ? "Stay-at-home — strong lean" :
      v < 40 ? "Stay-at-home — moderate lean" :
      v <= 60 ? `Balanced — ${100 - v}/${v}` :
      v < 80 ? "Working — moderate lean" : "Working — strong lean";

    metrics.forEach(m => {
      const bar = document.getElementById(`bar-${m.id}`);
      const valL = document.getElementById(`val-left-${m.id}`);
      const valR = document.getElementById(`val-right-${m.id}`);

      let pct = m.direction === "right" ? v : 100 - v;
      bar.style.width = Math.max(4, pct) + "%";
      bar.style.background = v < 50 ? m.leftColor : m.rightColor;

      valL.classList.toggle("active", v <= 50);
      valR.classList.toggle("active", v > 50);
    });

    document.getElementById("summary-text").textContent = getSummary(v);
  }

  buildGauges();
  const slider = document.getElementById("main-slider");
  slider.addEventListener("input", () => update(parseInt(slider.value)));
  update(50);
</script>

</body>
</html>
