# Estado atual — Adapta Cliente

- task_id: 124f370f-ea01-46d4-bdac-72c1cded2181
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-3-002-dashboard-campanha-e-baseline.md
- etapa: em_correcao
- autorizacao_implementacao: confirmada — 2026-09-28 16:22, Ricardo Junior: "pode implementar"
- teste_humano: falhou — 2026-09-30, Ricardo Junior informou estar bloqueado na tela `/dashboard`; screenshot mostra aviso de papel não autorizado
- verificacao_automatica: QA v0.0.83 passou em setup/static analysis/build/integrations/test; runtime autenticado falhou após login 200 com POST `/backend/v1/dashboard` 403
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-30-1502-enum-baseline-audit.md
- ultima_acao: logs Skip Cloud confirmam auth 200 e dashboard 403 em 18:45, 18:46 e 19:10 UTC; código atual lê `read_roles` JSON via `policy.get('read_roles')`; correção de normalização preparada mas ainda não aplicada
- proxima_acao: verificar por reprodução mínima o valor JSVM de `policy.get('read_roles')`, aplicar uma correção mínima no hook, executar QA de preview e pedir novo teste humano autenticado
- atualizado_em: 2026-09-30T16:11:49-03:00
