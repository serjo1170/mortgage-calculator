
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Mortgage Calculator Pro</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body {
  margin:0;
  font-family: Arial;
  background:#f4f6f9;
}

.header {
  background: linear-gradient(135deg,#2c7be5,#00c6ff);
  color:white;
  text-align:center;
  padding:40px 20px;
}

.container {
  max-width:900px;
  margin:20px auto;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:20px;
}

.card {
  background:white;
  padding:20px;
  border-radius:12px;
  box-shadow:0 5px 20px rgba(0,0,0,0.1);
}

input {
  width:100%;
  padding:10px;
  margin:5px 0;
  border:1px solid #ddd;
  border-radius:6px;
}

button {
  width:100%;
  padding:12px;
  background:#2c7be5;
  color:white;
  border:none;
  border-radius:6px;
  cursor:pointer;
}

button:hover {
  background:#1a5edb;
}

.result {
  font-size:18px;
  margin-top:10px;
}

.cta {
  margin-top:15px;
  background:#28a745;
}

.footer {
  text-align:center;
  padding:20px;
  font-size:14px;
  color:#777;
}
</style>
</head>

<body>

<div class="header">
  <h1>🏡 Mortgage Calculator Pro</h1>
  <p>Plan smarter. Borrow better.</p>
</div>

<div class="container">

<div class="card">
  <h3>Loan Details</h3>
  <input id="amount" placeholder="Loan Amount ($)">
  <input id="rate" placeholder="Interest Rate (%)">
  <input id="years" placeholder="Loan Term (Years)">
  <input id="tax" placeholder="Property Tax (yearly $)">
  <input id="insurance" placeholder="Insurance (yearly $)">
  <button onclick="calc()">Calculate</button>

  <div class="result" id="result"></div>
  <button class="cta">Get Pre-Approved</button>
</div>

<div class="card">
  <h3>Payment Breakdown</h3>
  <canvas id="chart"></canvas>
</div>

</div>

<div class="footer">
  Estimates only. Not financial advice.
</div>

<script>
let chart;

function calc() {
  let P = parseFloat(amount.value);
  let r = parseFloat(rate.value)/100/12;
  let n = parseFloat(years.value)*12;
  let tax = parseFloat(tax.value)/12 || 0;
  let ins = parseFloat(insurance.value)/12 || 0;

  let M = P * (r*Math.pow(1+r,n)) / (Math.pow(1+r,n)-1);

  if (!isFinite(M)) {
    result.innerText = "Enter valid data";
    return;
  }

  let total = M + tax + ins;

  result.innerHTML =
    "Monthly: $" + total.toFixed(2) + "<br>" +
    "Principal & Interest: $" + M.toFixed(2);

  drawChart(M, tax, ins);
}

function drawChart(M, tax, ins) {
  let ctx = document.getElementById('chart').getContext('2d');

  if (chart) chart.destroy();

  chart = new Chart(ctx, {
    type: 'doughnut',
    data: {
      labels: ['Loan', 'Tax', 'Insurance'],
      datasets: [{
        data: [M, tax, ins]
      }]
    }
  });
}
</script>

</body>
</html>
