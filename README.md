
<html>
<head>
<meta charset="UTF-8">
<title>Mortgage Calculator USA</title>
<style>
body {
  font-family: Arial;
  background: #f5f7fa;
  padding: 20px;
}
.container {
  max-width: 500px;
  margin: auto;
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 5px 20px rgba(0,0,0,0.1);
}
h2 {
  text-align: center;
}
input {
  width: 100%;
  padding: 12px;
  margin: 8px 0;
  border: 1px solid #ddd;
  border-radius: 6px;
}
button {
  width: 100%;
  padding: 12px;
  background: #2c7be5;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}
button:hover {
  background: #1a5edb;
}
.result {
  margin-top: 15px;
  font-size: 18px;
  text-align: center;
}
</style>
</head>
<body>

<div class="container">
<h2>Mortgage Calculator 🇺🇸</h2>

<input id="amount" placeholder="Loan Amount ($)">
<input id="rate" placeholder="Interest Rate (%)">
<input id="years" placeholder="Loan Term (Years)">
<input id="tax" placeholder="Property Tax (yearly $)">
<input id="insurance" placeholder="Insurance (yearly $)">

<button onclick="calc()">Calculate Payment</button>

<div class="result" id="result"></div>
</div>

<script>
function calc() {
  let P = parseFloat(amount.value);
  let r = parseFloat(rate.value)/100/12;
  let n = parseFloat(years.value)*12;
  let tax = parseFloat(tax.value)/12 || 0;
  let ins = parseFloat(insurance.value)/12 || 0;

  let M = P * (r*Math.pow(1+r,n)) / (Math.pow(1+r,n)-1);

  if (!isFinite(M)) {
    result.innerText = "Please enter valid numbers";
  } else {
    let total = M + tax + ins;
    result.innerText =
      "Monthly Payment: $" + total.toFixed(2);
  }
}
</script>

</body>
</html>
