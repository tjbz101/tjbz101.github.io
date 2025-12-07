
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title> String List & Pro Setups</title>
  <style>
    body{font-family:Arial,sans-serif;margin:0;background:#fff;color:#041E42;}
    h1,h3{text-align:center;color:#041E42;}
    h1{margin:20px 0 10px;}
    h3{font-size:1.2em;margin-bottom:20px;}
  .tab {
  overflow: hidden;
  background: transparent;
  display: flex;
  justify-content: center;
  gap: 12px;
  padding: 15px 10px;
  flex-wrap: wrap;
  border-bottom: 2px solid #ddd;
}
.tab button {
  background: #f0f0f0;
  color: #041E42;
  border: none;
  padding: 12px 28px;
  font-size: 16px;
  font-weight: 600;
  border-radius: 30px;
  transition: all 0.3s ease;
  min-width: 140px;
}
.tab button:hover {
  background: #041E42;
  color: white;
  transform: translateY(-2px);
}
.tab button.active {
  background: #041E42;
  color: white;
  box-shadow: 0 6px 20px rgba(4,30,66,0.4);
  transform: translateY(-3px);
}
    .tabcontent{display:none;padding:20px;animation:fade 0.5s;}
    @keyframes fade{from{opacity:0}to{opacity:1}}
    table{border-collapse:collapse;width:100%;margin-bottom:20px;}
    th,td{border:1px solid #ddd;padding:8px;text-align:left;}
    th{background:#041E42;color:#fff;cursor:pointer;}
    th:hover{background:#003087;}
    #searchInput{width:100%;max-width:600px;margin:20px auto;display:block;padding:12px;font-size:16px;border:1px solid #ddd;border-radius:4px;}
    @media(max-width:767px){table{display:block;overflow-x:auto;white-space:nowrap;}th,td{font-size:0.9em;}}
  </style>
</head>
<body>

<h1>The Tennis Shop </h1>
<h3>V120325F</h3>

<div class="tab">
  <button class="tablinks active" onclick="openTab(event,'AvailStrings')">Available Strings</button>
  <button class="tablinks" onclick="openTab(event,'ProList')">Player Profiles</button>
  <button class="tablinks" onclick="openTab(event,'StringingInfo')">Tension Simulator</button>
</div>

<div id="AvailStrings" class="tabcontent" style="display:block;">
  <p style="text-align:center;">
    Available strings, sort by name or type. We can split sets for a hybrid string job.<br>
    You provide strings → $20 | Pick from below → $25<br>
    Currently stringing on a Gamma ELS 7500 stringer (50 years experience).
  </p>
  <input type="text" id="searchInput" placeholder="Search by name or type..." onkeyup="searchTable()">
  <table id="stringTable">
    <thead>
      <tr>
        <th onclick="sortTable(0)">String Name ↕</th>
        <th onclick="sortTable(1)">Type ↕</th>
        <th>Available</th>
        <th>MSRP (Set)</th>
        <th>Comfort Rating</th>
        <th>Durability</th>
        <th>Spin Potential</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
</div>

<div id="ProList" class="tabcontent">
  <h3 style="text-align:center;">Pro Player String Setups (Dec 2025)</h3>
  <table id="proTable">
    <thead><tr><th>#</th><th>Player</th><th>Tour</th><th>Racket Model</th><th>String Setup</th><th>Tension (lbs)</th></tr></thead>
    <tbody></tbody>
  </table>
</div>

<div id="StringingInfo" class="tabcontent">
  <h3 style="text-align:center; color:#041E42; margin-bottom:20px;">
    Ultimate String Job Simulator — Your Exact Inventory + Presets
  </h3>

  <p style="text-align:center; max-width:800px; margin:0 auto 35px; color:#333;">
    Pick any string from your stock, set gauge/tension/pattern/head size, or hit a preset below.
  </p>

  <!-- Controls -->
  <div style="text-align:center; margin-bottom:40px;">
    <div style="margin:18px 0;">
      <strong>Mains:</strong>
      <select id="mainString"></select>
      <select id="mainGauge"><option value="16" selected>16g</option><option value="16L">16L</option><option value="17">17g</option><option value="18">18g</option></select>
      <span id="mainTension" style="font-weight:bold;color:#0066cc;">50</span> lbs
      <input type="range" id="mainSlider" min="38" max="68" value="50" step="0.5" style="width:280px;">
    </div>

    <div style="margin:18px 0;">
      <strong>Crosses:</strong>
      <select id="crossString"></select>
      <select id="crossGauge"><option value="16" selected>16g</option><option value="16L">16L</option><option value="17">17g</option><option value="18">18g</option></select>
      <span id="crossTension" style="font-weight:bold;color:#0066cc;">50</span> lbs
      <input type="range" id="crossSlider" min="38" max="68" value="50" step="0.5" style="width:280px;">
    </div>

    <div style="margin:25px 0;">
      <strong>Pattern:</strong>
      <select id="pattern">
        <option value="1619" selected>16×19</option>
        <option value="1819">18×19</option>
        <option value="1820">18×20</option>
      </select>

      <strong style="margin-left:30px;">Head Size:</strong>
      <select id="headsize">
        <option value="95">95 in²</option>
        <option value="98" selected>98 in²</option>
        <option value="100">100 in²</option>
        <option value="105">105 in²</option>
        <option value="110">110 in²</option>
        <option value="115">115 in²</option>
        <option value="125">125+ in²</option>
      </select>
    </div>
  </div>

  <!-- Bars -->
  <div style="display:flex;justify-content:center;align-items:end;gap:35px;max-width:1100px;margin:40px auto;padding:30px 20px;background:#f8f9fa;border-radius:18px;box-shadow:0 8px 30px rgba(0,0,0,0.15);flex-wrap:nowrap;overflow-x:auto;">
    <div style="text-align:center;min-width:110px;"><div style="font-weight:bold;color:#041E42;">Power</div><div style="height:220px;width:55px;background:#eee;border-radius:14px;margin:10px auto;overflow:hidden;position:relative;"><div id="powerFill" style="height:86%;background:#4CAF50;border-radius:14px;transition:all .6s ease;position:absolute;bottom:0;width:100%;"></div></div><div id="powerValue" style="color:#4CAF50;font-weight:bold;font-size:1.3em;">86%</div></div>
    <div style="text-align:center;min-width:110px;"><div style="font-weight:bold;color:#041E42;">Comfort</div><div style="height:220px;width:55px;background:#eee;border-radius:14px;margin:10px auto;overflow:hidden;position:relative;"><div id="comfortFill" style="height:93%;background:#2196F3;border-radius:14px;transition:all .6s ease;position:absolute;bottom:0;width:100%;"></div></div><div id="comfortValue" style="color:#2196F3;font-weight:bold;font-size:1.3em;">93%</div></div>
    <div style="text-align:center;min-width:110px;"><div style="font-weight:bold;color:#041E42;">Durability</div><div style="height:220px;width:55px;background:#eee;border-radius:14px;margin:10px auto;overflow:hidden;position:relative;"><div id="durabilityFill" style="height:52%;background:#FF9800;border-radius:14px;transition:all .6s ease;position:absolute;bottom:0;width:100%;"></div></div><div id="durabilityValue" style="color:#FF9800;font-weight:bold;font-size:1.3em;">52%</div></div>
    <div style="text-align:center;min-width:110px;"><div style="font-weight:bold;color:#041E42;">Spin</div><div style="height:220px;width:55px;background:#eee;border-radius:14px;margin:10px auto;overflow:hidden;position:relative;"><div id="spinFill" style="height:54%;background:#9C27B0;border-radius:14px;transition:all .6s ease;position:absolute;bottom:0;width:100%;"></div></div><div id="spinValue" style="color:#9C27B0;font-weight:bold;font-size:1.3em;">54%</div></div>
    <div style="text-align:center;min-width:110px;"><div style="font-weight:bold;color:#041E42;">Control</div><div style="height:220px;width:55px;background:#eee;border-radius:14px;margin:10px auto;overflow:hidden;position:relative;"><div id="controlFill" style="height:64%;background:#F44336;border-radius:14px;transition:all .6s ease;position:absolute;bottom:0;width:100%;"></div></div><div id="controlValue" style="color:#F44336;font-weight:bold;font-size:1.3em;">64%</div></div>
  </div>

  <!-- Presets + Copy Button -->
  <div style="text-align:center; margin:40px 0;">
    <strong style="color:#041E42;">Quick Presets:</strong><br><br>
    <button onclick="loadPreset('alcaraz()" class="preset">Alcaraz (RPM Blast 17g 55/53)</button>
    <button onclick="loadPreset('sinner')" class="preset">Sinner (Hawk Touch 61)</button>
    <button onclick="loadPreset('swiatek')" class="preset">Swiatek (Razor Code 53)</button>
    <button onclick="loadPreset('federer')" class="preset">Federer Classic (Gut/Poly)</button>
    <button onclick="loadPreset('armfriendly')" class="preset">Max Comfort</button>
    <button onclick="loadPreset('maxspin')" class="preset">Max Spin</button>
  </div>

  <button onclick="copySetup()" style="display:block;margin:30px auto;padding:12px 30px;font-size:1.1em;background:#041E42;color:white;border:none;border-radius:30px;cursor:pointer;box-shadow:0 4px 15px rgba(0,0,0,0.2);">
    📋 Copy My Setup to Clipboard
  </button>

  <script>
    // Your full 27-string + renamed generics database
    const stringData = {
      "1Generic Polyester":       {p:50,c:35,d:90,s:94,k:93},
      "1Generic Multifilament":   {p:86,c:93,d:52,s:54,k:64},
      "1Generic Synthetic Gut":   {p:72,c:81,d:74,s:62,k:71},
      "1Generic Natural Gut":     {p:93,c:96,d:38,s:48,k:58},
      "Asics Resolution 16":      {p:70,c:80,d:72,s:60,k:70},
      "Babolat Conquest":          {p:72,c:82,d:75,s:58,k:68},
      "Babolat N.Vy":             {p:75,c:85,d:65,s:55,k:65},
      "Babolat Excel":            {p:88,c:94,d:50,s:52,k:62},
      "Bluestar Multi Filament":  {p:87,c:93,d:55,s:54,k:64},
      "Gamma Octo TNT":           {p:74,c:83,d:78,s:62,k:72},
      "Head FXP":                {p:71,c:81,d:73,s:59,k:69},
      "Head FXP Tour":            {p:69,c:79,d:75,s:63,k:74},
      "Head Intellistring":       {p:73,c:84,d:70,s:57,k:67},
      "Head Velocity MLT":         {p:88,c:94,d:54,s:56,k:66},
      "Kirschbaum Super Smash":   {p:48,c:30,d:94,s:98,k:96},
      "Kirschbaum Synthetic Gut": {p:70,c:80,d:76,s:60,k:70},
      "Prince Control 15":        {p:87,c:92,d:52,s:53,k:63},
      "Prince Tour XC":           {p:50,c:34,d:91,s:95,k:94},
      "Prince Synthetic Gut 15L": {p:71,c:81,d:74,s:59,k:69},
      "Prince Synthetic Gut with Duraflex": {p:73,c:83,d:80,s:58,k:68},
      "Tourna Premier Poly":      {p:52,c:37,d:89,s:93,k:91},
      "Wilson Extreme Octane":    {p:76,c:85,d:70,s:62,k:72},
      "Wilson Hollowcore 16":     {p:78,c:87,d:68,s:60,k:70},
      "Wilson Hyperlast":         {p:49,c:32,d:92,s:96,k:95},
      "Wilson NXT with Duramax 15":{p:89,c:95,d:56,s:55,k:65},
      "Wilson Poly Last":         {p:48,c:30,d:93,s:97,k:96},
      "Wilson SGX":              {p:72,c:82,d:75,s:60,k:70},
      "Wilson Shock Shield 16":   {p:74,c:86,d:72,s:58,k:68},
      "Wilson Shock Shield 17":   {p:75,c:88,d:68,s:57,k:67},
      "Wilson Super Spin 16":     {p:85,c:90,d:50,s:70,k:65},
      "Wilson Synthetic Gut Extreme":{p:73,c:83,d:76,s:61,k:71}
    };

    // Populate dropdowns
    const list = Object.keys(stringData).sort();
    ['mainString','crossString'].forEach(id => {
      const sel = document.getElementById(id);
      list.forEach(s => {
        const opt = document.createElement('option');
        opt.value = s;
        opt.textContent = s.replace('1Generic ',''); // hide the 1 in display
        sel.appendChild(opt);
      });
      sel.value = '1Generic Multifilament';
    });

    const gaugeEffect = {"16":0,"16L":2,"17":5,"18":9};
    const patternEffect = {"1619":{s:+12,p:+8,k:-6,d:-8},"1819":{s:+4,p:+2,k:+2,d:+2},"1820":{s:-8,p:-6,k:+
  <script>
    // Your 27 strings + generic fallbacks
    const stringData = {
      "1 Generic Polyester":      {p:50,c:35,d:90,s:94,k:93},
      "1 Generic Multifilament":  {p:86,c:93,d:52,s:54,k:64},
      "1 Generic Synthetic Gut":  {p:72,c:81,d:74,s:62,k:71},
      "1 Generic Natural Gut":    {p:93,c:96,d:38,s:48,k:58},
      "Asics Resolution 16":   {p:70,c:80,d:72,s:60,k:70},
      "Babolat Conquest":       {p:72,c:82,d:75,s:58,k:68},
      "Babolat N.Vy":          {p:75,c:85,d:65,s:55,k:65},
      "Babolat Excel":          {p:88,c:94,d:50,s:52,k:62},
      "Bluestar Multi Filament":{p:87,c:93,d:55,s:54,k:64},
      "Gamma Octo TNT":        {p:74,c:83,d:78,s:62,k:72},
      "Head FXP":              {p:71,c:81,d:73,s:59,k:69},
      "Head FXP Tour":         {p:69,c:79,d:75,s:63,k:74},
      "Head Intellistring":    {p:73,c:84,d:70,s:57,k:67},
      "Head Velocity MLT":      {p:88,c:94,d:54,s:56,k:66},
      "Kirschbaum Super Smash": {p:48,c:30,d:94,s:98,k:96},
      "Kirschbaum Synthetic Gut":{p:70,c:80,d:76,s:60,k:70},
      "Prince Control 15":      {p:87,c:92,d:52,s:53,k:63},
      "Prince Tour XC":         {p:50,c:34,d:91,s:95,k:94},
      "Prince Synthetic Gut 15L":{p:71,c:81,d:74,s:59,k:69},
      "Prince Synthetic Gut with Duraflex":{p:73,c:83,d:80,s:58,k:68},
      "Tourna Premier Poly":    {p:52,c:37,d:89,s:93,k:91},
      "Wilson Extreme Octane":  {p:76,c:85,d:70,s:62,k:72},
      "Wilson Hollowcore 16":  {p:78,c:87,d:68,s:60,k:70},
      "Wilson Hyperlast":       {p:49,c:32,d:92,s:96,k:95},
      "Wilson NXT with Duramax 15":{p:89,c:95,d:56,s:55,k:65},
      "Wilson Poly Last":       {p:48,c:30,d:93,s:97,k:96},
      "Wilson SGX":            {p:72,c:82,d:75,s:60,k:70},
      "Wilson Shock Shield 16": {p:74,c:86,d:72,s:58,k:68},
      "Wilson Shock Shield 17": {p:75,c:88,d:68,s:57,k:67},
      "Wilson Super Spin 16":  {p:85,c:90,d:50,s:70,k:65},
      "Wilson Synthetic Gut Extreme":{p:73,c:83,d:76,s:61,k:71}
    };

    // Populate dropdowns
    const stringsList = Object.keys(stringData).sort();
    const selects = [document.getElementById('mainString'), document.getElementById('crossString')];
    selects.forEach(sel => {
      stringsList.forEach(str => {
        const opt = document.createElement('option');
        opt.value = str;
        opt.textContent = str;
        sel.appendChild(opt);
      });
      // Set defaults
      sel.value = sel.id === 'mainString' ? "Generic Polyester" : "Generic Multifilament";
    });

    // Rest of the math (gauge, pattern, headsize, tension) — same as last version
    const gaugeEffect = {"16":0,"16L":2,"17":5,"18":9};
    const patternEffect = {"1619":{s:+12,p:+8,k:-6,d:-8},"1819":{s:+4,p:+2,k:+2,d:+2},"1820":{s:-8,p:-6,k:+12,d:+10}};
    const headsizeEffect = {95:{k:+10,s:+5,p:-8},98:{k:+5,s:+2,p:-3},100:{p:+5,k:-2},105:{p:+12,k:-6},110:{p:+18,k:-10},115:{p:+25,k:-14},125:{p:+35,k:-18}};
    const perLb = {p:-1.1,c:-0.9,d:+0.7,s:+1.4,k:+1.7};

    function calc(){
      const m = stringData[document.getElementById('mainString').value];
      const c = stringData[document.getElementById('crossString').value];
      const mg = gaugeEffect[document.getElementById('mainGauge').value];
      const cg = gaugeEffect[document.getElementById('crossGauge').value];
      const pat = patternEffect[document.getElementById('pattern').value];
      const hs = headsizeEffect[document.getElementById('headsize').value];
      const mt = parseFloat(document.getElementById('mainSlider').value);
      const ct = parseFloat(document.getElementById('crossSlider').value);
      document.getElementById('mainTension').textContent = mt;
      document.getElementById('crossTension').textContent = ct;
      const avgT = (mt + ct) / 2;
      const diff = avgT - 55;
      const gaugeBonus = (mg + cg) / 2;

      const r = {
        p: Math.round((m.p + c.p)/2 + perLb.p * diff + gaugeBonus + (pat.p||0) + (hs.p||0)),
        c: Math.round((m.c + c.c)/2 + perLb.c * diff + gaugeBonus + (pat.c||0) + (hs.c||0)),
        d: Math.round((m.d + c.d)/2 + perLb.d * diff - gaugeBonus * 0.8 + (pat.d||0) + (hs.d||0)),
        s: Math.round((m.s + c.s)/2 + perLb.s * diff + gaugeBonus * 1.2 + (pat.s||0) + (hs.s||0)),
        k: Math.round((m.k + c.k)/2 + perLb.k * diff + gaugeBonus * 0.6 + (pat.k||0) + (hs.k||0))
      };

      ['power','comfort','durability','spin','control'].forEach(a=>{
        let v = r[a[0]];
        v = Math.max(10, Math.min(100, v));
        document.getElementById(a+'Fill').style.height = v+'%';
        document.getElementById(a+'Value').textContent = v+'%';
      });
    }

    ['mainString','mainGauge','mainSlider','crossString','crossGauge','crossSlider','pattern','headsize'].forEach(id=>{
      document.getElementById(id).addEventListener('input', calc);
      document.getElementById(id).addEventListener('change', calc);
    });

    calc(); // init
  </script>
</div>
<script>
const strings = [
  {name:"Asics Resolution 16",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Solid all-court synthetic gut. Balanced power/comfort."},
  {name:"Babolat Conquest",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"14-18 hours",spin:"Moderate (6/10)",review:"Arm-friendly, durable, cheap. Rec player favorite."},
  {name:"Babolat N.Vy",type:"Synthetic Gut",available:"Limited",msrp:"$25",comfort:"High (8/10)",durability:"10-14 hours",spin:"Moderate (6/10)",review:"Super soft and lively — feels almost like a multi."},
  {name:"Babolat Excel",type:"Multifilament",available:"Yes",msrp:"$25",comfort:"Very High (9/10)",durability:"8-12 hours",spin:"Low (5/10)",review:"One of the plushest multis. Gut-like comfort."},
  {name:"Bluestar Multi Filament",type:"Multifilament",available:"Yes",msrp:"$25",comfort:"Very High (9/10)",durability:"10-14 hours",spin:"Low (5/10)",review:"Budget gut substitute. Insanely comfortable."},
  {name:"Gamma Octo TNT",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"14-18 hours",spin:"Moderate (6/10)",review:"Octagonal shape adds bite. Durable and crisp."},
  {name:"Head FXP",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Classic reliable syn gut. Great value."},
  {name:"Head FXP Tour",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"10-14 hours",spin:"Moderate (6/10)",review:"Firmer version of FXP. Better control."},
  {name:"Head Intellistring",type:"Synthetic Gut",available:"Limited",msrp:"$25",comfort:"High (8/10)",durability:"10-14 hours",spin:"Moderate (6/10)",review:"Adaptive feel tech. Very comfortable."},
  {name:"Head Velocity MLT",type:"Multifilament",available:"Yes",msrp:"$25",comfort:"Very High (9/10)",durability:"15-20 hours",spin:"Moderate (7/10)",review:"Top-tier arm-friendly multi."},
  {name:"Kirschbaum Super Smash",type:"Polyester",available:"Yes",msrp:"$25",comfort:"Low (4/10)",durability:"20-25 hours",spin:"Very High (9/10)",review:"Classic shaped poly. Huge spin."},
  {name:"Kirschbaum Synthetic Gut",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Underrated budget syn gut."},
  {name:"Prince Control 15",type:"Multifilament",available:"Yes",msrp:"$25",comfort:"Very High (9/10)",durability:"8-12 hours",spin:"Low (5/10)",review:"Ultra-soft multi. Amazing for elbows."},
  {name:"Prince Tour XC",type:"Polyester",available:"Yes",msrp:"$25",comfort:"Low (4/10)",durability:"18-22 hours",spin:"Very High (9/10)",review:"Shaped poly with great bite."},
  {name:"Prince Synthetic Gut 15L",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Thinner gauge = more feel."},
  {name:"Prince Synthetic Gut with Duraflex",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"14-18 hours",spin:"Moderate (6/10)",review:"Most durable syn gut here."},
  {name:"Tourna Premier Poly",type:"Polyester",available:"Yes",msrp:"$25",comfort:"Low (4/10)",durability:"18-22 hours",spin:"Very High (9/10)",review:"Budget shaped poly that punches above price."},
  {name:"Wilson Extreme Octane",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Lively syn gut with good pop."},
  {name:"Wilson Hollowcore 16",type:"Synthetic Gut",available:"Limited",msrp:"$25",comfort:"High (8/10)",durability:"10-14 hours",spin:"Moderate (6/10)",review:"Hollow design gives extra power."},
  {name:"Wilson Hyperlast",type:"Polyester",available:"No",msrp:"$25",comfort:"Low (4/10)",durability:"18-22 hours",spin:"Very High (9/10)",review:"Old-school stiff poly."},
  {name:"Wilson NXT with Duramax 15",type:"Multifilament",available:"Yes",msrp:"$25",comfort:"Very High (9/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Gold standard multi."},
  {name:"Wilson Poly Last",type:"Polyester",available:"No",msrp:"$25",comfort:"Low (4/10)",durability:"18-22 hours",spin:"Very High (9/10)",review:"Discontinued but loved for control."},
  {name:"Wilson SGX",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Smooth all-around performance."},
  {name:"Wilson Shock Shield 16",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Vibration-dampening tech."},
  {name:"Wilson Shock Shield 17",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"10-14 hours",spin:"Moderate (6/10)",review:"Thinner = more feel."},
  {name:"Wilson Super Spin 16",type:"Multifilament",available:"No",msrp:"$25",comfort:"Very High (9/10)",durability:"8-12 hours",spin:"Moderate (7/10)",review:"Hex shape adds spin to soft multi."},
  {name:"Wilson Synthetic Gut Extreme",type:"Synthetic Gut",available:"Yes",msrp:"$25",comfort:"High (8/10)",durability:"12-16 hours",spin:"Moderate (6/10)",review:"Crisp and durable everyday string."}
];

const pros = [
  ["1","Carlos Alcaraz","ATP","Babolat Pure Aero 98 (98sq)","Babolat RPM Blast (poly)","55/53"],["2","Jannik Sinner","ATP","Head Speed Pro (100sq)","Head Hawk Touch (poly)","61/61"],["3","Novak Djokovic","ATP","Head Speed Pro (custom) (100sq)","Babolat Natural Gut mains / Luxilon ALU Power Rough crosses","59/56"],["4","Alexander Zverev","ATP","Head Gravity Pro (100sq)","Head Hawk Touch mains / Babolat VS Touch crosses","53/55"],["5","Daniil Medvedev","ATP","Tecnifibre T-Fight 305 (98sq)","Tecnifibre Razor Code Soft (poly)","48/48"],["6","Andrey Rublev","ATP","Head Gravity Pro (100sq)","Luxilon Adrenaline (poly)","57/57"],["7","Casper Ruud","ATP","Yonex EZONE 98 (98sq)","Yonex Poly Tour Spin mains / Poly Tour Pro crosses","54/54"],["8","Hubert Hurkacz","ATP","Yonex Percept 98H (98sq)","Solinco Tour Bite mains / Babolat VS Touch crosses","50/50"],["9","Stefanos Tsitsipas","ATP","Wilson Blade 98 (98sq)","Luxilon 4G / ALU Power (poly)","57/57"],["10","Holger Rune","ATP","Babolat Pure Aero VS (98sq)","Babolat RPM Blast (poly)","48/50"],["11","Grigor Dimitrov","ATP","Wilson Pro Staff RF97 Autograph (97sq)","Wilson Natural Gut mains / Luxilon 4G crosses","55/52"],["12","Alex de Minaur","ATP","Wilson Blade 98 (98sq)","Luxilon 4G (poly)","48.5/48.5"],["13","Taylor Fritz","ATP","Head IG Radical MP (95sq)","HEAD Hawk mains / Babolat VS Touch crosses","~52/~50"],["14","Tommy Paul","ATP","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","52/52"],["15","Frances Tiafoe","ATP","Yonex Percept 97 (97sq)","Yonex Poly Tour Pro (poly)","46/46"],["16","Ben Shelton","ATP","Yonex EZONE 98 (98sq)","Yonex Poly Tour Strike mains / Poly Tour Pro crosses","60/57"],["17","Ugo Humbert","ATP","Head Gravity MP (100sq)","Head Hawk Touch (poly)","53/55"],["18","Arthur Fils","ATP","Babolat Pure Drive 98 (98sq)","Babolat RPM Blast (poly)","50/52"],["19","Jack Draper","ATP","Dunlop Srixon Revo CV 3.0","Babolat RPM Blast (poly)","54/54"],["20","Sebastian Korda","ATP","Wilson Blade 98 (98sq)","Solinco Hyper-G Soft (poly)","51/53"],["21","Iga Swiatek","WTA","Tecnifibre T-Fight 305 (98sq)","Tecnifibre Razor Code (poly)","53/53"],["22","Aryna Sabalenka","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","50/50"],["23","Coco Gauff","WTA","Head Boom MP (100sq)","Luxilon ALU Power (poly)","53/53"],["24","Elena Rybakina","WTA","Yonex EZONE 98 (98sq)","Yonex Poly Tour Pro (poly)","53/55"],["25","Jasmine Paolini","WTA","Yonex VCORE 100 (100sq)","Yonex Poly Tour Pro (poly)","52/54"],["26","Qinwen Zheng","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power (poly)","50/52"],["27","Mirra Andreeva","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power Soft (poly)","49/51"],["28","Danielle Collins","WTA","Wilson Clash 100 (100sq)","Wilson NXT (multi)","55/55"],["29","Anna Kalinskaya","WTA","Wilson Blade 98 (98sq)","Luxilon RPM Blast (poly)","51/53"],["30","Madison Keys","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power (poly)","52/52"],["31","Beatriz Haddad Maia","WTA","Wilson Clash 100 (100sq)","Wilson NXT Duramax (multi)","54/54"],["32","Diana Shnaider","WTA","Babolat Pure Aero 98 (98sq)","Babolat RPM Blast (poly)","50/52"],["33","Emma Navarro","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","51/53"],["34","Ons Jabeur","WTA","Wilson Blade 98 (98sq)","Wilson NXT (multi)","53/55"],["35","Barbora Krejcikova","WTA","Yonex VCORE Pro 97 (97sq)","Yonex Poly Tour Pro (poly)","52/52"],["36","Elina Svitolina","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power Rough (poly)","50/50"],["37","Maria Sakkari","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","51/51"],["38","Daria Kasatkina","WTA","Diadem Forge 7 (unknown)","Diadem Evolution (poly)","49/51"],["39","Karolina Muchova","WTA","Head Gravity Pro (100sq)","Head Hawk Touch (poly)","52/54"],["40","Jessica Pegula","WTA","Yonex EZONE 98 (98sq)","Yonex Poly Tour Fire (poly)","50/52"],["41","Paula Badosa","WTA","Wilson Clash 100 (100sq)","Luxilon ALU Power (poly)","53/55"],["42","Zheng Qinwen","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power (poly)","50/52"],["43","Marketa Vondrousova","WTA","Wilson Pro Staff 97 (97sq)","Wilson NXT (multi)","54/54"],["44","Linda Noskova","WTA","Yonex EZONE 98 (98sq)","Yonex Poly Tour Pro (poly)","51/53"],["45","Elise Mertens","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power Soft (poly)","52/52"],["46","Donna Vekic","WTA","Head Gravity MP (100sq)","Head Hawk (poly)","53/55"],["47","Petra Kvitova","WTA","Wilson Pro Staff RF97 Autograph (97sq)","Luxilon ALU Power Rough (poly)","55/52"],["48","Victoria Azarenka","WTA","Wilson Aura Pro (unknown)","Wilson Natural Gut mains / Luxilon ALU crosses","56/53"],["49","Sofia Kenin","WTA","Wilson Blade 98 (98sq)","Luxilon RPM Team (poly)","50/50"],["50","Anastasija Sevastova","WTA","Wilson Blade 98 v9 (98sq)","Wilson NXT (multi)","52/54"]
];

// Render tables
strings.sort((a,b)=>a.name.localeCompare(b.name));
const stringBody = document.querySelector('#stringTable tbody');
strings.forEach(s=>{
  const tr=document.createElement('tr');
  tr.innerHTML=`<td><a href="#" onclick="toggleReview('${s.name.replace(/'/g,"\\'")}');return false;">${s.name}</a></td><td>${s.type}</td><td>${s.available}</td><td>${s.msrp}</td><td>${s.comfort}</td><td>${s.durability}</td><td>${s.spin}</td>`;
  stringBody.appendChild(tr);
});

const proBody = document.querySelector('#proTable tbody');
pros.forEach(p=>{
  const tr=document.createElement('tr');
  tr.innerHTML=`<td>${p[0]}</td><td>${p[1]}</td><td>${p[2]}</td><td>${p[3]}</td><td>${p[4]}</td><td>${p[5]}</td>`;
  proBody.appendChild(tr);
});

// Tablet + Desktop proof pop-up
let currentPopup = null;

// FINAL TABLET-PROOF POP-UP (replace just this function)
function toggleReview(name) {
  // Remove old popup
  document.querySelectorAll('.string-popup').forEach(p => p.remove());

  const s = strings.find(x => x.name === name);
  if (!s) return;
  const div = document.createElement('div');
  div.className = 'string-popup';
  div.style.cssText = `
    position:fixed;
    background:#041E42;
    color:white;
    padding:15px;
    border-radius:12px;
    max-width:320px;
    z-index:9999;
    box-shadow:0 8px 25px rgba(0,0,0,0.6);
    font-size:0.95em;
    pointer-events:none;
    opacity:0;
    transition:opacity 0.2s;
    left:20px;
    top:20px;
  `;
  div.innerHTML = `<strong>${name}</strong><br><em>${s.type}</em><hr style="border:0;border-top:1px solid #666;margin:8px 0">${s.review}`;
  document.body.appendChild(div);

  // Force show + position (works on first tap)
  setTimeout(() => {
    div.style.opacity = '1';
    div.style.left = '50%';
    div.style.top = '50%';
    div.style.transform = 'translate(-50%, -50%)';
  }, 10);

  // Close when tapping anywhere else
  const close = () => {
    div.remove();
    document.removeEventListener('click', close);
    document.removeEventListener('touchstart', close);
  };
  setTimeout(() => {
    document.addEventListener('click', close);
    document.addEventListener('touchstart', close);
  }, 100);
}

// Sort, search, tabs
let sortDir=[1,1];
function sortTable(col){
  sortDir[col] = sortDir[col] === 1 ? -1 : 1; // Flip direction (1=asc, -1=desc)
  
  strings.sort((a, b) => {
    let valueA = col === 0 ? a.name.toLowerCase() : a.type.toLowerCase();
    let valueB = col === 0 ? b.name.toLowerCase() : b.type.toLowerCase();
    if (valueA < valueB) return sortDir[col];
    if (valueA > valueB) return -sortDir[col];
    return 0;
  });
  
  // Re-render the table
  stringBody.innerHTML = '';
  strings.forEach(s => {
    const tr = document.createElement('tr');
    tr.innerHTML = `<td><a href="#" onclick="toggleReview('${s.name.replace(/'/g,"\\'")}');return false;">${s.name}</a></td><td>${s.type}</td><td>${s.available}</td><td>${s.msrp}</td><td>${s.comfort}</td><td>${s.durability}</td><td>${s.spin}</td>`;
    stringBody.appendChild(tr);
  });
}
function searchTable(){
  const term=document.getElementById('searchInput').value.toLowerCase();
  document.querySelectorAll('#stringTable tbody tr').forEach(r=>r.style.display=r.textContent.toLowerCase().includes(term)?'':'none');
}
function openTab(evt,tabName){
  document.querySelectorAll(".tabcontent").forEach(t=>t.style.display="none");
  document.querySelectorAll(".tablinks").forEach(b=>b.classList.remove("active"));
  document.getElementById(tabName).style.display="block";
  evt.currentTarget.classList.add("active");
}
</script>
</body>
</html>
