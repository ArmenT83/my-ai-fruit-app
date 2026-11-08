# 🤖 AI Adversarial Robustness & Fruit Classifier

A browser-based Image Classifier built with **TensorFlow.js** and **Teachable Machine**, deployed on **GitHub Pages** to test model robustness and decision boundary vulnerabilities in real-world scenarios.

🚀 **Live Demo:** Try to break the model here on [GitHub Pages](https://arment83.github.io)

---

## 🎯 Project Overview & Security Research
This project explores **AI Red Teaming** and **Adversarial Machine Learning**. The goal was to analyze how a lightweight neural network extracts features (shape vs. color bias) and how environmental shifts impact decision boundaries.

### 🧪 Key Testing Scenarios & Results:
- **Yellow Banana (Baseline):** `100% Banana` — Standard input baseline.
- **Green Banana (Background Noise):** Accuracy dropped from `98%` (lab) to `79%` (web) due to background context sensitivity.
- **Black Apple (Out-of-Distribution):** `100% Apple` — Proved the model learned geometric feature boundaries rather than relying purely on color dynamics.

---

## 🛠️ Tech Stack & Architecture
- **Model Training:** Teachable Machine (Transfer Learning)
- **Deployment & Inference:** TensorFlow.js (Client-side browser execution)
- **Frontend:** HTML5, CSS3, JavaScript (Fetch & File Reader APIs)
- **Security Concept:** AI Red Teaming, Adversarial Noise Testing, Input Validation

---

## 🛡️ AI Security Takeaway
In automated verification systems or surveillance environments, attackers can exploit AI models using **Adversarial Patches** or subtle background alterations. Client-side edge deployment auditing allows us to find decision boundary flaws before attackers do.
