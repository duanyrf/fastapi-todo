<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Quais códigos de status são mais adequados para indicar sucesso na resposta de tarefas

Os códigos de status mais adequados para indicar sucesso na resposta de tarefas em uma API REST são:

- **200 OK**: Utilizado quando a requisição foi bem-sucedida e o servidor retorna o conteúdo solicitado, como em consultas (GET), atualizações (PUT/PATCH) e deleções com retorno de conteúdo (DELETE)[^1][^2][^3][^4][^6].
- **201 Created**: Utilizado quando uma nova tarefa é criada com sucesso (POST). Indica que o recurso foi criado e normalmente retorna o objeto criado no corpo da resposta[^1][^2][^3][^4][^6].
- **204 No Content**: Utilizado quando uma tarefa é removida com sucesso (DELETE) e não há conteúdo a ser retornado no corpo da resposta[^4][^5][^6].

Esses códigos seguem as melhores práticas HTTP para indicar operações bem-sucedidas em APIs de gestão de tarefas.

<div style="text-align: center">⁂</div>

[^1]: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Reference/Status

[^2]: https://www.hostinger.com.br/tutoriais/https-status

[^3]: https://www.dotcom-monitor.com/wiki/pt-br/knowledge-base/lista-de-codigos-de-status-http-codigos-de-erro-http-explicados/

[^4]: https://www.luiztools.com.br/post/http-status-cheat-sheet/

[^5]: https://kinsta.com/pt/blog/lista-codigos-status-http/

[^6]: https://www.homehost.com.br/blog/internet/status-http-o-que-sao-codigos-de-resposta/

[^7]: https://www.hostgator.com.br/blog/http-status-code-como-resolver/

[^8]: https://www.devmedia.com.br/http-status-code/41222

[^9]: https://docs.digitalmanager.guru/developers/codigos-http-das-respostas

