<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Attendance - BCA 2nd Semester</title>
  <style>
    body {
      font-family: Arial;
      padding: 20px;
    }
    table {
      width: 100%;
      margin-top: 20px;
      border-collapse: collapse;
    }
    th, td {
      padding: 10px;
      border: 1px solid #ccc;
    }
    th {
      background-color: #3498db;
      color: white;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: green;
      color: white;
      border: none;
      cursor: pointer;
    }
    select {
      padding: 5px;
      margin-right: 10px;
    }
  </style>
</head>
<body>

  <h1>Attendance - BCA 2nd Semester</h1>

  <label>Subject:
    <select id="subjectSelect">
      <option value="DM">Discrete Mathematics (DM)</option>
      <option value="DE">Digital Electronics (DE)</option>
      <option value="DS">Data Structure (DS)</option>
      <option value="PC">Professional Communication (PC)</option>
      <option value="PP">Python Programming (PP)</option>
      <option value="IS">Information System (IS)</option>
      <option value="ESEP(SS)">ESEP(SS)</option>
      <option value="ESEP(QAAR)">ESEP(QAAR)</option>
      <option value="PSY">Psychology</option>
    </select>
  </label>

  <label>Period:
    <select id="periodSelect">
      <option>8:25-9:25</option>
      <option>9:30-10:25</option>
      <option>10:35-11:25</option>
      <option>11:40-12:40</option>
      <option>12:40-1:10</option>
      <option>1:10-2:10</option>
      <option>2:15-3:15</option>
      <option>3:20-4:20</option>
    </select>
  </label>

  <table>
    <thead>
      <tr>
        <th>Roll No.</th>
        <th>Name</th>
        <th>Present</th>
      </tr>
    </thead>
    <tbody id="studentList"></tbody>
  </table>

  <button onclick="saveAttendance()">Save Attendance</button>

  <script>
    const students = [
      "Pranat Singh", "Ritika Singh", "Vardan Gupta", "Tejasav Rana", "Ashish Kannaujiya",
      "Palak Tiwari", "Shilpi Bajpai", "Shlok Awasthi", "Saurang", "Anshul Gupta",
      "Ayush Srivastav", "Vinayak Gupta", "Mahi Yadav", "Tulika Tiwari", "Harshita Dutt Lakheda",
      "Aman Singh", "Sahil Maurya"
    ];

    const tbody = document.getElementById("studentList");

    students.forEach((name, index) => {
      const row = document.createElement("tr");

      const rollTd = document.createElement("td");
      rollTd.textContent = index + 1;

      const nameTd = document.createElement("td");
      nameTd.textContent = name;

      const presentTd = document.createElement("td");
      const checkbox = document.createElement("input");
      checkbox.type = "checkbox";
      checkbox.dataset.name = name;
      checkbox.dataset.roll = index + 1;
      presentTd.appendChild(checkbox);

      row.appendChild(rollTd);
      row.appendChild(nameTd);
      row.appendChild(presentTd);
      tbody.appendChild(row);
    });

    function saveAttendance() {
      const subject = document.getElementById("subjectSelect").value;
      const period = document.getElementById("periodSelect").value;
      const today = new Date().toLocaleDateString("en-GB"); // dd-mm-yyyy

      let presentList = [];
      let absentList = [];

      const checkboxes = document.querySelectorAll("input[type='checkbox']");
      checkboxes.forEach(cb => {
        const entry = `${cb.dataset.roll}. ${cb.dataset.name}`;
        if (cb.checked) presentList.push(entry);
        else absentList.push(entry);
      });

      const content =
`Date: ${today} | Subject: ${subject} | Period: ${period}

Present:
${presentList.join(", ")}

Absent:
${absentList.join(", ")}
`;

      const blob = new Blob([content], { type: "text/plain" });
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = `Attendance_${today.replace(/\//g, '-')}_${subject}.txt`;
      link.click();
    }
  </script>

</body>
</html>
