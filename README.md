# 🤖 FinOps Advisor: Agente de Voz Inteligente para Finanças ⚖️

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

Foi utilizado os seguintes **dados mockados** disponíveis na pasta [`data/`](./data/) para alimentar o agente:


| Arquivo | Formato | Utilização no Agente |
|---------|---------|----------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores para um atendimento contínuo. |
| `perfil_investidor.json` | JSON | Personalizar recomendações e validar limites de risco conforme o perfil do cliente. |
| `produtos_financeiros.json` | JSON | Sugerir serviços bancários e investimentos adequados ao portfólio do usuário. |
| `transacoes.csv` | CSV | Analisar o fluxo de caixa, identificar padrões de gastos e alertar sobre limites. |


📄 **Template:** [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md)

---

### 3. Prompts do Agente

Documente os prompts que definem o comportamento do seu agente:

- **Prompts do Agente:** Instruções estruturadas com Few-Shot Prompting e Grounding Estrito, garantindo que o agente atue como um Controller Sênior focado em precisão de dados.

- **Engenharia de Voz (TTS Optmized):** Refinamento de prompts para saídas curtas e diretas, otimizadas para motores de síntese de voz, garantindo fluidez em áudio acelerado (1.5x).

- **Tratamento de Exceções e Edge Cases:** Camada de segurança que blinda o agente contra perguntas fora do escopo financeiro e tentativas de acesso a dados sensíveis/senhas.

📄 **Template:** [`docs/03-prompts.md`](./docs/03-prompts.md)

---

### 4. Aplicação Funcional

**Protótipo funcional** de um Controller Digital capaz de realizar leitura de bases CSV/JSON, histórico de atendimento e automação de alertas financeiros via interação por voz:

- **Ferramentas de Desenvolvimento:** Desenvolvimento em Python 3.14 utilizando as bibliotecas Pyttsx3 para voz, SpeechRecognition para transcrição e o modelo Gemini-Flash-Latest para inferência.
  
- **Integração de Dados:** Conexão nativa com a base de conhecimento local composta por arquivos CSV (transacoes.csv, historico_atendimento.csv) e JSON (perfil_investidor.json, produtos_financeiros.json).
  
- **Pipeline de Recuperação (RAG):** Implementação de lógica para extração e pré-processamento de dados em tempo real, permitindo que a LLM contextualize respostas com base no histórico de atendimento e portfólio de produtos do cliente.

📁 **Pasta:** [`src/`](./src/)

---

### 5. Avaliação e Métricas

O desempenho do FinOps Advisor foi validado através de testes de estresse técnico e consistência de dados, garantindo uma ferramenta confiável para o suporte à decisão:

- **Assertividade e Precisão (RAG Local):** O agente demonstrou 100% de acerto na recuperação de dados sensíveis, extraindo valores exatos do transacoes.csv (como o gasto de R$ 550,00 em lazer) sem alucinações de valores ou categorias.
  
- **Segurança e Estabilidade de Ambiente:** Implementação de um ambiente virtual isolado (.venv), garantindo que a aplicação opere livre de conflitos de bibliotecas externas e mantendo a integridade do processamento de áudio e dados.
  
- **Coerência e Alinhamento Ético:** As respostas mantêm total fidelidade ao perfil do cliente, sugerindo aportes em áreas de interesse (Tecnologia/Energia) e emitindo alertas proativos sempre que um limite ético de gastos (R$ 500,00) é ultrapassado.

📄 **Template:** [`docs/04-metricas.md`](./docs/04-metricas.md)

---

### 6. Pitch: A Revolução da Gestão Financeira por Voz

**FinOps Advisor: Como a Inteligência Artificial está libertando profissionais de elite das planilhas complexas.**

Assista à nossa apresentação executiva de 3 minutos e descubra como transformamos dados estáticos em um consultor financeiro proativo:

⚡ **Do Caos à Clareza em Segundos:** Veja como o César utiliza comandos de voz para obter diagnósticos precisos sobre seus gastos e investimentos, eliminando a barreira técnica entre o usuário e seus dados financeiros.

🧠 **Inteligência com "Pé no Chão":** Entenda a arquitetura de RAG Local que permite à IA analisar extratos reais e perfis de investidor sem que as informações sensíveis saiam do ambiente controlado do usuário.

🛡️ **O Futuro da Controladoria Pessoal:** Descubra por que o sistema de alertas automáticos para gastos acima de R$ 500,00 é o divisor de águas para manter a saúde financeira em dia durante transições de carreira desafiadoras.

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
