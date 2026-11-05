# API REST de Cadastro de Usuários

![Java](https://img.shields.io/badge/Java-25-red)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.8-brightgreen)
![Maven](https://img.shields.io/badge/Build-Maven-blue)
![H2](https://img.shields.io/badge/Database-H2-yellow)

API REST para gerenciamento de usuários (CRUD), desenvolvida com Java e Spring Boot, organizada em camadas e com persistência via Spring Data JPA.

## Objetivo e contexto

Projeto acadêmico e de estudo, criado para desenvolver competências em back-end: construção de APIs REST, organização em camadas, orientação a objetos e persistência de dados com JPA.

## Funcionalidades

- Criar usuários
- Listar todos os usuários
- Buscar usuário por ID
- Atualizar dados de um usuário
- Excluir usuários
- Console web do H2 habilitado para inspeção do banco

## Arquitetura e organização do código

A aplicação segue o padrão em camadas, em que cada camada tem uma responsabilidade única:

```
Cliente HTTP
     │
     ▼
Controller   (UsuarioController)  → recebe as requisições HTTP e devolve as respostas
     │
     ▼
Service      (UsuarioService)     → concentra as regras de negócio
     │
     ▼
Repository   (UsuarioRepository)  → acesso ao banco via Spring Data JPA
     │
     ▼
Entity       (Usuario)            → modelo mapeado para a tabela
     │
     ▼
H2 Database (em memória)
```

## Tecnologias e decisões técnicas

| Tecnologia | Uso | Motivo da escolha |
|---|---|---|
| Java 25 / Spring Boot 3.5.8 | Base da aplicação | Stack amplamente usada em back-end corporativo |
| Spring Web | Endpoints REST | Exposição das operações do CRUD via HTTP |
| Spring Data JPA | Persistência | Reduz o código de acesso a dados e abstrai o SQL |
| H2 (em memória) | Banco de dados | Não exige instalação nem configuração; ambiente limpo a cada execução (`ddl-auto=create-drop`) |
| Lombok | Redução de código repetitivo | Evita getters, setters e construtores escritos manualmente |
| Maven (com Maven Wrapper) | Build | O `mvnw` dispensa a instalação prévia do Maven |

**Trade-off:** como o H2 roda em memória, os dados são perdidos ao encerrar a aplicação. Isso é adequado para estudo e demonstração, mas não para uso real.

## Como executar

**Pré-requisitos:** JDK 25 (versão definida no `pom.xml`) e Git.

```bash
git clone https://github.com/EnzoHayashi/CRUD-JAVA-SPRINGBOOT.git
cd CRUD-JAVA-SPRINGBOOT
./mvnw spring-boot:run
```

No Windows (PowerShell ou CMD), usar `mvnw.cmd spring-boot:run`.

A API fica disponível em `http://localhost:1110`.

### Configuração principal (`application.properties`)

| Propriedade | Valor |
|---|---|
| `server.port` | `1110` |
| `spring.datasource.url` | `jdbc:h2:mem:usuarios` |
| `spring.jpa.hibernate.ddl-auto` | `create-drop` |
| `spring.h2.console.path` | `/h2-console` |

## Endpoints

| Método | Endpoint | Descrição |
|---|---|---|
| `GET` | `/usuarios` | Lista todos os usuários |
| `GET` | `/usuarios/{id}` | Busca um usuário por ID |
| `POST` | `/usuarios` | Cria um novo usuário |
| `PUT` | `/usuarios/{id}` | Atualiza um usuário |
| `DELETE` | `/usuarios/{id}` | Remove um usuário |

## Exemplos de utilização

Criar um usuário:

```bash
curl -X POST http://localhost:1110/usuarios \
  -H "Content-Type: application/json" \
  -d '{"nome": "João Silva", "email": "joao@email.com"}'
```

Listar usuários:

```bash
curl http://localhost:1110/usuarios
```

Atualizar um usuário:

```bash
curl -X PUT http://localhost:1110/usuarios/1 \
  -H "Content-Type: application/json" \
  -d '{"nome": "João da Silva", "email": "joao@email.com"}'
```

Excluir um usuário:

```bash
curl -X DELETE http://localhost:1110/usuarios/1
```

### Console do H2

Com a aplicação em execução, acessar `http://localhost:1110/h2-console` e usar:

- **JDBC URL:** `jdbc:h2:mem:usuarios`
- **Usuário:** `ehl`
- **Senha:** (vazia)

> Credenciais restritas ao ambiente de desenvolvimento local.

<!-- Evidências: adicionar prints do Postman e do console H2 em docs/ e referenciar aqui.
![Criação de usuário](docs/post-usuario.png) -->

## Desafios e aprendizados

- Estruturação de um projeto Spring Boot em camadas (controller, service, repository e entity).
- Mapeamento de entidades com JPA/Hibernate e uso do H2 em memória.
- Teste manual dos endpoints REST com Postman e inspeção dos dados pelo console do H2.

## Melhorias futuras

- Validação de entrada com Bean Validation (`@Valid`, `@NotBlank`, `@Email`).
- Tratamento centralizado de exceções com respostas HTTP padronizadas (`@ControllerAdvice`).
- Uso de DTOs para separar o contrato da API do modelo de dados.
- Testes automatizados (JUnit e MockMvc) para o service e o controller.
- Documentação interativa da API com Swagger/OpenAPI.
- Troca do H2 por um banco persistente (PostgreSQL ou MySQL), com perfis de configuração por ambiente.
