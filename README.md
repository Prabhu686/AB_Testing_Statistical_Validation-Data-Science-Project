Statistical Validation of A/B Testing Experiments for E-Commerce User Interface Optimization

Open In Colab Show Image Show Image Show Image

Author: PRABHU D, Department of Computer Science and Engineering, Sri Eshwar College of Engineering, Coimbatore Domain: E-Commerce & Supply Chain | Level: K4 (Analyze) | COs: CO2, CO5 | Tech stack: Python (SciPy Stats module)

Overview

E-commerce companies redesign their user interfaces to increase purchases, but a launch decision is trustworthy only if the A/B test behind it is valid and analysed with the right statistical procedures. This project builds a reproducible framework that validates an A/B test from design to decision using the SciPy Stats module.

Workflow

What the project does
Stage	Methods (SciPy Stats)
Experiment design	Hypotheses, MDE, sample size and power analysis (stats.norm)
Validity checks	Sample ratio mismatch (chisquare), covariate balance (chi2_contingency), A/A test, peeking simulation
Primary metric (conversion)	Two-proportion z-test, chi-square, Fisher's exact (fisher_exact), permutation test, confidence interval, Cohen's h
Secondary / guardrail metrics	shapiro, normaltest, levene, Welch ttest_ind, mannwhitneyu, bootstrap, Cohen's d
Multiple testing	Bonferroni, Holm, Benjamini-Hochberg
Segment analysis	Device-level tests, Cochran's Q heterogeneity test
Bayesian and stability	Beta-Binomial posterior (stats.beta), novelty-effect trend test (linregress)
Decision	Rule-based Launch / No launch / Inconclusive report
Key results (simulated 14-day experiment, 20,000 users)
Check / metric	Result
Sample ratio mismatch	p = 1.00 (pass)
A/A false-positive rate	4.7% (nominal 5%)
Stop at first significant of 10 looks	19.1% false positives (peeking inflates error)
Conversion rate	10.47% to 12.47% (+2.00 pp, 95% CI +1.12 pp to +2.88 pp, p = 9.08 × 10⁻⁶)
Session duration	150.3s to 164.1s (Welch p = 3.72 × 10⁻¹⁸)
Revenue per user	6.77 to 8.17 (Welch p = 8.96 × 10⁻⁵)
Bounce rate (guardrail)	41.41% to 37.74% (p = 1.12 × 10⁻⁷)
After Holm correction	All four metrics remain significant
Segment effect	Strongest on mobile (Cochran's Q p = 0.010)
Bayesian P(treatment > control)	99.999%
Decision	LAUNCH the new interface

Conversion CI Peeking

Note: the dataset is synthetic (generated with a fixed seed) so that the true effect is known and every method can be checked. The notebook contains an optional cell to load a real A/B testing CSV (columns: user_id, group, converted, ...).

Repository structure
ab-testing-statistical-validation/
|-- AB_Testing_Statistical_Validation.ipynb   # main Google Colab notebook
|-- README.md
|-- requirements.txt
|-- LICENSE
|-- .gitignore
|-- images/                                   # diagrams and result figures
|-- docs/
|   |-- AB_Testing_Project_Report_PRABHU_D.docx
|   `-- AB_Testing_Research_Paper_PRABHU_D.docx
How to run

Option 1: Google Colab (recommended)

Click the Open in Colab badge above (or upload the .ipynb at colab.research.google.com).
Choose Runtime > Run all. It takes about one minute; no installation is needed.

Option 2: locally

bash
git clone https://github.com/Prabhu686/AB_Testing_Statistical_Validation-Data-Science-Project.git
cd ab-testing-statistical-validation
pip install -r requirements.txt
jupyter notebook AB_Testing_Statistical_Validation.ipynb

SciPy 1.10 or later is required (for scipy.stats.bootstrap and confidence_interval).

Using your own data

Replace the data-generation cell with your file and keep these columns: group (control/treatment), converted (0/1), and optionally device, revenue, session_sec, bounced, date. The rest of the notebook runs unchanged for the metrics that are present.

Technologies

Python 3, SciPy Stats, NumPy, Pandas, Matplotlib, Seaborn, Google Colab.

References

Key sources: Kohavi et al. (2009, 2020), Dmitriev et al. (2017), Johari et al. (2017), Fabijan et al. (2019), Holm (1979), Benjamini and Hochberg (1995), Welch (1947), Mann and Whitney (1947); full list in the report and paper under docs/.

License

MIT License, see LICENSE.
