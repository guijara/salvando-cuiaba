🌊 Salvando Cuiabá — Sistema Multiagente de Gestão de Crises Urbanas

O Salvando Cuiabá é uma solução de Engenharia de Software e Inteligência Artificial voltada para a detecção, análise e mitigação autônoma de crises urbanas (como alagamentos e temporais) na região metropolitana de Cuiabá.

O sistema combina uma arquitetura orientada a eventos resiliente no backend com uma orquestração de agentes autônomos baseada em grafos (LangGraph), mantendo sempre o operador humano no controle das ações finais de remediação (Human-in-the-Loop).

🏛️ Arquitetura do Sistema

O sistema opera sob o padrão de separação entre o Motor de Ingestão/Controle (Java/Spring) e a Orquestração Inteligente (Python/LangGraph), comunicando-se de forma assíncrona via mensageria.

 [ APIs Externas ] -> [ Ingestor & Filas ] -> [ Motor Agêntico ] -> [ Control Plane ] -> [ Tomada de Decisão ]
  (Clima / Trânsito)   (Java / RabbitMQ)       (Python / LangGraph)   (Dashboard / API)       (Operador Humano)


Agente Monitor (Ingestão): Consome dados de clima e trânsito em tempo real, disparando eventos de alerta quando limiares críticos são atingidos.

Agente Analista (Geoespacial): Enriquece os dados de alerta cruzando informações de localização com rotas de emergência e proximidade de hospitais.

Agente Comunicador (Fine-Tuned): Utiliza um modelo ajustado com relatórios oficiais para redigir boletins de emergência padronizados.

Control Plane (Human-in-the-Loop): Apresenta o plano de ação gerado para um operador humano aprovar ou ajustar antes da publicação oficial.

🚀 Principais Funcionalidades

Orquestração por Código com LangGraph: Mapeamento de estado e tomada de decisão não-linear entre múltiplos agentes especializados.

Arquitetura Resiliente & Mensageria: Backend em Java 21 + Spring Boot com RabbitMQ para processamento paralelo sem gargalos de I/O.

Fine-Tuning de LLMs: Modelo de linguagem treinado com jargões e protocolos oficiais de órgãos de Defesa Civil.

Estratégia Human-in-the-Loop: Garantia de segurança e controle ético, exigindo chancela humana para decisões críticas.

Esteira de Entrega com Harness: Pipeline automatizado de CI/CD para deploy seguro de microsserviços e modelos.

🛠️ Tech Stack

Backend & Infraestrutura: Java 21, Spring Boot, RabbitMQ, PostgreSQL, Docker, Harness.

Engine de IA: Python, LangGraph, LangChain, Hugging Face (Model Hub/Fine-tuning).

APIs Externas: OpenWeatherMap API, Google Maps Distance Matrix API.

📦 Como Rodar o Projeto

Pré-requisitos

Docker & Docker Compose instalados.

Java 21 JDK + Maven.

Python 3.11+.

1. Clonar o repositório

git clone https://github.com/guijara/salvando-cuiaba.git
cd salvando-cuiaba


2. Subir a infraestrutura (PostgreSQL & RabbitMQ)

docker-compose up -d


3. Configurar Variáveis de Ambiente

Crie um arquivo .env na raiz do projeto Python com as suas chaves:

OPENAI_API_KEY=sua_chave_aqui
OPENWEATHER_API_KEY=sua_chave_aqui
RABBITMQ_HOST=localhost
POSTGRES_URL=jdbc:postgresql://localhost:5432/cuiaba_db


4. Executar o Backend (Java)

cd backend
./mvnw spring-boot:run


5. Executar o Serviço de Agentes (Python)

cd agents
pip install -r requirements.txt
python main.py


👨‍💻 Autor

Desenvolvido por Guilherme Jara

LinkedIn | GitHub
