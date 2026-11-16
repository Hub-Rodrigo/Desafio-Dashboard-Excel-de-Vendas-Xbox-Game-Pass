# 🎮 Dashboard de Vendas — Xbox Game Pass

Dashboard interativo desenvolvido no **Microsoft Excel** com foco em organização de dados, modelagem analítica e visualização executiva para acompanhar o desempenho comercial de assinaturas do **Xbox Game Pass** e pacotes adicionais (*add-ons*) durante o período de 2024.

![Badge Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Badge Status](https://img.shields.io/badge/Status-Concluído-22C55E?style=for-the-badge)

## 🖼️ Preview do Dashboard

> *Nota: Após abrir o arquivo no Excel e atualizar os cálculos (`Ctrl + Alt + F9`), salve uma captura de tela do painel em `assets/dashboard_preview.png` para exibi-la aqui.*

```markdown
![Dashboard Xbox Game Pass](assets/dashboard_preview.png)
```

---

## 🎯 Objetivo do Projeto

Transformar uma base transacional bruta de **295 assinantes** em um painel visual claro, dinâmico e orientado à tomada de decisão, respondendo às perguntas de negócio do desafio:

1. **Qual é o faturamento líquido total** considerando planos base (*Core*, *Standard*, *Ultimate*), pacotes adicionais e cupons de desconto?
2. **Como a receita se comporta entre assinantes com e sem renovação automática (`Auto Renewal`)** de acordo com a periodicidade do plano (*Monthly*, *Quarterly*, *Annual*)?
3. **Qual é a receita gerada pelos pacotes complementares (*cross-sell*)** — *EA Play Season Pass* e *Minecraft Season Pass* — em cada categoria de assinatura?
4. **Qual é a evolução mensal das vendas** ao longo de 2024 e o **ticket médio** por assinatura?

---

## 🗂️ Estrutura do Repositório

```text
├── assets/
│   └── dashboard_preview.png      # Captura de tela do painel finalizado
├── data/
│   └── base.xlsx                  # Base de dados original fornecida no desafio
├── dashboard_xbox_finalizado.xlsx # Arquivo Excel completo com modelagem e dashboard
└── README.md                      # Documentação do projeto
```

---

## ⚙️ Arquitetura da Planilha (`dashboard_xbox_finalizado.xlsx`)

O arquivo foi estruturado seguindo boas práticas de Business Intelligence em planilhas, separando dados, lógica e visualização em **4 camadas**:

1. **`Dashboard` (Camada Executiva):**
   * **Filtro Interativo (`C6` — *Subscription Type*):** Lista suspensa (`Todos`, `Monthly`, `Quarterly`, `Annual`) que recalcula instantaneamente todo o painel.
   * **4 Cartões de KPIs Dinâmicos:**
     * *Total Subscriptions Xbox Game Pass* (com subtítulo dinâmico de Ticket Médio)
     * *Total Subscriptions EA Play Season Pass* (com percentual de participação na receita)
     * *Total Subscriptions Minecraft Pass* (com percentual de participação na receita)
     * *Assinantes & Taxa Auto-Renewal* (contagem ativa + percentual de renovação automática)
   * **4 Gráficos Nativos Integrados:**
     * Faturamento por Renovação Automática (`No` vs. `Yes`)
     * Composição de Receita por Plano (`Core`, `Standard`, `Ultimate`) empilhada com *Add-ons*
     * Evolução Mensal de Faturamento ao longo de 2024 (`Jan` a `Dez`)
     * Distribuição Percentual de Receita por Periodicidade Geral
2. **`Cálculos` (Camada Analítica):**
   * Tabelas auxiliares estruturadas para responder às perguntas de negócio e alimentar os cartões e gráficos sem risco de quebra de layout.
3. **`Bases` (Base Tratada):**
   * Os 295 registros formatados como **Tabela Oficial do Excel (`Tabela1`)**, com colunas calculadas via fórmulas (`MÊS`, `TEXTO` para mês/ano, `Gross Value` e `Total Value` líquido descontando cupons) e **Formatação Condicional** destacando assinaturas com renovação automática (`Yes`).
4. **`Assets` (Identidade Visual):**
   * Guia documentado da paleta de cores oficial (`#107C10`, `#22C55E`, `#9BC848`, `#5BF6A8`, `#2AE6B1` e fundo neutro `#E8E6E9`).

---

## 📊 Principais Resultados e Insights

Com base na consolidação dos 295 registros da base de dados:

| Indicador | Monthly | Quarterly | Annual | Total Geral |
| :--- | :---: | :---: | :---: | :---: |
| **Qtd. Assinantes** | 139 | 85 | 71 | **295** |
| **Faturamento Total (`Total Value`)** | R\$ 3.571,00 | R\$ 2.308,00 | R\$ 1.754,00 | **R\$ 7.633,00** |
| **Receita — Auto Renewal (`Yes`)** | R\$ 747,00 | R\$ 1.502,00 | R\$ 1.537,00 | **R\$ 3.786,00** |
| **Receita — Auto Renewal (`No`)** | R\$ 2.824,00 | R\$ 806,00 | R\$ 217,00 | **R\$ 3.847,00** |
| **Vendas EA Play Season Pass** | R\$ 1.350,00 | R\$ 990,00 | R\$ 600,00 | **R\$ 2.940,00** |
| **Vendas Minecraft Season Pass** | R\$ 1.800,00 | R\$ 1.140,00 | R\$ 940,00 | **R\$ 3.880,00** |
| **Ticket Médio** | R\$ 25,69 | R\$ 27,15 | R\$ 24,70 | **R\$ 25,87** |

### 💡 Insights Estratégicos

* **Retenção vs. Aquisição Avulsa:** Enquanto o plano *Monthly* lidera em volume de receita bruta (R\$ 3.571,00), **79%** dessa receita vem de assinantes sem renovação automática (`No`). Já nos planos *Quarterly* e *Annual*, a renovação automática (`Yes`) representa **65%** e **87,6%** da receita, respectivamente, garantindo maior previsibilidade de caixa.
* **Desempenho de Cross-Sell:** O *Minecraft Season Pass* superou o *EA Play* em faturamento total (R\$ 3.880,00 contra R\$ 2.940,00), impulsionado pela sua disponibilidade tanto no plano *Standard* quanto no *Ultimate*, enquanto o *EA Play* está restrito exclusivamente ao tier *Ultimate*.

---

## 🛠️ Fórmulas e Recursos Utilizados

* **Tabelas Estruturadas (`Tabela1`):** Referências estruturadas para expansão automática de dados e integridade das fórmulas.
* **Agregação Condicional Dinâmica:** Uso combinado de `SE` (`IF`), `SOMASES` (`SUMIFS`), `CONT.SES` (`COUNTIFS`) e `SEERRO` (`IFERROR`) para alternar dinamicamente entre a visão consolidada (`Todos`) e os filtros por periodicidade.
* **Tratamento Temporal e Financeiro:** Funções `MÊS` (`MONTH`) e `TEXTO` (`TEXT`) para agrupamento cronológico, além do cálculo líquido descontando cupons promocionais.
* **Validação de Dados e Formatação Condicional:** Menu suspenso interativo na célula `C6` do Dashboard e destaque visual automático na base para contratos recorrentes.

---

## 🚀 Como Reproduzir o Projeto

1. Faça o clone deste repositório ou baixe os arquivos diretamente:
   ```bash
   git clone https://github.com/seu-usuario/dashboard-vendas-xbox.git
   ```
2. Abra o arquivo **`dashboard_xbox_finalizado.xlsx`** no **Microsoft Excel** (versão 2016 ou superior).
3. Caso o Excel abra em *Modo de Exibição Protegido*, clique em **Habilitar Edição** e pressione **`Ctrl + Alt + F9`** para atualizar todas as fórmulas.
4. Utilize o seletor **Subscription Type** na célula `C6` (*Todos*, *Monthly*, *Quarterly*, *Annual*) para explorar os resultados dinamicamente.