# Estado atual — Adapta Cliente

- task_id: ab9ce40f-304e-4ef6-929f-1efa7f7a0a87
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-3-001-consolidacao-eventos-e-funil.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-24 17:00, Ricardo Junior: "Autorizo implementar a consolidação da SPEC-3-001 conforme o plano analisado."
- teste_humano: em andamento — 2026-09-25 16:32, login autenticado no preview com HTTP 200 (log 19:32:32 UTC) e consultas ao funil com HTTP 200; Ricardo relatou valores divergentes das fixtures informadas. Diagnóstico: a janela padrão de 30 dias (27/08–25/09) agrega também as fixtures-base preservadas das Fases 1 e 2 e resíduos dos testes humanos anteriores, não apenas as fixtures 0051 de 23/09; a tabela de conferência enviada descrevia somente o dia 23/09. Números da tela internamente consistentes (14÷7=200%; 5/16=31,3%).
- verificacao_automatica: passou — v0.0.81 (96ce32e), QA completo; autenticação real confirmada pelos logs (HTTP 200) e endpoint `/backend/v1/funnel` respondendo 200 autenticado.
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-25-0834-autenticacao-antes-do-papel.md
- ultima_acao: login e leitura do funil confirmados nos logs; divergência de contagens diagnosticada como composição da janela de 30 dias (fixtures-base 0003/0008/0028/0030 preservadas + fixtures 0051), não como erro de fórmula; pendente conferência da janela isolada 23/09
- proxima_acao: Ricardo conferir o funil com De=23/09/2026 e Até=23/09/2026 e comparar com as fixtures 0051 (6/6/5/2/2, taxa 100%, cobertura 50%, 1 órfão)
- atualizado_em: 2026-09-25T16:37:05-03:00