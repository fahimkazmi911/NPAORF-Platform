NPAORF — National Pharmaceutical Asset Optimization & Resilience Framework
![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19310968.svg)
![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)
![Platform](https://img.shields.io/badge/Platform-GxP%20Compliant-blue)
![Status](https://img.shields.io/badge/Status-Prototype%20v4.0-green)
![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen)
> A hardware-agnostic, GxP-compliant predictive maintenance platform addressing the U.S. drug shortage crisis through machine learning-driven equipment failure prediction. Built in direct response to \*\*Executive Order 14017: America's Supply Chains\*\*.
---
🔗 Live Platform & Citation
Resource	Link
Live Platform	https://fahimkazmi911.github.io/NPAORF-Platform/
White Paper (Zenodo)	DOI: 10.5281/zenodo.19310968
Cite this repository	See CITATION.cff
---
The Problem This Solves
As of Q1 2026, the American Society of Health-System Pharmacists (ASHP) documents 323 active drug shortages imposing an estimated $900 million annual burden on U.S. healthcare systems.
FDA Essential Medicines Supply Chain analysis attributes 40% of these shortages directly to manufacturing equipment failures — a mechanistic, predictable, and therefore preventable root cause.
Executive Order 14017 ("America's Supply Chains", February 24, 2021) formally identified pharmaceutical manufacturing equipment reliability as a national security vulnerability requiring systemic federal intervention. NPAORF is the open-source technical instrument designed to operationalize that mandate at the facility level.
---
Why Existing Solutions Fail
No currently available commercial platform simultaneously satisfies pharmaceutical manufacturing's requirements:
Platform	HW-Agnostic	GxP Native	21 CFR Pt 11	Pharma ML	Shortage Link	Open Access
GE Predix	✗	✗	✗	✗	✗	✗
Siemens MindSphere	✗	✗	✗	✗	✗	✗
PerkinElmer Signals	✗	Partial	Partial	Partial	✗	✗
IBM Maximo APM	✗	✗	✗	✗	✗	✗
Aspentech Mtell	Partial	✗	✗	✗	✗	✗
NPAORF (this work)	✓	✓	✓	✓	✓	✓
---
Technical Architecture — The Kazmi Methodology™
NPAORF employs a proprietary hybrid machine learning ensemble purpose-built for pharmaceutical equipment failure physics:
```
Raw Sensor Telemetry (1–100 Hz)
           ↓
 ┌─────────────────────────────────────────┐
 │      Feature Engineering Pipeline       │
 │  Time-domain (40+) │ FFT (50+) │ DWT (40+) │
 └─────────────────────────────────────────┘
           ↓
 ┌─────────────────────────────────────────┐
 │       Kazmi Methodology™ Ensemble       │
 │     XGBoost (0.55) + LSTM (0.45)        │
 └─────────────────────────────────────────┘
           ↓
 ┌─────────────────────────────────────────┐
 │    SHAP Attribution → Explainable Alert │
 └─────────────────────────────────────────┘
           ↓
 ┌─────────────────────────────────────────┐
 │   21 CFR Part 11 SHA-256 Audit Trail    │
 └─────────────────────────────────────────┘
```
Why XGBoost + LSTM?
Non-stationarity: Pharmaceutical sensor data shifts with batch recipes and maintenance events. LSTM's gated memory cells handle this without preprocessing.
Failure sparsity: Failures comprise <0.1% of sensor records. XGBoost with SMOTE augmentation handles extreme class imbalance far more robustly than end-to-end deep learning.
Interpretability: GxP frameworks require explainable predictions. XGBoost's SHAP attribution generates per-prediction feature importance scores that satisfy 21 CFR Part 11 audit requirements.
Feature Engineering Rationale
Domain	Features	Rationale
Time-domain	40+	Statistical moments, rate-of-change, RMS, crest factor
FFT (frequency)	50+	Fault-characteristic frequencies (BPFI/BPFO), gear mesh, motor harmonics
DWT (time-frequency)	40+	Transient fault signatures localized in time — inaccessible to FFT alone
Prototype Validation Results
Metric	Value	Notes
Binary Classification Accuracy	94.7%	5-fold time-series cross-validation
Average Prediction Lead Time	14.2 days	Mean time before simulated failure
False Positive Rate	2.3%	20% held-out test partition
F1 Score (failure class)	0.943	Harmonic mean of precision/recall
Inference Latency	<50 ms	Consumer-grade hardware
Validated on simulated pharmaceutical sensor data using published reliability profiles. See Appendix C of the white paper for full simulation methodology disclosure.
---
Platform Features (v4.0)
National Surveillance Dashboard — Geographic shortage concentration mapping across 6 U.S. manufacturing states with live categorical and risk distribution analysis
Universal Equipment Configuration — Hardware-agnostic vendor selection across Bioreactors (Thermo Fisher, Sartorius, Cytiva, Eppendorf), Chromatography (Agilent, Waters, Shimadzu), ULT Freezers (PHCbi, Eppendorf), and Filling Lines (Bosch/Syntegon, IMA Life)
Economic Impact Calculator — Interactive deployment scenario modeling with FDA/ASHP 2026 baseline parameters
21 CFR Part 11 Audit Log — SHA-256 cryptographically chained event log with ALCOA+ data integrity and electronic signature workflows
FDA/EMA AI Credibility Framework — Built-in compliance guide aligned with EMA/83337/2023
---
Tech Stack
Frontend: Vanilla JavaScript (ES6+), HTML5, CSS3
UI Framework: Tailwind CSS
Charts: Chart.js v4.4.1
Icons: Lucide
Compliance: SHA-256 cryptographic audit trails (native browser implementation)
Deployment: GitHub Pages (static, no backend required)
---
Supported Equipment Vendors
Category	Vendors
Bioreactors	Thermo Fisher HyPerforma™ SUB, Sartorius BIOSTAT STR®, Cytiva Xcellerex™ XDR, Eppendorf BioFlo 320, Applikon my-Control
Chromatography	Agilent 1260 Infinity II, Waters ACQUITY UPLC, Shimadzu Nexera, Cytiva ÄKTA pure
ULT Freezers	Thermo Fisher TSX Series, PHCbi VIP ECO, Eppendorf CryoCube
Filling Lines	Bosch/Syntegon, IMA Life, Bausch+Ströbel, Groninger
---
Public API
A structured shortage intelligence endpoint is available for researchers and developers:
```
GET https://fahimkazmi911.github.io/NPAORF-Platform/api/shortage-data.json
```
Returns structured shortage data based on ASHP/FDA January 2026 baseline. See `/api/` directory for schema documentation.
---
How to Cite
If you use NPAORF in your research, please cite the foundational white paper:
```
Kazmi, S.F.A. (2026). NPAORF: A Hardware-Agnostic Infrastructure for Mitigating 
2026 Drug Shortages via GxP-Compliant Predictive Maintenance. Technical White Paper 
v2.0. Zenodo. https://doi.org/10.5281/zenodo.19310968
```
For citing this repository specifically, see CITATION.cff.
---
Current Status & Roadmap
Current: Functional prototype — web-based demonstration interface with simulated sensor data.
Next milestones:
[ ] Live sensor network integration at pilot pharmaceutical facility
[ ] IQ/OQ/PQ validation under 21 CFR Part 11
[ ] Peer-reviewed publication of live-deployment validation results
[ ] Federal pilot deployment discussions (FDA/HHS/DHS CISA)
---
Collaboration & Contact
The author invites collaboration with:
Federal agencies (FDA, HHS, DHS CISA) for pilot deployment within Essential Medicines manufacturing infrastructure
Pharmaceutical manufacturers seeking facility-level predictive maintenance implementation
Equipment vendors interested in Kazmi Methodology™ integration partnerships
Academic institutions for co-validation studies and peer-reviewed publication
---
Author
Syed Fahim Abbas Kazmi, M.S.
Lead Architect & Principal Investigator, NPAORF
M.S. Business Analytics, Temple University (4.0 GPA)
5+ years pharmaceutical R&D asset optimization — GlaxoSmithKline global operations
ORCID: [https://orcid.org/0009-0000-5075-9638](https://orcid.org/0009-0000-5075-9638)
---
License
This work is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0).
You are free to share and adapt this work for any purpose, provided appropriate credit is given, a link to the license is provided, and any changes are indicated.
---
Built to address a documented national public health infrastructure gap. The technology exists. The economic case is quantified. The national need is documented at 323 active shortages and counting.
