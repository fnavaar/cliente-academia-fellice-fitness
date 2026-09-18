# Status operacional

- **Fase atual:** Fase 2 — autoagendamento assistido e continuidade da jornada.
- **Caminho canônico:** `04_fase-atual/` — underscore depois de `04`; `04-fase-atual/` não existe.
- **Fase 1:** encerrada; F1-T001 a F1-T008 concluídas, com teste humano registrado para F1-T007 e F1-T008.
- **Fase 2:** desbloqueios documentais concluídos em 2026-09-16; implementação em curso desde 2026-09-17 — F2-IMP-007 concluída com aceite humano em 2026-09-18.
- **Progresso documental:** 5/5 tasks de decisão concluídas.
- **Progresso de implementação:** 7/9 tasks concluídas (78%); **SPEC-2-001 ACEITA**; F2-IMP-008 é a próxima elegível.
- **Produto no preview:** triagem F1; grade de teste (248 slots); página /agendar com fechadura de capacidade no servidor; **página /visao funcional** — visão operacional de tentativas com contexto da triagem (objetivo, proximidade, ocupação, interesse, UTMs), filtros por estado e detalhe completo; **fila com assunção segura** — botão "Assumir caso" grava dono + assumed_at pelo servidor e evento APPOINTMENT_ASSUMED; rota do atendente `/fila`.
- **Bloqueios documentais:** resolvidos para SPEC-2-001 e SPEC-2-002.
- **Implementação:** F2-IMP-001..006 concluídas com aceite humano em 2026-09-17; F2-IMP-007 concluída com aceite humano em 2026-09-18; nenhuma publicação em produção.

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
- F2-IMP-004 — conflito, idempotência, desistência, fallback e rollback. ✅ concluída — 2026-09-17 (fechadura de capacidade no servidor: hook enforce_slot_capacity.js em create/update/delete + contador agenda_slot_occupancy sincronizado + página esconde slot cheio/mostra vagas restantes; 2 rodadas de debug documentadas em 06_notas/debug/; provas: 2 reservas aceitas em cap 2, 3ª recusada HTTP 400, desistência libera vaga, rollback preserva histórico, DELETE via API recusado 403; teste humano aprovado "testado e funcionou"; ambiente limpo — v0.0.45)
- F2-IMP-005 — TDD integrado e aceite da agenda. ✅ concluída — 2026-09-17 (**SPEC-2-001 ACEITA pelo Champion**): pacote de evidências e roteiro de teste publicados; teste humano 5/5 cenários; veredito ACEITO no recibo do fase.md; revalidação independente 5/5 + ambiente limpo (v0.0.48)
- F2-IMP-006 — visão operacional de tentativas. ✅ concluída — 2026-09-17 (página /visao no Skip 51806 v0.0.59: login autenticado, lista com filtros por estado e contadores, contexto da triagem completo no card e no detalhe, motivo do encaminhamento em destaque; campos de contexto em lead_appointments (0029) preenchidos nas fixtures (0030); hook copia o contexto da triagem no create — prova 0031 de herança completa; CA-2.08 provado (recriação recusada 400); debug de sessão órfã corrigido (bootstrap com authRefresh); teste humano aprovado ("verificado" — 4 tentativas, filtros corretos, contexto completo, sem botões de ação); usuário sintético removido — 0034)
- F2-IMP-007 — permissões, fila e assunção de tentativas. ✅ concluída — 2026-09-18 (RBAC pelas regras das coleções lead_appointments/lead_appointment_events + hook protect_assumption.js como defesa em profundidade; migrações 0035–0039; debug r1 documentado em 06_notas/debug/ (actor_id vazio — authStore lido no momento do clique); provas ao vivo v0.0.66: assunção grava dono+assumed_at (servidor) + evento APPOINTMENT_ASSUMED, troca/remoção de dono recusadas 400, papel gestao sem leitura (0 itens) e sem escrita (404); teste humano aprovado ("Testei e funcionou"); revalidação independente 7/7 provas refazeitas do zero; limpeza pós-aceite — 0040 no-op silencioso corrigido pela 0041 (aprendizado AP-2026-09-18-0940): usuários sintéticos removidos (login 400), tentativas 007/007b e eventos delas removidos; v0.0.71)
- F2-IMP-008 — escalada visual, reatribuição, encerramento e rollback. **Elegível** (pré-condição F2-IMP-007 aceita).
- F2-IMP-009 — TDD integrado e aceite da visão operacional. Bloqueada por F2-IMP-008 e evidências.

## Pendências registradas

- **LGPD (validar com compliance):** base legal da finalidade de agendamento — o consentimento F1-T004 cobre comunicações; o agendamento se apoia em execução de serviço solicitado. Registrado no contrato da F2-IMP-001, seção 7. A página /agendar já coleta os campos sob essa base provisória documentada.
- **Semântica de reagendamento (RN-2.06):** implementada e provada na F2-IMP-003 (tentativa não confirmada é atualizada com o novo slot, sem duplicar); validar com o Champion na próxima oportunidade.
- **Capacidade 2 no sábado [VALIDAR NA CALL DE SETUP]:** a regra da F2-T001 não distingue dia da semana; a grade gerada aplica capacidade 2 também aos blocos de sábado dentro da janela 11:30–13:00. Se o sábado deve ficar todo com capacidade 1, ajustar em emenda da SPEC.
- **Continuidade triagem → agendamento (achado do consultor, 17/09):** botão "Agende aqui" no painel lateral da triagem; lead redigita nome/canal na /agendar e o agendamento não herda o lead_submission_id da triagem. Decisão do Champion pendente: aceitar como está, mover o botão para o final do fluxo e/ou implementar a passagem de contexto.
- **Fortalecimento do CA-2.03 (pós-aceite):** validação de campos mínimos hoje no fluxo da página; via API direta o servidor ainda não rejeita CONCLUIDO sem campos — recomendada task de fortalecimento no servidor.
- **Restrição de leitura por atribuição (F2-IMP-008):** o consultor hoje lê todas as tentativas (fila única); a visão restrita "só as atribuídas a ele ou em ENCAMINHAMENTO_HUMANO" entra na F2-IMP-008 junto da escalada, conforme registrado no changelog da F2-IMP-007.

## Próxima ação segura

Executar somente F2-IMP-008 (escalada visual, reatribuição, encerramento e rollback da fila, SPEC-2-002) no ambiente de teste — com análise, autorização explícita e teste humano. Nenhuma publicação em produção ou Fase 3 é autorizada por este status.

## Limite operacional

As tasks F2-T001..T005 registraram decisões humanas. F2-IMP-001..007 materializaram fundação de dados, grade de teste, fluxo de agendamento, fechadura de capacidade, aceite formal da SPEC-2-001, visão operacional de leitura e fila com assunção segura no ambiente de teste — sem publicação em produção e sem dado real. Nenhuma integração externa, conta real, conector ou publicação de produção foi criada.
