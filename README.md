# OpenMC Core Adaptation: MHTGR-350 to a 45 MWt FCM Microreactor

**Author:** Martin Zurita  
**Objective:** A computational reactor physics study adapting the internationally validated MHTGR-350 macro-geometry to model a 45 MWt UIUC microreactor utilizing Fully Ceramic Micro-encapsulated (FCM) TRISO fuel.

## Project Overview
This repository contains a full Monte Carlo neutron transport and depletion study utilizing **OpenMC**. The project demonstrates a two-step "Hybrid Core" methodology:
1. Replicating the MHTGR-350 benchmark to validate the baseline Constructive Solid Geometry (CSG) and cross-sections.
2. Modifying the baseline to model a next-generation 45 MWt microreactor running on 9.9% enriched HALEU UCO fuel within a Silicon Carbide (SiC) matrix.

The transition from a 350 MWt macroscopic core to a 45 MWt microreactor was achieved by rigorously scaling the depletable heavy metal volume to an 85-block equivalent, preserving the validated power density of ~0.53 MWt/block.

## Repository Structure

* **`01_MHTGR_Benchmark/`** 
  * Contains the foundational OpenMC validation scripts based on the General Atomics MHTGR-350 design. Features 15.5% enriched fuel in a standard graphite matrix to establish baseline $k_{eff}$ stability.
* **`02_UIUC_Microreactor/`** 
  * Contains the modified core scripts for the 45 MWt design. Features updated material definitions for 9.9% enriched FCM pellets (2.3 cm diameter) containing 7,644 TRISO particles per pellet.
  * **`01_Cold_State.ipynb`**: Baseline criticality at 294 K.
  * **`02_Hot_State.ipynb`**: High-temperature operations simulating Doppler broadening at 1173.15 K.
  * **`03_Depletion.ipynb`**: 20-year burnup sequence utilizing the `PredictorIntegrator` operator.

## Methodology & Core Physics
* **Cross-Sections:** ENDF/B-VII.1 continuous-energy data.
* **Thermal Physics:** On-the-fly cross-section interpolation was utilized between the 900 K and 1200 K datasets to simulate the 1173.15 K (900°C) operating state.
* **Depletion Volume Scaling:** The physical FCM pellet dimensions were used to calculate the exact heavy metal mass. The depletable volume was scaled using 216 fuel channels × 31 pellets per channel × 85 physical blocks.
* **Boundary Conditions:** A 2D Radial Super-Cell model was utilized with reflective boundary conditions on the outer hexagonal prism to simulate an infinite repeating lattice.

## Core Geometry Visualization
*(The standard MHTGR hexagonal graphite block mapped with 9.9% enriched FCM UIUC cooling channels and Lumped Burnable Poisons.)*

`[Insert your Notebook 1/2 Cross-Section Image Here: e.g., ![Core Layout](images/core_cross_section.png)]`

## Preliminary Results
* **Cold-State Baseline (294 K):** The integration of heavy Boron-10 Lumped Burnable Poisons (LBPs) alongside the reduced 9.9% enrichment successfully suppressed excess reactivity, yielding a realistic, highly manageable startup $k_{eff}$ of **1.08924 ± 0.00026**.
* **Hot-State Operations (1173.15 K):** `[Insert your final Hot State k-eff here once Notebook 2 finishes]`
* **20-Year Depletion (45 MWt):** 

`[Insert your k-eff vs Time Letdown Curve Image Here]`
`[Insert your Isotopic Evolution (U-235 vs Pu-239) Image Here]`
