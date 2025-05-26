<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# FastAPI ToDo List API

Uma API web simples e robusta para gestão de tarefas (ToDo List), construída com **FastAPI**, **Python 3.13** e gerenciada com **uv** para controle de dependências e ambiente. Este projeto serve como base para aplicações de produtividade, estudos de APIs RESTful e integração com frontends modernos.

---

## Table of Contents

1. **Conheça o Projeto**
  1. [Sobre o Projeto](#sobre-o-projeto)
  2. [Tecnologias Utilizadas](#tecnologias-utilizadas)
  3. [Instalação e Execução](#instalação-e-execução)
  4. [Endpoints da API](#endpoints-da-api)
  5. [Modelos de Dados](#modelos-de-dados)
  6. [Códigos de Status HTTP](#códigos-de-status-http)
  7. [Testes e Documentação Interativa](#testes-e-documentação-interativa)
  8. [Contribuindo](#contribuindo)
  9. [Licença](#licença)

2. [Tutorial Construindo uma API de Gestão de Tarefas com FastAPI, Python 3.13 e uv](01-tutorial.md)

3. **Perguntas Frequentes**
  1. [Quais endpoints iniciais devo criar para a API de gestão de tarefas e suas URIs?](02-endpoints_iniciais.md)
  2. [Como definir os modelos Pydantic para representar tarefas com atributos como título, descrição, prioridade e status?](03-definicao_modelos_pydantic.md)
  3. [Quais modelos de resposta devo criar para retornar informações das tarefas com status code adequado?](04-modelos_retorno_pydantic.md)
  4. [Quais códigos de status são mais adequados para indicar sucesso na resposta de tarefas?](05-codigos_%20status_sucesso.md)
  5. [Como usar códigos 4xx e 5xx para sinalizar erros específicos nas tarefas?](06-codigos_status_erros.md)

---

## Sobre o Projeto

A **FastAPI ToDo List API** permite criar, listar, atualizar e excluir tarefas, com suporte a atributos como título, descrição, prioridade e status. O projeto foi desenhado para ser simples, didático e facilmente extensível, utilizando as melhores práticas REST e validação de dados com Pydantic.

---

## Tecnologias Utilizadas

- **[FastAPI](https://fastapi.tiangolo.com/)** — Framework web moderno para APIs em Python
- **[Python 3.13](https://www.python.org/downloads/)** — Última versão da linguagem Python
- **[uv](https://github.com/astral-sh/uv)** — Gerenciador de dependências e ambientes Python
- **[Pydantic](https://docs.pydantic.dev/)** — Validação e tipagem de dados
- **Swagger UI** — Documentação interativa automática

---

## Instalação e Execução


### Clone o repositório

```bash
git clone https://github.com/seu-usuario/fastapi-todo.git
cd fastapi-todo
```

### Inicialize o ambiente virtual

```bash
uv venv
```

- No MacOS/Linux:

```bash
source .venv/bin/activate
```

- No Windows:

```bash
.venv\Scripts\activate
```
 - Instale as dependências:

 ```bash
uv add fastapi --extra standard
```

### Execute a aplicação

```bash
fastapi dev
```

- Acesse a API em `http://127.0.0.1:8000`.

---

## Endpoints da API

| Método | URI             | Descrição                        | Status Code |
|--------|-----------------|----------------------------------|-------------|
| GET    | /tasks          | Lista todas as tarefas           | 200         |
| GET    | /tasks/{id}     | Detalha uma tarefa específica    | 200/404     |
| POST   | /tasks          | Cria uma nova tarefa             | 201         |
| PUT    | /tasks/{id}     | Atualiza uma tarefa existente    | 200/404     |
| DELETE | /tasks/{id}     | Remove uma tarefa                | 204/404     |

- **Paginação:** Suporte via query strings `skip` e `limit` em `/tasks`.

---

## Modelos de Dados

### TaskCreate (entrada)

```

class TaskCreate(BaseModel):
title: str
description: Optional[str] = None
priority: int
status: Literal["pendente", "em andamento", "concluída"]

```

### Task (resposta)

```

class Task(TaskCreate):
id: str
created_at: datetime

```

---

## Códigos de Status HTTP

- **200 OK**: Sucesso em consultas e atualizações.
- **201 Created**: Tarefa criada com sucesso.
- **204 No Content**: Tarefa excluída com sucesso.
- **400 Bad Request**: Dados inválidos.
- **404 Not Found**: Tarefa não encontrada.
- **422 Unprocessable Entity**: Dados semanticamente incorretos.
- **500 Internal Server Error**: Erro inesperado no servidor.

---

## Testes e Documentação Interativa

Acesse a documentação interativa em:

- [Swagger UI](http://127.0.0.1:8000/docs)
- [ReDoc](http://127.0.0.1:8000/redoc)

Você pode testar todos os endpoints diretamente pelo navegador.

---

## Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.

---

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

---
```

