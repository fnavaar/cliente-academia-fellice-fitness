# Estado atual — Adapta Cliente

- task_id: 4217198c-8077-4769-b2c0-7b7482136553
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-3-001-consolidacao-eventos-e-funil.md
- etapa: aguardando_autorizacao
- autorizacao_implementacao: ausente
- teste_humano: pendente — para esta task de revisão; os testes humanos da implementação foram aprovados em 25/09 ("Conferi a janela isolada de 23/09: os valores batem com as fixtures da SPEC-3-001." e "Conferi o recálculo determinístico e o rollback/reativação da SPEC-3-001 no preview; os dois passaram.")
- verificacao_automatica: passou — revisão de leitura em 25/09: CA-3.01..05 conformes com prova técnica (logs HTTP 200 de /backend/v1/funnel e /funnel/control, migrações 0050–0051 aplicadas, código de src/pages/Funil.tsx e funnel_aggregate.js inspecionado) e humana; pacote de evidências incompleto — faltam capturas do ambiente de teste e export sanitizado; logs de rollback existem apenas como logs de runtime do Skip Cloud
- aprendizado: pendente
- ultima_acao: análise da task de revisão de aceite concluída em 25/09/2026; nada registrado em fase/STATUS/changelog e nenhum aceite declarado
- proxima_acao: aguardar autorização para registrar o resultado da revisão e a juntada (ou pendência formal) das evidências ausentes
- atualizado_em: 2026-09-25T17:15:00-03:00
