# Teachable_Machine
Supervised Learning 

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>

const URL = "https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/";
let model, webcam, labelContainer, maxPredictions;

async function init() {
    const modelURL = URL + "model.json";
    const metadataURL = URL + "metadata.json";
    model = await tmImage.load(modelURL, metadataURL);
    // Add logic to setup webcam and start prediction loops
}

let classifier;
let imageModelURL = 'https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/';

function preload() {
  classifier = ml5.imageClassifier(imageModelURL + 'model.json');
}
