
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
    table { border-collapse: collapse; width: 100%; margin-bottom: 20px; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: left; position: relative; }
    th { background-color: #041E42; color: #fff; cursor: pointer; }
    th:hover { background-color: #003087; }
    .sort-arrow { margin-left: 5px; }
    .review { display: none; position: absolute; top: 100%; left: 0; padding: 5px; border: 1px solid #ccc; background: #f9f9f9; max-width: 250px; max-height: 150px; overflow-y: auto; z-index: 1; }
    a { color: #0066cc; text-decoration: none; }
    a:hover { text-decoration: underline; }
    /* Media Queries for Responsiveness */
    @media (max-width: 767px) { /* iPhones/Mobile */
      table { overflow-x: auto; display: block; }
      th, td { font-size: 0.8em; padding: 4px; min-width: 100px; }
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
  <h3>V091425J</h3>
  <p>Available strings, sort by name or type. We can split sets for a hybrid string job.<br>You provide strings, $20, or pick from below, $25.  Currently stringing on a Gamma ELS 7500 stringer, 50 years of experience.  </p>

  <table id="stringTable">
    <thead>
      <tr>
        <th onclick="sortTable(1)">String Name<span id="sortNameArrow" class="sort-arrow"></span></th>
        <th onclick="sortTable(2)">Type<span id="sortTypeArrow" class="sort-arrow"></span></th>
        <th>Available</th>
        <th>MSRP (Set)</th>
      </tr>
    </thead>
    <tbody>
      <!-- Strings will be loaded here -->
    </tbody>
  </table>

  <script>
    let strings = [
      { name: "Asics Resolution 16", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Babolat Conquest", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Babolat N.Vy", type: "Synthetic Gut", available: "Limited", msrp: "$25" },
      { name: "Babolat Excel", type: "Multifilament", available: "Yes", msrp: "$25" },
      { name: "Bluestar Multi Filament", type: "Multifilament", available: "Yes", msrp: "$25" },
      { name: "Gamma Octo TNT", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Head FXP", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Head FXP Tour", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Head Intellistring", type: "Synthetic Gut", available: "Limited", msrp: "$25" },
      { name: "Head Velocity MLT", type: "Multifilament", available: "Yes", msrp: "$25" },
      { name: "Kirschbaum Super Smash", type: "Polyester", available: "Yes", msrp: "$25" },
      { name: "Kirschbaum Synthetic Gut", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Prince Control 15", type: "Multifilament", available: "Yes", msrp: "$25" },
      { name: "Prince Tour XC", type: "Polyester", available: "Yes", msrp: "$25" },
      { name: "Prince Synthetic Gut 15L", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Prince Synthetic Gut with Duraflex", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Tourna Premier Poly", type: "Polyester", available: "Yes", msrp: "$25" },
      { name: "Wilson Extreme Octane", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Wilson Hollowcore 16", type: "Synthetic Gut", available: "Limited", msrp: "$25" },
      { name: "Wilson Hyperlast", type: "Polyester", available: "No", msrp: "$25" },
      { name: "Wilson NXT with Duramax 15", type: "Multifilament", available: "Yes", msrp: "$25" },
      { name: "Wilson Poly Last", type: "Polyester", available: "No", msrp: "$25" },
      { name: "Wilson SGX", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Wilson Shock Shield 16", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Wilson Shock Shield 17", type: "Synthetic Gut", available: "Yes", msrp: "$25" },
      { name: "Wilson Super Spin 16", type: "Multifilament", available: "No", msrp: "$25" },
      { name: "Wilson Synthetic Gut Extreme", type: "Synthetic Gut", available: "Yes", msrp: "$25" }
    ];

    // Default sort by String Name (ascending)
    strings.sort((a, b) => a.name.localeCompare(b.name));

    let sortDirection = { 1: 'asc', 2: 'asc' }; // Initial sort direction

    function renderTable() {
      const tbody = document.querySelector('#stringTable tbody');
      tbody.innerHTML = '';
      strings.forEach((str, index) => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td><a href="#" onclick="showReview('${str.name}', event); return false;">${str.name}</a><div class="review" id="review-${str.name.replace(/ /g, '-')}" style="display:none;"></div></td>
          <td>${str.type}</td>
          <td>${str.available}</td>
          <td>${str.msrp}</td>
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

    renderTable();
  </script>
</body>
</html>
