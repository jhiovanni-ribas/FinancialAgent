
# 🛠️ Código da Aplicação - FinOps Advisor

Esta pasta contém o núcleo da inteligência e interface do agente financeiro desenvolvido para o perfil do César (LegalOps).

## 📂 Estrutura do Projeto

```text
src/
├── main.py             # Script principal (Lógica de voz + RAG + Gemini)
├── data/               # Base de conhecimento local (CSV/JSON)
│   ├── perfil_investidor.json
│   ├── produtos_financeiros.json
│   ├── transacoes.csv
│   └── historico_atendimento.csv
└── requirements.txt    # Dependências do projeto
```

## 📦 Dependências (requirements.txt)

```
pandas
pyttsx3
google-genai
sounddevice
scipy
SpeechRecognition
```

# ETAPAS

1. Preparar o Ambiente
Recomendamos o uso de um ambiente virtual para evitar conflitos de interpretadores:

```bash
# Criar ambiente virtual
python -m venv .venv

# Ativar no Windows (PowerShell)
.\.venv\Scripts\activate

# Se houver erro de permissão no PowerShell:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```
2. Instalar Bibliotecas
   
```
pip install -r requirements.txt
```

3. Configurar API Key

No arquivo main.py, substitua a variável api_key pela sua chave gerada no Google AI Studio:
client = genai.Client(api_key="SUA_CHAVE_AQUI")


4. Executar
   
```
python main.py
```

# Lógica de Funcionamento: RAG Local
O script utiliza uma técnica de RAG (Retrieval-Augmented Generation) simplificada:

**Extração:** O motor de dados lê arquivos .csv e .json locais.
**Contextualização:** Os dados são injetados no System Prompt enviado ao Gemini-Flash.
**Interface Humana:** A interação ocorre via captura de áudio (STT) e resposta sintetizada (TTS) com velocidade de 1.5x (300 rate).


