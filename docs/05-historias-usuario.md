# 05 — Histórias de Usuário e Critérios de Aceitação

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Documento:** Histórias de Usuário — Product Backlog Inicial  
**Versão:** 1.0  
**Status:** Elaborado — aguardando refinamento e priorização

**Documentos de referência:**
- `01-visao-do-projeto.md`
- `02-levantamento-requisitos.md`
- `03-requisitos.md`
- `04-regras-de-negocio.md`

---

## 1. Objetivo

Este documento apresenta as histórias de usuário identificadas para o Sistema de Ordens de Serviço para Assistência Técnica.

As histórias representam necessidades dos usuários e serão utilizadas para orientar o planejamento, a implementação e a validação das funcionalidades.

Cada história contém:

- Identificador único.
- Perfil de usuário.
- Necessidade.
- Benefício esperado.
- Critérios de aceitação.
- Referências aos requisitos funcionais e às regras de negócio.

As histórias representam o backlog inicial do produto. Sua presença neste documento não significa que todas serão implementadas no MVP.

---

## 2. Convenções

### 2.1 Identificadores

As histórias utilizarão o formato:

`US-001`, `US-002`, `US-003` etc.

US significa *User Story*.

### 2.2 Estrutura

**Como** [perfil de usuário],  
**quero** [funcionalidade],  
**para** [benefício esperado].

### 2.3 Critérios de aceitação

Os critérios serão descritos preferencialmente no formato:

**Dado que** [contexto],  
**quando** [ação],  
**então** [resultado esperado].

Esse formato facilita a elaboração de testes e a validação das funcionalidades.

### 2.4 Estado das histórias

As histórias poderão apresentar os seguintes estados:

- **Pronta para refinamento:** necessidade identificada, mas ainda exige detalhamento.
- **Candidata ao desenvolvimento:** possui critérios iniciais, mas depende de priorização.
- **Bloqueada por decisão:** exige definição de regra de negócio antes da implementação.

A condição de uma história estar documentada não significa que ela esteja pronta para iniciar o desenvolvimento.

---

# 3. Épico 01 — Autenticação e Usuários

## US-001 — Autenticar usuário

**Como** usuário interno da assistência,  
**quero** acessar o sistema mediante autenticação,  
**para** utilizar somente as funcionalidades autorizadas.

**Critérios de aceitação:**

1. Dado que o usuário não está autenticado, quando tentar acessar uma funcionalidade interna, então o sistema deverá exigir autenticação.
2. Dado que o usuário forneceu credenciais válidas, quando a autenticação for concluída, então o sistema deverá permitir o acesso conforme seu perfil.
3. Dado que a autenticação falhou, quando o usuário tentar acessar uma funcionalidade protegida, então o acesso deverá ser negado.

**Referências:** RF-001, RNF-001, RN-045.  
**Estado:** Candidata ao desenvolvimento.

---

## US-002 — Controlar permissões

**Como** responsável pela assistência,  
**quero** que os usuários tenham permissões conforme seus perfis,  
**para** impedir operações não autorizadas.

**Critérios de aceitação:**

1. Dado que um usuário está autenticado, quando solicitar uma operação, então o sistema deverá verificar suas permissões.
2. Dado que o usuário não possui autorização, quando tentar executar a operação, então o sistema deverá impedir sua execução.
3. Dado que o usuário possui autorização, quando solicitar a operação, então o sistema poderá prosseguir.

**Referências:** RF-002, RNF-002, RN-046.  
**Estado:** Bloqueada por decisão.

**Pendência:** definir a matriz completa de permissões.

---

## US-003 — Cadastrar funcionários

**Como** usuário do RH,  
**quero** cadastrar funcionários,  
**para** manter suas informações administrativas organizadas.

**Critérios de aceitação:**

1. Dado que o RH possui autorização, quando informar os dados obrigatórios de um funcionário, então o sistema deverá permitir o cadastro.
2. Dado que um campo obrigatório não foi preenchido, quando tentar salvar, então o sistema deverá impedir a conclusão do cadastro.
3. Dado que o funcionário está cadastrado, quando for consultado, então suas informações deverão estar disponíveis ao usuário autorizado.

**Referências:** RF-003.  
**Estado:** Bloqueada por decisão.

**Pendência:** definir campos obrigatórios e permissões administrativas.

---

# 4. Épico 02 — Gestão de Clientes

## US-004 — Cadastrar cliente

**Como** gerente,  
**quero** cadastrar clientes,  
**para** registrar seus dados de contato e vinculá-los aos atendimentos.

**Critérios de aceitação:**

1. Dado que o gerente informou os dados obrigatórios, quando salvar o cadastro, então o cliente deverá ser registrado.
2. Dado que o telefone não foi informado, quando tentar salvar, então o sistema deverá impedir o cadastro.
3. Dado que o cliente foi cadastrado, quando realizar uma consulta, então seu registro deverá estar disponível.

**Referências:** RF-004, RN-001.  
**Estado:** Candidata ao desenvolvimento.

---

## US-005 — Pesquisar cliente

**Como** gerente,  
**quero** pesquisar clientes pelo nome ou telefone,  
**para** localizar rapidamente seus cadastros.

**Critérios de aceitação:**

1. Dado que existe um cliente cadastrado, quando pesquisar pelo nome, então o sistema deverá apresentar os registros correspondentes.
2. Dado que existe um cliente cadastrado, quando pesquisar pelo telefone, então o sistema deverá permitir localizá-lo.
3. Dado que não existem resultados, quando a pesquisa for concluída, então o sistema deverá informar que nenhum cliente foi encontrado.

**Referências:** RF-005.  
**Estado:** Candidata ao desenvolvimento.

---

## US-006 — Reutilizar cadastro de cliente

**Como** gerente,  
**quero** selecionar um cliente já cadastrado ao abrir uma nova OS,  
**para** evitar preencher novamente seus dados.

**Critérios de aceitação:**

1. Dado que o cliente já está cadastrado, quando uma nova OS for criada, então o gerente poderá selecioná-lo.
2. Dado que o cliente foi selecionado, quando a OS for salva, então ela deverá permanecer vinculada ao cadastro existente.
3. Dado que o cliente possui atendimentos anteriores, quando consultar seu histórico, então as ordens anteriores deverão continuar disponíveis.

**Referências:** RF-006, RF-007, RN-002, RN-003.  
**Estado:** Candidata ao desenvolvimento.

---

# 5. Épico 03 — Gestão de Equipamentos

## US-007 — Cadastrar equipamento

**Como** gerente,  
**quero** cadastrar cada equipamento individualmente,  
**para** evitar confusões entre computadores e notebooks recebidos.

**Critérios de aceitação:**

1. Dado que o gerente informa os dados necessários, quando salvar o equipamento, então o sistema deverá criar um cadastro individual.
2. Dado que dois equipamentos possuem marca e modelo iguais, quando forem cadastrados, então deverão receber identificadores internos diferentes.
3. Dado que o equipamento foi cadastrado, quando for consultado, então deverá estar associado ao cliente correspondente.

**Referências:** RF-009, RF-010, RF-013, RN-005, RN-006, RN-008.  
**Estado:** Candidata ao desenvolvimento.

---

## US-008 — Identificar equipamento sem número de série

**Como** gerente,  
**quero** utilizar um código interno para identificar computadores sem número de série geral de fábrica,  
**para** manter seu controle individual.

**Critérios de aceitação:**

1. Dado que o equipamento não possui número de série geral de fábrica, quando for cadastrado, então o sistema deverá gerar um código interno único.
2. Dado que o código foi atribuído, quando o equipamento for consultado, então sua identificação deverá estar disponível.
3. Dado que um código já pertence a outro equipamento, quando um novo cadastro for realizado, então o sistema não poderá reutilizá-lo.

**Referências:** RF-010, RF-011, RN-006, RN-007.  
**Estado:** Candidata ao desenvolvimento.

---

## US-009 — Consultar histórico do equipamento

**Como** gerente,  
**quero** visualizar todas as manutenções anteriores de um equipamento,  
**para** compreender seu histórico técnico.

**Critérios de aceitação:**

1. Dado que o equipamento possui ordens anteriores, quando consultar seu histórico, então o sistema deverá apresentá-las.
2. Dado que uma OS anterior está encerrada ou cancelada, quando consultar o histórico, então ela deverá continuar disponível.
3. Dado que uma OS foi selecionada no histórico, quando abrir seus detalhes, então deverão ser apresentados os registros disponíveis do atendimento.

**Referências:** RF-015, RN-009.  
**Estado:** Candidata ao desenvolvimento.

---

# 6. Épico 04 — Ordens de Serviço

## US-010 — Abrir ordem de serviço

**Como** gerente,  
**quero** abrir uma ordem de serviço vinculada a um cliente e equipamento,  
**para** registrar o atendimento realizado.

**Critérios de aceitação:**

1. Dado que cliente e equipamento estão cadastrados, quando o gerente abrir uma OS, então poderá associá-los ao atendimento.
2. Dado que os dados obrigatórios foram preenchidos, quando salvar, então o sistema deverá criar a OS.
3. Dado que a OS foi criada, então deverá receber um número único gerado automaticamente.
4. Dado que a OS foi registrada, então seu estado inicial deverá ser Aberto.

**Referências:** RF-016, RF-017, RN-010, RN-011, RN-012.  
**Estado:** Candidata ao desenvolvimento.

---

## US-011 — Acompanhar andamento da OS

**Como** gerente,  
**quero** visualizar e atualizar o estado das ordens de serviço,  
**para** acompanhar o andamento dos atendimentos.

**Critérios de aceitação:**

1. Dado que uma OS existe, quando for consultada, então seu estado atual deverá ser exibido.
2. Dado que o usuário possui autorização, quando solicitar uma transição permitida, então o sistema deverá atualizar o estado.
3. Dado que uma transição não é permitida, quando for solicitada, então o sistema deverá impedir a alteração.

**Referências:** RF-019, RF-020, RN-012, RN-015.  
**Estado:** Bloqueada por decisão.

**Pendência:** definir todas as transições permitidas.

---

## US-012 — Consultar ordens por estado

**Como** gerente,  
**quero** visualizar as ordens separadas por situação,  
**para** identificar rapidamente os atendimentos que exigem acompanhamento.

**Critérios de aceitação:**

1. Dado que existem ordens concluídas, quando consultar essa categoria, então o sistema deverá apresentá-las.
2. Dado que existem ordens encerradas, quando consultar essa categoria, então elas deverão aparecer separadamente.
3. Dado que existem ordens canceladas, quando consultar o histórico de cancelamentos, então elas deverão estar disponíveis.

**Referências:** RF-018, RF-021, RF-055, RN-013.  
**Estado:** Candidata ao desenvolvimento.

---

## US-013 — Encerrar ordem de serviço

**Como** gerente,  
**quero** encerrar uma OS após a retirada do equipamento e a quitação do valor devido,  
**para** finalizar corretamente o atendimento.

**Critérios de aceitação:**

1. Dado que o equipamento ainda não foi retirado, quando tentar encerrar a OS, então o sistema deverá impedir o encerramento.
2. Dado que existe saldo financeiro pendente, quando tentar encerrar a OS, então o sistema deverá impedir a operação.
3. Dado que a retirada foi confirmada e o pagamento integral registrado, quando encerrar a OS, então seu estado deverá ser atualizado para Encerrado.
4. Dado que a OS foi encerrada, então a data de saída deverá ser registrada.

**Referências:** RF-022, RF-036, RN-013, RN-014, RN-024.  
**Estado:** Candidata ao desenvolvimento.

---

## US-014 — Cancelar ordem de serviço

**Como** gerente,  
**quero** cancelar atendimentos sem apagar seus registros,  
**para** manter o histórico e atualizar os indicadores operacionais.

**Critérios de aceitação:**

1. Dado que uma OS atende às condições de cancelamento, quando for cancelada, então seu estado deverá ser Cancelado.
2. Dado que a OS foi cancelada, então seu número original deverá ser preservado.
3. Dado que a OS foi cancelada, então deverá permanecer disponível no histórico.
4. Dado que uma OS ativa foi cancelada, então a contagem de ordens ativas deverá ser atualizada.

**Referências:** RF-023, RF-053, RF-054, RN-030 a RN-033.  
**Estado:** Bloqueada por decisão.

**Pendência:** definir as condições de cancelamento e o tratamento financeiro.

---

# 7. Épico 05 — Diagnósticos e Orçamentos

## US-015 — Registrar diagnóstico técnico

**Como** gerente,  
**quero** registrar o diagnóstico de um equipamento,  
**para** documentar os problemas identificados.

**Critérios de aceitação:**

1. Dado que existe uma OS, quando o diagnóstico for registrado, então suas informações deverão permanecer associadas ao atendimento.
2. Dado que o orçamento for recusado e não houver outros serviços autorizados, então o valor devido pelo diagnóstico deverá ser de R$ 50,00.
3. Dado que o reparo for aprovado, então a cobrança do diagnóstico deverá respeitar sua inclusão na mão de obra.

**Referências:** RF-024, RF-030, RN-016 a RN-018.  
**Estado:** Candidata ao desenvolvimento.

---

## US-016 — Elaborar orçamento

**Como** gerente,  
**quero** elaborar orçamentos discriminados,  
**para** apresentar ao cliente os serviços e seus respectivos valores.

**Critérios de aceitação:**

1. Dado que existe uma OS, quando o gerente criar um orçamento, então poderá adicionar serviços com descrição e valor.
2. Dado que existem itens no orçamento, quando seus valores forem registrados, então o sistema deverá calcular o total.
3. Dado que a mão de obra inclui o diagnóstico, quando o total for calculado, então o diagnóstico não poderá ser somado novamente.

**Referências:** RF-025, RF-026, RF-027, RN-018, RN-019.  
**Estado:** Candidata ao desenvolvimento.

---

## US-017 — Registrar aprovação ou recusa

**Como** gerente,  
**quero** registrar a decisão do cliente sobre o orçamento,  
**para** acompanhar somente os serviços autorizados.

**Critérios de aceitação:**

1. Dado que o cliente aprovou o orçamento, quando a aprovação for registrada, então o sistema deverá permitir o prosseguimento do reparo.
2. Dado que o cliente recusou o orçamento, quando a recusa for registrada, então a OS deverá indicar Orçamento recusado.
3. Dado que o orçamento foi recusado, então o reparo não deverá ser registrado como executado.
4. Dado que o orçamento foi recusado, então suas informações deverão permanecer no histórico.

**Referências:** RF-028, RF-029, RN-020, RN-021.  
**Estado:** Candidata ao desenvolvimento.

---

# 8. Épico 06 — Gestão Financeira

## US-018 — Registrar pagamento integral

**Como** gerente ou usuário do RH,  
**quero** registrar o pagamento integral de uma OS,  
**para** manter o controle financeiro do atendimento.

**Critérios de aceitação:**

1. Dado que existe um valor devido, quando o pagamento integral for registrado, então o sistema deverá associá-lo à OS.
2. Dado que o valor informado é inferior ao total devido, quando tentar registrar o pagamento, então o sistema deverá rejeitar o pagamento parcial.
3. Dado que o pagamento foi registrado, então o histórico financeiro deverá ser atualizado.
4. Dado que o pagamento foi realizado, então a forma de pagamento deverá ser registrada.

**Referências:** RF-031 a RF-035, RF-037, RN-022, RN-023, RN-025, RN-026.  
**Estado:** Candidata ao desenvolvimento.

---

## US-019 — Consultar histórico financeiro

**Como** gerente ou usuário do RH autorizado,  
**quero** consultar os pagamentos registrados,  
**para** acompanhar os recebimentos da assistência.

**Critérios de aceitação:**

1. Dado que existem pagamentos registrados, quando consultar o histórico financeiro, então o sistema deverá apresentá-los.
2. Dado que um pagamento está associado a uma OS, quando seus detalhes forem consultados, então a referência à OS deverá estar disponível.
3. Dado que o usuário não possui autorização para consultar informações financeiras, quando tentar acessá-las, então o sistema deverá impedir o acesso.

**Referências:** RF-002, RF-034, RN-025, RN-047.  
**Estado:** Candidata ao desenvolvimento, sujeita à definição de permissões.

---

# 9. Épico 07 — Controle de Estoque

## US-020 — Cadastrar e consultar peças

**Como** gerente,  
**quero** cadastrar peças e consultar suas quantidades,  
**para** acompanhar os materiais disponíveis na assistência.

**Critérios de aceitação:**

1. Dado que uma peça foi cadastrada, quando consultar o estoque, então ela deverá aparecer na listagem.
2. Dado que uma peça possui quantidade registrada, quando consultar seus detalhes, então a quantidade disponível deverá ser apresentada.

**Referências:** RF-038, RF-039, RN-034.  
**Estado:** Candidata ao desenvolvimento.

---

## US-021 — Associar peça à OS

**Como** gerente,  
**quero** registrar peças utilizadas ou destinadas a uma ordem de serviço,  
**para** manter o controle dos materiais do atendimento.

**Critérios de aceitação:**

1. Dado que uma peça pertence ao estoque da assistência, quando for retirada para uma OS, então a quantidade disponível deverá ser atualizada.
2. Dado que uma peça foi fornecida pelo cliente, quando for registrada na OS, então não deverá reduzir o estoque da empresa.
3. Dado que uma peça foi fornecida pelo cliente, então seu valor não deverá ser cobrado como peça da assistência.
4. Dado que ocorreu uma movimentação, então ela deverá permanecer registrada.

**Referências:** RF-040 a RF-042, RF-044, RN-035, RN-036, RN-040.  
**Estado:** Candidata ao desenvolvimento.

---

## US-022 — Devolver peça não utilizada

**Como** gerente,  
**quero** devolver ao estoque peças não utilizadas em atendimentos cancelados,  
**para** manter a quantidade disponível correta.

**Critérios de aceitação:**

1. Dado que uma peça foi retirada do estoque e não foi utilizada, quando sua devolução for confirmada, então a quantidade disponível deverá ser atualizada.
2. Dado que uma peça foi instalada, danificada ou consumida, então ela não deverá retornar automaticamente ao estoque disponível.
3. Dado que a devolução foi realizada, então a movimentação deverá permanecer registrada.

**Referências:** RF-043, RF-044, RN-037 a RN-040.  
**Estado:** Bloqueada por decisão.

**Pendência:** definir o procedimento de confirmação de utilização.

---

# 10. Épico 08 — Fotografias e Documentos

## US-023 — Anexar fotografias

**Como** gerente,  
**quero** anexar fotografias à ordem de serviço,  
**para** documentar as condições do equipamento.

**Critérios de aceitação:**

1. Dado que existe uma OS, quando uma fotografia válida for anexada, então ela deverá ficar associada ao atendimento.
2. Dado que existem fotografias do recebimento e do período posterior à manutenção, então o sistema deverá permitir distingui-las.
3. Dado que a OS foi encerrada, quando consultar seu histórico, então as fotografias deverão continuar disponíveis.

**Referências:** RF-045 a RF-047, RN-041, RN-042.  
**Estado:** Candidata ao desenvolvimento, sujeita à definição de limites de arquivos.

---

## US-024 — Gerar comprovante de recebimento

**Como** gerente,  
**quero** gerar um comprovante de recebimento em PDF,  
**para** fornecer ao cliente um registro formal da entrega do equipamento.

**Critérios de aceitação:**

1. Dado que uma OS foi criada, quando o gerente solicitar o comprovante, então o sistema deverá gerar um PDF.
2. Dado que o PDF foi gerado, então deverá conter os dados obrigatórios definidos na RN-043.
3. Dado que existe uma OS registrada, quando o gerente solicitar novamente o comprovante, então o sistema deverá permitir sua reemissão.
4. Dado que o PDF está disponível, então poderá ser obtido para impressão ou compartilhamento manual.

**Referências:** RF-048 a RF-051, RN-043, RN-044.  
**Estado:** Candidata ao desenvolvimento.

---

# 11. Épico 09 — Dashboard Operacional

## US-025 — Visualizar indicadores de atendimento

**Como** gerente,  
**quero** visualizar indicadores das ordens de serviço,  
**para** acompanhar a situação operacional da assistência.

**Critérios de aceitação:**

1. Dado que existem ordens cadastradas, quando o painel for consultado, então o sistema deverá apresentar seus indicadores.
2. Dado que uma OS ativa foi cancelada, quando os indicadores forem atualizados, então ela não deverá ser contabilizada entre as ordens ativas.
3. Dado que uma OS mudou de estado, quando o painel for atualizado, então os indicadores deverão refletir sua situação atual.

**Referências:** RF-052 a RF-055, RN-032.  
**Estado:** Candidata ao desenvolvimento.

---

# 12. Backlog Inicial do Produto

As histórias foram agrupadas por épico.

| Épico | Histórias | Quantidade |
|---|---|---:|
| Autenticação e usuários | US-001 a US-003 | 3 |
| Clientes | US-004 a US-006 | 3 |
| Equipamentos | US-007 a US-009 | 3 |
| Ordens de serviço | US-010 a US-014 | 5 |
| Diagnósticos e orçamentos | US-015 a US-017 | 3 |
| Financeiro | US-018 a US-019 | 2 |
| Estoque | US-020 a US-022 | 3 |
| Fotografias e documentos | US-023 a US-024 | 2 |
| Dashboard | US-025 | 1 |
| **Total** | **US-001 a US-025** | **25** |

A prioridade das histórias será estabelecida durante o planejamento do MVP.

---

# 13. Definition of Ready (DoR)

Uma história poderá ser considerada pronta para desenvolvimento quando:

- Seu objetivo estiver claro.
- O benefício esperado estiver identificado.
- Seus critérios de aceitação forem verificáveis.
- As regras de negócio aplicáveis estiverem definidas.
- Suas dependências forem conhecidas.
- Não existirem dúvidas críticas que impeçam a implementação.
- Seu escopo for adequado à tarefa planejada.

Uma história bloqueada por decisão não deverá ser iniciada sem o refinamento necessário.

---

# 14. Definition of Done (DoD)

Uma história poderá ser considerada concluída quando:

- A implementação atender aos critérios de aceitação.
- As regras de negócio relacionadas forem respeitadas.
- Os testes aplicáveis forem executados com sucesso.
- O código passar pela revisão definida para o projeto.
- Não existirem falhas críticas conhecidas relacionadas à entrega.
- A documentação afetada for atualizada.
- As alterações estiverem registradas no controle de versão.
- O Pull Request tiver sido aprovado e integrado à branch de destino.

A DoD poderá ser refinada conforme as ferramentas e a organização do projeto forem definidas.

---

# 15. Organização no GitHub

As histórias poderão ser convertidas em GitHub Issues.

### Modelo sugerido de Issue

**Título:** `[US-010] Criar ordem de serviço`

**Descrição:**

Como gerente, quero abrir uma ordem de serviço vinculada a um cliente e equipamento, para registrar o atendimento realizado.

**Critérios de aceitação:**

- [ ] Permitir selecionar cliente cadastrado.
- [ ] Permitir selecionar equipamento vinculado ao cliente.
- [ ] Registrar defeito relatado e data de entrada.
- [ ] Gerar número único automaticamente.
- [ ] Criar a OS com estado inicial Aberto.

**Referências:**

- RF-016.
- RF-017.
- RN-010.
- RN-011.
- RN-012.

**Labels sugeridas:**

- `feature`
- `backend`
- `frontend`
- `needs-refinement`

As labels e a divisão entre tarefas de backend, frontend e testes deverão ser definidas durante o planejamento.

---

# 16. Rastreabilidade

Cada história deverá manter referência aos requisitos e regras de negócio que motivaram sua criação.

A rastreabilidade seguirá a relação:

**Necessidade → RF → RN → US → Issue → Implementação → Teste**

Exemplo:

| Elemento | Referência |
|---|---|
| Necessidade | Registrar atendimentos |
| Requisito | RF-016 |
| Regra | RN-011 |
| História | US-010 |
| Issue | A ser criada |
| Testes | A serem implementados |

Essa estrutura permitirá identificar quais necessidades estão implementadas e quais ainda estão pendentes.

---

# 17. Pendências de Refinamento

Antes da implementação de determinadas histórias, será necessário:

1. Definir a matriz detalhada de permissões.
2. Definir os campos do cadastro de funcionários.
3. Formalizar as transições de estado das ordens de serviço.
4. Definir as condições de cancelamento.
5. Refinar a confirmação de peças utilizadas.
6. Definir o registro de pagamentos em criptomoedas.
7. Definir limites e políticas de armazenamento de fotografias.
8. Priorizar as histórias para o MVP.

Essas pendências poderão ser registradas em Issues específicas de análise e refinamento.

---

# 18. Encerramento

O backlog inicial contém **25 histórias de usuário**, distribuídas em nove épicos funcionais.

As histórias descrevem necessidades do negócio e apresentam critérios iniciais de aceitação.

A priorização e a seleção das histórias para a primeira entrega serão realizadas no planejamento do MVP.

**Próxima etapa:** `06-casos-de-uso.md` — Modelagem dos Casos de Uso do Sistema.