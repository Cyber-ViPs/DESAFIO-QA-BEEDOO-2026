# DESAFIO-QA-BEEDOO-2026

Repositório destinado ao desafio técnico para a vaga de QA Junior na Beedoo. Este projeto contém o planejamento, execução e reporte de testes do módulo de cadastro e listagem de cursos.

## 🔗 Links Úteis
* 📑 [Planilha de Casos de Teste (Google Sheets)](_LINK)
* 📸 [Evidências de Teste (Google Drive)](C_LINK)

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
* **Validação de Regras de Negócio:** Campos obrigatórios e lógica de datas (Início < Fim).
* **Consistência de Dados:** Garantir que o que é enviado via API é refletido corretamente na interface.

---

## 🛠️ Metodologia e Ferramentas
* **Proxy de Interceptação:** Uso do **Burp Suite** para validar vulnerabilidades no Back-end e análise de requisições JSON.
* **Escrita de Testes:** Metodologia BDD com **Gherkin** para clareza de cenários.
* **Análise Técnica:** Inspeção de console e tráfego de rede via Chrome DevTools.

---

## 🧠 Raciocínio de Teste (Tomada de Decisão)
Durante o processo, optei por uma abordagem de **Exploratory Testing** (Testes Exploratórios) focada em segurança. Ao identificar que o sistema aceitava tags HTML, utilizei payloads de **Stored XSS** para validar o nível de proteção da aplicação.

Como suporte, utilizei Inteligência Artificial para estruturar os cenários de teste em Gherkin, garantindo que a documentação seguisse padrões de mercado, adaptando cada cenário à realidade da aplicação Beedoo.
