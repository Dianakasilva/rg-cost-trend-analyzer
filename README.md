# RG Cost Trend Analyzer – Agente no Microsoft Foundry

Agente de IA criado no **Microsoft Foundry** (Azure) para ajudar a identificar se o **custo de um Resource Group** aumentou, reduziu ou se manteve estável entre dois períodos.

O agente:

- Recebe o nome de um Resource Group (real ou de teste) e os custos de dois períodos;
- Calcula:
  - Diferença absoluta em moeda;
  - Variação percentual;
- Classifica como **AUMENTO**, **REDUÇÃO** ou **ESTÁVEL**;
- Explica o resultado em português, de forma clara para **FinOps**.

> ✅ Projeto individual da disciplina, com tema livre.  
> 📅 Prazo de entrega: **23/11/2025 às 23:59**.

---

## 🎯 Objetivo do projeto

Demonstrar um agente funcional no Microsoft Foundry que:

1. Usa um **modelo de linguagem pré-treinado** (gpt-5-mini);
2. Implementa pelo menos **1 ação funcional** (cálculo da variação de custo);
3. Ajuda a responder perguntas como:

> “O custo do RG `rg-aks-prod` aumentou ou diminuiu em relação ao mês anterior? Em quanto (R$) e em qual percentual?”

4. Está documentado em um **repositório público do GitHub**, contendo:
   - README completo;
   - Roteiro detalhado (`docs/roteiro.md`);
   - Prints de tela;
   - Referências.

---

## 🧠 Visão geral do agente

- **Nome do agente:** `RG Cost Trend Analyzer`
- **Plataforma:** Microsoft Foundry (Azure)
- **Modelo:** `gpt-5-mini`  
  - Tipo de implantação: **Global Standard**  
  - Região: **Brazil South**
- **Idioma:** Português (Brasil)
- **Funcionalidade principal:**  
  Calcular a diferença de custo entre dois períodos e indicar se houve aumento ou redução.

### Exemplo 1 – Redução de custo

**Prompt:**

> Quero analisar o Resource Group `rg-aks-prod`.  
> Em outubro o custo foi de R$ 65.726,42 e em novembro foi de R$ 63.720,81.  
> Me diga se houve aumento ou redução, em quanto (R$) e em porcentagem.

**Resposta (resumo):**

- Diferença: **- R$ 2.005,61**
- Variação: **≈ -3,05%**
- Tendência: **REDUÇÃO**

*(Ver print `docs/prints/print-05-execucao-reducao.png`.)*

### Exemplo 2 – Aumento de custo

**Prompt:**

> Quero analisar o Resource Group `rg-app-prod`.  
> Em setembro o custo foi de R$ 50.000,00 e em outubro foi de R$ 65.000,00.  
> Me diga se houve aumento ou redução, em quanto (R$) e em porcentagem.

**Resposta (resumo):**

- Diferença: **+ R$ 15.000,00**
- Variação: **+30%**
- Tendência: **AUMENTO**

*(Ver print `docs/prints/print-06-execucao-aumento.png`.)*

---

## 🧮 Lógica de cálculo

A lógica foi definida diretamente nas **instruções do agente (system prompt)**:

- `diferenca_absoluta = custo_periodo_atual - custo_periodo_anterior`
- Se `custo_periodo_anterior > 0`:
  - `variacao_percentual = (diferenca_absoluta / custo_periodo_anterior) * 100`
- Classificação:
  - `AUMENTO` se `diferenca_absoluta > 0`
  - `REDUÇÃO` se `diferenca_absoluta < 0`
  - `ESTÁVEL` se `|variacao_percentual| < 1%`

O agente sempre devolve:

- Nome do RG;
- Períodos comparados;
- Custo do período anterior;
- Custo do período atual;
- Diferença absoluta;
- Variação percentual;
- Tendência (AUMENTO, REDUÇÃO ou ESTÁVEL);
- Resumo explicativo em português.

---

## 📸 Prints do agente em funcionamento

As imagens de evidência da implementação ficam em `docs/prints/`.

> ⚠️ Lembre de subir os arquivos de imagem com estes nomes na pasta `docs/prints/` para os links funcionarem.

### 1. Projeto no Microsoft Foundry

Tela de visão geral do projeto/hub do Foundry, com chave de API e endpoint:

![Visão geral do projeto no Foundry](docs/prints/print-01-projeto-foundry.png)

---

### 2. Implantação do modelo `gpt-5-mini` (Global Standard, Brazil South)

Tela de implantação do modelo `gpt-5-mini`, mostrando:

- Nome da implantação;  
- Tipo de implantação `Global Standard`;  
- Região `Brazil South`.

![Implantação do modelo gpt-5-mini](docs/prints/print-02-implantacao-gpt5mini.png)

---

### 3. Lista de agentes – RG Cost Trend Analyzer

Tela de **Agentes** no Foundry, mostrando o agente:

- Nome: `RG Cost Trend Analyzer`;  
- Modelo: `gpt-5-mini`.

![Lista de agentes com o RG Cost Trend Analyzer](docs/prints/print-03-lista-agentes.png)

---

### 4. Instruções (system prompt) com a lógica de cálculo

Tela de edição do agente, com as instruções definindo:

- Fórmulas de cálculo;  
- Regras de classificação;  
- Formato da resposta.

![System prompt com a lógica de cálculo](docs/prints/print-04-system-prompt.png)

---

### 5. Execução – Exemplo de REDUÇÃO de custo

![Execução com redução de custo](docs/prints/print-05-execucao-reducao.png)

---

### 6. Execução – Exemplo de AUMENTO de custo

![Execução com aumento de custo](docs/prints/print-06-execucao-aumento.png)


## 📁 Estrutura do repositório

```text
rg-cost-trend-analyzer/
├─ README.md
├─ docs/
│  ├─ roteiro.md
│  └─ prints/
│     ├─ print-01-projeto-foundry.png
│     ├─ print-02-implantacao-gpt5mini.png
│     ├─ print-03-lista-agentes.png
│     ├─ print-04-system-prompt.png
│     ├─ print-05-execucao-reducao.png
│     └─ print-06-execucao-aumento.png
└─ 
   



