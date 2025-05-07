# Room-Log
ate
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Daily Room Cleaning Log</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f9f9f9;
      padding: 20px;
      max-width: 600px;
      margin: auto;
    }
    h1 {
      text-align: center;
    }
    .day {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: white;
      padding: 10px;
      margin: 5px 0;
      border-radius: 5px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    }
    .date {
      font-weight: bold;
    }
    input[type="checkbox"] {
      transform: scale(1.2);
    }
    #reset {
      margin-top: 20px;
      display: block;
      width: 100%;
      padding: 10px;
      background: #e74c3c;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>🧹 Daily Room Cleaning Log</h1>
  <div id="log"></div>
  <button id="reset">Reset All</button>

  <script>
    const logContainer = document.getElementById("log");
    const startDate = new Date("2025-05-06");
    const days = 92; // 3 months: May 6 - Aug 5 (including leap year safety)

    for (let i = 0; i < days; i++) {
      const date = new Date(startDate);
      date.setDate(startDate.getDate() + i);
      const dateStr = date.toISOString().split("T")[0];

      const div = document.createElement("div");
      div.className = "day";

      const label = document.createElement("label");
      label.className = "date";
      label.textContent = date.toDateString();

      const checkbox = document.createElement("input");
      checkbox.type = "checkbox";
      checkbox.checked = localStorage.getItem(dateStr) === "true";

      checkbox.addEventListener("change", () => {
        localStorage.setItem(dateStr, checkbox.checked);
      });

      div.appendChild(label);
      div.appendChild(checkbox);
      logContainer.appendChild(div);
    }

    document.getElementById("reset").addEventListener("click", () => {
      if (confirm("Are you sure you want to reset all checkboxes?")) {
        for (let i = 0; i < days; i++) {
          const date = new Date(startDate);
          date.setDate(startDate.getDate() + i);
          const dateStr = date.toISOString().split("T")[0];
          localStorage.removeItem(dateStr);
        }
        location.reload();
      }
    });
  </script>
</body>
</html>
