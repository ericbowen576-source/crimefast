<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>CrimeFast – Quick Crime Quote</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg: #050816;
      --card: #0f172a;
      --accent: #38bdf8;
      --accent-soft: rgba(56,189,248,0.12);
      --text: #e5e7eb;
      --muted: #9ca3af;
      --danger: #f97373;
      --success: #4ade80;
      --border: #1f2937;
      --radius: 10px;
      --shadow: 0 18px 45px rgba(0,0,0,0.55);
    }

    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text",
        "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      min-height: 100vh;
      background: radial-gradient(circle at top, #1f2937 0, #020617 55%);
      color: var(--text);
      display: flex;
      align-items: stretch;
      justify-content: center;
    }

    .app-shell {
      max-width: 1100px;
      width: 100%;
      margin: 24px;
      display: grid;
      grid-template-columns: minmax(0, 3fr) minmax(0, 2fr);
      gap: 20px;
    }

    @media (max-width: 900px) {
      .app-shell {
        grid-template-columns: 1fr;
      }
    }

    .panel {
      background: linear-gradient(145deg, #020617, #020617 40%, #020617 100%);
      border-radius: 18px;
      border: 1px solid rgba(148,163,184,0.18);
      box-shadow: var(--shadow);
      padding: 20px 22px 22px;
      position: relative;
      overflow: hidden;
    }

    .panel::before {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at top left, rgba(56,189,248,0.12), transparent 55%);
      opacity: 0.9;
      pointer-events: none;
    }

    .panel-inner {
      position: relative;
      z-index: 1;
    }

    header {
      margin-bottom: 18px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .logo-mark {
      width: 32px;
      height: 32px;
      border-radius: 999px;
      background: radial-gradient(circle at 30% 20%, #e5e7eb, #38bdf8 40%, #0ea5e9 70%, #020617 100%);
      box-shadow: 0 0 0 1px rgba(148,163,184,0.4), 0 0 30px rgba(56,189,248,0.6);
    }

    .logo-text {
      display: flex;
      flex-direction: column;
    }

    .logo-title {
      font-weight: 650;
      letter-spacing: 0.03em;
      font-size: 1.05rem;
    }

    .logo-sub {
      font-size: 0.75rem;
      color: var(--muted);
    }

    .pill {
      padding: 4px 10px;
      border-radius: 999px;
      border: 1px solid rgba(148,163,184,0.4);
      font-size: 0.7rem;
      color: var(--muted);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: rgba(15,23,42,0.9);
    }

    .pill-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: #22c55e;
      box-shadow: 0 0 10px rgba(34,197,94,0.8);
    }

    h2 {
      margin: 0 0 4px;
      font-size: 1.1rem;
      font-weight: 600;
    }

    .subtitle {
      margin: 0 0 16px;
      font-size: 0.85rem;
      color: var(--muted);
    }

    .qa-step {
      margin-bottom: 16px;
      padding: 12px 12px 14px;
      border-radius: 12px;
      border: 1px solid rgba(148,163,184,0.25);
      background: radial-gradient(circle at top left, rgba(56,189,248,0.08), rgba(15,23,42,0.9));
    }

    .qa-label {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--muted);
      margin-bottom: 4px;
    }

    .qa-question {
      font-size: 0.95rem;
      margin-bottom: 8px;
    }

    .field-row {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      align-items: center;
    }

    label {
      font-size: 0.8rem;
      color: var(--muted);
    }

    input[type="text"],
    input[type="number"],
    select {
      background: rgba(15,23,42,0.9);
      border-radius: 999px;
      border: 1px solid rgba(148,163,184,0.4);
      padding: 7px 11px;
      color: var(--text);
      font-size: 0.85rem;
      outline: none;
      min-width: 0;
    }

    input[type="number"]::-webkit-outer-spin-button,
    input[type="number"]::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }

    input[type="number"] {
      -moz-appearance: textfield;
    }

    input:focus,
    select:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 1px rgba(56,189,248,0.5);
    }

    .inline-field {
      display: flex;
      flex-direction: column;
      gap: 4px;
      min-width: 120px;
      flex: 1;
    }

    .toggle-group {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .toggle {
      border-radius: 999px;
      border: 1px solid rgba(148,163,184,0.4);
      padding: 6px 12px;
      font-size: 0.8rem;
      cursor: pointer;
      background: rgba(15,23,42,0.9);
      color: var(--muted);
      transition: all 0.15s ease;
    }

    .toggle.active {
      background: var(--accent-soft);
      border-color: var(--accent);
      color: var(--text);
      box-shadow: 0 0 0 1px rgba(56,189,248,0.5);
    }

    .toggle.danger.active {
      background: rgba(248,113,113,0.12);
      border-color: var(--danger);
      color: #fecaca;
      box-shadow: 0 0 0 1px rgba(248,113,113,0.5);
    }

    .btn-row {
      display: flex;
      justify-content: flex-end;
      gap: 10px;
      margin-top: 10px;
    }

    button {
      border-radius: 999px;
      border: none;
      padding: 8px 16px;
      font-size: 0.85rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: all 0.15s ease;
    }

    .btn-primary {
      background: linear-gradient(135deg, #38bdf8, #0ea5e9);
      color: #020617;
      font-weight: 600;
      box-shadow: 0 10px 25px rgba(56,189,248,0.4);
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 14px 30px rgba(56,189,248,0.55);
    }

    .btn-ghost {
      background: transparent;
      color: var(--muted);
      border: 1px solid rgba(148,163,184,0.4);
    }

    .btn-ghost:hover {
      background: rgba(15,23,42,0.9);
      color: var(--text);
    }

    .summary-card {
      margin-top: 6px;
      padding: 12px 12px 14px;
      border-radius: 12px;
      border: 1px solid rgba(148,163,184,0.25);
      background: radial-gradient(circle at top right, rgba(56,189,248,0.08), rgba(15,23,42,0.9));
      font-size: 0.85rem;
    }

    .summary-header {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 6px;
    }

    .summary-title {
      font-size: 0.9rem;
      font-weight: 600;
    }

    .summary-limit {
      font-size: 0.8rem;
      color: var(--muted);
    }

    .summary-premium {
      font-size: 1.2rem;
      font-weight: 650;
    }

    .summary-premium span {
      font-size: 0.8rem;
      font-weight: 400;
      color: var(--muted);
      margin-left: 4px;
    }

    .summary-line {
      display: flex;
      justify-content: space-between;
      margin: 2px 0;
      color: var(--muted);
    }

    .summary-line strong {
      color: var(--text);
      font-weight: 500;
    }

    .badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 3px 8px;
      border-radius: 999px;
      font-size: 0.7rem;
      border: 1px solid rgba(148,163,184,0.4);
      color: var(--muted);
      margin-top: 4px;
    }

    .badge-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: var(--accent);
      box-shadow: 0 0 10px rgba(56,189,248,0.8);
    }

    .subjectivities {
      margin-top: 10px;
      padding-top: 8px;
      border-top: 1px dashed rgba(148,163,184,0.4);
      font-size: 0.8rem;
    }

    .subjectivities ul {
      padding-left: 18px;
      margin: 4px 0 0;
    }

    .subjectivities li {
      margin-bottom: 2px;
    }

    .pill-small {
      display: inline-flex;
      align-items: center;
      gap: 4px;
      padding: 2px 7px;
      border-radius: 999px;
      border: 1px solid rgba(148,163,184,0.4);
      font-size: 0.7rem;
      color: var(--muted);
    }

    .pill-small .dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: #facc15;
    }

    .quote-meta {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-top: 6px;
      font-size: 0.75rem;
      color: var(--muted);
    }

    .quote-meta span {
      padding: 2px 7px;
      border-radius: 999px;
      border: 1px solid rgba(148,163,184,0.3);
      background: rgba(15,23,42,0.9);
    }

    .footer-note {
      margin-top: 10px;
      font-size: 0.7rem;
      color: var(--muted);
    }

    .footer-note strong {
      color: var(--text);
      font-weight: 500;
    }

    .error {
      color: #fecaca;
      font-size: 0.75rem;
      margin-top: 4px;
    }
  </style>
</head>
<body>
  <div class="app-shell">
    <!-- LEFT: Q&A FLOW -->
    <div class="panel">
      <div class="panel-inner">
        <header>
          <div class="logo">
            <div class="logo-mark"></div>
            <div class="logo-text">
              <div class="logo-title">CrimeFast</div>
              <div class="logo-sub">Instant crime quote builder</div>
            </div>
          </div>
          <div class="pill">
            <span class="pill-dot"></span>
            Live prototype · Static · No backend
          </div>
        </header>

        <h2>Open CrimeFast</h2>
        <p class="subtitle">
          Answer a few underwriting questions and CrimeFast will generate a crime quote structure you can drop into a
          market email or quote letter.
        </p>

        <!-- STEP 1: BASIC INFO -->
        <div class="qa-step">
          <div class="qa-label">Step 1</div>
          <div class="qa-question">Tell me about the insured.</div>
          <div class="field-row">
            <div class="inline-field">
              <label>Named insured</label>
              <input type="text" id="insuredName" placeholder="SD Eats, LLC" />
            </div>
            <div class="inline-field">
              <label>Industry / operations</label>
              <input type="text" id="industry" placeholder="Quick service restaurants (Sonic franchisee)" />
            </div>
          </div>
          <div class="field-row" style="margin-top:8px;">
            <div class="inline-field">
              <label>Annual revenue (USD)</label>
              <input type="number" id="revenue" placeholder="29755222" />
            </div>
            <div class="inline-field">
              <label>Total employees</label>
              <input type="number" id="employees" placeholder="414" />
            </div>
            <div class="inline-field">
              <label>Locations</label>
              <input type="number" id="locations" placeholder="18" />
            </div>
          </div>
        </div>

        <!-- STEP 2: RISK PROFILE -->
        <div class="qa-step">
          <div class="qa-label">Step 2</div>
          <div class="qa-question">How does the money move?</div>
          <div class="field-row">
            <div class="inline-field">
              <label>Cash handling intensity</label>
              <select id="cashIntensity">
                <option value="low">Low (mostly electronic)</option>
                <option value="medium" selected>Medium (mixed cash / card)</option>
                <option value="high">High (heavy cash)</option>
              </select>
            </div>
            <div class="inline-field">
              <label>Internal controls quality</label>
              <select id="controlsQuality">
                <option value="strong" selected>Strong (segregation, dual control, reconciliations)</option>
                <option value="average">Average</option>
                <option value="weak">Weak / informal</option>
              </select>
            </div>
          </div>
          <div class="field-row" style="margin-top:8px;">
            <div class="inline-field">
              <label>Prior crime losses (last 3 years)</label>
              <div class="toggle-group">
                <div class="toggle" data-toggle="losses" data-value="no">No</div>
                <div class="toggle danger" data-toggle="losses" data-value="yes">Yes</div>
              </div>
            </div>
            <div class="inline-field">
              <label>Requested limit</label>
              <div class="toggle-group">
                <div class="toggle active" data-toggle="limit" data-value="250000">$250,000</div>
                <div class="toggle" data-toggle="limit" data-value="500000">$500,000</div>
              </div>
            </div>
          </div>
          <div id="lossesNote" class="error" style="display:none;">
            You marked prior crime losses. CrimeFast will load a surcharge and flag this as a talking point.
          </div>
        </div>

        <!-- STEP 3: ENTITIES -->
        <div class="qa-step">
          <div class="qa-label">Step 3</div>
          <div class="qa-question">Any related entities to schedule?</div>
          <p style="font-size:0.8rem;color:var(--muted);margin:0 0 6px;">
            List key affiliates you want on the policy (e.g., CINOS I, LLC; SD Fusion, LLC; Morco Management).
          </p>
          <textarea id="entities" rows="3" style="
            width:100%;
            border-radius:12px;
            border:1px solid rgba(148,163,184,0.4);
            background:rgba(15,23,42,0.9);
            color:var(--text);
            font-size:0.8rem;
            padding:8px 10px;
            resize:vertical;
          " placeholder="CINOS I, LLC (Sonic – 98% Bryant Morrison; 2% Morco Management)
CINOS II, LLC (Sonic – 98% Bryant Morrison; 2% Morco Management)
CINOS V, LLC (Sonic – 98% Bryant Morrison; 2% Morco Management)
SD Fusion, LLC (Sonic – 100% Bryant Morrison)
Morco Management (Mgmt company – 100% Amy Morrison)"></textarea>
        </div>

        <!-- STEP 4: TERM -->
        <div class="qa-step">
          <div class="qa-label">Step 4</div>
          <div class="qa-question">What term are you targeting?</div>
          <div class="field-row">
            <div class="inline-field">
              <label>Inception</label>
              <input type="text" id="termFrom" placeholder="06/01/2026" />
            </div>
            <div class="inline-field">
              <label>Expiration</label>
              <input type="text" id="termTo" placeholder="10/01/2027" />
            </div>
          </div>
        </div>

        <div class="btn-row">
          <button class="btn-ghost" type="button" id="resetBtn">Reset</button>
          <button class="btn-primary" type="button" id="quoteBtn">
            Generate CrimeFast quote
          </button>
        </div>

        <div id="validationError" class="error" style="display:none;margin-top:8px;">
          Please complete at least: Named insured, revenue, employees, locations, and requested limit.
        </div>
      </div>
    </div>

    <!-- RIGHT: QUOTE OUTPUT -->
    <div class="panel">
      <div class="panel-inner">
        <header>
          <div>
            <div class="logo-title">Quote preview</div>
            <div class="logo-sub">What you can paste into an email or proposal</div>
          </div>
          <div class="pill">
            <span class="pill-dot"></span>
            Generated by CrimeFast
          </div>
        </header>

        <div id="quoteOutput" class="summary-card">
          <div class="summary-header">
            <div>
              <div class="summary-title">No quote yet</div>
              <div class="summary-limit">Click “Generate CrimeFast quote” to see terms.</div>
            </div>
          </div>
          <p style="font-size:0.8rem;color:var(--muted);margin:4px 0 0;">
            Once you run the flow, this panel will show:
          </p>
          <ul style="font-size:0.8rem;color:var(--muted);margin:4px 0 0 18px;">
            <li>Limit, deductible, and annual premium</li>
            <li>Key underwriting assumptions</li>
            <li>Subjectivities you can send to the retailer</li>
          </ul>
        </div>

        <div class="footer-note">
          <strong>Note:</strong> This is a static prototype. Rating logic is illustrative only and not an official GAIG
          rate plan. You can adjust the factors in the JavaScript section as your pricing strategy evolves.
        </div>
      </div>
    </div>
  </div>

  <script>
    // --- Simple rating + logic engine for CrimeFast ---

    const state = {
      limit: 250000,
      priorLosses: "no",
    };

    function formatMoney(n) {
      if (isNaN(n)) return "$0";
      return "$" + n.toLocaleString("en-US", { maximumFractionDigits: 0 });
    }

    function getBaseRate(revenue, employees, locations) {
      // Very simple illustrative logic:
      // Start with a base rate per $1,000 of revenue, then adjust for size.
      if (!revenue || revenue <= 0) return 0.18;

      let rate = 0.18; // base per $1,000

      if (revenue > 10000000 && revenue <= 30000000) rate = 0.16;
      if (revenue > 30000000 && revenue <= 60000000) rate = 0.14;
      if (revenue > 60000000) rate = 0.12;

      // Slight bump for many locations (more cash points)
      if (locations >= 15 && locations < 30) rate *= 1.05;
      if (locations >= 30) rate *= 1.1;

      // Slight bump for large headcount
      if (employees > 500 && employees <= 1000) rate *= 1.05;
      if (employees > 1000) rate *= 1.1;

      return rate;
    }

    function getRiskFactor(cashIntensity, controlsQuality, priorLosses) {
      let factor = 1.0;

      // Cash intensity
      if (cashIntensity === "medium") factor *= 1.05;
      if (cashIntensity === "high") factor *= 1.12;

      // Controls
      if (controlsQuality === "average") factor *= 1.05;
      if (controlsQuality === "weak") factor *= 1.15;
      if (controlsQuality === "strong") factor *= 0.95;

      // Prior losses
      if (priorLosses === "yes") factor *= 1.25;

      return factor;
    }

    function calculatePremium(limit, revenue, employees, locations, cashIntensity, controlsQuality, priorLosses) {
      const baseRate = getBaseRate(revenue, employees, locations); // per $1,000
      const riskFactor = getRiskFactor(cashIntensity, controlsQuality, priorLosses);

      // Convert revenue to thousands
      const revThousands = (revenue || 0) / 1000;
      let premium = revThousands * baseRate * riskFactor;

      // Scale with limit (simple linear scaling)
      const limitFactor = limit / 250000; // 250k is base
      premium *= limitFactor;

      // Minimum premium floor
      if (premium < 1500) premium = 1500;

      return Math.round(premium);
    }

    function buildSubjectivities(priorLosses, controlsQuality) {
      const items = [];

      items.push("Confirm cash-handling controls including dual-control cash counts, daily deposits, and restricted safe access.");
      items.push("Confirm segregation of duties for disbursements, reconciliations, and vendor maintenance.");
      items.push("Confirm all locations follow the same internal control framework.");

      if (controlsQuality === "weak" || controlsQuality === "average") {
        items.push("Provide brief narrative on planned enhancements to internal controls over the next 12 months.");
      }

      if (priorLosses === "yes") {
        items.push("Provide details of all prior crime or fidelity losses in the last 5 years, including cause and corrective actions.");
      }

      return items;
    }

    function buildQuote() {
      const insuredName = document.getElementById("insuredName").value.trim() || "Insured";
      const industry = document.getElementById("industry").value.trim() || "Commercial business";
      const revenue = parseFloat(document.getElementById("revenue").value || "0");
      const employees = parseInt(document.getElementById("employees").value || "0", 10);
      const locations = parseInt(document.getElementById("locations").value || "0", 10);
      const cashIntensity = document.getElementById("cashIntensity").value;
      const controlsQuality = document.getElementById("controlsQuality").value;
      const entities = document.getElementById("entities").value.trim();
      const termFrom = document.getElementById("termFrom").value.trim() || "06/01/2026";
      const termTo = document.getElementById("termTo").value.trim() || "10/01/2027";

      // Basic validation
      const validationError = document.getElementById("validationError");
      if (!insuredName || !revenue || !employees || !locations || !state.limit) {
        validationError.style.display = "block";
        return;
      } else {
        validationError.style.display = "none";
      }

      const premium = calculatePremium(
        state.limit,
        revenue,
        employees,
        locations,
        cashIntensity,
        controlsQuality,
        state.priorLosses
      );

      const subjectivities = buildSubjectivities(state.priorLosses, controlsQuality);

      const quoteDiv = document.getElementById("quoteOutput");
      quoteDiv.innerHTML = "";

      const wrapper = document.createElement("div");

      const header = document.createElement("div");
      header.className = "summary-header";

      const left = document.createElement("div");
      const title = document.createElement("div");
      title.className = "summary-title";
      title.textContent = insuredName + " – Crime";

      const limitLine = document.createElement("div");
      limitLine.className = "summary-limit";
      limitLine.textContent = formatMoney(state.limit) + " Comprehensive Crime (Discovery Form)";

      left.appendChild(title);
      left.appendChild(limitLine);

      const right = document.createElement("div");
      right.className = "summary-premium";
      right.innerHTML = formatMoney(premium) + '<span>annual premium (illustrative)</span>';

      header.appendChild(left);
      header.appendChild(right);

      const meta = document.createElement("div");
      meta.className = "quote-meta";
      meta.innerHTML = `
        <span>Deductible: $5,000</span>
        <span>Form: Comprehensive Asset Protection (Discovery)</span>
        <span>Term: ${termFrom} to ${termTo}</span>
      `;

      const coverageLines = document.createElement("div");
      coverageLines.style.marginTop = "6px";
      coverageLines.innerHTML = `
        <div class="summary-line">
          <span>Employee Theft</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Employee Theft of Client's Property</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Forgery or Alteration</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Inside / Outside the Premises</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Computer Hacking & Funds Transfer Fraud</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Money Orders & Counterfeit Currency</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Credit, Debit, or Charge Card Forgery</span>
          <strong>${formatMoney(state.limit)}</strong>
        </div>
        <div class="summary-line">
          <span>Claims Expense Coverage</span>
          <strong>$10,000</strong>
        </div>
      `;

      const badge = document.createElement("div");
      badge.className = "badge";
      badge.innerHTML = `<span class="badge-dot"></span> Generated via CrimeFast – ${industry}`;

      const subjDiv = document.createElement("div");
      subjDiv.className = "subjectivities";
      subjDiv.innerHTML = `<strong>Subjectivities / Underwriting Notes:</strong>`;
      const ul = document.createElement("ul");
      subjectivities.forEach((s) => {
        const li = document.createElement("li");
        li.textContent = s;
        ul.appendChild(li);
      });
      subjDiv.appendChild(ul);

      if (entities) {
        const entDiv = document.createElement("div");
        entDiv.style.marginTop = "8px";
        entDiv.innerHTML = `<span class="pill-small"><span class="dot"></span> Scheduled entities (summary)</span>`;
        const pre = document.createElement("pre");
        pre.style.margin = "4px 0 0";
        pre.style.fontSize = "0.75rem";
        pre.style.whiteSpace = "pre-wrap";
        pre.style.color = "var(--muted)";
        pre.textContent = entities;
        entDiv.appendChild(pre);
        subjDiv.appendChild(entDiv);
      }

      const footer = document.createElement("div");
      footer.className = "footer-note";
      footer.innerHTML = `
        <strong>Positioning language:</strong> “We can offer ${formatMoney(
          state.limit
        )} Comprehensive Crime on a discovery form with a $5,000 deductible, subject to standard crime underwriting and the subjectivities noted above.”
      `;

      wrapper.appendChild(header);
      wrapper.appendChild(meta);
      wrapper.appendChild(coverageLines);
      wrapper.appendChild(badge);
      wrapper.appendChild(subjDiv);
      wrapper.appendChild(footer);

      quoteDiv.appendChild(wrapper);
    }

    // --- UI wiring ---

    function initToggles() {
      const lossToggles = document.querySelectorAll('[data-toggle="losses"]');
      lossToggles.forEach((el) => {
        el.addEventListener("click", () => {
          lossToggles.forEach((x) => x.classList.remove("active"));
          el.classList.add("active");
          state.priorLosses = el.getAttribute("data-value");
          document.getElementById("lossesNote").style.display =
            state.priorLosses === "yes" ? "block" : "none";
        });
      });

      const limitToggles = document.querySelectorAll('[data-toggle="limit"]');
      limitToggles.forEach((el) => {
        el.addEventListener("click", () => {
          limitToggles.forEach((x) => x.classList.remove("active"));
          el.classList.add("active");
          state.limit = parseInt(el.getAttribute("data-value"), 10);
        });
      });
    }

    function initButtons() {
      document.getElementById("quoteBtn").addEventListener("click", buildQuote);

      document.getElementById("resetBtn").addEventListener("click", () => {
        document.getElementById("insuredName").value = "";
        document.getElementById("industry").value = "";
        document.getElementById("revenue").value = "";
        document.getElementById("employees").value = "";
        document.getElementById("locations").value = "";
        document.getElementById("cashIntensity").value = "medium";
        document.getElementById("controlsQuality").value = "strong";
        document.getElementById("entities").value = "";
        document.getElementById("termFrom").value = "";
        document.getElementById("termTo").value = "";
        document.getElementById("validationError").style.display = "none";
        document.getElementById("lossesNote").style.display = "none";

        // Reset toggles
        document.querySelectorAll('[data-toggle="losses"]').forEach((x) => x.classList.remove("active"));
        document.querySelector('[data-toggle="losses"][data-value="no"]').classList.add("active");
        state.priorLosses = "no";

        document.querySelectorAll('[data-toggle="limit"]').forEach((x) => x.classList.remove("active"));
        document.querySelector('[data-toggle="limit"][data-value="250000"]').classList.add("active");
        state.limit = 250000;

        // Reset quote panel
        const quoteDiv = document.getElementById("quoteOutput");
        quoteDiv.innerHTML = `
          <div class="summary-header">
            <div>
              <div class="summary-title">No quote yet</div>
              <div class="summary-limit">Click “Generate CrimeFast quote” to see terms.</div>
            </div>
          </div>
          <p style="font-size:0.8rem;color:var(--muted);margin:4px 0 0;">
            Once you run the flow, this panel will show:
          </p>
          <ul style="font-size:0.8rem;color:var(--muted);margin:4px 0 0 18px;">
            <li>Limit, deductible, and annual premium</li>
            <li>Key underwriting assumptions</li>
            <li>Subjectivities you can send to the retailer</li>
          </ul>
        `;
      });
    }

    document.addEventListener("DOMContentLoaded", () => {
      initToggles();
      initButtons();
    });
  </script>
</body>
</html>
