<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

## Tutorial: Construindo uma API de Gestão de Tarefas (ToDo List) com FastAPI, Python 3.13 e uv

Este tutorial mostra como criar uma API Web de tarefas usando FastAPI, Python 3.13 e uv para gerenciamento de dependências. Abordaremos desde a documentação inicial até a implementação dos endpoints e testes via Swagger.

---

## **1. Estrutura do Projeto e Gerenciamento com uv**

- Crie o diretório do projeto:

```bash
mkdir fastapi-todo && cd fastapi-todo
```

- Inicialize o projeto com `uv`:

```bash
uv init --app
```

- Adicione FastAPI como dependência:

```bash
uv add fastapi --extra standard
```

- Estrutura sugerida:

```
fastapi-todo/
├── pyproject.toml
└── app/
    └── main.py
```

- Para rodar o projeto:

```bash
uv run fastapi dev
```

Isso gerencia dependências, cria o ambiente virtual e executa a aplicação[^5].

---

## **2. Documentação Inicial da API**

| Endpoint | Método | URI | Descrição | Dados de Entrada | Retorno Esperado | Status Code |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Listar tarefas | GET | /tasks | Lista todas as tarefas | Query: skip, limit (opcional) | Lista de tarefas | 200 |
| Obter tarefa por ID | GET | /tasks/{task_id} | Detalha uma tarefa específica | Parâmetro de URL: task_id | Tarefa | 200 |
| Criar nova tarefa | POST | /tasks | Cria uma nova tarefa | Corpo: título, descrição, status | Tarefa criada | 201 |
| Atualizar tarefa | PUT | /tasks/{task_id} | Atualiza uma tarefa existente | Parâmetro de URL: task_id, corpo | Tarefa atualizada | 200 |
| Deletar tarefa | DELETE | /tasks/{task_id} | Remove uma tarefa | Parâmetro de URL: task_id | Mensagem de sucesso | 204 |


---

## **3. Modelos de Dados Pydantic**

Vamos definir os modelos para entrada e saída de dados:

```python
from pydantic import BaseModel
from typing import Optional
from datetime import datetime

class TaskCreate(BaseModel):
    title: str
    description: Optional[str] = None
    completed: bool = False

class Task(TaskCreate):
    id: str
    created_at: datetime
```

- `title`: str — título da tarefa
- `description`: Optional[str] — descrição opcional
- `completed`: bool — status de conclusão
- `id`: str — identificador único
- `created_at`: datetime — data de criação[^2]

---

## **4. Implementação dos Endpoints**

No arquivo `app/main.py`:

```python
from fastapi import FastAPI, HTTPException, Query, Path, status
from typing import List, Optional
from uuid import uuid4
from datetime import datetime

from pydantic import BaseModel

class TaskCreate(BaseModel):
    title: str
    description: Optional[str] = None
    completed: bool = False

class Task(TaskCreate):
    id: str
    created_at: datetime

app = FastAPI(
    title="API de Tarefas",
    description="API para gestão de tarefas a fazer",
    version="0.1.0"
)

# Simulação de banco de dados em memória
tasks_db = {}

@app.get("/tasks", response_model=List[Task], status_code=status.HTTP_200_OK)
def list_tasks(skip: int = Query(0, ge=0), limit: int = Query(10, gt=0)):
    """
    Lista tarefas com paginação via query string.
    """
    tasks = list(tasks_db.values())
    return tasks[skip: skip + limit]

@app.get("/tasks/{task_id}", response_model=Task, status_code=status.HTTP_200_OK)
def get_task(task_id: str = Path(...)):
    """
    Busca uma tarefa pelo ID via parâmetro de URL.
    """
    task = tasks_db.get(task_id)
    if not task:
        raise HTTPException(status_code=404, detail="Tarefa não encontrada")
    return task

@app.post("/tasks", response_model=Task, status_code=status.HTTP_201_CREATED)
def create_task(task: TaskCreate):
    """
    Cria uma nova tarefa via corpo da requisição.
    """
    task_id = str(uuid4())
    new_task = Task(id=task_id, created_at=datetime.utcnow(), **task.dict())
    tasks_db[task_id] = new_task
    return new_task

@app.put("/tasks/{task_id}", response_model=Task, status_code=status.HTTP_200_OK)
def update_task(task_id: str, task: TaskCreate):
    """
    Atualiza uma tarefa existente.
    """
    stored_task = tasks_db.get(task_id)
    if not stored_task:
        raise HTTPException(status_code=404, detail="Tarefa não encontrada")
    updated_task = Task(id=task_id, created_at=stored_task.created_at, **task.dict())
    tasks_db[task_id] = updated_task
    return updated_task

@app.delete("/tasks/{task_id}", status_code=status.HTTP_204_NO_CONTENT)
def delete_task(task_id: str):
    """
    Remove uma tarefa.
    """
    if task_id in tasks_db:
        del tasks_db[task_id]
    else:
        raise HTTPException(status_code=404, detail="Tarefa não encontrada")
```

- **Query strings**: `skip`, `limit` em `/tasks` para paginação[^3].
- **Parâmetro de URL**: `task_id` em `/tasks/{task_id}`.
- **Corpo da requisição**: Modelo `TaskCreate` em POST/PUT.
- **Modelos de resposta**: Definidos via `response_model` nos decorators.
- **Status code**: Definidos via `status_code` nos decorators[^4].

---

## **5. Testando com Swagger**

Ao rodar a aplicação, acesse:

```
http://127.0.0.1:8000/docs
```

- O Swagger UI será gerado automaticamente, permitindo testar todos os endpoints, visualizar modelos de entrada e saída e status codes esperados[^4].

---

## **Resumo**

- **uv** gerencia dependências e execução do projeto[^5].
- **FastAPI** facilita a criação de endpoints REST, validação automática e documentação interativa.
- **Pydantic** garante dados tipados e validados.
- **Swagger** é gerado automaticamente para testes e documentação.

Com isso, você tem uma API de tarefas pronta para evoluir!

<div style="text-align: center">⁂</div>

[^1]: https://betterstack.com/community/guides/scaling-python/introduction-to-fastapi/

[^2]: https://dev.to/jamesbmour/part-2-building-a-todo-api-with-fastapi-step-by-step-guide-3042

[^3]: https://www.oneloop.ai/blog/understanding-query-params-headers-and-body-params-in-fastapi-when-to-use-each

[^4]: https://stackoverflow.com/questions/62705219/in-pythons-fastapi-autogenerated-openapi-swagger-documentation-page-how-can-i

[^5]: https://docs.astral.sh/uv/guides/integration/fastapi/

[^6]: https://fastapi.tiangolo.com/tutorial/body-nested-models/

[^7]: https://docs.astral.sh/uv/guides/integration/aws-lambda/

[^8]: https://fastapi.tiangolo.com/tutorial/

[^9]: https://betterstack.com/community/guides/scaling-python/pdm-explained/

[^10]: https://fastapi.tiangolo.com/release-notes/

