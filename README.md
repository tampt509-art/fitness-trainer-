<!DOCTYPE html>
<html>
<head>

<meta name="viewport" content="width=device-width, initial-scale=1">

<title>Fitness Trainer</title>

<style>

body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
padding:20px;
}

h1{
font-size:28px;
}

select{
font-size:18px;
padding:10px;
margin:10px;
border-radius:8px;
}

#exercise{
font-size:26px;
margin-top:20px;
}

#setinfo{
font-size:18px;
color:#7dd3fc;
}

#timer{
font-size:60px;
margin:20px;
color:#22c55e;
}

button{
font-size:18px;
padding:12px 18px;
margin:6px;
border:none;
border-radius:10px;
}

.start{background:#22c55e;color:white;}
.pause{background:#f59e0b;color:white;}
.stop{background:#ef4444;color:white;}

</style>

</head>

<body>

<h1>💪 Smart Fitness Trainer</h1>

<select id="daySelect">
<option value="day1">Day 1 – Chest + Triceps</option>
<option value="day2">Day 2 – Back + Biceps</option>
<option value="day3">Day 3 – Shoulders + Traps</option>
<option value="day4">Day 4 – Core + Forearms</option>
</select>

<div id="exercise">Ready</div>
<div id="setinfo"></div>
<div id="timer">0</div>

<button class="start" onclick="startWorkout()">START</button>
<button class="pause" onclick="pauseWorkout()">PAUSE</button>
<button class="stop" onclick="stopWorkout()">STOP</button>

<script>

let workouts={
day1:["Floor Press","Floor Fly","Pullover"],
day2:["Bent Row","Reverse Fly","Bicep Curl"],
day3:["Shoulder Press","Lateral Raise","Shrugs"],
day4:["Side Bend","Russian Twist","Wrist Curl"]
};

let exercises=[];
let current=0;
let timer;
let timeLeft=30;

function speak(text){
let msg=new SpeechSynthesisUtterance(text);
speechSynthesis.speak(msg);
}

function startWorkout(){

let day=document.getElementById("daySelect").value;

exercises=workouts[day];

current=0;

nextExercise();

}

function countdown(callback){

let count=3;

let cd=setInterval(()=>{

speak(count);

count--;

if(count<0){

clearInterval(cd);

speak("Start");

callback();

}

},1000);

}

function nextExercise(){

if(current>=exercises.length){

document.getElementById("exercise").innerText="Workout Complete";

speak("Workout complete");

return;

}

let ex=exercises[current];

document.getElementById("exercise").innerText=ex;

countdown(startTimer);

}

function startTimer(){

timeLeft=30;

document.getElementById("timer").innerText=timeLeft;

timer=setInterval(()=>{

timeLeft--;

document.getElementById("timer").innerText=timeLeft;

if(timeLeft<=0){

clearInterval(timer);

rest();

}

},1000);

}

function rest(){

speak("Rest");

document.getElementById("exercise").innerText="Rest";

timeLeft=15;

document.getElementById("timer").innerText=timeLeft;

timer=setInterval(()=>{

timeLeft--;

document.getElementById("timer").innerText=timeLeft;

if(timeLeft<=0){

clearInterval(timer);

current++;

nextExercise();

}

},1000);

}

function pauseWorkout(){
clearInterval(timer);
}

function stopWorkout(){

clearInterval(timer);

document.getElementById("exercise").innerText="Stopped";

document.getElementById("timer").innerText="0";

}

</script>

</body>
</html>
