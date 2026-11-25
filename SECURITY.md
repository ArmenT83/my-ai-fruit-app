# 🔒 Security Research Report

**Project:** AI Adversarial Robustness & Fruit Classifier
**Scope:** Client-side image classifier (TensorFlow.js + Teachable Machine)
**Methodology:** Adversarial testing inspired by OWASP Top 10 frameworks (see note on frameworks below)
**Date:** November 2026
**Author:** [твоё имя с LinkedIn]

---

## 1. Scope & Objective

The goal of this exercise was to red team my own AI project: a lightweight image classifier distinguishing apples and bananas, deployed as a browser app. The focus was on adversarial inputs and out-of-distribution behavior — how the model reacts when real-world inputs deviate from training conditions.

## 2. Model Overview

- **Architecture:** Transfer learning (Teachable Machine / MobileNet-based feature extractor + custom head)
- **Training data:** Small personal dataset (apples / bananas on uniform background)
- **Inference:** Client-side (TensorFlow.js in the browser)

## 3. Phase 1 — Baseline & Robustness Testing

| Test | Input | Result | Observation |
| :--- | :--- | :--- | :--- |
| Baseline | Yellow banana | 100% Banana | Standard input |
| Background shift | Green banana (web photo) | 98% → 79% | Accuracy drop due to background sensitivity |
| OOD generalization | Black apple | 100% Apple | Model learned shape, not color |

**Insight:** background context became part of the decision signal — a classic sign of data bias in a small training set.

## 4. Phase 2 — Adversarial Testing

| # | Attack Vector | Result | Status |
| :--- | :--- | :--- | :--- |
| 1 | Text-on-Image Injection ("I AM AN APPLE") | Ignored by AI (100% Banana) | 🟢 Resisted |
| 2 | Adversarial Patch (chessboard pattern) | Resisted local noise (100% Banana) | 🟢 Resisted |
| 3 | Out-of-Distribution Input (dog photo) | Falsely predicted Banana (95%) | 🔴 Failed |

### 4.1 Text-on-Image Injection
Text "I AM AN APPLE" written directly on a banana. The model ignored the text entirely and relied on shape/color features. Conclusion: the model does not read text; adversarial text overlays are not an attack vector for this architecture.

### 4.2 Adversarial Patch
A high-contrast chessboard pattern pasted on the banana. The model still predicted Banana (100%). Conclusion: the model prioritizes global shape over local noise; it resists simple patch attacks but may remain vulnerable to optimized (gradient-based) adversarial patches.

### 4.3 Out-of-Distribution Input (Critical Finding 🔴)
A Shiba Inu photo — a class the model has never seen. The model predicted **Banana: 95%** with high confidence.

**Confident Misinformation:** the model cannot say "I don't know." It forces the closest match. A simple confidence threshold would not catch this failure: the output looks perfectly normal (95%) while being wrong.

**Real-world impact:** in automated verification or filtering systems, such behavior means unknown objects silently pass as a known class.

## 5. Note on Frameworks

Attack categories were originally referenced against the OWASP LLM Top 10 for consistency with my ongoing AI Red Teaming track. Since this project is a pure ML (vision) classifier rather than an LLM, the more precise mapping is the OWASP Machine Learning Security Top 10 (adversarial attack, distribution shift).

## 6. Mitigation Ideas (Next Steps)

- Move inference to a backend (prerequisite for server-side security controls).
- Add input validation and rate-limiting once server-side inference is in place.
- Implement similarity-based OOD detection (e.g., cosine distance over feature vectors) to reject unknown classes before the classifier forces a prediction.

## 7. Conclusion

The model resists naive visual attacks (text injection, simple patch) but fails on out-of-distribution inputs with high confidence. The main lesson: **a confidence score is not a measure of correctness.** Robustness must be tested against what the model has *never seen*, not only against perturbations of known classes.

---
*This research was performed on my own project. Feedback welcome — connect with me on [LinkedIn]www.linkedin.com/in/
armen-t-961210413
.*
