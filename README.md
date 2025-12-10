<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<title>百家樂隨機模擬器</title>
<style>
body { font-family: Arial; background: #f2f2f2; padding: 20px; text-align: center; }
button { margin: 10px; padding: 12px 25px; font-size: 18px; }
#result { font-size: 32px; margin-top: 20px; color: #333; }
#stats { margin-top: 30px; font-size: 20px; }
</style>
</head>
<body>

<h1>百家樂隨機模擬器</h1>

<button onclick="drawOne()">抽一手</button>
<button onclick="drawMany(100)">連抽 100 次</button>
<button onclick="drawMany(1000)">連抽 1000 次</button>
<button onclick="resetStats()">清空統計</button>

<div id="result"></div>

<div id="stats">
<p>莊 (1)：<span id="b">0</span></p>
<p>閒 (2)：<span id="p">0</span></p>
<p>和 (3)：<span id="t">0</span></p>
<p>總數：<span id="total">0</span></p>
</div>

<script>
let b=0,p=0,t=0,total=0;

function baccaratRandom() {
    let r=Math.random();
    if(r<0.458) return 1;
    else if(r<0.458+0.446) return 2;
    else return 3;
}

function updateStats(result) {
    if(result===1) b++;
    if(result===2) p++;
    if(result===3) t++;
    total++;
    document.getElementById("b").innerText=b;
    document.getElementById("p").innerText=p;
    document.getElementById("t").innerText=t;
    document.getElementById("total").innerText=total;
}

function drawOne() {
    let result=baccaratRandom();
    updateStats(result);
    document.getElementById("result").innerHTML="結果："+result;
}

function drawMany(n){
    let last=0;
    for(let i=0;i<n;i++){
        last=baccaratRandom();
        updateStats(last);
    }
    document.getElementById("result").innerHTML="最後一手："+last+"（共 "+n+" 手）";
}

function resetStats(){
    b=0;p=0;t=0;total=0;
    document.getElementById("b").innerText=0;
    document.getElementById("p").innerText=0;
    document.getElementById("t").innerText=0;
    document.getElementById("total").innerText=0;
    document.getElementById("result").innerHTML="";
}
</script>

</body>
</html>