# Roteiro do Projeto – RG Cost Trend Analyzer

Este documento descreve o passo a passo para criação do agente **RG Cost Trend Analyzer** no Microsoft Foundry, utilizando o modelo `gpt-5-mini` para analisar aumento ou redução de custos de Resource Groups entre dois períodos.

O roteiro serve como evidência da implementação (pedido da disciplina), incluindo prints de tela, decisões de arquitetura e observações.

---

## 1. Criação / seleção do projeto no Microsoft Foundry

1. Acessar o portal do **Microsoft Foundry** com a conta Azure.
2. Selecionar ou criar um **hub/projeto** para o laboratório, por exemplo:

   - Nome do hub/projeto: `aihub-finops-rg-cost` ou `rgcostanalyzer`.

3. Na tela de visão geral, verificar:
   - **Chave de API** do projeto;
   - **Endpoint de chamada**.

> **Print:** `docs/prints/print-01-projeto-foundry.png`  
> *(Visão geral do projeto no Foundry.)*

---

## 2. Implantação do modelo gpt-5-mini

Como o agente precisa entender perguntas em português e realizar cálculos simples, foi escolhido o modelo **`gpt-5-mini`** (bom equilíbrio entre custo e capacidade).

Passos:

1. No menu **Agentes**, iniciar a criação de um novo agente.
2. Na etapa de seleção de modelo, escolher **`gpt-5-mini`**.
3. Na tela de implantação do modelo, configurar:

   - **Nome da implantação:** `gpt-5-mini`
   - **Tipo de implantação:** `Global Standard`
   - **Local do recurso:** `Brazil South`
   - **Capacidade:** padrão (100K tokens por minuto)
   - **Segurança de conteúdo:** `DefaultV2`
   - **Política de atualização:** `Quando uma nova versão padrão estiver disponível`

4. Clicar em **Implantar** e aguardar a conclusão.

> **Print:** `docs/prints/print-02-implantacao-gpt5mini.png`  
> *(Tela de implantação do modelo, com `Global Standard` e `Brazil South`.)*

---

## 3. Criação do agente RG Cost Trend Analyzer

Depois de implantar o modelo, o próximo passo é criar o agente.

1. No menu **Agentes**, clicar em **Novo agente**.
2. Configurar:

   - **Nome do agente:** `RG Cost Trend Analyzer`
   - **Implantação de modelo:** `gpt-5-mini (version: 2025-08-07)` ou equivalente
   - **Idioma principal:** Português (Brasil)

3. Salvar o agente.

> **Print:** `docs/prints/print-03-lista-agentes.png`  
> *(Tela listando o agente `RG Cost Trend Analyzer` usando o modelo `gpt-5-mini`.)*

---

## 4. Configuração das instruções (system prompt)

Para transformar o modelo genérico em um agente de **FinOps** focado em análise de custos, foi definido um **system prompt** com regras claras de cálculo.

Na tela de edição do agente, no campo **Instruções**, foi configurado um texto semelhante a:

```text
Você é um agente de FinOps especializado em análise de custos de cloud por Resource Group.
Seu objetivo é ajudar o usuário a entender se o custo de um Resource Group aumentou, reduziu ou se manteve estável entre dois períodos.

REGRAS DE CÁLCULO:
- Considere sempre que os valores fornecidos pelo usuário já estão na mesma moeda.
- Use as fórmulas:

  diferenca_absoluta = custo_periodo_atual - custo_periodo_anterior

  Se custo_periodo_anterior > 0:
      variacao_percentual = (diferenca_absoluta / custo_periodo_anterior) * 100
  Caso contrário, não calcule a variação percentual.

- Classificação:
  - Se diferenca_absoluta > 0 => tendência = "AUMENTO"
  - Se diferenca_absoluta < 0 => tendência = "REDUÇÃO"
  - Se o valor absoluto da variacao_percentual for menor que 1% => tendência = "ESTÁVEL"

COMPORTAMENTO DE RESPOSTA:
Sempre que o usuário informar nome do RG e custos de dois períodos diferentes, você deve:

1. Repetir os valores entendidos (nome do RG, período anterior e período atual).
2. Aplicar as fórmulas exatamente como definido acima.
3. Responder em formato estruturado:

- Nome do RG
- Período analisado (ex.: Outubro/2025 x Novembro/2025)
- Custo período anterior
- Custo período atual
- Diferença absoluta (com sinal)
- Variação percentual (com uma casa decimal)
- Tendência (AUMENTO, REDUÇÃO ou ESTÁVEL)
- Uma explicação curta em português claro, voltada para FinOps.

Sempre responda em português (Brasil).
Não invente valores: use apenas os números fornecidos pelo usuário.
