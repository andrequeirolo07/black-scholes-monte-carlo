# Monte Carlo Option Pricing under Black–Scholes (Python)

**Summary**  
This project was developed as part of my MSc mathematical finance preparation.  
It implements a Monte Carlo pricer for European call and put options and validates the results against the analytical Black–Scholes model.  
The notebook includes 95% confidence intervals, convergence diagnostics, and plots saved automatically to the `plots/` folder.



---

## Math quickview

**Risk-neutral GBM dynamics**

dS_t = (r - q) * S_t * dt + sigma * S_t * dW_t

**Black–Scholes closed form (European call/put)**

d1 = [ ln(S0/K) + (r - q + 0.5*sigma^2)*T ] / (sigma * sqrt(T))
d2 = d1 - sigma * sqrt(T)

Call = S0 * exp(-qT) * N(d1) - K * exp(-rT) * N(d2)
Put = K * exp(-rT) * N(-d2) - S0 * exp(-qT) * N(-d1)

**Monte Carlo estimator**
Price ≈ exp(-rT) * mean(payoff(ST))
SE ≈ exp(-rT) * std(payoff(ST)) / sqrt(N)
95% CI ≈ Price ± 1.96 * SE

Error shrinks on the order of 1/sqrt(N).

---

## Files

- `mc_price.ipynb` — Jupyter notebook with code, explanations, and outputs  
- `requirements.txt` — Python dependencies  
- `.gitignore` — ignore junk files  
- `LICENSE` — MIT license  
- `plots/gbm_paths.png` — simulated GBM paths  
- `plots/terminal_hist.png` — histogram of terminal prices  
- `plots/convergence.png` — convergence of MC price to Black–Scholes  

---

## Results (textbook inputs)

**Parameters:** S0 = 100, K = 100, r = 2%, q = 0%, sigma = 20%, T = 1 year  

- **Monte Carlo (50,000 sims)**  
  - Call ≈ 8.9624 (SE 0.0622, 95% CI [8.840495624408408, 9.084334708282196])  
  - Put  ≈ 6.9599 (SE 0.0436, 95% CI [6.874518751772253, 7.045374187808121])  

- **Black–Scholes**  
  - Call = 8.9160  
  - Put  = 6.9359 

**Check.** The MC values fall inside the confidence intervals around the BS benchmarks, confirming correctness.  

**Plots.**  
- *GBM paths* show simulated price trajectories.  
- *Terminal distribution* illustrates dispersion of $S_T$.  
- *Convergence plot* shows MC estimates stabilizing around BS as $N$ increases.  

---

## How to run

```bash
conda create -n quant python=3.11 -y
conda activate quant
pip install -r requirements.txt
jupyter lab


## Development log

- **2025-09-18** — Set up project folder structure and initialized Git repository.  
- **2025-09-19** — Installed Python environment, configured VS Code, and created first notebook file.  
- **2025-09-20** — Implemented Black–Scholes pricing functions and verified with test parameters.  
- **2025-09-21** — Added GBM path simulator and Monte Carlo pricer; validated against BS; saved plots.  
- **2025-09-22** — Wrote Markdown explanations (overview, math quickview, results) and polished notebook for readability.  
- **2025-09-23** — Created supporting files (`README.md`, `requirements.txt`, `.gitignore`, `LICENSE`) and finalized repo structure.  


## Results Note
With parameters \(S_0 = 100\), \(K = 100\), \(r = 2\%\), and \(\sigma = 20\%\):
- Monte Carlo estimate for the call option ≈ **8.9624**
- Black–Scholes analytical price = **8.9160**

The Monte Carlo estimate falls within the expected 95 % confidence interval and converges toward the theoretical value as \(N\) increases, demonstrating correct implementation.
