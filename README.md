# Differentially Private Robust Low-Rank Approximation (DP-LRA)

This project implements **Algorithm 1** from the NeurIPS 2018 paper *Differentially Private Robust Low-Rank Approximation*. The method combines **randomized sketching** with **Laplace noise injection** to compute a rank-k approximation that is both **robust to outliers** and **(ε, δ)-differentially private**.  
:contentReference[oaicite:1]{index=1}

---

## 📘 Overview

Classical low-rank approximation (via SVD) is accurate but:

- expensive for large matrices  
- sensitive to outliers  
- not differentially private  

The DP-LRA algorithm addresses these issues by:

1. Using **p-stable sketching** to achieve robustness  
2. Adding **calibrated Laplace noise** for differential privacy  
3. Reconstructing a private low-rank approximation using SVD on noisy sketches  

---

## 🧠 Method Summary

### **1. Sketching**
Generate the following using p-stable random matrices:

- \( S A \)
- \( A T \)
- \( S A T \)

These sketches reduce dimensionality while preserving the structure of A.

### **2. Differential Privacy**
Add Laplace noise to the sketches:

- \( \tilde{S}A = SA + N_1 \)
- \( \tilde{A}T = AT + N_2 \)
- \( \widetilde{SAT} = SAT + N_3 \)

Noise scales depend on:
- privacy parameter \( \varepsilon \)  
- failure probability \( \delta \)  
- p-stable sensitivity bounds  

### **3. Low-Rank Reconstruction**
Perform SVD on the noisy sketches to estimate subspaces:

- \( U_k \) from \( \tilde{S}A \)  
- \( V_k \) from \( A\tilde{T} \)  

Final reconstruction:

\[
M \approx U_k \Sigma_k V_k^\top
\]

---

## 🧪 Experiments

Experiments were run on synthetic low-rank matrices with decaying singular values.  
We evaluated the effects of:

### **Privacy parameter (ε)**
- Small ε → strong privacy → larger noise → higher error  
- Larger ε approaches non-private baseline  

### **Rank (k)**
- Increasing k improves approximation accuracy  
- Total error decreases as more singular directions are captured  

### **p-norm (1 ≤ p < 2)**
- Smaller p improves robustness to outliers  
- Slightly increases variance  

### **Sketch sizes (s, t, φ, ψ)**
- Larger sketch sizes reduce error  
- Extremely large sketches show diminishing returns  
- Optimal sketch size depends on matrix dimension and target rank  

---

## 📈 Key Findings

- Clear **privacy–utility tradeoff**: higher privacy reduces accuracy  
- p-stable sketches enable robustness under the ℓ₁/ℓ_p norms  
- Sketch size and rank are the strongest factors for reducing error  
- Algorithm reconstructs useful approximations under moderate noise levels  
- Behavior matches theoretical error bounds from the NeurIPS paper  

---

## ✅ Conclusion

This project demonstrates a practical implementation of **differentially private, robust low-rank approximation**.  
It confirms that Algorithm 1:

- preserves robust structure using p-stable embeddings  
- provides differential privacy via Laplace noise  
- achieves competitive accuracy with properly chosen sketch sizes and privacy budgets  

The implementation serves as a complete, reproducible framework for experimenting with DP-LRA techniques.

---

## 📚 Reference

**Differentially Private Robust Low-Rank Approximation**  
NeurIPS 2018  
(Original algorithm implemented in this project.)

