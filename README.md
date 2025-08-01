# Mines
Qureshi mines prediction 
<!DOCTYPE html><html lang="ur" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>Qureshi Mines Prediction</title>
  <style>
    body {
      font-family: 'Noto Nastaliq Urdu', sans-serif;
      background-color: #121212;
      color: white;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #00ff99;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(5, 60px);
      gap: 10px;
      justify-content: center;
      margin: 20px 0;
    }
    .box {
      background-color: #333;
      border: 2px solid #555;
      padding: 20px;
      border-radius: 8px;
      font-size: 18px;
    }
    .safe {
      background-color: #0f0;
      color: black;
    }
    button {
      padding: 10px 20px;
      font-size: 18px;
      background-color: #00ff99;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    button:hover {
      background-color: #00cc77;
    }
  </style>
</head>
<body>
  <h1>قریشی مائنز پیشن گوئی</h1>
  <p>20 میں سے 5 سیف باکسز منتخب کریں - صرف تفریحی مقصد کے لیے</p>
  <div id="grid" class="grid"></div>
  <button onclick="predictSafeBoxes()">پیشگوئی کریں</button>
  <h2 id="result"></h2>  <script>
    const grid = document.getElementById('grid');

    function createGrid() {
      grid.innerHTML = '';
      for (let i = 1; i <= 20; i++) {
        const div = document.createElement('div');
        div.classList.add('box');
        div.innerText = i;
        div.id = 'box-' + i;
        grid.appendChild(div);
      }
    }

    function predictSafeBoxes() {
      createGrid();
      const totalBoxes = 20;
      const totalMines = 5;
      const safeToPredict = 5;

      const allBoxes = Array.from({ length: totalBoxes }, (_, i) => i + 1);
      const mines = [];
      while (mines.length < totalMines) {
        const mine = Math.floor(Math.random() * totalBoxes) + 1;
        if (!mines.includes(mine)) mines.push(mine);
      }

      const safeBoxes = allBoxes.filter(b => !mines.includes(b));
      const predictedSafe = [];
      while (predictedSafe.length < safeToPredict) {
        const choice = safeBoxes[Math.floor(Math.random() * safeBoxes.length)];
        if (!predictedSafe.includes(choice)) predictedSafe.push(choice);
      }

      for (const safe of predictedSafe) {
        const box = document.getElementById('box-' + safe);
        if (box) box.classList.add('safe');
      }

      document.getElementById('result').innerText = `🟢 محفوظ باکسز: ${predictedSafe.join(', ')}`;
    }

    createGrid();
  </script></body>
</html>
