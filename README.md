# DESAFIO-QA-BEEDOO-2026

Repositório destinado ao desafio técnico para a vaga de QA Junior na Beedoo. Este projeto contém o planejamento, execução e reporte de testes do módulo de cadastro e listagem de cursos.

## 🔗 Links Úteis
* 📑 [Planilha de Casos de Teste (Google Sheets)](https://docs.google.com/spreadsheets/d/1i9TfLWUStx_cEQRWvclmrPvYJf3d-rd0sZQmlaM4_B8/edit?gid=0#gid=0)

* 📸 [Evidências de Teste (Google Drive)](https://drive.google.com/drive/folders/1uyLMuJq5qik9FHZIM2Ei1fwQGMQEZyqU?hl=pt-br)
 
* 🐞 [Relatório Detalhado de Bugs (Bugs.md)](./Bugs.md)
---

## 🧐 1. Análise Inicial da Aplicação

### Objetivo da Aplicação
O sistema visa gerenciar o catálogo de treinamentos da Beedoo, permitindo o registro e a consulta de cursos disponíveis. É uma peça fundamental para a organização da trilha de conhecimento dos usuários.

### Principais Fluxos
1. **Cadastro de Cursos:** Inclusão de novos registros via formulário (Nome, Imagem, Data, Descrição).
2. **Listagem Dinâmica:** Visualização dos cursos ativos em formato de cards.
3. **Exclusão de Cursos:** Remoção de itens do catálogo.

### Pontos Críticos Identificados
* **Sanitização de Inputs:** Verificação de vulnerabilidades de Segurança (XSS).
* **Validação de Regras de Negócio:** Campos obrigatórios e lógica de datas.
* **Integridade de Ações:** Falhas nas operações de CRUD. Identificado erro 405 Method Not Allowed na requisição DELETE, impedindo a exclusão real do registro e gerando mensagens falsas de sucesso na interface.
* **Consistência de Dados:** Garantir que o que é enviado via API é refletido corretamente na interface.

**Nota de Observação: Durante os testes, foram identificados comportamentos sistêmicos na validação de formulários. Os principais achados incluem:**

[BUG-01] Vulnerabilidade de segurança (XSS).

[BUG-02] Falta de validação de obrigatoriedade de campos.

[BUG-03] Ausência de tratamento visual (placeholder) para imagens.

[BUG-04] Falha na validação lógica de períodos (datas).

[BUG-05] Falha na funcionalidade de exclusão de cursos.

[BUG-06] Ausência ou inoperância da funcionalidade de edição de cursos.
---

## 🛡️ Resultados de Testes de Segurança e Integração

Análise de Tráfego: Confirmado o uso do método POST para envio de dados, evitando a exposição de parâmetros na URL.

Validação de API: Identificada falha de permissão no servidor (405 Method Not Allowed) durante a tentativa de exclusão de registros via método DELETE.

Integridade de Dados: Confirmada a ausência de sanitização de inputs, resultando em vulnerabilidade de Stored XSS.
---

## 🛠️ Metodologia e Ferramentas
* **Proxy de Interceptação:** Uso do **Burp Suite** para validar vulnerabilidades no Back-end e análise de requisições JSON.
* **Escrita de Testes:** Metodologia BDD com **Gherkin** para clareza de cenários.
* **Análise Técnica:** Inspeção de console e tráfego de rede via Chrome DevTools.
---

### Cenário: Validar vulnerabilidade de XSS no cadastro
**Dado** que o usuário acessa o formulário de cadastro de curso
**Quando** insere um payload malicioso `<script>alert('XSS')</script>` no campo Nome
**E** submete o formulário
**Então** o sistema deve sanitizar o input, armazenando apenas o texto literal
**E** não deve executar o script no navegador ao listar o curso.

### Cenário: Tentativa de cadastro com campos vazios
**Dado** que o usuário está na tela de cadastro
**Quando** clica em "CADASTRAR CURSO" sem preencher os campos obrigatórios
**Então** o sistema deve exibir mensagens de erro informando a obrigatoriedade dos campos
**E** não deve permitir a criação do registro.

### Cenário: Cadastro de curso com sucesso (Caminho Feliz)
**Dado** que o usuário preenche todos os campos do formulário com dados válidos
**Quando** clica no botão "CADASTRAR CURSO"
**Então** o sistema deve salvar o registro com sucesso
**E** exibir o card do curso corretamente na listagem.


## 🧠 Raciocínio de Teste (Tomada de Decisão)
Durante o processo, optei por uma abordagem de **Exploratory Testing** (Testes Exploratórios) focada em segurança. Ao identificar que o sistema aceitava tags HTML, utilizei payloads de **Stored XSS** para validar o nível de proteção da aplicação.

"Documentação técnica estruturada com auxílio de IA para alinhamento aos padrões de mercado (BDD/Gherkin e boas práticas de QA)."
