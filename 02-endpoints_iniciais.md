<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Quais endpoints iniciais devo criar para a API de gestão de tarefas e suas URIs?

Para uma API inicial de gestão de tarefas (ToDo List), os endpoints essenciais e suas URIs são:


| Ação | Método HTTP | URI | Descrição |
| :-- | :-- | :-- | :-- |
| Listar todas as tarefas | GET | /todos | Retorna uma lista de tarefas, geralmente paginada |
| Obter tarefa por ID | GET | /todos/{id} | Retorna os detalhes de uma tarefa específica |
| Criar nova tarefa | POST | /todos | Cria uma nova tarefa com dados enviados no corpo |
| Atualizar tarefa | PUT | /todos/{id} | Atualiza todos os dados de uma tarefa existente |
| Deletar tarefa | DELETE | /todos/{id} | Remove uma tarefa específica |

Esses endpoints seguem as melhores práticas REST, utilizando URIs claras e métodos HTTP apropriados para cada operação[^2][^5][^3]. A URI base `/todos` representa o recurso de tarefas, e o identificador `{id}` é usado para operações em tarefas específicas.

<div style="text-align: center">⁂</div>

[^1]: https://www.ibm.com/br-pt/think/topics/api-endpoint

[^2]: https://www.ethereum-blockchain-developer.com/courses/learn-react/todo-list-endpoints

[^3]: https://www.ibm.com/docs/pt-br/SSZQFR_2.3.3.0/psapsys_restapi/jobs.html

[^4]: https://docs.automationanywhere.com/pt-BR/bundle/enterprise-v2019/page/api-task-real-time-endpoint.html

[^5]: https://roadmap.sh/projects/todo-list-api

[^6]: https://apidog.com/pt/blog/rest-api-endpoints-pt/

[^7]: https://www.dotcom-monitor.com/pt-br/aprenda-com-o-dotcom-monitor/o-que-sao-pontos-de-extremidade-de-api-por-que-sao-importantes/

[^8]: https://www.youtube.com/watch?v=1K6EqMKm5wo

[^9]: https://cloud.google.com/application-integration/docs/configure-call-rest-endpoint-task

[^10]: https://apidog.com/pt/blog/api-uri-vs-api-url-pt/

