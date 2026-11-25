# 🤖 AI Adversarial Robustness & Fruit Classifier 🍎🍌

A browser-based Image Classifier built with **TensorFlow.js** and **Teachable Machine**, deployed on GitHub Pages to test model robustness, feature extraction (shape vs. color), and decision boundary vulnerabilities in real-world scenarios.

## 🚀 Live Demo
👉 **[Try to break the model here on GitHub Pages](ԱՅՍՏԵՂ ԴԻՐ ՔՈ ԼԻՆԿԸ)** 
*(Try uploading a dog, a green banana, or a text-injected image to see how the AI reacts!)*

## 🎯 Project Overview & Security Research
This project explores **AI Red Teaming** and **Adversarial Machine Learning**. The goal was to analyze how a lightweight neural network extracts features and how environmental shifts or injected payloads impact its decision boundaries.

## 🧪 Phase 1: Initial Robustness Testing
- 🍌 **Yellow Banana (Baseline):** 100% Banana. Standard input baseline.
- 🤔 Green Banana (Background Shift): Accuracy dropped from 98% (lab) to 79% (web). The likely cause: the model saw training images with a uniform background, so background context became part of its decision signal — a classic sign of data bias in a small training set.
- 🤯 **Black Apple (Out-of-Distribution Generalization):** 100% Apple. Proved the model learned geometric feature boundaries (shape, curvature) rather than relying purely on color dynamics.

## 🛡️ Phase 2: OWASP LLM Top 10 Red Teaming
I tested the model against specific vulnerabilities to understand how AI can be exploited in surveillance or automated verification systems.
| Test | Attack Vector | Result | Status |
| :--- | :--- | :--- | :--- |
| **Text-on-Image Injection** | "I AM AN APPLE" | Ignored by AI (100% Banana) | 🟢 Resisted |
| **Adversarial Patch** | Chessboard pattern | Resisted local noise (100% Banana) | 🟢 Resisted |
| **Out-of-Distribution (OOD)** | Image of a Dog | Falsely predicted Banana (95%) | 🔴 Failed |


*You can read the detailed vulnerability report in the **[SECURITY.md](./SECURITY.md)** file.*

## 🛠️ Tech Stack & Architecture
- **Model Training:** Teachable Machine (Transfer Learning)
- **Deployment & Inference:** TensorFlow.js (Client-side browser execution)
- **Frontend:** HTML5, CSS3, JavaScript (File Reader APIs)
- **Security Concept:** AI Red Teaming, Adversarial Noise Testing, Prompt Injection, OOD Misinformation

## 💡 Key Security Takeaways
1. **Shape over Color:** The model successfully generalized to a black apple, proving it learned geometry.
2. **Context Sensitivity:** Backgrounds (like the green banana test) heavily influence lightweight models.
3. **Confident Misinformation:** A simple "confidence threshold" isn't enough. If the AI is 95% confidently wrong about a dog being a banana, the filter won't catch it. 

🔮 Next Steps

Working on ideas to mitigate the OOD vulnerability — e.g., moving inference to a backend and adding similarity-based unknown detection. Details in future iterations.


---
*Built with curiosity and a hacker mindset. 🤝*
