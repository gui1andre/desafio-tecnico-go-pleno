# 🚀 Desafio Técnico — Backend Go (Nível Pleno)

## 📦 Desafio: API de Gestão de Pedidos

Desenvolva uma **API RESTful** para gerenciamento de pedidos de uma loja virtual, utilizando **Go** como linguagem principal.

---

## 📋 Contexto

Uma loja virtual precisa de um sistema para gerenciar seus **clientes**, **produtos** e **pedidos**. Sua missão é construir a API que suporte essas operações de forma robusta, escalável e bem estruturada.

---

## ✅ Requisitos Funcionais

### Clientes
- `POST /customers` — Criar um novo cliente
- `GET /customers/:id` — Buscar cliente por ID
- `PUT /customers/:id` — Atualizar dados do cliente
- `DELETE /customers/:id` — Remover cliente

### Produtos
- `POST /products` — Criar um novo produto (nome, descrição, preço, estoque)
- `GET /products` — Listar produtos (com paginação)
- `GET /products/:id` — Buscar produto por ID
- `PUT /products/:id` — Atualizar produto
- `DELETE /products/:id` — Remover produto

### Pedidos
- `POST /orders` — Criar um pedido (associado a um cliente, com um ou mais produtos e quantidades)
- `GET /orders/:id` — Buscar pedido por ID (com detalhes dos itens)
- `GET /orders` — Listar pedidos (com filtro por status e paginação)
- `PATCH /orders/:id/status` — Atualizar status do pedido (`pending`, `confirmed`, `shipped`, `delivered`, `cancelled`)

---

## ⚙️ Requisitos Técnicos

### Obrigatórios
- Linguagem: **Go 1.21+**
- Banco de dados relacional: **PostgreSQL** (via Docker Compose)
- Uso de **migrations** para versionamento do schema
- Arquitetura em camadas: separação clara entre `handler`, `service` e `repository`
- Validação de entrada nos handlers
- Tratamento de erros consistente com respostas HTTP adequadas
- **Testes unitários** para a camada de serviço (mínimo 70% de cobertura)
- `Dockerfile` e `docker-compose.yml` para subir o ambiente completo

### Diferenciais (não obrigatórios, mas valorizados)
- Autenticação via **JWT**
- Cache de listagem de produtos com **Redis**
- Uso de **mensageria** (ex: RabbitMQ ou Kafka) para emitir eventos ao mudar status do pedido
- **Tracing/Observabilidade** (ex: OpenTelemetry)
- Documentação da API com **Swagger/OpenAPI**
- Testes de integração

---

## 🏗️ Regras de Negócio

1. Não é permitido criar um pedido para um cliente inexistente.
2. Não é permitido adicionar ao pedido um produto com estoque insuficiente.
3. Ao confirmar um pedido (`confirmed`), o estoque dos produtos deve ser decrementado atomicamente.
4. Um pedido `cancelled` ou `delivered` não pode ter seu status alterado novamente.
5. O valor total do pedido deve ser calculado automaticamente com base nos itens e quantidades.

---

## 📁 Estrutura Sugerida

```
.
├── cmd/
│   └── api/
│       └── main.go
├── internal/
│   ├── domain/          # entidades e interfaces
│   ├── handler/         # camada HTTP
│   ├── service/         # regras de negócio
│   └── repository/      # acesso ao banco de dados
├── migrations/
├── docker-compose.yml
├── Dockerfile
└── README.md
```

---

## 📬 Entrega

- Suba o código neste repositório com histórico de commits organizado.
- Inclua um `README` de execução explicando como rodar o projeto localmente.
- O projeto deve subir completamente com `docker-compose up`.

---

## 🧪 Critérios de Avaliação

| Critério | Peso |
|---|---|
| Organização e arquitetura do código | Alto |
| Cobertura e qualidade dos testes | Alto |
| Aderência às regras de negócio | Alto |
| Tratamento de erros e validações | Médio |
| Clareza do README e facilidade de execução | Médio |
| Diferenciais implementados | Bônus |

---

> **Tempo estimado:** 4–8 horas  
> **Nível:** Pleno
