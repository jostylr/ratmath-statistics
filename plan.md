# Statistics Package Plan

This document outlines the plan for the `stats` package, providing probability distributions, statistical functions, and graphics primitives for data visualization within the ratmath ecosystem.

## Package Structure

```
packages/stats/
├── src/
│   ├── index.js              # Main exports and registration
│   ├── ratmath-module.js     # VariableManager module integration
│   ├── descriptive.js        # Descriptive statistics (mean, variance, etc.)
│   ├── distributions.js      # Probability distributions
│   ├── hypothesis.js         # Hypothesis testing
│   ├── regression.js         # Regression analysis
│   ├── sampling.js           # Random sampling and simulation
│   ├── combinatorics.js      # Counting and probability helpers
│   └── graphics.js           # Statistical graphics primitives
├── help/
│   ├── stats.txt             # Main package help
│   ├── distributions.txt     # Distribution reference
│   └── regression.txt        # Regression help
├── tests/
│   ├── descriptive.test.js
│   ├── distributions.test.js
│   ├── regression.test.js
│   └── sampling.test.js
└── package.json
```

---

## Philosophy

The stats package emphasizes:
- **Exact rational arithmetic** where possible (means, variances of rational data)
- **Oracle-based** computation for irrational quantities (normal CDF, etc.)
- **Integration with graphics** for statistical visualization
- **Educational clarity** with step-by-step computations available

---

## Category 1: Descriptive Statistics

### Central Tendency

| Function | Signature | Description |
|----------|-----------|-------------|
| `Mean` | `Mean(data)` | Arithmetic mean |
| `Median` | `Median(data)` | Median value |
| `Mode` | `Mode(data)` | Most frequent value(s) |
| `GeometricMean` | `GeometricMean(data)` | Geometric mean (oracle) |
| `HarmonicMean` | `HarmonicMean(data)` | Harmonic mean |
| `TrimmedMean` | `TrimmedMean(data, pct)` | Trimmed mean |
| `WeightedMean` | `WeightedMean(data, weights)` | Weighted average |

### Dispersion

| Function | Signature | Description |
|----------|-----------|-------------|
| `Variance` | `Variance(data, pop?)` | Variance (sample or population) |
| `StdDev` | `StdDev(data, pop?)` | Standard deviation (oracle) |
| `Range` | `Range(data)` | Max - Min |
| `IQR` | `IQR(data)` | Interquartile range |
| `MAD` | `MAD(data)` | Mean absolute deviation |
| `CV` | `CV(data)` | Coefficient of variation |

### Quantiles & Percentiles

| Function | Signature | Description |
|----------|-----------|-------------|
| `Quantile` | `Quantile(data, p)` | p-th quantile (0 ≤ p ≤ 1) |
| `Percentile` | `Percentile(data, p)` | p-th percentile |
| `Quartiles` | `Quartiles(data)` | Q1, Q2, Q3 |
| `FiveNum` | `FiveNum(data)` | Five-number summary |
| `Deciles` | `Deciles(data)` | Decile boundaries |

### Shape

| Function | Signature | Description |
|----------|-----------|-------------|
| `Skewness` | `Skewness(data)` | Skewness coefficient |
| `Kurtosis` | `Kurtosis(data)` | Kurtosis (excess) |
| `Moments` | `Moments(data, n)` | First n moments |

### Data Summaries

| Function | Signature | Description |
|----------|-----------|-------------|
| `Summary` | `Summary(data)` | Full statistical summary |
| `FreqTable` | `FreqTable(data)` | Frequency table |
| `RelFreq` | `RelFreq(data)` | Relative frequencies |
| `CumFreq` | `CumFreq(data)` | Cumulative frequencies |

---

## Category 2: Probability Distributions

### Discrete Distributions

| Distribution | Functions | Parameters |
|--------------|-----------|------------|
| **Binomial** | `BinomialPMF`, `BinomialCDF`, `BinomialQuantile` | n, p |
| **Poisson** | `PoissonPMF`, `PoissonCDF`, `PoissonQuantile` | λ |
| **Geometric** | `GeometricPMF`, `GeometricCDF` | p |
| **NegBinomial** | `NegBinomialPMF`, `NegBinomialCDF` | r, p |
| **Hypergeometric** | `HypergeomPMF`, `HypergeomCDF` | N, K, n |
| **Uniform (discrete)** | `DiscreteUniformPMF` | a, b |

### Continuous Distributions

| Distribution | Functions | Parameters |
|--------------|-----------|------------|
| **Normal** | `NormalPDF`, `NormalCDF`, `NormalQuantile` | μ, σ |
| **StandardNormal** | `Phi`, `PhiInv` | (none) |
| **Uniform** | `UniformPDF`, `UniformCDF` | a, b |
| **Exponential** | `ExponentialPDF`, `ExponentialCDF` | λ |
| **Gamma** | `GammaPDF`, `GammaCDF` | α, β |
| **Beta** | `BetaPDF`, `BetaCDF` | α, β |
| **ChiSquare** | `ChiSqPDF`, `ChiSqCDF`, `ChiSqQuantile` | df |
| **StudentT** | `TPDF`, `TCDF`, `TQuantile` | df |
| **F** | `FPDF`, `FCDF`, `FQuantile` | df1, df2 |
| **Cauchy** | `CauchyPDF`, `CauchyCDF` | x₀, γ |
| **Lognormal** | `LognormalPDF`, `LognormalCDF` | μ, σ |
| **Weibull** | `WeibullPDF`, `WeibullCDF` | k, λ |

### Distribution Object Pattern

```
D := Normal(0, 1)         # Create distribution object
PDF(D, 0)                 # → 0.3989... (oracle)
CDF(D, 1.96)              # → 0.975 (oracle)
Quantile(D, 0.975)        # → 1.96 (oracle)
Mean(D)                   # → 0
Variance(D)               # → 1
Random(D)                 # → random sample
Random(D, 100)            # → 100 random samples
```

### Distribution Properties

| Function | Signature | Description |
|----------|-----------|-------------|
| `DistMean` | `DistMean(D)` | Expected value |
| `DistVar` | `DistVar(D)` | Variance |
| `DistStd` | `DistStd(D)` | Standard deviation |
| `DistMode` | `DistMode(D)` | Mode |
| `DistMedian` | `DistMedian(D)` | Median |
| `DistSkew` | `DistSkew(D)` | Skewness |
| `DistKurt` | `DistKurt(D)` | Kurtosis |
| `DistMGF` | `DistMGF(D, t)` | Moment generating function |

---

## Category 3: Hypothesis Testing

### One-Sample Tests

| Function | Signature | Description |
|----------|-----------|-------------|
| `ZTest` | `ZTest(data, mu0, sigma)` | Z-test for mean |
| `TTest` | `TTest(data, mu0)` | One-sample t-test |
| `PropTest` | `PropTest(x, n, p0)` | Proportion test |
| `ChiSqGOF` | `ChiSqGOF(observed, expected)` | Chi-square goodness of fit |

### Two-Sample Tests

| Function | Signature | Description |
|----------|-----------|-------------|
| `TTest2` | `TTest2(data1, data2, paired?)` | Two-sample t-test |
| `PropTest2` | `PropTest2(x1, n1, x2, n2)` | Two-proportion test |
| `FTest` | `FTest(data1, data2)` | F-test for variances |
| `ChiSqIndep` | `ChiSqIndep(table)` | Chi-square independence |

### Test Results

```
result := TTest(data, 100)
Get(result, "statistic")     # Test statistic
Get(result, "pvalue")        # P-value
Get(result, "df")            # Degrees of freedom
Get(result, "ci")            # Confidence interval
Get(result, "conclusion")    # "Reject H0" or "Fail to reject H0"
```

### Confidence Intervals

| Function | Signature | Description |
|----------|-----------|-------------|
| `ConfInt` | `ConfInt(data, level?)` | CI for mean |
| `PropCI` | `PropCI(x, n, level?)` | CI for proportion |
| `VarCI` | `VarCI(data, level?)` | CI for variance |

---

## Category 4: Regression

### Linear Regression

| Function | Signature | Description |
|----------|-----------|-------------|
| `LinReg` | `LinReg(x, y)` | Simple linear regression |
| `MultiReg` | `MultiReg(X, y)` | Multiple linear regression |
| `Predict` | `Predict(model, x)` | Predict from model |
| `Residuals` | `Residuals(model)` | Get residuals |
| `RSquared` | `RSquared(model)` | Coefficient of determination |

### Regression Results

```
model := LinReg(x, y)
Get(model, "slope")          # β₁
Get(model, "intercept")      # β₀
Get(model, "r")              # Correlation coefficient
Get(model, "r2")             # R²
Get(model, "se")             # Standard error
Get(model, "residuals")      # Residual values
```

### Correlation

| Function | Signature | Description |
|----------|-----------|-------------|
| `Cor` | `Cor(x, y)` | Pearson correlation |
| `Cov` | `Cov(x, y)` | Covariance |
| `SpearmanCor` | `SpearmanCor(x, y)` | Spearman rank correlation |
| `KendallTau` | `KendallTau(x, y)` | Kendall's tau |
| `CorMatrix` | `CorMatrix(data)` | Correlation matrix |

### Polynomial & Other Fits

| Function | Signature | Description |
|----------|-----------|-------------|
| `PolyFit` | `PolyFit(x, y, degree)` | Polynomial regression |
| `ExpFit` | `ExpFit(x, y)` | Exponential fit y = ae^(bx) |
| `PowerFit` | `PowerFit(x, y)` | Power fit y = ax^b |
| `LogFit` | `LogFit(x, y)` | Logarithmic fit y = a + b·ln(x) |

---

## Category 5: Sampling & Simulation

### Random Sampling

| Function | Signature | Description |
|----------|-----------|-------------|
| `Sample` | `Sample(data, n, replace?)` | Random sample from data |
| `Shuffle` | `Shuffle(data)` | Random permutation |
| `Bootstrap` | `Bootstrap(data, stat, n)` | Bootstrap resampling |

### Random Number Generation

| Function | Signature | Description |
|----------|-----------|-------------|
| `RandUniform` | `RandUniform(a, b)` | Uniform random in [a, b] |
| `RandInt` | `RandInt(a, b)` | Random integer in [a, b] |
| `RandNormal` | `RandNormal(mu?, sigma?)` | Normal random |
| `RandExp` | `RandExp(lambda)` | Exponential random |
| `SetSeed` | `SetSeed(seed)` | Set RNG seed |

### Simulation

| Function | Signature | Description |
|----------|-----------|-------------|
| `Simulate` | `Simulate(expr, n)` | Simulate expression n times |
| `MonteCarlo` | `MonteCarlo(f, n, bounds)` | Monte Carlo integration |

---

## Category 6: Combinatorics & Probability

### Counting

| Function | Signature | Description |
|----------|-----------|-------------|
| `Factorial` | `Factorial(n)` | n! |
| `Permute` | `Permute(n, r)` | P(n,r) |
| `Choose` | `Choose(n, r)` | C(n,r) = binomial coefficient |
| `Multinomial` | `Multinomial(n, k1, k2, ...)` | Multinomial coefficient |

### Probability Helpers

| Function | Signature | Description |
|----------|-----------|-------------|
| `Prob` | `Prob(event, space)` | P(event) given sample space |
| `Odds` | `Odds(p)` | Convert probability to odds |
| `OddsToProb` | `OddsToProb(odds)` | Convert odds to probability |
| `BayesUpdate` | `BayesUpdate(prior, likelihood, evidence)` | Bayesian update |

---

## Category 7: Statistical Graphics

These functions generate graphics-core objects for visualization.

### Univariate Plots

| Function | Signature | Description |
|----------|-----------|-------------|
| `Histogram` | `Histogram(data, bins?)` | Histogram |
| `BoxPlot` | `BoxPlot(data, opts?)` | Box-and-whisker plot |
| `DotPlot` | `DotPlot(data)` | Dot plot |
| `StemLeaf` | `StemLeaf(data)` | Stem-and-leaf (text) |
| `DensityPlot` | `DensityPlot(data, opts?)` | Kernel density estimate |

### Bivariate Plots

| Function | Signature | Description |
|----------|-----------|-------------|
| `ScatterPlot` | `ScatterPlot(x, y, opts?)` | Scatter plot |
| `LinePlot` | `LinePlot(x, y)` | Connected line plot |
| `RegPlot` | `RegPlot(x, y)` | Scatter with regression line |
| `ResidualPlot` | `ResidualPlot(model)` | Residual plot |

### Distribution Plots

| Function | Signature | Description |
|----------|-----------|-------------|
| `PlotPDF` | `PlotPDF(dist, opts?)` | Plot probability density |
| `PlotCDF` | `PlotCDF(dist, opts?)` | Plot cumulative distribution |
| `PlotPMF` | `PlotPMF(dist, opts?)` | Plot probability mass function |
| `QQPlot` | `QQPlot(data, dist?)` | Q-Q plot |
| `PPPlot` | `PPPlot(data, dist?)` | P-P plot |

### Categorical Plots

| Function | Signature | Description |
|----------|-----------|-------------|
| `BarChart` | `BarChart(categories, values)` | Bar chart |
| `PieChart` | `PieChart(categories, values)` | Pie chart |
| `ParetoDiagram` | `ParetoDiagram(data)` | Pareto chart |

### Graphics Options

```
Histogram(data, {
  bins: 10,               # Number of bins
  binWidth: auto,         # Or specify width
  density: 0,             # Normalize to density
  cumulative: 0,          # Cumulative histogram
  color: "blue",
  fillOpacity: 0.7
})

BoxPlot(data, {
  horizontal: 0,          # Horizontal orientation
  showOutliers: 1,        # Mark outliers
  showMean: 0,            # Show mean marker
  notched: 0              # Notched box plot
})
```

---

## Implementation Priority

### Phase 1: Descriptive Statistics
- [ ] Mean, Median, Mode
- [ ] Variance, StdDev (with oracle)
- [ ] Quantiles, FiveNum
- [ ] Summary function

### Phase 2: Basic Distributions
- [ ] Normal (with oracle for CDF)
- [ ] Binomial (exact rational)
- [ ] Uniform, Exponential
- [ ] Distribution object pattern

### Phase 3: Statistical Graphics
- [ ] Histogram
- [ ] BoxPlot
- [ ] ScatterPlot
- [ ] PlotPDF, PlotCDF

### Phase 4: Regression
- [ ] Simple linear regression
- [ ] Correlation
- [ ] R², residuals

### Phase 5: Hypothesis Testing
- [ ] Z-test, T-test
- [ ] Confidence intervals
- [ ] Chi-square tests

### Phase 6: More Distributions
- [ ] Student's t, Chi-square, F
- [ ] Gamma, Beta
- [ ] Discrete: Poisson, Geometric

### Phase 7: Advanced
- [ ] Multiple regression
- [ ] Bootstrap
- [ ] Monte Carlo

---

## Dependencies

- `@ratmath/core`: Rational arithmetic
- `@ratmath/oracles`: Oracle interface for irrational CDFs
- `@ratmath/arith-funs`: Factorial, combinatorics
- `@ratmath/graphics-core`: Graphics primitives

---

## Open Questions

1. **Oracle precision**: How precise for normal CDF?
   - Proposed: User-configurable, default to 10^-10

2. **Large data**: Streaming/incremental algorithms?
   - Proposed: Standard in-memory first; streaming later

3. **Random seeds**: Reproducible randomness?
   - Proposed: SetSeed function with LCG or xorshift

4. **Missing data**: NA/null handling?
   - Proposed: Functions accept `na.rm` option

5. **Exact vs approximate**: When to use exact vs oracle?
   - Proposed: Exact for rational results; oracle for transcendentals
