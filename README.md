Since I can't look inside your private training session to see exactly what classes you've trained (e.g., "Cat vs. Dog" or "Rock, Paper, Scissors"), I’ve created a **comprehensive, high-quality README** that uses your specific model link.

Just fill in the **[Bracketed Text]** sections once you paste this into GitHub!

---

# 🧠 Teachable Machine Image Classifier

This repository contains a real-time image classification model trained using **Google’s Teachable Machine**. It utilizes **TensorFlow.js** to run deep learning inference directly in the browser.

## 🔗 Model Link

**Live Model URL:** [https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/](https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/)

---

## 📋 About the Project

This project is designed to recognize and classify images into the following categories:

* **[Class Name 1]**: (e.g., "Bottle in hand")
* **[Class Name 2]**: (e.g., "Mobile Phone in hand")
* **[Class Name 3]**: (e.g., "Empty background")

The model was trained using a custom dataset of images and uses a transfer learning approach based on the **MobileNet** architecture.

## 🚀 How to Run Locally

To get this model running on your own machine or GitHub Pages, follow these steps:

### 1. The Single-File Method

Create a file named `index.html` and paste the code from this repository. The model is hosted via the Google cloud link, so you don't need to download the weights manually.

### 2. Implementation Script

If you are building your own site, use the following snippet to load this specific model:

```javascript
// The link to your model provided by Teachable Machine
const URL = "https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/";

async function init() {
    const modelURL = URL + "model.json";
    const metadataURL = URL + "metadata.json";

    // Load the model and metadata
    const model = await tmImage.load(modelURL, metadataURL);
    const maxPredictions = model.getTotalClasses();
    
    console.log("Model loaded successfully!");
}

```

---

## 🛠️ Technology Stack

* **Framework:** [TensorFlow.js](https://www.tensorflow.org/js)
* **Training Tool:** [Teachable Machine](https://teachablemachine.withgoogle.com/)
* **Language:** JavaScript / HTML5 / CSS3

## 📂 Repository Contents

* `README.md`: Documentation and project overview.
* `index.html`: A complete, functional demo using your webcam.

## 🤝 Contributing
## Proof of Concept

Feel free to fork this project and adapt it for your own use cases—whether that's building an automated plant identifier, a gesture-controlled UI, or a security filter.

<img width="340" height="640" alt="image" src="https://github.com/user-attachments/assets/b6e71abb-62b0-487e-92b1-4b22a07f557c" />

<img width="340" height="6400" alt="image" src="https://github.com/user-attachments/assets/c0636e32-b413-4742-85d8-7c62687721de" />

<img width="340" height="640" alt="image" src="https://github.com/user-attachments/assets/f6ebf8a6-cf39-4549-adfd-99665a9bc03b" />






---

*Created by Atoosa Ashraf*

---

### One quick suggestion:

Since you have the model link, would you like me to write a **Python script** that lets you use this same model on your local computer (using `OpenCV` and `TensorFlow`) instead of just in a web browser?# Teachable_Machine
Supervised Learning 

Since I can't look inside your private training session to see exactly what classes you've trained (e.g., "Cat vs. Dog" or "Rock, Paper, Scissors"), I’ve created a **comprehensive, high-quality README** that uses your specific model link.

Just fill in the **[Bracketed Text]** sections once you paste this into GitHub!

---

# 🧠 Teachable Machine Image Classifier

This repository contains a real-time image classification model trained using **Google’s Teachable Machine**. It utilizes **TensorFlow.js** to run deep learning inference directly in the browser.

## 🔗 Model Link

**Live Model URL:** [https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/](https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/)

---

## 📋 About the Project

This project is designed to recognize and classify images into the following categories:

* **[Class Name 1]**: (e.g., "Phone in hand")
* **[Class Name 2]**: (e.g., "Empty background")
* **[Class Name 3]**: (e.g., "Wearing Glasses")

The model was trained using a custom dataset of images and uses a transfer learning approach based on the **MobileNet** architecture.

## 🚀 How to Run Locally

To get this model running on your own machine or GitHub Pages, follow these steps:

### 1. The Single-File Method

Create a file named `index.html` and paste the code from this repository. The model is hosted via the Google cloud link, so you don't need to download the weights manually.

### 2. Implementation Script

If you are building your own site, use the following snippet to load this specific model:

```javascript
// The link to your model provided by Teachable Machine
const URL = "https://teachablemachine.withgoogle.com/models/bB_mTkvjxm/";

async function init() {
    const modelURL = URL + "model.json";
    const metadataURL = URL + "metadata.json";

    // Load the model and metadata
    const model = await tmImage.load(modelURL, metadataURL);
    const maxPredictions = model.getTotalClasses();
    
    console.log("Model loaded successfully!");
}

```

---


### One quick suggestion:

Since you have the model link, would you like me to write a **Python script** that lets you use this same model on your local computer (using `OpenCV` and `TensorFlow`) instead of just in a web browser?
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
