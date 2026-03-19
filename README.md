<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>A-OS Market</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body {
    margin:0;
    font-family:Arial;
    background:linear-gradient(135deg,#0f0f1a,#1c1c3a);
    color:white;
    text-align:center;
}

h1 {
    padding:20px;
}

.container {
    display:flex;
    justify-content:center;
    gap:20px;
    flex-wrap:wrap;
}

.card {
    background:#1f1f3a;
    padding:20px;
    border-radius:15px;
    cursor:pointer;
    width:200px;
    transition:0.3s;
}

.card:hover {
    transform:scale(1.05);
    background:#3a3aff;
}

canvas {
    margin-top:40px;
    max-width:800px;
}
</style>
</head>
<body>

<h1>🚀 A-OS Market</h1>

<div class="container" id="acoes"></div>

<canvas id="grafico"></canvas>

<script>
const acoes = [
    {nome:"Apple", valor:150},
    {nome:"Microsoft", valor:120},
    {nome:"Netflix", valor:90}
];

const container = document.getElementById("acoes");

acoes.forEach((acao,index)=>{
    const div=document.createElement("div");
    div.className="card";
    div.innerHTML=`${acao.nome}<br>$${acao.valor}`;
    div.onclick=()=>mostrarGrafico(index);
    container.appendChild(div);
});

const ctx=document.getElementById("grafico").getContext("2d");

const grafico=new Chart(ctx,{
    type:"line",
    data:{
        labels:[],
        datasets:[{
            label:"Valor",
            data:[],
            borderColor:"#3a3aff"
        }]
    }
});

function mostrarGrafico(index){
    let valor=acoes[index].valor;

    grafico.data.labels=[];
    grafico.data.datasets[0].data=[];

    for(let i=0;i<10;i++){
        grafico.data.labels.push("Hora "+i);
        valor+=Math.random()*10-5;
        grafico.data.datasets[0].data.push(valor.toFixed(2));
    }

    grafico.update();
}
</script>

</body>
</html>
