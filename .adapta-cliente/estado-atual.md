# Estado atual — Adapta Cliente

- fase: 2
- task_id: F2-IMP-004
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-001-agenda-disponibilidade-e-reserva.md
- etapa: em_correcao
- autorizacao_implementacao: confirmada — 2026-09-17, Ricardo Junior: "vamos prosseguir"
- teste_humano: falhou — 2026-09-17, Ricardo Junior: "estou agendando no mesmo horário que tem informado 2 vagas e está permitindo mais de 2" — relato correto; reproduzido: slot cap 2 com 3 reservas CONCLUIDO; a capacidade não é controlada em nenhuma camada (o índice único só impede o MESMO lead no MESMO slot)
- teste_humano_detalhe: a prova de concorrência da F2-IMP-004 usou slot cap 1 (índice único recusa o 2º) e não exercitou o limite de capacidade 2 — lacuna da prova, não do modelo
- verificacao_automatica: passou parcialmente — roteiro de bordas ok exceto o limite de capacidade por slot, que exige controle de contagem (não existe no contrato atual)
- aprendizado: pendente
- ultima_acao: falha reproduzida e causa raiz identificada — falta enforcement de capacidade (contagem de reservas ativas por slot)
- proxima_acao: implementar controle de capacidade na página /agendar (contagem de reservas ativas por slot antes de confirmar) + migração de limpeza das reservas de teste excedentes
- gate: debug em curso; volta ao teste humano após a correção
- limite: nenhuma publicação em produção, integração externa ou Fase 3 autorizada
- atualizado_em: 2026-09-17T16:30:00-03:00
