# 08 — Realistic 15-Day Implementation Roadmap & Measurable Impact

**Contributor:** `Gemini_1` | **Date:** November 13, 2026

## 1. Day-by-Day 15-Day Execution Plan for 4 Team Members (Section 10 Requirement)

We divide the 4-member student team into clear, non-overlapping roles after Day 5:
* **Member 1 (Data & Geospatial Engineer):** Sentinel-1/2 STAC/GEE extraction, UPAg/ICRISAT dataset merging, SoilGrids/Open-Meteo pipeline.
* **Member 2 (AI/ML & Uncertainty Engineer):** CatBoost/XGBoost training, Conformal Quantile Regression (`P10/P50/P90`), out-of-time validation (`MAE, RMSE, R², PICP`), SHAP explainability.
* **Member 3 (Optimization & Backend Engineer):** FAO-56 water balance + Urea leaching counterfactual solver, FastAPI endpoints, SQLite/DuckDB cache, TTS voice alert generator.
* **Member 4 (Frontend & Pitch Lead):** React + Tailwind + Leaflet interactive map, Yield Fan Chart, Counterfactual "What-If" Sliders, WhatsApp card preview, slide deck polish.

| Day | Milestone Activity | Concrete Deliverable / Exit Criterion | Owner(s) |
| :---: | :--- | :--- | :--- |
| **Day 1** | Problem research & requirement finalization | Completed `01_REAL_WORLD_PROBLEM_RESEARCH.md` with verified 2025–2026 Indian statistics | All 4 Members |
| **Day 2** | Competitor analysis & 8-idea scorecard evaluation | Completed `02_COMPETITOR_AND_EXISTING_SOLUTIONS.md` & `03_INNOVATIVE_IDEAS_AND_SCORECARD.md`; team locks in **Pragnya KisanPulse** | All 4 Members |
| **Day 3** | Data-source verification & system architecture lock | Verified API responses from Open-Meteo, NASA POWER, Copernicus, and UPAg CSVs; finalized `05_TECHNICAL_ARCHITECTURE.md` | Members 1, 2, 3 |
| **Day 4** | PowerPoint deck creation & internal pitch rehearsal | Built 12-slide presentation from `09_POWERPOINT_STORYBOARD.md` for initial round submission | Member 4 + All |
| **Day 5** | Mentor/team feedback, scope freeze & repo setup | Frozen MoSCoW scope; initialized FastAPI + React monorepo and pre-cached SQLite feature store | All 4 Members |
| **Day 6** | Dataset collection, cleaning & spatio-temporal join | Clean multi-year panel joining [UPAg District APY](https://upag.gov.in/) with seasonal GDD, rainfall, SoilGrids, and Sentinel `SAVI/NDMI/NDRE/RVI` for 3 benchmark states (Telangana, AP, Punjab) | Members 1 & 2 |
| **Day 7** | Baseline & Stage-1/Stage-2 Yield Prediction Models | Trained Ridge, Random Forest, and **CatBoost MultiQuantile (`P10, P50, P90`)** models with temporal split (train $\le 2022$, val $2023$, test $2024\text{–}2025$) | Member 2 |
| **Day 8** | Conformal calibration, SHAP drivers & ablation testing | Calibrated Conformal Quantile intervals ($\ge 80\%$ empirical coverage), logged `MAE, RMSE, MAPE, R²`, and exported TreeSHAP feature importance | Member 2 |
| **Day 9** | Counterfactual Resource Optimization Engine | Coded and unit-tested the 7-day **Irrigation ($ET_c$ + `NDMI`) & Split-Urea Leaching Counterfactual Solver** with ICAR safety caps | Member 3 |
| **Day 10** | FastAPI backend integration & Two-Tier Cache | Connected `/analyze-plot` and `/simulate-counterfactual` endpoints with live Open-Meteo/Copernicus calls + instant local SQLite fallback for 15 demo farms | Members 1 & 3 |
| **Day 11** | React + Leaflet Frontend & Counterfactual Sliders | Built interactive satellite map (`SAVI/NDMI/NDRE` layers), `P10–P90` Yield Fan Chart, and live "What-If" input timing sliders | Member 4 |
| **Day 12** | End-to-end integration & Vernacular Voice Alert | Added 1-click Telugu/Hindi/English audio advisory playback and WhatsApp summary card; verified end-to-end latency $< 400\text{ ms}$ | Members 3 & 4 |
| **Day 13** | Stress testing, missing-data toggle & UI polish | Added interactive **"Simulate Missing Soil/Cloudy Satellite"** toggle for judges to see conformal intervals self-adjust | All 4 Members |
| **Day 14** | Cloud deployment & recorded backup demo video | Deployed live web app (Render/Railway/Vercel) and recorded a 2-minute 1080p backup walkthrough video in case of venue Wi-Fi failure | All 4 Members |
| **Day 15** | Final rehearsal, judge Q&A drill & submission | 5-minute timed pitch rehearsal + 10-question judge defense drill | All 4 Members |

---

## 2. Strict Scope Management (MoSCoW Prioritization)

| Priority Tier | Included / Excluded Features | Rationale for 15-Day Hackathon Window |
| :--- | :--- | :--- |
| **MUST-HAVE (Core MVP)** | 1. Interactive plot selection across **3 real Indian states** (Telangana/AP cyclone & paddy belt, Punjab groundwater belt, Maharashtra rainfed cotton/soybean belt).<br>2. Real Sentinel-2 (`SAVI, NDMI, NDRE`) + Sentinel-1 SAR (`RVI`) time-series visualization.<br>3. Calibrated **CatBoost Conformal Quantile Yield Predictor (`P10, P50, P90`)** + SHAP explanations.<br>4. **Interactive Counterfactual Simulator** comparing *Routine Input Schedule* vs. *AI-Optimized Timing* on Yield, Water Saved (L), Urea Leaching Avoided (kg), and Net Benefit (₹/acre).<br>5. Playable **Telugu, Hindi, and English Voice Advisory** + WhatsApp preview card. | Directly proves every requirement of the problem statement with high visual and technical impact. |
| **SHOULD-HAVE (Secondary)** | 1. **"Missing Data / Cloudy Sky" Stress-Test Toggle** showing how the system gracefully falls back to Sentinel-1 SAR and widens confidence bounds.<br>2. **FPO Village Triage View** ranking 20 neighboring plots by moisture/nitrogen stress priority. | Demonstrates technical maturity and scalability to judges during Q&A. |
| **COULD-HAVE (Optional)** | 1. PDF export of a plot's **Pre- vs. Post-Cyclone SAR Damage Report** for PMFBY insurance support.<br>2. Live Twilio WhatsApp sandbox webhook sending the voice note to a judge's phone. | High "wow" factor if Day 12 finishes on schedule. |
| **EXCLUDED (Out of Scope)** | 1. Physical Arduino/ESP32 soil sensor hardware.<br>2. Training 2D/3D deep CNNs on raw multi-gigabyte GeoTIFF imagery.<br>3. Native iOS/Android app store builds, user login/payment gateways, or e-commerce fertilizer store. | Wastes time on boilerplate or unverified hardware instead of the core AI prediction & optimization engine. |

---

## 3. Measurable Impact Framework & Epistemic Separation (Section 11 Requirement)

A major weakness of hackathon pitches is presenting simulated numbers as if they were verified field trials. We strictly separate our metrics into four transparent tiers:

### Tier 1: Experimentally Measured Model Performance (Measured on Held-Out 2024–2025 Data)
* **Yield Prediction Error:** `MAE` (quintals/ha), `RMSE` (quintals/ha), `MAPE (%)`, and `$R^2$` on unseen 2024–2025 district-season test splits ([UPAg dataset](https://upag.gov.in/dash-reports/desdistrictwisecompletedatasetreport)).
* **Early Prediction Lead Time:** Accuracy at **Day 81 after transplantation** using `SAVI` vs. Day 116 using standard `NDVI` (benchmarking the [IJISAE Karnataka finding](https://ijisae.org/index.php/IJISAE/article/view/2326)).
* **Uncertainty Calibration:** Empirical coverage of `[P10, P90]` conformal intervals (target: $80\% \pm 3\%$) and graceful degradation under 25%/50% masked features.
* **System Latency:** Time to generate plot prediction + 7-day counterfactual ranking ($< 350\text{ ms}$ on cached tile vectors; $< 2.5\text{ s}$ on live API fetch).

### Tier 2: Historical Weather & Agronomic Backtesting Results (2024–2026 Events)
* **Leaching Avoidance Backtest:** Replay of historical 2025–2026 monsoon/cyclone rainfall sequences (including October–November 2026 **Cyclones Arnab & Murasu** in Andhra Pradesh/Telangana per [DD News](https://ddnews.gov.in/en/cyclones-arnab-murasu-damage-crops-across-4-61-lakh-hectares-in-andhra-pradesh/)) to measure what percentage of fixed-schedule urea applications would have been flagged for a 3-to-5-day hold before $>25\text{ mm}$ rainfall events.
* **Irrigation Scheduling Backtest:** Replay of 2024–2025 Punjab/Haryana paddy-wheat seasons comparing fixed 7-day flood irrigation against `NDMI + FAO-56 ETc` triggered irrigation, benchmarked against the peer-reviewed **10.89% water demand reduction** from schedule optimization ([ResearchGate 2024](https://www.researchgate.net/publication/383677840_Water_accounting_of_groundwater_over_exploited_districts_in_Haryana_and_Punjab_states_to_analyse_impacts_of_water_conservation_measures_on_water_availability)).

### Tier 3: Simulated Counterfactual Scenarios (Clearly Labelled in UI & Slides)
* **Per-Acre Urea Savings Simulation:** Assuming a typical 2-acre paddy farmer applies 3 split doses of 45 kg urea/acre (₹266.50 per 45 kg subsidized bag, or ~₹2,000+/bag economic subsidy cost to the government) and faces one heavy-rain leaching event where 60% of surface-applied N is lost (consistent with ICAR's 30–45% NUE per [PIB 2026](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2237709)), delaying top-dressing by 4 days preserves ~25–30 kg of effective N uptake, protecting **1.5–2.2 quintals/acre of yield (~₹3,450–₹5,060/acre at ₹2,300/qtl MSP)** and eliminating a redundant booster bag.
* **Per-Acre Water & Pumping Savings Simulation:** Eliminating 2 unnecessary 50mm flood irrigations per season saves **~4,04,680 litres ($\approx 405\text{ m}^3$) of groundwater per acre**.

### Tier 4: Projected Macro Outcomes at FPO Scale (With Explicit Assumptions)
* *Explicit Disclaimer for Judges:* "Because a 15-day hackathon does not span a 120-day cropping season, our prototype demonstrates **verified historical backtesting and technical feasibility**, not live multi-month agronomic field trials. Field validation with a local KVK/FPO is our immediate post-hackathon step."
