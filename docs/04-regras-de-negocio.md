# 04 — Regras de Negócio

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Documento:** Especificação de Regras de Negócio  
**Versão:** 1.0 — Especificação inicial  
**Status:** Elaborado — aguardando revisão e aprovação  
**Documentos de referência:**
- `01-visao-do-projeto.md`
- `02-levantamento-requisitos.md`
- `03-requisitos.md`

---

## 1. Objetivo

Este documento estabelece as regras de negócio que deverão orientar o funcionamento do Sistema de Ordens de Serviço para Assistência Técnica.

As regras representam políticas operacionais, condições, restrições e decisões definidas pelo responsável pelo projeto.

Elas deverão ser consideradas durante:

- A modelagem do domínio.
- A implementação das funcionalidades.
- A validação de dados.
- A definição dos fluxos de atendimento.
- A elaboração de testes.
- A revisão das entregas.

Uma regra de negócio não determina necessariamente qual tecnologia será utilizada para implementá-la.

---

## 2. Convenções

Cada regra possui um identificador único no formato `RN-XXX`.

### Estados de definição

- **Confirmada:** regra aprovada durante o levantamento.
- **Parcialmente definida:** princípio confirmado, mas com condições pendentes.
- **Proposta:** regra sugerida para avaliação, ainda não aprovada.

Os identificadores deverão ser preservados durante a evolução do projeto.

---

# 3. Regras de Cadastro de Clientes

## RN-001 — Telefone obrigatório

**Estado:** Confirmada  
**Requisitos relacionados:** RF-004, RF-005

Todo cliente deverá possuir um número de telefone informado em seu cadastro.

O sistema não poderá concluir o cadastro de um cliente sem telefone.

## RN-002 — Reutilização do cadastro

**Estado:** Confirmada  
**Requisitos relacionados:** RF-006, RF-007

Quando um cliente retornar à assistência, o cadastro existente poderá ser reutilizado.

As novas ordens de serviço deverão ser associadas ao mesmo cliente.

## RN-003 — Histórico de atendimentos por cliente

**Estado:** Confirmada  
**Requisitos relacionados:** RF-007

O histórico das ordens de serviço de um cliente deverá permanecer associado ao seu cadastro, inclusive após o encerramento ou cancelamento dos atendimentos.

## RN-004 — Tratamento de cadastros duplicados

**Estado:** Proposta  
**Requisitos relacionados:** RF-004, RF-005, RF-008

O sistema deverá auxiliar na identificação de possíveis cadastros duplicados.

**Pendente:** definir se a coincidência de telefone deverá gerar apenas um alerta ou impedir a criação de outro cadastro.

---

# 4. Regras de Cadastro de Equipamentos

## RN-005 — Identificação individual

**Estado:** Confirmada  
**Requisitos relacionados:** RF-009, RF-010

Cada computador ou notebook deverá possuir um cadastro individual.

Dois equipamentos pertencentes ao mesmo cliente não poderão compartilhar o mesmo identificador interno.

## RN-006 — Código interno único

**Estado:** Confirmada  
**Requisitos relacionados:** RF-010

O sistema deverá gerar um código interno único para cada equipamento.

Um código já utilizado não poderá ser atribuído a outro equipamento.

## RN-007 — Identificação de equipamentos sem número de série

**Estado:** Confirmada  
**Requisitos relacionados:** RF-010, RF-011

Computadores que não possuírem número de série geral de fábrica poderão receber uma identificação própria da assistência técnica.

Essa identificação será representada pelo código interno do equipamento.

O número de série de fábrica, quando disponível, deverá ser registrado separadamente.

## RN-008 — Associação entre cliente e equipamento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-013, RF-014

Cada equipamento deverá estar associado a um cliente.

Um cliente poderá possuir vários equipamentos.

**Pendente:** definir o procedimento para transferência de propriedade de um equipamento.

## RN-009 — Histórico individual do equipamento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-015

As ordens de serviço deverão permanecer associadas ao equipamento correspondente.

O histórico deverá permitir identificar atendimentos anteriores, diagnósticos, serviços, peças, valores e estados das ordens.

---

# 5. Regras de Ordens de Serviço

## RN-010 — Numeração única da OS

**Estado:** Confirmada  
**Requisitos relacionados:** RF-016, RF-017

Cada ordem de serviço deverá receber um número único, gerado automaticamente pelo sistema.

O número de uma OS não poderá ser reutilizado, inclusive após seu cancelamento.

## RN-011 — Associação obrigatória

**Estado:** Confirmada  
**Requisitos relacionados:** RF-016

Toda ordem de serviço deverá estar vinculada a um cliente e a um equipamento cadastrado.

## RN-012 — Estados do atendimento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-019, RF-020

O fluxo principal de uma ordem de serviço compreenderá:

1. Aberto.
2. Em diagnóstico.
3. Aguardando aprovação.
4. Em manutenção.
5. Concluído.
6. Encerrado.

Também existirão os estados alternativos:

- Orçamento recusado.
- Cancelado.

## RN-013 — Distinção entre Concluído e Encerrado

**Estado:** Confirmada  
**Requisitos relacionados:** RF-019, RF-021, RF-022

Uma OS no estado **Concluído** indica que o serviço técnico foi finalizado, mas o equipamento ainda não foi retirado.

Uma OS no estado **Encerrado** indica que o equipamento foi retirado e o atendimento foi finalizado.

Os dois estados não poderão ser tratados como equivalentes.

## RN-014 — Registro da retirada

**Estado:** Confirmada  
**Requisitos relacionados:** RF-022

A data de saída deverá representar a retirada do equipamento pelo cliente.

A conclusão do reparo não deverá, por si só, registrar a retirada.

## RN-015 — Transições de estados

**Estado:** Parcialmente definida  
**Requisitos relacionados:** RF-019, RF-020

O sistema deverá respeitar as condições de transição entre os estados da OS.

O fluxo principal seguirá a sequência definida na RN-012.

O tratamento de retornos a estados anteriores, reaberturas e demais transições excepcionais ainda deverá ser refinado.

---

# 6. Regras de Diagnóstico e Orçamento

## RN-016 — Valor padrão do diagnóstico

**Estado:** Confirmada  
**Requisitos relacionados:** RF-024, RF-030

O valor padrão do diagnóstico técnico será de **R$ 50,00** por equipamento atendido.

**Pendente:** definir se e como usuários autorizados poderão alterar esse valor.

## RN-017 — Diagnóstico em orçamento recusado

**Estado:** Confirmada  
**Requisitos relacionados:** RF-029, RF-030

Quando o cliente recusar o reparo, o diagnóstico continuará sendo devido.

Caso não existam outros serviços autorizados, o valor a cobrar será de R$ 50,00.

## RN-018 — Diagnóstico incluído na mão de obra

**Estado:** Confirmada  
**Requisitos relacionados:** RF-026, RF-027, RF-030

Quando o cliente aprovar o reparo, o valor do diagnóstico estará incluído no preço da mão de obra.

O sistema não poderá adicionar novamente a taxa de diagnóstico ao total quando ela já estiver incluída na mão de obra.

## RN-019 — Orçamento discriminado

**Estado:** Confirmada  
**Requisitos relacionados:** RF-025, RF-026, RF-027

O orçamento deverá apresentar os serviços propostos e seus respectivos valores.

O valor total deverá ser calculado a partir dos itens registrados, respeitando a política de cobrança do diagnóstico.

## RN-020 — Aprovação do orçamento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-028, RF-020

A execução do reparo proposto dependerá da aprovação do orçamento pelo cliente.

O sistema deverá registrar a aprovação para permitir o acompanhamento do serviço autorizado.

## RN-021 — Recusa do orçamento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-029

Quando o cliente recusar o orçamento:

- A recusa deverá ser registrada.
- O orçamento permanecerá no histórico.
- O reparo recusado não poderá ser considerado executado.
- O diagnóstico continuará devido.
- O atendimento poderá ser encerrado após a retirada e a quitação do valor devido.

---

# 7. Regras Financeiras

## RN-022 — Pagamento na retirada

**Estado:** Confirmada  
**Requisitos relacionados:** RF-031, RF-033

O pagamento da ordem de serviço ocorrerá no momento da retirada do equipamento.

Não serão previstos pagamentos antecipados na versão inicialmente especificada.

## RN-023 — Pagamento integral

**Estado:** Confirmada  
**Requisitos relacionados:** RF-035

O sistema não permitirá pagamentos parciais.

O cliente deverá quitar integralmente o valor devido pela ordem de serviço.

## RN-024 — Encerramento condicionado à quitação

**Estado:** Confirmada  
**Requisitos relacionados:** RF-036, RF-022

Uma ordem de serviço somente poderá ser encerrada quando:

1. O equipamento tiver sido retirado.
2. O pagamento integral devido tiver sido confirmado no sistema.

Não será permitido encerrar uma OS com saldo financeiro pendente.

## RN-025 — Registro manual de pagamentos

**Estado:** Confirmada  
**Requisitos relacionados:** RF-031, RF-033, RF-037

Os pagamentos deverão ser registrados manualmente por usuários autorizados dos perfis Gerente ou RH.

O registro deverá identificar:

- Ordem de serviço.
- Valor recebido.
- Forma de pagamento.

O sistema atualizará os registros financeiros após a confirmação manual.

## RN-026 — Formas de pagamento aceitas

**Estado:** Confirmada  
**Requisitos relacionados:** RF-032

O sistema deverá permitir registrar pagamentos realizados por:

- Pix.
- Dinheiro.
- Cartão de débito.
- Cartão de crédito.
- Criptomoedas.

**Pendente:** definir como registrar a equivalência em reais de pagamentos em criptomoedas.

## RN-027 — Ausência de processamento financeiro automático

**Estado:** Confirmada  
**Requisitos relacionados:** RF-031, RF-037

Na primeira versão, o sistema não realizará transferências financeiras nem confirmação automática de pagamentos por instituições externas.

O sistema funcionará como ferramenta de registro e controle financeiro.

## RN-028 — Correção de registros financeiros

**Estado:** Proposta  
**Requisitos relacionados:** RF-031, RF-034

Correções de pagamentos registrados incorretamente deverão preservar informações suficientes para identificar a alteração.

**Pendente:** definir quais usuários poderão corrigir pagamentos e qual procedimento será adotado.

## RN-029 — Múltiplas formas de pagamento

**Estado:** Pendente de decisão  
**Requisitos relacionados:** RF-032, RF-035

Ainda não foi definido se uma quitação integral poderá ser realizada utilizando mais de uma forma de pagamento.

Essa possibilidade não deverá ser confundida com pagamentos parciais em momentos diferentes.

---

# 8. Regras de Cancelamento

## RN-030 — Cancelamento sem exclusão

**Estado:** Confirmada  
**Requisitos relacionados:** RF-023

O cancelamento de uma ordem de serviço deverá alterar seu estado para **Cancelado**.

O registro não deverá ser excluído definitivamente.

## RN-031 — Preservação do histórico de cancelamento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-023, RF-017

Uma OS cancelada deverá permanecer disponível para consulta.

Seu número original não poderá ser alterado nem reutilizado.

## RN-032 — Atualização dos indicadores

**Estado:** Confirmada  
**Requisitos relacionados:** RF-053, RF-054

Uma OS cancelada não deverá integrar a contagem de ordens ativas.

O sistema deverá atualizar automaticamente os indicadores após o cancelamento.

## RN-033 — Condições de cancelamento

**Estado:** Parcialmente definida  
**Requisitos relacionados:** RF-023

O sistema permitirá cancelar ordens de serviço, mas as seguintes condições ainda precisam ser definidas:

- Estados em que o cancelamento será permitido.
- Obrigatoriedade de informar o motivo.
- Tratamento de diagnósticos já realizados.
- Tratamento de valores eventualmente devidos.
- Procedimento de retirada do equipamento cancelado.

Até o refinamento dessas condições, o cancelamento não deverá ser interpretado automaticamente como perdão de valores devidos.

---

# 9. Regras de Estoque

## RN-034 — Controle de quantidade disponível

**Estado:** Confirmada  
**Requisitos relacionados:** RF-038, RF-039

O sistema deverá manter o registro da quantidade disponível de cada peça cadastrada no estoque da assistência.

## RN-035 — Retirada de peças para OS

**Estado:** Confirmada  
**Requisitos relacionados:** RF-040, RF-041

Quando uma peça pertencente à assistência for retirada do estoque para uma ordem de serviço, a quantidade disponível deverá ser atualizada automaticamente.

## RN-036 — Peças fornecidas pelo cliente

**Estado:** Confirmada  
**Requisitos relacionados:** RF-042

Peças fornecidas pelo cliente poderão ser registradas na OS.

Essas peças:

- Não deverão reduzir o estoque da assistência.
- Não deverão ser cobradas como peças fornecidas pela empresa.

A mão de obra de instalação poderá compor o orçamento normalmente.

## RN-037 — Devolução de peças não utilizadas

**Estado:** Confirmada  
**Requisitos relacionados:** RF-043, RF-044

Quando uma ordem de serviço for cancelada, peças retiradas do estoque que não tenham sido utilizadas poderão retornar ao estoque disponível.

A devolução deverá atualizar a quantidade e registrar a movimentação correspondente.

## RN-038 — Peças instaladas, danificadas ou consumidas

**Estado:** Confirmada  
**Requisitos relacionados:** RF-043

Peças já instaladas, danificadas ou consumidas não deverão retornar automaticamente ao estoque disponível.

## RN-039 — Confirmação da utilização de peças

**Estado:** Parcialmente definida  
**Requisitos relacionados:** RF-043, RF-044

A devolução ao estoque dependerá da identificação das peças efetivamente não utilizadas.

**Pendente:** definir como essa confirmação será registrada pelo gerente.

## RN-040 — Histórico de movimentações

**Estado:** Confirmada  
**Requisitos relacionados:** RF-044

O sistema deverá preservar o histórico das movimentações de peças, incluindo retiradas e devoluções.

---

# 10. Regras de Fotografias e Documentos

## RN-041 — Fotografias vinculadas à OS

**Estado:** Confirmada  
**Requisitos relacionados:** RF-045, RF-046, RF-047

As fotografias deverão permanecer vinculadas à ordem de serviço correspondente.

O sistema deverá permitir identificar fotografias do recebimento e do período posterior à manutenção.

## RN-042 — Preservação do registro fotográfico

**Estado:** Confirmada  
**Requisitos relacionados:** RF-047

As fotografias deverão permanecer disponíveis para consulta após o encerramento da ordem de serviço.

As políticas de retenção e exclusão ainda deverão ser definidas.

## RN-043 — Comprovante de recebimento

**Estado:** Confirmada  
**Requisitos relacionados:** RF-048, RF-049

O comprovante de recebimento deverá ser gerado a partir das informações registradas na OS.

Deverá conter:

- Identificação da assistência.
- Número da OS.
- Nome e telefone do cliente.
- Identificação do equipamento.
- Marca e modelo.
- Número de série de fábrica, quando disponível.
- Código interno.
- Defeito relatado.
- Data de entrada.

## RN-044 — Disponibilização do comprovante

**Estado:** Confirmada  
**Requisitos relacionados:** RF-050, RF-051

O comprovante deverá estar disponível em PDF para impressão, compartilhamento manual e emissão posterior.

O compartilhamento automatizado por WhatsApp não foi confirmado para a primeira versão.

---

# 11. Regras de Acesso e Operação

## RN-045 — Acesso autenticado

**Estado:** Confirmada  
**Requisitos relacionados:** RF-001, RNF-001

O acesso às funcionalidades internas dependerá de autenticação.

## RN-046 — Perfis de usuários

**Estado:** Confirmada  
**Requisitos relacionados:** RF-002, RNF-002

O sistema utilizará inicialmente os perfis:

- Gerente.
- RH.

As permissões específicas de cada perfil deverão ser refinadas.

## RN-047 — Registro de pagamentos por perfil

**Estado:** Confirmada  
**Requisitos relacionados:** RF-031, RF-002

Gerente e RH poderão registrar pagamentos.

As demais permissões financeiras deverão ser detalhadas posteriormente.

## RN-048 — Operação para uma empresa

**Estado:** Confirmada  
**Requisitos relacionados:** RNF-014

A primeira versão atenderá uma única empresa.

Não será exigida gestão de múltiplas empresas.

## RN-049 — Restrição a computadores autorizados

**Estado:** Parcialmente definida  
**Requisitos relacionados:** RNF-004

O acesso deverá considerar a necessidade de utilização em computadores autorizados.

O mecanismo de autorização será definido na arquitetura.

---

# 12. Matriz de Rastreabilidade

A tabela relaciona as principais regras aos requisitos funcionais correspondentes.

| Área | Regras | Requisitos principais |
|---|---|---|
| Clientes | RN-001 a RN-004 | RF-004 a RF-008 |
| Equipamentos | RN-005 a RN-009 | RF-009 a RF-015 |
| Ordens de serviço | RN-010 a RN-015 | RF-016 a RF-023 |
| Diagnóstico e orçamento | RN-016 a RN-021 | RF-024 a RF-030 |
| Financeiro | RN-022 a RN-029 | RF-031 a RF-037 |
| Cancelamento | RN-030 a RN-033 | RF-017, RF-023, RF-053, RF-054 |
| Estoque | RN-034 a RN-040 | RF-038 a RF-044 |
| Fotografias e documentos | RN-041 a RN-044 | RF-045 a RF-051 |
| Acesso e operação | RN-045 a RN-049 | RF-001, RF-002, RF-031 e RNFs relacionados |

---

# 13. Cenários para Validação

Os cenários abaixo representam exemplos de testes derivados das regras confirmadas.

### Cenário 01 — Cliente sem telefone

**Dado que** o gerente está cadastrando um cliente,  
**Quando** tentar concluir o cadastro sem informar telefone,  
**Então** o sistema deverá impedir a operação.

**Regras:** RN-001.

### Cenário 02 — Identificação única

**Dado que** um equipamento já possui um código interno,  
**Quando** outro equipamento for cadastrado,  
**Então** o sistema deverá atribuir um código diferente.

**Regras:** RN-005 e RN-006.

### Cenário 03 — Diagnóstico com orçamento recusado

**Dado que** o diagnóstico foi realizado,  
**E** o cliente recusou o reparo,  
**E** não existem outros serviços autorizados,  
**Quando** o valor devido for calculado,  
**Então** o total deverá ser de R$ 50,00.

**Regras:** RN-016 e RN-017.

### Cenário 04 — Diagnóstico incluído na mão de obra

**Dado que** o cliente aprovou o reparo,  
**E** o preço da mão de obra já inclui o diagnóstico,  
**Quando** o orçamento for totalizado,  
**Então** o sistema não deverá adicionar novamente R$ 50,00.

**Regras:** RN-018 e RN-019.

### Cenário 05 — Pagamento incompleto

**Dado que** uma OS possui valor devido de R$ 150,00,  
**Quando** o usuário tentar registrar apenas R$ 100,00 como pagamento,  
**Então** o sistema deverá rejeitar o pagamento parcial.

**Regras:** RN-023.

### Cenário 06 — Encerramento sem quitação

**Dado que** uma OS possui saldo pendente,  
**Quando** o usuário tentar encerrá-la,  
**Então** o sistema deverá impedir o encerramento.

**Regras:** RN-024.

### Cenário 07 — Cancelamento de OS

**Dado que** uma OS está ativa e atende às condições de cancelamento,  
**Quando** o cancelamento for registrado,  
**Então** a OS deverá receber o estado Cancelado,  
**E** seu histórico deverá ser preservado,  
**E** ela deverá deixar de integrar a contagem de ordens ativas.

**Regras:** RN-030, RN-031 e RN-032.

**Observação:** as condições específicas de cancelamento ainda precisam ser refinadas.

### Cenário 08 — Devolução de peça não utilizada

**Dado que** uma peça da assistência foi retirada do estoque para uma OS,  
**E** a peça não foi utilizada,  
**Quando** sua devolução for confirmada,  
**Então** a quantidade disponível deverá ser atualizada,  
**E** a movimentação deverá ser registrada.

**Regras:** RN-037 e RN-040.

### Cenário 09 — Peça fornecida pelo cliente

**Dado que** o cliente forneceu uma peça para o reparo,  
**Quando** ela for registrada na OS,  
**Então** o estoque da assistência não deverá ser reduzido,  
**E** o valor da peça não deverá ser cobrado como item fornecido pela empresa.

**Regras:** RN-036.

---

# 14. Pendências de Negócio

As seguintes decisões permanecem abertas:

1. Condições detalhadas de cancelamento.
2. Tratamento financeiro de diagnósticos em OS canceladas.
3. Procedimento de confirmação de peças utilizadas.
4. Alteração do valor padrão do diagnóstico.
5. Correção de pagamentos registrados incorretamente.
6. Utilização de múltiplas formas de pagamento na quitação.
7. Conversão e registro de pagamentos em criptomoedas.
8. Reabertura de ordens de serviço.
9. Transferência de propriedade de equipamentos.
10. Matriz detalhada de permissões.
11. Políticas de retenção e exclusão de fotografias.
12. Termos de recebimento e eventual assinatura do cliente.

Essas pendências deverão ser refinadas conforme sua prioridade no planejamento do MVP.

---

# 15. Controle de Mudanças

Toda alteração em uma regra de negócio deverá considerar:

1. Identificação da regra afetada.
2. Justificativa da mudança.
3. Impacto nos requisitos relacionados.
4. Impacto nos fluxos e casos de uso.
5. Necessidade de atualizar testes.
6. Registro da alteração no controle de versão.

Regras confirmadas não deverão ser modificadas silenciosamente durante a implementação.

---

# 16. Encerramento

Este documento apresenta **49 regras de negócio**, classificadas entre confirmadas, parcialmente definidas, propostas e pendentes.

As regras fornecem uma referência para a implementação e validação do comportamento do sistema.

**Próxima etapa:** `05-historias-usuario.md` — Histórias de Usuário e Critérios de Aceitação.