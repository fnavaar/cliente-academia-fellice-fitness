# Estado atual — Adapta Cliente

- task_id: F2-IMP-008
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-002-visao-operacional-tentativas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-18, Ricardo Junior: "Autorizo implementar após essas definições"; decisões: turnos 08:00–12:00, 12:00–16:00, 16:00–20:00; Mel com papel próprio `supervisora`; encerramento mantém `ENCAMINHAMENTO_HUMANO` com `closed_at`/motivo; reatribuição exclusiva de Gestão/Subgerente/Mel
- teste_humano: pendente — 21/09/2026: passos 1–3 e 5–7 OK; passo 4 reprovado no 1º teste (reatribuição bloqueada — debug r1, corrigido v0.0.74) e aprovado em parte no reteste (reatribuição gravou dono/responsavel_anterior/eventos, mas a UI não exibia o responsável anterior — debug r2, corrigido v0.0.75); reteste final do passo 4 pendente
- teste_humano_detalhe: fixtures sintéticas 008/008b/004/008r5 e contas temporárias 0044 mantidas até o aceite; credenciais não registradas no repositório
- verificacao_automatica: passou — v0.0.75 (`6b9f0f1`), pipeline completo OK; debug r1 provado via API (Gestão assume → Supervisora reatribui 200, PATCH direto 403); debug r2: `responsavel_anterior` confirmado no banco e agora renderizado no card da `/visao`
- aprendizado: pendente
- ultima_acao: debug r2 F2-IMP-008 — card da `/visao` passa a exibir "Reatribuída — responsável anterior: …" (v0.0.75); changelog completo restaurado (commit 1289943)
- proxima_acao: reteste final do passo 4 no preview v0.0.75 — confirmar a linha "Reatribuída — responsável anterior" no card; após aceite, limpeza das fixtures/usuários sintéticos e fechamento documental
- atualizado_em: 2026-09-21T10:45:00-03:00