<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Peixaria - Pedido</title>

<style>
  body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #0077b6, #00b4d8);
    margin: 0;
    padding: 0;
  }

  .container {
    max-width: 400px;
    margin: 40px auto;
    background: #fff;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 0 15px rgba(0,0,0,0.2);
  }

  h2 {
    text-align: center;
    color: #0077b6;
  }

  label {
    margin-top: 10px;
    display: block;
  }

  select, input {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border-radius: 8px;
    border: 1px solid #ccc;
  }

  button {
    width: 100%;
    padding: 12px;
    margin-top: 12px;
    border: none;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
  }

  .calc {
    background: #0077b6;
    color: white;
  }

  .whatsapp {
    background: #25D366;
    color: white;
  }

  .print {
    background: #555;
    color: white;
  }

  #resumo {
    margin-top: 15px;
    padding: 10px;
    background: #f1f1f1;
    border-radius: 8px;
  }
</style>
</head>

<body>

<div class="container">
  <h2>🐟 Pedido de Peixes</h2>

  <label>Tipo de peixe:</label>
  <select id="peixe">
    <option value="9.99">Sardinha</option>
    <option value="19.99">Tilápia</option>
    <option value="99.99">Salmão</option>
    <option value="25.99">Merluza</option>
    <option value="12.99">Tambaqui</option>
  </select>

  <label>Quantidade (kg):</label>
  <input type="number" id="quantidade" placeholder="Ex: 2.5" step="0.1">

  <button class="calc" onclick="calcular()">Calcular</button>

  <div id="resumo"></div>

  <button class="whatsapp" onclick="enviarWhatsApp()">Finalizar pelo WhatsApp</button>
  <button class="print" onclick="imprimir()">Imprimir Recibo</button>
</div>

<script>
let pedidoTexto = "";

function calcular() {
  const select = document.getElementById("peixe");
  const peixeNome = select.options[select.selectedIndex].text;
  const preco = parseFloat(select.value);
  const quantidade = parseFloat(document.getElementById("quantidade").value);

  if (isNaN(quantidade) || quantidade <= 0) {
    alert("Digite uma quantidade válida!");
    return;
  }

  const total = preco * quantidade;

  pedidoTexto = 
    "Pedido de Peixe:\n" +
    "Tipo: " + peixeNome + "\n" +
    "Quantidade: " + quantidade + " kg\n" +
    "Total: R$ " + total.toFixed(2).replace(".", ",");

  document.getElementById("resumo").innerHTML =
    "<strong>Resumo do Pedido:</strong><br>" +
    "Peixe: " + peixeNome + "<br>" +
    "Quantidade: " + quantidade + " kg<br>" +
    "Total: R$ " + total.toFixed(2).replace(".", ",");
}

function enviarWhatsApp() {
  if (!pedidoTexto) {
    alert("Calcule o pedido primeiro!");
    return;
  }

  const numero = "5575981101778"; // 🔴 COLOQUE SEU NÚMERO AQUI
  const url = "https://wa.me/" + numero + "?text=" + encodeURIComponent(pedidoTexto);

  window.open(url, "_blank");
}

function imprimir() {
  if (!pedidoTexto) {
    alert("Calcule o pedido primeiro!");
    return;
  }

  const janela = window.open("", "", "width=300,height=400");
  janela.document.write("<pre>" + pedidoTexto + "</pre>");
  janela.print();
}
</script>

</body>
</html>
