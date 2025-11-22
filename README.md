# RG Cost Trend Analyzer – Agente no Microsoft Foundry (Azure)

Este repositório contém o projeto **RG Cost Trend Analyzer**, um agente criado no **Microsoft Foundry (Azure)** para analisar se o **custo de um Resource Group** aumentou, reduziu ou se manteve estável entre dois períodos.

O agente:

- Recebe:
  - Nome de um Resource Group (real ou de teste);
  - Custo de um período anterior;
  - Custo de um período atual;
- Calcula:
  - Diferença absoluta em moeda;
  - Variação percentual;
- Classifica o resultado como:
  - **AUMENTO**
  - **REDUÇÃO**
  - **ESTÁVEL** (quando a variação é menor que 1% em módulo);
- Explica o resultado em português, com foco em **FinOps**.

> ✅ Projeto individual – Azure Frontier Girls – Build Your First Copilot Challenge (Foundry Edition).  
> 📅 Prazo de entrega: **23/11/2025 às 23:59**.  
> 🎯 Tema: **Como identificar aumento ou redução de custos de Resource Groups**.

---

## 🎯 Objetivo do projeto

Demonstrar um **agente funcional** no Microsoft Foundry que:

1. Utiliza um **modelo de linguagem pré-treinado** (`gpt-5-mini`);
2. Implementa pelo menos **1 ação funcional** (cálculo de variação de custo entre dois períodos);
3. Auxilia na análise de custos de Resource Groups em um contexto de **FinOps**;
4. Está documentado em um **repositório público no GitHub**, com:
   - README completo;
   - Roteiro passo a passo (`docs/roteiro.md`);
   - Prints de telas do Foundry;
   - Referências.

---

## 🧠 Visão geral do agente

- **Nome do agente:** `RG Cost Trend Analyzer`  
- **Plataforma:** Microsoft Foundry (Azure)  
- **Modelo de IA:** `gpt-5-mini`  
  - Tipo de implantação: **Global Standard**  
  - Região: **Brazil South**  
- **Idioma:** Português (Brasil)  

### O que o agente faz

1. Recebe do usuário:
   - Nome do Resource Group;
   - Custo do período anterior;
   - Custo do período atual;
2. Aplica as fórmulas de cálculo definidas no **system prompt**;
3. Devolve uma resposta estruturada informando:
   - Diferença absoluta em reais (R$);
   - Variação percentual aproximada (%);
   - Classificação final: **AUMENTO**, **REDUÇÃO** ou **ESTÁVEL**;
   - Um resumo explicativo em português, voltado para FinOps.

Não há integração automática com o Azure Cost Management neste MVP.  
Os valores são informados pelo usuário (cenários reais ou simulados) para focar na **lógica de cálculo e análise**.

---

## 🧮 Lógica de cálculo usada pelo agente

A lógica foi implementada diretamente nas **instruções (system prompt)** do agente.

**Diferença absoluta:**

```text
diferenca_absoluta = custo_periodo_atual - custo_periodo_anterior

variacao_percentual = (diferenca_absoluta / custo_periodo_anterior) * 100

Se diferenca_absoluta > 0      => tendência = "AUMENTO"
Se diferenca_absoluta < 0      => tendência = "REDUÇÃO"
Se |variacao_percentual| < 1%  => tendência = "ESTÁVEL"

## 🚀 Como testar o agente

1. Acesse o Microsoft Foundry com a conta utilizada no laboratório.
2. Abra o projeto/hub onde o agente foi criado.
3. Vá em **Agentes** e selecione `RG Cost Trend Analyzer`.
4. Abra o painel de teste (chat) e envie um dos exemplos:

```text
Quero analisar o Resource Group rg-aks-prod.
Em outubro o custo foi de R$ 65.726,42 e em novembro foi de R$ 63.720,81.
Me diga se houve aumento ou redução, em quanto (R$) e em porcentagem.


### 2) “Pré-requisitos” (bem simples, opcional)

```markdown
## ✅ Pré-requisitos

- Conta Azure com acesso ao Microsoft Foundry / Azure AI.
- Projeto/hub configurado no Foundry.
- Modelo `gpt-5-mini` implantado na região **Brazil South** (Global Standard).



