# 08 — Decisões Técnicas e Arquitetura Inicial

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Documento:** Arquitetura Inicial e Registros de Decisão Arquitetural  
**Versão:** 1.0 — Proposta inicial  
**Status:** Em avaliação — decisões técnicas pendentes

**Documentos de referência:**
- `01-visao-do-projeto.md`
- `02-levantamento-requisitos.md`
- `03-requisitos.md`
- `04-regras-de-negocio.md`
- `05-historias-usuario.md`
- `06-casos-de-uso.md`
- `07-prototipos.md`

---

## 1. Objetivo

Este documento apresenta as diretrizes arquiteturais iniciais e registra as decisões que orientarão o desenvolvimento do Sistema de Ordens de Serviço para Assistência Técnica.

Seu objetivo é:

- Identificar as principais responsabilidades do sistema.
- Propor uma organização arquitetural.
- Registrar decisões e alternativas.
- Documentar justificativas técnicas.
- Identificar riscos e dependências.
- Apoiar a escolha das tecnologias.
- Facilitar a manutenção e evolução do projeto.

A arquitetura será refinada conforme as necessidades do MVP forem priorizadas.

---

# 2. Contexto Arquitetural

O sistema será utilizado por uma assistência técnica para controlar clientes, equipamentos, ordens de serviço, diagnósticos, orçamentos, pagamentos, estoque e documentos.

A solução deverá considerar:

- Utilização por uma única empresa.
- Usuários internos com autenticação.
- Perfis iniciais Gerente e RH.
- Interface web.
- Necessidade de utilização em Windows.
- Armazenamento persistente dos registros.
- Preservação do histórico.
- Emissão de comprovantes em PDF.
- Armazenamento de fotografias.
- Consistência das operações financeiras e de estoque.

O sistema não terá, inicialmente, processamento automático de pagamentos nem portais próprios para clientes e técnicos.

---

# 3. Diretrizes Arquiteturais

As seguintes diretrizes são propostas para orientar a implementação.

## 3.1 Separação de responsabilidades

A aplicação deverá evitar misturar:

- Interface do usuário.
- Regras de negócio.
- Persistência de dados.
- Integrações externas.
- Geração de documentos.

Essa separação deverá facilitar testes e manutenção.

## 3.2 Centralização das regras de negócio

As regras que determinam operações permitidas deverão ser aplicadas na camada responsável pela lógica de negócio.

Exemplos:

- Impedir encerramento de OS com saldo pendente.
- Evitar reutilização de números de OS.
- Impedir pagamento parcial.
- Evitar cobrança duplicada de diagnóstico.
- Preservar o histórico de cancelamentos.
- Controlar devolução de peças não utilizadas.

A interface poderá antecipar validações para melhorar a experiência, mas não deverá ser a única responsável por garantir essas regras.

## 3.3 Consistência dos dados

Operações que modificam informações relacionadas deverão preservar a integridade dos registros.

Exemplo:

Ao retirar uma peça do estoque para uma OS, o sistema deverá registrar a movimentação e atualizar a quantidade disponível de maneira consistente.

## 3.4 Segurança desde o início

A arquitetura deverá considerar:

- Autenticação.
- Autorização.
- Proteção dos dados.
- Validação de entradas.
- Tratamento de erros.
- Proteção de credenciais.
- Restrição de operações administrativas.

Os mecanismos específicos serão escolhidos durante a implementação.

## 3.5 Evolução incremental

A arquitetura deverá permitir desenvolver o produto em etapas, começando pelas funcionalidades prioritárias do MVP.

Não será necessário implementar toda a arquitetura definitiva antes da primeira entrega funcional.

---

# 4. Arquitetura Lógica Proposta

Uma alternativa inicial é utilizar uma arquitetura em camadas.

```text
+--------------------------------------------------+
|                  INTERFACE                       |
|                                                  |
|  Dashboard | Clientes | Equipamentos | OS        |
|  Orçamentos | Financeiro | Estoque               |
+------------------------+-------------------------+
                         |
                         v
+--------------------------------------------------+
|                 APLICAÇÃO                        |
|                                                  |
|  Casos de uso e coordenação das operações        |
|                                                  |
|  Criar OS | Registrar pagamento | Encerrar OS    |
|  Elaborar orçamento | Movimentar estoque         |
+------------------------+-------------------------+
                         |
                         v
+--------------------------------------------------+
|                   DOMÍNIO                        |
|                                                  |
|  Entidades | Regras de negócio | Validações      |
|                                                  |
|  Cliente | Equipamento | Ordem de Serviço        |
|  Orçamento | Pagamento | Peça                    |
+------------------------+-------------------------+
                         |
                         v
+--------------------------------------------------+
|                INFRAESTRUTURA                    |
|                                                  |
|  Banco de dados | Arquivos | PDF | Segurança     |
|  Repositórios | Serviços externos               |
+--------------------------------------------------+
```

Essa representação é conceitual.

Ela não determina ainda a estrutura exata de pastas, classes, módulos ou serviços.

---

# 5. Responsabilidades das Camadas

## 5.1 Interface

Responsável pela interação com os usuários.

Exemplos:

- Apresentar formulários.
- Exibir informações.
- Mostrar mensagens de erro.
- Disponibilizar ações.
- Exibir indicadores.
- Permitir navegação.

A interface não deverá ser a única responsável pela aplicação das regras de negócio.

## 5.2 Aplicação

Responsável por coordenar os casos de uso.

Exemplos:

- Criar uma ordem de serviço.
- Registrar um diagnóstico.
- Elaborar um orçamento.
- Registrar um pagamento.
- Encerrar uma OS.
- Cancelar uma OS.
- Movimentar o estoque.

A camada de aplicação deverá coordenar as operações necessárias para alcançar cada objetivo.

## 5.3 Domínio

Responsável pelos conceitos e regras centrais do negócio.

Exemplos:

- Uma OS precisa possuir identificação única.
- O diagnóstico não pode ser cobrado duas vezes.
- Pagamentos parciais não são permitidos.
- Uma OS não pode ser encerrada com saldo pendente.
- Peças consumidas não retornam automaticamente ao estoque.

O domínio deverá representar as regras independentemente dos detalhes de interface e persistência, sempre que viável.

## 5.4 Infraestrutura

Responsável pelos mecanismos técnicos necessários à operação.

Exemplos:

- Acesso ao banco de dados.
- Armazenamento de fotografias.
- Geração de arquivos PDF.
- Implementação de repositórios.
- Serviços de autenticação.
- Registro de logs.

---

# 6. Modelo Conceitual de Dados

As entidades iniciais identificadas são:

| Entidade | Responsabilidade |
|---|---|
| Usuário | Representar quem acessa o sistema |
| Funcionário | Armazenar informações administrativas |
| Cliente | Representar o proprietário atendido |
| Equipamento | Identificar individualmente o equipamento |
| Ordem de Serviço | Registrar e acompanhar o atendimento |
| Diagnóstico | Registrar conclusões da análise |
| Orçamento | Registrar proposta de reparo |
| Item de Orçamento | Representar serviços e peças cobrados |
| Pagamento | Registrar quitação financeira |
| Peça | Representar item controlado em estoque |
| Movimentação de Estoque | Registrar entradas, retiradas e devoluções |
| Fotografia | Representar arquivo associado à OS |

A relação exata entre Usuário e Funcionário ainda deverá ser definida.

---

# 7. Relacionamentos Conceituais

```text
CLIENTE
  |
  +---- possui ----> EQUIPAMENTO
  |                       |
  |                       +---- possui ----> ORDEM DE SERVIÇO
  |                                               |
  +---------------- vinculado a ------------------+
                                                  |
                                                  +---- DIAGNÓSTICO
                                                  |
                                                  +---- ORÇAMENTO
                                                  |         |
                                                  |         +---- ITENS
                                                  |
                                                  +---- PAGAMENTO
                                                  |
                                                  +---- FOTOGRAFIAS
                                                  |
                                                  +---- PEÇAS UTILIZADAS
                                                            |
                                                            v
                                                    MOVIMENTAÇÕES
                                                      DE ESTOQUE
```

### Relações iniciais

- Um cliente poderá possuir vários equipamentos.
- Um equipamento poderá possuir várias ordens de serviço.
- Uma ordem de serviço pertencerá a um equipamento.
- Uma ordem de serviço estará associada a um cliente.
- Uma OS poderá possuir diagnóstico.
- Uma OS poderá possuir orçamento.
- Um orçamento poderá possuir vários itens.
- Uma OS poderá possuir fotografias.
- Uma OS poderá possuir registros de movimentação de peças.
- Uma OS poderá possuir registro de pagamento.

**Pendente:** definir cardinalidades completas, campos obrigatórios e políticas de alteração dos registros.

---

# 8. Registros de Decisão Arquitetural (ADRs)

Os ADRs documentam decisões importantes e suas consequências.

Cada registro utilizará:

- Identificador.
- Título.
- Estado.
- Contexto.
- Decisão.
- Justificativa.
- Consequências.

Estados possíveis:

- **Aceito:** decisão confirmada.
- **Proposto:** alternativa recomendada para avaliação.
- **Pendente:** decisão ainda não tomada.
- **Substituído:** decisão posteriormente alterada.

---

## ADR-001 — Escopo de Empresa Única

**Estado:** Aceito

### Contexto

O sistema foi concebido inicialmente para atender uma única assistência técnica.

### Decisão

A primeira versão não exigirá suporte a múltiplas empresas.

### Justificativa

O escopo inicial não apresenta necessidade de gerenciamento multiempresa.

### Consequências

- Menor complexidade funcional inicial.
- Não será necessário desenvolver recursos de cadastro e administração de múltiplas empresas no MVP.
- Uma futura expansão poderá exigir revisão do modelo de dados e das regras de isolamento.

**Referências:** RN-048, RNF-014.

---

## ADR-002 — Controle de Acesso por Perfis

**Estado:** Aceito quanto ao princípio; detalhamento pendente.

### Contexto

O sistema será utilizado por funcionários com responsabilidades diferentes.

### Decisão

O acesso às operações deverá considerar os perfis Gerente e RH.

### Justificativa

Nem todos os usuários deverão possuir as mesmas permissões.

### Consequências

- A solução precisará de autenticação e autorização.
- As operações protegidas deverão verificar permissões.
- A matriz detalhada de permissões ainda precisa ser aprovada.

**Referências:** RF-001, RF-002, RN-045, RN-046.

---

## ADR-003 — Identificação Única de Equipamentos

**Estado:** Aceito

### Contexto

Equipamentos semelhantes podem pertencer ao mesmo cliente ou não possuir número de série geral de fábrica.

### Decisão

Cada equipamento receberá um identificador interno único gerado pelo sistema.

O número de série de fábrica será registrado separadamente quando disponível.

### Justificativa

A identificação interna evita dependência exclusiva de informações fornecidas pelo fabricante.

### Consequências

- O banco de dados deverá preservar a unicidade do identificador.
- O código não poderá ser reutilizado.
- O identificador poderá ser utilizado em etiquetas.

**Referências:** RF-009 a RF-011, RN-005 a RN-007.

---

## ADR-004 — Preservação do Histórico das OS

**Estado:** Aceito

### Contexto

O histórico de atendimentos é necessário para acompanhar equipamentos e clientes.

### Decisão

O cancelamento de uma ordem de serviço não resultará em sua exclusão definitiva.

### Justificativa

A assistência precisa preservar registros anteriores e permitir consultas futuras.

### Consequências

- O cancelamento será representado por estado.
- Os números das ordens não poderão ser reutilizados.
- Consultas e indicadores deverão distinguir ordens ativas e canceladas.
- Políticas de retenção e exclusão de dados deverão ser avaliadas separadamente.

**Referências:** RF-023, RN-030 a RN-032.

---

## ADR-005 — Registro Manual de Pagamentos

**Estado:** Aceito

### Contexto

A assistência precisa registrar pagamentos, mas não foi solicitada integração financeira automática na primeira versão.

### Decisão

Os pagamentos serão registrados manualmente por usuários autorizados.

### Justificativa

A necessidade inicial é controlar recebimentos, não processar transações financeiras.

### Consequências

- Não será necessária integração com gateway de pagamento no MVP.
- O sistema dependerá da confirmação manual do recebimento.
- Serão necessárias validações para impedir pagamentos parciais.
- Correções financeiras exigirão regras específicas.

**Referências:** RF-031 a RF-037, RN-022 a RN-027.

---

## ADR-006 — Arquitetura em Camadas

**Estado:** Proposto

### Contexto

O sistema possui diferentes áreas funcionais e regras de negócio que precisam ser mantidas de maneira consistente.

### Proposta

Organizar a solução em responsabilidades de interface, aplicação, domínio e infraestrutura.

### Justificativa

Essa separação poderá melhorar a organização, a testabilidade e a manutenção.

### Consequências esperadas

**Vantagens:**
- Separação das responsabilidades.
- Facilidade de testes.
- Maior clareza na localização das regras de negócio.
- Possibilidade de evolução incremental.

**Desvantagens:**
- Exige disciplina na organização do código.
- Pode adicionar complexidade desnecessária se aplicada de forma excessiva.

### Alternativas

- Arquitetura monolítica simples.
- Monólito modular.
- Arquitetura em camadas.
- Arquitetura hexagonal.

**Decisão final:** pendente.

---

## ADR-007 — Estratégia de Aplicação Web e Windows

**Estado:** Pendente

### Contexto

O sistema deverá possuir interface web e atender à necessidade de utilização em computadores Windows.

### Alternativas

**Alternativa A — Aplicação web responsiva**

A solução funciona diretamente no navegador.

**Alternativa B — Aplicação web com empacotamento desktop**

Uma aplicação web é disponibilizada também por meio de um aplicativo para Windows.

**Alternativa C — Aplicação desktop específica**

Uma interface própria para Windows é desenvolvida separadamente.

### Critérios de avaliação

- Facilidade de desenvolvimento.
- Custo de manutenção.
- Distribuição de atualizações.
- Experiência de uso.
- Compatibilidade com Windows.
- Segurança.
- Necessidade de operação offline.

### Decisão final

Ainda não definida.

---

## ADR-008 — Linguagem e Framework Backend

**Estado:** Pendente

### Contexto

O sistema precisará implementar regras de negócio, operações de cadastro, controle de estoque e registros financeiros.

### Alternativas a avaliar

- Python com FastAPI.
- Node.js com TypeScript.
- Outras tecnologias compatíveis com o escopo.

### Critérios de avaliação

- Conhecimento da equipe.
- Facilidade de manutenção.
- Bibliotecas disponíveis.
- Testabilidade.
- Integração com banco de dados.
- Custo operacional.
- Complexidade de implantação.

### Decisão final

Ainda não definida.

---

## ADR-009 — Tecnologia Frontend

**Estado:** Pendente

### Contexto

O sistema precisa disponibilizar uma interface administrativa com formulários, tabelas, filtros e indicadores.

### Alternativas a avaliar

- React com TypeScript.
- Outra biblioteca ou framework web.
- Interface renderizada pelo servidor.

### Critérios de avaliação

- Complexidade da interface.
- Facilidade de manutenção.
- Reutilização de componentes.
- Integração com backend.
- Experiência de desenvolvimento.
- Possibilidade de distribuição no Windows.

### Decisão final

Ainda não definida.

---

## ADR-010 — Banco de Dados

**Estado:** Pendente

### Contexto

O sistema precisará armazenar dados relacionados de clientes, equipamentos, ordens, pagamentos e estoque.

### Alternativas a avaliar

- PostgreSQL.
- SQLite.
- Outro banco de dados compatível.

### Critérios de avaliação

- Integridade referencial.
- Suporte a transações.
- Volume de dados esperado.
- Operação simultânea por usuários.
- Facilidade de backup.
- Custos de hospedagem.
- Facilidade de manutenção.

### Decisão final

Ainda não definida.

---

## ADR-011 — Armazenamento de Fotografias

**Estado:** Pendente

### Contexto

As ordens de serviço poderão possuir múltiplas fotografias.

### Alternativas a avaliar

- Armazenamento em diretório controlado pelo servidor.
- Armazenamento de objetos.
- Outro serviço de arquivos compatível.

### Critérios de avaliação

- Segurança.
- Custos.
- Facilidade de backup.
- Controle de acesso.
- Recuperação de arquivos.
- Escalabilidade.

### Decisão final

Ainda não definida.

---

## ADR-012 — Geração de PDF

**Estado:** Pendente

### Contexto

O sistema deverá gerar comprovantes de recebimento.

### Alternativas a avaliar

- Geração de PDF no backend.
- Geração de PDF no frontend.
- Serviço específico de geração de documentos.

### Critérios de avaliação

- Consistência do documento.
- Facilidade de manutenção do modelo.
- Segurança dos dados.
- Compatibilidade com impressão.
- Possibilidade de reemissão.

### Decisão final

Ainda não definida.

---

## ADR-013 — Autorização de Dispositivos

**Estado:** Pendente

### Contexto

Existe a necessidade de restringir o acesso a computadores autorizados.

### Alternativas a avaliar

- Controle por usuários e permissões.
- Controle de acesso por rede privada.
- VPN.
- Gerenciamento de dispositivos autorizados.
- Combinação de mecanismos.

### Observação

Autenticar um usuário não significa, por si só, comprovar que o dispositivo utilizado está autorizado.

### Decisão final

Ainda não definida.

---

## ADR-014 — Estratégia de Implantação

**Estado:** Pendente

### Contexto

O sistema poderá precisar ser acessado por mais de um usuário e deverá preservar os dados de maneira confiável.

### Alternativas a avaliar

- Hospedagem em servidor local.
- Hospedagem em nuvem.
- Arquitetura híbrida.

### Critérios de avaliação

- Custo mensal.
- Disponibilidade.
- Segurança.
- Facilidade de manutenção.
- Backup.
- Necessidade de acesso remoto.
- Dependência de conexão com a internet.

### Decisão final

Ainda não definida.

---

# 9. Estratégia de Segurança Proposta

A implementação deverá considerar os seguintes controles:

## 9.1 Autenticação

Verificar a identidade do usuário antes de permitir o acesso.

## 9.2 Autorização

Verificar as permissões do usuário para cada operação protegida.

## 9.3 Validação de dados

Validar informações recebidas pelo sistema antes de processá-las.

## 9.4 Proteção de credenciais

Não armazenar senhas em texto puro.

Utilizar mecanismos apropriados de armazenamento seguro de credenciais.

## 9.5 Controle de arquivos

Validar arquivos enviados e restringir seu acesso aos usuários autorizados.

## 9.6 Registro de eventos

Avaliar o registro de operações relevantes, especialmente:

- Cancelamento de OS.
- Registro e correção de pagamentos.
- Movimentações de estoque.
- Alterações administrativas.

A política de auditoria ainda deverá ser detalhada.

---

# 10. Estratégia de Testes Proposta

A implementação deverá considerar diferentes níveis de testes.

### 10.1 Testes unitários

Verificar regras de negócio isoladamente.

Exemplos:

- Cálculo do orçamento.
- Cobrança do diagnóstico.
- Validação de pagamento integral.
- Verificação de transições de estado.

### 10.2 Testes de integração

Verificar a interação entre componentes.

Exemplos:

- Criar OS e persistir os dados.
- Registrar movimentação de estoque.
- Registrar pagamento.
- Consultar histórico.

### 10.3 Testes de API

Caso seja adotada uma API, validar:

- Entradas.
- Respostas.
- Autenticação.
- Autorização.
- Tratamento de erros.

### 10.4 Testes de interface

Verificar os principais fluxos do usuário.

Exemplos:

- Cadastrar cliente.
- Abrir OS.
- Elaborar orçamento.
- Registrar pagamento.
- Encerrar atendimento.

### 10.5 Testes de regras críticas

Priorizar cenários que envolvam:

- Integridade financeira.
- Consistência de estoque.
- Identificadores únicos.
- Preservação do histórico.
- Restrições de encerramento.

---

# 11. Estratégia de Versionamento Proposta

O desenvolvimento poderá utilizar Git e GitHub.

### Branch principal

`main`

Representará a versão integrada e validada do projeto.

### Branches de trabalho

Exemplos:

- `docs/initial-discovery`
- `feature/client-registration`
- `feature/equipment-registration`
- `feature/service-orders`
- `fix/payment-validation`

### Fluxo sugerido

1. Criar uma GitHub Issue.
2. Definir critérios de aceitação.
3. Criar uma branch relacionada à tarefa.
4. Implementar a funcionalidade.
5. Executar testes.
6. Revisar as alterações.
7. Criar um commit.
8. Enviar a branch ao GitHub.
9. Abrir um Pull Request.
10. Revisar e integrar a alteração.

O padrão definitivo de nomes e a política de revisão serão estabelecidos no planejamento.

---

# 12. Organização de Código — Exemplo Conceitual

A estrutura abaixo é apenas uma referência para discussão.

```text
sistema-ordens-servico/
|
+-- docs/
|
+-- backend/
|   |
|   +-- src/
|   |   +-- application/
|   |   +-- domain/
|   |   +-- infrastructure/
|   |   +-- interfaces/
|   |
|   +-- tests/
|
+-- frontend/
|   |
|   +-- src/
|       +-- components/
|       +-- pages/
|       +-- services/
|       +-- types/
|
+-- .github/
|   +-- workflows/
|
+-- README.md
```

**Atenção:** essa estrutura não deverá ser criada automaticamente antes da escolha da stack e da organização arquitetural.

A estrutura real deverá ser adaptada à tecnologia escolhida e à complexidade do MVP.

---

# 13. Riscos Arquiteturais Identificados

| Risco | Impacto possível | Tratamento proposto |
|---|---|---|
| Escolher stack sem avaliar requisitos | Retrabalho | Registrar ADR antes da implementação |
| Regras apenas no frontend | Operações inconsistentes | Validar regras na lógica de negócio |
| Movimentação incorreta de estoque | Quantidades divergentes | Utilizar operações consistentes e testes |
| Pagamentos registrados incorretamente | Divergência financeira | Validação e futura trilha de auditoria |
| Fotografias sem política de armazenamento | Perda ou exposição de arquivos | Definir estratégia de arquivos e backup |
| Permissões incompletas | Acesso indevido | Refinar matriz de autorização |
| Arquitetura excessivamente complexa | Atraso no MVP | Preferir simplicidade e evolução incremental |
| Ausência de backups | Perda de dados | Definir estratégia de recuperação |

---

# 14. Pendências para Decisão

Antes de iniciar a implementação, será necessário avaliar as decisões que afetam diretamente o primeiro incremento do MVP.

### Decisões técnicas prioritárias

1. Modelo de implantação inicial.
2. Stack backend.
3. Stack frontend.
4. Banco de dados.
5. Organização arquitetural.
6. Estratégia inicial de autenticação.
7. Fluxo de desenvolvimento com Git e GitHub.

### Decisões que poderão ser adiadas

1. Empacotamento como aplicativo Windows.
2. Armazenamento definitivo de fotografias.
3. Solução definitiva de geração de PDF.
4. Integrações externas futuras.
5. Estratégias de escalabilidade avançada.

O adiamento dependerá das funcionalidades selecionadas para o MVP.

---

# 15. Critérios para Aprovação da Arquitetura

A arquitetura proposta deverá ser avaliada considerando:

- Atendimento aos requisitos prioritários.
- Simplicidade de implementação.
- Segurança.
- Consistência dos dados.
- Facilidade de testes.
- Facilidade de manutenção.
- Custos de desenvolvimento e operação.
- Conhecimento disponível.
- Possibilidade de evolução futura.

A decisão não deverá se basear apenas na popularidade das tecnologias.

---

# 16. Controle de Mudanças Arquiteturais

Quando uma decisão técnica relevante for tomada ou alterada:

1. Criar ou atualizar o ADR correspondente.
2. Registrar o contexto e as alternativas.
3. Documentar a justificativa.
4. Identificar consequências.
5. Atualizar a documentação relacionada.
6. Registrar a mudança no Git.

Decisões substituídas deverão permanecer documentadas para preservar o histórico técnico do projeto.

---

# 17. Encerramento

Este documento estabelece uma base para a definição da arquitetura do Sistema de Ordens de Serviço para Assistência Técnica.

Foram registrados **14 ADRs**, abrangendo decisões confirmadas do domínio, propostas arquiteturais e escolhas técnicas pendentes.

A arquitetura definitiva será selecionada considerando as necessidades do MVP e os recursos disponíveis.