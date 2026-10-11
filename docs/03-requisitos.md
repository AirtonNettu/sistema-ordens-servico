# 03 — Especificação de Requisitos de Software

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Documento:** Especificação de Requisitos de Software (ERS)  
**Versão:** 1.0 — Especificação inicial  
**Status:** Elaborado — aguardando revisão e aprovação  
**Origem:** `02-levantamento-requisitos.md`

---

## 1. Objetivo

Este documento especifica os requisitos funcionais e não funcionais do Sistema de Ordens de Serviço para Assistência Técnica.

Seu objetivo é estabelecer uma referência para:

- Planejamento do desenvolvimento.
- Definição do escopo do produto.
- Modelagem do sistema.
- Implementação das funcionalidades.
- Elaboração de testes.
- Validação das entregas.
- Rastreamento das necessidades do negócio.

Os requisitos aqui descritos representam o escopo funcional identificado durante o levantamento, não necessariamente o escopo completo da primeira versão.

A seleção das funcionalidades do Produto Mínimo Viável (MVP) será realizada no documento `09-planejamento-mvp.md`.

---

## 2. Convenções

### 2.1 Identificação

Cada requisito possui um identificador único.

| Prefixo | Significado |
|---|---|
| RF | Requisito Funcional |
| RNF | Requisito Não Funcional |

Exemplo:

**RF-001 — Cadastrar clientes**

O identificador deverá permanecer estável mesmo quando a descrição do requisito for atualizada.

### 2.2 Linguagem

A expressão **"O sistema deverá"** indica um comportamento esperado que poderá ser verificado durante os testes.

### 2.3 Estados de definição

Os requisitos poderão receber os seguintes estados:

- **Definido:** comportamento confirmado no levantamento.
- **Parcialmente definido:** necessidade confirmada, mas existem detalhes pendentes.
- **Proposto:** requisito sugerido para avaliação, ainda não aprovado.

---

# 3. Requisitos Funcionais

## 3.1 Autenticação e controle de acesso

### RF-001 — Autenticar usuários

**Estado:** Definido

O sistema deverá exigir autenticação para permitir o acesso às funcionalidades internas.

### RF-002 — Controlar permissões por perfil

**Estado:** Parcialmente definido

O sistema deverá controlar o acesso às funcionalidades conforme o perfil do usuário autenticado.

Perfis inicialmente identificados:

- Gerente.
- RH.

A matriz detalhada de permissões deverá ser definida posteriormente.

### RF-003 — Cadastrar funcionários

**Estado:** Parcialmente definido

O sistema deverá permitir o cadastro e a consulta de funcionários por usuários autorizados.

Os campos obrigatórios e as operações administrativas ainda deverão ser detalhados.

---

## 3.2 Gestão de clientes

### RF-004 — Cadastrar clientes

**Estado:** Definido

O sistema deverá permitir cadastrar clientes, incluindo obrigatoriamente um número de telefone de contato.

### RF-005 — Consultar clientes

**Estado:** Definido

O sistema deverá permitir localizar clientes pelo nome ou número de telefone.

### RF-006 — Reutilizar cadastros

**Estado:** Definido

O sistema deverá permitir selecionar um cliente previamente cadastrado ao abrir uma nova ordem de serviço.

### RF-007 — Consultar histórico do cliente

**Estado:** Definido

O sistema deverá apresentar as ordens de serviço anteriormente vinculadas ao cliente selecionado.

### RF-008 — Atualizar cadastro de clientes

**Estado:** Proposto

O sistema deverá permitir que usuários autorizados atualizem os dados cadastrais de clientes existentes.

**Justificativa:** dados de contato podem mudar ao longo do tempo.

---

## 3.3 Gestão de equipamentos

### RF-009 — Cadastrar equipamentos individualmente

**Estado:** Definido

O sistema deverá permitir cadastrar individualmente computadores e notebooks, mesmo quando pertencerem ao mesmo cliente e possuírem características semelhantes.

### RF-010 — Gerar identificação interna

**Estado:** Definido

O sistema deverá gerar um identificador interno único para cada equipamento cadastrado.

O identificador não poderá ser reutilizado.

### RF-011 — Registrar identificação de fábrica

**Estado:** Definido

O sistema deverá permitir registrar o número de série do fabricante quando disponível.

Para equipamentos sem número de série geral de fábrica, o identificador interno da assistência será utilizado como identificação principal.

### RF-012 — Consultar equipamentos

**Estado:** Definido

O sistema deverá permitir localizar equipamentos por seu identificador interno.

### RF-013 — Vincular equipamento ao cliente

**Estado:** Definido

O sistema deverá associar cada equipamento ao cadastro de seu proprietário.

Um cliente poderá possuir vários equipamentos.

### RF-014 — Reutilizar cadastro de equipamento

**Estado:** Definido

O sistema deverá permitir selecionar um equipamento previamente cadastrado ao abrir uma nova ordem de serviço.

### RF-015 — Consultar histórico de manutenção

**Estado:** Definido

O sistema deverá apresentar o histórico das ordens de serviço vinculadas ao equipamento.

---

## 3.4 Gestão de ordens de serviço

### RF-016 — Criar ordem de serviço

**Estado:** Definido

O sistema deverá permitir criar ordens de serviço associadas a um cliente e a um equipamento.

A OS deverá registrar, no mínimo:

- Identificação do cliente.
- Identificação do equipamento.
- Defeito relatado.
- Data de entrada.
- Estado do atendimento.

### RF-017 — Gerar número da OS

**Estado:** Definido

O sistema deverá gerar automaticamente um número único para cada ordem de serviço.

Números já utilizados não poderão ser reutilizados.

### RF-018 — Consultar ordens de serviço

**Estado:** Definido

O sistema deverá permitir consultar as ordens de serviço registradas.

### RF-019 — Acompanhar estados da OS

**Estado:** Definido

O sistema deverá permitir acompanhar as ordens de serviço pelos seguintes estados:

1. Aberto.
2. Em diagnóstico.
3. Aguardando aprovação.
4. Em manutenção.
5. Concluído.
6. Encerrado.

Estados alternativos:

- Orçamento recusado.
- Cancelado.

### RF-020 — Atualizar estado da OS

**Estado:** Parcialmente definido

O sistema deverá permitir que usuários autorizados atualizem o estado de uma ordem de serviço.

As transições permitidas e as restrições específicas serão detalhadas nas regras de negócio.

### RF-021 — Separar ordens por situação

**Estado:** Definido

O sistema deverá permitir visualizar separadamente ordens de serviço concluídas, encerradas e canceladas.

### RF-022 — Registrar data de saída

**Estado:** Definido

O sistema deverá registrar a data de saída do equipamento quando sua retirada for confirmada.

### RF-023 — Cancelar ordem de serviço

**Estado:** Parcialmente definido

O sistema deverá permitir cancelar uma OS sem excluir seu registro.

Ao cancelar:

- O estado deverá ser atualizado para Cancelado.
- O número original deverá ser preservado.
- O histórico deverá permanecer disponível.
- A OS deverá deixar de integrar a contagem de ordens ativas.

As condições para autorizar o cancelamento ainda deverão ser detalhadas.

---

## 3.5 Diagnósticos e orçamentos

### RF-024 — Registrar diagnóstico

**Estado:** Definido

O sistema deverá permitir registrar informações do diagnóstico realizado no equipamento.

### RF-025 — Registrar orçamento

**Estado:** Definido

O sistema deverá permitir criar um orçamento associado à ordem de serviço.

### RF-026 — Discriminar serviços e valores

**Estado:** Definido

O sistema deverá permitir incluir no orçamento serviços individualizados, com descrição e valor.

### RF-027 — Calcular total do orçamento

**Estado:** Definido

O sistema deverá calcular automaticamente o valor total do orçamento a partir dos itens registrados.

### RF-028 — Registrar aprovação do orçamento

**Estado:** Definido

O sistema deverá permitir registrar a aprovação do orçamento pelo cliente.

### RF-029 — Registrar recusa do orçamento

**Estado:** Definido

O sistema deverá permitir registrar a recusa do orçamento, preservando as informações apresentadas ao cliente.

O reparo recusado não deverá ser registrado como executado.

### RF-030 — Controlar cobrança de diagnóstico

**Estado:** Definido

O sistema deverá aplicar a política de cobrança de diagnóstico estabelecida pelo negócio:

- Diagnóstico padrão de R$ 50,00.
- Cobrança do diagnóstico quando o reparo for recusado.
- Inclusão do diagnóstico no valor da mão de obra quando o reparo for aprovado.
- Prevenção de cobrança duplicada.

---

## 3.6 Gestão financeira

### RF-031 — Registrar pagamentos

**Estado:** Definido

O sistema deverá permitir que gerente ou RH registrem manualmente os pagamentos relacionados às ordens de serviço.

### RF-032 — Registrar forma de pagamento

**Estado:** Definido

O sistema deverá permitir registrar as seguintes formas de pagamento:

- Pix.
- Dinheiro.
- Cartão de débito.
- Cartão de crédito.
- Criptomoedas.

### RF-033 — Registrar valor recebido

**Estado:** Definido

O sistema deverá registrar o valor recebido e associá-lo à ordem de serviço correspondente.

### RF-034 — Consultar histórico financeiro

**Estado:** Definido

O sistema deverá permitir consultar os pagamentos registrados.

### RF-035 — Impedir pagamento parcial

**Estado:** Definido

O sistema não deverá aceitar o registro de pagamentos parciais de ordens de serviço.

### RF-036 — Validar quitação para encerramento

**Estado:** Definido

O sistema deverá impedir o encerramento de uma ordem de serviço quando existir saldo financeiro pendente.

### RF-037 — Atualizar registros financeiros

**Estado:** Definido

Após o registro de um pagamento integral, o sistema deverá atualizar as informações financeiras associadas à ordem de serviço.

**Restrição de escopo:** a primeira versão registrará pagamentos, mas não realizará transações bancárias ou confirmações automáticas junto a instituições financeiras.

---

## 3.7 Controle de estoque

### RF-038 — Cadastrar peças

**Estado:** Definido

O sistema deverá permitir cadastrar peças utilizadas nos serviços de manutenção.

### RF-039 — Consultar estoque

**Estado:** Definido

O sistema deverá permitir consultar as quantidades disponíveis das peças cadastradas.

### RF-040 — Associar peças à OS

**Estado:** Definido

O sistema deverá permitir registrar as peças relacionadas a uma ordem de serviço.

### RF-041 — Atualizar estoque automaticamente

**Estado:** Definido

O sistema deverá atualizar a quantidade disponível de uma peça da assistência quando ela for retirada do estoque para utilização em uma OS.

### RF-042 — Registrar peças fornecidas pelo cliente

**Estado:** Definido

O sistema deverá permitir registrar peças fornecidas pelo cliente sem:

- Cobrar seu valor como peça da assistência.
- Reduzir o estoque da empresa.

### RF-043 — Devolver peças não utilizadas

**Estado:** Parcialmente definido

O sistema deverá permitir devolver ao estoque peças não utilizadas em ordens de serviço canceladas.

A devolução deverá atualizar a quantidade disponível e preservar o histórico da movimentação.

O procedimento de confirmação das peças não utilizadas ainda será detalhado.

### RF-044 — Registrar movimentações de estoque

**Estado:** Definido

O sistema deverá manter registros das movimentações de entrada, retirada e devolução de peças.

---

## 3.8 Registro fotográfico

### RF-045 — Anexar fotografias

**Estado:** Definido

O sistema deverá permitir anexar fotografias às ordens de serviço.

### RF-046 — Classificar fotografias

**Estado:** Definido

O sistema deverá permitir identificar fotografias registradas no recebimento e após a manutenção.

### RF-047 — Consultar fotografias

**Estado:** Definido

O sistema deverá permitir consultar as fotografias vinculadas à OS, inclusive após seu encerramento.

---

## 3.9 Emissão de documentos

### RF-048 — Gerar comprovante em PDF

**Estado:** Definido

O sistema deverá gerar um comprovante de recebimento em PDF utilizando os dados registrados na ordem de serviço.

### RF-049 — Apresentar informações no comprovante

**Estado:** Definido

O comprovante deverá conter:

- Identificação da assistência técnica.
- Número da OS.
- Nome e telefone do cliente.
- Identificação do equipamento.
- Marca e modelo.
- Número de série, quando disponível.
- Código interno do equipamento.
- Defeito relatado.
- Data de entrada.

### RF-050 — Disponibilizar comprovante

**Estado:** Definido

O sistema deverá permitir obter o PDF para impressão ou compartilhamento manual com o cliente, inclusive por WhatsApp.

### RF-051 — Reemitir comprovante

**Estado:** Definido

O sistema deverá permitir consultar e emitir novamente o comprovante de uma OS registrada.

---

## 3.10 Painel de acompanhamento

### RF-052 — Apresentar indicadores operacionais

**Estado:** Definido

O sistema deverá apresentar indicadores de acompanhamento das ordens de serviço.

### RF-053 — Atualizar contagem de ordens

**Estado:** Definido

O sistema deverá atualizar os indicadores quando uma OS for criada, tiver seu estado alterado ou for cancelada.

### RF-054 — Excluir canceladas da contagem ativa

**Estado:** Definido

O sistema não deverá contabilizar ordens canceladas entre as ordens ativas.

### RF-055 — Consultar atendimentos por estado

**Estado:** Definido

O sistema deverá permitir consultar ordens de serviço agrupadas ou filtradas por estado.

---

# 4. Requisitos Não Funcionais

Os requisitos não funcionais descrevem características de qualidade, segurança, operação e restrições da solução.

Os requisitos abaixo distinguem as necessidades já identificadas das propostas que precisarão ser refinadas antes da implementação.

## 4.1 Segurança

### RNF-001 — Acesso autenticado

**Estado:** Definido

As funcionalidades internas do sistema deverão estar disponíveis somente para usuários autenticados.

### RNF-002 — Autorização por perfil

**Estado:** Parcialmente definido

O sistema deverá aplicar restrições de acesso conforme o perfil do usuário, impedindo operações não autorizadas.

### RNF-003 — Proteção das informações

**Estado:** Proposto

O sistema deverá adotar mecanismos de proteção para dados pessoais, financeiros e registros dos atendimentos.

Os controles técnicos específicos serão definidos na arquitetura.

### RNF-004 — Restrição de dispositivos

**Estado:** Parcialmente definido

O sistema deverá considerar a necessidade de restringir o acesso a computadores autorizados pela empresa.

O mecanismo de autorização ainda não foi escolhido.

---

## 4.2 Integridade e consistência

### RNF-005 — Identificadores únicos

**Estado:** Definido

O sistema deverá garantir que os identificadores internos de equipamentos e os números de ordens de serviço sejam únicos e não reutilizáveis.

### RNF-006 — Consistência do estoque

**Estado:** Definido

As movimentações de peças deverão preservar a consistência entre as quantidades disponíveis e as operações registradas.

### RNF-007 — Consistência financeira

**Estado:** Definido

O sistema deverá preservar a consistência entre os valores devidos, os pagamentos registrados e o estado financeiro das ordens de serviço.

### RNF-008 — Preservação de histórico

**Estado:** Definido

O sistema deverá preservar os registros históricos de atendimentos encerrados e cancelados.

---

## 4.3 Usabilidade

### RNF-009 — Organização das informações

**Estado:** Definido

A interface deverá permitir distinguir visualmente os diferentes estados das ordens de serviço.

### RNF-010 — Facilidade de consulta

**Estado:** Proposto

A interface deverá oferecer mecanismos de busca e navegação que facilitem a localização de clientes, equipamentos e atendimentos.

### RNF-011 — Clareza de mensagens

**Estado:** Proposto

O sistema deverá apresentar mensagens compreensíveis para erros de validação e operações não permitidas.

---

## 4.4 Compatibilidade e acesso

### RNF-012 — Interface web

**Estado:** Definido

O produto deverá disponibilizar uma interface acessível por navegador web.

### RNF-013 — Utilização no Windows

**Estado:** Parcialmente definido

O produto deverá contemplar a necessidade de utilização em ambiente Windows.

A implementação de um aplicativo Windows separado será avaliada durante o planejamento técnico.

### RNF-014 — Operação para uma empresa

**Estado:** Definido

A solução inicial atenderá uma única empresa, sem necessidade de arquitetura multiempresa.

---

## 4.5 Desempenho e confiabilidade

### RNF-015 — Desempenho das consultas

**Estado:** Proposto

O sistema deverá apresentar desempenho adequado nas consultas de clientes, equipamentos e ordens de serviço.

Metas mensuráveis de tempo de resposta serão definidas antes dos testes de desempenho.

### RNF-016 — Tratamento de falhas

**Estado:** Proposto

O sistema deverá tratar falhas de operações sem produzir alterações inconsistentes nos registros.

### RNF-017 — Recuperação de dados

**Estado:** Proposto

A solução deverá considerar mecanismos de cópia de segurança e recuperação de dados.

A frequência dos backups e os objetivos de recuperação ainda serão definidos.

---

## 4.6 Manutenibilidade e testabilidade

### RNF-018 — Organização do código

**Estado:** Proposto

O código-fonte deverá ser organizado de maneira a facilitar manutenção, testes e evolução das funcionalidades.

### RNF-019 — Testabilidade

**Estado:** Proposto

As principais regras de negócio deverão permitir verificação por testes automatizados.

### RNF-020 — Rastreabilidade de alterações

**Estado:** Proposto

O projeto deverá utilizar controle de versão para registrar alterações no código e na documentação.

---

# 5. Restrições de Escopo

As seguintes funcionalidades não estão previstas no escopo inicial confirmado:

- Gestão de múltiplas empresas.
- Portal de clientes.
- Portal próprio para técnicos.
- Processamento automático de pagamentos.
- Integração bancária para confirmação de recebimentos.

Essas funcionalidades poderão ser consideradas futuramente, mediante análise e priorização.

---

# 6. Dependências entre requisitos

Algumas funcionalidades dependem da existência de outras.

| Requisito | Dependência principal |
|---|---|
| RF-006 — Reutilizar cliente | RF-004 — Cadastrar cliente |
| RF-013 — Vincular equipamento | RF-004 e RF-009 |
| RF-016 — Criar OS | RF-004, RF-009 e RF-013 |
| RF-015 — Histórico do equipamento | RF-016 |
| RF-025 — Registrar orçamento | RF-016 |
| RF-031 — Registrar pagamento | RF-016 |
| RF-036 — Validar quitação | RF-031 e RF-033 |
| RF-040 — Associar peças | RF-016 e RF-038 |
| RF-043 — Devolver peças | RF-040 e RF-044 |
| RF-048 — Gerar PDF | RF-016 e RF-017 |
| RF-053 — Atualizar indicadores | RF-016, RF-019 e RF-023 |

Esta tabela apresenta dependências funcionais iniciais. A ordem definitiva de implementação será definida no planejamento do MVP.

---

# 7. Pendências para Refinamento

As seguintes questões permanecem abertas:

1. Definir a matriz detalhada de permissões de Gerente e RH.
2. Definir os campos completos do cadastro de funcionários.
3. Definir as transições permitidas entre estados das ordens de serviço.
4. Definir as condições de cancelamento e eventual cobrança de diagnóstico.
5. Definir como confirmar o uso efetivo de peças.
6. Definir como registrar pagamentos em criptomoedas.
7. Definir se uma quitação integral poderá utilizar múltiplos meios de pagamento.
8. Definir procedimentos de correção de pagamentos.
9. Definir regras de atualização do valor do diagnóstico.
10. Definir formatos, tamanhos e retenção das fotografias.
11. Definir termos e eventual assinatura no comprovante.
12. Definir as políticas de backup e recuperação.
13. Definir metas mensuráveis de desempenho.
14. Definir o mecanismo de autorização de dispositivos.
15. Definir a estratégia de disponibilização para Windows.

Essas questões poderão ser convertidas em GitHub Issues de refinamento.

---

# 8. Critérios de Qualidade dos Requisitos

Durante a revisão, cada requisito deverá ser avaliado quanto a:

- **Clareza:** possui interpretação compreensível?
- **Necessidade:** atende a uma demanda real do negócio?
- **Consistência:** não contradiz outros requisitos?
- **Viabilidade:** pode ser implementado com os recursos disponíveis?
- **Verificabilidade:** pode ser validado por teste ou inspeção?
- **Rastreabilidade:** pode ser relacionado à sua origem e às entregas correspondentes?

Requisitos classificados como parcialmente definidos ou propostos não deverão ser tratados automaticamente como decisões aprovadas.

---

# 9. Rastreabilidade

A rastreabilidade será mantida por meio da relação:

**Necessidade levantada → Requisito → Regra de negócio → História de usuário → Caso de uso → Implementação → Teste**

Exemplo:

- Necessidade: impedir encerramento com pagamento pendente.
- Requisito: RF-036.
- Regra de negócio: a ser registrada em `04-regras-de-negocio.md`.
- História de usuário: a ser registrada em `05-historias-usuario.md`.
- Teste: validar que uma OS com saldo pendente não pode ser encerrada.

Os identificadores dos requisitos deverão ser utilizados nas Issues e nos critérios de aceitação quando aplicável.

---

# 10. Aprovação e Controle de Mudanças

**Estado do documento:** aguardando revisão e aprovação.

Alterações futuras deverão:

1. Identificar o requisito afetado.
2. Descrever a mudança solicitada.
3. Avaliar impactos em outros requisitos e regras de negócio.
4. Atualizar a documentação relacionada.
5. Registrar a alteração no controle de versão.

---

# 11. Encerramento

A especificação inicial contém:

- **55 requisitos funcionais**, entre definidos, parcialmente definidos e propostos.
- **20 requisitos não funcionais**, entre definidos, parcialmente definidos e propostos.

Os requisitos estabelecem uma base para o planejamento do produto e para a criação de atividades de desenvolvimento.

A aprovação desta especificação não significa que todos os requisitos serão implementados na primeira entrega.
