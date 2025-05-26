<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Como definir os modelos Pydantic para representar tarefas com atributos como título, descrição, prioridade e status

Você pode definir os modelos Pydantic para representar uma tarefa com os atributos título, descrição, prioridade e status da seguinte forma:

```python
from pydantic import BaseModel, Field
from typing import Optional, Literal

class Task(BaseModel):
    title: str = Field(..., description="Título da tarefa")
    description: Optional[str] = Field(None, description="Descrição detalhada da tarefa")
    priority: int = Field(..., ge=1, le=5, description="Prioridade da tarefa (1 a 5)")
    status: Literal["pendente", "em andamento", "concluída"] = Field(..., description="Status da tarefa")
```

- **title**: obrigatório, tipo `str`, representa o título da tarefa.
- **description**: opcional, tipo `str`, permite uma descrição detalhada.
- **priority**: obrigatório, tipo `int`, pode ser validado para aceitar apenas valores de 1 a 5 (por exemplo, usando o parâmetro `ge` e `le` do `Field`)[^1][^3][^5].
- **status**: obrigatório, tipo `Literal`, restringe os valores permitidos para "pendente", "em andamento" ou "concluída", garantindo maior segurança e clareza na API[^5].

Você pode usar o recurso `Field` do Pydantic para adicionar validações, descrições e exemplos aos campos, o que melhora a documentação automática da API[^1][^3].

Esse modelo pode ser utilizado tanto para entrada (criação/atualização) quanto para resposta, conforme a necessidade dos endpoints[^2][^5].

<div style="text-align: center">⁂</div>

[^1]: https://pythonacademy.com.br/blog/pydantic-e-tipos-avancados

[^2]: https://fastapi.tiangolo.com/pt/tutorial/response-model/

[^3]: https://pythonacademy.com.br/blog/introducao-ao-pydantic-validacao-e-modelagem-de-dados-simplificada-com-python

[^4]: https://giovannireisnunes.wordpress.com/2022/08/26/usando-o-pydantic-parte-1/

[^5]: https://fastapi.tiangolo.com/pt/python-types/

[^6]: https://www.youtube.com/watch?v=UdfLu1G47BU

[^7]: https://docs.pydantic.dev/1.10/usage/models/

