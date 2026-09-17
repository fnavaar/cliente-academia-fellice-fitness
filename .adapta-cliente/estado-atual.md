# Estado atual — Adapta Cliente

- fase: 2
- task_id: F2-IMP-004
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-001-agenda-disponibilidade-e-reserva.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-17, Ricardo Junior: "vamos prosseguir"
- teste_humano: falhou 2x e corrigido — 1ª falha: nenhuma camada contava ocupação (corrigida na rodada 1); 2ª falha (reteste): página escondia slot cheio mas o contador não era atualizado e o servidor aceitava acima da capacidade via API direta (corrigida na rodada 2 com hook de servidor); aguardando 2º reteste
- teste_humano_detalhe: rodada 2 — hook enforce_slot_capacity.js em lead_appointments (create/update/delete): conta reservas ativas (CONCLUIDO+TENTATIVA) por slot, rejeita acima da capacidade com HTTP 400 "Este horário acabou de encher", sincroniza agenda_slot_occupancy após cada escrita; migração 0021 ressincronizou contadores e limpou provas
- verificacao_automatica: passou — v0.0.43, pipeline completo ok; provas ao vivo: recusa em slot cheio (HTTP 400), 2 reservas aceitas em cap 2 (200/200), 3ª recusada (400), desistência libera vaga (PATCH 200 + nova reserva 200), contador correto (2/2), cenário exato do reteste reproduzido e recusado sem efeito colateral
- aprendizado: pendente
- ultima_acao: fechadura de capacidade no servidor implementada e provada; contadores ressincronizados; ambiente com 7 reservas (3 do teste humano no slot 1200 — recusa ativa para novas, 4 fixtures)
- proxima_acao: 2º reteste humano — reservar 2 vagas num slot cap 2 e confirmar que a 3ª é recusada; depois fechamento e limpeza das 3 reservas do teste humano via migração
- gate: aceite humano antes de liberar F2-IMP-005
- limite: nenhuma publicação em produção, integração externa ou Fase 3 autorizada
- atualizado_em: 2026-09-17T17:05:00-03:00
