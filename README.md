<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Data Unit</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px;
    }
    th {
      background-color: #f2f2f2;
    }
    caption {
      caption-side: top;
      font-size: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>

<h2>DATA UNIT TERBARU</h2>
<table id="csv-table">
  <caption>Daftar Unit</caption>
  <thead></thead>
  <tbody></tbody>
</table>

<script>
  async function loadCSV() {
    const response = await fetch('data.csv');
    const csvText = await response.text();

    const parsed = Papa.parse(csvText, {
      header: true,
      skipEmptyLines: true
    });

    const tableHead = document.querySelector("#csv-table thead");
    const tableBody = document.querySelector("#csv-table tbody");

    // Buat Header
    const headers = Object.keys(parsed.data[0]);
    const headerRow = document.createElement("tr");
    headers.forEach(header => {
      const th = document.createElement("th");
      th.textContent = header;
      headerRow.appendChild(th);
    });
    tableHead.appendChild(headerRow);

    // Buat Baris Data
    parsed.data.forEach(row => {
      const tr = document.createElement("tr");
      headers.forEach(header => {
        const td = document.createElement("td");
        td.textContent = row[header];
        tr.appendChild(td);
      });
      tableBody.appendChild(tr);
    });
  }

  loadCSV();
</script>

</body>
</html>
