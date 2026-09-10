# SPEC-2-002 — Visão operacional de tentativas e agendamentos

**Fase:** 2  
**Status:** bloqueada — configuração operacional pendente  
**Dono:** Champion do cliente e liderança Comercial  
**Origem no escopo:** D-001, D-003, RQ-002, RQ-005 e Fase 2 de `03-Projeto/02-Escopo-Definitivo.md`  
**Degrau da solução:** recurso nativo da plataforma de pré-agendamento — registra uma visão/fila operacional de tentativas de agendamento com contexto do lead; não integra Kommo, Lóvavel ou agenda externa nesta fase.

## Contexto e decisões fechadas

- **Estado atual:** o consultor não tem visibilidade consolidada do estado de cada tentativa de agendamento; leads encaminhados por dúvida ou por falha de agenda chegam sem contexto estruturado. Fontes: `03-Projeto/requisitos.md` §RQ-002 e §RQ-005; `03-Projeto/02-Escopo-Definitivo.md` §§Fase 1 e Fase 2; `spec-1-002-encaminhamento-humano-com-contexto.md`.
- **Estado desejado:** o Consultor Comercial, o Subgerente e a Gestão têm uma visão operacional que mostra cada tentativa de agendamento com seu estado atual (`TENTATIVA`, `CONCLUIDO`, `DESISTENCIA`, `ENCAMINHAMENTO_HUMANO`), o contexto da triagem da Fase 1 e os dados do horário escolhido quando houver.
- **Decisões já fechadas:** a visão não envia mensagem, não cria oportunidade no Kommo, não altera o CRM e não confirma presença; o agendamento só é `CONCLUIDO` quando a SPEC-2-001 assim registrar. O consultor vê somente tentativas atribuídas a ele ou em `ENCAMINHAMENTO_HUMANO`. A Gestão/Subgerente vê todos os estados.
- **Bloqueios:** os papéis com permissão de leitura e escrita nessa visão, a regra de encaminhamento para humano quando o lead não consegue agendar e o responsável por encerrar ou reatribuir tentativas paradas não estão documentados nas fontes.

## BLOQUEIOS executáveis

| Informação necessária | Dono da decisão | Por que bloqueia | Evidência para liberar |
|---|---|---|---|
| Papéis com permissão de leitura e de escrita na visão operacional (quem vê o quê, quem pode atualizar estado) | Champion do cliente | Sem matriz de permissões, dados de contato e estado de agendamento poderiam ser expostos a papéis não autorizados. | Matriz curta de leitura e escrita por papel (Consultor, Subgerente, Gestão, Champion) registrada e aprovada pelo Champion. |
| Regra de encaminhamento para humano quando o lead não consegue agendar (motivo obrigatório, estado de destino, dono inicial) | Liderança Comercial | Sem a regra, tentativas em `ENCAMINHAMENTO_HUMANO` chegam sem dono e sem próximo passo claro. | Regra de atribuição inicial, campo de motivo e estado de destino aprovados pela liderança Comercial. |
| Responsável por encerrar ou reatribuir tentativas paradas (sem ação do consultor por período a definir) | Liderança Comercial | Sem dono de escalada, tentativas paradas acumulam sem responsável visível. | Papel responsável pela escalada e critério de parada registrados e aprovados pela liderança Comercial. |

## Resultado observável

Um consultor autorizado abre a visão operacional e identifica, sem pedir novamente as mesmas informações: quem tentou agendar, quando iniciou, qual versão do formulário respondeu, qual origem/campanha veio (ou se faltou), quais respostas forneceu na triagem, qual horário escolheu (se houver) e qual é o estado atual da tentativa. O sistema mostra as tentativas em `ENCAMINHAMENTO_HUMANO` com motivo e dono inicial; o Subgerente e a Gestão veem todos os estados. Nenhuma tentativa é declarada `CONCLUIDA` por esta visão; a transição de estado vem exclusivamente da SPEC-2-001.

## Limites e dependências

- **Inclui:** visão/fila de tentativas com estado, contexto da triagem (da Fase 1) e dados de agendamento (da SPEC-2-001), atribuição de dono em `ENCAMINHAMENTO_HUMANO`, escalada de tentativas paradas e trilha de eventos de estado.
- **Fora de escopo:** envio de mensagem, ligação, WhatsApp, Kommo, Lóvavel, confirmação D-1/D-0, cálculo de conversão, SLA de resposta, classificação comercial automática, descarte de lead e decisão sobre Free Pass.
- **Entradas e pré-condições:** SPEC-2-001 testada; Champion definiu papéis e permissões; liderança Comercial definiu regra de encaminhamento e responsável de escalada; Consultor Comercial recebeu permissão mínima no ambiente de teste.
- **Saídas/artefatos:** visão/fila operacional de tentativas, trilha de estado e roteiro de operação manual para Consultor, Subgerente e Gestão.
- **Dependências e responsáveis:** Champion aprova papéis, permissões e publicação; liderança Comercial define regra de encaminhamento e escalada; Consultor Comercial assume e atualiza somente registros atribuídos; executor não integra contas externas.
- **Atores e permissões mínimas:** Lead cria a tentativa (via SPEC-2-001); Consultor Comercial lê e atualiza estado de tentativas atribuídas ou em `ENCAMINHAMENTO_HUMANO`; Subgerente e Gestão leem todos os estados sem poder concluir tentativas; Champion configura e consulta; Marketing não acessa dados de contato individuais nem tentativas individuais.
- **Superfícies/arquivos/configurações afetadas:** visão/fila interna da plataforma de pré-agendamento; este arquivo; `01-SPECs/00-INDICE.md`; `02-Plano_de_acao/02.Fase_2/00-Tasks_Gerais.md`; `matriz-de-rastreabilidade.md`.
- **Risco e plano B:** se não houver papéis ou regra de encaminhamento aprovados, exibir a visão somente no ambiente de teste e manter o fluxo humano atual da SPEC-1-002 sem publicar. Em indisponibilidade da visão, preservar tentativas na SPEC-2-001 e registrar o incidente; não enviar dados de contato por canal alternativo sem aprovação.
- **Rollback ou reversão:** desativar a regra de atribuição de novas tentativas em `ENCAMINHAMENTO_HUMANO`, manter registros existentes como somente leitura e retornar o atendimento ao canal humano aprovado na SPEC-1-002.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| SPEC-2-001 → visão operacional | Plataforma de pré-agendamento | `appointment_id`, `lead_submission_id`, `form_id`, `form_version`, `slot_id`, `slot_datetime`, `nome`, `canal_de_retorno`, `objetivo`, `proximidade`, `ocupacao`, `interesse_em_visita`, UTMs, `attribution_status`, `status`, `handoff_reason`, `dono`, `assumed_at`, `escalated_at`, `closed_at` | Consultor vê somente tentativas atribuídas ou em `ENCAMINHAMENTO_HUMANO`; Subgerente/Gestão veem todos; Champion configura; sem token/API externa | Atualização do mesmo `appointment_id` modifica o registro existente; não cria segunda entrada. | Falha ao atualizar estado mantém o estado anterior visível e gera pendência com dono; não marca como assumido ou concluído em caso de erro. |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-2.07 | Tentativa entra em `ENCAMINHAMENTO_HUMANO` via SPEC-2-001 | Criar entrada na visão com motivo, dono inicial (conforme regra da liderança Comercial) e estado `ENCAMINHAMENTO_HUMANO` | Sem dono/regra aprovada, manter em teste e bloquear publicação | Escopo definitivo, Fase 2; SPEC-2-001 |
| RN-2.08 | Consultor autorizado assume uma tentativa em `ENCAMINHAMENTO_HUMANO` | Registrar dono e `assumed_at`; estado permanece `ENCAMINHAMENTO_HUMANO` com dono visível | Permissão ausente não altera estado e gera pendência visível | RQ-002; SPEC-1-002 |
| RN-2.09 | Consultor registra resolução da tentativa encaminhada | Atualizar estado para `CONCLUIDO` somente se SPEC-2-001 também registrar conclusão; ou encerrar com motivo livre | Não usar encerramento sem agendamento como métrica de conversão nesta fase | Limites da Fase 2 |
| RN-2.10 | Tentativa parada sem ação por critério a definir | Escalar visualmente para o responsável de escalada aprovado; não alterar estado automaticamente | Se o critério de parada não estiver definido, apresentar a tentativa como pendente sem prazo automático | Liderança Comercial; escopo definitivo §4 |
| RN-2.11 | Mesma tentativa reprocessada (mesmo `appointment_id`) | Reutilizar o registro existente; não criar duplicata | Tentativa nova vinda de nova ação do lead cria novo `appointment_id` | SPEC-2-001; RN-2.01 |

## Fluxo e regras

1. SPEC-2-001 registra uma tentativa; qualquer estado (`TENTATIVA`, `CONCLUIDO`, `DESISTENCIA`, `ENCAMINHAMENTO_HUMANO`) fica visível na visão operacional.
2. Para tentativas em `ENCAMINHAMENTO_HUMANO`, a plataforma aplica a regra de atribuição inicial aprovada pela liderança Comercial e define o dono.
3. O Consultor autorizado abre a visão, localiza tentativas atribuídas a ele, revê o contexto completo da triagem e do horário tentado (se houver) e registra sua ação.
4. O Subgerente e a Gestão veem todos os estados sem poder concluir tentativas de forma independente da SPEC-2-001.
5. Tentativas paradas são sinalizadas para o responsável de escalada sem mudança automática de estado.
6. Falha de permissão ou indisponibilidade não altera estado e preserva a tentativa com pendência rastreável.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Tentativa `ENCAMINHAMENTO_HUMANO` com motivo | Entrada na visão com dono inicial, contexto completo e estado correto | Consultor assume e o sistema registra responsável e horário |
| Reprocessamento | Mesmo `appointment_id` atualizado na SPEC-2-001 | O mesmo registro é atualizado; não há duplicata | Revisar o evento e conservar trilha de estados |
| Permissão negada | Usuário sem papel tenta assumir ou alterar | Estado não muda; pendência fica visível para Champion | Champion corrige permissão e reprocessa |
| Escalada | Tentativa parada sem ação | Sinalização visual para o responsável de escalada; sem mudança automática de estado | Responsável de escalada decide próximo passo |
| Rollback | Regra de encaminhamento apresenta defeito | Desativar atribuição automática; manter registros existentes como somente leitura; retornar ao canal humano da SPEC-1-002 | Registrar incidente e aguardar aprovação antes de nova publicação |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** esta SPEC, SPEC-2-001, SPEC-1-001, SPEC-1-002, `02-Escopo-Definitivo.md` §§3–6 (Fase 2) e `requisitos.md` §§RQ-002 e RQ-005.
2. **Alterar somente:** visão/fila de tentativas, estados e permissões mínimas em ambiente autorizado; índice e matriz do plano.
3. **Não alterar:** Kommo, WhatsApp, Lóvavel, agenda externa, mensagens, campanhas, credenciais, dados históricos ou permissões globais.
4. **Executar nesta ordem:** validar SPEC-2-001 → configurar papéis e regra de encaminhamento em teste → testar criação, reprocessamento, permissão negada e escalada → registrar regra de atribuição/escalada aprovadas → obter aceite humano → publicar.
5. **Parar e pedir validação quando:** papéis, regra de encaminhamento ou responsável de escalada não estiverem registrados; qualquer ação exigir mensagem, webhook, login externo ou mudança em CRM; reprocessamento criar duplicata.
6. **Estado válido ao parar:** registros de teste isolados; visão não publicada; nenhum lead real ou sistema externo foi alterado.

## Checklist de execução

- [ ] SPEC-2-001 passou em ambiente de teste.
- [ ] Champion aprovou a matriz de permissões por papel para a visão operacional.
- [ ] Liderança Comercial definiu regra de atribuição inicial, campo de motivo e critério de escalada para tentativas paradas.
- [ ] Visão usa `appointment_id` como chave e não cria duplicata em reprocessamento.
- [ ] Cenários de permissão negada, reprocessamento, escalada e rollback foram exercitados.
- [ ] A visão não envia mensagem nem escreve em sistema externo.
- [ ] Evidência e aceite humano de publicação foram registrados.

## Critérios de aceite

- [ ] **CA-2.06:** Toda tentativa registrada na SPEC-2-001 aparece na visão operacional com estado, contexto de triagem e dados de agendamento (quando disponíveis).
- [ ] **CA-2.07:** Tentativa em `ENCAMINHAMENTO_HUMANO` recebe dono inicial conforme regra aprovada; Consultor autorizado pode assumir e o sistema registra responsável e `assumed_at`.
- [ ] **CA-2.08:** Reprocessar o mesmo `appointment_id` não cria segundo registro na visão.
- [ ] **CA-2.09:** Usuário sem permissão e falha de atualização não geram mudança de estado; a pendência fica visível.
- [ ] **CA-2.10:** A visão pode ser desativada/revertida sem excluir tentativas ou seus eventos.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Tentar assumir tentativa com usuário sem permissão e simular falha de atualização | No ambiente de teste, usar papel não autorizado e interromper a atualização | Sem mudança de estado nem confirmação falsa; pendência fica registrada | Capturas de permissão/erro e trilha de eventos |
| GREEN | Processar fixture `tentativa_encaminhamento_humano_valida` | Tentativa em `ENCAMINHAMENTO_HUMANO` com motivo preenchido; Consultor de teste assume | Entrada na visão com dono, `assumed_at` e contexto completo | Capturas da visão e detalhe da tentativa |
| REFACTOR/REGRESSÃO | Reprocessar a mesma tentativa, escalar por parada e executar rollback | Reexecutar o fixture, simular parada e desativar a regra em teste | Sem duplicata; escalada sinalizada; rollback mantém registros sem alterar sistemas externos | Roteiro de teste assinado e export/visualização de eventos |

**Dados/fixtures:** tentativas sintéticas da SPEC-2-001 em todos os estados; dois usuários de teste, um autorizado e outro sem permissão; um com `ENCAMINHAMENTO_HUMANO` e motivo preenchido.  
**Caminhos de erro obrigatórios:** permissão insuficiente, atualização interrompida, reprocessamento, dono ausente, escalada por parada e rollback.  
**Evidência exigida:** capturas/registro do ambiente de teste, trilha de estado e aceite humano; não anexar dados de leads reais.

## Handoff e operação

- **Como demonstrar:** criar tentativa sintética em `ENCAMINHAMENTO_HUMANO`, mostrar atribuição e contexto na visão, assumir com Consultor autorizado, repetir o envio e comprovar ausência de duplicata; simular parada e verificar sinalização de escalada; em seguida testar rollback.
- **Como operar depois:** liderança Comercial mantém responsável de escalada atualizado; Champion aprova qualquer publicação ou mudança de papéis; Consultor atualiza somente o estado das tentativas atribuídas a ele.
- **Como monitorar:** quantidade de tentativas por estado, encaminhamentos sem dono, tempo médio até assunção (sem SLA automático nesta fase), escaladas e rollbacks; conversão até agendamento fica fora desta fase até a Fase 3.
- **Pendência conhecida:** papéis, regra de encaminhamento e critério de escalada precisam ser declarados pelo Champion e pela liderança Comercial antes da publicação; esta SPEC não concede acesso a contas externas.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F2-T004 | Registrar papéis, permissões e regra de encaminhamento para humano | Champion + Liderança Comercial | SPEC-2-002 | Matriz de leitura/escrita por papel e regra de atribuição inicial estão registradas e aprovadas. | Primeiro e segundo bloqueios executáveis. | Matriz de permissões e regra de encaminhamento documentadas e aprovadas. | Decisões do Champion e da liderança Comercial. | bloqueada — aguarda decisão humana |
| F2-T005 | Registrar responsável por encerrar ou reatribuir tentativas paradas | Liderança Comercial | SPEC-2-002 | Papel responsável pela escalada e critério de parada estão registrados e aprovados. | Terceiro bloqueio executável. | Papel de escalada e critério documentados e aprovados pela liderança Comercial. | Decisão da liderança Comercial. | bloqueada — aguarda decisão humana |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
