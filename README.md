
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Brownies String Manager</title>
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
    .review { display: none; margin-top: 5px; padding: 5px; border: 1px solid #ccc; background: #f9f9f9; }
    a { color: #0066cc; text-decoration: none; }
    a:hover { text-decoration: underline; }
  </style>
</head>
<body>
  <h1>Brownies String Manager</h1>
  <p>Add, remove, or edit strings. Changes save locally in your browser.</p>

  <form id="addForm">
    <input type="text" id="stringName" placeholder="String Name" required>
    <select id="type">
      <option value="Multi">Multi</option>
      <option value="Syn">Syn</option>
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
      { name: "Babolat N.Vy", type: "Syn", available: "Limited", msrp: "$7.50 (est.)" },
      { name: "Babolat Excel", type: "Multi", available: "Yes", msrp: "$18.95" },
      { name: "Head Velocity MLT", type: "Multi", available: "Yes", msrp: "$11.95" },
      { name: "Head FXP", type: "Syn", available: "Yes", msrp: "$9.95" },
      { name: "Head FXP Tour", type: "Syn", available: "Yes", msrp: "$10.95" },
      { name: "Premier Control 15", type: "Poly", available: "Yes", msrp: "$13.95" },
      { name: "Premier Tour XC", type: "Poly", available: "Yes", msrp: "$14.95" },
      { name: "Prince Synthetic Gut with Duraflex", type: "Syn", available: "Yes", msrp: "$7.95" },
      { name: "Prince Synthetic Gut 15L", type: "Syn", available: "Yes", msrp: "$6.95" },
      { name: "Head Intellistring", type: "Syn", available: "Limited", msrp: "$8.50 (est.)" },
      { name: "Kirschbaum Super Smash", type: "Poly", available: "Yes", msrp: "$13.95" },
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

    function show
