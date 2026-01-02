# resto-calculator
Сметни бързо рестото между левове и евро!
<!DOCTYPE html>
<html lang="bg">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ресто Калкулатор</title>
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">
  <style>
    body { font-family: Arial; background: #1e1e1e; color: white; padding: 20px; }
    h1 { text-align: center; margin-bottom: 20px; }
    .box { background: #2a2a2a; padding: 15px; border-radius: 10px; margin-bottom: 15px; }
    label { display: block; margin-bottom: 5px; }
    input, select, button { width: 100%; font-size: 24px; padding: 10px; margin-bottom: 10px; border-radius: 8px; border: none; }
    button { background: #4CAF50; color: white; font-weight: bold; }
    .clear { background: #f44336; }
    .result { font-size: 22px; text-align: center; margin-top: 10px; }
  </style>
</head>
<body>

<h1>Ресто Калкулатор</h1>

<div class="box">
  <label>Сума за плащане</label>
  <input id="total" type="number" step="0.01" placeholder="0.00">
  <select id="totalCurrency">
    <option value="BGN">Лева (BGN)</option>
    <option value="EUR">Евро (EUR)</option>
  </select>
</div>

<div class="box">
  <label>Дадена сума</label>
  <input id="paid" type="number" step="0.01" placeholder="0.00">
  <select id="paidCurrency">
    <option value="BGN">Лева (BGN)</option>
    <option value="EUR">Евро (EUR)</option>
  </select>
</div>

<button onclick="calculate()">ИЗЧИСЛИ</button>
<button class="clear" onclick="clearAll()">НОВА СМЕТКА</button>

<div class="box result" id="result"></div>

<script>
  const RATE = 1.95583;

  function toBGN(amount, currency) { return currency==='EUR'? amount*RATE : amount; }

  function calculate() {
    const total = parseFloat(document.getElementById('total').value) || 0;
    const paid = parseFloat(document.getElementById('paid').value) || 0;
    const totalCur = document.getElementById('totalCurrency').value;
    const paidCur = document.getElementById('paidCurrency').value;
    const totalBGN = toBGN(total, totalCur);
    const paidBGN = toBGN(paid, paidCur);
    const changeBGN = paidBGN - totalBGN;
    if(changeBGN<0) { document.getElementById('result').innerHTML='❗ Недостатъчна сума'; return; }
    const changeEUR = changeBGN/RATE;
    document.getElementById('result').innerHTML = `<strong>${changeBGN.toFixed(2)} лв</strong><br><strong>${changeEUR.toFixed(2)} €</strong>`;
  }

  function clearAll() {
    document.getElementById('total').value='';
    document.getElementById('paid').value='';
    document.getElementById('result').innerHTML='';
  }
</script>

</body>
</html>
