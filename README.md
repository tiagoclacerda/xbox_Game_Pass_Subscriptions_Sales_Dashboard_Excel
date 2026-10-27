# 🎮 Xbox Game Pass Subscriptions Sales — Dashboard em Excel

Dashboard interativo construído inteiramente no **Microsoft Excel** para analisar as vendas de assinaturas do Xbox Game Pass ao longo de 2024. O projeto transforma uma base de 295 assinaturas em respostas objetivas para perguntas de negócio, com KPIs, gráficos dinâmicos e filtros por segmentação de dados.

![Dashboard](docs/dashboard.png)

---

## 📌 Sumário

- [Objetivo](#-objetivo)
- [Dados utilizados](#-dados-utilizados)
- [Perguntas de negócio](#-perguntas-de-negócio)
- [Estrutura da planilha](#-estrutura-da-planilha)
- [Principais resultados](#-principais-resultados)
- [Como reproduzir](#-como-reproduzir)
- [Estrutura do repositório](#-estrutura-do-repositório)
- [Ferramentas](#-ferramentas)
- [Observações sobre os dados](#-observações-sobre-os-dados)
- [Autor](#-autor)

---

## 🎯 Objetivo

Construir um dashboard no próprio Excel que responda a perguntas de negócio sobre as assinaturas do Xbox Game Pass: quantos assinantes existem, quanto geram de receita, como se distribuem entre planos e periodicidades, qual a adesão à renovação automática e aos passes de temporada, quanto se concede em cupons e como as novas assinaturas evoluem mês a mês.

---

## 🗂️ Dados utilizados

A base está na aba **Bases** (tabela `tbl_dados`) e contém **295 assinaturas**, uma por linha, com início entre **01/01/2024 e 16/12/2024**. Não há valores vazios e o `Subscriber ID` é único.

| Coluna | Descrição |
|---|---|
| `Subscriber ID` | Identificador único da assinatura |
| `Name` | Nome do assinante |
| `Plan` | Plano contratado: **Core**, **Standard** ou **Ultimate** |
| `Start Date` | Data de início da assinatura |
| `Auto Renewal` | Renovação automática (Sim/Não) |
| `Subscription Price` | Preço da assinatura base |
| `Subscription Type` | Periodicidade: **Monthly**, **Quarterly** ou **Annual** |
| `EA Play Season Pass` | Adesão ao passe EA Play (Sim/Não) |
| `EA Play Season Pass Price` | Valor do passe EA Play |
| `Minecraft Season Pass` | Adesão ao passe Minecraft (Sim/Não) |
| `Minecraft Season Pass Price` | Valor do passe Minecraft |
| `Coupon Value` | Valor de desconto aplicado por cupom |
| `Total Value` | Valor total = assinatura + passes − cupom |

> O projeto utiliza **somente as colunas originais da tabela**, sem criação de colunas auxiliares. O agrupamento por mês é feito diretamente na tabela dinâmica a partir de `Start Date`.

---

## ❓ Perguntas de negócio

O dashboard foi desenhado para responder a 8 perguntas:

| # | Pergunta | Visual |
|---|---|---|
| 1 | Quantos assinantes temos, qual a receita total e o ticket médio? | 3 cartões de KPI |
| 2 | Qual a distribuição de assinantes por plano? | Gráfico de rosca |
| 3 | Qual plano gera mais receita e qual tem o maior ticket médio? | Colunas + linha (eixo secundário) |
| 4 | Como se distribuem Monthly, Quarterly e Annual dentro de cada plano? | Colunas empilhadas 100% |
| 5 | Qual o percentual de assinantes com renovação automática, por plano e por tipo? Quem renova gasta mais? | Colunas agrupadas (por plano) + tabelas de apoio em Cálculos |
| 6 | Qual a adesão ao EA Play e ao Minecraft por plano? | 2 gráficos de colunas agrupadas |
| 7 | Qual o valor total e médio de cupom por plano? | Colunas agrupadas |
| 8 | Quantas novas assinaturas entram por mês? | Gráfico de linha |

---

## 🧱 Estrutura da planilha

O arquivo `XBOX_DASHBORAD_SALES.xlsx` possui 4 abas:

| Aba | Função |
|---|---|
| **Assets** | Imagens e elementos visuais usados no layout (logo, avatar, ícones) |
| **Bases** | Tabela de dados (`tbl_dados`) com as 295 assinaturas |
| **Cálculos** | 11 tabelas dinâmicas que alimentam os KPIs e os gráficos, cada uma identificada com a pergunta que responde |
| **Dashboard** | Painel final com KPIs, gráficos dinâmicos e segmentações de dados |

### Tabelas dinâmicas (aba Cálculos)

| Tabela | Linhas | Colunas | Valores |
|---|---|---|---|
| KPIs Gerais | — | Σ Valores | Contagem de Subscriber ID, Soma e Média de Total Value |
| Assinantes por Plano | Plan | — | Contagem de Subscriber ID |
| Receita e Ticket por Plano | Plan | Σ Valores | Soma e Média de Total Value |
| Periodicidade por Plano | Plan | Subscription Type | Contagem de Subscriber ID |
| Renovação por Plano | Plan | Auto Renewal | Contagem de Subscriber ID |
| Renovação por Tipo | Subscription Type | Auto Renewal | Contagem de Subscriber ID |
| Gasto de Quem Renova | Auto Renewal | — | Média de Total Value |
| Adesão ao EA Play | Plan | EA Play Season Pass | Contagem de Subscriber ID |
| Adesão ao Minecraft | Plan | Minecraft Season Pass | Contagem de Subscriber ID |
| Cupons por Plano | Plan | Σ Valores | Soma e Média de Coupon Value |
| Novas Assinaturas por Mês | Start Date (agrupada em Meses) | — | Contagem de Subscriber ID |

### Segmentações de dados

Quatro segmentações no painel lateral do Dashboard, **conectadas às 11 tabelas dinâmicas**, de modo que qualquer filtro atualiza KPIs e gráficos ao mesmo tempo:

- **Plan**
- **Subscription Type**
- **Auto Renewal**
- **Meses (Start Date)**

Todas permitem seleção múltipla (botão de seleção múltipla ou tecla `Ctrl`).

---

## 📊 Principais resultados

Valores considerando o período completo, sem filtros aplicados.

**Visão geral**
- **295** assinantes, **7.633** de receita total e ticket médio de **25,87**.
- O total de cupons concedidos foi de **2.122**, o que equivale a cerca de **21,8%** da receita bruta (receita total + cupons).

**Planos**
- Distribuição equilibrada de assinantes: Core (101), Standard (96) e Ultimate (98).
- A receita é muito concentrada no **Ultimate**: 5.388 (cerca de 70,6% do total), contra 1.801 do Standard e 444 do Core.
- Ticket médio: Core ≈ 4,40, Standard ≈ 18,76 e Ultimate ≈ 54,98.

**Periodicidade e renovação automática**
- Monthly é o tipo mais comum (139), seguido de Quarterly (85) e Annual (71).
- A renovação automática é de cerca de 50% no geral (148 Sim, 147 Não), mas varia muito por tipo: **~84% nas assinaturas Annual**, **~71% nas Quarterly** e **~20% nas Monthly**.
- O gasto médio é praticamente igual entre quem renova (≈ 25,58) e quem não renova (≈ 26,17).

**Passes de temporada**
- **EA Play:** 98 adesões (≈ 33%), todas no plano Ultimate.
- **Minecraft:** 194 adesões (≈ 66%), distribuídas entre Standard e Ultimate.
- O plano Core não tem adesão a nenhum dos passes.

**Cupons**
- Standard (média ≈ 11,24) e Ultimate (média ≈ 10,02) concentram os descontos; no Core o uso é residual (média ≈ 0,60).

**Evolução temporal**
- Janeiro e fevereiro têm apenas 2 novas assinaturas cada; a partir de março o ritmo se estabiliza em torno de 30 a 31 por mês. Dezembro tem 16 porque a base termina em 16/12/2024.

---

## 🔁 Como reproduzir

### Pré-requisitos
- **Microsoft Excel 2016 ou superior** (necessário para segmentações de dados e gráficos dinâmicos).

### Abrindo o dashboard pronto
1. Baixe o arquivo `XBOX_DASHBORAD_SALES.xlsx` deste repositório.
2. Abra no Excel e, se solicitado, clique em **Habilitar Edição**.
3. Vá à aba **Dashboard** e use as segmentações do painel lateral para filtrar os dados.
4. Para atualizar após alterar a base: **Dados → Atualizar Tudo**.

### Construindo do zero
1. **Base:** coloque os dados na aba Bases e converta em tabela (`Ctrl + T`), nomeando-a `tbl_dados`.
2. **Tabelas dinâmicas:** na aba Cálculos, crie a primeira tabela dinâmica a partir de `tbl_dados` e crie as demais **copiando e colando** essa tabela, para que todas compartilhem o mesmo cache de dados. Configure Linhas, Colunas e Valores conforme a [tabela de tabelas dinâmicas](#tabelas-dinâmicas-aba-cálculos).
3. **Contagem de assinantes:** nos Valores, use **Contagem** de `Subscriber ID` (e não Soma).
4. **Agrupamento por mês:** na tabela de novas assinaturas, clique com o botão direito em uma data de `Start Date` → **Agrupar** → **Meses**.
5. **Gráficos dinâmicos:** selecione cada tabela dinâmica e use **Analisar Tabela Dinâmica → Gráfico Dinâmico**, escolhendo o tipo indicado na seção de perguntas. Mova-os para a aba Dashboard.
6. **Segmentações:** em **Analisar Tabela Dinâmica → Inserir Segmentação de Dados**, crie as 4 segmentações. Em cada uma, clique com o botão direito → **Relatar Conexões** e marque todas as tabelas dinâmicas.
7. **Cartões de KPI:** insira formas (retângulos arredondados), selecione a forma, clique na barra de fórmulas e digite `=` seguido da célula do KPI (por exemplo, `=Cálculos!C4`).
8. **Acabamento:** aplique o estilo de segmentação verde, oculte os botões de campo dos gráficos, padronize as cores por categoria e adicione cabeçalho, logo e painel lateral.

---

## 📁 Estrutura do repositório

```
.
├── README.md
├── XBOX_DASHBORAD_SALES.xlsx    # Planilha com base, cálculos e dashboard
└── docs/
    └── dashboard.png            # Captura de tela do dashboard
```

---

## 🛠️ Ferramentas

- Microsoft Excel (Tabelas, Tabelas Dinâmicas, Gráficos Dinâmicos, Segmentações de Dados, Formas vinculadas a células)

---

## ⚠️ Observações sobre os dados

- **Nomes repetidos:** existem 280 nomes únicos para 295 `Subscriber ID`. Algumas pessoas aparecem mais de uma vez, às vezes em planos diferentes; por isso, as contagens usam o `Subscriber ID` (assinaturas), e não o nome.
- **Sem churn:** a base não possui data de cancelamento nem status da assinatura, então o projeto não mede cancelamento. A renovação automática é o único indicador de retenção disponível.
- **Último mês parcial:** a base termina em 16/12/2024, portanto dezembro representa apenas parte do mês.
- **Moeda:** a base não informa a moeda. Os valores monetários aparecem formatados como R$ no dashboard.
- **Passes por plano:** o EA Play só aparece no plano Ultimate e o Minecraft só no Standard e no Ultimate, o que sugere uma regra de negócio na origem dos dados.

---

## 👤 Autor

**[Seu nome]**
[LinkedIn](https://www.linkedin.com/in/tiago-campos-lacerda/)) · [GitHub](https://github.com/tiagoclacerda)
