# Base de Conhecimento

## ## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|----------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores para um atendimento contínuo. |
| `perfil_investidor.json` | JSON | Personalizar recomendações e validar limites de risco conforme o perfil do cliente. |
| `produtos_financeiros.json` | JSON | Sugerir serviços bancários e investimentos adequados ao portfólio do usuário. |
| `transacoes.csv` | CSV | Analisar o fluxo de caixa, identificar padrões de gastos e alertar sobre limites. |


---

## Adaptações nos Dados

Expandimos os dados mockados para incluir campos de "Categoria de Risco" no arquivo JSON e "Status de Urgência" no histórico de transações, permitindo que o agente priorize alertas de voz sobre gastos essenciais.

---

## Estratégia de Integração

### Como os dados são carregados?

Os arquivos são carregados na inicialização do sistema através da biblioteca Pandas (para CSVs) e json nativo. Eles permanecem em memória durante a sessão para garantir que a resposta de voz seja instantânea.

### Como os dados são usados no prompt?

Utilizamos uma estratégia de RAG Dinâmico: o script Python filtra as linhas mais relevantes da base de dados com base na pergunta do usuário e as injeta no contexto do Prompt do Gemini. Isso evita que o prompt fique muito longo e caro, mantendo o foco na dúvida atual.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: César (Exemplo)
- Perfil: Arrojado
- Saldo disponível: R$ 12.500

Últimas transações:
- 15/04: Investimento Ações - R$ 2.000
- 17/04: Assinatura Software - R$ 150
...
```
