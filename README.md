# 📘 Cadastro de Usuários – API CRUD  

![Java](https://img.shields.io/badge/Java-17+-red)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-brightgreen)
![Maven](https://img.shields.io/badge/Maven-Build-blue)
![H2](https://img.shields.io/badge/Database-H2-yellow)
![Status](https://img.shields.io/badge/Status-Ativo-success)

---

## 📝 Sobre o projeto

Este projeto é uma **API REST** desenvolvida em **Java + Spring Boot** para gerenciamento de usuários através de operações CRUD (Create, Read, Update, Delete).

Tecnologias usadas:

- Java 25 (JDK 25)
- Spring Boot
- H2 Database
- Spring Data JPA
- Lombok
- Maven

prática de back-end e demonstração de API REST.

---

## 🚀 Funcionalidades

- Criar usuários  
- Listar todos os usuários  
- Buscar usuário por ID  
- Atualizar dados  
- Excluir usuários  
- Persistência via Spring Data JPA  
- Console H2 ativado  

---

## 🧩 Arquitetura

A aplicação segue o padrão em camadas:

controller → recebe requisições HTTP
service → regras de negócio
repository → operações no banco de dados
entity → modelo representando a tabela


### 📊 Diagrama da Arquitetura

      ┌─────────────────────────┐
      │       Controller         │
      │   (UsuarioController)    │
      └──────────────┬──────────┘
                     │
                     ▼
      ┌─────────────────────────┐
      │        Service          │
      │    (UsuarioService)     │
      └──────────────┬──────────┘
                     │
                     ▼
      ┌─────────────────────────┐
      │       Repository         │
      │  (UsuarioRepository)     │
      └──────────────┬──────────┘
                     │
                     ▼
      ┌─────────────────────────┐
      │         Entity           │
      │       (Usuario)          │
      └─────────────────────────┘


---

## 📘 Diagrama UML – Entidade `Usuario`


+----------------------+
|      Usuario         |
+----------------------+
| - id: Long           |
| - nome: String       |
| - email: String      |
| - idade: Integer     |
+----------------------+
| + getId()            |
| + getNome()          |
| + getEmail()         |
| + getIdade()         |
| + setId()            |
| + setNome()          |
| + setEmail()         |
| + setIdade()         |
+----------------------+

---

## 🔄 Fluxo do CRUD

        Cliente/API Client
                │
                ▼
        [Controller]
                │
                ▼
        [Service Layer]
                │
                ▼
        [Repository JPA]
                │
                ▼
         [H2 Database]

---

## ⚙️ Configurações principais (`application.properties`)


spring.application.name=cadastro-usuario

# H2 Console
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

# Banco de dados H2
spring.datasource.url=jdbc:h2:mem:usuarios
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=ehl
spring.datasource.password=

# Criar e dropar tabelas a cada execução
spring.jpa.hibernate.ddl-auto=create-drop

# Porta do servidor
server.port=1110

---

## ▶️ Como executar o projeto
✔️ Pré-requisitos

Java 17+

Maven

✔️ Executando

./mvnw spring-boot:run

A API iniciará em:

http://localhost:1110

---

## 📌 Endpoints da API

Método	Endpoint	Descrição
GET	/usuarios	Lista todos os usuários
GET	/usuarios/{id}	Busca um usuário por ID
POST	/usuarios	Cria um novo usuário
PUT	/usuarios/{id}	Atualiza um usuário
DELETE	/usuarios/{id}	Remove um usuário

Exemplo JSON (POST/PUT)

{
  "nome": "João Silva",
  "email": "joao@email.com",
}

---

## 🧪 Banco de Dados H2

📍 Acesse o console:

http://localhost:1110/h2-console


📌 Configurações:

JDBC URL: jdbc:h2:mem:usuarios

Usuário: ehl

Senha:

---

## 🧾 Licença

Projeto desenvolvido para estudos e prática de APIs REST com Java e Spring Boot.
