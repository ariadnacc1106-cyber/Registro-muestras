<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sistema de Identificación de Muestras</title>
  <style>
    body {
      font-family: Arial, Helvetica, sans-serif;
      background-color: #f4f6f8;
      margin: 0;
      padding: 20px;
    }
    .container {
      max-width: 900px;
      margin: auto;
      background: #ffffff;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #2c3e50;
    }
    h2 {
      margin-top: 25px;
      font-size: 18px;
      color: #1f6aa5;
    }
    .field-group {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      margin-top: 15px;
    }
    .field {
      display: flex;
      flex-direction: column;
    }
    label {
      font-weight: bold;
      margin-bottom: 5px;
    }
    input, select {
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 14px;
    }
    .actions {
      margin-top: 30px;
      text-align: center;
    }
    button {
      background-color: #1f6aa5;
      color: white;
      border: none;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 4px;
      cursor: pointer;
    }
    .result {
      margin-top: 30px;
      padding: 20px;
      background-color: #eef5fb;
      border-left: 5px solid #1f6aa5;
    }
    .code {
      font-weight: bold;
      font-size: 18px;
      color: #1f6aa5;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Sistema de Código de Identificación de Muestras</h1>

    <h2>Datos de entrada</h2>
    <div class="field-group">
      <div class="field">
        <label>Fecha de recepción</label>
        <input type="date" id="fecha" />
      </div>
      <div class="field">
        <label>Número secuencial</label>
        <input type="number" id="secuencial" min="1" value="1" />
      </div>
      <div class="field">
        <label>Tipo de muestra</label>
        <select id="tipo">
          <option value="CH">Cortes histológicos teñidos (CH)</option>
          <option value="BP">Bloques de parafina archivados (BP)</option>
          <option value="EC">Extensiones citológicas teñidas (EC)</option>
          <option value="CBL">Citología en base líquida (CBL)</option>
          <option value="PCE">Preparaciones citológicas especiales (PCE)</option>
        </select>
      </div>
      <div class="field">
        <label>Técnica aplicada</label>
        <select id="tecnica">
          <option value="HE">Hematoxilina-Eosina (HE)</option>
          <option value="TE">Tinción especial (TE)</option>
          <option value="PAP">Papanicolaou (PAP)</option>
          <option value="GIE">Giemsa (GIE)</option>
          <option value="BL">Base líquida (BL)</option>
          <option value="ICQ">Inmunocitoquímica (ICQ)</option>
          <option value="ME">Marcadores específicos (ME)</option>
          <option value="NA">No aplica (NA)</option>
        </select>
      </div>
    </div>

    <div class="actions">
      <button onclick="generarCodigo()">Generar código</button>
    </div>

    <div id="resultado" class="result" style="display:none;"></div>
  </div>

  <script>
    const tipos = {
      CH: "Corte histológico teñido",
      BP: "Bloque de parafina archivado",
      EC: "Extensión citológica teñida",
      CBL: "Citología en base líquida",
      PCE: "Preparación citológica especial"
    };

    const tecnicas = {
      HE: "Hematoxilina-Eosina",
      TE: "Tinción especial",
      PAP: "Papanicolaou",
      GIE: "Giemsa",
      BL: "Base líquida",
      ICQ: "Inmunocitoquímica",
      ME: "Marcadores específicos",
      NA: "No aplica"
    };

    function generarCodigo() {
      const fechaInput = document.getElementById('fecha').value;
      if (!fechaInput) {
        alert('Seleccione una fecha');
        return;
      }
      const fecha = fechaInput.replaceAll('-', '');
      const tipo = document.getElementById('tipo').value;
      const tecnica = document.getElementById('tecnica').value;
      const sec = document.getElementById('secuencial').value.padStart(4, '0');

      const codigo = `${fecha}-${tipo}-${tecnica}-${sec}`;

      document.getElementById('resultado').style.display = 'block';
      document.getElementById('resultado').innerHTML = `
        <p><strong>Código generado:</strong></p>
        <p class="code">${codigo}</p>
        <p><strong>Tipo de muestra:</strong> ${tipos[tipo]}</p>
        <p><strong>Técnica aplicada:</strong> ${tecnicas[tecnica]}</p>
      `;
    }
  </script>
</body>
</html>
