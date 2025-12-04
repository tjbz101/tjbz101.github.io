
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>String List + Pro Setups</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; background-color: #fff; color: #041E42; }
    h1 { text-align: center; color: #041E42; margin: 20px 0 10px; }
    h3 { text-align: center; color: #041E42; margin-bottom: 20px; font-size: 1.2em; }

    /* Tab styling */
    .tab {
      overflow: hidden;
      border-bottom: 1px solid #ccc;
      background-color: #f1f1f1;
      display: flex;
      justify-content: left;
      flex-wrap: wrap;
    }
    .tab button {
      background-color: inherit;
      border: none;
      outline: none;
      cursor: pointer;
      padding: 14px 20px;
      transition: 0.3s;
      font-size: 17px;
    }
    .tab button:hover { background-color: #ddd; }
    .tab button.active { background-color: #041E42; color: white; }

    .tabcontent {
      display: none;
      padding: 20px;
      animation: fadeEffect 0.5s;
    }
    @keyframes fadeEffect { from {opacity: 0;} to {opacity: 1;} }

    table { border-collapse: collapse; width: 100%; margin-bottom: 20px; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
    th { background-color: #041E42; color: #fff; cursor: pointer; }
    th:hover { background-color: #003087; }
    .sort-arrow { margin-left: 5px; }

    #searchInput {
      width: 100%; max-width: 600px; margin: 20px auto; display: block;
      padding: 12px; font-size: 16px; border: 1px solid #ddd; border-radius: 4px;
    }

    @media (max-width: 767px) {
      table { display: block; overflow-x: auto; white-space: nowrap; }
      th, td { font-size: 0.8em; padding: 4px; }
    }
  </style>
</head>
<body>

  <h1>Available String List & Player Profiles</h1>
  <h3>V120325B</h3>

  <div class="tab">
    <button class="tablinks active" onclick="openTab(event, 'AvailStrings')">Avail Strings</button>
    <button class="tablinks" onclick="openTab(event, 'ProList')">Pro List</button>
    <button class="tablinks" onclick="openTab(event, 'StringingInfo')">Stringing Info</button>
  </div>

  <!-- Tab 1: Available Strings -->
  <div id="AvailStrings" class="tabcontent" style="display: block;">
    <p style="text-align:center;">
      Available strings, sort by name or type. We can split sets for a hybrid string job.<br>
      You provide strings → $20 | Pick from below → $25<br>
      Currently stringing on a Gamma ELS 7500 stringer (50 years experience).
    </p>

    <input type="text" id="searchInput" placeholder="Search by name or type..." onkeyup="searchTable()">

    <table id="stringTable">
      <thead>
        <tr>
          <th onclick="sortTable(0)">String Name<span id="sortNameArrow" class="sort-arrow"> ↑</span></th>
          <th onclick="sortTable(1)">Type<span id="sortTypeArrow" class="sort-arrow"></span></th>
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

  <!-- Tab 2: Pro List -->
  <div id="ProList" class="tabcontent">
    <h3 style="text-align:center;">Pro Player String Setups (Dec 2025)</h3>
    <table id="proTable">
      <thead>
        <tr>
          <th>#</th><th>Player</th><th>Tour</th><th>Racket Model</th><th>String Setup</th><th>Tension (lbs)</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </div>

  <!-- Tab 3: Stringing Info -->
  <div id="StringingInfo" class="tabcontent">
    <h3 style="text-align:center;">Stringing Info</h3>
    <p style="text-align:center;">
      <img src="https://i.ibb.co/p6Gd1WyQ/IMG-0513.jpg" 
           alt="Stringing Info" style="max-width:100%; height:auto; border:2px solid #041E42; border-radius:8px;">
    </p>
  </div>

<script>
  // All available strings
  const strings = [
    { name: "Asics Resolution 16", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Babolat Conquest", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "14-18 hours", spin: "Moderate (6/10)" },
    { name: "Babolat N.Vy", type: "Synthetic Gut", available: "Limited", msrp: "$25", comfort: "High (8/10)", durability: "10-14 hours", spin: "Moderate (6/10)" },
    { name: "Babolat Excel", type: "Multifilament", available: "Yes", msrp: "$25", comfort: "Very High (9/10)", durability: "8-12 hours", spin: "Low (5/10)" },
    { name: "Bluestar Multi Filament", type: "Multifilament", available: "Yes", msrp: "$25", comfort: "Very High (9/10)", durability: "10-14 hours", spin: "Low (5/10)" },
    { name: "Gamma Octo TNT", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "14-18 hours", spin: "Moderate (6/10)" },
    { name: "Head FXP", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Head FXP Tour", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "10-14 hours", spin: "Moderate (6/10)" },
    { name: "Head Intellistring", type: "Synthetic Gut", available: "Limited", msrp: "$25", comfort: "High (8/10)", durability: "10-14 hours", spin: "Moderate (6/10)" },
    { name: "Head Velocity MLT", type: "Multifilament", available: "Yes", msrp: "$25", comfort: "Very High (9/10)", durability: "15-20 hours", spin: "Moderate (7/10)" },
    { name: "Kirschbaum Super Smash", type: "Polyester", available: "Yes", msrp: "$25", comfort: "Low (4/10)", durability: "20-25 hours", spin: "Very High (9/10)" },
    { name: "Kirschbaum Synthetic Gut", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Prince Control 15", type: "Multifilament", available: "Yes", msrp: "$25", comfort: "Very High (9/10)", durability: "8-12 hours", spin: "Low (5/10)" },
    { name: "Prince Tour XC", type: "Polyester", available: "Yes", msrp: "$25", comfort: "Low (4/10)", durability: "18-22 hours", spin: "Very High (9/10)" },
    { name: "Prince Synthetic Gut 15L", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Prince Synthetic Gut with Duraflex", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "14-18 hours", spin: "Moderate (6/10)" },
    { name: "Tourna Premier Poly", type: "Polyester", available: "Yes", msrp: "$25", comfort: "Low (4/10)", durability: "18-22 hours", spin: "Very High (9/10)" },
    { name: "Wilson Extreme Octane", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Wilson Hollowcore 16", type: "Synthetic Gut", available: "Limited", msrp: "$25", comfort: "High (8/10)", durability: "10-14 hours", spin: "Moderate (6/10)" },
    { name: "Wilson Hyperlast", type: "Polyester", available: "No", msrp: "$25", comfort: "Low (4/10)", durability: "18-22 hours", spin: "Very High (9/10)" },
    { name: "Wilson NXT with Duramax 15", type: "Multifilament", available: "Yes", msrp: "$25", comfort: "Very High (9/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Wilson Poly Last", type: "Polyester", available: "No", msrp: "$25", comfort: "Low (4/10)", durability: "18-22 hours", spin: "Very High (9/10)" },
    { name: "Wilson SGX", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Wilson Shock Shield 16", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" },
    { name: "Wilson Shock Shield 17", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "10-14 hours", spin: "Moderate (6/10)" },
    { name: "Wilson Super Spin 16", type: "Multifilament", available: "No", msrp: "$25", comfort: "Very High (9/10)", durability: "8-12 hours", spin: "Moderate (7/10)" },
    { name: "Wilson Synthetic Gut Extreme", type: "Synthetic Gut", available: "Yes", msrp: "$25", comfort: "High (8/10)", durability: "12-16 hours", spin: "Moderate (6/10)" }
  ];

  // ALL 50 pro players
  const pros = [
    ["1","Carlos Alcaraz","ATP","Babolat Pure Aero 98 (98sq)","Babolat RPM Blast (poly)","50/52"],
    ["2","Jannik Sinner","ATP","Head Speed Pro (100sq)","Head Hawk Touch (poly)","58/60"],
    ["3","Novak Djokovic","ATP","Head Speed Pro (custom) (100sq)","Babolat Natural Gut mains / Luxilon ALU Power Rough crosses","59/56"],
    ["4","Alexander Zverev","ATP","Head Gravity Pro (100sq)","Head Hawk (poly)","53/55"],
    ["5","Daniil Medvedev","ATP","Tecnifibre T-Fight 305 (98sq)","Tecnifibre Razor Code (poly)","52/54"],
    ["6","Andrey Rublev","ATP","Head YouTek IG Speed MP (100sq)","Head Hawk Touch (poly)","55/57"],
    ["7","Casper Ruud","ATP","Yonex EZONE 98 (98sq)","Yonex Poly Tour Pro (poly)","54/54"],
    ["8","Hubert Hurkacz","ATP","Wilson Blade 98 v9 (18x20) (98sq)","Luxilon ALU Power (poly)","52/52"],
    ["9","Stefanos Tsitsipas","ATP","Wilson Blade 98 (custom black) (98sq)","Luxilon RPM Team (poly)","50/52"],
    ["10","Holger Rune","ATP","Babolat Pure Aero VS (98sq)","Babolat RPM Blast (poly)","48/50"],
    ["11","Grigor Dimitrov","ATP","Wilson Pro Staff RF97 Autograph (97sq)","Wilson Natural Gut mains / Luxilon ALU Rough crosses","55/52"],
    ["12","Alex de Minaur","ATP","Wilson Blade 98 (98sq)","Luxilon ALU Power Soft (poly)","51/53"],
    ["13","Taylor Fritz","ATP","Head IG Radical MP (95sq)","HEAD Hawk (poly) mains / Babolat VS Touch (natural gut) crosses","~52/~50"],
    ["14","Tommy Paul","ATP","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","52/52"],
    ["15","Frances Tiafoe","ATP","Yonex VCORE Pro 97 (97sq)","Yonex Poly Tour Pro (poly)","42/42"],
    ["16","Ben Shelton","ATP","Yonex EZONE 98 (98sq)","Yonex Poly Tour Fire (poly)","48/50"],
    ["17","Ugo Humbert","ATP","Head Gravity MP (100sq)","Head Hawk Touch (poly)","53/55"],
    ["18","Arthur Fils","ATP","Babolat Pure Drive 98 (98sq)","Babolat RPM Blast (poly)","50/52"],
    ["19","Jack Draper","ATP","Wilson Pro Staff 97 (97sq)","Luxilon ALU Power (poly)","52/54"],
    ["20","Sebastian Korda","ATP","Wilson Blade 98 (98sq)","Solinco Hyper-G Soft (poly)","51/53"],
    ["21","Iga Swiatek","WTA","Yonex EZONE 98 (98sq)","Luxilon ALU Power Rough (poly)","52/52"],
    ["22","Aryna Sabalenka","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","50/50"],
    ["23","Coco Gauff","WTA","Head Aurora Pro (unknown)","Head Lynx Tour (poly)","51/53"],
    ["24","Elena Rybakina","WTA","Yonex EZONE 98 (98sq)","Yonex Poly Tour Pro (poly)","53/55"],
    ["25","Jasmine Paolini","WTA","Yonex VCORE 100 (100sq)","Yonex Poly Tour Spin (poly)","52/54"],
    ["26","Qinwen Zheng","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power (poly)","50/52"],
    ["27","Mirra Andreeva","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power Soft (poly)","49/51"],
    ["28","Danielle Collins","WTA","Wilson Clash 100 (100sq)","Wilson NXT (multi)","55/55"],
    ["29","Anna Kalinskaya","WTA","Wilson Blade 98 (98sq)","Luxilon RPM Blast (poly)","51/53"],
    ["30","Madison Keys","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power (poly)","52/52"],
    ["31","Beatriz Haddad Maia","WTA","Wilson Clash 100 (100sq)","Wilson NXT Duramax (multi)","54/54"],
    ["32","Diana Shnaider","WTA","Babolat Pure Aero 98 (98sq)","Babolat RPM Blast (poly)","50/52"],
    ["33","Emma Navarro","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","51/53"],
    ["34","Ons Jabeur","WTA","Wilson Blade 98 (98sq)","Wilson NXT (multi)","53/55"],
    ["35","Barbora Krejcikova","WTA","Yonex VCORE Pro 97 (97sq)","Yonex Poly Tour Pro (poly)","52/52"],
    ["36","Elina Svitolina","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power Rough (poly)","50/50"],
    ["37","Maria Sakkari","WTA","Wilson Blade 98 v9 (98sq)","Luxilon ALU Power (poly)","51/51"],
    ["38","Daria Kasatkina","WTA","Diadem Forge 7 (unknown)","Diadem Evolution (poly)","49/51"],
    ["39","Karolina Muchova","WTA","Head Gravity Pro (100sq)","Head Hawk Touch (poly)","52/54"],
    ["40","Jessica Pegula","WTA","Yonex EZONE 98 (98sq)","Yonex Poly Tour Fire (poly)","50/52"],
    ["41","Paula Badosa","WTA","Wilson Clash 100 (100sq)","Luxilon ALU Power (poly)","53/55"],
    ["42","Zheng Qinwen","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power (poly)","50/52"],
    ["43","Marketa Vondrousova","WTA","Wilson Pro Staff 97 (97sq)","Wilson NXT (multi)","54/54"],
    ["44","Linda Noskova","WTA","Yonex EZONE 98 (98sq)","Yonex Poly Tour Pro (poly)","51/53"],
    ["45","Elise Mertens","WTA","Wilson Blade 98 (98sq)","Luxilon ALU Power Soft (poly)","52/52"],
    ["46","Donna Vekic","WTA","Head Gravity MP (100sq)","Head Hawk (poly)","53/55"],
    ["47","Petra Kvitova","WTA","Wilson Pro Staff RF97 Autograph (97sq)","Luxilon ALU Power Rough (poly)","55/52"],
    ["48","Victoria Azarenka","WTA","Wilson Aura Pro (unknown)","Wilson Natural Gut mains / Luxilon ALU crosses","56/53"],
    ["49","Sofia Kenin","WTA","Wilson Blade 98 (98sq)","Luxilon RPM Team (poly)","50/50"],
    ["50","Anastasija Sevastova","WTA","Wilson Blade 98 v9 (98sq)","Wilson NXT (multi)","52/54"]
  ];

  // Render strings table
  strings.sort((a,b) => a.name.localeCompare(b.name));
  const stringBody = document.querySelector('#stringTable tbody');
  strings.forEach(s => {
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${s.name}</td><td>${s.type}</td><td>${s.available}</td><td>${s.msrp}</td><td>${s.comfort}</td><td>${s.durability}</td><td>${s.spin}</td>`;
    stringBody.appendChild(tr);
  });

  // Render pro table
  const proBody = document.querySelector('#proTable tbody');
  pros.forEach(p => {
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${p[0]}</td><td>${p[1]}</td><td>${p[2]}</td><td>${p[3]}</td><td>${p[4]}</td><td>${p[5]}</td>`;
    proBody.appendChild(tr);
  });

  // Sorting for strings table
  let sortDir = [1, 1]; // 0=name asc, 1=type asc
  function sortTable(col) {
    sortDir[col] = sortDir[col] === 1 ? -1 : 1;
    strings.sort((a,b) => {
      let x = col === 0 ? a.name : a.type;
      let y = col === 0 ? b.name : b.type;
      return sortDir[col] * x.localeCompare(y);
    });
    stringBody.innerHTML = '';
    strings.forEach(s => {
      const tr = document.createElement('tr');
      tr.innerHTML = `<td>${s.name}</td><td>${s.type}</td><td>${s.available}</td><td>${s.msrp}</td><td>${s.comfort}</td><td>${s.durability}</td><td>${s.spin}</td>`;
      stringBody.appendChild(tr);
    });
  }

  // Search
  function searchTable() {
    const term = document.getElementById('searchInput').value.toLowerCase();
    document.querySelectorAll('#stringTable tbody tr').forEach(row => {
      row.style.display = row.textContent.toLowerCase().includes(term) ? '' : 'none';
    });
  }

  // Tab switching
  function openTab(evt, tabName) {
    document.querySelectorAll(".tabcontent").forEach(t => t.style.display = "none");
    document.querySelectorAll(".tablinks").forEach(b => b.classList.remove("active"));
    document.getElementById(tabName).style.display = "block";
    evt.currentTarget.classList.add("active");
  }
</script>

</body>
</html>
