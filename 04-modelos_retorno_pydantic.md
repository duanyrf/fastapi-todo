<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Quais modelos de resposta devo criar para retornar informações das tarefas com status code adequado?

Para retornar informações das tarefas em uma API de gestão de tarefas, você deve criar modelos de resposta Pydantic que representem os dados essenciais da tarefa e utilizar status codes adequados para cada operação. Veja como estruturar isso:

---

## **Modelos de Resposta Pydantic**

Um modelo típico para retorno de tarefa pode ser:

```python
from pydantic import BaseModel
from typing import Optional, Literal

class TaskResponse(BaseModel):
    id: int
    title: str
    description: Optional[str] = None
    priority: int
    status: Literal["pendente", "em andamento", "concluída"]
```

- **id**: identificador único da tarefa (int)
- **title**: título da tarefa (str)
- **description**: descrição opcional (str)
- **priority**: prioridade da tarefa (int, por exemplo, 1 a 5)
- **status**: status da tarefa, limitado a valores específicos (Literal)

Para retornar uma lista de tarefas, utilize uma lista desse modelo:

```python
from typing import List

tasks: List[TaskResponse]
```


---

## **Status Codes Adequados**

Os principais status codes para operações REST são[^2][^3][^4][^5][^7][^9]:

- **200 OK**: Para retornos de consulta (GET), atualização (PUT/PATCH) e deleção (DELETE) bem-sucedidas, quando há corpo de resposta.
- **201 Created**: Para criação de uma nova tarefa (POST), retornando o objeto criado.
- **204 No Content**: Para deleção bem-sucedida quando não há corpo de resposta.
- **404 Not Found**: Quando a tarefa não existe.
- **400 Bad Request**: Quando os dados enviados são inválidos.

Exemplo de uso no FastAPI:

```python
from fastapi import FastAPI, status

app = FastAPI()

@app.get("/tasks", response_model=List[TaskResponse], status_code=status.HTTP_200_OK)
def list_tasks():
    ...

@app.post("/tasks", response_model=TaskResponse, status_code=status.HTTP_201_CREATED)
def create_task(task: TaskCreate):
    ...

@app.get("/tasks/{task_id}", response_model=TaskResponse, status_code=status.HTTP_200_OK)
def get_task(task_id: int):
    ...
```


---

## **Resumo**

- Crie um modelo de resposta Pydantic que reflita os atributos da tarefa.
- Use status codes adequados para cada operação, conforme as boas práticas REST[^2][^3][^4][^5][^7][^9].
- Defina o modelo de resposta e o status code no decorator do endpoint FastAPI.

Assim, sua API será clara, padronizada e facilitará a integração com outros sistemas.

<div style="text-align: center">⁂</div>

[^1]: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Reference/Status

[^2]: https://www.erudio.com.br/blog/http-status-codes-em-servicos-rest/

[^3]: https://fastapi.tiangolo.com/pt/tutorial/response-status-code/

[^4]: https://fastapi.tiangolo.com/tutorial/response-status-code/

[^5]: https://ninelabs.blog/padrao-de-codigos-de-status-http-em-apis-rest/

[^6]: https://fastapi.tiangolo.com/pt/tutorial/response-model/

[^7]: https://learn.microsoft.com/pt-br/partner-center/developer/referrals-api-response-codes

[^8]: https://fastapi.tiangolo.com/pt/tutorial/handling-errors/

[^9]: https://www.luiztools.com.br/post/http-status-cheat-sheet/

[^10]: https://fastapi.tiangolo.com/pt/advanced/response-change-status-code/

[^11]: https://fastapi.tiangolo.com/pt/advanced/additional-status-codes/

[^12]: https://www.dotcom-monitor.com/wiki/pt-br/knowledge-base/lista-de-codigos-de-status-http-codigos-de-erro-http-explicados/

[^13]: https://pt.stackoverflow.com/questions/361465/para-uma-busca-sem-resultados-a-resposta-http-deve-ser-404-204-ou-200-com-o-co

[^14]: https://www.programicio.com/python/fastapi/fundamentos/enviando-codigos-de-status-http

[^15]: https://kinsta.com/pt/blog/fastapi/

[^16]: https://fastapidozero.dunossauro.com/01/

[^17]: https://repost.aws/pt/knowledge-center/api-gateway-status-codes-rest-api

[^18]: https://apidog.com/pt/blog/understanding-api-response-types-and-formats-a-comprehensive-guide-pt/

[^19]: https://blog.casadodesenvolvedor.com.br/boas-praticas-documentacao-de-api/

[^20]: https://fastapi.tiangolo.com/advanced/response-change-status-code/

