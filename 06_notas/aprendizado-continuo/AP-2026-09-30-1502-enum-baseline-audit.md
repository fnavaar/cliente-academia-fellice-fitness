# AP-2026-09-30-1502 — conferir enums de eventos antes de gravar baseline

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: `124f370f-ea01-46d4-bdac-72c1cded2181` / SPEC-3-002
- Sinal: a coleção `lead_dashboard_baseline_events` tinha `action` como select com o único valor `FROZEN`. A revisão detectou que dois estados de baseline propostos como novas ações não seriam aceitos pelo schema existente; eles foram mantidos nos campos do baseline e no payload do evento, preservando a ação `FROZEN`.
- Evidência: definição da coleção Skip Cloud lida em 2026-09-30; migration 0054; QA v0.0.83 passou e migration foi aplicada.
- Regra reutilizável: antes de emitir um novo valor em um select de auditoria, ler a definição ativa da coleção e confirmar que o enum foi estendido na mesma migration; quando o enum for intencionalmente estável, preservar a ação existente e registrar detalhe no payload versionado.
- Quando aplicar: novas transições/auditorias escritas em coleções PocketBase com campos select.
- Quando não aplicar: enums que a SPEC declara fechados e não permite alterar; nesses casos, não inventar estados nem contornar a validação.
- Confiança: alta — schema ativo confirmou o conjunto permitido e migration/QA passaram após manter `FROZEN`.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
