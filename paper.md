---
title: 'calculoGEE: Client-Side Scope 2 GHG Emissions Calculator for the Brazilian Interconnected System'
tags:
  - javascript
  - ghg protocol
  - carbon accounting
  - sustainability
  - brazil
  - scope 2
authors:
  - name: Gabriel Costa Bahia Rocha
    orcid: 0009-0004-4451-203X
    affiliation: 1
affiliations:
 - name: Gestão Ambiental e Sustentabilidade, Universidade Federal de Alfenas (UNIFAL-MG), Brazil
   index: 1
date: 20 January 2026
bibliography: paper.bib
---

# Summary

`calculoGEE` (Scope 2 Module) is an open-source web tool designed to calculate Greenhouse Gas (GHG) emissions from purchased electricity. It specifically targets the temporal variability of the Brazilian National Interconnected System (SIN). Unlike standard calculators that often rely on static annual averages, `calculoGEE` implements a time-weighted algorithm using official monthly **Average Emission Factors**. The software operates entirely on the client side using Vanilla JavaScript, ensuring user data privacy, eliminating server costs, and facilitating adoption in educational and low-resource environments.

# Statement of Need

Accurate Scope 2 accounting in Brazil requires handling significant hydrological seasonality. The carbon intensity of the energy grid fluctuates drastically between wet and dry months due to the dispatch of thermal power plants. Consequently, using a single annual average factor introduces statistical errors when calculating emissions for specific short-term events (e.g., festivals, seasonal industrial operations) or reporting periods that do not align with the calendar year.

Furthermore, there is a frequent methodological confusion in the field between:

1. **Corporate Inventories:** These require the **Average Emission Factor**, which considers the emissions of all generating plants in the system [@MCTI_Fatores].
2. **Clean Development Mechanism (CDM):** These projects require the **Operating Margin Factor**, which focuses only on plants operating at the margin to estimate avoided emissions [@UNFCCC_Tool].

General-purpose calculators often fail to distinguish these methods clearly or lack the database granularity to apply monthly factors correctly over arbitrary time ranges. `calculoGEE` enforces the MCTI methodology for corporate inventories, ensuring compliance with national reporting standards. It utilizes a decoupled JSON database (`fatores.json`) to accommodate frequent updates from the National System Operator (ONS), such as the grid expansion data integrated in January 2025.

# Algorithm

The software replaces static multiplication with a time-weighted loop. For any given user-defined date range, the algorithm iterates through the active days of each month involved to apply the specific emission factor ($EF$) for that period.

The weighted emission factor ($EF_{weighted}$) is defined as:

$$EF_{weighted} = \frac{\sum_{i=1}^{n} (d_i \times EF_i)}{\sum_{i=1}^{n} d_i}$$

Where:
* $n$: the number of distinct months in the interval.
* $d_i$: the number of active days within month $i$.
* $EF_i$: the official Average Emission Factor ($tCO_2e/MWh$) for month $i$, sourced from SIRENE/MCTI.

Finally, the Total Emissions ($E_{total}$) are calculated based on the user's energy consumption ($C_{kWh}$):

$$E_{total} = \left( \frac{C_{kWh}}{1000} \right) \times EF_{weighted}$$

# Software Architecture

The implementation focuses on scientific reproducibility, accessibility, and ease of maintenance:

* **Decoupled Data:** Emission factors are isolated in an external JSON file. This allows non-developers to audit the data sources or update the dataset (e.g., adapting the tool for other national grids like the US eGRID or European EEA data) without modifying the application logic.
* **Privacy-First:** The tool uses the Fetch API to retrieve parameters, but all mathematical processing executes locally in the user's browser. No consumption data is transmitted to external servers.
* **Contextual Output:** To aid data interpretation and science communication, the system converts abstract mass values ($tCO_2e$) into tangible equivalencies (e.g., "number of trees planted", "km driven") based on standard factors [@WRI_GHG].

Figure 1 details the data flow and the time-weighted logic implemented in the source code.

![Algorithm flowchart demonstrating the logic implemented in the script tag. The diagram details the interaction between the English logic flow and the specific Portuguese variables used in the source code. The process highlights the Time-Weighted Algorithm (yellow block) responsible for handling the variability of the Brazilian energy grid factors stored in `fatores.json`.](path/to/your/figure1.png)

# Usage and Validation

To demonstrate the precision of the time-weighted algorithm, consider a scenario where an organization needs to report emissions for a billing period spanning two months with distinct hydrological characteristics (e.g., a transition from a wet to a dry season).

**Scenario:**
* **Period:** April 15, 2024 to May 15, 2024 (Total: 31 days).
* **Consumption:** 1,000 kWh.
* **Data Source:** The tool automatically retrieves the specific factors for April ($EF_{Apr}$) and May ($EF_{May}$) from the JSON database.

Instead of applying a generic annual average, the tool performs the following calculation:

$$EF_{weighted} = \frac{(16 \text{ days} \times EF_{Apr}) + (15 \text{ days} \times EF_{May})}{31 \text{ days}}$$

This granular approach ensures that the final report reflects the exact carbon intensity of the grid during the consumption period. Figure 2 shows the user interface displaying the calculation breakdown and contextual equivalencies.

![Screenshot of the `calculoGEE` interface (Scope 2 module). The interface displays the input fields for dates and energy consumption, followed by the calculated results and a "Factor Breakdown" section that details the specific days and emission factors used for the weighted average calculation.](path/to/your/figure2.png)

# Availability

* **Repository:** https://github.com/lagando/calculoGEE
* **Live Tool:** https://lagando.github.io/calculoGEE/escopo2.html
* **License:** MIT License

# References
