# System-Identification-using-ARX-OE-MATLAB
System identification using ARX and OE models with residual analysis, model selection, and complexity–accuracy trade-offs.

# System Identification: ARX vs OE (Residual Analysis + Model Selection)

This project documents a system identification workflow comparing ARX and Output-Error (OE) models using goodness-of-fit and residual diagnostics.  
The goal is to select a model that balances **accuracy** and **complexity**, supported by statistical validation.

## Contents
- 📄 Report: `report/System_Identification_Coursework_Ben.pdf`
- 📊 Figures: `figures/` (recommended: export plots from the report into images)
- 💻 Code: `code/` (optional — add MATLAB scripts if you want reproducibility)

---

## Problem Overview
Given input–output data from a dynamic system, identify a parametric model that:
1. Fits measured output well
2. Produces residuals consistent with white noise (independent over time and from the input)
3. Avoids unnecessary complexity (over-parameterization)

---

## Methodology
### 1) ARX Identification (Exercise 1)
- Selected ARX structure after trial-and-error tuning of orders.
- Chosen structure: **na = 1, nb = 9, nk = 5**
- Achieved **87.41% fit**.
- Residual diagnostics:
  - Residual autocorrelation within **99% confidence bounds**
  - Input–residual cross-correlation within **99% confidence bounds**
  - Conclusion: residuals behave like white noise → model captures useful dynamics.

### 2) OE Identification + Comparison (Exercise 2)
Three OE candidates were compared:

| Model | nb | nf | nk | Fit (%) | Notes |
|------:|---:|---:|---:|--------:|------|
| oe125 | 1  | 2  | 5  | 79.26   | Underfit; diagnostics occasionally violate confidence bounds |
| oe235 | 2  | 3  | 5  | 86.98   | Strong fit + good diagnostics with moderate complexity |
| oe185 | 1  | 8  | 5  | 87.44   | Highest fit but higher order increases complexity |

### 3) Model Selection (Exercise 3)
**Selected model: oe235**  
Reason: It provides near-top fit with clean residual diagnostics while avoiding the extra parameters of oe185. Higher-order parameters approaching zero in oe185 suggest unnecessary complexity and potential noise-fitting.

### 4) Final ARX vs OE Comparison (Exercise 4)
- ARX slightly higher fit (~0.43%) but uses **~2× parameters** (10 vs 5).
- Both models pass residual correlation tests.
- Residual histograms are approximately normal; OE shows tighter concentration around zero.
- **Final choice: OE (oe235)** as the best complexity–accuracy trade-off.

---

## Key Results
- ARX achieved strong fit with validated residual behavior.
- OE model **oe235** achieved comparable accuracy with fewer parameters and strong diagnostics.
- Final recommendation: **OE (oe235)** for efficient and robust modeling.

---

## How to Reproduce (optional)
If code/data are added later, include:
1. MATLAB version + System Identification Toolbox
2. Steps:
   - Load dataset
   - Fit ARX + OE models
   - Validate via residual analysis
   - Compare fits + histograms

---

## Skills Demonstrated
- System Identification (ARX, OE)
- Residual diagnostics (autocorrelation, cross-correlation)
- Bias–variance / complexity trade-off reasoning
- MATLAB modeling workflow and quantitative validation

---

## Author
Ben Paul Richard
