# Stochastic Interest Rate Term Structure Modeling 📈

An institutional-grade implementation of the **Cox-Ingersoll-Ross (CIR)** single-factor interest rate model, alongside an **Affine Jump-Diffusion (AJD)** extension. This project successfully reconstructs the out-of-sample yield curve relying strictly on a 3-Month instantaneous short-rate proxy, achieving a highly robust **0.93 Out-of-Sample R²**.

## 🚀 Key Methodologies & Mathematical Architecture

* **Strict Q-Measure Calibration:** Utilizes cross-sectional Non-Linear Least Squares to directly map the risk-neutral measure ($\mathbb{Q}$) rather than relying on historical P-measure transition densities.
* **Bounded Gradient Descent (SLSQP & L-BFGS-B):** Replaces standard heuristic algorithms (like Nelder-Mead) with advanced gradient optimizers to mathematically enforce the Feller Condition ($2\kappa\theta \ge \sigma^2$) and prevent negative simulated rates.
* **Horizon-Targeted Asymptotic Weighting:** Standard 1-factor models often suffer from "curve whiplash" when fitting 30-Year bonds. This model deploys an inverse-maturity weighting array ($\frac{2.0}{\tau}$) to successfully anchor the 2.0Y prediction tail while preserving the model's ability to learn the long-run macroeconomic trend ($\theta$).
* **Jump-Diffusion Compensator:** Extends the stochastic differential equation (SDE) with a Compound Poisson Jump Process to model macroeconomic shocks (e.g., emergency rate cuts) while preserving affine tractability via numerical integration.

## 📊 Performance Metrics

* **Base CIR Composite Out-of-Sample R²:** ~0.93
* **Jump-Diffusion Composite Out-of-Sample R²:** ~0.89
* Successfully defended the 2.0Y maturity tail from algorithmic collapse, a common failure point in single-factor curve reconstruction. *(Note: The Base CIR generalized slightly better out-of-sample, demonstrating a classic bias-variance tradeoff where the JD extension's flexibility acts as a structural drag during non-volatile test periods).*

## 📂 Repository Contents

* `Parth_Vaish_CIR_Predictions.csv` — **[Audit File]** The final exported matrix of out-of-sample yield curve predictions for both models, provided for direct verification.
* `Parth_Vaish_CIR_Project_FinClub.ipynb` — The notebook containing the OOP pipeline, calibration engine, vectorized yield plotting, and critical theoretical analysis.

## 🛠️ Tech Stack

**Language:** Python 3  
**Libraries:** `SciPy` (Optimize, Integrate) | `NumPy` | `Pandas` | `scikit-learn` | `Matplotlib` / `Seaborn`
