# GS02 - Gestor de Resíduos Inteligente (MVP)

## 🎯 Objetivo do Projeto

Este projeto é um **Produto Mínimo Viável (MVP)** desenvolvido para a disciplina GS02, com o objetivo de aplicar técnicas de Visão Computacional e Inteligência Artificial para auxiliar cooperativas de catadores de resíduos. O foco é na **identificação automática e precisa** de diferentes tipos de materiais recicláveis (Plástico, Vidro, Metal, Papel, Orgânico e Embalagens) em um ambiente simulado de esteira de triagem.

O sistema demonstra a arquitetura completa de um sistema de triagem inteligente, desde a detecção do objeto até o envio da informação para um sistema de controle (simulado por uma API).

## 🏗️ Arquitetura do Sistema

O projeto é dividido em três componentes principais que simulam um sistema de triagem em tempo real:

| Componente | Tecnologia | Função |
| :--- | :--- | :--- |
| **Modelo de Detecção** | YOLOv8n (Ultralytics) | Treinado para identificar 6 classes de resíduos. |
| **Processador em Lote** | Python (OpenCV, Requests) | Lê imagens de uma pasta, executa a detecção, desenha a caixa delimitadora e codifica o resultado em Base64. |
| **API de Simulação** | Python (Flask) | Simula o servidor de controle da esteira. Recebe o POST do processador, decodifica a imagem e a classe, e registra a ação. |
| **Frontend (Simulação)** | Netlify (Externo) | Simulação visual da esteira de triagem. |

## ⚙️ Requisitos e Instalação

Para rodar o projeto localmente, você precisará ter o Python 3.8+ instalado.

### 1. Clonar o Repositório

```bash
git clone https://github.com/jjdominguess/GS02_Gestor_de_Residuos.git
cd GS02_Gestor_de_Residuos
```

### 2. Instalar Dependências

Recomendamos o uso de um ambiente virtual (`venv` ou `conda`).

```bash
# Cria e ativa o ambiente virtual
python -m venv yolo_env
# No Windows:
.\yolo_env\Scripts\activate
# No Linux/macOS:
source yolo_env/bin/activate

# Instala as bibliotecas necessárias
pip install ultralytics opencv-python numpy requests flask
```

### 3. Configuração do Modelo

O projeto espera que o seu modelo treinado (`best.pt`) esteja no caminho padrão.

*   **Verifique o caminho:** Certifique-se de que o arquivo `best.pt` do seu treinamento multiclasse esteja acessível.
*   **Ajuste:** Se necessário, altere a variável `MODEL_PATH` nos scripts `batch_processor.py` e `sample-api.py`.

## 🚀 Como Executar o Protótipo

O protótipo é executado em dois passos, simulando a comunicação entre o detector e o servidor.

### Passo 1: Iniciar a API de Simulação (Servidor)

Abra um terminal e execute o script da API. Ele ficará aguardando requisições na porta `5000`.

```bash
python sample-api.py
```

### Passo 2: Processar as Imagens e Enviar o POST

1.  **Crie a pasta:** Crie uma pasta chamada `images_to_process` na raiz do projeto.
2.  **Adicione Imagens:** Coloque as imagens que deseja testar dentro dessa pasta.
3.  **Execute o Processador:** Abra um **segundo terminal** e execute o script de processamento em lote.

```bash
python batch_processor.py
```

**Resultado:**
*   O `batch_processor.py` irá processar cada imagem, detectar o material e enviar um POST JSON para a API.
*   O terminal da API (`sample-api.py`) irá logar o recebimento do dado e salvar a imagem processada (com a caixa de detecção) na pasta `imagens_recebidas/`.

## 💻 Treinamento no Google Colab

Para replicar o treinamento do modelo YOLOv8 multiclasse, utilize o notebook Jupyter anexo (`yolov8_multiclass_training.ipynb`).

O notebook contém os passos necessários para:
1.  Instalar as bibliotecas no ambiente Colab.
2.  Montar o Google Drive para acesso ao dataset.
3.  Executar o comando de treinamento com o dataset unificado.

Este notebook é ideal para re-treinar o modelo com novos dados ou para demonstrar o processo de treinamento.

---
*Desenvolvido por [Seu Nome/Time] para a GS02.*
