<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gizi Seimbang Interaktif</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}
body{background:#f4f7fa;scroll-behavior:smooth}

/* NAVBAR */
nav{
position:fixed;width:100%;top:0;
background:rgba(46,139,87,0.95);
padding:15px;text-align:center;z-index:1000}
nav a{color:white;text-decoration:none;margin:0 15px;font-weight:600}
nav a:hover{color:#ffd700}

/* HERO */
.hero{
height:100vh;
background:linear-gradient(120deg,#2e8b57,#ff8c00);
display:flex;justify-content:center;align-items:center;
text-align:center;color:white;padding:20px}
.hero h1{font-size:3rem}
.hero p{margin-top:15px;font-size:18px}

/* SECTION */
section{padding:100px 20px;max-width:1100px;margin:auto}
h2{text-align:center;margin-bottom:30px;color:#2e8b57}

/* CARD */
.card{
background:white;padding:25px;margin:20px 0;
border-radius:15px;
box-shadow:0 8px 20px rgba(0,0,0,0.08);
transition:.3s}
.card:hover{
transform:translateY(-5px)}

/* ISI PIRINGKU */
.plate-container{
display:flex;justify-content:center;align-items:center;
}
.plate{
width:300px;height:300px;border-radius:50%;
background:#fff;
box-shadow:0 15px 35px rgba(0,0,0,0.2);
position:relative;overflow:hidden;
}
.food{position:absolute;width:50%;height:50%}
.sayur{background:#4caf50;top:0;left:0}
.buah{background:#f44336;top:0;right:0}
.karbo{background:#ff9800;bottom:0;left:0}
.protein{background:#2196f3;bottom:0;right:0}

/* BUTTON */
button{
background:#2e8b57;color:white;border:none;
padding:10px 15px;border-radius:8px;
cursor:pointer;margin-top:10px}
button:hover{background:#1b5e20}

/* INPUT */
input{
padding:8px;margin:5px 0;width:100%;
border-radius:6px;border:1px solid #ccc}

/* FOOTER */
footer{
background:#2e8b57;color:white;
text-align:center;padding:20px}
</style>
</head>

<body>

<nav>
<a href="#materi">Materi</a>
<a href="#piring">Isi Piringku</a>
<a href="#imt">Kalkulator IMT</a>
<a href="#quiz">Quiz</a>
</nav>

<div class="hero">
<div>
<h1>Edukasi Gizi Seimbang</h1>
<p>Makan Sehat • Aktif Bergerak • Hidup Lebih Baik</p>
</div>
</div>

<!-- MATERI -->
<section id="materi">
<h2>Pengertian Gizi Seimbang</h2>
<div class="card">
<p>
Gizi seimbang adalah pola makan sehari-hari yang mengandung zat gizi dalam jenis dan jumlah sesuai kebutuhan tubuh,
disertai aktivitas fisik, perilaku hidup bersih, dan pemantauan berat badan secara teratur.
</p>
</div>

<h2>Empat Pilar Gizi Seimbang</h2>
<div class="card">
<ul>
<li>Konsumsi makanan beragam</li>
<li>Perilaku hidup bersih</li>
<li>Aktivitas fisik minimal 30 menit/hari</li>
<li>Memantau berat badan secara rutin</li>
</ul>
</div>
</section>

<!-- ISI PIRINGKU -->
<section id="piring">
<h2>Ilustrasi Isi Piringku</h2>
<div class="plate-container">
<div class="plate">
<div class="food sayur"></div>
<div class="food buah"></div>
<div class="food karbo"></div>
<div class="food protein"></div>
</div>
</div>
<p style="text-align:center;margin-top:15px">
50% Sayur & Buah • 25% Karbohidrat • 25% Protein
</p>
</section>

<!-- IMT -->
<section id="imt">
<h2>Kalkulator Indeks Massa Tubuh (IMT)</h2>
<div class="card">
<label>Berat Badan (kg)</label>
<input type="number" id="bb">
<label>Tinggi Badan (cm)</label>
<input type="number" id="tb">
<button onclick="hitungIMT()">Hitung IMT</button>
<p id="hasilIMT"></p>
</div>
</section>

<!-- QUIZ -->
<section id="quiz">
<h2>Quiz Gizi Seimbang</h2>
<div class="card">
<p id="question"></p>
<div id="options"></div>
<p id="score"></p>
</div>
</section>

<footer>
<p>© 2026 Website Edukasi Gizi Seimbang</p>
</footer>

<script>
/* IMT */
function hitungIMT(){
let bb=document.getElementById("bb").value;
let tb=document.getElementById("tb").value/100;
let imt=(bb/(tb*tb)).toFixed(2);
let kategori="";

if(imt<18.5) kategori="Berat badan kurang";
else if(imt<25) kategori="Normal";
else if(imt<30) kategori="Berat badan berlebih";
else kategori="Obesitas";

document.getElementById("hasilIMT").innerHTML=
"IMT Anda: "+imt+" ("+kategori+")";
}

/* QUIZ */
const quizData=[
{q:"Apa sumber protein nabati?",a:["Nasi","Tempe","Gula","Minyak"],c:1},
{q:"Berapa menit aktivitas fisik dianjurkan?",a:["5","15","30","10"],c:2},
{q:"Setengah isi piring berisi?",a:["Protein","Karbo","Sayur & Buah","Gula"],c:2}
];

let current=0, skor=0;

function loadQuiz(){
if(current>=quizData.length){
document.getElementById("question").innerText="Quiz selesai!";
document.getElementById("options").innerHTML="";
document.getElementById("score").innerText=
"Skor Anda: "+skor+" dari "+quizData.length;
return;
}

let q=quizData[current];
document.getElementById("question").innerText=q.q;
let opsi="";
q.a.forEach((opt,i)=>{
opsi+=`<button onclick="cek(${i})">${opt}</button><br>`;
});
document.getElementById("options").innerHTML=opsi;
}

function cek(i){
if(i===quizData[current].c) skor++;
current++;
loadQuiz();
}

loadQuiz();
</script>

</body>
</html>
