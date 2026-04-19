
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

## 1. Preparar o Ambiente
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

Lógica de Funcionamento: RAG Local
O script utiliza uma técnica de RAG (Retrieval-Augmented Generation) simplificada:

**Extração:** O motor de dados lê arquivos .csv e .json locais.
**Contextualização:** Os dados são injetados no System Prompt enviado ao Gemini-Flash.
**Interface Humana:** A interação ocorre via captura de áudio (STT) e resposta sintetizada (TTS) com velocidade de 1.5x (300 rate).


# SCRIPT

import os
import json
import pandas as pd
import pyttsx3
import sounddevice as sd
from scipy.io.wavfile import write
import speech_recognition as sr
from google import genai

# 1. Configurações Iniciais e API
MODELO_ESTAVEL = 'gemini-flash-latest'

# SEGURANÇA: Buscando a chave das variáveis de ambiente do sistema
# Para rodar localmente, você pode definir no terminal: setx GEMINI_API_KEY "sua_chave"
api_key = os.getenv("GEMINI_API_KEY")

if not api_key:
    print("⚠️ Erro: Variável de ambiente GEMINI_API_KEY não encontrada.")
    # Apenas para teste local rápido, você pode descomentar a linha abaixo (MAS NÃO SUBIR AO GITHUB)
    # api_key = "COLE_SUA_CHAVE_AQUI_APENAS_PARA_TESTE_LOCAL"

client = genai.Client(api_key=api_key)

# 2. Motor de Dados (RAG Local)
def carregar_contexto():
    """Lê a base de conhecimento para ancorar as respostas do Gemini."""
    try:
        # Caminhos relativos para funcionar em qualquer PC
        with open('data/perfil_investidor.json', 'r', encoding='utf-8') as f:
            perfil = json.load(f)
        
        with open('data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
            produtos = json.load(f)
            
        transacoes = pd.read_csv('data/transacoes.csv').to_string()
        historico = pd.read_csv('data/historico_atendimento.csv').to_string()
        
        return f"""
        DADOS DO CLIENTE (CÉSAR): {perfil}
        CATÁLOGO DE PRODUTOS: {produtos}
        EXTRATO DE TRANSAÇÕES: {transacoes}
        HISTÓRICO DE CHATS ANTERIORES: {historico}
        """
    except Exception as e:
        return f"Erro ao carregar base de dados: {e}"

# 3. Funções de Voz (STT e TTS)
def falar(texto):
    """Transforma texto em voz (1.5x) para o César."""
    print(f"FinOps Advisor: {texto}")
    try:
        engine = pyttsx3.init()
        engine.setProperty('rate', 300) # Velocidade acelerada (perfil executivo)
        texto_limpo = texto.replace("*", "").replace("#", "")
        engine.say(texto_limpo)
        engine.runAndWait()
    except Exception as e:
        print(f"Erro no áudio: {e}")

def ouvir_usuario():
    """Captura a voz do usuário e converte em texto."""
    fs = 44100
    segundos = 5
    print("\n--- 🎙️ Ouvindo César (5s)... ---")
    
    gravacao = sd.rec(int(segundos * fs), samplerate=fs, channels=1, dtype='int16')
    sd.wait()
    write('pergunta.wav', fs, gravacao)
    
    rec = sr.Recognizer()
    with sr.AudioFile('pergunta.wav') as source:
        audio = rec.record(source)
        try:
            texto = rec.recognize_google(audio, language="pt-BR")
            print(f"César: {texto}")
            return texto
        except:
            return None

# 4. Loop de Inteligência
system_prompt = """
Você é o FinOps Advisor, um Controller Financeiro Sênior. 
Trate o usuário como César. Use os dados fornecidos para dar respostas curtas e precisas.
Sempre alerte se houver gastos individuais acima de R$ 500. 
Seja analítico e focado em investimentos e LegalOps.
"""

print("--- FINOPS ADVISOR INICIADO ---")
falar("Olá César! Sou seu Advisor. Como está sua gestão financeira hoje?")

while True:
    contexto_atual = carregar_contexto()
    pergunta = ouvir_usuario()
    
    if pergunta:
        # Comandos de interrupção
        if pergunta.lower() in ['sair', 'parar', 'tchau', 'encerrar']:
            falar("Até logo, César! Sucesso na sua transição para LegalOps.")
            break
            
        try:
            # RAG: Injetando o sistema + dados locais + pergunta do usuário
            prompt_completo = f"{system_prompt}\n\nCONTEXTO:\n{contexto_atual}\n\nPERGUNTA: {pergunta}"
            
            response = client.models.generate_content(
                model=MODELO_ESTAVEL, 
                contents=prompt_completo
            )
            
            if response.text:
                falar(response.text)
                
        except Exception as e:
            print(f"Erro na API Gemini: {e}")
    else:
        print("Aguardando voz...")

        


