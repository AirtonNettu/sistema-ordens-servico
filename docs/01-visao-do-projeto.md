# Visão do Projeto

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Status:** Visão inicial definida pelo responsável pelo projeto — pendente de revisão e aprovação formal  
**Finalidade:** Projeto-laboratório para aplicar práticas de Engenharia de Software, desde a análise de requisitos até a implementação e manutenção.

---

## 1. Contexto do Projeto

O projeto consiste no desenvolvimento de um sistema de gerenciamento de ordens de serviço destinado a uma pequena assistência técnica de computadores.

O sistema busca centralizar informações administrativas, operacionais e financeiras, substituindo processos manuais ou informações dispersas em papéis, planilhas e aplicativos de mensagens.

A primeira versão será destinada a uma única empresa.

## 2. Problema a Resolver

Pequenas assistências técnicas podem enfrentar dificuldades para organizar atendimentos, cadastrar clientes, elaborar orçamentos, calcular valores, controlar pagamentos e acompanhar ordens de serviço.

A utilização de registros descentralizados pode provocar erros de cálculo, retrabalho, dificuldades de consulta e perda de informações.

O problema central identificado é a ausência de uma ferramenta integrada que simplifique e automatize essas atividades.

## 3. Objetivo Geral

Desenvolver um sistema de gerenciamento de ordens de serviço que simplifique, centralize e automatize os processos administrativos, operacionais e financeiros de uma assistência técnica de computadores.

O sistema deverá facilitar o registro e a consulta de informações, reduzir tarefas manuais e melhorar o acompanhamento dos atendimentos.

## 4. Objetivos Específicos

- Centralizar os cadastros de clientes e funcionários.
- Organizar a criação e o acompanhamento das ordens de serviço.
- Automatizar a numeração das ordens de serviço.
- Facilitar a elaboração de orçamentos e o cálculo de valores.
- Apoiar o controle financeiro e o registro de pagamentos.
- Gerenciar o estoque de peças.
- Automatizar a atualização do estoque quando peças forem registradas nas ordens de serviço.
- Disponibilizar acesso pelo navegador e por aplicativo Windows.
- Controlar o acesso conforme o perfil do usuário.

## 5. Stakeholders e Usuários

### 5.1 Gerente

Responsável pela administração da assistência técnica.

Atividades previstas:

- Gerenciar clientes e ordens de serviço.
- Acompanhar orçamentos e serviços.
- Consultar e gerenciar informações financeiras.
- Acompanhar os processos operacionais da empresa.

### 5.2 Recursos Humanos (RH)

Responsável por atividades administrativas e de gestão de funcionários.

Atividades previstas:

- Cadastrar e gerenciar funcionários.
- Controlar informações administrativas.
- Consultar e gerenciar informações financeiras.

### 5.3 Clientes

São as pessoas que solicitam serviços à assistência técnica.

Seus dados serão cadastrados no sistema, mas não terão acesso direto à plataforma na primeira versão.

### 5.4 Técnicos

Participam da execução dos serviços de manutenção, mas não terão acesso direto ao sistema na primeira versão.

Suas necessidades operacionais ainda deverão ser investigadas durante o levantamento de requisitos.

## 6. Escopo do Projeto

### 6.1 Funcionalidades incluídas

- Cadastro e gerenciamento de clientes.
- Cadastro e gerenciamento de funcionários.
- Criação e acompanhamento de ordens de serviço.
- Numeração automática e sequencial das ordens de serviço.
- Elaboração e acompanhamento de orçamentos.
- Cálculo automático de valores.
- Controle financeiro e registro de pagamentos.
- Cadastro e controle de estoque.
- Registro de peças utilizadas em serviços.
- Atualização automática do estoque.
- Autenticação e controle de acesso por perfil.
- Interface web e aplicativo Windows.

### 6.2 Funcionalidades não incluídas inicialmente

- Gerenciamento de múltiplas empresas independentes.
- Portal de acesso para clientes.
- Acesso direto de técnicos ao sistema.

Outras exclusões poderão ser definidas durante o levantamento de requisitos.

### 6.3 Produto mínimo viável (MVP)

O conjunto mínimo de funcionalidades necessário para a primeira entrega ainda será definido após o levantamento e a priorização dos requisitos.

As funcionalidades previstas no escopo não representam, necessariamente, entregas obrigatórias da primeira versão operacional.

## 7. Plataformas e Condições de Acesso

O sistema deverá disponibilizar duas formas de acesso:

- **Aplicação web:** utilização por meio de navegador.
- **Aplicativo Windows:** utilização por meio de programa instalado.

As interfaces deverão trabalhar com informações consistentes.

Condições previstas:

- **Gerente:** acesso por computador pessoal autorizado.
- **RH:** acesso restrito a computador autorizado da empresa.

Os mecanismos de autenticação, autorização e restrição por dispositivo serão especificados posteriormente.

## 8. Diretrizes Iniciais de Automação

### 8.1 Ordens de serviço

Cada nova ordem de serviço deverá receber automaticamente uma numeração sequencial e única.

### 8.2 Controle de estoque

O sistema deverá atualizar automaticamente a quantidade disponível de uma peça quando seu uso for registrado em uma ordem de serviço.

As condições de cancelamento, devolução e correção de movimentações serão investigadas durante o levantamento de requisitos.

### 8.3 Operações financeiras

O sistema deverá apoiar o cálculo automático de valores de serviços e o acompanhamento de pagamentos.

As fórmulas, condições de pagamento e regras financeiras serão definidas posteriormente.

## 9. Questões em Aberto

1. Qual será o fluxo completo de uma ordem de serviço, desde a abertura até o encerramento?
2. Quais informações serão obrigatórias no cadastro de clientes e equipamentos?
3. Como serão realizados a aprovação e o cancelamento de orçamentos?
4. Quais serão os estados possíveis de uma ordem de serviço?
5. Como funcionarão cancelamentos, devoluções e ajustes de estoque?
6. Quais operações financeiras serão permitidas a cada perfil?
7. Como será aplicada a restrição de acesso por computador?
8. Quais funcionalidades serão prioritárias para o MVP?
9. Quais indicadores permitirão avaliar se o sistema atingiu seus objetivos?

## 10. Critérios de Validação da Visão

A visão do projeto será considerada aprovada quando o responsável pelo projeto confirmar:

- O problema de negócio.
- Os objetivos pretendidos.
- Os perfis de usuário.
- O escopo inicial e suas exclusões.
- As plataformas e condições gerais de acesso.
- As principais diretrizes de automação.

A aprovação da visão não substitui a validação