🌿 Dashboard ESG – Sustentabilidade e Impacto Ambiental  
**Power BI | DAX | ESG Analytics | What-If Simulations**

## 🧭 Visão Geral
Este projeto foi desenvolvido no **Power BI** para monitorar e simular indicadores de **Sustentabilidade (ESG)** — *Environmental, Social and Governance* — conectando metas ambientais e sociais com resultados financeiros.

O painel adota um **tema escuro corporativo**, é totalmente interativo e utiliza **parâmetros What-If** para análise de cenários.

## 🎯 Objetivos
- Centralizar indicadores ESG em um painel executivo.  
- Simular reduções de emissões e consumo hídrico.  
- Projeções de políticas de inclusão e diversidade.  
- Ajuste dinâmico do ROI conforme desempenho ESG.  
- Automatizar relatórios de sustentabilidade corporativa.  

## 🗂 Estrutura de Dados
**Tabelas Dimensionais:**
- Dim_Date → datas, ano, mês, trimestre.  
- Dim_Site → locais de operação.  
- Dim_Sector → setor e categoria.  
- Dim_Employee → colaboradores e atributos sociais.  
- Dim_Device → sensores e fontes de energia.  
- Dim_Source → tipos de energia (renovável/não renovável).  

**Tabelas Fato:**
- Fact_Emissions → emissões de CO₂ e métricas por site.  
- Fact_EnergyWater → consumo de energia e água.  
- Fact_DiversitySnapshot → diversidade e inclusão.  
- Fact_FinancialsESG → métricas financeiras (ROI, lucro, OPEX, CAPEX).  
- Fact_Benchmarks → comparativos e índices de referência.  
- Fact_Incidents → incidentes éticos e de governança.  

## 🔗 Relacionamentos
- Fact_Emissions[Chave_Data] → Dim_Date[DateKey]  
- Fact_EnergyWater[Chave_Data] → Dim_Date[DateKey]  
- Fact_DiversitySnapshot[EmployeeID] → Dim_Employee[EmployeeID]  
- Fact_FinancialsESG[SiteID] → Dim_Site[SiteID]  
- Fact_Benchmarks[SectorID] → Dim_Sector[SectorID]  
- Fact_Incidents[EmployeeID] → Dim_Employee[EmployeeID]  

## ⚙️ Parâmetros What-If
1. Pct_Red_CO2 → 0% a 40%  
2. Pct_Red_Agua → 0% a 50%  
3. Pct_Aumento_Mulheres → 0% a 20%  
4. Ajuste_ROI → -10% a +20%  
5. (Opcional) Pct_Red_Energia → 0% a 50%

Criados em: `Modeling → New Parameter → Numeric Range`

## 🧮 Medidas DAX
Total_CO2_t =
SUM(Fact_Emissions[CO2_kg]) / 1000


## 🎨 Layout e Design
Tema escuro corporativo (#1C1C1C) com cores:
- Verde-esmeralda (#2ECC71)
- Azul petróleo (#0E4D64)
- Roxo (#8E44AD)
- Dourado (#F1C40F)

## 📊 Páginas do Dashboard
1. Visão Geral ESG  
2. Ambiental  
3. Social  
4. Governança e Financeiro  
5. Simulações ESG – What-If  

## 🔧 Passo a Passo Técnico
1. Importar bases CSV → Power BI → Get Data  
2. Tratar colunas no Power Query  
3. Criar relacionamentos  
4. Adicionar medidas DAX  
5. Criar parâmetros What-If  
6. Configurar sliders e slicers  
7. Inserir ícones e bookmarks  
8. Aplicar o tema escuro  
9. Criar visuais e KPIs  
10. Publicar no Power BI Service  

## 📁 Estrutura do Projeto
Dashboard-ESG-Sustentabilidade/  
├── data/  
├── images/  
├── Dashboard_ESG.pbix  
└── README.md  

## 💻 Requisitos
- Power BI Desktop 2024+  
- Excel 2021+  
- Tipografia Segoe UI / Calibri Light  

## 👤 Autor
**Guilherme Alencar – Analista de Dados**  
LinkedIn | Medium | GitHub

## 🧾 Licença
Licença MIT. Livre para uso e modificação com créditos.

> “Transformar sustentabilidade em performance mensurável é o verdadeiro papel da análise de dados.” 🌎📈


