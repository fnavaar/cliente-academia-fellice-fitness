# Status operacional

- **Fase atual:** Fase 2 — autoagendamento assistido e continuidade da jornada.
- **Caminho canônico:** `04_fase-atual/` — underscore depois de `04`; `04-fase-atual/` não existe.
- **Fase 1:** encerrada; F1-T001 a F1-T008 concluídas, com teste humano registrado para F1-T007 e F1-T008.
- **Fase 2:** desbloqueios documentais concluídos em 2026-09-16; implementação em curso desde 2026-09-17.
- **Progresso documental:** 5/5 tasks de decisão concluídas.
- **Progresso de implementação:** 3/9 tasks concluídas (33%); F2-IMP-004 é a próxima elegível.
- **Produto no preview:** triagem F1 disponível; grade de disponibilidade de teste (248 slots); **página /agendar funcional** — lead escolhe horário, preenche campos mínimos e confirma, com fallback para atendimento humano; rota do atendente `/fila` (a auditoria de 16/09 registrou `/queue` por engano).
- **Bloqueios documentais:** resolvidos para SPEC-2-001 e SPEC-2-002.
- **Implementação:** F2-IMP-001, F2-IMP-002 e F2-IMP-003 concluídas com aceite humano em 2026-09-17; nenhuma publicação em produção.

## Tasks documentais concluídas

- F2-T001 — duração, capacidade e grade inicial. ✅ concluída — 2026-09-16
- F2-T002 — responsável por manter e fechar a agenda. ✅ concluída — 2026-09-16
- F2-T003 — campos mínimos para conclusão do agendamento. ✅ concluída — 2026-09-16
- F2-T004 — papéis, permissões e encaminhamento humano. ✅ concluída — 2026-09-16
- F2-T005 — escalada, encerramento e reatribuição de tentativas paradas. ✅ concluída — 2026-09-16

## Tasks de implementação

- F2-IMP-001 — contrato técnico e fixtures sintéticas de agenda/tentativa. ✅ concluída — 2026-09-17 (migrações 0007/0008 no Skip 51806 v0.0.20; pipeline QA ok; provas ao vivo: duplicata recusada, criação pública aceita, leitura anônima sem vazamento, leitura autenticada ok; teste humano aprovado; usuário sintético removido — 0010)
- F2-IMP-002 — grade de disponibilidade de teste. ✅ concluída — 2026-09-17 (migração 0011, v0.0.23: 248 slots, 14 dias, seg–sex 08:00–19:00 e sáb 09:00–13:00, blocos de 30 min, capacidade 2 nos blocos iniciando 11:30–16:30 exatos; ciclo de vida provado via API; teste humano aprovado; usuário sintético removido — 0013)
- F2-IMP-003 — seleção, validação e conclusão do agendamento. ✅ concluída — 2026-09-17 (página /agendar no Skip 51806 v0.0.26: grade agrupada por dia → campos mínimos → confirmação com código de reserva; link na triagem; provas ao vivo: CONCLUIDO com concluded_at e evento, fallback ENCAMINHAMENTO_HUMANO com motivo, reescolha de slot atualiza sem duplicar, página HTTP 200; teste humano aprovado — fluxo completo percorrido no preview; usuário de verificação removido — 0015)
- F2-IMP-004 — conflito, idempotência, desistência, fallback e rollback. **Elegível.**
- F2-IMP-005 — TDD integrado e aceite da agenda. Bloqueada por F2-IMP-004 e evidências.
- F2-IMP-006 — visão operacional de tentativas. Bloqueada por F2-IMP-005 e aceite humano.
- F2-IMP-007 — permissões, fila, assunção e atualização segura. Bloqueada por F2-IMP-006 e aceite humano.
- F2-IMP-008 — escalada visual, reatribuição, encerramento e rollback. Bloqueada por F2-IMP-007 e aceite humano.
- F2-IMP-009 — TDD integrado e aceite da visão operacional. Bloqueada por F2-IMP-008 e evidências.

## Pendências registradas

- **LGPD (validar com compliance):** base legal da finalidade de agendamento — o consentimento F1-T004 cobre comunicações; o agendamento se apoia em execução de serviço solicitado. Registrado no contrato da F2-IMP-001, seção 7. A página /agendar já coleta os campos sob essa base provisória documentada.
- **Semântica de reagendamento (RN-2.06):** implementada e provada na F2-IMP-003 (tentativa não confirmada é atualizada com o novo slot, sem duplicar); validar com o Champion na próxima oportunidade.
- **Capacidade 2 no sábado [VALIDAR NA CALL DE SETUP]:** a regra da F2-T001 não distingue dia da semana; a grade gerada aplica capacidade 2 também aos blocos de sábado dentro da janela 11:30–13:00. Se o sábado deve ficar todo com capacidade 1, ajustar em emenda da SPEC.

## Próxima ação segura

Executar somente F2-IMP-004 no ambiente de teste, com fixtures sintéticas — provar conflito de concorrência (duas reservas no mesmo slot), idempotência de reprocessamento, desistência com liberação de capacidade e rollback da grade preservando histórico. Depois da prova e do teste humano, liberar F2-IMP-005. Nenhuma task seguinte, publicação ou Fase 3 é autorizada por este status.

## Limite operacional

As tasks F2-T001..T005 registraram decisões humanas. F2-IMP-001..003 materializaram fundação de dados, grade de teste e fluxo de agendamento no ambiente de teste — sem publicação em produção e sem dado real. Nenhuma integração externa, conta real, conector ou publicação de produção foi criada.
