# AP-2026-09-25-1646 — Comparar fixtures do funil por janela isolada

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: `ab9ce40f-304e-4ef6-929f-1efa7f7a0a87` / SPEC-3-001
- Sinal: a comparação com a janela padrão de 30 dias misturou as fixtures específicas da SPEC com fixtures-base preservadas; ao isolar 2026-09-23, os valores bateram com o conjunto de fixtures. O responsável confirmou também recálculo determinístico e rollback/reativação no preview.
- Evidência: logs autenticados do Skip em 2026-09-25 para consultas repetidas `GET /backend/v1/funnel?from=2026-09-23&to=2026-09-23` e controles HTTP 200; confirmação humana no ciclo de teste da task; `changelog.md`.
- Regra reutilizável: ao conferir agregados contra fixtures sintéticas de uma data específica, filtrar primeiro exatamente o período de semeadura. Se o período amplo contiver fixtures históricas preservadas, não tratar a diferença como erro antes de repetir a conferência na janela isolada.
- Quando aplicar: validação de métricas ou contagens esperadas para fixtures semeadas em uma janela conhecida.
- Quando não aplicar: análises cujo objetivo seja incluir intencionalmente várias coortes, campanhas ou todo o histórico disponível.
- Confiança: alta — a comparação isolada foi aprovada pelo responsável e as consultas do período aparecem nos logs autenticados.
- Privacidade: sem credenciais, contatos reais ou dados pessoais.
