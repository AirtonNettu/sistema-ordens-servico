# 09 — Planejamento do MVP e Organização do Desenvolvimento

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Documento:** Planejamento do Produto Mínimo Viável (MVP)  
**Versão:** 1.0 — Proposta inicial  
**Status:** Aguardando revisão e aprovação

**Documentos de referência:**
- `01-visao-do-projeto.md`
- `02-levantamento-requisitos.md`
- `03-requisitos.md`
- `04-regras-de-negocio.md`
- `05-historias-usuario.md`
- `06-casos-de-uso.md`
- `07-prototipos.md`
- `08-decisoes-tecnicas.md`

---

## 1. Objetivo

Este documento apresenta uma proposta de planejamento para o desenvolvimento incremental do Sistema de Ordens de Serviço para Assistência Técnica.

Seu objetivo é definir:

- O escopo inicial do MVP.
- As funcionalidades prioritárias.
- A sequência de implementação.
- As dependências entre entregas.
- A organização do Product Backlog.
- O fluxo de desenvolvimento com Git e GitHub.
- Os critérios para iniciar e concluir tarefas.
- A estratégia inicial de testes e validação.

O planejamento poderá ser atualizado conforme o projeto evoluir.

---

# 2. Definição do MVP

MVP significa *Minimum Viable Product*, ou Produto Mínimo Viável.

Para este projeto, o MVP deverá representar a menor versão do sistema capaz de executar um fluxo real de atendimento da assistência técnica, respeitando as regras de negócio essenciais.

A proposta é permitir que um usuário autorizado consiga:

1. Acessar o sistema.
2. Cadastrar ou localizar um cliente.
3. Cadastrar ou localizar um equipamento.
4. Abrir uma ordem de serviço.
5. Registrar o diagnóstico.
6. Elaborar um orçamento.
7. Registrar a aprovação ou recusa.
8. Acompanhar o atendimento.
9. Registrar o pagamento integral devido.
10. Confirmar a retirada do equipamento.
11. Encerrar a ordem de serviço.
12. Consultar o histórico do atendimento.

**Resultado esperado:** um atendimento poderá ser registrado e acompanhado do recebimento à entrega, sem depender de controles paralelos para suas informações principais.

---

# 3. Estratégia de Priorização

Será utilizada uma adaptação do método MoSCoW.

| Prioridade | Significado |
|---|---|
| Must Have | Essencial para o MVP |
| Should Have | Importante, mas pode ser entregue depois |
| Could Have | Desejável, caso exista capacidade |
| Won't Have Now | Fora do MVP inicial |

As prioridades abaixo são propostas e ainda precisam ser validadas.

## 3.1 Must Have — Essencial

- Autenticação inicial.
- Cadastro e pesquisa de clientes.
- Cadastro individual de equipamentos.
- Identificadores únicos.
- Abertura de ordens de serviço.
- Consulta e atualização de estados.
- Registro de diagnóstico.
- Elaboração de orçamento.
- Aprovação ou recusa de orçamento.
- Cálculo correto dos valores.
- Registro de pagamento integral.
- Encerramento condicionado à quitação e retirada.
- Consulta do histórico de atendimentos.

## 3.2 Should Have — Importante

- Cancelamento de OS, após refinamento das regras.
- Cadastro e controle de peças.
- Movimentações de estoque.
- Comprovante de recebimento em PDF.
- Dashboard operacional.
- Controle de permissões mais detalhado.

**Observação:** autenticação e autorização mínima são obrigatórias desde o início. A classificação acima se refere ao refinamento de permissões administrativas adicionais.

## 3.3 Could Have — Desejável

- Registro fotográfico.
- Impressão de etiquetas de equipamentos.
- Indicadores financeiros avançados.
- Filtros e pesquisas adicionais.
- Melhorias visuais e personalização.

## 3.4 Won't Have Now — Fora do MVP

- Gestão de múltiplas empresas.
- Portal de clientes.
- Portal próprio para técnicos.
- Gateway de pagamentos.
- Confirmação bancária automática.
- Aplicativo móvel nativo.
- Integrações externas não essenciais.

A distribuição como aplicativo Windows separado será avaliada após a escolha da estratégia técnica.

---

# 4. Estratégia de Desenvolvimento Incremental

O sistema será desenvolvido em pequenos incrementos funcionais.

Cada incremento deverá entregar funcionalidades verificáveis e preservar a estabilidade das partes já implementadas.

A ordem proposta é:

| Incremento | Objetivo |
|---|---|
| 0 | Preparar o projeto |
| 1 | Implementar clientes e equipamentos |
| 2 | Implementar ordens de serviço |
| 3 | Implementar diagnóstico e orçamento |
| 4 | Implementar pagamentos e encerramento |
| 5 | Consolidar e validar o MVP |

Funcionalidades adicionais serão planejadas após a validação do fluxo principal.

---

# 5. Incremento 0 — Preparação do Projeto

## Objetivo

Estabelecer uma base técnica e organizacional para o desenvolvimento.

## Atividades propostas

### 5.1 Revisar documentação

- Verificar consistência entre requisitos e regras.
- Revisar histórias de usuário.
- Identificar decisões bloqueantes.
- Confirmar o escopo inicial do MVP.

### 5.2 Aprovar decisões técnicas

- Escolher a linguagem backend.
- Escolher o framework backend.
- Escolher a tecnologia frontend.
- Escolher o banco de dados.
- Definir a arquitetura inicial.
- Definir a estratégia de execução local.

### 5.3 Organizar o repositório

- Revisar a estrutura do projeto.
- Configurar o `.gitignore`.
- Atualizar o `README.md`.
- Definir convenções de branches e commits.
- Preparar o ambiente de desenvolvimento.

### 5.4 Preparar qualidade

- Escolher ferramentas de testes.
- Definir comandos de execução.
- Definir validações automatizadas iniciais.
- Estabelecer a Definition of Done.

## Critérios de conclusão

O incremento estará concluído quando:

- As decisões técnicas necessárias estiverem registradas.
- O ambiente de desenvolvimento estiver funcional.
- O repositório estiver organizado.
- O projeto puder ser executado localmente.
- Os testes iniciais puderem ser executados.

**Entrega:** base técnica pronta para o desenvolvimento.

---

# 6. Incremento 1 — Clientes e Equipamentos

## Objetivo

Permitir o cadastro e a consulta das entidades necessárias à abertura de atendimentos.

## Histórias relacionadas

- US-004 — Cadastrar cliente.
- US-005 — Pesquisar cliente.
- US-006 — Reutilizar cadastro.
- US-007 — Cadastrar equipamento.
- US-008 — Identificar equipamento sem número de série.
- US-009 — Consultar histórico do equipamento.

## Funcionalidades

### Clientes

- Cadastrar cliente.
- Validar telefone obrigatório.
- Pesquisar por nome ou telefone.
- Selecionar cliente existente.

### Equipamentos

- Cadastrar equipamento.
- Vincular equipamento ao cliente.
- Gerar código interno único.
- Registrar número de série quando disponível.
- Consultar equipamentos.

O histórico de manutenção será progressivamente preenchido nos incrementos seguintes, quando as ordens de serviço forem implementadas.

## Critérios de conclusão

- Clientes podem ser cadastrados e localizados.
- Equipamentos podem ser cadastrados individualmente.
- Equipamentos possuem identificadores únicos.
- Um cliente pode possuir vários equipamentos.
- Os testes das regras principais são aprovados.

**Entrega:** módulo de clientes e equipamentos funcional.

---

# 7. Incremento 2 — Ordens de Serviço

## Objetivo

Permitir a abertura e o acompanhamento de atendimentos.

## Histórias relacionadas

- US-010 — Abrir OS.
- US-011 — Acompanhar andamento.
- US-012 — Consultar ordens por estado.

## Funcionalidades

- Criar OS.
- Selecionar cliente.
- Selecionar equipamento.
- Registrar defeito relatado.
- Registrar data de entrada.
- Gerar número único.
- Criar OS com estado Aberto.
- Consultar ordens.
- Atualizar estados permitidos.
- Filtrar ordens por estado.

## Dependências

- Incremento 1 concluído.
- Regras mínimas de transição de estados definidas.

## Critérios de conclusão

- Uma OS pode ser aberta com cliente e equipamento existentes.
- Cada OS recebe número único.
- A OS inicia no estado Aberto.
- As consultas retornam os atendimentos registrados.
- Transições inválidas são rejeitadas.
- Os testes principais são aprovados.

**Entrega:** módulo básico de ordens de serviço funcional.

---

# 8. Incremento 3 — Diagnóstico e Orçamento

## Objetivo

Permitir registrar a análise técnica e a decisão do cliente sobre o reparo.

## Histórias relacionadas

- US-015 — Registrar diagnóstico.
- US-016 — Elaborar orçamento.
- US-017 — Registrar aprovação ou recusa.

## Funcionalidades

- Registrar diagnóstico.
- Criar orçamento.
- Adicionar serviços e valores.
- Calcular total.
- Aplicar política de diagnóstico.
- Registrar aprovação.
- Registrar recusa.
- Preservar histórico do orçamento.

## Regras críticas

- Diagnóstico padrão de R$ 50,00.
- Diagnóstico devido em caso de recusa.
- Diagnóstico incluído na mão de obra quando o reparo for aprovado.
- Proibição de cobrança duplicada.
- Reparo condicionado à aprovação.

## Critérios de conclusão

- Diagnósticos podem ser registrados.
- Orçamentos são calculados corretamente.
- A aprovação é registrada.
- A recusa é registrada.
- O diagnóstico não é cobrado duas vezes.
- Os testes financeiros básicos são aprovados.

**Entrega:** fluxo de diagnóstico e orçamento funcional.

---

# 9. Incremento 4 — Pagamentos e Encerramento

## Objetivo

Permitir finalizar o atendimento conforme as regras financeiras da assistência.

## Histórias relacionadas

- US-013 — Encerrar OS.
- US-018 — Registrar pagamento integral.
- US-019 — Consultar histórico financeiro.

## Funcionalidades

- Consultar valor devido.
- Registrar pagamento manual.
- Registrar forma de pagamento.
- Impedir pagamento parcial.
- Atualizar situação financeira.
- Confirmar retirada do equipamento.
- Registrar data de saída.
- Encerrar OS.
- Consultar histórico financeiro.

## Regras críticas

- Pagamento na retirada.
- Pagamento integral.
- Ausência de adiantamentos.
- Encerramento condicionado à quitação.
- Encerramento condicionado à retirada.
- Distinção entre Concluído e Encerrado.

## Dependências

- Incremento 2 concluído.
- Incremento 3 concluído.
- Definição mínima para registro de pagamentos em criptomoedas, caso essa modalidade integre a entrega.

## Critérios de conclusão

- Pagamentos integrais podem ser registrados.
- Pagamentos parciais são rejeitados.
- OS com saldo pendente não pode ser encerrada.
- OS sem confirmação de retirada não pode ser encerrada.
- A data de saída é registrada.
- O histórico permanece disponível.
- Os testes principais são aprovados.

**Entrega:** fluxo principal de atendimento completo.

---

# 10. Incremento 5 — Consolidação do MVP

## Objetivo

Validar o funcionamento integrado das funcionalidades implementadas.

## Atividades

### 10.1 Testes de integração

Verificar a comunicação entre:

- Clientes.
- Equipamentos.
- Ordens de serviço.
- Diagnósticos.
- Orçamentos.
- Pagamentos.

### 10.2 Testes de fluxo completo

Executar cenários de atendimento desde o cadastro até o encerramento.

### 10.3 Validação de regras

Confirmar que:

- Identificadores não são reutilizados.
- Diagnóstico não é cobrado duas vezes.
- Pagamentos parciais são rejeitados.
- Encerramento exige quitação e retirada.
- Históricos são preservados.

### 10.4 Revisão da interface

Avaliar:

- Clareza dos formulários.
- Navegação.
- Mensagens de erro.
- Apresentação dos estados.
- Facilidade de consulta.

### 10.5 Documentação

- Atualizar o README.
- Registrar instruções de execução.
- Documentar configurações necessárias.
- Revisar ADRs.
- Registrar limitações conhecidas.

## Critérios de conclusão

- Fluxo principal validado.
- Testes essenciais aprovados.
- Nenhuma falha crítica conhecida impedindo o uso do MVP.
- Documentação atualizada.
- Versão integrada e identificada no Git.

**Entrega:** primeira versão funcional do MVP.

---

# 11. Funcionalidades Posteriores ao MVP

Após a validação do fluxo principal, poderão ser planejados incrementos adicionais.

## 11.1 Estoque

- Cadastro de peças.
- Controle de quantidades.
- Associação de peças às OS.
- Movimentações.
- Devolução de peças não utilizadas.

## 11.2 Documentos

- Comprovante de recebimento em PDF.
- Reemissão.
- Melhorias no modelo de documento.

## 11.3 Fotografias

- Anexos.
- Classificação.
- Consulta de histórico.
- Controle de armazenamento.

## 11.4 Dashboard

- Indicadores operacionais.
- Consultas por estado.
- Atualização das contagens.
- Informações financeiras, quando aprovadas.

## 11.5 Administração

- Cadastro de funcionários.
- Matriz detalhada de permissões.
- Configurações administrativas.

## 11.6 Cancelamento

- Definição das condições de cancelamento.
- Tratamento financeiro.
- Preservação do histórico.
- Atualização dos indicadores.
- Tratamento de peças vinculadas.

A sequência dessas entregas dependerá das necessidades identificadas após a validação do MVP.

---

# 12. Organização do Product Backlog

O Product Backlog reunirá todas as histórias e tarefas previstas para o produto.

Cada item deverá possuir, quando aplicável:

- Identificador.
- Título.
- Descrição.
- Objetivo.
- Prioridade.
- Critérios de aceitação.
- Dependências.
- Estado.
- Referências aos requisitos e regras.

## Exemplo

**Identificador:** US-010

**Título:** Criar ordem de serviço.

**Objetivo:** permitir registrar o recebimento de um equipamento.

**Critérios de aceitação:**

- Cliente selecionado.
- Equipamento selecionado.
- Defeito relatado registrado.
- Número único gerado.
- Estado inicial Aberto.

**Dependências:** cadastro de clientes e equipamentos.

**Prioridade proposta:** Must Have.

---

# 13. Organização das GitHub Issues

O GitHub Issues será utilizado para acompanhar o trabalho.

## 13.1 Tipos de Issues

**Feature**

Implementação de uma nova funcionalidade.

**Bug**

Correção de comportamento incorreto.

**Documentation**

Criação ou atualização de documentação.

**Refactor**

Melhoria da estrutura interna sem alteração intencional de comportamento.

**Test**

Criação ou melhoria de testes.

**Chore**

Atividades de manutenção, configuração ou infraestrutura do projeto.

## 13.2 Exemplo de Issue

### [US-004] Implementar cadastro de clientes

**Descrição**

Como gerente, quero cadastrar clientes para registrar seus dados e vinculá-los aos atendimentos.

**Critérios de aceitação**

- [ ] Permitir informar nome.
- [ ] Exigir telefone.
- [ ] Validar dados obrigatórios.
- [ ] Persistir o cadastro.
- [ ] Permitir consultar o cliente cadastrado.
- [ ] Criar testes para as regras implementadas.

**Referências**

- RF-004.
- RN-001.
- US-004.
- UC-002.

**Dependências**

- Ambiente inicial configurado.
- Persistência de dados disponível.

**Labels propostas**

- `feature`
- `backend`
- `frontend`

A divisão em uma ou mais Issues será realizada durante o refinamento.

---

# 14. GitHub Project — Kanban

Será proposta a utilização de um quadro Kanban no GitHub Projects.

## Colunas iniciais

### Backlog

Itens identificados, mas ainda não selecionados para execução.

### Ready

Itens refinados, priorizados e prontos para desenvolvimento.

### In Progress

Itens em desenvolvimento.

### In Review

Itens aguardando revisão, testes ou aprovação de Pull Request.

### Done

Itens concluídos conforme a Definition of Done.

## Regras propostas

- Evitar iniciar várias tarefas simultaneamente.
- Não mover uma Issue para Done apenas porque o código foi escrito.
- Manter as Issues relacionadas aos Pull Requests.
- Registrar bloqueios e dependências.
- Atualizar o quadro conforme o trabalho avançar.

---

# 15. Estratégia de Branches

A estratégia proposta é utilizar branches de curta duração para desenvolver funcionalidades e corrigir problemas.

## Branch principal

`main`

Contém a versão integrada do projeto.

## Padrões sugeridos

| Tipo | Exemplo |
|---|---|
| Funcionalidade | `feature/client-registration` |
| Correção | `fix/order-status-validation` |
| Documentação | `docs/update-requirements` |
| Testes | `test/payment-rules` |
| Refatoração | `refactor/order-service` |
| Configuração | `chore/project-setup` |

## Fluxo

1. Selecionar uma Issue.
2. Criar uma branch a partir da base atualizada.
3. Implementar a tarefa.
4. Executar os testes.
5. Revisar as alterações.
6. Criar commits.
7. Enviar a branch ao GitHub.
8. Abrir um Pull Request.
9. Revisar e integrar.

A estratégia será adaptada às necessidades de um projeto desenvolvido inicialmente por uma pessoa.

---

# 16. Convenção de Commits

Será proposta uma convenção baseada em Conventional Commits.

| Prefixo | Utilização |
|---|---|
| `feat` | Nova funcionalidade |
| `fix` | Correção de erro |
| `docs` | Documentação |
| `test` | Testes |
| `refactor` | Refatoração |
| `chore` | Manutenção e configuração |

## Exemplos

```text
docs: add initial software requirements

feat: implement client registration

test: add client validation tests

fix: prevent closing unpaid service orders

refactor: extract order status validation
```

Os commits deverão representar alterações coerentes e possuir mensagens compreensíveis.

---

# 17. Fluxo de Pull Request

Cada Pull Request deverá apresentar informações suficientes para facilitar a revisão.

## Modelo proposto

### Título

`feat: implement client registration`

### Descrição

Implementa o cadastro de clientes conforme a história US-004.

### Alterações

- Formulário de cadastro.
- Validação de telefone obrigatório.
- Persistência dos dados.
- Testes.

### Critérios de validação

- [ ] Requisitos atendidos.
- [ ] Testes executados.
- [ ] Regras de negócio verificadas.
- [ ] Documentação atualizada quando necessário.
- [ ] Alterações revisadas.

### Referências

Issue relacionada e identificadores dos requisitos.

O PR deverá ser integrado somente após a verificação dos critérios definidos para o projeto.

---

# 18. Definition of Ready (DoR)

Uma tarefa estará pronta para desenvolvimento quando:

- Seu objetivo estiver claro.
- Seus critérios de aceitação forem verificáveis.
- As regras de negócio aplicáveis estiverem definidas.
- Suas dependências forem conhecidas.
- O escopo estiver suficientemente delimitado.
- As decisões técnicas necessárias estiverem disponíveis.
- Não existirem bloqueios críticos conhecidos.

Uma tarefa não deverá ser iniciada apenas porque possui um título no backlog.

---

# 19. Definition of Done (DoD)

Uma tarefa será considerada concluída quando:

- O comportamento implementado atender aos critérios de aceitação.
- As regras de negócio forem respeitadas.
- Os testes aplicáveis forem aprovados.
- O código for revisado.
- Não existirem falhas críticas conhecidas relacionadas à entrega.
- A documentação afetada estiver atualizada.
- As alterações estiverem registradas em commits.
- O Pull Request tiver sido integrado à branch de destino.
- A Issue e o quadro Kanban estiverem atualizados.

Esses critérios poderão ser refinados conforme a maturidade do projeto evoluir.

---

# 20. Estratégia de Testes

O projeto deverá utilizar testes proporcionais à criticidade das funcionalidades.

## 20.1 Testes unitários

Priorizar regras como:

- Telefone obrigatório.
- Identificadores únicos.
- Cálculo de orçamento.
- Cobrança de diagnóstico.
- Pagamento integral.
- Condições de encerramento.

## 20.2 Testes de integração

Validar operações que envolvem persistência e relacionamento de dados.

Exemplos:

- Cadastrar cliente e equipamento.
- Criar OS vinculada ao equipamento.
- Registrar orçamento.
- Registrar pagamento.
- Encerrar atendimento.

## 20.3 Testes de interface

Validar os fluxos principais realizados pelo usuário.

## 20.4 Testes de regressão

Após alterações importantes, executar os testes existentes para identificar possíveis regressões.

## 20.5 Evidências

Os Pull Requests poderão registrar:

- Comandos executados.
- Resultado dos testes.
- Capturas de tela, quando relevantes.
- Limitações conhecidas.

---

# 21. Integração Contínua — Proposta

Após a escolha da stack, poderá ser configurado um workflow de GitHub Actions.

O objetivo será executar verificações automáticas em Pull Requests.

Verificações candidatas:

- Instalação de dependências.
- Análise estática.
- Formatação.
- Testes automatizados.
- Verificação de build.

A configuração deverá ser proporcional ao estágio do projeto.

Não será necessário implantar uma infraestrutura complexa de CI/CD antes de existir uma aplicação funcional.

---

# 22. Gestão de Riscos

| Risco | Consequência | Tratamento |
|---|---|---|
| Escopo excessivo | Atraso na entrega | Priorizar MVP |
| Escolhas técnicas precipitadas | Retrabalho | Avaliar e registrar ADRs |
| Histórias grandes demais | Dificuldade de execução | Dividir em tarefas menores |
| Regras de negócio indefinidas | Implementação incorreta | Refinar antes de codificar |
| Ausência de testes | Regressões | Testar regras críticas |
| Falta de commits | Perda de rastreabilidade | Commits frequentes e coerentes |
| Documentação desatualizada | Inconsistência | Atualizar junto às mudanças |
| Muitas tarefas simultâneas | Perda de foco | Limitar trabalho em andamento |

---

# 23. Critérios de Aceitação do MVP

O MVP poderá ser considerado funcional quando:

1. Um usuário autorizado conseguir acessar o sistema.
2. Um cliente puder ser cadastrado e localizado.
3. Um equipamento puder ser cadastrado e identificado.
4. Uma OS puder ser aberta com número único.
5. O diagnóstico puder ser registrado.
6. O orçamento puder ser calculado.
7. A aprovação ou recusa puder ser registrada.
8. O valor devido respeitar as regras do diagnóstico.
9. Um pagamento integral puder ser registrado.
10. Pagamentos parciais forem rejeitados.
11. Uma OS com saldo pendente não puder ser encerrada.
12. Uma OS sem retirada confirmada não puder ser encerrada.
13. Uma OS quitada e retirada puder ser encerrada.
14. O histórico do atendimento permanecer disponível.
15. Os testes essenciais estiverem aprovados.

Esses critérios representam a proposta inicial de validação do MVP.

---

# 24. Plano de Execução Imediato

Após a revisão e aprovação deste documento, a sequência proposta será:

### Etapa A — Consolidar a documentação

Revisar os documentos 01 a 09 e corrigir eventuais inconsistências.

### Etapa B — Registrar a documentação no Git

Verificar alterações, criar commits coerentes e integrar a branch de documentação.

### Etapa C — Definir a stack

Avaliar as alternativas e registrar as decisões nos ADRs.

### Etapa D — Organizar o GitHub

Criar as primeiras Issues e preparar o quadro Kanban.

### Etapa E — Preparar o ambiente

Configurar o projeto, dependências, testes e estrutura inicial.

### Etapa F — Desenvolver o primeiro incremento

Iniciar pelas funcionalidades de clientes e equipamentos, conforme a priorização aprovada.

---

# 25. Controle de Evolução

Este planejamento deverá ser atualizado quando ocorrerem mudanças relevantes em:

- Escopo do MVP.
- Prioridades.
- Dependências.
- Decisões técnicas.
- Critérios de aceitação.
- Estratégia de testes.
- Organização do desenvolvimento.

As alterações deverão ser registradas no Git.

Quando uma mudança afetar decisões arquiteturais, o ADR correspondente deverá ser revisado.

---

# 26. Encerramento

Este documento apresenta uma proposta de planejamento incremental para o desenvolvimento do Sistema de Ordens de Serviço para Assistência Técnica.

O planejamento organiza o trabalho em seis incrementos, do preparo do ambiente à validação do fluxo principal.

Também estabelece uma proposta de utilização de:

- Product Backlog.
- GitHub Issues.
- GitHub Projects.
- Kanban.
- Branches.
- Commits.
- Pull Requests.
- Testes automatizados.
- Definition of Ready.
- Definition of Done.

**Status final:** planejamento inicial elaborado, aguardando aprovação.

