<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Atividade SENAI – Cubagem </title>

<!-- jsPDF -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<style>
    body {
        font-family: Arial, sans-serif;
        background: #e8f1ff;
        margin: 0;
        padding: 0;
    }

    header {
        background: #003e7e;
        padding: 20px;
        display: flex;
        align-items: center;
        color: white;
    }

    header img {
        height: 60px;
        margin-right: 20px;
    }

    header h1 {
        margin: 0;
        font-size: 28px;
    }

    .container {
        background: white;
        padding: 25px;
        border-radius: 10px;
        width: 90%;
        margin: 25px auto;
        box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    h2 {
        color: #003e7e;
        border-left: 5px solid #0055b5;
        padding-left: 10px;
    }

    .question {
        background: #f0f6ff;
        border-left: 4px solid #003e7e;
        padding: 12px;
        border-radius: 8px;
        margin: 12px 0;
    }

    input[type="text"], input[type="number"] {
        padding: 8px;
        width: 250px;
        margin-top: 6px;
        border-radius: 5px;
        border: 1px solid #003e7e;
    }

    button {
        padding: 12px 22px;
        background: #003e7e;
        color: white;
        border: none;
        border-radius: 8px;
        font-size: 15px;
        cursor: pointer;
        margin-right: 10px;
    }

    button:hover {
        background: #0055b5;
    }

    #resultado, #medalha {
        text-align: center;
        margin-top: 20px;
        font-size: 22px;
        color: #003e7e;
    }
</style>
</head>

<body>

<!-- CABEÇALHO COM LOGO -->
<header>
    <img src="https://www.senairs.org.br/sites/default/files/styles/scale_sm/public/logos/avatares_sistema_fiergs_senai_cor.png?itok=fuuHGGm3">
    <h1>Atividade Interativa – Cubagem e Armazenagem</h1>
</header>

<div class="container">

<h2>Nome do aluno:</h2>
<input type="text" id="nomeAluno" placeholder="Digite seu nome">

<hr>

<!-- QUESTÕES -->

<h2>Categoria 1 – Container</h2>
<div class="question">
    1) Quantas caixas 30×18×13 cm cabem em um container 12,05m × 2,28m × 2,50m?<br>
    <input type="number" id="q0" placeholder="Resposta">
</div>

<div class="question">
    2) Quantas caixas 25×25×25 cm cabem em um container de 6m × 2,4m × 2,4m?<br>
    <input type="number" id="q1" placeholder="Resposta">
</div>

<hr>

<h2>Categoria 2 – Caminhão</h2>
<div class="question">
    3) Um caminhão baú 8m × 2,40m × 2,40m levará caixas 40×30×30 cm. Quantas cabem?<br>
    <input type="number" id="q2" placeholder="Resposta">
</div>

<div class="question">
    4) Quantas caixas 50×40×30 cm cabem em um caminhão 7m × 2,5m × 2,5m?<br>
    <input type="number" id="q3" placeholder="Resposta">
</div>

<hr>

<h2>Categoria 3 – Estoque / Armazenagem</h2>
<div class="question">
    5) Um estoque tem 10m² e caixas ocupam 0,25m² cada. Quantas cabem no piso?<br>
    <input type="number" id="q4" placeholder="Resposta">
</div>

<div class="question">
    6) Pallet 1,20m × 1m × 1,60m com caixas 60×40×40 cm. Quantas cabem?<br>
    <input type="number" id="q5" placeholder="Resposta">
</div>

<div class="question">
    7) Uma prateleira 2m × 60cm × 50cm comporta caixas 30×20×20 cm. Quantas cabem?<br>
    <input type="number" id="q6" placeholder="Resposta">
</div>

<div class="question">
    8) Quantas caixas 30×30 cm cabem em um pallet de 1m × 1,2m?<br>
    <input type="number" id="q7" placeholder="Resposta">
</div>

<div class="question">
    9) Um estoque vertical de 3m possui caixas de 30cm. Quantos níveis suporta?<br>
    <input type="number" id="q8" placeholder="Resposta">
</div>

<div class="question">
    10) Área de armazenagem com 20m² e caixas ocupando 0,5m². Quantas cabem?<br>
    <input type="number" id="q9" placeholder="Resposta">
</div>

<hr>

<button onclick="corrigir()">Finalizar Atividade</button>
<button onclick="gerarPDF()">Exportar para PDF</button>

<div id="resultado"></div>
<div id="medalha"></div>

</div>

<script>
/* Gabarito */
let respostas = ["9120","5529","1066","291","40","24","24","12","10","40"];

/* Correção */
function corrigir() {
    let score = 0;

    for (let i = 0; i < respostas.length; i++) {
        let respostaAluno = document.getElementById("q"+i).value;
        if (respostaAluno == respostas[i]) score++;
    }

    let nome = document.getElementById("nomeAluno").value || "Aluno não identificado";

    document.getElementById("resultado").innerHTML =
        `${nome}, você acertou <strong>${score}</strong> de 10 questões.`;

    // Medalhas
    let medalha = "";
    if (score <= 4) medalha = "🥉 Medalha de Bronze";
    else if (score <= 7) medalha = "🥈 Medalha de Prata";
    else medalha = "🥇 Medalha de Ouro";

    document.getElementById("medalha").innerHTML = medalha;
}

/* Exportar PDF */
function gerarPDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    let nome = document.getElementById("nomeAluno").value || "Aluno não identificado";
    let resultado = document.getElementById("resultado").innerText;
    let medalha = document.getElementById("medalha").innerText;

    doc.setFontSize(18);
    doc.text("Resultado da Atividade SENAI", 20, 20);

    doc.setFontSize(14);
    doc.text("Aluno: " + nome, 20, 40);
    doc.text(resultado, 20, 60);
    doc.text(medalha, 20, 80);

    doc.save("resultado_senai.pdf");
}
</script>

</body>
</html>
