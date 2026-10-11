# 02 — Levantamento de Requisitos

**Projeto:** Sistema de Ordens de Serviço para Assistência Técnica  
**Fase:** Engenharia de Requisitos — Levantamento  
**Status:** Consolidado — sujeito a refinamentos  
**Responsável:** Responsável pelo projeto  
**Técnica utilizada:** Entrevista simulada com o responsável pelo negócio

---

## 1. Objetivo do documento

Este documento apresenta as necessidades, expectativas e decisões identificadas durante o levantamento de requisitos do Sistema de Ordens de Serviço para Assistência Técnica.

O objetivo desta etapa é compreender o problema de negócio e identificar as funcionalidades necessárias antes de iniciar o desenvolvimento.

As informações levantadas serão utilizadas na elaboração dos requisitos funcionais, requisitos não funcionais, regras de negócio, histórias de usuário e casos de uso.

Este documento registra **o que o negócio precisa**, sem determinar antecipadamente como cada funcionalidade será implementada.

---

## 2. Contexto do negócio

A assistência técnica realiza atendimentos relacionados à manutenção de computadores e notebooks.

O processo envolve:

- Recebimento de equipamentos.
- Cadastro de clientes.
- Identificação dos equipamentos.
- Registro de defeitos relatados.
- Diagnóstico técnico.
- Elaboração de orçamentos.
- Aprovação ou recusa de serviços.
- Execução de manutenções.
- Controle de peças.
- Registro de pagamentos.
- Entrega dos equipamentos.
- Consulta do histórico de atendimentos.

O sistema deverá centralizar essas informações, reduzindo a dependência de registros em papel, mensagens e controles separados.

---

## 3. Usuários e envolvidos

### 3.1 Gerente

Responsável pela operação dos atendimentos.

Necessidades identificadas:

- Cadastrar e consultar clientes.
- Cadastrar e identificar equipamentos.
- Criar e acompanhar ordens de serviço.
- Registrar diagnósticos.
- Elaborar orçamentos.
- Registrar serviços e peças.
- Controlar o andamento das manutenções.
- Consultar históricos.
- Registrar pagamentos.
- Acompanhar informações financeiras.

### 3.2 RH

Usuário interno com responsabilidades administrativas.

Necessidades identificadas:

- Cadastrar e gerenciar informações de funcionários.
- Consultar informações administrativas autorizadas.
- Registrar pagamentos.
- Acessar informações financeiras conforme suas permissões.

### 3.3 Cliente

Pessoa que solicita o atendimento e entrega o equipamento.

Na primeira versão, o cliente não terá acesso direto ao sistema.

### 3.4 Técnico

Profissional responsável pelo diagnóstico ou pela manutenção.

Na primeira versão, não foi definido um perfil próprio de acesso para técnicos.

---

## 4. Necessidades levantadas

### 4.1 Cadastro de clientes

O sistema deverá permitir cadastrar clientes e reutilizar seus dados em atendimentos futuros.

**Decisões confirmadas:**

- O telefone de contato será obrigatório.
- O gerente poderá pesquisar clientes por nome ou telefone.
- Um cliente poderá possuir várias ordens de serviço.
- O histórico de atendimentos deverá permanecer associado ao cliente.
- O sistema deverá facilitar a identificação de cadastros existentes para evitar duplicidades.

**Necessidade de negócio:** reduzir o retrabalho e facilitar a comunicação com o cliente.

### 4.2 Cadastro de equipamentos

Cada computador ou notebook deverá possuir um cadastro individual.

**Decisões confirmadas:**

- Um cliente poderá possuir vários equipamentos.
- Equipamentos iguais deverão ser identificados separadamente.
- Cada equipamento terá um código interno único.
- O código interno será gerado automaticamente.
- Quando houver número de série de fábrica, ele deverá ser registrado.
- Equipamentos sem número de série geral de fábrica poderão receber uma identificação própria da assistência.
- O código interno poderá ser utilizado em uma etiqueta adesiva fixada no equipamento.
- O gerente poderá localizar equipamentos por sua identificação.

**Necessidade de negócio:** impedir confusões entre equipamentos e permitir o acompanhamento individual de cada um.

### 4.3 Abertura de ordens de serviço

O gerente deverá conseguir abrir uma OS para registrar o recebimento de um equipamento.

**Informações identificadas:**

- Número da OS.
- Cliente responsável.
- Telefone de contato.
- Equipamento.
- Modelo do equipamento.
- Defeito relatado.
- Data de entrada.
- Data de saída, quando aplicável.
- Estado atual do atendimento.

**Decisões confirmadas:**

- A numeração da OS será automática e única.
- A OS estará associada ao cliente e ao equipamento.
- O sistema deverá permitir acompanhar o andamento do atendimento.

### 4.4 Estados das ordens de serviço

Foi definido o seguinte fluxo principal:

1. **Aberto:** equipamento recebido e OS registrada.
2. **Em diagnóstico:** equipamento em análise técnica.
3. **Aguardando aprovação:** orçamento apresentado e aguardando resposta.
4. **Em manutenção:** reparo autorizado e em execução.
5. **Concluído:** serviço técnico finalizado, equipamento aguardando retirada.
6. **Encerrado:** equipamento retirado e atendimento finalizado.

Também foram identificados estados alternativos:

- **Orçamento recusado:** cliente não autorizou o reparo.
- **Cancelado:** atendimento cancelado, com histórico preservado.

O sistema deverá permitir visualizar separadamente ordens concluídas, encerradas e canceladas.

**Distinção importante:**

Uma OS concluída ainda não está necessariamente encerrada. O encerramento depende da retirada do equipamento e das condições financeiras definidas.

### 4.5 Diagnóstico técnico

A assistência cobrará pelo diagnóstico dos equipamentos.

**Decisões confirmadas:**

- O valor padrão do diagnóstico será de **R$ 50,00**.
- O diagnóstico será cobrado mesmo quando o orçamento de reparo for recusado.
- Quando o reparo for aprovado, o diagnóstico estará incluído no valor da mão de obra.
- O sistema não deverá cobrar o diagnóstico duas vezes.

**Exemplo:**

Se o cliente recusar o reparo e nenhum outro serviço tiver sido autorizado, deverá pagar R$ 50,00 pelo diagnóstico.

Se o cliente aprovar um reparo cuja mão de obra já inclui o diagnóstico, o valor de R$ 50,00 não será somado novamente.

### 4.6 Orçamentos

O sistema deverá permitir registrar orçamentos detalhados.

**Necessidades identificadas:**

- Informar os serviços propostos.
- Registrar o valor de cada serviço.
- Registrar peças e seus respectivos valores, quando aplicável.
- Calcular automaticamente o total.
- Registrar aprovação ou recusa do orçamento.
- Preservar o histórico dos orçamentos.

**Decisão confirmada:**

Peças fornecidas pelo próprio cliente poderão ser registradas na OS, mas não serão cobradas como peças da assistência nem movimentarão o estoque da empresa.

### 4.7 Recusa de orçamento

Quando o cliente não autorizar o reparo:

- A OS deverá registrar o estado **Orçamento recusado**.
- O orçamento permanecerá no histórico.
- O reparo recusado não deverá ser registrado como executado.
- O diagnóstico continuará sendo devido.
- A OS poderá ser encerrada após a retirada do equipamento e o pagamento integral devido.

### 4.8 Pagamentos

O sistema deverá registrar os pagamentos dos atendimentos.

**Decisões confirmadas:**

- O pagamento ocorrerá no momento da retirada do equipamento.
- Não haverá pagamento antecipado.
- Não serão permitidos pagamentos parciais.
- O pagamento deverá corresponder ao valor integral devido.
- O registro será realizado manualmente pelo gerente ou RH.
- O sistema não processará transferências financeiras nem verificará automaticamente o recebimento junto a bancos na primeira versão.

**Formas de pagamento aceitas:**

- Pix.
- Dinheiro.
- Cartão de débito.
- Cartão de crédito.
- Criptomoedas.

O sistema deverá registrar o valor recebido, o meio de pagamento e a OS correspondente.

**Condição de encerramento:**

Uma OS não poderá ser encerrada enquanto existir valor financeiro pendente.

### 4.9 Cancelamento de ordens de serviço

O sistema deverá permitir cancelar atendimentos sem excluir seus registros.

**Decisões confirmadas:**

- A OS cancelada receberá o estado **Cancelado**.
- O número original da OS será preservado.
- O número não poderá ser reutilizado.
- A OS permanecerá disponível no histórico.
- A OS cancelada deixará de ser contabilizada entre as ordens ativas.
- Os indicadores do painel deverão ser atualizados automaticamente.

**Exemplo:**

Se existirem 50 ordens ativas e uma delas for cancelada, o painel deverá apresentar 49 ordens ativas.

A OS cancelada continuará disponível para consulta.

### 4.10 Controle de estoque

O sistema deverá controlar peças utilizadas nos atendimentos.

**Necessidades identificadas:**

- Cadastrar peças.
- Consultar quantidades disponíveis.
- Associar peças às ordens de serviço.
- Atualizar automaticamente o estoque quando houver retirada de peças da empresa para uma OS.
- Registrar movimentações de estoque.

**Cancelamento:**

Quando uma OS for cancelada, peças não utilizadas poderão retornar ao estoque, com atualização automática da quantidade.

Peças já instaladas, danificadas ou consumidas não deverão retornar automaticamente ao estoque disponível.

Peças fornecidas pelo cliente não deverão movimentar o estoque da empresa.

### 4.11 Histórico de manutenção

O sistema deverá manter o histórico completo dos atendimentos realizados em cada equipamento.

O gerente poderá consultar:

- Número das ordens de serviço anteriores.
- Datas dos atendimentos.
- Defeitos relatados.
- Diagnósticos.
- Serviços executados.
- Peças utilizadas.
- Valores cobrados.
- Estados dos atendimentos.

O histórico deverá continuar disponível após a conclusão, encerramento ou cancelamento das ordens de serviço.

### 4.12 Registro fotográfico

O sistema deverá permitir anexar fotografias às ordens de serviço.

**Decisões confirmadas:**

- Registrar fotografias das condições do equipamento no recebimento.
- Permitir fotografias após a manutenção.
- Permitir múltiplas imagens por OS.
- Manter as imagens vinculadas ao atendimento.
- Preservar as fotografias no histórico.

**Necessidade de negócio:** documentar as condições físicas dos equipamentos e facilitar consultas futuras.

### 4.13 Comprovante de recebimento

O sistema deverá gerar comprovantes de recebimento em PDF.

**Informações previstas:**

- Identificação da assistência técnica.
- Número da OS.
- Nome e telefone do cliente.
- Identificação do equipamento.
- Marca e modelo.
- Número de série, quando disponível.
- Código interno do equipamento.
- Defeito relatado.
- Data de entrada.

O gerente poderá imprimir o comprovante ou compartilhar o PDF com o cliente pelo WhatsApp.

O documento deverá permanecer disponível para emissão posterior.

### 4.14 Funcionários e permissões

O sistema deverá permitir o cadastro de funcionários e controlar o acesso às funcionalidades conforme o perfil autorizado.

Foram identificados dois perfis iniciais:

- Gerente.
- RH.

O acesso deverá exigir autenticação.

As permissões específicas de cada operação ainda precisarão ser detalhadas.

### 4.15 Painel de acompanhamento

O sistema deverá apresentar informações operacionais que facilitem a gestão da assistência.

**Necessidades identificadas:**

- Consultar ordens de serviço por estado.
- Visualizar ordens concluídas que aguardam retirada.
- Consultar ordens encerradas.
- Consultar ordens canceladas.
- Acompanhar quantidades de ordens ativas.
- Atualizar automaticamente indicadores quando os dados forem alterados.

Os indicadores financeiros e demais métricas deverão ser detalhados na especificação de requisitos.

---

## 5. Necessidades de acesso e utilização

Foram identificadas as seguintes expectativas:

- Utilização por uma única empresa na primeira versão.
- Disponibilização de uma interface web.
- Interesse em uma aplicação para Windows.
- Acesso mediante autenticação.
- Restrição de acesso conforme o perfil do usuário.
- Utilização em computadores autorizados.

A forma técnica de implementar essas restrições ainda será avaliada na etapa de arquitetura.

---

## 6. Limites de escopo identificados

Não fazem parte do escopo inicialmente confirmado:

- Gestão de múltiplas empresas.
- Portal de acesso para clientes.
- Portal próprio para técnicos.
- Processamento automático de pagamentos.
- Integração bancária para confirmação de pagamentos.

Essas funcionalidades poderão ser reavaliadas em versões futuras.

---

## 7. Questões pendentes

O levantamento identificou algumas decisões que ainda precisam ser refinadas.

### 7.1 Operação

- Em quais estados será permitido cancelar uma OS?
- O motivo do cancelamento será obrigatório?
- Como tratar a cobrança de diagnóstico em cancelamentos?
- Como confirmar se uma peça foi efetivamente utilizada?
- Será possível reabrir uma OS encerrada?
- Como tratar equipamentos que mudam de proprietário?

### 7.2 Financeiro

- Como registrar pagamentos em criptomoedas e seu valor equivalente em reais?
- Será permitido utilizar mais de um meio de pagamento em uma única quitação integral?
- Como corrigir registros de pagamento realizados incorretamente?
- Quem poderá alterar o valor padrão do diagnóstico?

### 7.3 Documentos e arquivos

- O comprovante terá campo para assinatura?
- Quais termos de recebimento serão utilizados?
- O envio por WhatsApp será manual ou automatizado?
- Quais serão os formatos e limites de tamanho das fotografias?
- Como serão controladas a exclusão e a retenção de imagens?

### 7.4 Acesso e segurança

- Quais permissões específicas cada perfil terá?
- Como serão autorizados os computadores utilizados?
- Quais políticas de autenticação e recuperação de acesso serão adotadas?

Essas pendências deverão ser registradas e priorizadas durante o refinamento do backlog. Nem todas precisam ser resolvidas antes do início do desenvolvimento.

---

## 8. Síntese do levantamento

O levantamento permitiu identificar os principais processos da assistência técnica e estabelecer uma base para o desenvolvimento do sistema.

As áreas funcionais identificadas foram:

1. Gestão de clientes.
2. Gestão de equipamentos.
3. Gestão de ordens de serviço.
4. Diagnósticos e orçamentos.
5. Gestão de pagamentos.
6. Controle de estoque.
7. Histórico de manutenções.
8. Registro fotográfico.
9. Emissão de documentos.
10. Gestão de funcionários e permissões.
11. Painel de acompanhamento.

As decisões registradas representam as necessidades levantadas, não uma obrigação de implementar todas as funcionalidades simultaneamente.

A definição do **Produto Mínimo Viável (MVP)** determinará quais funcionalidades serão priorizadas para a primeira entrega.

---

## 9. Encerramento da etapa

**Status do levantamento:** concluído para fins de especificação inicial.

**Próxima etapa:** `03-requisitos.md` — Especificação de Requisitos Funcionais e Não Funcionais.

A partir deste levantamento, as necessidades identificadas serão convertidas em requisitos verificáveis, organizados e rastreáveis.

Novas necessidades poderão surgir durante o desenvolvimento e deverão passar por análise, priorização e controle de mudanças.