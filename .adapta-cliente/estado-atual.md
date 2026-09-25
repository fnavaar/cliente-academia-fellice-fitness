# Estado atual — Adapta Cliente

- task_id: ab9ce40f-304e-4ef6-929f-1efa7f7a0a87
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-3-001-consolidacao-eventos-e-funil.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-24 17:00, Ricardo Junior: "Autorizo implementar a consolidação da SPEC-3-001 conforme o plano analisado."
- teste_humano: em andamento — 2026-09-25 16:39, Ricardo confirmou: "Conferi a janela isolada de 23/09: os valores batem com as fixtures da SPEC-3-001." Consulta autenticada da janela isolada observada no log como HTTP 200; fixtures conferidas pelo responsável. Restam os critérios de recálculo determinístico e rollback sem perda de eventos.
- verificacao_automatica: passou — v0.0.81 (96ce32e), QA completo; autenticação real e endpoint `/backend/v1/funnel` respondem HTTP 200; preview ativo; produção não publicada.
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-25-0834-autenticacao-antes-do-papel.md
- ultima_acao: confirmado que discrepância anterior veio da janela padrão de 30 dias incluir fixtures-base preservadas; teste humano da janela isolada 23/09 passou conforme confirmação de Ricardo; SPEC-3-001 ainda não concluída
- proxima_acao: Ricardo validar no preview que atualização repetida do mesmo período retorna os mesmos valores e, se autorizado pelo seu papel, testar rollback/reativação sem perda de eventos; depois informar o resultado
- atualizado_em: 2026-09-25T16:40:43-03:00
