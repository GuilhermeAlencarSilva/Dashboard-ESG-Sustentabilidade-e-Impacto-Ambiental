🌿 Dashboard ESG – Sustentabilidade e Impacto Ambiental  
**Power BI | DAX | ESG Analytics | What-If Simulations**

## 🧭 Visão Geral
Este projeto foi desenvolvido no **Power BI** para monitorar e simular indicadores de **Sustentabilidade (ESG)** *Environmental, Social and Governance* conectando metas ambientais e sociais com resultados financeiros.

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

Emissoes_Projetadas_CO2 =
VAR Red = SELECTEDVALUE('Pct_Red_CO2'[Pct_Red_CO2 Value]) / 100
VAR Base = [Total_CO2_t]
RETURN Base * (1 - Red)

Economia_Projetada_CO2 =
[Total_CO2_t] - [Emissoes_Projetadas_CO2]

Reducao_pct_CO2 =
DIVIDE(([Total_CO2_t] - [Emissoes_Projetadas_CO2]), [Total_CO2_t], 0) * 100

Total_Agua_m3 =
SUM(Fact_EnergyWater[Consumo_Agua_m3])

Agua_Projetada_m3 =
VAR Red = SELECTEDVALUE('Pct_Red_Agua'[Pct_Red_Agua Value]) / 100
VAR Base = [Total_Agua_m3]
RETURN Base * (1 - Red)

Economia_Projetada_Agua_m3 =
[Total_Agua_m3] - [Agua_Projetada_m3]

Reducao_pct_Agua =
DIVIDE(([Total_Agua_m3] - [Agua_Projetada_m3]), [Total_Agua_m3], 0) * 100

Total_Energia_kWh =
SUM(Fact_EnergyWater[Consumo_Energia_kWh])

Energia_Projetada_kWh =
VAR Red = SELECTEDVALUE('Pct_Red_Energia'[Pct_Red_Energia Value]) / 100
VAR Base = [Total_Energia_kWh]
RETURN Base * (1 - Red)

Economia_Projetada_Energia_kWh =
[Total_Energia_kWh] - [Energia_Projetada_kWh]

Total_Mulheres =
CALCULATE(
    COUNTROWS(Fact_DiversitySnapshot),
    Fact_DiversitySnapshot[Genero] = "Feminino"
)

Mulheres_Projetadas =
VAR Aum = SELECTEDVALUE('Pct_Aumento_Mulheres'[Pct_Aumento_Mulheres Value]) / 100
VAR Base = [Total_Mulheres]
RETURN Base * (1 + Aum)

Delta_Diversidade_pct =
DIVIDE(([Mulheres_Projetadas] - [Total_Mulheres]), [Total_Mulheres], 0) * 100

Total_Incidentes =
COUNTROWS(Fact_Incidents)

Taxa_IncidentRate =
DIVIDE([Total_Incidentes], COUNTROWS(Dim_Employee)) * 100

Promocoes_por_Cargo =
CALCULATE(
    COUNTROWS(Fact_DiversitySnapshot),
    Fact_DiversitySnapshot[Promovido] = "Sim"
)

ROI_Medio =
AVERAGE(Fact_FinancialsESG[ROI])

ROI_Ajustado =
VAR Ajuste = SELECTEDVALUE('Ajuste_ROI'[Ajuste_ROI Value]) / 100
VAR Base = [ROI_Medio]
RETURN Base * (1 + Ajuste)

Delta_ROI_pct =
DIVIDE(([ROI_Ajustado] - [ROI_Medio]), [ROI_Medio], 0) * 100

Impacto_Financeiro_ESG =
VAR lucro_atual = SUM(Fact_FinancialsESG[LucroLiquido])
VAR lucro_proj = lucro_atual * (1 + [Delta_ROI_pct] / 100)
RETURN lucro_proj - lucro_atual


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

## 👤 Autor
**Guilherme Alencar – Analista de Dados**  
LinkedIn https://www.linkedin.com/in/guilherme-alencar-327413213/| Medium https://medium.com/@GuilhermeAlencarCruz

## 🧾 Licença
Licença MIT. Livre para uso e modificação com créditos.

> “Transformar sustentabilidade em performance mensurável é o verdadeiro papel da análise de dados.” 🌎📈


