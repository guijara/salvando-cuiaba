# 🌊 Salvando Cuiabá — Sistema Multiagente de Gestão de Crises Urbanas

[![Java 21](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Python 3.11](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![LangGraph](https://img.shields.io/badge/LangGraph-Orchestration-violet.svg)](https://www.langchain.com/langgraph)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-Messaging-ff6600.svg)](https://www.rabbitmq.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

O **Salvando Cuiabá** é uma solução de Engenharia de Software e Inteligência Artificial voltada para a detecção, análise e mitigação autônoma de crises urbanas (como alagamentos e temporais) na região metropolitana de Cuiabá. 

O sistema combina uma **arquitetura orientada a eventos resiliente** no backend com uma **orquestração de agentes autônomos baseada em grafos (LangGraph)**, mantendo sempre o operador humano no controle das ações finais de remediação (*Human-in-the-Loop*).

---

## 🏛️ Arquitetura do Sistema

O sistema opera sob o padrão de separação entre o **Motor de Ingestão/Controle (Java/Spring)** e a **Orquestração Inteligente (Python/LangGraph)**, comunicando-se de forma assíncrona via mensageria.

```text
 [ APIs Externas ] -> [ Ingestor & Filas ] -> [ Motor Agêntico ] -> [ Control Plane ] -> [ Tomada de Decisão ]
  (Clima / Trânsito)   (Java / RabbitMQ)       (Python / LangGraph)   (Dashboard / API)       (Operador Humano)
```

1. **Agente Monitor (Ingestão):** Consome dados de clima e trânsito em tempo real, disparando eventos de alerta quando limiares críticos são atingidos.
2. **Agente Analista (Geoespacial):** Enriquece os dados de alerta cruzando informações de localização com rotas de emergência e proximidade de hospitais.
3. **Agente Comunicador (Fine-Tuned):** Utiliza um modelo ajustado com relatórios oficiais para redigir boletins de emergência padronizados.
4. **Control Plane (Human-in-the-Loop):** Apresenta o plano de ação gerado para um operador humano aprovar ou ajustar antes da publicação oficial.

---

## 🚀 Principais Funcionalidades

- **Orquestração por Código com LangGraph:** Mapeamento de estado e tomada de decisão não-linear entre múltiplos agentes especializados.
- **Arquitetura Resiliente & Mensageria:** Backend em Java 21 + Spring Boot com RabbitMQ para processamento paralelo sem gargalos de I/O.
- **Fine-Tuning de LLMs:** Modelo de linguagem treinado com jargões e protocolos oficiais de órgãos de Defesa Civil.
- **Estratégia Human-in-the-Loop:** Garantia de segurança e controle ético, exigindo chancela humana para decisões críticas.
- **Esteira de Entrega com Harness:** Pipeline automatizado de CI/CD para deploy seguro de microsserviços e modelos.

---

## 🛠️ Tech Stack

- **Backend & Infraestrutura:** Java 21, Spring Boot, RabbitMQ, PostgreSQL, Docker, Harness.
- **Engine de IA:** Python, LangGraph, LangChain, Hugging Face (Model Hub/Fine-tuning).
- **APIs Externas:** OpenWeatherMap API, Google Maps Distance Matrix API.

---

## 📦 Como Rodar o Projeto

### Pré-requisitos
- Docker & Docker Compose instalados.
- Java 21 JDK + Maven.
- Python 3.11+.

### 1. Clonar o repositório
```bash
git clone https://github.com/guijara/salvando-cuiaba.git
cd salvando-cuiaba
```

### 2. Subir a infraestrutura (PostgreSQL & RabbitMQ)
```bash
docker-compose up -d
```

### 3. Configurar Variáveis de Ambiente
Crie um arquivo `.env` na raiz do projeto Python com as suas chaves:
```env
OPENAI_API_KEY=sua_chave_aqui
OPENWEATHER_API_KEY=sua_chave_aqui
RABBITMQ_HOST=localhost
POSTGRES_URL=jdbc:postgresql://localhost:5432/cuiaba_db
```

### 4. Executar o Backend (Java)
```bash
cd backend
./mvnw spring-boot:run
```

### 5. Executar o Serviço de Agentes (Python)
```bash
cd agents
pip install -r requirements.txt
python main.py
```

---

## 👨‍💻 Autor

Desenvolvido por **Guilherme Jara**  
[LinkedIn](https://linkedin.com/in/guilhermejara) | [GitHub](https://github.com/guijara)
