# 07 — Protótipos e Estrutura das Telas

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Documento:** Protótipos de Baixa Fidelidade e Navegação  
**Versão:** 1.0 — Proposta inicial  
**Status:** Aguardando revisão e aprovação

**Documentos de referência:**
- `01-visao-do-projeto.md`
- `02-levantamento-requisitos.md`
- `03-requisitos.md`
- `04-regras-de-negocio.md`
- `05-historias-usuario.md`
- `06-casos-de-uso.md`

---

## 1. Objetivo

Este documento apresenta a proposta inicial de organização visual e navegação do Sistema de Ordens de Serviço para Assistência Técnica.

O objetivo é definir como os usuários poderão acessar as funcionalidades identificadas nas etapas anteriores.

Os protótipos apresentados são de baixa fidelidade e deverão orientar a construção posterior das interfaces.

Eles não representam uma aprovação definitiva do design.

---

## 2. Princípios de Interface

A interface deverá priorizar:

- Clareza das informações.
- Navegação simples.
- Facilidade para localizar ordens de serviço.
- Identificação visual dos estados dos atendimentos.
- Redução de preenchimentos repetitivos.
- Organização das informações por funcionalidade.
- Mensagens de validação compreensíveis.
- Consistência entre formulários, tabelas e ações.

**Diretriz proposta:** utilizar um layout administrativo com menu lateral, cabeçalho e área central de conteúdo.

---

# 3. Estrutura Geral do Sistema

## 3.1 Layout principal

```text
+----------------------------------------------------------+
| SISTEMA DE ORDENS DE SERVIÇO            Usuário | Sair    |
+------------------+---------------------------------------+
|                  |                                       |
|  MENU            |  CONTEÚDO PRINCIPAL                   |
|                  |                                       |
|  Dashboard       |  Título da página                     |
|  Ordens Serviço  |                                       |
|  Clientes        |  Indicadores, formulários,            |
|  Equipamentos    |  tabelas e informações                |
|  Orçamentos      |                                       |
|  Financeiro      |                                       |
|  Estoque         |                                       |
|  Funcionários    |                                       |
|                  |                                       |
+------------------+---------------------------------------+
```

### Elementos propostos

**Menu lateral**

Responsável pelo acesso às principais áreas.

**Cabeçalho**

Apresenta identificação do sistema, usuário autenticado e opção de saída.

**Área central**

Exibe o conteúdo da funcionalidade selecionada.

**Observação:** a disponibilidade de cada opção dependerá das permissões do usuário.

---

# 4. Mapa de Navegação

```text
Sistema
|
+-- Autenticação
|
+-- Dashboard
|
+-- Ordens de Serviço
|   |
|   +-- Listagem
|   +-- Nova OS
|   +-- Detalhes da OS
|       |
|       +-- Diagnóstico
|       +-- Orçamento
|       +-- Serviços e Peças
|       +-- Fotografias
|       +-- Pagamento
|       +-- Comprovante PDF
|       +-- Histórico
|
+-- Clientes
|   |
|   +-- Listagem
|   +-- Cadastro
|   +-- Detalhes
|   +-- Histórico
|
+-- Equipamentos
|   |
|   +-- Listagem
|   +-- Cadastro
|   +-- Detalhes
|   +-- Histórico de Manutenção
|
+-- Financeiro
|   |
|   +-- Pagamentos
|   +-- Histórico Financeiro
|
+-- Estoque
|   |
|   +-- Peças
|   +-- Movimentações
|
+-- Funcionários
|
+-- Configurações
```

**Observação:** a tela de configurações é uma proposta de navegação, não uma funcionalidade já aprovada.

---

# 5. Protótipo 01 — Tela de Autenticação

**Objetivo:** permitir acesso ao sistema por usuários autorizados.

**Referências:** UC-001, US-001, RF-001.

```text
+------------------------------------------------+
|                                                |
|             ASSISTÊNCIA TÉCNICA                |
|                                                |
|               Acesso ao Sistema                |
|                                                |
|   Usuário / E-mail                             |
|   +----------------------------------------+   |
|   |                                        |   |
|   +----------------------------------------+   |
|                                                |
|   Senha                                        |
|   +----------------------------------------+   |
|   |                                        |   |
|   +----------------------------------------+   |
|                                                |
|             [ ENTRAR NO SISTEMA ]              |
|                                                |
+------------------------------------------------+
```

### Comportamentos esperados

- Solicitar credenciais.
- Validar autenticação.
- Impedir acesso não autorizado.
- Encaminhar o usuário autenticado à área permitida.

**Pendente:** definir identificador de login e mecanismo de recuperação de acesso.

---

# 6. Protótipo 02 — Dashboard

**Objetivo:** apresentar uma visão geral dos atendimentos.

**Referências:** UC-019, US-025, RF-052 a RF-055.

```text
+----------------------------------------------------------+
| DASHBOARD                                                |
| Visão geral da assistência técnica                       |
+----------------------------------------------------------+
|                                                          |
| +-------------+ +-------------+ +---------------------+  |
| | OS ATIVAS   | | EM          | | AGUARDANDO          |  |
| |             | | DIAGNÓSTICO | | APROVAÇÃO           |  |
| |     24      | |      6      | |         4           |  |
| +-------------+ +-------------+ +---------------------+  |
|                                                          |
| +----------------------+ +-----------------------------+ |
| | EM MANUTENÇÃO        | | CONCLUÍDAS                  | |
| |                      | | Aguardando retirada         | |
| |         8            | |           6                 | |
| +----------------------+ +-----------------------------+ |
|                                                          |
| ORDENS DE SERVIÇO RECENTES                               |
| +------------------------------------------------------+ |
| | Nº OS | Cliente | Equipamento | Estado              | |
| |-------|---------|-------------|---------------------| |
| | 001   | Cliente | Notebook    | Em diagnóstico      | |
| | 002   | Cliente | Desktop     | Em manutenção       | |
| | 003   | Cliente | Notebook    | Concluído           | |
| +------------------------------------------------------+ |
|                                                          |
| [ NOVA ORDEM DE SERVIÇO ]                                |
+----------------------------------------------------------+
```

### Informações propostas

- Total de ordens ativas.
- Ordens em diagnóstico.
- Ordens aguardando aprovação.
- Ordens em manutenção.
- Ordens concluídas aguardando retirada.
- Listagem de atendimentos recentes.

Os valores apresentados são ilustrativos.

### Comportamentos esperados

- Atualizar indicadores conforme alterações nas OS.
- Não contabilizar ordens canceladas entre as ativas.
- Permitir acessar os detalhes de um atendimento.

**Pendente:** definir quais indicadores adicionais serão priorizados.

---

# 7. Protótipo 03 — Listagem de Ordens de Serviço

**Objetivo:** consultar e localizar atendimentos.

**Referências:** UC-006, UC-019, US-011, US-012.

```text
+----------------------------------------------------------+
| ORDENS DE SERVIÇO                        [ + NOVA OS ]   |
+----------------------------------------------------------+
|                                                          |
| Pesquisar: [ Número, cliente ou equipamento           ]  |
|                                                          |
| [ Todas ] [ Ativas ] [ Concluídas ] [ Encerradas ]       |
| [ Recusadas ] [ Canceladas ]                             |
|                                                          |
| +------------------------------------------------------+ |
| | Nº   | Cliente | Equipamento | Entrada | Estado      | |
| |------|---------|-------------|---------|-------------| |
| | 001  | Cliente | Notebook    | 10/10   | Aberto      | |
| | 002  | Cliente | Desktop     | 10/10   | Diagnóstico | |
| | 003  | Cliente | Notebook    | 09/10   | Concluído   | |
| +------------------------------------------------------+ |
|                                                          |
| Selecionar OS para visualizar detalhes.                  |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Pesquisar atendimentos.
- Filtrar ordens por estado.
- Distinguir concluídas e encerradas.
- Consultar histórico de cancelamentos.
- Abrir detalhes de uma OS.

**Proposta:** utilizar indicadores visuais de estado, sem depender exclusivamente de cores.

---

# 8. Protótipo 04 — Nova Ordem de Serviço

**Objetivo:** registrar o recebimento de um equipamento.

**Referências:** UC-005, US-010, RF-016, RF-017.

```text
+----------------------------------------------------------+
| NOVA ORDEM DE SERVIÇO                                    |
+----------------------------------------------------------+
|                                                          |
| CLIENTE                                                  |
|                                                          |
| Buscar cliente: [ Nome ou telefone                  ]    |
|                                                          |
| [ Selecionar cliente ]    [ + Novo cliente ]             |
|                                                          |
| EQUIPAMENTO                                              |
|                                                          |
| [ Selecionar equipamento cadastrado              v ]     |
|                                                          |
| [ + Cadastrar equipamento ]                              |
|                                                          |
| INFORMAÇÕES DO ATENDIMENTO                               |
|                                                          |
| Defeito relatado:                                        |
| +------------------------------------------------------+ |
| |                                                      | |
| |                                                      | |
| +------------------------------------------------------+ |
|                                                          |
| Data de entrada: [ DD/MM/AAAA ]                          |
|                                                          |
| Estado inicial: ABERTO                                   |
| Número da OS: GERADO AUTOMATICAMENTE                     |
|                                                          |
| [ CANCELAR ]                          [ CRIAR OS ]       |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Selecionar cliente existente.
- Selecionar equipamento vinculado ao cliente.
- Registrar defeito relatado.
- Registrar data de entrada.
- Gerar número único.
- Criar OS no estado Aberto.

### Validações

- Cliente obrigatório.
- Equipamento obrigatório.
- Defeito relatado obrigatório.
- Impedir associação inconsistente entre cliente e equipamento.

---

# 9. Protótipo 05 — Detalhes da Ordem de Serviço

**Objetivo:** centralizar todas as informações do atendimento.

**Referências:** UC-006 a UC-012, UC-014, UC-017, UC-018.

```text
+----------------------------------------------------------+
| ORDEM DE SERVIÇO #001                                    |
| Estado: EM DIAGNÓSTICO                                   |
+----------------------------------------------------------+
|                                                          |
| Cliente: Cliente Exemplo                                 |
| Telefone: (00) 00000-0000                                |
| Equipamento: Notebook                                    |
| Código interno: EQ-000125                                |
| Entrada: 10/10/2026                                      |
|                                                          |
| [ Dados Gerais ] [ Diagnóstico ] [ Orçamento ]           |
| [ Peças ] [ Fotos ] [ Financeiro ] [ Histórico ]          |
|                                                          |
| -------------------------------------------------------- |
|                                                          |
| CONTEÚDO DA ABA SELECIONADA                              |
|                                                          |
| Informações relacionadas à etapa do atendimento.         |
|                                                          |
| -------------------------------------------------------- |
|                                                          |
| [ EMITIR COMPROVANTE ]     [ ALTERAR ESTADO ]            |
+----------------------------------------------------------+
```

### Abas propostas

**Dados Gerais**

Cliente, equipamento, defeito e datas.

**Diagnóstico**

Conclusões da análise técnica.

**Orçamento**

Serviços, peças, valores e aprovação.

**Peças**

Itens vinculados à OS e sua origem.

**Fotos**

Registros fotográficos do atendimento.

**Financeiro**

Valor devido, pagamento e situação financeira.

**Histórico**

Informações anteriores e registros relevantes.

### Comportamentos esperados

- Centralizar informações da OS.
- Evitar navegação desnecessária entre várias telas.
- Exibir ações compatíveis com o estado do atendimento.
- Impedir operações não autorizadas.

---

# 10. Protótipo 06 — Cadastro de Clientes

**Objetivo:** registrar e consultar clientes.

**Referências:** UC-002, UC-003, US-004 a US-006.

```text
+----------------------------------------------------------+
| CLIENTES                               [ + NOVO CLIENTE ] |
+----------------------------------------------------------+
|                                                          |
| Buscar: [ Nome ou telefone                           ]   |
|                                                          |
| +------------------------------------------------------+ |
| | Nome               | Telefone       | Ações          | |
| |--------------------|----------------|----------------| |
| | Cliente Exemplo    | (00) 00000-0000| Ver detalhes   | |
| +------------------------------------------------------+ |
+----------------------------------------------------------+

              NOVO CLIENTE

+----------------------------------------------------------+
| Nome:                                                    |
| [                                                    ]   |
|                                                          |
| Telefone*:                                               |
| [                                                    ]   |
|                                                          |
| [ CANCELAR ]                          [ SALVAR ]          |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Cadastrar clientes.
- Exigir telefone.
- Pesquisar por nome ou telefone.
- Consultar histórico.
- Reutilizar cadastro existente.

**Pendente:** definir campos cadastrais adicionais e tratamento de duplicidades.

---

# 11. Protótipo 07 — Cadastro de Equipamentos

**Objetivo:** registrar e identificar equipamentos individualmente.

**Referências:** UC-004, US-007, US-008.

```text
+----------------------------------------------------------+
| CADASTRO DE EQUIPAMENTO                                  |
+----------------------------------------------------------+
|                                                          |
| Cliente: [ Selecionar cliente                       v ]  |
|                                                          |
| Tipo: [ Notebook / Desktop                          v ]  |
|                                                          |
| Marca: [                                             ]   |
|                                                          |
| Modelo: [                                            ]   |
|                                                          |
| Número de série de fábrica: [                        ]   |
|                                                          |
| Código interno: GERADO AUTOMATICAMENTE                   |
|                                                          |
| [ CANCELAR ]                         [ SALVAR ]           |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Gerar código interno único.
- Permitir equipamentos sem número de série geral.
- Registrar número de série quando disponível.
- Associar equipamento ao cliente.
- Permitir consulta por código interno.

**Funcionalidade futura:** impressão de etiquetas de identificação.

---

# 12. Protótipo 08 — Diagnóstico e Orçamento

**Objetivo:** registrar a análise e apresentar os valores do atendimento.

**Referências:** UC-007, UC-008, UC-009, US-015 a US-017.

```text
+----------------------------------------------------------+
| DIAGNÓSTICO E ORÇAMENTO — OS #001                         |
+----------------------------------------------------------+
|                                                          |
| Diagnóstico técnico:                                     |
| +------------------------------------------------------+ |
| |                                                      | |
| +------------------------------------------------------+ |
|                                                          |
| ORÇAMENTO                                                |
|                                                          |
| +------------------------------------------------------+ |
| | Descrição                   | Valor                  | |
| |-----------------------------|------------------------| |
| | Mão de obra                 | R$ 120,00              | |
| | Peça da assistência         | R$ 180,00              | |
| +------------------------------------------------------+ |
|                                                          |
| [ + ADICIONAR ITEM ]                                     |
|                                                          |
| TOTAL: R$ 300,00                                         |
|                                                          |
| Diagnóstico de R$ 50,00 incluído na mão de obra.         |
|                                                          |
| [ SALVAR ORÇAMENTO ]                                     |
|                                                          |
| Decisão do cliente:                                      |
|                                                          |
| [ APROVAR ]                 [ RECUSAR ]                   |
+----------------------------------------------------------+
```

Os valores apresentados são ilustrativos.

### Comportamentos esperados

- Registrar diagnóstico.
- Adicionar serviços e peças.
- Calcular total.
- Evitar cobrança duplicada de diagnóstico.
- Registrar aprovação ou recusa.
- Preservar orçamento no histórico.

### Situação de orçamento recusado

Quando o orçamento for recusado e não houver outros serviços autorizados, o sistema deverá considerar o diagnóstico de R$ 50,00 como valor devido.

---

# 13. Protótipo 09 — Financeiro

**Objetivo:** registrar pagamentos e consultar recebimentos.

**Referências:** UC-010, US-018, US-019.

```text
+----------------------------------------------------------+
| FINANCEIRO — OS #001                                     |
+----------------------------------------------------------+
|                                                          |
| Valor devido:                  R$ 300,00                 |
|                                                          |
| Situação:                      PENDENTE                  |
|                                                          |
| FORMA DE PAGAMENTO                                       |
|                                                          |
| [ Pix                                              v ]   |
|                                                          |
| Valor recebido: [ R$ 300,00                          ]   |
|                                                          |
| [ REGISTRAR PAGAMENTO INTEGRAL ]                         |
|                                                          |
| -------------------------------------------------------- |
|                                                          |
| HISTÓRICO DE PAGAMENTOS                                  |
|                                                          |
| Data       | OS    | Forma       | Valor                  |
| -----------|-------|-------------|----------------------- |
| 10/10/2026 | 001   | Pix         | R$ 300,00              |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Registrar pagamento manualmente.
- Associar pagamento à OS.
- Registrar forma de pagamento.
- Impedir pagamento parcial.
- Atualizar situação financeira.
- Impedir encerramento com saldo pendente.

### Formas de pagamento

- Pix.
- Dinheiro.
- Débito.
- Crédito.
- Criptomoedas.

**Pendente:** detalhar o registro de pagamentos em criptomoedas e as correções financeiras.

---

# 14. Protótipo 10 — Estoque

**Objetivo:** consultar peças e registrar movimentações.

**Referências:** UC-013 a UC-015, US-020 a US-022.

```text
+----------------------------------------------------------+
| ESTOQUE                                  [ + NOVA PEÇA ]  |
+----------------------------------------------------------+
|                                                          |
| Buscar peça: [                                       ]   |
|                                                          |
| +------------------------------------------------------+ |
| | Peça             | Quantidade disponível | Ações     | |
| |------------------|-----------------------|-----------| |
| | Memória RAM      |          10           | Detalhes  | |
| | SSD              |           5           | Detalhes  | |
| | Fonte            |           3           | Detalhes  | |
| +------------------------------------------------------+ |
|                                                          |
| [ CONSULTAR MOVIMENTAÇÕES ]                              |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Cadastrar peças.
- Consultar quantidades.
- Registrar retirada para OS.
- Registrar devolução de peças não utilizadas.
- Preservar movimentações.
- Distinguir peças da empresa e peças fornecidas pelo cliente.

**Pendente:** definir o procedimento de confirmação de peças utilizadas.

---

# 15. Protótipo 11 — Fotografias

**Objetivo:** documentar as condições do equipamento.

**Referências:** UC-017, US-023.

```text
+----------------------------------------------------------+
| FOTOGRAFIAS — OS #001                                    |
+----------------------------------------------------------+
|                                                          |
| [ + ADICIONAR FOTOGRAFIA ]                               |
|                                                          |
| Categoria: [ Recebimento / Após manutenção          v ]  |
|                                                          |
| FOTOGRAFIAS DO RECEBIMENTO                               |
|                                                          |
| +--------------+  +--------------+                      |
| |              |  |              |                      |
| |    FOTO 1    |  |    FOTO 2    |                      |
| |              |  |              |                      |
| +--------------+  +--------------+                      |
|                                                          |
| FOTOGRAFIAS APÓS MANUTENÇÃO                              |
|                                                          |
| +--------------+                                         |
| |              |                                         |
| |    FOTO 3    |                                         |
| |              |                                         |
| +--------------+                                         |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Anexar múltiplas imagens.
- Classificar fotografias.
- Consultar imagens anteriores.
- Preservar registros no histórico.

**Pendente:** definir formatos, tamanhos máximos e permissões para exclusão.

---

# 16. Protótipo 12 — Comprovante de Recebimento

**Objetivo:** apresentar a estrutura inicial do documento PDF.

**Referências:** UC-018, US-024.

```text
+----------------------------------------------------------+
|                   ASSISTÊNCIA TÉCNICA                    |
|                                                          |
|              COMPROVANTE DE RECEBIMENTO                  |
+----------------------------------------------------------+
|                                                          |
| Ordem de Serviço: 001                                    |
| Data de Entrada: 10/10/2026                              |
|                                                          |
| DADOS DO CLIENTE                                         |
|                                                          |
| Nome: Cliente Exemplo                                    |
| Telefone: (00) 00000-0000                                |
|                                                          |
| DADOS DO EQUIPAMENTO                                     |
|                                                          |
| Tipo: Notebook                                           |
| Marca: Exemplo                                           |
| Modelo: Exemplo                                          |
| Número de série: Quando disponível                       |
| Código interno: EQ-000125                                |
|                                                          |
| DEFEITO RELATADO                                         |
|                                                          |
| Equipamento não liga.                                    |
|                                                          |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Gerar PDF a partir da OS.
- Apresentar informações obrigatórias.
- Permitir impressão.
- Permitir compartilhamento manual.
- Permitir emissão posterior.

**Pendente:** definir termos de recebimento e eventual campo de assinatura.

---

# 17. Protótipo 13 — Funcionários

**Objetivo:** organizar o cadastro administrativo de funcionários.

**Referências:** UC-020, US-003.

```text
+----------------------------------------------------------+
| FUNCIONÁRIOS                         [ + NOVO CADASTRO ]  |
+----------------------------------------------------------+
|                                                          |
| Buscar funcionário: [                                ]   |
|                                                          |
| +------------------------------------------------------+ |
| | Funcionário        | Informações | Ações             | |
| |--------------------|-------------|-------------------| |
| | Funcionário 01     | Consultar   | Ver detalhes      | |
| +------------------------------------------------------+ |
+----------------------------------------------------------+
```

### Comportamentos esperados

- Cadastrar funcionários.
- Consultar informações autorizadas.
- Restringir acesso conforme permissões.

**Pendente:** definir campos cadastrais e matriz de permissões.

---

# 18. Fluxo de Navegação — Atendimento Completo

O fluxo principal proposto para o atendimento será:

1. Gerente acessa o sistema.
2. Localiza ou cadastra o cliente.
3. Localiza ou cadastra o equipamento.
4. Abre a ordem de serviço.
5. Gera o comprovante de recebimento.
6. Registra o diagnóstico.
7. Elabora o orçamento.
8. Registra a decisão do cliente.
9. Se aprovado, acompanha a manutenção.
10. Registra a conclusão do serviço.
11. Registra o pagamento integral na retirada.
12. Confirma a retirada do equipamento.
13. Encerra a ordem de serviço.

### Fluxo alternativo — Orçamento recusado

1. O cliente recusa o orçamento.
2. O gerente registra a recusa.
3. O diagnóstico permanece devido.
4. O cliente realiza o pagamento integral na retirada.
5. O gerente confirma a retirada.
6. A OS é encerrada.

### Fluxo alternativo — Cancelamento

O cancelamento deverá seguir as regras específicas que ainda serão refinadas, incluindo o tratamento financeiro e das peças vinculadas.

---

# 19. Estados Visuais

A interface deverá distinguir os estados das ordens de serviço.

| Estado | Identificação textual |
|---|---|
| Aberto | Aberto |
| Em diagnóstico | Em diagnóstico |
| Aguardando aprovação | Aguardando aprovação |
| Em manutenção | Em manutenção |
| Concluído | Concluído |
| Encerrado | Encerrado |
| Orçamento recusado | Orçamento recusado |
| Cancelado | Cancelado |

**Diretriz proposta:** associar cores aos estados para facilitar a leitura, mantendo sempre o texto visível.

A paleta de cores será definida durante o design visual.

---

# 20. Requisitos de Usabilidade Propostos

As seguintes diretrizes deverão ser avaliadas durante a implementação:

### 20.1 Navegação consistente

Manter o mesmo padrão de menu, cabeçalho e ações nas diferentes telas.

### 20.2 Validação de formulários

Apresentar mensagens claras quando campos obrigatórios não forem preenchidos.

### 20.3 Ações críticas

Solicitar confirmação antes de operações relevantes, como cancelamento de ordens de serviço.

### 20.4 Feedback de operações

Informar ao usuário quando uma operação for concluída ou não puder ser realizada.

### 20.5 Organização visual

Utilizar hierarquia de títulos, agrupamento de campos e espaçamento adequado.

### 20.6 Acessibilidade

Evitar que informações importantes dependam exclusivamente de cores.

---

# 21. Limitações dos Protótipos

Os protótipos apresentados não definem:

- Identidade visual definitiva.
- Paleta de cores.
- Tipografia.
- Biblioteca de componentes.
- Framework frontend.
- Estrutura técnica das páginas.
- Responsividade detalhada.
- Animações e interações avançadas.

Essas decisões deverão ser tratadas na etapa de design e arquitetura.

---

# 22. Validação dos Protótipos

Antes da implementação, os protótipos deverão ser revisados quanto a:

1. Correspondência com os requisitos funcionais.
2. Respeito às regras de negócio.
3. Facilidade de navegação.
4. Clareza dos formulários.
5. Visibilidade dos estados das OS.
6. Organização das informações financeiras.
7. Facilidade para consultar clientes e equipamentos.
8. Consistência das ações disponíveis.
9. Adequação ao escopo do MVP.

Alterações aprovadas deverão ser registradas na documentação.

---

# 23. Encerramento

Este documento apresenta **13 protótipos textuais de baixa fidelidade** e uma proposta de navegação para o Sistema de Ordens de Serviço.

Os protótipos oferecem uma referência inicial para o desenvolvimento das interfaces, sem estabelecer ainda o design visual definitivo.
