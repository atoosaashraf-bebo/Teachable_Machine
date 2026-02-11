# Teachable_Machine
Supervised Learning 

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teachable Machine Image Model</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            background-color: #f4f4f9;
        }
        h1 { color: #333; }
        #webcam-container {
            margin: 20px;
            border: 5px solid #333;
            border-radius: 10px;
            overflow: hidden;
            background: #000;
        }
        #label-container {
            display: flex;
            flex-direction: column;
            gap: 10px;
            width: 300px;
        }
        .prediction-bar {
            background: #eee;
            border-radius: 5px;
            position: relative;
            height: 30px;
            width: 100%;
        }
        .fill {
            background: #4CAF50;
            height: 100%;
            border-radius: 5px;
            transition: width 0.2s ease-in-out;
        }
        .label-text {
            position: absolute;
            left: 10px;
            top: 5px;
            font-size: 14px;
            font-weight: bold;
            color: #000;
        }
        button {
            padding: 12px 24px;
            font-size: 16px;
            cursor: pointer;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            transition: 0.3s;
        }
        button:hover { background-color: #0056b3; }
    </style>
</head>
<body>

    <h1>Teachable Machine Image Model</h1>
    <button type="button" onclick="init()">Start Camera</button>
    
    <div id="webcam-container"></div>
    <div id="label-container"></div>

    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>

    <script type="text/javascript">
        // The link to your model provided by Teachable Machine
        const URL = "https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/";

        let model, webcam, labelContainer, maxPredictions;

        // Load the image model and setup the webcam
        async function init() {
            const modelURL = URL + "model.json";
            const metadataURL = URL + "metadata.json";

            // Load the model and metadata
            model = await tmImage.load(modelURL, metadataURL);
            maxPredictions = model.getTotalClasses();

            // Convenience function to setup a webcam
            const flip = true; // whether to flip the webcam
            webcam = new tmImage.Webcam(400, 400, flip); // width, height, flip
            await webcam.setup(); // request access to the webcam
            await webcam.play();
            window.requestAnimationFrame(loop);

            // Append elements to the DOM
            document.getElementById("webcam-container").appendChild(webcam.canvas);
            labelContainer = document.getElementById("label-container");
            for (let i = 0; i < maxPredictions; i++) {
                // Create progress bars for each class
                const barWrapper = document.createElement("div");
                barWrapper.className = "prediction-bar";
                barWrapper.innerHTML = `<div class="fill" style="width: 0%"></div><div class="label-text"></div>`;
                labelContainer.appendChild(barWrapper);
            }
        }

        async function loop() {
            webcam.update(); // update the webcam frame
            await predict();
            window.requestAnimationFrame(loop);
        }

        // Run the webcam image through the image model
        async function predict() {
            const prediction = await model.predict(webcam.canvas);
            for (let i = 0; i < maxPredictions; i++) {
                const classPrediction = prediction[i].className;
                const probability = (prediction[i].probability * 100).toFixed(0);
                
                const bar = labelContainer.childNodes[i].querySelector('.fill');
                const text = labelContainer.childNodes[i].querySelector('.label-text');
                
                bar.style.width = probability + "%";
                text.innerHTML = `${classPrediction}: ${probability}%`;
            }
        }
    </script>
</body>
</html>
