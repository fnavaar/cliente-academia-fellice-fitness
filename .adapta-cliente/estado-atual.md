# Estado atual — Adapta Cliente

- task_id: F2-IMP-008
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-002-visao-operacional-tentativas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-18, Ricardo Junior: "Autorizo implementar após essas definições"; decisões: turnos 08:00–12:00, 12:00–16:00, 16:00–20:00; Mel com papel próprio `supervisora`; encerramento mantém `ENCAMINHAMENTO_HUMANO` com `closed_at`/motivo; reatribuição exclusiva de Gestão/Subgerente/Mel
- teste_humano: pendente — testar `/visao` com papéis autorizados; conferir escalada visual sem mudança automática, reatribuição, encerramento mantendo `ENCAMINHAMENTO_HUMANO` e rollback preservando registros/eventos
- teste_humano_detalhe: fixtures sintéticas 008/008b e contas temporárias 0044 mantidas até o aceite; credenciais não registradas no repositório
- verificacao_automatica: passou — v0.0.73 (`50f3c16`), pipeline completo OK; provas ao vivo: logins 200, Consultor sem escalar/reatribuir 403, Supervisora reatribui 200, Gestão encerra 200 sem mudar status, PATCH direto 403, evento direto 403, rollback 200, ação durante rollback 400, restore 200, appointments/eventos preservados
- aprendizado: pendente
- ultima_acao: F2-IMP-008 implementada no Skip e verificada automaticamente; resumo salvo em `artifacts/f2-imp-008-qa-summary.md`
- proxima_acao: teste humano do fluxo real no preview; após aceite, limpeza das fixtures/usuários sintéticos e fechamento documental
- atualizado_em: 2026-09-18T10:48:00-03:00
