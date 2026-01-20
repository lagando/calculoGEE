calculoGEE: Client-Side Scope 2 GHG Emissions Calculator for the Brazilian Interconnected System
Authors:
Gabriel Costa Bahia Rocha¹
¹ Gestão Ambiental e Sustentabilidade, Universidade Federal de Alfenas (UNIFAL-MG), Poços de Caldas, MG, Brazil.
Correspondence: gabrielbahiapro@gmail.com

Summary
calculoGEE (Scope 2 Module) is an open-source web tool that calculates Greenhouse Gas (GHG) emissions from purchased electricity. It specifically targets the temporal variability of the Brazilian National Interconnected System (SIN). Unlike calculators that rely on static annual averages, calculoGEE implements a time-weighted algorithm using official monthly Average Emission Factors. The software runs entirely on the client side using Vanilla JavaScript, ensuring privacy and eliminating server costs.

Statement of Need
Accurate Scope 2 accounting in Brazil requires handling hydrological seasonality. The carbon intensity of the grid fluctuates significantly between wet and dry months. Using a single annual average factor allows for statistical errors when calculating emissions for specific short-term events or seasonal operations.
Furthermore, there is a frequent methodological confusion between:
1.	Corporate Inventories: Require the Average Emission Factor (emissions of all plants) [@MCTI_Fatores].
2.	Clean Development Mechanism (CDM): Requires the Operating Margin Factor (emissions of plants at the margin) [@UNFCCC_Tool].
General-purpose calculators often fail to distinguish these methods or lack the database granularity to apply monthly factors. calculoGEE enforces the MCTI methodology for inventories, ensuring compliance with national reporting standards. It utilizes a decoupled JSON database (fatores.json) to accommodate frequent updates from the National System Operator (ONS), such as the grid expansion data integrated in 2025.




Algorithm
The software replaces static multiplication with a time-weighted loop. For any given date range, the algorithm iterates through the active days of each month to apply the specific emission factor ($EF$) for that period.
The weighted factor ($EF_{weighted}$) is defined as:
$$EF_{weighted} = \frac{\sum_{i=1}^{n} (d_i \times EF_i)}{\sum_{i=1}^{n} d_i}$$

Where:
•	$n$: distinct months in the interval.
•	$d_i$: active days in month $i$.
•	$EF_i$: Official Average Emission Factor ($tCO_2e/MWh$) for month $i$ sourced from SIRENE/MCTI.
Total Emissions ($E_{total}$) are calculated from consumption ($C_{kWh}$):
$$E_{total} = \left( \frac{C_{kWh}}{1000} \right) \times EF_{weighted}$$
Software Architecture
The implementation focuses on reproducibility and ease of maintenance:
•	Decoupled Data: Emission factors are isolated in an external JSON file. This allows non-developers to audit or update the dataset without modifying the application logic.
•	Privacy-First: The tool uses the Fetch API to retrieve parameters, but all calculations execute locally in the user's browser. No user input data is transmitted to external servers.
•	Contextual Output: To aid data interpretation, the system converts mass values ($tCO_2e$) into equivalencies (e.g., trees planted, km driven) based on EPA factors.
Figure 1 details the data flow and the time-weighted logic.
![Insert Figure 1 Here]
Figure 1. Algorithm flowchart demonstrating the logic implemented in the script tag. The diagram details the interaction between the English logic flow and the specific Portuguese variables used in the source code (e.g., 'somaPonderada', 'fatoresEmissao'). The process highlights the Time-Weighted Algorithm (yellow block) responsible for handling the variability of the Brazilian energy grid factors stored in fatores.json. Source: Author.
Usage and Validation
To demonstrate the precision of the time-weighted algorithm, consider a scenario where an organization needs to report emissions for a billing period spanning two months with distinct hydrological characteristics (e.g., a transition from a wet to a dry season).
Scenario:
•	Period: April 15, 2024 to May 15, 2024 (31 days).
•	Consumption: 1,000 kWh.
•	Data Source: The tool automatically retrieves factors for April ($EF_{Apr}$) and May ($EF_{May}$) from the JSON database.
Instead of applying a generic annual average, the tool calculates:
$$EF_{weighted} = \frac{(16 \text{ days} \times EF_{Apr}) + (15 \text{ days} \times EF_{May})}{31 \text{ days}}$$
This granular approach ensures that the final report reflects the exact carbon intensity of the grid during the consumption period. Figure 2 shows the user interface displaying the calculation breakdown and contextual equivalencies.
![Insert Figure 2 Here]
Figure 2. Screenshot of the calculoGEE interface (Scope 2 module). The interface displays the input fields for dates and energy consumption, followed by the calculated results and a "Factor Breakdown" section that details the specific days and emission factors used for the weighted average calculation. Source: Author.
Availability
•	Repository: https://github.com/lagando/calculoGEE
•	Live Tool: https://lagando.github.io/calculoGEE/escopo2.html
•	License: MIT License
References
1.	MCTI. (2025). Fatores de Emissão de CO2 pela geração de energia elétrica no Sistema Interligado Nacional do Brasil: Fator médio - Inventários corporativos. Ministério da Ciência, Tecnologia e Inovações. Available at: https://www.gov.br/mcti/pt-br/acompanhe-o-mcti/sirene/dados-e-ferramentas/fatores-de-emissao.
2.	WRI & WBCSD. (2004). The Greenhouse Gas Protocol: A Corporate Accounting and Reporting Standard. World Resources Institute and World Business Council for Sustainable Development.
3.	UNFCCC. (2024). Tool to calculate the emission factor for an electricity system (Version 07.0). Clean Development Mechanism (CDM). Available at: https://cdm.unfccc.int/methodologies/PAmethodologies/tools/am-tool-07-v7.0.pdf.


 

