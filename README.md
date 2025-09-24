# Dodgeball Analytics: Player Detection → Throw Categorization → Ball Counts → Win-Rate & Impact

[![Open in Colab](https://img.shields.io/badge/Open%20in-Colab-yellow.svg)](https://colab.research.google.com/drive/1OZbOTxo16YGmxt-V08jD19TMM3QxdOfn)

This repository contains a reproducible pipeline to:

- **Extract player coordinates** from match video using **YOLOv8** + court **homographies**
- **Categorize throws** (Phase-1 logic) and tag events with context (e.g., `opening_rush`, `set_throw`, `counter_rush`, `dump`, `bounce`, `bounce`)
- **Analyze success rates** by throw type, incl. **punish/follow-up** effects
- **Estimate ball counts** over time with anchor logic and **rollback suggestions** for QA
- **Predict win rate** and compute per-category **impact** metrics

> **Best way to run:** click the Colab badge above or open each notebook directly in Google Colab. The notebooks are written and tested for Colab + Google Drive.

All videos referenced in the examples are publicly available on the **NSWDL YouTube channel**.

---

## 📁 Repository Structure

Exactly four notebooks are included:


