# SPEC-1-002 — Encaminhamento humano com contexto preservado

**Fase:** 1  
**Status:** bloqueada — configuração operacional pendente  
**Dono:** liderança Comercial e Consultor Comercial  
**Origem no escopo:** D-001, RQ-002 e Fase 1 de `03-Projeto/02-Escopo-Definitivo.md`  
**Degrau da solução:** recurso nativo da plataforma de pré-agendamento — registra uma fila/visão operacional e contexto de encaminhamento sem escrever em CRM, agenda ou mensageria externa.

## Contexto e decisões fechadas

- **Estado atual:** o consultor assume manualmente leads em `AGUARDANDO ATENDIMENTO` e o contexto pode ficar distribuído entre canais. A operação atual utiliza Kommo/WhatsApp, mas integração direta foi deliberadamente adiada. Fontes: `03-Projeto/requisitos.md` §RQ-002; `04-Mapeamento-Processos/01-Videos/Analise - Teste 2.md` §3.
- **Estado desejado:** uma submissão que pede ajuda humana, apresenta dúvida ou não pode continuar na jornada produz um registro operacional visível ao Consultor Comercial, com respostas, atribuição e dono/status de encaminhamento.
- **Decisões já fechadas:** atendimento e negociação seguem humanos; a Fase 1 não envia mensagem, não muda etapa no Kommo, não cria oportunidade e não confirma agendamento. A primeira interação humana é registrada na plataforma de pré-agendamento, não por automação externa.
- **Bloqueios:** o canal operacional aprovado, a regra de distribuição, os responsáveis por turno e as permissões mínimas não estão documentados. O Ethos deve preparar o roteiro de teste, mas parar antes de criar fila, apontar usuário real, webhook, link de WhatsApp ou notificação externa até o Champion e a liderança Comercial registrarem esses itens.

## BLOQUEIOS executáveis

| Informação necessária | Dono da decisão | Por que bloqueia | Evidência para liberar |
|---|---|---|---|
| Canal operacional e responsável por cada turno | Champion e liderança Comercial | Sem destino e dono, o sistema não pode criar/atribuir pedido humano com segurança. | Canal nomeado, horários/regra de cobertura e donos registrados. |
| Regra de distribuição e encerramento | Liderança Comercial | Sem regra, o executor inventaria quem recebe, reassume ou encerra um caso. | Estados permitidos, responsável por transição e regra de reatribuição aprovados. |
| Papéis mínimos para Champion e Consultor Comercial | Champion | Sem permissão explícita, há risco de expor dados de contato ou de mudança indevida de estado. | Matriz curta de leitura, assunção, reatribuição e publicação aprovada. |

## Resultado observável

Um consultor autorizado abre uma fila de encaminhamentos e identifica, sem pedir novamente as mesmas informações, quem pediu ajuda, quando enviou, qual versão do formulário respondeu, qual origem/campanha veio (ou se faltou), quais respostas forneceu e se o caso está `PENDENTE`, `ASSUMIDO` ou `ENCERRADO_SEM_AGENDAMENTO`. O sistema não declara agendamento nem atendimento concluído apenas porque a fila foi criada.

## Limites e dependências

- **Inclui:** criação de registro de encaminhamento interno, contexto mínimo, atribuição de dono dentro da plataforma, transições de estado, visibilidade de pendências e trilha de eventos.
- **Fora de escopo:** distribuição automática, SLA de primeira resposta, mensagens, ligação, WhatsApp, Kommo, Lóvavel, agendamento, alteração de campanha, negociação, descarte ou classificação comercial automática.
- **Entradas e pré-condições:** SPEC-1-001 testada; Champion definiu canal operacional, responsáveis por turno e quem pode ler a fila; Consultor Comercial recebeu permissão mínima no ambiente de teste.
- **Saídas/artefatos:** fila/visão de encaminhamentos, registro de eventos de estado e roteiro de operação manual.
- **Dependências e responsáveis:** Champion aprova canal, papéis e publicação; liderança Comercial define responsáveis; Consultor Comercial assume/encerra somente registros atribuídos; executor não integra contas externas.
- **Atores e permissões mínimas:** Lead cria o pedido; Consultor Comercial lê/assume registros atribuídos; Champion consulta e configura; Marketing não acessa telefone, respostas individuais ou fila.
- **Superfícies/arquivos/configurações afetadas:** visão/fila interna da plataforma de pré-agendamento; este arquivo; `01-SPECs/00-INDICE.md`; `matriz-de-rastreabilidade.md`.
- **Risco e plano B:** se não houver canal ou responsável aprovado, exibir o pedido apenas na fila de teste e manter o fluxo humano atual sem publicar. Em indisponibilidade da fila, preservar a submissão e registrar o incidente; não enviar dados por canal alternativo sem aprovação.
- **Rollback ou reversão:** desativar a regra de criação de novos encaminhamentos, manter os registros já existentes como somente leitura e retornar o atendimento ao canal humano atual.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| SPEC-1-001 → fila interna | Plataforma de pré-agendamento | `handoff_id`, `lead_submission_id`, `form_id`, `form_version`, `created_at`, `motivo`, `nome`, `canal_de_retorno`, `objetivo`, `proximidade`, `ocupacao`, `interesse_em_visita`, UTMs, `attribution_status`, `status`, `dono`, `assumed_at`, `closed_at` | Consultor vê somente registros atribuídos; Champion configura; sem token/API externa | Reprocessar o mesmo `lead_submission_id` atualiza o mesmo `handoff_id`; não cria um segundo encaminhamento. | Falha ao criar fila deixa submissão com `ENCAMINHAMENTO_FALHOU` e pendência visível; não marca como assumido. |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-1.06 | `precisa_de_ajuda_humana=true` | Criar/atualizar um encaminhamento interno `PENDENTE` com contexto da submissão | Sem dono/canal aprovado, manter em teste e bloquear publicação | Escopo definitivo §4; SPEC-1-001 |
| RN-1.07 | Consultor autorizado assume o caso | Registrar dono e `assumed_at`; estado vira `ASSUMIDO` | Permissão ausente não altera estado e mostra pendência | RQ-002 |
| RN-1.08 | Mesmo envio é reprocessado | Reutilizar o `handoff_id` do mesmo `lead_submission_id` | Submissão nova cria novo encaminhamento próprio | RQ-001 e RQ-002 |
| RN-1.09 | Consultor encerra sem agendamento | Registrar `ENCERRADO_SEM_AGENDAMENTO`, motivo livre e horário; não apagar contexto | Não usar esse estado como perda comercial ou métrica de conversão nesta fase | Limites da Fase 1 |

## Fluxo e regras

1. A SPEC-1-001 grava submissão concluída com pedido explícito de ajuda ou com próximo passo que exige humano.
2. A plataforma procura `lead_submission_id`; se ainda não há fila, cria `handoff_id` e estado `PENDENTE`; se já existe, atualiza o registro sem duplicá-lo.
3. O Consultor Comercial autorizado vê a fila, abre o contexto e assume o caso. A ação registra dono e horário, mas não envia mensagem nem altera CRM.
4. Depois do contato pelos meios aprovados fora desta SPEC, o consultor registra somente o estado de encaminhamento. O agendamento, se houver, será tratado na Fase 2.
5. Falha de criação, permissão insuficiente ou ausência de canal/responsável não simula sucesso; mantém pendência rastreável para o Champion.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Submissão válida pede ajuda humana | Uma fila `PENDENTE` com contexto completo e identificador único | Consultor assume e o sistema registra responsável/horário |
| Limite | Reprocessamento do mesmo `lead_submission_id` | O mesmo `handoff_id` é mantido; não há duplicata | Revisar o evento duplicado e conservar trilha |
| Falha | Usuário sem permissão tenta assumir; ou criação falha | Estado não muda para `ASSUMIDO`; pendência é visível | Champion corrige permissão/indisponibilidade e reprocessa com a mesma chave |
| Recuperação | Canal humano fica indisponível | Novos pedidos não são marcados como atendidos; fila registra incidente | Suspender regra de publicação e usar o fluxo humano atual após autorização |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** esta SPEC, SPEC-1-001, `02-Escopo-Definitivo.md` §§3–6 e `requisitos.md` §RQ-002.
2. **Alterar somente:** fila/visão interna, estados e permissões mínimas em ambiente autorizado; índice e matriz do plano.
3. **Não alterar:** Kommo, WhatsApp, Lóvavel, agenda, mensagens, regras de campanha, credenciais, dados históricos ou permissões globais.
4. **Executar nesta ordem:** validar SPEC-1-001 → configurar estados e chave idempotente em teste → testar criação, reprocessamento, permissão e falha → registrar canal/dono aprovados → obter aceite humano → publicar.
5. **Parar e pedir validação quando:** canal operacional, dono de turno ou permissão não estiverem registrados; qualquer ação exigir mensagem, webhook, login externo ou mudança em CRM; o comportamento de reprocessamento não for idempotente.
6. **Estado válido ao parar:** registros de teste permanecem isolados; fila não é publicada; nenhum lead real ou sistema externo foi alterado.

## Checklist de execução

- [ ] SPEC-1-001 passou em ambiente de teste.
- [ ] Champion e liderança Comercial definiram canal operacional, responsáveis por turno, regra de distribuição/encerramento e quem pode ler/assumir a fila.
- [ ] Fila usa `lead_submission_id` como chave de idempotência e não cria duplicata em reprocessamento.
- [ ] Cenários de permissão negada, falha de criação e recuperação foram exercitados.
- [ ] A fila não envia mensagem nem escreve em sistema externo.
- [ ] Evidência e aceite humano de publicação foram registrados.

## Critérios de aceite

- [ ] **CA-1.06:** Pedido de ajuda humana cria um único `handoff_id` com contexto, versão, atribuição e estado `PENDENTE`.
- [ ] **CA-1.07:** Consultor autorizado pode assumir o encaminhamento, e o sistema registra dono e `assumed_at` sem apagar as respostas.
- [ ] **CA-1.08:** Reprocessar a mesma submissão não cria segundo encaminhamento.
- [ ] **CA-1.09:** Usuário sem permissão e falha de criação não geram `ASSUMIDO` ou sucesso aparente; a pendência fica visível.
- [ ] **CA-1.10:** A fila pode ser desativada/revertida sem excluir submissões ou encaminhamentos já registrados.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Abrir pedido humano com usuário sem permissão e simular falha de criação | No ambiente de teste, tentar assumir sem papel e interromper a criação da fila | Não há estado `ASSUMIDO` nem confirmação falsa; pendência fica registrada | Capturas de permissão/erro e registro de evento |
| GREEN | Processar fixture `pedido_humano_valido` | Enviar submissão com pedido humano e assumir com consultor de teste autorizado | Um `handoff_id` `PENDENTE` é criado; ao assumir, grava dono e horário | Capturas da fila e detalhe do encaminhamento |
| REFACTOR/REGRESSÃO | Reprocessar a mesma submissão, encerrar sem agendamento e executar rollback | Reexecutar o fixture, mudar o estado e desativar a regra em teste | Sem duplicata; histórico íntegro; nenhuma escrita/mensagem externa; registros preservados após reversão | Roteiro de teste assinado e export/visualização de eventos |

**Dados/fixtures:** submissões sintéticas da SPEC-1-001 com e sem atribuição, uma com `precisa_de_ajuda_humana=true`; dois usuários de teste, um autorizado e outro sem permissão.  
**Caminhos de erro obrigatórios:** permissão insuficiente, criação interrompida, reprocessamento, dono ausente, canal indisponível e rollback.  
**Evidência exigida:** capturas/registro do ambiente de teste, trilha de estado e aceite humano; não anexar dados de leads reais.

## Handoff e operação

- **Como demonstrar:** enviar um pedido humano sintético, mostrar contexto e estado `PENDENTE`, assumir com usuário autorizado, repetir o envio e comprovar que não há duplicata; em seguida testar reversão.
- **Como operar depois:** liderança Comercial mantém responsáveis por turno; Champion aprova qualquer publicação ou mudança de canal; Consultor Comercial atualiza apenas o estado de encaminhamento.
- **Como monitorar:** quantidade de pendentes, assumidos, falhas de criação, reprocessamentos e encaminhamentos sem dono; SLA e conversão ficam fora desta fase até decisão específica.
- **Pendência conhecida:** canal, dono de turno e permissões reais precisam ser declarados pelo Champion antes da publicação; essa SPEC não concede acesso a contas externas.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T002 | Registrar canal humano e cobertura por turno | Champion do cliente | SPEC-1-002 | Canal e responsáveis por turno estão registrados. | Primeiro bloqueio executável. | Canal nomeado e cobertura. | Decisão do Champion. | bloqueada |
| F1-T005 | Registrar regras de distribuição e encerramento humano | Liderança Comercial | SPEC-1-002 | Estados, transições, reatribuição e encerramento estão aprovados. | Segundo bloqueio executável. | Regras documentadas. | Decisão da liderança Comercial. | bloqueada |
| F1-T006 | Registrar permissões mínimas do encaminhamento humano | Champion do cliente | SPEC-1-002 | Matriz curta de permissões está aprovada. | Terceiro bloqueio executável. | Matriz de leitura, assunção, reatribuição e publicação. | Decisão do Champion. | bloqueada |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
