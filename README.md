# Pingpang
Use code and stats analysis to tell you how to improve your skill and learn from those talented players!
# The Physics of Choice — Table Tennis Project

> *Deconstructing elite table tennis through physics, statistics, and experimental validation.*

---

## 📌 Overview

Every second on a table tennis court is a collision of physics and human decision-making. This project investigates **why certain techniques dominate professional play** — not through intuition, but through **empirical measurement**.

The research follows a complete scientific cycle:

1. **Physical modeling** — deriving the mechanics behind each technique
2. **Statistical analysis** — extracting usage patterns from match data
3. **Experimental validation** — testing equipment performance under controlled conditions
4. **Predictive modeling** — forecasting real match outcomes

---

## 🔬 Research Questions

| Domain | Question |
|--------|----------|
| **Physics** | What physical principles govern each technique? (Magnus Effect, impulse-momentum theorem, angular momentum conservation) |
| **Statistics** | Which techniques do TOP10 players rely on most? What is their scoring efficiency? |
| **Experiment** | How does racket rubber friction affect spin generation and ball speed? |
| **Synthesis** | Can we build a predictive model that forecasts point outcomes based on physical parameters? |

---

## 🧪 Methodological Framework

### a. Technique Inventory & Player Mapping

Identified 10 signature techniques from 10 elite players (5 male, 5 female), ensuring coverage across playing styles, grip types, and eras:

| Player | Signature Technique | Core Physics |
|--------|---------------------|--------------|
| Ma Long | Forehand Loop | Magnus Effect |
| Fan Zhendong | Backhand Flick (Banana) | Angular Momentum / Collision |
| Tomokazu Harimoto | Sidespin Serve | Magnus Effect (Horizontal) |
| Sun Yingsha | Forehand Power Loop | Magnus Effect + Kinetic Chain |
| Ito Mima | Backhand Drive (Pimpled Rubber) | Low Friction / Rebound |
| Timo Boll | Backhand Loop / Fast Counter | Impulse-Momentum |
| Xu Xin | Far-from-table Forehand Counter | Magnus Effect (Extended Flight) |
| Wang Chuqin | Forehand Drive + Fast Transition | Impulse-Momentum / Footwork Kinematics|
| Lin Yun-Ju | Forehand Drive (Speed) | Impulse-Momentum |
| Wang Manyu | Backhand Loop (Power) | Angular Momentum |

### b. Physical Principle Analysis

Each technique is analyzed through a **four-layer framework**:

| Layer | Description | Example (Forehand Loop) |
|-------|-------------|--------------------------|
| **Physical Law** | What fundamental principle applies? | Magnus Effect + Bernoulli's Principle |
| **Mathematical Model** | What equation describes it? | $F = 2\rho A v \omega r^3$ |
| **Tactical Translation** | Why does this help score points? | Downward force bends trajectory → opponent misjudges landing point |
| **Conditional Effectiveness** | When is it most effective? | Mid-to-far distance (longer flight time → stronger Magnus effect) |

> *Full derivations and force diagrams are documented in each technique's “physical profile.”*

---

### c. Statistical Analysis (Python)

A custom Python pipeline processes match data to quantify:

#### Data Collected (per match)

| Field | Description |
|-------|-------------|
| `player` | Player being analyzed |
| `technique` | Last shot technique used to win the point |
| `result` | 1 = player won the point / 0 = player lost |
| `rally_length` | Number of shots exchanged |
| `position` | Playing zone: short-table / mid-distance / far-distance |
| `pressure` | Whether the point was a crucial point (deuce / game point / match point) |
| `point_type` | Winner / Forced Error / Unforced Error / Serve Winner |

#### Analysis Outputs

| Analysis | Visualization | Physical Interpretation |
|----------|---------------|-------------------------|
| **Technique usage rate** | Bar chart | Which techniques dominate the TOP10's game? |
| **Technique scoring efficiency** | Bar chart | Which techniques convert most effectively? |
| **Usage vs. Win Rate** | Scatter plot (4-quadrant) | Identify “core weapons” (high usage + high win rate) vs. “efficiency black holes” (high usage + low win rate) |
| **Crucial vs. Normal points** | Side-by-side bar chart | Do players switch to higher-reliability techniques under pressure? |
| **Position-based performance** | Heatmap / Stacked bar chart | How does playing zone affect technique effectiveness? |

### d. Equipment Experiment: Racket Rubber Performance

A controlled experiment comparing different rubber types (tacky vs. tensor vs. standard) across two physical dimensions:

#### Experiment 1: Friction Coefficient

**Methodology**:
- Place ball on rubber surface
- Gradually incline surface until ball begins sliding
- Record critical angle $\theta$
- Calculate static friction coefficient: $\mu_s = \tan\theta$

#### Experiment 2: Rebound Elasticity

**Methodology**:
- Release ball from fixed height (50cm) onto rubber
- Record rebound height from high-speed video
- Calculate coefficient of restitution: $e = h_{\text{rebound}} / h_{\text{drop}}$

#### Anticipated Findings

| Rubber Type | Friction Coefficient | Rebound Height | Implication |
|-------------|---------------------|----------------|-------------|
| Tacky (e.g., DHS Hurricane 3) | High | Moderate | Maximum spin generation → ideal for loopers |
| Tensor (e.g., Tenergy 05) | Moderate | High | Balanced speed + spin → all-round performance |
| Standard (control) | Low | High | Maximum speed → ideal for hitters / blockers |

#### Physical Interpretation

Higher friction allows greater tangential force transfer during the impact:
$F_{\text{tangential}} = \mu \cdot F_{\text{normal}}$

This translates to higher spin rates, which — through the Magnus Effect — enables **more unpredictable ball trajectories**. The data will reveal whether this theoretical advantage actually manifests in scoring efficiency.

---

### e. Validation: Real-Match Prediction

**The “make or break” component of this research.**

Using the statistical model built from training data, the model will **predict the outcome of an unseen match** (e.g., a WTT event not used in model training).

| Step | Action |
|------|--------|
| ① | Train model on annotated match data |
| ② | Select an unseen WTT match for validation |
| ③ | Predict point-by-point outcomes based on physical parameters |
| ④ | Compare predictions against actual results |
| ⑤ | Report prediction accuracy and analyze discrepancies |

> *A model that can predict real match outcomes demonstrates that the underlying physics **actually explains** what determines winning and losing — not just retrospectively, but prospectively.*

---

## 📁 Repository Structure

```
table-tennis-physics-analysis/
│
├── data/
│   ├── raw/                           # Raw match annotation data
│   │   ├── ma_long_tokyo2020_set1.csv
│   │   └── ... (expanding dataset)
│   └── processed/                     # Cleaned data for analysis
│
├── notebooks/                         # Jupyter notebooks for analysis
│   ├── 01_eda.ipynb                   # Exploratory data analysis
│   ├── 02_tech_usage_analysis.ipynb   # Usage rate & win rate
│   ├── 03_prediction_model.ipynb      # Predictive model (validation)
│   └── 04_experiment_analysis.ipynb   # Rubber experiment results
│
├── src/
│   ├── analysis.py                    # Main analysis script
│   ├── model.py                       # Prediction model pipeline
│   └── utils.py                       # Helper functions
│
├── experiments/
│   ├── rubber_friction_data.csv       # Raw experiment data
│   └── photos/                        # Experiment setup & process photos
│
├── figures/                           # All generated plots
│   ├── usage_rate.png
│   ├── win_rate.png
│   ├── usage_vs_win_rate.png
│   └── crucial_vs_normal.png
│
├── paper/                             # Research paper drafts
│   └── the_physics_of_choice.pdf
│
├── README.md
├── requirements.txt
└── LICENSE
```

---

## 🛠️ How to Run

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/table-tennis-physics-analysis.git
cd table-tennis-physics-analysis
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the main analysis

```bash
python src/analysis.py
```

### 4. Explore Jupyter notebooks (recommended for detailed exploration)

```bash
jupyter notebook notebooks/01_eda.ipynb
```

---

## 📊 Current Results (Preliminary)

*Data collection and analysis are ongoing. Preliminary results from the 2020 Tokyo Olympics Final (Set 1) suggest:*

| Finding | Implication |
|---------|-------------|
| Forehand loop accounts for 54.5% of Ma Long's points in Set 1 | The technique is his primary scoring weapon |
| Forehand loop points average 8.0 shots vs. 4.2 for other techniques | The technique is **specialized** for extended rallies, not quick finishes |
| High-friction rubbers theoretically enable higher spin rates | Experiment will verify whether this translates to higher scoring efficiency |

*Full analysis will be published as a research paper upon data collection completion.*

---

## 🔗 Related Work

This project is one of three interdisciplinary labs investigating **what it means to be an observer**:

| Lab | Focus | Status |
|-----|-------|--------|
| **Cosmos Lab** | Astrophysics — gravitational waves & Hubble constant (OSU Project) | ✅ Completed |
| **Choice Lab** | Table tennis — physics of decision-making | 🔄 In Progress |
| **Memory Lab** | History — Apollo exhibition & Tianjin colonial architecture mapping | 🔄 In Progress |

---

## 📝 License

feel free to use, adapt, and cite with proper attribution.

---

## ✍️ Author

**[Minnie]** — interdisciplinary researcher at the intersection of physics, sports science, and philosophy of science.

- Personal Website: [tengziyu0923@icloud.com]
- GitHub: [@minnie-0923]
- Research Focus: Anthropic Principle, Science Communication, History & Philosophy of Science

---

*“Every observation is an act of articulation — bringing form to the formless, clarity to the complex.”*
