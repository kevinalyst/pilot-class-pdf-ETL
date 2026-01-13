## Executive summary

Across all schools, **mean Q1–Q12 learning experience increased from 3.62 (Baseline) to 4.08 (AI)**, an **overall lift of +0.46 points (+12.78%)**. The equity analysis shows the **under–resourced vs resourced “experience gap” shrank from 0.79 (Baseline) to 0.45 (AI)**, a **gap reduction of 0.35 (43.67%)**.

To quantify robustness, we tested whether the **gap reduction is reliably > 0**. The result (**t = 2.36, p = 0.02; 95% CI: [0.06, 0.63]**) indicates the observed gap reduction is unlikely under a “no gap reduction” null model and is plausibly between **+0.06 and +0.63 points** on the 1–5 scale.

---

## What these metrics mean

### Experience metrics (Q1–Q12)
- **Avg Q1–Q12 (AI-User)** and **Avg Q1–Q12 (Baseline)**: the average perceived learning experience score on Q1–Q12 for the AI (intervention) and non-AI (control) groups.
- **Experience Lift**: **AI − Baseline** (absolute change in points).
- **Experience Lift (%)**: **(AI − Baseline) / Baseline** (relative change).

These answer: *“Does the AI condition improve the average learning experience?”*

### Equity metrics
- **Equity Gap (Baseline)**: **Avg(Resourced) − Avg(Under-resourced)** in the control condition.
- **Equity Gap (AI)**: the same gap under the intervention.
- **Gap Reduction**: **Gap(Baseline) − Gap(AI)** (how much the disparity shrinks).
- **Gap Reduction (%)**: **Gap Reduction / Gap(Baseline)** (how much of the baseline disparity is “closed”).

These answer: *“Does the AI condition reduce the disparity between resourced and under-resourced schools?”*

### Why Gap Reduction and Equity DiD were identical in our output
Given our definitions, **Gap Reduction (abs)** and **Equity DiD (abs)** are algebraically the same contrast of four group means, so they **should** produce the same t-stat, p-value, and CI. That’s not a bug; it’s just the same estimator written two ways.

---

## Why these metrics are the right ones for statistical testing

### Why test **Gap Reduction**
If our research claim is “mitigate inequity,” the primary target isn’t just a higher mean score—it’s a **smaller gap**. Gap Reduction directly operationalizes that claim.

### Why include both **absolute** and **percent** versions
- **Absolute** gap reduction (points) is interpretable on our 1–5 scale (“how many points of disparity were reduced?”).
- **Percent** gap reduction is a normalized story (“what fraction of the original inequity gap was closed?”).

### Why use a t-test + confidence interval (CI)
- A **p-value** tells us how incompatible our observed result is with a specified null model (e.g., “true gap reduction = 0”), *but it does not measure effect size or importance*.   
- A **95% CI** gives the plausible range of the true effect size under the model; it conveys uncertainty (precision), which is what reviewers actually want.   

### Why Welch-style inference (unequal variances / unequal n)
our group sizes and variability differ across school groups and conditions, so **Welch’s t-test** (unequal variances) is a defensible default; it is specifically designed to be more reliable when variances and sample sizes differ.   
The **Welch–Satterthwaite** approach provides an effective degrees-of-freedom approximation for these unequal-variance settings.   

---

## Conclusion

The results support two linked statements:

1) **Overall improvement:** the AI condition is associated with a **meaningful increase in Q1–Q12 learning experience** (+0.46 points; +12.78%).  
2) **Equity improvement:** the AI condition is associated with a **substantial reduction in the resourced–under-resourced experience gap** (0.79 → 0.45; −0.35, i.e., 43.67%), and the statistical test suggests the gap reduction is **reliably positive** (p = 0.02; 95% CI excludes 0).

The careful phrasing is “associated with” unless assignment to AI vs control was randomized or otherwise tightly controlled. Also: don’t oversell the p-value—ASA explicitly warns that statistical significance is not the same thing as practical importance, and p-values alone are not a good measure of evidence. 
