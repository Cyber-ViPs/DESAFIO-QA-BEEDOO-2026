[BUG-01] Descrição: Vulnerabilidade de Stored XSS e falta de validação em campos obrigatórios no cadastro.

Severidade: Crítica (Impacta a segurança da aplicação e a integridade do banco de dados).

Passos para Reproduzir:

  1 -  Acessar a página de "Cadastrar Curso".

  2 - No campo "Nome do Curso", inserir o payload: <img src=x onerror=alert('XSS')>.

  3 - Deixar os campos "Data de Início", "Data de Fim" e "Descrição" vazios.

  4 - Clicar no botão "CADASTRAR CURSO".

  5 - Observar a "Lista de Cursos".

**Resultado Atual:** O sistema exibe um alerta de JavaScript (alert).

**Resultado Esperado:** O sistema deve realizar a sanitização das entradas, impedindo a execução de scripts (XSS).


 ### Evidências
  * [Visualizar Print do Erro](https://drive.google.com/file/d/1YTkF4xqiQeTFsQWT1NCpbAV12rvCNQkQ/view?usp=drive_link)

NOTA:
  "Analisei que a aplicação provavelmente não possui middlewares de validação no back-end (como o Joi ou Zod) e não faz o escape de caracteres especiais no front-end antes de renderizar o HTML, 
permitindo que o navegador interprete strings como código executável."




[BUG-02] Descrição: > "O formulário de cadastro de cursos permite a submissão de dados sem o preenchimento dos campos obrigatórios (Nome, Descrição, Instrutor, Data Inicio e Data Fim, Número de Vagas e Tipo de Curso ), resultando em registros inconsistentes na listagem."

Severidade: Alta (Impacta a integridade dos dados e a experiência do usuário, permitindo registros incompletos no banco de dados)

Passos para Reproduzir:

  1 -  Acessar a página de "Cadastrar Curso".

  2 - Deixar os campos "Nome do Curso", "Descrição", "Instrutor", "Url da Imagem de Capa", "Data de Início e Data de Fim", "Número de Vagas" e "Tipo de Curso"  vazios.

  3 - Clicar no botão "CADASTRAR CURSO".

  4 - Observar a "Lista de Cursos".

**Resultado Atual:** O curso é cadastrado mesmo com campos obrigatórios vazios, gerando um card quebrado na listagem.

**Resultado Esperado:** O sistema deve validar campos obrigatórios e exibir uma mensagem de erro de validação para todos os campos marcados como obrigatórios (*) (ex: "O campo Nome é obrigatório") caso o usuário tente salvar sem preenchê-los.

 ### Evidências
  * [Visualizar Print do Erro](https://drive.google.com/file/d/1s413W0UAqexQQNSsCyogh_Nl8RFfGZ0f/view?usp=drive_link)

NOTA: Até mesmo campos que poderiam ser opcionais, como URL da imagem, não possuem um tratamento para quando estão vazios (ex: exibir imagem padrão)




[BUG-03] Descrição: Ausência de imagem padrão (placeholder) para campos de URL vazios

Severidade: Baixa (Impacto puramente visual na experiência do usuário).

Passos para Reproduzir:

   1 - Acessar a página de "Cadastrar Curso".

   2 - Preencher os campos obrigatórios (quando validados) e deixar o campo "Url da Imagem de Capa" vazio.

   3 - Clicar no botão "CADASTRAR CURSO".

   4 - Observar a "Lista de Cursos".

**Resultado Atual:** O card do curso é renderizado sem imagem, gerando um espaço vazio ou elemento quebrado.

**Resultado Esperado:** O sistema deve exibir automaticamente uma imagem padrão (placeholder) quando o campo de URL estiver vazio, mantendo a padronização visual da interface.

 ### Evidências
  * [Visualizar Print do Erro](https://drive.google.com/file/d/1uRHPaqTiwXSM0k6meixrlXHgKISqGohE/view?usp=drive_link)



[BUG-04] Descrição: Falha de validação lógica no período de datas (Data de Início > Data de Fim)

Severidade: Média (Impacto na integridade das regras de negócio, permitindo períodos de curso inválidos).

Passos para Reproduzir:

   1 - Acessar a página de "Cadastrar Curso".

   2 - No campo "Data de Início", inserir 01/01/2021 e, no campo "Data de Fim", inserir 01/01/2010.

   3 - Clicar no botão "CADASTRAR CURSO".

   4 - Observar a "Lista de Cursos".

**Resultado Atual:** O sistema permite a submissão e salva o registro com o período inconsistente.

**Resultado Esperado:** O sistema deve validar a lógica do período, impedindo o cadastro e exibindo um aviso ao usuário caso a "Data de Início" seja posterior à "Data de Fim".

 ### Evidências
  * [Visualizar Print do Erro](https://drive.google.com/file/d/1itxPnJAMgeAGl2rAX7G9Krls078ZuYVZ/view?usp=drive_link)




[BUG-05] Descrição: O sistema dá uma "falsa sensação de segurança" (o usuário acha que deletou, mas o dado continua lá). Isso é grave, pois o usuário pode acreditar que o curso saiu do catálogo quando, na verdade, ele ainda está lá.

Severidade Média/Alta.

Passos para Reproduzir:
    1 - Ir em Litar Cursos. 
    2 - Clica no Botão [ EXCLUIR CURSO]
    3 - Observar a "Lista de Cursos".

**Resultado Atual:** O sistema não faz a devida exclusão do curso embora mostre que o curso foi excluído com sucesso. Porém a requisição DELETE retorna um Erro 405 (Method Not Allowed), impedindo a exclusão real do registro.

**Resultado Esperado:** O sistema deve estar configurado para aceitar o método DELETE na API, ou o front-end deve tratar o erro 405 exibindo uma mensagem de falha ao usuário, em vez de uma mensagem de sucesso. 


### Evidências
  * [Visualizar Print do Erro](https://drive.google.com/file/d/1Fz484_kzdY5t_t1vVNW9jvyO7x6hWbJx/view?usp=drive_link)



[BUG-06] Descrição: Ausência do botão [editar curso] impossibilitando o usuário editar o curso previamente salvo.

Severidade Média.

Passos para Reproduzir:
    1 - Ir em Litar Cursos. 
    2 - Verificar a interface da 'Lista de Cursos' em busca da funcionalidade de edição.
    3 - Observar a "Lista de Cursos".

**Resultado Atual:** O sistema não da ao usuário final a possibilidade de edição tornando o uso do sistema muito mais lento o forçado a cadastra outro curso no sistema com as devidas correções.

**Resultado Esperado:** O sistema da a capacidade de edição dos curso já existente no sistema poupando de ter que refazer todo o processo de cadastramento novamente.

### Evidências
  * [Visualizar Print do Erro](https://drive.google.com/file/d/1K9LAs6PaTiIcoHU5ZNMesL0JVbHjSmc4/view?usp=drive_link)

