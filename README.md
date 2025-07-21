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

📉 Results
Model	Clean Accuracy	Under Attack (ε=0.2)
Target (MLP)	~97%	~XX% (drops!)
Surrogate	~95%	-

Transfer success rate ≈ XX% (how many adversarial examples fooled the target)

🎯 Why This Is Realistic
This simulates a real-world adversarial scenario:

The attacker does not have access to the victim model

They build a surrogate and craft attacks locally

These attacks are transferred to the victim with surprising effectiveness

This is common in:

Facial recognition evasion

Security bypass of ML models in production

Adversarial testing for model robustness

🔐 Files
main.ipynb: full pipeline with training, FGSM, and transfer attack

model_target.pth: saved model to simulate the victim

.venv/: local Python environment (not pushed)

🧑‍💻 Author
Emanuele Rossi – AI Red Teaming portfolio
Project 3 of the Red Team series: black-box adversarial ML