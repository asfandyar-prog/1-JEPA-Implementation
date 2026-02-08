🧠 Toy I-JEPA (Image Joint Embedding Predictive Architecture)

A minimal, from-scratch PyTorch implementation of a toy I-JEPA-style self-supervised vision model, inspired by Meta AI’s Image Joint Embedding Predictive Architecture.

This repository is not a reproduction of the full I-JEPA paper.
Instead, it is designed to build deep intuition about the core ideas behind JEPA-style learning by implementing the smallest possible working system.

⸻

📌 Motivation

Modern self-supervised learning methods often rely on:
	•	heavy data augmentations
	•	pixel-level reconstruction
	•	contrastive objectives with negative samples

JEPA takes a different route:

Learn by predicting missing representations from visible context — without reconstructing pixels and without contrastive losses.

This project focuses on understanding that idea clearly and concretely, without abstraction-heavy frameworks or large-scale engineering.

⸻

🔍 What This Project Implements

✔ Patch-based Vision Transformer (ViT-style) encoder
✔ Context–target masking over image patches
✔ Student–teacher (EMA) architecture
✔ Predictor that infers target representations from context representations
✔ L2 loss in representation space (no reconstruction, no contrastive loss)
✔ Visualization of context vs target patches on real images

⸻

❌ What This Project Does NOT Do
	•	❌ No large-scale pretraining
	•	❌ No multi-crop or heavy data augmentations
	•	❌ No classification head or downstream evaluation
	•	❌ No pixel reconstruction (not MAE)
	•	❌ No contrastive learning (not DINO / SimCLR)

This is an educational + research-intuition implementation.

⸻

🧩 High-Level Architecture

Input Image
   │
   ├─ Patch Embedding (16×16)
   │
   ├─ Context Mask ──► Student Encoder ──► Context Representations
   │
   ├─ Target Mask ───► Teacher Encoder ──► Target Representations (EMA, no grad)
   │
   └─ Predictor
        └─ Predict target representations from context


Training Objective

\mathcal{L} = \| \hat{z}_{target} - z_{target} \|_2^2

⸻

🧪 Dataset
	•	CIFAR-10, resized to 224 × 224
	•	Used only to test correctness and learning dynamics
	•	No labels are used (fully self-supervised)

⸻

📊 Visualization

The code includes a visualization showing:
	•	🟩 Green patches → context (visible to student)
	•	🟥 Red patches → target (hidden, must be predicted)

This helps verify that:
	•	the masking logic is correct
	•	the learning task matches the JEPA formulation

⸻

🚀 How to Run
	1.	Open the notebook / script
	2.	Run top → bottom
	3.	Verify:
	•	loss decreases
	•	visualization appears correctly
	•	no runtime / autograd / device errors

The model is intentionally small and should run on:
	•	CPU
	•	Colab
	•	Kaggle
	•	Consumer GPUs

⸻

🧠 Key Takeaways
	•	JEPA learns semantics, not pixels
	•	Prediction happens in representation space
	•	No contrastive negatives are required
	•	The teacher provides a stable target via EMA
	•	Masking defines what must be understood, not what must be reconstructed

⸻

📚 References
	•	LeCun et al., “Self-Supervised Learning: The Dark Matter of Intelligence”
	•	Assran et al., “I-JEPA: Self-Supervised Learning from Images by Predicting Joint Embeddings”
	•	Vision Transformer (Dosovitskiy et al.)

⸻

⚠️ Disclaimer

This code is not an official implementation of I-JEPA and should not be used for benchmarking or performance claims.

It exists purely to:

understand, reason about, and experiment with JEPA-style learning.

⸻

✨ Author Note

This project was built through iterative debugging and reasoning, not copy-paste.
If you are reading the code carefully and asking why each part exists — you are using it correctly.
