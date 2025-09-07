<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>String Manager</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    table { border-collapse: collapse; width: 100%; margin-bottom: 20px; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; cursor: pointer; }
    th:hover { background-color: #ddd; }
    form { margin-bottom: 20px; }
    input[type="text"], select { margin-right: 10px; padding: 5px; }
    button { padding: 5px 10px; margin: 5px 0; }
    .remove-btn { background-color: #f44336; color: white; border: none; cursor: pointer; }
    .save-btn { background-color: #4CAF50; color: white; border: none; cursor: pointer; }
    .sort-arrow { margin-left: 5px; }
    .review { display: none; margin-top: 5px; padding: 5px; border: 1px solid #ccc; background: #f9f9f9; max-width: 300px; }
    a { color: #0066cc; text-decoration: none; }
    a:hover { text-decoration: underline; }
  </style>
</head>
<body>
  <h1> String Manager</h1>
  <p>Add, remove, or edit strings. Changes save locally in your browser.</p>

  <form id="addForm">
    <input type="text" id="stringName" placeholder="String Name" required>
    <select id="type">
      <option value="Multi">Multi</option>
      <option value="Syn">Synthetic</option>
      <option value="Poly">Poly</option>
      <option value="Natural Gut">Natural Gut</option>
    </select>
    <select id="available">
      <option value="Yes">Yes</option>
      <option value="No">No</option>
      <option value="Limited">Limited</option>
    </select>
    <input type="text" id="msrp" placeholder="MSRP (Set)" required>
    <button type="submit">Add String</button>
  </form>

  <table id="stringTable">
    <thead>
      <tr>
        <th>Checkbox</th>
        <th onclick="sortTable(1)">String Name<span id="sortNameArrow" class="sort-arrow"></span></th>
        <th onclick="sortTable(2)">Type<span id="sortTypeArrow" class="sort-arrow"></span></th>
        <th>Available</th>
        <th>MSRP (Set)</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <!-- Strings will be loaded here -->
    </tbody>
  </table>

  <button class="remove-btn" onclick="removeChecked()">Remove Checked</button>
  <button class="save-btn" onclick="saveChanges()">Save Changes</button>

  <script>
    let strings = JSON.parse(localStorage.getItem('timStringList')) || [
      { name: "Wilson Poly Last", type: "Poly", available: "No", msrp: "$8.00 (est.)" },
      { name: "Asics Resolution 16", type: "Poly", available: "Yes", msrp: "$12.95" },
      { name: "Gamma Octo TNT", type: "Poly", available: "Yes", msrp: "$14.95" },
      { name: "Babolat Conquest", type: "Poly", available: "Yes", msrp: "$15.95" },
      { name: "Babolat N.vy", type: "Syn", available: "Limited", msrp: "$7.50 (est.)" },
      { name: "Babolat Xcel", type: "Multi", available: "Yes", msrp: "$18.95" },
      { name: "Head Velocity MLT", type: "Multi", available: "Yes", msrp: "$11.95" },
      { name: "Head FXP", type: "Syn", available: "Yes", msrp: "$9.95" },
      { name: "Head FXP Tour", type: "Syn", available: "Yes", msrp: "$10.95" },
      { name: "Premier Control 15", type: "Poly", available: "Yes", msrp: "$13.95" },
      { name: "Premier Tour XC", type: "Poly", available: "Yes", msrp: "$14.95" },
      { name: "Prince Synthetic Gut with Duraflex", type: "Syn", available: "Yes", msrp: "$7.95" },
      { name: "Prince Synthetic Gut 15L", type: "Syn", available: "Yes", msrp: "$6.95" },
      { name: "Head Intellistring", type: "Syn", available: "Limited", msrp: "$8.50 (est.)" },
      { name: "Kirschbaum Super Smash", type: "Multi", available: "Yes", msrp: "$13.95" },
      { name: "Kirschbaum Synthetic Gut", type: "Syn", available: "Yes", msrp: "$6.50" },
      { name: "Bluestar Multi Filament", type: "Multi", available: "Yes", msrp: "$17.95" },
      { name: "Tourna Premier Poly", type: "Poly", available: "Yes", msrp: "$12.95" },
      { name: "Wilson Shock Shield 16", type: "Syn", available: "Yes", msrp: "$8.95" },
      { name: "Wilson Shock Shield 17", type: "Syn", available: "Yes", msrp: "$8.95" },
      { name: "Wilson NXT with Duramax 15", type: "Multi", available: "Yes", msrp: "$21.95" },
      { name: "Wilson Hyperlast", type: "Poly", available: "No", msrp: "$9.00 (est.)" },
      { name: "Wilson Super Spin 16", type: "Multi", available: "No", msrp: "$10.00 (est.)" },
      { name: "Wilson Hollowcore 16", type: "Syn", available: "Limited", msrp: "$7.50 (est.)" },
      { name: "Wilson Synthetic Gut Extreme", type: "Syn", available: "Yes", msrp: "$7.95" },
      { name: "Wilson Extreme Octane", type: "Syn", available: "Yes", msrp: "$7.50" },
      { name: "Wilson SGX", type: "Syn", available: "Yes", msrp: "$7.95" }
    ];

    let sortDirection = { 1: 'asc', 2: 'asc' }; // Column 1 (Name), Column 2 (Type)

    function renderTable() {
      const tbody = document.querySelector('#stringTable tbody');
      tbody.innerHTML = '';
      strings.forEach((str, index) => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td><input type="checkbox" class="checkbox" data-index="${index}"></td>
          <td><a href="#" onclick="showReview('${str.name}', event); return false;">${str.name}</a><div class="review" id="review-${str.name.replace(/ /g, '-')}" style="display:none;"></div></td>
          <td contenteditable="true" data-field="type">${str.type}</td>
          <td contenteditable="true" data-field="available">${str.available}</td>
          <td contenteditable="true" data-field="msrp">${str.msrp}</td>
          <td><button onclick="deleteRow(${index})">Delete</button></td>
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
        if (direction === 'asc') {
          return valueA.localeCompare(valueB);
        } else {
          return valueB.localeCompare(valueA);
        }
      });

      localStorage.setItem('timStringList', JSON.stringify(strings));
      renderTable();
    }

    function updateSortArrows() {
      const nameArrow = document.getElementById('sortNameArrow');
      const typeArrow = document.getElementById('sortTypeArrow');
      nameArrow.textContent = sortDirection[1] === 'asc' ? ' ↑' : ' ↓';
      typeArrow.textContent = sortDirection[2] === 'asc' ? ' ↑' : ' ↓';
    }

    function addString(e) {
      e.preventDefault();
      const newString = {
        name: document.getElementById('stringName').value,
        type: document.getElementById('type').value,
        available: document.getElementById('available').value,
        msrp: document.getElementById('msrp').value
      };
      strings.push(newString);
      localStorage.setItem('timStringList', JSON.stringify(strings));
      renderTable();
      addForm.reset();
    }

    function removeChecked() {
      const checkboxes = document.querySelectorAll('.checkbox:checked');
      const indices = Array.from(checkboxes).map(cb => parseInt(cb.dataset.index)).sort((a, b) => b - a);
      indices.forEach(index => strings.splice(index, 1));
      localStorage.setItem('timStringList', JSON.stringify(strings));
      renderTable();
    }

    function deleteRow(index) {
      strings.splice(index, 1);
      localStorage.setItem('timStringList', JSON.stringify(strings));
      renderTable();
    }

    function saveChanges() {
      const rows = document.querySelectorAll('#stringTable tbody tr');
      rows.forEach((row, index) => {
        const fields = row.querySelectorAll('[data-field]');
        fields.forEach(field => {
          strings[index][field.dataset.field] = field.textContent.trim();
        });
      });
      localStorage.setItem('timStringList', JSON.stringify(strings));
      alert('Changes saved!');
    }

    function showReview(stringName, event) {
      event.preventDefault();
      const reviewId = `review-${stringName.replace(/ /g, '-')}`;
      const reviewDiv = document.getElementById(reviewId);
      if (reviewDiv.style.display === 'none') {
        let reviewText = '';
        switch (stringName) {
          case 'Wilson Poly Last':
            reviewText = 'Wilson Poly Last, a discontinued polyester, offers solid control and durability, Users note a stiff feel, ideal for baseline play if stored well.';
            break;
          case 'Asics Resolution 16':
            reviewText = 'Asics Resolution 16, a polyester string, delivers excellent spin and control with decent durability. Players praise its crisp response, though it may feel harsh for some.';
            break;
          case 'Gamma Octo TNT':
            reviewText = 'Gamma Octo TNT, an octagonal polyester, is lauded for its spin potential and durability. Reviews highlight a firm feel, great for aggressive players seeking precision.';
            break;
          case 'Babolat Conquest':
            reviewText = 'Babolat Conquest, a polyester, provides strong control and spin with good tension maintenance. Users enjoy its bite, though it’s less arm-friendly for long sessions.';
            break;
          case 'Babolat N.vy':
            reviewText = 'Babolat N.Vy, a synthetic gut, offers a soft, arm-friendly feel with decent power. Limited availability makes it a niche choice, with users noting good value.';
            break;
          case 'Babolat Excel':
            reviewText = 'Babolat Excel, a multifilament, shines with comfort and power, mimicking natural gut. Reviews praise its plush feel, though durability is moderate for frequent play.';
            break;
          case 'Head Velocity MLT':
            reviewText = 'Head Velocity MLT, a multifilament, is known for its soft, comfortable play and good power. Players appreciate its arm-friendliness, with solid tension retention.';
            break;
          case 'Head FXP':
            reviewText = 'Head FXP, a synthetic gut, offers a balanced mix of power and control at a budget price. Users find it reliable for all-court play with decent durability.';
            break;
          case 'Head FXP Tour':
            reviewText = 'Head FXP Tour, an upgraded synthetic gut, provides enhanced comfort and control. Reviews highlight its versatility, though it’s less durable than polys.';
            break;
          case 'Premier Control 15':
            reviewText = 'Premier Control 15, a polyester, excels in precision and spin with a firm feel. Players note its durability, though it may lack power for some styles.';
            break;
          case 'Premier Tour XC':
            reviewText = 'Premier Tour XC, a polyester, offers great spin and control with solid durability. Users enjoy its crisp response, ideal for competitive baseline play.';
            break;
          case 'Prince Synthetic Gut with Duraflex':
            reviewText = 'Prince Synthetic Gut with Duraflex, a synthetic gut, delivers a soft feel with good power and durability. Reviews praise its value and all-around playability.';
            break;
          case 'Prince Synthetic Gut 15L':
            reviewText = 'Prince Synthetic Gut 15L, a heavier synthetic gut, provides a lively response with decent comfort. Users note its affordability, though durability varies.';
            break;
          case 'Head Intellistring':
            reviewText = 'Head Intellistring, a synthetic gut, offers a balanced play with moderate power. Limited stock feedback suggests it’s a solid, budget-friendly option.';
            break;
          case 'Kirschbaum Super Smash':
            reviewText = 'Kirschbaum Super Smash, a polyester, is favored for its spin and durability. Players love its aggressive bite, though it’s stiffer on the arm.';
            break;
          case 'Kirschbaum Synthetic Gut':
            reviewText = 'Kirschbaum Synthetic Gut, a budget synthetic, provides good power and comfort. Reviews highlight its value, with decent performance for casual play.';
            break;
          case 'Bluestar Multi Filament':
            reviewText = 'Bluestar Multi Filament, a multifilament, offers a soft, gut-like feel with excellent power. Users praise its comfort, though durability is average.';
            break;
          case 'Tourna Poly Premier':
            reviewText = 'Tourna Poly Premier, a polyester, delivers solid spin and control at a low cost. Players note its firmness, great for budget-conscious spin seekers.';
            break;
          case 'Tourna Premier Poly':
            reviewText = 'Tourna Premier Poly, a polyester, provides good spin and durability. Reviews commend its value, though it may feel harsh for some players.';
            break;
          case 'Wilson Shock Shield 16':
            reviewText = 'Wilson Shock Shield 16, a synthetic gut, offers vibration dampening with a soft feel. Users appreciate its comfort, ideal for arm protection.';
            break;
          case 'Wilson Shock Shield 17':
            reviewText = 'Wilson Shock Shield 17, a thinner synthetic gut, provides similar comfort with added feel. Reviews note its effectiveness for sensitive arms.';
            break;
          case 'Wilson NXT with Duramax 15':
            reviewText = 'Wilson NXT with Duramax 15, a multifilament, combines plush comfort with enhanced durability. Players love its power and gut-like response.';
            break;
          case 'Wilson Hyperlast':
            reviewText = 'Wilson Hyperlast, a discontinued polyester, offers control and durability. Users recall its firm feel, though age may affect performance.';
            break;
          case 'Wilson Super Spin 16':
            reviewText = 'Wilson Super Spin 16, a discontinued multifilament, excels in spin and comfort. Reviews highlight its hexagonal shape, though durability is limited.';
            break;
          case 'Wilson Hollowcore 16':
            reviewText = 'Wilson Hollowcore 16, a synthetic gut, provides a unique hollow design for power. Limited feedback suggests a soft, lively feel.';
            break;
          case 'Wilson Synthetic Gut Extreme':
            reviewText = 'Wilson Synthetic Gut Extreme, a synthetic gut, offers a crisp, durable play. Users praise its value and all-court performance.';
            break;
          case 'Wilson Extreme Octane':
            reviewText = 'Wilson Extreme Octane, a synthetic gut, delivers a lively response with good control. Reviews note its affordability and decent durability.';
            break;
          case 'Wilson SGX':
            reviewText = 'Wilson SGX, a synthetic gut, provides a balanced feel with vibrant colors. Users enjoy its versatility and budget-friendly price.';
            break;
          default:
            reviewText = 'No detailed review available for this string.';
        }
        reviewDiv.textContent = reviewText;
        reviewDiv.style.display = 'block';
      } else {
        reviewDiv.style.display = 'none';
      }
    }

    const addForm = document.getElementById('addForm');
    addForm.addEventListener('submit', addString);

    renderTable();
  </script>
</body>
</html>
