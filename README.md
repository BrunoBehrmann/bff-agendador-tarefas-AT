# ⚙️ BFF Agendador de Tarefas

> API Backend-For-Frontend (BFF) responsável por orquestrar o ecossistema de microsserviços de agendamento de tarefas e envio de notificações.

---

## 🎯 Sobre o Projeto

O **bff-agendador-tarefas** atua como o ponto de entrada único (Gateway / BFF) para os clientes no ecossistema de microsserviços. Ele centraliza as requisições externas, simplifica os contratos de comunicação e orquestra de forma desacoplada as chamadas para os microsserviços de domínio (Usuários, Agendamento e Notificação).

---

## 🏛️ Arquitetura do Ecossistema

Este serviço faz parte de uma arquitetura distribuída composta por 4 APIs independentes e containerizadas:

1. **[bff-agendador-tarefas](https://github.com/BrunoBehrmann/bff-agendador-tarefas-AT)** *(Este Repositório)*: Gateway / Orquestrador.
2. **[agendador-tarefas](https://github.com/BrunoBehrmann/agendador-tarefas-AT)**: Microsserviço de regras de negócio, persistência e execução de tarefas (Cron/Task).
3. **[usuario](https://github.com/BrunoBehrmann/usuario-AT)**: Microsserviço de gerenciamento e cadastro de usuários.
4. **[notificacao](https://github.com/BrunoBehrmann/notificacao-AT)**: Microsserviço dedicado ao disparo automatizado de e-mails.

---

## 🛠️ Tecnologias e Dependências

* **Core & Framework:**
  * **Java 17+**
  * **Spring Boot**
  * **Spring Cloud OpenFeign** (Comunicação HTTP declarativa entre microsserviços)
  * **Spring Data JPA / Hibernate**
  * **Spring Web** (Criação de rotas RESTful)
* **Banco de Dados:**
  * **PostgreSQL**
* **DevOps & Ferramentas:**
  * **Docker & Docker Compose** (Orquestração de todo o ambiente local)
  * **Maven** (Gerenciamento de dependências e build)

---

## 🚀 Como Executar

1. **Pré-requisitos:**
   * Ter o [Docker](https://www.docker.com/) e o [Docker Compose](https://docs.docker.com/compose/) instalados.

2. **Clonar o repositório:**
   ```bash
   git clone https://github.com/BrunoBehrmann/bff-agendador-tarefas.git
   cd bff-agendador-tarefas
   ```

3. **Subir os containers:**
   ```bash
   docker-compose up --build
   ```

---

## 📌 Endpoints Principais (Orquestrados)

| Método | Endpoint | Descrição | Microsserviço Destino |
| :--- | :--- | :--- | :--- |
| `POST` | `/usuario` | Cadastra um novo usuário | `usuario` |
| `POST` | `/tarefas` | Cria um novo agendamento | `agendador-tarefas` |
| `GET` | `/tarefas/{id}` | Consulta detalhes de uma tarefa | `agendador-tarefas` |
| `DELETE` | `/tarefas/{id}` | Remove um agendamento | `agendador-tarefas` |
