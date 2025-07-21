# Black-Box Adversarial Attack on MNIST (Transfer-Based)

This project demonstrates how to perform a **black-box adversarial attack** using **transferability** between models. The attacker does **not have access to the target model’s architecture or gradients**, but can train a local substitute model and craft adversarial inputs using it.

## 🧠 What It Demonstrates

- A **target model** is trained on MNIST but treated as a black-box: we never access its weights or gradients.
- A **surrogate model** is trained by the attacker with the same data distribution.
- The attacker generates adversarial examples on the surrogate using **FGSM**.
- These examples are used to attack the target.  
→ If the target misclassifies, the transfer attack was successful.

## 🧪 Workflow

| Step | Description |
|------|-------------|
| 1️⃣ | Train a target model on MNIST (to be attacked later) |
| 2️⃣ | Train a surrogate model (different architecture) |
| 3️⃣ | Generate adversarial examples on the surrogate using FGSM |
| 4️⃣ | Feed those examples to the target model and measure performance drop |

## ⚔️ Attack Technique

**Fast Gradient Sign Method (FGSM)**  
Adds a small perturbation in the direction of the gradient to cause misclassification.  
On the surrogate model:

```python
perturbed = image + epsilon * sign(∇_image Loss(model(image), label))

These perturbed images are then used against the target model — even though no gradients or internal access is available for it.

## Results

| Model          | Clean Accuracy | Under Attack (ε=0.2) |
| -------------- | -------------- | -------------------- |
| **Target (MLP)**   | ~97%           | ~XX% (drops!)        |
| **Surrogate**      | ~95%           | –                    |

**Transfer success rate:** ≈ XX%  
*(Percentage of adversarial examples crafted on the surrogate that fooled the target model.)*

---

## Why This Is Realistic

- **No white‑box access:** Attacker never sees the victim’s gradients or internal structure.  
- **Surrogate-based crafting:** Adversarial examples are generated locally on a stand‑in model.  
- **Effective transfer:** Perturbed inputs still fool the unseen target with high success.  

_Common real‑world uses:_  
- Facial recognition evasion  
- Security bypass of ML models in production  
- Adversarial robustness testing  

---

## Files

- `main.ipynb` — Full pipeline with training, FGSM attack, and transfer evaluation  
- `model_target.pth` — Saved weights simulating the victim (target) model  
- `.venv/` — Local Python environment (excluded from repository)  

---

## Author

**Emanuele Rossi**  
AI Red Teaming portfolio  
_Project 3 of the Red Team series: black‑box adversarial ML_  
