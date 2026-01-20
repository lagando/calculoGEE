# calculoGEE 🌍
### Calculadora de Emissões de GEE / GHG Emissions Calculator Suite

[![Status do Site](https://github.com/lagando/calculoGEE/actions/workflows/pages/pages-build-deployment/badge.svg)](https://lagando.github.io/calculoGEE/escopo1.html)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Science](https://img.shields.io/badge/Science-Open%20Source-green)](https://github.com/lagando/calculoGEE)

[🇧🇷 Português](#-versão-em-português) | [🇺🇸 English (Scientific & Technical Context)](#-english-version)

---

<a name="-versão-em-português"></a>
## 🇧🇷 Versão em Português

Uma suíte de calculadoras de emissões de Gases de Efeito Estufa (GEE) para os Escopos 1, 2, 3 e Emissões Evitadas, desenvolvida para ser uma ferramenta prática, educativa e de alta precisão temporal para inventários de emissões.

### 🚀 Acesso às Ferramentas

Acesse as calculadoras online através dos links abaixo. O projeto é **Client-Side**, rodando 100% no seu navegador, garantindo privacidade dos dados (nenhum dado é enviado para servidores externos).

* ➡️ [**Calculadora de Escopo 1** (Emissões Diretas)](https://lagando.github.io/calculoGEE/escopo1.html)
* ➡️ [**Calculadora de Escopo 2** (Energia Elétrica)](https://lagando.github.io/calculoGEE/escopo2.html)
* ➡️ [**Calculadora de Escopo 3** (Emissões Indiretas)](https://lagando.github.io/calculoGEE/escopo3.html)
* ➡️ [**Calculadora de Emissões Evitadas** (Reciclagem)](https://lagando.github.io/calculoGEE/evitadas.html)

### 📖 Sobre o Projeto

Este projeto foi criado para simplificar o cálculo de emissões de GEE, seguindo as metodologias do **Programa Brasileiro GHG Protocol** e utilizando fatores de emissão de fontes públicas e oficiais.

O diferencial técnico desta ferramenta, especialmente no **Escopo 2**, é a **granularidade temporal**. Ao contrário de calculadoras que usam médias anuais simples, este software utiliza um algoritmo que pondera os fatores de emissão mês a mês (baseado nos dados do SIN - Sistema Interligado Nacional), oferecendo um cálculo muito mais preciso para o cenário brasileiro, onde a matriz energética varia conforme o regime de chuvas.

**Os módulos abrangem:**
* **Escopo 1:** Emissões diretas (queima de combustíveis e ar condicionado).
* **Escopo 2:** Emissões indiretas pelo consumo de energia elétrica (Rede SIN).
* **Escopo 3:** Emissões indiretas (viagens, resíduos, etc.).
* **Emissões Evitadas:** Cálculo do impacto positivo da reciclagem.

**Fontes de Dados:**
* Ministério da Ciência, Tecnologia e Inovações (MCTI).
* EPE (Empresa de Pesquisa Energética).
* Defra (UK) e EPA (USA) para referências globais cruzadas.

### 🛠️ Tecnologias Utilizadas

O projeto foi construído sobre uma arquitetura leve e acessível:
* **HTML5** (Semântico)
* **CSS3** (Responsivo)
* **JavaScript (Vanilla)** - Processamento matemático e lógica de ponderação temporal.
* **JSON** - Base de dados desacoplada para fatores de emissão.

### 👨‍💻 Autor

**Gabriel Bahia**
* **E-mail:** gabrielbahiapro@gmail.com
* **GitHub:** [@lagando](https://github.com/lagando)

---

<a name="-english-version"></a>
## 🇺🇸 English Version

### Open-Source Client-Side Approach for Dynamic GHG Calculation

This repository hosts a suite of Greenhouse Gas (GHG) emission calculators designed to address the challenge of **temporal variability** in emission factors. While currently populated with Brazilian Grid datasets (Scope 2), the software architecture is **region-agnostic** and designed for easy adaptation to any international energy grid.

### 🚀 Access the Tools

Access the online calculators via the links below. The project runs **Client-Side** directly in your browser, ensuring data privacy (no data is sent to external servers).

* ➡️ [**Scope 1 Calculator** (Direct Emissions)](https://lagando.github.io/calculoGEE/escopo1.html)
* ➡️ [**Scope 2 Calculator** (Purchased Electricity)](https://lagando.github.io/calculoGEE/escopo2.html)
* ➡️ [**Scope 3 Calculator** (Indirect Emissions)](https://lagando.github.io/calculoGEE/escopo3.html)
* ➡️ [**Avoided Emissions** (Recycling Impact)](https://lagando.github.io/calculoGEE/evitadas.html)

### 📖 About the Project & Scientific Value

This project was developed to simplify GHG emission calculations following the **GHG Protocol** methodology.

**Key Technical Differentiator (Scope 2):**
Most online carbon calculators rely on static annual averages. This tool implements a **Time-Weighted Average Algorithm** via JavaScript, allowing for precise calculations in energy grids with high variability (such as the Brazilian hydroelectric-dependent grid).

**Modules Overview:**
* **Scope 1:** Direct emissions from fuel combustion and fugitive emissions (e.g., HVAC).
* **Scope 2:** Indirect emissions from purchased electricity (Grid Average).
* **Scope 3:** Other indirect emissions (Business travel, waste disposal).
* **Avoided Emissions:** Quantification of the positive environmental impact of recycling.

**Features for Researchers:**
1.  **High Granularity:** The algorithm breaks down consumption periods into daily segments to apply the correct monthly emission factor (`tCO2e/MWh`).
2.  **Data Decoupling:** Emission factors are stored in an external `fatores.json` file, allowing researchers from other countries to adapt the tool by simply replacing the dataset.
3.  **Carbon Literacy:** Includes a "Contextual Visualization" module, converting abstract tCO2e numbers into tangible equivalents (e.g., trees planted, km driven) to improve public understanding.

### 🛠️ Tech Stack

The project relies on a lightweight, accessible, and serverless architecture:
* **HTML5** (Semantic & Accessible/WCAG friendly)
* **CSS3** (Responsive Design)
* **JavaScript (Vanilla)** - Core logic for temporal weighting algorithms.
* **JSON** - Decoupled database for emission factors.

### 👨‍💻 Author

**Gabriel Bahia**
* **Contact:** gabrielbahiapro@gmail.com
* **GitHub:** [@lagando](https://github.com/lagando)

### 🚀 How to Replicate/Adapt (For Research)

To use this engine for your country's data:
1.  Fork this repository.
2.  Update `fatores.json` with your local emission factors in the format `{"Year": {"Month": Factor}}`.
3.  The algorithm will automatically recalculate weighted averages based on your new dataset.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
