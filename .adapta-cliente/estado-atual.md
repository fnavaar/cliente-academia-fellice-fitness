# Estado atual — Adapta Cliente

- task_id: 124f370f-ea01-46d4-bdac-72c1cded2181
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-3-002-dashboard-campanha-e-baseline.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-28 16:22, Ricardo Junior: "pode implementar"
- teste_humano: pendente — aguarda novo teste autenticado após correção em 2026-09-30
- verificacao_automatica: passou — Skip v0.0.85 `c41cf7c`; setup, análise estática, build, integrações e testes aprovados; smoke sem token retornou 401 esperado
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-30-1639-dashboard-rbac-json.md
- ultima_acao: hook corrigido para usar allowlist B3-04 explícita como autoridade, mantendo `b3_04_confirmed`, negativas para papéis fora da matriz e freeze exclusivo do Champion; QA v0.0.85 completo passou; `/dashboard` abre login e endpoint anônimo retorna 401
- proxima_acao: Ricardo executar teste humano autenticado no preview v0.0.85; validar leitura autorizada, negativas de leitura/escrita, dados agregados, baseline e rollback
- atualizado_em: 2026-09-30T16:43:32-03:00
