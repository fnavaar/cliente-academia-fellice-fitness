# Status operacional

- **Fase atual:** Fase 2 — autoagendamento assistido e continuidade da jornada.
- **Caminho canônico:** `04_fase-atual/` — underscore depois de `04`; `04-fase-atual/` não existe.
- **Fase 1:** encerrada; F1-T001 a F1-T008 concluídas, com teste humano registrado para F1-T007 e F1-T008.
- **Fase 2:** desbloqueios documentais concluídos em 2026-09-16; implementação iniciada em 2026-09-17.
- **Progresso documental:** 5/5 tasks de decisão concluídas.
- **Progresso de implementação:** 1/9 tasks concluídas (11%); F2-IMP-002 é a próxima elegível.
- **Produto no preview:** triagem F1 disponível; fundação de dados da agenda criada no banco (coleções agenda_slots, lead_appointments, lead_appointment_events) — nenhuma tela nova; a rota do atendente é `/fila` (a auditoria de 16/09 registrou `/queue` por engano).
- **Bloqueios documentais:** resolvidos para SPEC-2-001 e SPEC-2-002.
- **Implementação:** F2-IMP-001 concluída com aceite humano em 2026-09-17; nenhuma publicação em produção.

## Tasks documentais concluídas

- F2-T001 — duração, capacidade e grade inicial. ✅ concluída — 2026-09-16
- F2-T002 — responsável por manter e fechar a agenda. ✅ concluída — 2026-09-16
- F2-T003 — campos mínimos para conclusão do agendamento. ✅ concluída — 2026-09-16
- F2-T004 — papéis, permissões e encaminhamento humano. ✅ concluída — 2026-09-16
- F2-T005 — escalada, encerramento e reatribuição de tentativas paradas. ✅ concluída — 2026-09-16

## Tasks de implementação

- F2-IMP-001 — contrato técnico e fixtures sintéticas de agenda/tentativa. ✅ concluída — 2026-09-17 (migrações 0007/0008 no Skip 51806 v0.0.20; pipeline QA ok; provas ao vivo: duplicata recusada, criação pública aceita, leitura anônima sem vazamento, leitura autenticada ok; teste humano aprovado pelo consultor; usuário sintético de teste removido após validação — 0010)
- F2-IMP-002 — grade de disponibilidade de teste. **Elegível.**
- F2-IMP-003 — seleção, validação e conclusão do agendamento. Bloqueada por F2-IMP-002 e aceite humano.
- F2-IMP-004 — conflito, idempotência, desistência, fallback e rollback. Bloqueada por F2-IMP-003 e aceite humano.
- F2-IMP-005 — TDD integrado e aceite da agenda. Bloqueada por F2-IMP-004 e evidências.
- F2-IMP-006 — visão operacional de tentativas. Bloqueada por F2-IMP-005 e aceite humano.
- F2-IMP-007 — permissões, fila, assunção e atualização segura. Bloqueada por F2-IMP-006 e aceite humano.
- F2-IMP-008 — escalada visual, reatribuição, encerramento e rollback. Bloqueada por F2-IMP-007 e aceite humano.
- F2-IMP-009 — TDD integrado e aceite da visão operacional. Bloqueada por F2-IMP-008 e evidências.

## Pendências registradas

- **LGPD (antes de F2-IMP-003):** validar com compliance a base legal da finalidade de agendamento — o consentimento F1-T004 cobre comunicações; o agendamento se apoia em execução de serviço solicitado. Registrado no contrato da F2-IMP-001, seção 7.
- **Semântica de reagendamento (RN-2.06):** decisão documentada no contrato (tentativa não confirmada é atualizada com o novo slot); validar com o Champion na próxima oportunidade.

## Próxima ação segura

Executar somente F2-IMP-002 no ambiente de teste, com fixtures sintéticas — materializar a grade decidida (30 min, capacidade 1, exceção 2 entre 11:30–16:30, seg–sex 08:00–19:30, sáb 09:00–13:30) sobre a fundação aprovada. Depois da prova e do teste humano, liberar F2-IMP-003. Nenhuma task seguinte, publicação ou Fase 3 é autorizada por este status.

## Limite operacional

As tasks F2-T001..T005 registraram decisões humanas. A F2-IMP-001 materializou a fundação de dados no ambiente de teste, sem telas, sem publicação e sem dado real. Nenhuma integração externa, conta real, conector ou publicação de produção foi criada.
