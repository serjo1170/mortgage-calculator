[index.html.txt](https://github.com/user-attachments/files/26322470/index.html.txt)
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Mortgage Calculator USA</title>
<style>
body { font-family: Arial; max-width: 500px; margin: auto; padding:20px;}
input, button { width:100%; padding:10px; margin:5px 0;}
button { background:#222; color:white; cursor:pointer;}
</style>
</head>
<body>

<h2>Mortgage Calculator 🇺🇸</h2>

<input id="amount" placeholder="Loan Amount ($)">
<input id="rate" placeholder="Interest Rate (%)">
<input id="years" placeholder="Years">

<button onclick="calc()">Calculate</button>

<h3 id="result"></h3>

<script>
function calc() {
  let P = parseFloat(amount.value);
  let r = parseFloat(rate.value)/100/12;
  let n = parseFloat(years.value)*12;

  let M = P * (r*Math.pow(1+r,n)) / (Math.pow(1+r,n)-1);

  if (!isFinite(M)) {
    result.innerText = "Enter valid numbers";
  } else {
    result.innerText = "Monthly Payment: $" + M.toFixed(2);
  }
}
</script>

</body>
</html>
