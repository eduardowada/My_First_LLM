# Chatbot com Large Language Model (LLM)

Este projeto consiste na criação de um chatbot utilizando um modelo de linguagem de grande escala (LLM) desenvolvido em Python durante a imersão de inteligência artificial da Alura.


##  Descrição do Projeto
- Este projeto implementa um chatbot usando a biblioteca google-generativeai para interagir com um modelo de linguagem desenvolvido pela Google. O chatbot - pode responder a várias perguntas e fornecer informações sobre diferentes tópicos, demonstrando as capacidades do modelo de linguagem natural.

## Instalação
1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/My_First_LLM.git
cd My_First_LLM
```

2. Instale as dependências:

```bash
pip install -q -U google-generativeai
```

## Uso

1. Importe a biblioteca e configure a chave de API:

```python
import google.generativeai as genai
from google.colab import userdata

GOOGLE_API_KEY = "COLE SUA API KEY AQUI"
genai.configure(api_key=GOOGLE_API_KEY)
```

2. Liste os modelos disponíveis:

```python
for m in genai.list_models():
    if 'generateContent' in m.supported_generation_methods:
        print(m.name)
```

3. Configure o modelo:

```python
generation_config = {
    "candidate_count": 1,
    "temperature": 0.5,
}

safety_settings = {
    "HARASSMENT": "BLOCK_NONE",
    "HATE": "BLOCK_NONE",
    "SEXUAL": "BLOCK_NONE",
    "DANGEROUS": "BLOCK_NONE",
}

model = genai.GenerativeModel(model_name="gemini-1.0-pro", generation_config=generation_config, safety_settings=safety_settings)
```

## Configuração do Modelo
A configuração do modelo inclui a definição de parâmetros como candidate_count e temperature, além de configurações de segurança para filtrar conteúdos inadequados. O modelo utilizado é o gemini-1.0-pro.

## Exemplos de Interação
1. Geração de conteúdo:

```python
response = model.generate_content("Vamos aprender conteúdo sobre IA. Me dê sugestões.")
print(response.text)
```

Saída:

```markdown

**Fundamentos da IA**
...
**Recursos para Aprender IA**
```

Início do chat:

```python
chat = model.start_chat(history=[])
```

Interação contínua:

```python
prompt = input("Esperando prompt: ")

while prompt != "fim":
    response = chat.send_message(prompt)
    print("Resposta: ", response.text, "\n")
    prompt = input("Esperando prompt: ")
```

Melhorando a visualização:

```python
import textwrap
from IPython.display import display
from IPython.display import Markdown

def to_markdown(text):
    text = text.replace('•', '  *')
    return Markdown(textwrap.indent(text, '> ', predicate=lambda _: True))

for message in chat.history:
    display(to_markdown(f'**{message.role}**: {message.parts[0].text}'))
    print('-'*100)
```
