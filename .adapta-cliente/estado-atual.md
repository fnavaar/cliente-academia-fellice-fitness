# Estado atual — Adapta Cliente

- fase: 2
- task_id: F2-IMP-004
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-001-agenda-disponibilidade-e-reserva.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-17, Ricardo Junior: "vamos prosseguir"
- teste_humano: falhou e corrigido — Ricardo reproduziu a falha de capacidade (slot cap 2 aceitou 3+); debug executado; aguardando reteste
- teste_humano_detalhe: falha reproduzida e corrigida — ver debug summary no changelog
- verificacao_automatica: passou — v0.0.40, pipeline completo ok; correção em 3 camadas: (1) migração 0018 criou agenda_slot_occupancy (ocupação por slot, recalculada, leitura pública, escrita só consultor/champion); (2) página /agendar esconde slot cheio (active >= capacity), mostra vagas restantes e bloqueia clique; (3) ambiente limpo (0020 removeu as reservas de teste, deleteRule null provado — API recusa DELETE anônimo/consultor, HTTP 403)
- aprendizado: pendente
- ultima_acao: debug concluído — capacidade controlada, ambiente limpo (4 fixtures, ocupação zerada, grade 248)
- proxima_acao: reteste humano do consultor — reservar 2 vagas num slot cap 2 e confirmar que a 3ª é bloqueada
- gate: aceite humano antes de liberar F2-IMP-005
- limite: nenhuma publicação em produção, integração externa ou Fase 3 autorizada
- atualizado_em: 2026-09-17T16:45:00-03:00
