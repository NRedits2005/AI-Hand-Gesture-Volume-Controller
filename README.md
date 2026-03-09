
---

# Interactive Gesture File (Better UI Version)

Here is a **cleaner interactive interface** you can use as `index.html`.

```html
<!DOCTYPE html>
<html>
<head>

<title>AI Gesture Music Controller</title>

<meta charset="UTF-8">

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>

<style>

body{
background:linear-gradient(135deg,#141e30,#243b55);
color:white;
font-family:Arial;
text-align:center;
}

h1{
margin-top:20px;
}

button{
padding:12px 20px;
font-size:16px;
background:#00e5ff;
border:none;
border-radius:6px;
cursor:pointer;
}

input{
margin-top:10px;
}

audio{
margin-top:10px;
}

#webcam-container{
margin-top:20px;
}

#prediction{
font-size:22px;
margin-top:20px;
}

#volumeBar{
width:300px;
height:20px;
}

</style>

</head>

<body>

<h1>🎵 AI Gesture Music Controller</h1>

<button onclick="init()">Start Camera</button>

<br><br>

<input type="file" id="songSelector" accept="audio/*">

<br><br>

<audio id="audioPlayer" controls></audio>

<p>Volume : <span id="vol">0.50</span></p>

<progress id="volumeBar" value="0.5" max="1"></progress>

<div id="webcam-container"></div>

<div id="prediction">Waiting for gesture...</div>

<script>

const MODEL_URL = "https://teachablemachine.withgoogle.com/models/foR1hW9Ip/";

let model, webcam;

let audio = document.getElementById("audioPlayer");
let fileInput = document.getElementById("songSelector");

let volDisplay = document.getElementById("vol");
let volumeBar = document.getElementById("volumeBar");

let predictionText = document.getElementById("prediction");

audio.volume = 0.5;

fileInput.addEventListener("change", function(){

const file = this.files[0];

if(file){

audio.src = URL.createObjectURL(file);

audio.play();

}

});

async function init(){

const modelURL = MODEL_URL + "model.json";
const metadataURL = MODEL_URL + "metadata.json";

model = await tmImage.load(modelURL, metadataURL);

webcam = new tmImage.Webcam(250,250,true);

await webcam.setup();
await webcam.play();

document.getElementById("webcam-container").appendChild(webcam.canvas);

window.requestAnimationFrame(loop);

}

async function loop(){

webcam.update();
await predict();

window.requestAnimationFrame(loop);

}

async function predict(){

const prediction = await model.predict(webcam.canvas);

let highest = prediction.reduce((a,b)=>a.probability>b.probability?a:b);

predictionText.innerHTML =
highest.className + " : " + highest.probability.toFixed(2);

if(highest.probability > 0.9){

if(highest.className === "Volume Up"){

audio.volume = Math.min(1 , audio.volume + 0.05);

}

if(highest.className === "Volume Down"){

audio.volume = Math.max(0 , audio.volume - 0.05);

}

updateVolume();

}

}

function updateVolume(){

volDisplay.innerText = audio.volume.toFixed(2);

volumeBar.value = audio.volume;

}

</script>

</body>
</html>
