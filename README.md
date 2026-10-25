# Model Criticism via Stochastic Optimization

Worked examples accompanying the paper *Model Criticism via Stochastic Optimization* by Ren-Yi Wang
(Irving Institute for Cancer Dynamics, Columbia University).

Many generative models are specified by how data are simulated. An observation is a deterministic
transform `Y = G(θ, X)` of a draw `X` from an assumed noise law. The procedure in the paper tests whether
such a model fits the data and, when it does not, shows **where** it fails, without choosing a test
statistic. It splits the data into an estimation block and a held-out block:

1. **Estimation stage.** Fit `θ` on the first block by minimizing a Wasserstein distance between the data
   and simulations from the model, with the noise law held fixed (robust and strongly consistent).
2. **Recourse stage.** Freeze `θ`, push a finite set of representative noise values (the `N₁`-medoid of
   simulated noise) through the fitted mechanism to obtain model atoms, and let the held-out block
   reweight them. The optimal weights are the held-out frequencies of the atoms' cells; comparing them with
   the fitted model's own cell probabilities localizes the misspecification, and a Pearson test on the cell
   counts is calibrated by the split.

## Contents

| file | description |
|---|---|
| `model_critic_via_stoch_op.ipynb` | all four examples of the paper |
| `requirements.txt` | Python dependencies |

The notebook contains four examples:

- **Gaussian location–scale family** with heavy-tailed (`t2`) and contaminated data; size and power of the
  Pearson test, a prior-misspecification check, and a comparison with split predictive checks and
  uniform parametrization checks.
- **Number of segregating sites under Kingman's coalescent**, with exponential population growth as the
  misspecification; the recourse is also displayed on the noise space (genealogy length × mutation-clock rate).
- **Yule (pure birth) process** written as a stochastic differential equation driven by a Poisson random
  measure, with a saturating, state-dependent birth rate as the misspecification; the diagnostic is shown
  in observation space and in noise space (Poisson sample paths).
- **Ornstein–Uhlenbeck diffusion** through its Itô map, with a driving noise concentrated near the origin as
  the misspecification; the diagnostic is read off paths in both spaces.

## Running the notebook

The notebook needs only `numpy`, `pandas` and `matplotlib`; the few distribution functions, tail
probabilities and derivative-free optimizers it uses are implemented in its first cells, so it does not
depend on `scipy`.

```bash
git clone https://github.com/RenYiW/Model-Criticism-via-Stochastic-Optimization.git
cd Model-Criticism-via-Stochastic-Optimization
python -m venv .venv && source .venv/bin/activate      # optional
pip install -r requirements.txt
jupyter lab model_critic_via_stoch_op.ipynb
```

A full run takes roughly 15–20 minutes on a laptop, dominated by the size and power study of the Gaussian
example. Set `QUICK = True` in the second cell for a fast pass with small replicate numbers (the numbers are
then only illustrative).

## Citation

If you use this code, please cite the paper:

```bibtex
@unpublished{wang2026model,
  author = {Wang, Ren-Yi},
  title  = {Model Criticism via Stochastic Optimization},
  year   = {2026},
  note   = {Manuscript}
}
```

## License

MIT License; see `LICENSE`.
