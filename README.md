# Base-converter.-<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ISMAIL Converter</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f9fafb;
      margin: 0;
      padding: 40px 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .header {
      display: flex;
      align-items: center;
      margin-bottom: 30px;
    }

    .header img {
      width: 50px;
      height: 50px;
      border-radius: 10px;
      margin-right: 15px;
    }

    .header span {
      font-size: 24px;
      font-weight: bold;
      color: #333;
    }

    .converter {
      background: white;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 550px;
      display: flex;
      flex-direction: column;
      gap: 24px;
    }

    h2 {
      text-align: center;
      margin: 0;
      color: #333;
    }

    .section {
      border-top: 1px solid #e2e8f0;
      padding-top: 20px;
    }

    .field {
      display: flex;
      flex-direction: column;
      margin-bottom: 10px;
    }

    label {
      margin-bottom: 5px;
      font-weight: 500;
      color: #444;
    }

    input {
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 8px;
    }

    input:focus {
      outline: none;
      border-color: #3b82f6;
      box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.2);
    }
  </style>
</head>
<body>

  <div class="header">
    <img src="logo.png" alt="ISMAIL Logo" />
    <span>ISMAIL</span>
  </div>

  <div class="converter">
    <h2>All-in-One Converter</h2>

    <!-- Temperature -->
    <div class="section">
      <h3>Temperature</h3>
      <div class="field"><label>Celsius</label><input type="number" id="celsius" oninput="convertTemp('celsius')"></div>
      <div class="field"><label>Fahrenheit</label><input type="number" id="fahrenheit" oninput="convertTemp('fahrenheit')"></div>
      <div class="field"><label>Kelvin</label><input type="number" id="kelvin" oninput="convertTemp('kelvin')"></div>
    </div>

    <!-- Length -->
    <div class="section">
      <h3>Length</h3>
      <div class="field"><label>Meters</label><input type="number" id="meters" oninput="convertLength('meters')"></div>
      <div class="field"><label>Kilometers</label><input type="number" id="kilometers" oninput="convertLength('kilometers')"></div>
      <div class="field"><label>Feet</label><input type="number" id="feet" oninput="convertLength('feet')"></div>
      <div class="field"><label>Inches</label><input type="number" id="inches" oninput="convertLength('inches')"></div>
      <div class="field"><label>Miles</label><input type="number" id="miles" oninput="convertLength('miles')"></div>
    </div>

    <!-- Weight -->
    <div class="section">
      <h3>Weight</h3>
      <div class="field"><label>Kilograms</label><input type="number" id="kilograms" oninput="convertWeight('kilograms')"></div>
      <div class="field"><label>Grams</label><input type="number" id="grams" oninput="convertWeight('grams')"></div>
      <div class="field"><label>Pounds</label><input type="number" id="pounds" oninput="convertWeight('pounds')"></div>
      <div class="field"><label>Ounces</label><input type="number" id="ounces" oninput="convertWeight('ounces')"></div>
    </div>

    <!-- Base -->
    <div class="section">
      <h3>Base Converter</h3>
      <div class="field"><label>Binary (Base 2)</label><input type="text" id="binary" oninput="convertBase('binary')"></div>
      <div class="field"><label>Decimal (Base 10)</label><input type="text" id="decimal" oninput="convertBase('decimal')"></div>
      <div class="field"><label>Octal (Base 8)</label><input type="text" id="octal" oninput="convertBase('octal')"></div>
      <div class="field"><label>Hexadecimal (Base 16)</label><input type="text" id="hex" oninput="convertBase('hex')"></div>
    </div>
  </div>

  <script>
    function convertTemp(source) {
      const c = document.getElementById('celsius');
      const f = document.getElementById('fahrenheit');
      const k = document.getElementById('kelvin');
      let value = parseFloat(document.getElementById(source).value);
      if (isNaN(value)) return;
      if (source === 'celsius') {
        f.value = (value * 9/5 + 32).toFixed(2);
        k.value = (value + 273.15).toFixed(2);
      } else if (source === 'fahrenheit') {
        c.value = ((value - 32) * 5/9).toFixed(2);
        k.value = (((value - 32) * 5/9) + 273.15).toFixed(2);
      } else if (source === 'kelvin') {
        c.value = (value - 273.15).toFixed(2);
        f.value = ((value - 273.15) * 9/5 + 32).toFixed(2);
      }
    }

    function convertLength(source) {
      const units = { meters: 1, kilometers: 0.001, feet: 3.28084, inches: 39.3701, miles: 0.000621371 };
      let value = parseFloat(document.getElementById(source).value);
      if (isNaN(value)) return;
      let meters = value / units[source];
      for (let unit in units) {
        if (unit !== source) {
          document.getElementById(unit).value = (meters * units[unit]).toFixed(4);
        }
      }
    }

    function convertWeight(source) {
      const units = { kilograms: 1, grams: 1000, pounds: 2.20462, ounces: 35.274 };
      let value = parseFloat(document.getElementById(source).value);
      if (isNaN(value)) return;
      let kg = value / units[source];
      for (let unit in units) {
        if (unit !== source) {
          document.getElementById(unit).value = (kg * units[unit]).toFixed(4);
        }
      }
    }

    function convertBase(base) {
      const binary = document.getElementById('binary');
      const decimal = document.getElementById('decimal');
      const octal = document.getElementById('octal');
      const hex = document.getElementById('hex');
      let value = '';
      try {
        switch (base) {
          case 'binary': value = parseInt(binary.value, 2); break;
          case 'decimal': value = parseInt(decimal.value, 10); break;
          case 'octal': value = parseInt(octal.value, 8); break;
          case 'hex': value = parseInt(hex.value, 16); break;
        }
        if (!isNaN(value)) {
          binary.value = value.toString(2);
          decimal.value = value.toString(10);
          octal.value = value.toString(8);
          hex.value = value.toString(16).toUpperCase();
        }
      } catch (e) {}
    }
  </script>
</body>
</html>
