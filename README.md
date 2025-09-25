
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>String List</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; background-color: #fff; }
    h1 { color: #041E42; text-align: center; margin-bottom: 10px; }
    h3 { color: #041E42; text-align: center; margin-bottom: 20px; font-size: 1.2em; }
    p { text-align: center; color: #041E42; margin-bottom: 20px; }
    #searchInput { width: 100%; padding: 10px; margin-bottom: 20px; border: 1px solid #ddd; border-radius: 4px; font-size: 16px; }
    table { border-collapse: collapse; width: 100%; margin-bottom: 20px; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
    th { background-color: #041E42; color: #fff; cursor: pointer; }
    th:hover { background-color: #003087; }
    .sort-arrow { margin-left: 5px; }
    .review { display: none; margin-top: 5px; padding: 5px; border: 1px solid #ccc; background: #f9f9f9; max-width: 300px; }
    a { color: #0066cc; text-decoration: none; }
    a:hover { text-decoration: underline; }
    .hidden-row { display: none; }
    /* Media Queries for Responsiveness */
    @media (max-width: 767px) { /* iPhones/Mobile */
      table { overflow-x: auto; display: block; width: 100%; }
      th, td { font-size: 0.75em; padding: 3px; min-width: 80px; white-space: nowrap; }
      .review { max-width: 90%; left: 5%; }
    }
    @media (min-width: 768px) and (max-width: 1023px) { /* Tablets */
      th, td { padding: 6px; font-size: 0.9em; }
    }
    @media (min-width: 1024px) { /* Desktops */
      /* No changes needed, full table layout */
    }
  </style>
</head>
<body>
  <h1>String List</h1>
  <h3>V092225O</h3>
  <p>Available strings, sort by name or type. We can split sets for a hybrid string job. You provide strings, $20, or pick from below, $25. Currently stringing on a Gamma ELS 7500 stringer, 50 years of experience. String comments, type, and current availability derived by AI.</p>

  <input type="text" id="searchInput" placeholder="Search by name or type..." onkeyup="searchTable()">

  <table id="stringTable">
    <thead>
      <tr>
        <th onclick="sortTable(1)">String Name<span id="sortNameArrow" class="sort-arrow"></span></th>
        <th onclick="sortTable(2)">Type<span id="sortTypeArrow" class="sort-arrow"></span></th>
        <th>Available</th>
        <th>MSRP (Set)</th>
        <th>Comfort Rating</th>
        <th>Durability</th>
        <th>Spin Potential</th>
      </tr>
    </thead>
    <tbody>
      <!-- Strings will be loaded here -->
    </tbody>
  </table>

  <script>
    let strings = [
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

    // Default sort by String Name (ascending)
    strings.sort((a, b) => a.name.localeCompare(b.name));

    let sortDirection = { 1: 'asc', 2: 'asc' }; // Initial sort direction

    function renderTable() {
      const tbody = document.querySelector('#stringTable tbody');
      const thead = document.querySelector('#stringTable thead');
      tbody.innerHTML = '';
      strings.forEach((str, index) => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td><a href="#" onclick="showReview('${str.name}', event); return false;">${str.name}</a><div class="review" id="review-${str.name.replace(/ /g, '-')}" style="display:none;"></div></td>
          <td>${str.type}</td>
          <td>${str.available}</td>
          <td>${str.msrp}</td>
          <td>${str.comfort}</td>
          <td>${str.durability}</td>
          <td>${str.spin}</td>
        `;
        tbody.appendChild(tr);
      });
      updateSortArrows();
    }

    function sortTable(columnIndex) {
      const direction = sortDirection[columnIndex] === 'asc' ? 'desc' : 'asc';
      sortDirection[columnIndex] = direction;

      strings.sort((a, b) => {
        const valueA = columnIndex === 1 ? a.name.toLowerCase() : a.type.toLowerCase();
        const valueB = columnIndex === 1 ? b.name.toLowerCase() : b.type.toLowerCase();
        return direction === 'asc' ? valueA.localeCompare(valueB) : valueB.localeCompare(valueA);
      });

      renderTable();
    }

    function updateSortArrows() {
      const nameArrow = document.getElementById('sortNameArrow');
      const typeArrow = document.getElementById('sortTypeArrow');
      nameArrow.textContent = sortDirection[1] === 'asc' ? ' ↑' : ' ↓';
      typeArrow.textContent = sortDirection[2] === 'asc' ? ' ↑' : ' ↓';
    }

    function showReview(stringName, event) {
      event.preventDefault();
      const reviewId = `review-${stringName.replace(/ /g, '-')}`;
      const reviewDiv = document.getElementById(reviewId);
      if (reviewDiv.style.display === 'none') {
        let reviewText = '';
        switch (stringName) {
          case 'Asics Resolution 16': reviewText = 'Asics Resolution 16, a synthetic gut string from Asics, provides a balanced feel with good comfort and power. Limited feedback suggests it’s a solid all-around option.'; break;
          case 'Babolat Conquest': reviewText = 'Babolat Conquest, a synthetic gut from Babolat, offers strong comfort and durability. Users enjoy its playability, though it’s less spin-focused than polys.'; break;
          case 'Babolat N.Vy': reviewText = 'Babolat N.Vy, a synthetic gut from Babolat, offers a soft, arm-friendly feel with decent power. Limited availability makes it a niche choice, with users noting good value.'; break;
          case 'Babolat Excel': reviewText = 'Babolat Excel, a multifilament from Babolat, shines with comfort and power, mimicking natural gut. Reviews praise its plush feel, though durability is moderate for frequent play.'; break;
          case 'Bluestar Multi Filament': reviewText = 'Bluestar Multi Filament, a multifilament, offers a soft, gut-like feel with excellent power. Users praise its comfort, though durability is average.'; break;
          case 'Gamma Octo TNT': reviewText = 'Gamma Octo TNT, a synthetic gut from Gamma, is lauded for its all-around performance and durability. Reviews highlight a firm feel, great for aggressive players.'; break;
          case 'Head FXP': reviewText = 'Head FXP, a synthetic gut from Head, offers a balanced mix of power and control at a budget price. Users find it reliable for all-court play with decent durability.'; break;
          case 'Head FXP Tour': reviewText = 'Head FXP Tour, a synthetic gut from Head, provides enhanced comfort and control. Reviews highlight its versatility, though it’s less durable than polys.'; break;
          case 'Head Intellistring': reviewText = 'Head Intellistring, a synthetic gut from Head, offers a balanced play with moderate power. Limited stock feedback suggests it’s a solid, budget-friendly option.'; break;
          case 'Head Velocity MLT': reviewText = 'Head Velocity MLT, a multifilament from Head, is known for its soft, comfortable play and good power. Players appreciate its arm-friendliness, with solid tension retention.'; break;
          case 'Kirschbaum Super Smash': reviewText = 'Kirschbaum Super Smash, a polyester from Kirschbaum, is favored for its spin and durability. Players love its aggressive bite, though it’s stiffer on the arm.'; break;
          case 'Kirschbaum Synthetic Gut': reviewText = 'Kirschbaum Synthetic Gut, a budget synthetic from Kirschbaum, provides good power and comfort. Reviews highlight its value, with decent performance for casual play.'; break;
          case 'Prince Control 15': reviewText = 'Prince Control 15, a multifilament, excels in precision and comfort with a soft feel. Players note its playability, though durability is average.'; break;
          case 'Prince Tour XC': reviewText = 'Prince Tour XC, a polyester, offers great spin and control with solid durability. Users enjoy its crisp response, ideal for competitive baseline play.'; break;
          case 'Prince Synthetic Gut 15L': reviewText = 'Prince Synthetic Gut 15L, a synthetic gut from Prince, provides a lively response with decent comfort. Users note its affordability, though durability varies.'; break;
          case 'Prince Synthetic Gut with Duraflex': reviewText = 'Prince Synthetic Gut with Duraflex, a synthetic gut from Prince, delivers a soft feel with good power and durability. Reviews praise its value and all-around playability.'; break;
          case 'Tourna Premier Poly': reviewText = 'Tourna Premier Poly, a polyester from Tourna, offers good spin and durability. Reviews commend its value, though it may feel harsh for some players.'; break;
          case 'Wilson Extreme Octane': reviewText = 'Wilson Extreme Octane, a synthetic gut from Wilson, delivers a lively response with good control. Reviews note its affordability and decent durability.'; break;
          case 'Wilson Hollowcore 16': reviewText = 'Wilson Hollowcore 16, a synthetic gut from Wilson, provides a unique hollow design for power. Limited feedback suggests a soft, lively feel.'; break;
          case 'Wilson Hyperlast': reviewText = 'Wilson Hyperlast, a polyester from Wilson, offers control and durability. Users recall its firm feel.'; break;
          case 'Wilson NXT with Duramax 15': reviewText = 'Wilson NXT with Duramax 15, a multifilament from Wilson, combines plush comfort with enhanced durability. Players love its power and gut-like response.'; break;
          case 'Wilson Poly Last': reviewText = 'Wilson Poly Last, a polyester from Wilson, offers solid control and durability, though its age may reduce elasticity. Users note a stiff feel, ideal for baseline play if stored well.'; break;
          case 'Wilson SGX': reviewText = 'Wilson SGX, a synthetic gut from Wilson, provides a balanced feel with vibrant colors. Users enjoy its versatility and budget-friendly price.'; break;
          case 'Wilson Shock Shield 16': reviewText = 'Wilson Shock Shield 16, a synthetic gut from Wilson, offers vibration dampening with a soft feel. Users appreciate its comfort, ideal for arm protection.'; break;
          case 'Wilson Shock Shield 17': reviewText = 'Wilson Shock Shield 17, a thinner synthetic gut from Wilson, provides similar comfort with added feel. Reviews note its effectiveness for sensitive arms.'; break;
          case 'Wilson Super Spin 16': reviewText = 'Wilson Super Spin 16, a multifilament from Wilson, excels in spin and comfort. Reviews highlight its hexagonal shape, though durability is limited.'; break;
          case 'Wilson Synthetic Gut Extreme': reviewText = 'Wilson Synthetic Gut Extreme, a synthetic gut from Wilson, offers a crisp, durable play. Users praise its value and all-court performance.'; break;
          default: reviewText = 'No detailed review available for this string.';
        }
        reviewDiv.textContent = reviewText;
        reviewDiv.style.display = 'block';
      } else {
        reviewDiv.style.display = 'none';
      }
    }

    function searchTable() {
      const input = document.getElementById('searchInput').value.toLowerCase();
      const rows = document.querySelectorAll('#stringTable tbody tr');
      rows.forEach(row => {
        const name = row.cells[0].textContent.toLowerCase();
        const type = row.cells[1].textContent.toLowerCase();
        if (name.includes(input) || type.includes(input)) {
          row.classList.remove('hidden-row');
        } else {
          row.classList.add('hidden-row');
        }
      });
    }

    renderTable();
  </script>


  <table>
    <tr>
        <th>#</th>
        <th>Player</th>
        <th>Tour</th>
        <th>Racket Model</th>
        <th>String Setup</th>
        <th>Tension (lbs)</th>
    </tr>
    <tr><td>1</td><td>Carlos Alcaraz</td><td>ATP</td><td>Babolat Pure Aero 98</td><td>Babolat RPM Blast (poly)</td><td>50/52</td></tr>
    <tr><td>2</td><td>Jannik Sinner</td><td>ATP</td><td>Head Speed Pro</td><td>Head Hawk Touch (poly)</td><td>58/60</td></tr>
    <tr><td>3</td><td>Novak Djokovic</td><td>ATP</td><td>Head Speed Pro (custom)</td><td>Babolat Natural Gut mains / Luxilon ALU Power Rough crosses</td><td>59/56</td></tr>
    <tr><td>4</td><td>Alexander Zverev</td><td>ATP</td><td>Head Gravity Pro</td><td>Head Hawk (poly)</td><td>53/55</td></tr>
    <tr><td>5</td><td>Daniil Medvedev</td><td>ATP</td><td>Tecnifibre T-Fight 305</td><td>Tecnifibre Razor Code (poly)</td><td>52/54</td></tr>
    <tr><td>6</td><td>Andrey Rublev</td><td>ATP</td><td>Head YouTek IG Speed MP</td><td>Head Hawk Touch (poly)</td><td>55/57</td></tr>
    <tr><td>7</td><td>Casper Ruud</td><td>ATP</td><td>Yonex EZONE 98</td><td>Yonex Poly Tour Pro (poly)</td><td>54/54</td></tr>
    <tr><td>8</td><td>Hubert Hurkacz</td><td>ATP</td><td>Wilson Blade 98 v9 (18x20)</td><td>Luxilon ALU Power (poly)</td><td>52/52</td></tr>
    <tr><td>9</td><td>Stefanos Tsitsipas</td><td>ATP</td><td>Wilson Blade 98 (custom black)</td><td>Luxilon RPM Team (poly)</td><td>50/52</td></tr>
    <tr><td>10</td><td>Holger Rune</td><td>ATP</td><td>Babolat Pure Aero VS</td><td>Babolat RPM Blast (poly)</td><td>48/50</td></tr>
    <tr><td>11</td><td>Grigor Dimitrov</td><td>ATP</td><td>Wilson Pro Staff RF97 Autograph</td><td>Wilson Natural Gut mains / Luxilon ALU Rough crosses</td><td>55/52</td></tr>
    <tr><td>12</td><td>Alex de Minaur</td><td>ATP</td><td>Wilson Blade 98</td><td>Luxilon ALU Power Soft (poly)</td><td>51/53</td></tr>
    <tr><td>13</td><td>Taylor Fritz</td><td>ATP</td><td>Dunlop CX 200 Tour</td><td>Solinco Confidential (poly)</td><td>50/50</td></tr>
    <tr><td>14</td><td>Tommy Paul</td><td>ATP</td><td>Wilson Blade 98 v9</td><td>Luxilon ALU Power (poly)</td><td>52/52</td></tr>
    <tr><td>15</td><td>Frances Tiafoe</td><td>ATP</td><td>Yonex VCORE Pro 97</td><td>Yonex Poly Tour Pro (poly)</td><td>42/42</td></tr>
    <tr><td>16</td><td>Ben Shelton</td><td>ATP</td><td>Yonex EZONE 98</td><td>Yonex Poly Tour Fire (poly)</td><td>48/50</td></tr>
    <tr><td>17</td><td>Ugo Humbert</td><td>ATP</td><td>Head Gravity MP</td><td>Head Hawk Touch (poly)</td><td>53/55</td></tr>
    <tr><td>18</td><td>Arthur Fils</td><td>ATP</td><td>Babolat Pure Drive 98</td><td>Babolat RPM Blast (poly)</td><td>50/52</td></tr>
    <tr><td>19</td><td>Jack Draper</td><td>ATP</td><td>Wilson Pro Staff 97</td><td>Luxilon ALU Power (poly)</td><td>52/54</td></tr>
    <tr><td>20</td><td>Sebastian Korda</td><td>ATP</td><td>Wilson Blade 98</td><td>Solinco Hyper-G Soft (poly)</td><td>51/53</td></tr>
    <tr><td>21</td><td>Iga Swiatek</td><td>WTA</td><td>Yonex EZONE 98</td><td>Luxilon ALU Power Rough (poly)</td><td>52/52</td></tr>
    <tr><td>22</td><td>Aryna Sabalenka</td><td>WTA</td><td>Wilson Blade 98 v9</td><td>Luxilon ALU Power (poly)</td><td>50/50</td></tr>
    <tr><td>23</td><td>Coco Gauff</td><td>WTA</td><td>Head Aurora Pro</td><td>Head Lynx Tour (poly)</td><td>51/53</td></tr>
    <tr><td>24</td><td>Elena Rybakina</td><td>WTA</td><td>Yonex EZONE 98</td><td>Yonex Poly Tour Pro (poly)</td><td>53/55</td></tr>
    <tr><td>25</td><td>Jasmine Paolini</td><td>WTA</td><td>Yonex VCORE 100</td><td>Yonex Poly Tour Spin (poly)</td><td>52/54</td></tr>
    <tr><td>26</td><td>Qinwen Zheng</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon ALU Power (poly)</td><td>50/52</td></tr>
    <tr><td>27</td><td>Mirra Andreeva</td><td>WTA</td><td>Wilson Blade 98 v9</td><td>Luxilon ALU Power Soft (poly)</td><td>49/51</td></tr>
    <tr><td>28</td><td>Danielle Collins</td><td>WTA</td><td>Wilson Clash 100</td><td>Wilson NXT (multi)</td><td>55/55</td></tr>
    <tr><td>29</td><td>Anna Kalinskaya</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon RPM Blast (poly)</td><td>51/53</td></tr>
    <tr><td>30</td><td>Madison Keys</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon ALU Power (poly)</td><td>52/52</td></tr>
    <tr><td>31</td><td>Beatriz Haddad Maia</td><td>WTA</td><td>Wilson Clash 100</td><td>Wilson NXT Duramax (multi)</td><td>54/54</td></tr>
    <tr><td>32</td><td>Diana Shnaider</td><td>WTA</td><td>Babolat Pure Aero 98</td><td>Babolat RPM Blast (poly)</td><td>50/52</td></tr>
    <tr><td>33</td><td>Emma Navarro</td><td>WTA</td><td>Wilson Blade 98 v9</td><td>Luxilon ALU Power (poly)</td><td>51/53</td></tr>
    <tr><td>34</td><td>Ons Jabeur</td><td>WTA</td><td>Wilson Blade 98</td><td>Wilson NXT (multi)</td><td>53/55</td></tr>
    <tr><td>35</td><td>Barbora Krejcikova</td><td>WTA</td><td>Yonex VCORE Pro 97</td><td>Yonex Poly Tour Pro (poly)</td><td>52/52</td></tr>
    <tr><td>36</td><td>Elina Svitolina</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon ALU Power Rough (poly)</td><td>50/50</td></tr>
    <tr><td>37</td><td>Maria Sakkari</td><td>WTA</td><td>Wilson Blade 98 v9</td><td>Luxilon ALU Power (poly)</td><td>51/51</td></tr>
    <tr><td>38</td><td>Daria Kasatkina</td><td>WTA</td><td>Diadem Forge 7</td><td>Diadem Evolution (poly)</td><td>49/51</td></tr>
    <tr><td>39</td><td>Karolina Muchova</td><td>WTA</td><td>Head Gravity Pro</td><td>Head Hawk Touch (poly)</td><td>52/54</td></tr>
    <tr><td>40</td><td>Jessica Pegula</td><td>WTA</td><td>Yonex EZONE 98</td><td>Yonex Poly Tour Fire (poly)</td><td>50/52</td></tr>
    <tr><td>41</td><td>Paula Badosa</td><td>WTA</td><td>Wilson Clash 100</td><td>Luxilon ALU Power (poly)</td><td>53/55</td></tr>
    <tr><td>42</td><td>Zheng Qinwen</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon ALU Power (poly)</td><td>50/52</td></tr>
    <tr><td>43</td><td>Marketa Vondrousova</td><td>WTA</td><td>Wilson Pro Staff 97</td><td>Wilson NXT (multi)</td><td>54/54</td></tr>
    <tr><td>44</td><td>Linda Noskova</td><td>WTA</td><td>Yonex EZONE 98</td><td>Yonex Poly Tour Pro (poly)</td><td>51/53</td></tr>
    <tr><td>45</td><td>Elise Mertens</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon ALU Power Soft (poly)</td><td>52/52</td></tr>
    <tr><td>46</td><td>Donna Vekic</td><td>WTA</td><td>Head Gravity MP</td><td>Head Hawk (poly)</td><td>53/55</td></tr>
    <tr><td>47</td><td>Petra Kvitova</td><td>WTA</td><td>Wilson Pro Staff RF97 Autograph</td><td>Luxilon ALU Power Rough (poly)</td><td>55/52</td></tr>
    <tr><td>48</td><td>Victoria Azarenka</td><td>WTA</td><td>Wilson Aura Pro</td><td>Wilson Natural Gut mains / Luxilon ALU crosses</td><td>56/53</td></tr>
    <tr><td>49</td><td>Sofia Kenin</td><td>WTA</td><td>Wilson Blade 98</td><td>Luxilon RPM Team (poly)</td><td>50/50</td></tr>
    <tr><td>50</td><td>Anastasija Sevastova</td><td>WTA</td><td>Wilson Blade 98 v9</td><td>Wilson NXT (multi)</td><td>52/54</td></tr>
</table>

<style>
    table {
        width: 80%;
        margin: 20px auto;
        border-collapse: collapse;
        font-family: Arial, sans-serif;
    }
    th, td {
        border: 1px solid #ddd;
        padding: 8px;
        text-align: left;
    }
    th {
        background-color: #f2f2f2;
        color: #333;
    }
    tr:nth-child(even) {
        background-color: #f9f9f9;
    }
    tr:hover {
        background-color: #f5f5f5;
    }
</style>
</body>
</html>
