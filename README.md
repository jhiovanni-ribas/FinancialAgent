# 🎙️ FinOps Advisor: 
Agente de Voz Inteligente para Finanças 🤖⚖️

Este repositório contém o projeto final do Bootcamp de IA Generativa. Desenvolvemos um agente financeiro inteligente capaz de realizar consultas proativas por voz, utilizando técnicas avançadas de IA Generativa para auxiliar na tomada de decisão financeira com precisão e segurança.


## Contexto

Os assistentes virtuais financeiros estão evoluindo de chatbots reativos para agentes proativos. O FinOps Advisor foi projetado para:

**Antecipar necessidades:** Analisar o histórico de transações para alertar sobre limites de orçamento.
**Sugestões Personalizadas:** Cruzar perfis de investimento com dados financeiros para recomendações sob medida.
**Interface Voice-First:** Otimizado para profissionais jurídicos e financeiros que precisam de acesso a dados sem usar as mãos.
**Anti-Alucinação:** Implementa um controle rígido de grounding utilizando apenas bases de dados locais.

> [!TIP]
> Na pasta [`examples/`](./examples/) você encontra referências de implementação para cada etapa deste desafio.

---

### 1. Documentação do Agente: FinOps Advisor

Abaixo estão as **definições** do Projeto:

- **Caso de Uso:** Assistente de voz para profissionais de LegalOps que realiza consultas "mãos-livres" em bases de dados financeiras e perfis de investimento.
- **Persona e Tom de Voz:** Atua como um **Controller Sênior**, utilizando um tom executivo, técnico e pedagógico, focado em respostas curtas para áudio.
- **Arquitetura:** Pipeline de voz local com estratégia **RAG** (Retrieval-Augmented Generation), integrando arquivos CSV/JSON ao modelo **Google Gemini Pro**.
- **Segurança:** Implementa **Grounding Estrito**, restringindo as respostas apenas aos dados fornecidos para eliminar alucinações e garantir 100% de confiabilidade.

📄 **Template:** [`docs/01-documentacao-agente.md`](./docs/01-documentacao-agente.md)

---

### 2. Base de Conhecimento

Utilize os **dados mockados** disponíveis na pasta [`data/`](./data/) para alimentar seu agente:

| Arquivo | Formato | Descrição |
|---------|---------|-----------|
| `transacoes.csv` | CSV | Histórico de transações do cliente |
| `historico_atendimento.csv` | CSV | Histórico de atendimentos anteriores |
| `perfil_investidor.json` | JSON | Perfil e preferências do cliente |
| `produtos_financeiros.json` | JSON | Produtos e serviços disponíveis |

Você pode adaptar ou expandir esses dados conforme seu caso de uso.

📄 **Template:** [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md)

---

### 3. Prompts do Agente

Documente os prompts que definem o comportamento do seu agente:

- **System Prompt:** Instruções gerais de comportamento e restrições
- **Exemplos de Interação:** Cenários de uso com entrada e saída esperada
- **Tratamento de Edge Cases:** Como o agente lida com situações limite

📄 **Template:** [`docs/03-prompts.md`](./docs/03-prompts.md)

---

### 4. Aplicação Funcional

Desenvolva um **protótipo funcional** do seu agente:

- Chatbot interativo (sugestão: Streamlit, Gradio ou similar)
- Integração com LLM (via API ou modelo local)
- Conexão com a base de conhecimento

📁 **Pasta:** [`src/`](./src/)

---

### 5. Avaliação e Métricas

Descreva como você avalia a qualidade do seu agente:

**Métricas Sugeridas:**
- Precisão/assertividade das respostas
- Taxa de respostas seguras (sem alucinações)
- Coerência com o perfil do cliente

📄 **Template:** [`docs/04-metricas.md`](./docs/04-metricas.md)

---

### 6. Pitch

Grave um **pitch de 3 minutos** (estilo elevador) apresentando:

- Qual problema seu agente resolve?
- Como ele funciona na prática?
- Por que essa solução é inovadora?

📄 **Template:** [`docs/05-pitch.md`](./docs/05-pitch.md)

---

## 🛠️ Ferramentas Utilizadas

Todas as ferramentas selecionadas para o **FinOps Advisor** possuem versões gratuitas ou são de código aberto:

| Categoria | Ferramentas |
|-----------|-------------|
| **LLM Engine** | [Gemini API](https://ai.google.dev/), [Google AI Studio](https://aistudio.google.com/) |
| **Desenvolvimento** | [Python 3.14](https://www.python.org/), [VS Code](https://code.visualstudio.com/), [Pandas](https://pandas.pydata.org/) |
| **Engenharia de Voz** | [SpeechRecognition](https://pypi.org/project/SpeechRecognition/), [pyttsx3](https://pypi.org/project/pyttsx3/), [SoundDevice](https://python-sounddevice.readthedocs.io/) |
| **Diagramas** | [Mermaid](https://mermaid.js.org/), [Lucidchart](https://www.lucidchart.com/) |

---

## Estrutura do Repositório

```
📁 lab-agente-financeiro/
│
├── 📄 README.md
│
├── 📁 data/                          # Dados mockados para o agente
│   ├── historico_atendimento.csv     # Histórico de atendimentos (CSV)
│   ├── perfil_investidor.json        # Perfil do cliente (JSON)
│   ├── produtos_financeiros.json     # Produtos disponíveis (JSON)
│   └── transacoes.csv                # Histórico de transações (CSV)
│
├── 📁 docs/                          # Documentação do projeto
│   ├── 01-documentacao-agente.md     # Caso de uso e arquitetura
│   ├── 02-base-conhecimento.md       # Estratégia de dados
│   ├── 03-prompts.md                 # Engenharia de prompts
│   ├── 04-metricas.md                # Avaliação e métricas
│   └── 05-pitch.md                   # Roteiro do pitch
│
├── 📁 src/                           # Código da aplicação
│   └── app.py                        # (exemplo de estrutura)
│
├── 📁 assets/                        # Imagens e diagramas
│   └── ...
│
└── 📁 examples/                      # Referências e exemplos
    └── README.md
```

---

## Dicas Finais

1. **Comece pelo prompt:** Um bom system prompt é a base de um agente eficaz
2. **Use os dados mockados:** Eles garantem consistência e evitam problemas com dados sensíveis
3. **Foque na segurança:** No setor financeiro, evitar alucinações é crítico
4. **Teste cenários reais:** Simule perguntas que um cliente faria de verdade
5. **Seja direto no pitch:** 3 minutos passam rápido, vá ao ponto
