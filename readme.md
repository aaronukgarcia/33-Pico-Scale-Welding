# Pico-Scale Welding: Nanoscale Material Joining

[![Status](https://img.shields.io/badge/Status-Phase_1_Approved-green)]() [![Fragility](https://img.shields.io/badge/Fragility-78%25_High_Risk-orange)]() [![License](https://img.shields.io/badge/License-MIT-blue)]()

> **Technical Specification:** Achieving positional accuracy of ±50 nm (1σ) for the repair of Fan-Out Wafer-Level Packaging (FOWLP) redistribution layers.

---

## 📖 Overview

This repository hosts the technical specifications, simulation parameters, and control architecture for the **Pico-Scale Welding Programme**.

Our objective is to operationalize **Electrospray Nanowelding** within the "Nanoscale Thermal Regime" (1–100 nm)—a length scale where Fourier's Law breaks down due to ballistic phonon transport. This project targets the repair of sub-5 μm defects in advanced semiconductor packaging, a market segment currently unserved by traditional wire bonding.

We operate with a "worse-before-better" J-Curve cost model, targeting a long-term production density where electrical resistivity is within 3× of bulk material values.

## ⚠️ Research Status & Risk Profile

* **Current Phase:** Phase 1 (Prototyping & Characterization).
* **Fragility Assessment:** 78% (approx. 22% success probability).
* **Timeline:** 20-month development cycle.

This is a high-risk, exploratory engineering effort. We openly acknowledge substantial technical hurdles, including domain shift in AI deployment and cycle time variance due to sintering physics.

## 🏗️ Technical Scope

### 1. The Physics
We utilize the **Two-Temperature Model (TTM)** to describe electron-lattice energy exchange under ultrafast heating. The target Heat-Affected Zone (HAZ) is **500 nm**, derived from the electron diffusion length under femtosecond laser heating (~140 nm conservative bound) and superconducting coherence lengths.

### 2. Architecture Down-Selection
Following feasibility analysis, **Electrospray Nanowelding** was selected as the primary architecture. Alternative methods (Atomic Fountain Deposition and Plasma Bridge Welding) were terminated due to fundamental physics constraints.

### 3. Software & ML Stack
We maintain a strict Software Bill of Materials (SBOM) using CycloneDX format.

| Component | Version | Role |
| :--- | :--- | :--- |
| **PyTorch** | \2.1.x\ | Defect Classification (ResNet-50) |
| **ONNX Runtime** | \1.16.x\ | Inference Engine |
| **OpenCV** | \4.8.x\ | Image Normalization (TIFF/PNG handling) |

## 🤝 Invitation to Contribute

We are actively seeking contributions to address specific "Capability Gaps" identified in our feasibility analysis.

### 🧠 Challenge A: AI Explainability
The system uses a ResNet-50 backbone to classify defects as *Repairable*, *Scrap*, or *Uncertain*.
* **The Problem:** Operators require human-readable "features" to trust the model.
* **Contribution Goal:** Improve feature extraction to output semantic descriptions (e.g., "Linear discontinuity, 12 μm length", "Adjacent to via") rather than pixel heatmaps.

### ⏱️ Challenge B: Tail Latency Management
* **The Problem:** Sintering times vary significantly based on material volume. We project P99 latency events (240s) occurring approximately every 100 joints.
* **Contribution Goal:** Develop scheduler algorithms that can accommodate a 10% schedule buffer and handle "slow-sintering" events without triggering a full system abort.

### 🏭 Challenge C: MES Interface (SECS-II)
* **The Problem:** Integrating with legacy Fab Manufacturing Execution Systems (MES).
* **Contribution Goal:** We need to build a robust JSON-to-SECS-II translation layer to validate message exchange milestones in Month 12.

## 🛠️ Getting Started

**Prerequisites:**
* Python 3.10+
* Dependencies must be pinned to specific versions (not ranges) with hash verification.

\\\ash
# Clone the repository
git clone https://github.com/AaronGarcia-Lab/33-Pico-Scale-Welding.git

# Install dependencies (Strict hash verification required)
pip install -r requirements.txt --require-hashes
\\\

## 📄 Documentation
* **White Paper:** \Pico_Scale_Welding_WhitePaper.docx\ - The full technical feasibility analysis and architecture definitions.
* **Term Sheets:** Summary of vendor agreements (zeroK) and data pilot LOIs.

## 📬 Contact & Data Sovereignty
* **Author:** Aaron Garcia (Independent Researcher).
* **Data Policy:** Training data (e.g., defect images) is retained by the customer under strict sovereignty agreements and is **not** included in this public repository.
* **License:** Code is available under MIT; Model weights derived from proprietary data are subject to specific licensing.

---
*Status: APPROVED FOR PHASE 1*.
