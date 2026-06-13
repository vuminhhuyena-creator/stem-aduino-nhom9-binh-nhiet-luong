<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<title>Bình nhiệt lượng kế thông minh</title>

<style>

body{
font-family:Arial;
max-width:1000px;
margin:auto;
padding:20px;
background:#f5f5f5;
}

.card{
background:white;
padding:20px;
margin-bottom:20px;
border-radius:10px;
box-shadow:0 0 8px rgba(0,0,0,.1);
}

button{
padding:10px 20px;
font-size:16px;
cursor:pointer;
}

.correct{
color:green;
font-weight:bold;
}

.wrong{
color:red;
font-weight:bold;
}

.dropzone{
width:180px;
height:70px;
border:2px dashed #666;
margin:10px;
display:inline-block;
vertical-align:top;
padding:5px;
}

.drag{
background:#2196F3;
color:white;
padding:10px;
margin:5px;
cursor:move;
border-radius:5px;
}

input{
padding:8px;
width:120px;
}

</style>
</head>

<body>

<h1>BÌNH NHIỆT LƯỢNG KẾ THÔNG MINH</h1>

<div class="card">

<h2>Phần 1. Trắc nghiệm</h2>

<p>Thiết bị đo nhiệt độ trong hệ Arduino là:</p>

<input type="radio" name="q1" value="A"> Arduino<br>
<input type="radio" name="q1" value="B"> LCD<br>
<input type="radio" name="q1" value="C"> DS18B20<br>

<button onclick="checkQ1()">Kiểm tra</button>

<p id="q1result"></p>

</div>

<div class="card">

<h2>Phần 2. Kéo thả linh kiện</h2>

<h3>Kéo đúng linh kiện vào vị trí</h3>

<div id="arduino" class="drag" draggable="true">
Arduino Uno
</div>

<div id="sensor" class="drag" draggable="true">
DS18B20
</div>

<div id="lcd" class="drag" draggable="true">
LCD
</div>

<br><br>

<div class="dropzone" data-answer="arduino">
Arduino
</div>

<div class="dropzone" data-answer="sensor">
Cảm biến
</div>

<div class="dropzone" data-answer="lcd">
Màn hình
</div>

<br>

<button onclick="checkDrag()">Kiểm tra</button>

<p id="dragResult"></p>

</div>

<div class="card">

<h2>Phần 3. Tính nhiệt dung riêng</h2>

<p>
m = 0.2 kg
</p>

<p>
Q = 3360 J
</p>

<p>
Δt = 4°C
</p>

<p>

Nhập kết quả:

<input id="cvalue">

</p>

<button onclick="checkC()">
Kiểm tra
</button>

<p id="cresult"></p>

</div>

<script>

function checkQ1(){

let ans=document.querySelector(
'input[name="q1"]:checked');

if(!ans) return;

if(ans.value==="C")
{
document.getElementById("q1result").innerHTML=
"<span class='correct'>Chính xác!</span>";
}
else
{
document.getElementById("q1result").innerHTML=
"<span class='wrong'>Sai rồi!</span>";
}

}

let drags=document.querySelectorAll(".drag");

drags.forEach(item=>{

item.addEventListener("dragstart",e=>{

e.dataTransfer.setData(
"text",
e.target.id);

});

});

let zones=document.querySelectorAll(".dropzone");

zones.forEach(zone=>{

zone.addEventListener("dragover",
e=>e.preventDefault());

zone.addEventListener("drop",e=>{

e.preventDefault();

let id=e.dataTransfer.getData("text");

zone.innerHTML=
document.getElementById(id).innerHTML;

zone.dataset.user=id;

});

});

function checkDrag(){

let ok=true;

zones.forEach(zone=>{

if(zone.dataset.user!==zone.dataset.answer)
ok=false;

});

document.getElementById("dragResult").innerHTML=
ok ?
"<span class='correct'>Lắp đúng hệ thống!</span>"
:
"<span class='wrong'>Chưa chính xác!</span>";

}

function checkC(){

let value=
parseFloat(
document.getElementById("cvalue").value);

if(Math.abs(value-4200)<50)
{
document.getElementById("cresult").innerHTML=
"<span class='correct'>Đúng!</span>";
}
else
{
document.getElementById("cresult").innerHTML=
"<span class='wrong'>Sai!</span>";
}

}

</script>

</body>
</html>
