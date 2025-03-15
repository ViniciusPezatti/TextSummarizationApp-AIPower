📌 Projeto: Resumo de Texto com LangChain e Anthropic

Este projeto utiliza a biblioteca LangChain para processar e resumir um texto longo com a API da Anthropic (Claude-3). Ele realiza a divisão do texto em partes menores e usa um modelo de IA para gerar um resumo conciso.

📂 Estrutura do Código

🔹 Importando as bibliotecas

# Importando as bibliotecas
from langchain_anthropic import ChatAnthropic  # Interação com a API da Anthropic
from langchain.docstore.document import Document  # Manipulação de documentos
from langchain.text_splitter import CharacterTextSplitter  # Divisão de texto
from langchain.chains.summarize import load_summarize_chain  # Carga da cadeia de sumarização
from dotenv import load_dotenv, find_dotenv  # Gerenciamento de variáveis de ambiente
import os  # Manipulação de variáveis do sistema

🔹 Carregando variáveis de ambiente

# Carregar as variáveis de ambiente
load_dotenv(find_dotenv())  # Procura e carrega o arquivo .env
ANTHROPIC_API_KEY = os.environ["ANTHROPIC_API_KEY"]  # Obtém a chave da API da Anthropic

A API Key da Anthropic é carregada de um arquivo .env. Para que o código funcione corretamente, crie um arquivo .env na raiz do projeto e adicione a sua chave da API:

ANTHROPIC_API_KEY=SUACHAVEAQUI

🔹 Criando o modelo de IA

# Criar o modelo AI
llm = ChatAnthropic(
    model='claude-3-opus-20240229',  # Define o modelo Claude-3
    temperature=1,  # Ajusta a criatividade
    anthropic_api_key=ANTHROPIC_API_KEY
)

A variável temperature controla o nível de criatividade do modelo:

0.0: Respostas mais diretas e precisas.

1.0: Respostas mais variadas e criativas.

🔹 Definindo o texto a ser resumido

text = (
    "O Brasil é um país localizado na América do Sul, sendo o quinto maior país do mundo em área territorial. "
    "É uma república federativa presidencialista, formada pela união de 26 estados federados e por um distrito federal. "
    "A capital do Brasil é Brasília e a cidade mais populosa é São Paulo. A língua oficial do Brasil é o português e a moeda é o real. "
    "O Brasil é um país com uma grande diversidade cultural e é conhecido por suas belezas naturais, como as praias, a floresta amazônica e as cachoeiras. "
    "A economia do Brasil é uma das maiores do mundo e é baseada na agricultura, na indústria e nos serviços. "
    "A hiperautomação transforma empresas ao otimizar os processos de negócios, eliminando tarefas repetitivas e automatizando as manuais. "
    "Isso traz vários benefícios importantes."
)

Este é o texto que será processado e resumido pelo modelo.

🔹 Dividindo o texto

# SPLIT TEXT: Dividir o texto em partes menores
text_splitter = CharacterTextSplitter()
texts = text_splitter.split_text(text)

Aqui o texto é dividido em partes menores para facilitar o processamento.

🔹 Criando documentos a partir do texto dividido

# Criar Documentos a partir dos pedaços de texto
docs = [Document(page_content=chunk) for chunk in texts]

Cada pedaço de texto é transformado em um objeto Document.

🔹 Carregando e executando a cadeia de sumarização

# Carregar a cadeia de sumarização utilizando o prompt padrão (sem customização)
chain = load_summarize_chain(llm=llm, chain_type="stuff")

# Executa a cadeia de sumarização e exibe o resumo
summary = chain.invoke(docs)
print(summary['output_text'])

O load_summarize_chain carrega um pipeline que gera o resumo do texto.
O resultado final é impresso no console.

🚀 Como Executar o Projeto

🔹 1. Clonar o repositório

git clone https://github.com/ViniciusPezatti/TextSummarizationApp-AIPower.git
cd SEU_REPOSITORIO

🔹 2. Criar e ativar um ambiente virtual (venv)

No Windows:

python -m venv venv
venv\Scripts\activate

No macOS/Linux:

python3 -m venv venv
source venv/bin/activate

🔹 3. Instalar as dependências

pip install -r requirements.txt

🔹 4. Criar o arquivo .env

Crie um arquivo .env na raiz do projeto e adicione sua chave da API:

ANTHROPIC_API_KEY=SUACHAVEAQUI

🔹 5. Executar o programa

python main.py

🛠 Tecnologias Utilizadas

Python

LangChain

Anthropic API

dotenv

📜 Licença

Este projeto está licenciado sob a MIT License. Sinta-se à vontade para utilizar e modificar.

💡 Autor

Desenvolvido por SEU NOME. Se tiver dúvidas ou sugestões, sinta-se à vontade para contribuir!

