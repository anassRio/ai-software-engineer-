# 00 — AI Fundamentals

**Goal**: Understand the core ML/AI concepts you actually need, from a Software Engineer perspective.  
**Duration**: 1-2 weeks  
**Outcome**: You can explain how neural networks learn and why this matters for LLMs

---

## 🎯 Objective

Build foundational understanding in machine learning **as it relates to LLMs and agents**.

You're NOT becoming a data scientist. You're learning enough to:
- Understand what LLMs actually do (next module)
- Know what's possible and what's not
- Recognize overfitting, training dynamics, limitations
- Understand why certain architectural choices matter

---

## 🧠 Core Concepts to Master

### The Learning Process
- **Supervised learning**: Model learns from input → output examples
- **Training vs Inference**: Two completely different phases
- **Weights & Parameters**: What the model actually "learns"
- **Loss function**: How we measure "badness" (lower is better)
- **Gradient descent**: How we improve weights (step-by-step optimization)
- **Backpropagation**: Computing gradients efficiently

### Neural Networks Basics
- **Layers**: Input → Hidden → Output
- **Activation functions**: Why non-linearity matters
- **Forward pass**: Compute prediction
- **Backward pass**: Compute gradients, update weights
- **Epochs & iterations**: How many times we see data

### Important Constraints
- **Overfitting**: Model memorizes training data instead of learning
- **Underfitting**: Model too simple to capture patterns
- **Generalization**: Does it work on NEW data?
- **Data quality**: Garbage in = garbage out

### Infrastructure
- **GPUs**: Why training needs special hardware
- **Scaling**: Bigger models need more data and compute
- **Inference**: Running trained models is cheaper than training

---

## 📋 What You Actually Need to Know

### ✅ Essential
- [ ] Supervised learning: input → model → output
- [ ] Training: adjusting weights to minimize loss
- [ ] Inference: using trained model to make predictions
- [ ] Overfitting: when generalization fails
- [ ] Why gradients matter (rough explanation is fine)
- [ ] Forward pass → compute loss → backward pass → update weights

### ⚠️ Nice to Have
- [ ] Linear algebra (vectors, matrices, dot product)
- [ ] Calculus derivatives (conceptual understanding)
- [ ] Different activation functions (ReLU, sigmoid, tanh)
- [ ] Batch normalization, dropout
- [ ] Optimization algorithms (Adam, SGD)

### ❌ Skip For Now
- Convolutional networks (CNN) in depth
- Recurrent networks (RNN/LSTM) in depth
- Reinforcement learning
- Advanced regularization techniques
- Mathematical proofs

---

## 📚 Resources

### Video (Best for Intuition)
- **3Blue1Brown - Neural Networks Series** (4 videos, ~60 min total)
  - https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R4_67m3IWWaRW45K369
  - Most intuitive explanation available
  - No math required, great visuals
  - START HERE

### Structured Course (Optional)
- **DeepLearning.AI - Machine Learning Specialization** (Andrew Ng)
  - https://www.deeplearning.ai/
  - More formal, comprehensive
  - Can audit for free

### Written (Reference)
- **Neural Networks from Scratch** (interactive)
  - https://nnfs.io/
  - Code-first explanation in Python

---

## 💻 Labs (Hands-On Practice)

Do these in order. Each teaches a specific concept through code.

### Lab 1: Simple Perceptron (15 min)
**What you'll build**: A single neuron that learns to classify points

**Concepts**: Forward pass, loss, update rule  
**Language**: Python + NumPy (no frameworks)

**Steps**:
1. Initialize random weights
2. Compute prediction: `y_pred = w * x + b`
3. Compute loss: `loss = (y_pred - y_true)^2`
4. Compute gradient (or use numerical approximation)
5. Update weights: `w = w - lr * gradient`
6. Repeat 100 times, watch loss decrease
7. Test on new data points

**What you learn**: The absolute basics of training

**File**: `labs/lab-01-simple-perceptron.py`

---

### Lab 2: Training vs Inference (20 min)
**What you'll build**: Observe that training and inference are different

**Concepts**: Dropout, batch norm behave differently in each phase

**Steps**:
1. Build a small 2-layer network
2. Train it on MNIST digits (28x28 pixels → 10 classes)
3. Track training loss (should decrease)
4. Track validation loss (should decrease but maybe plateau)
5. When training loss < validation loss = overfitting
6. Use the trained model for inference on test data
7. Measure accuracy

**What you learn**: Overfitting is real. Inference is just forward pass (fast). Training is expensive.

**File**: `labs/lab-02-training-vs-inference.py`

---

### Lab 3: The Learning Rate Experiment (20 min)
**What you'll build**: Understand how hyperparameters affect training

**Concepts**: Learning rate, convergence, instability

**Steps**:
1. Train the same network with different learning rates: [0.001, 0.01, 0.1, 1.0]
2. Plot loss curves for each
3. Observe:
   - Too small LR: converges slowly or not at all
   - Good LR: smooth convergence
   - Too large LR: loss explodes (unstable)
4. Find the sweet spot

**What you learn**: Hyperparameters matter. There's a tradeoff.

**File**: `labs/lab-03-learning-rate.py`

---

## 🔬 Mental Model

```
┌────────────────────────────────────────────────────────────────────────┐
│ TRAINING (expensive, offline, iterative)                    │
├────────────────────────────────────────────────────────────────────────┤
│ 1. Start with random weights                                │
│ 2. Forward pass: Input → Network → Prediction              │
│ 3. Compute loss: How wrong is prediction?                   │
│ 4. Backward pass: Where did error come from?               │
│ 5. Gradient: How to adjust each weight                      │
│ 6. Update weights: w = w - learning_rate * gradient        │
│ 7. Repeat 1000s of times on millions of examples           │
│ 8. Validation: Does it work on data we didn't train on?    │
│ 9. Save trained weights                                     │
└────────────────────────────────────────────────────────────────────────┘
                          ↓
┌────────────────────────────────────────────────────────────────────────┐
│ INFERENCE (cheap, online, single pass)                      │
├────────────────────────────────────────────────────────────────────────┤
│ 1. Load trained weights                                     │
│ 2. Forward pass: Input → Network → Prediction              │
│ 3. Return prediction                                        │
│ ✓ No backprop. No gradient computation. No weight updates. │
│ ✓ Can run on CPU (fast). Can run millions of times.        │
└────────────────────────────────────────────────────────────────────────┘
```

**Key insight**: Training is slow, inference is fast. This is why GPT is expensive to train but cheap to use.

---

## ✅ Validation Checklist

You've mastered this module when you can:

- [ ] Explain the difference between training and inference in simple words
- [ ] Explain why gradient descent helps training (no math required)
- [ ] Build and train a simple network from scratch (NumPy)
- [ ] Identify overfitting when looking at training vs validation curves
- [ ] Explain what learning rate does and why it matters
- [ ] Answer: "Is bigger model always better?" (No, with reasons)
- [ ] Explain: "Where do model weights come from?" (Training)
- [ ] Explain: "Why do we need GPUs?" (Matrix multiplication is expensive)

---

## 📝 Notes

*Fill this in as you progress:*

- Key insights I learned:

- Concepts I need to revisit:

- Connection to my existing software engineering knowledge:

- Questions for next module:

---

## 📊 Progress

- [ ] Watched 3Blue1Brown series
- [ ] Understand forward pass → loss → backward pass → update
- [ ] Completed Lab 1 (simple perceptron)
- [ ] Completed Lab 2 (training vs inference)
- [ ] Completed Lab 3 (learning rate experiment)
- [ ] Can explain key concepts to someone else
- [ ] Validation checklist complete

---

## 🎯 Next Steps

When ready for **Module 01 (LLM Fundamentals)**:

✅ You understand that neural networks learn by adjusting weights  
✅ You know training and inference are different  
✅ You recognize overfitting and basic training dynamics  

**Next**: Understand how transformers specifically work (the architecture behind all modern LLMs)

---

**Previous**: None (start here)  
**Next**: [01 — LLM Fundamentals](../01-llm/)