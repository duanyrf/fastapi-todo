<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Como usar códigos 4xx e 5xx para sinalizar erros específicos nas tarefas?

Para sinalizar erros específicos em tarefas usando códigos 4xx e 5xx na sua API, siga estas orientações:

---

## **Códigos 4xx — Erros do Cliente**

Use códigos 4xx quando o erro foi causado por uma solicitação inválida do cliente. Exemplos comuns:

- **400 Bad Request**: Dados de entrada inválidos, campos obrigatórios ausentes ou formato incorreto.
- **401 Unauthorized**: Usuário não autenticado tentando acessar recursos protegidos.
- **403 Forbidden**: Usuário autenticado, mas sem permissão para acessar o recurso.
- **404 Not Found**: Tarefa solicitada não existe.
- **405 Method Not Allowed**: Método HTTP não permitido para o endpoint.
- **409 Conflict**: Tentativa de criar uma tarefa que já existe.
- **422 Unprocessable Entity**: Dados válidos em formato, mas semanticamente incorretos (por exemplo, prioridade fora do intervalo permitido)[^7][^6].

No FastAPI, use a exceção `HTTPException` para retornar esses erros:

```python
from fastapi import HTTPException

# Exemplo: tarefa não encontrada
raise HTTPException(status_code=404, detail="Tarefa não encontrada")
```


---

## **Códigos 5xx — Erros do Servidor**

Use códigos 5xx quando o erro ocorreu no servidor, mesmo que a solicitação do cliente estivesse correta:

- **500 Internal Server Error**: Erro inesperado, bug ou falha de infraestrutura.
- **502 Bad Gateway**: Problema ao se comunicar com outro serviço.
- **503 Service Unavailable**: Servidor indisponível, sobrecarga ou manutenção.
- **504 Gateway Timeout**: Timeout ao aguardar resposta de outro serviço[^1][^2][^6].

No FastAPI, erros não tratados automaticamente resultam em 500. Para personalizar, crie um handler global:

```python
from fastapi import Request
from fastapi.responses import JSONResponse

@app.exception_handler(Exception)
async def global_exception_handler(request: Request, exc: Exception):
    return JSONResponse(
        status_code=500,
        content={"message": "Erro interno do servidor"}
    )
```


---

## **Boas Práticas**

- Sempre forneça uma mensagem detalhada no corpo da resposta, explicando o erro para facilitar o diagnóstico pelo cliente[^3][^8].
- Use cabeçalhos customizados (ex: `X-Error-Code`) para códigos de erro internos, se necessário[^8].
- Diferencie claramente erros do cliente (4xx) e do servidor (5xx) para facilitar a correção e o suporte[^6][^2][^7].

---

**Resumo:**

- Use 4xx para erros causados por solicitações inválidas do cliente (ex: dados incorretos, recurso não encontrado).
- Use 5xx para erros inesperados ou falhas internas do servidor.
- No FastAPI, utilize `HTTPException` para 4xx e handlers globais para 5xx.
- Sempre retorne mensagens claras e, se possível, códigos de erro estruturados no corpo da resposta.

<div style="text-align: center">⁂</div>

[^1]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes

[^2]: https://restcookbook.com/HTTP Methods/400-vs-500/

[^3]: https://guptadeepak.com/comprehensive-guide-to-api-error-code-management/

[^4]: https://fastapi.tiangolo.com/tutorial/handling-errors/

[^5]: https://fastapi.tiangolo.com/reference/exceptions/

[^6]: https://enterprisecraftsmanship.com/posts/rest-api-response-codes-400-vs-500/

[^7]: https://stackoverflow.com/questions/24043019/when-should-an-api-throw-a-4xx-status-code-error-and-when-a-5xx

[^8]: https://betterstack.com/community/guides/scaling-python/error-handling-fastapi/

[^9]: https://fastapi.tiangolo.com/em/tutorial/handling-errors/

[^10]: https://blog.stackademic.com/error-and-exception-handling-in-fastapi-c0949bb42e1b

[^11]: https://restfulapi.net/http-status-codes/

[^12]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status

[^13]: https://developers.pipefy.com/reference/status-and-error-handling

[^14]: https://www.w3.org/Protocols/HTTP/HTRESP.html

[^15]: https://openapi.com/blog/status-codes-rest-api

[^16]: https://fastapi.tiangolo.com/pt/tutorial/handling-errors/

[^17]: https://www.getorchestra.io/guides/fastapi-mastering-error-handling-with-examples

[^18]: https://stackoverflow.com/questions/78649853/fastapi-sql-post-request-receiving-500-error-internal-server-error

[^19]: https://www.youtube.com/watch?v=jYbNq6QAQNI

[^20]: https://stackoverflow.com/questions/72831952/how-do-i-integrate-custom-exception-handling-with-the-fastapi-exception-handling

