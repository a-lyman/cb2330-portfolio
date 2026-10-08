# data/

## dose_response.csv

**Where the numbers came from**

Sago, C. D. et al. (2018). High-throughput in vivo screen of functional mRNA delivery identifies nanoparticles for endothelial cell gene editing. *PNAS* 115(42): E9944–E9952.
https://doi.org/10.1073/pnas.1811276115

Figure 1G. Cre mRNA was delivered to Cre-reporter mice with L2K (Lipofectamine 2000) at
three doses, and the percentage of cells that had switched to RFP+ was read out by flow
cytometry. This panel is the dose-response control for the reporter system: it shows the
readout responds to dose and saturates above 80% RFP+.

The paper does not publish these three numbers as a table, so they are **visual estimates
of the bar heights** read off the published figure. They are therefore approximate; an
error of a few percentage points per bar is plausible, and this is the error the notebook
propagates in the uncertainty section (±0.03 in fraction units).

**Shape**

3 rows, 2 columns, comma-separated, one header row.

| column        | type  | units            | meaning                                           |
|---------------|-------|------------------|---------------------------------------------------|
| `dose_ng`     | int   | ng of Cre mRNA   | dose administered                                 |
| `pct_rfp_pos` | float | percent of cells | cells scored RFP+ at that dose                     |

Values: (10, 4), (100, 14), (1000, 87).

The notebook converts `pct_rfp_pos` to a fraction on [0, 1] before fitting.

**What is not here**

No replicate-level values, no cell counts, and no error bars were recoverable from the
figure at the resolution available. This is why the notebook scores candidate parameters
with sum of squared error rather than a binomial negative log-likelihood — a likelihood
would need the number of cells behind each percentage.
