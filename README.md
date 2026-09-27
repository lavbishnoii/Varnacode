# Varnacode
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Varnacode</title>

<style>
body {
    margin:0;
    font-family:Arial;
    background:linear-gradient(135deg,#000,#0a0a2a);
    color:white;
    text-align:center;
}

.container {
    padding:20px;
}

h1 {
    color:gold;
}

textarea {
    width:90%;
    max-width:400px;
    height:100px;
    border-radius:10px;
    padding:10px;
    margin:10px;
    font-size:16px;
}

button {
    padding:10px 20px;
    margin:5px;
    border:none;
    border-radius:20px;
    font-size:16px;
    cursor:pointer;
}

.encode {background:gold;}
.decode {background:cyan;}
.copy {background:limegreen;}

#output {
    margin-top:20px;
    font-size:18px;
    color:cyan;
    word-wrap:break-word;
}
</style>

</head>
<body>

<div class="container">
    <h1>🔐 Varnacode</h1>
    <p>Encode & Decode your secret language</p>

    <textarea id="inputText" placeholder="Hindi ya English likho..."></textarea><br>

    <button class="encode" onclick="encode()">Encode</button>
    <button class="decode" onclick="decode()">Decode</button>
    <button class="copy" onclick="copyText()">Copy</button>

    <div id="output"></div>
</div>

<script>

// FULL MAP
const map = {
"अ":"A1","आ":"A2","इ":"A3","ई":"A4","उ":"A5","ऊ":"A6","ऋ":"A7",
"ए":"A8","ऐ":"A9","ओ":"A10","औ":"A11",

"क":"K1","ख":"K2","ग":"K3","घ":"K4","ङ":"K5",
"च":"C1","छ":"C2","ज":"C3","झ":"C4","ञ":"C5",
"ट":"T1","ठ":"T2","ड":"T3","ढ":"T4","ण":"T5",
"त":"t1","थ":"t2","द":"t3","ध":"t4","न":"t5",
"प":"P1","फ":"P2","ब":"P3","भ":"P4","म":"P5",
"य":"Y1","र":"R1","ल":"L1","व":"V1",
"श":"S1","ष":"S2","स":"S3","ह":"H1",

"ा":"A2","ि":"A3","ी":"A4","ु":"A5","ू":"A6","ृ":"A7",
"े":"A8","ै":"A9","ो":"A10","ौ":"A11"
};

// reverse map
const reverseMap = {};
for (let key in map) {
    reverseMap[map[key]] = key;
}

// Improved English → Hindi (basic)
function engToHindi(text){
return text.toLowerCase()
.replace(/kh/g,"ख")
.replace(/gh/g,"घ")
.replace(/ch/g,"च")
.replace(/aa/g,"आ")
.replace(/ai/g,"ऐ")
.replace(/au/g,"औ")
.replace(/oo/g,"ऊ")
.replace(/ee/g,"ई")
.replace(/a/g,"अ")
.replace(/r/g,"र")
.replace(/m/g,"म")
.replace(/t/g,"त")
.replace(/n/g,"न")
.replace(/p/g,"प")
.replace(/l/g,"ल")
.replace(/h/g,"ह");
}

// ENCODE
function encode(){
let input = document.getElementById("inputText").value;
let hindi = engToHindi(input);

let result = "";
for(let ch of hindi){
if(map[ch]) result += map[ch];
else if(ch===" ") result += " _ ";
}

document.getElementById("output").innerText = result;
}

// DECODE
function decode(){
let input = document.getElementById("inputText").value.trim();
let parts = input.split(" ");
let result = "";

for(let part of parts){
if(part === "_") result += " ";
else if(reverseMap[part]) result += reverseMap[part];
}

document.getElementById("output").innerText = result;
}

// COPY
function copyText(){
let text = document.getElementById("output").innerText;
navigator.clipboard.writeText(text);
alert("Copied!");
}

</script>

</body>
</html>
