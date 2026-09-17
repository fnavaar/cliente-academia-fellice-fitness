# Estado atual — Adapta Cliente

- fase: 2
- task_id: F2-IMP-004
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-001-agenda-disponibilidade-e-reserva.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-17, Ricardo Junior: "vamos prosseguir"
- teste_humano: pendente
- verificacao_automatica: passou — Skip 51806 v0.0.31, pipeline completo ok; roteiro RED/GREEN/regressão executado ao vivo: (1) CONCORRÊNCIA — lead A CONCLUIDO no slot cap 1, lead B recusado pelo índice único e registrado como TENTATIVA com conflict_detected=true + evento APPOINTMENT_CONFLICT; (2) IDEMPOTÊNCIA — reenvio idêntico recusado (HTTP 400 validation_not_unique), 1 registro preservado; (3) DESISTÊNCIA — DESISTENCIA + APPOINTMENT_ABANDONED, slot liberado e re-reservado pelo lead D; (4) ROLLBACK — down-migration real executada (revertido até 0013): grade removida e recriada, tentativas/eventos preservados, ambiente restaurado (0017); limitação registrada: concorrência é provada pelo índice único do banco, não por transação distribuída
- aprendizado: pendente
- ultima_acao: roteiro de bordas executado; rollback real provado; ambiente restaurado (grade 248, fixtures 4, usuário de verificação ativo para o teste humano)
- proxima_acao: teste humano do consultor — conferir roteiro e registros; depois remover usuário de verificação (0018)
- gate: aceite humano antes de liberar F2-IMP-005
- limite: nenhuma publicação em produção, integração externa ou Fase 3 autorizada
- atualizado_em: 2026-09-17T16:30:00-03:00
