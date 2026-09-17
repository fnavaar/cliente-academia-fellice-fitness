# AP-2026-09-17-1938 — number required rejeita 0 e controle de capacidade por contagem

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-004 / SPEC-2-001 (debug)
- Sinal: (1) No PocketBase, campo `number` com `required: true` rejeita o valor 0 ("Cannot be blank") — 3 builds falharam antes da causa ser identificada; 0 é estado válido (slot vazio) e o campo não deve ser required. (2) Índice único composto impede apenas o MESMO lead no MESMO slot — não limita o total de reservas por slot; controle de capacidade exige contagem de reservas ativas por slot (coleção de ocupação) + filtro na oferta da página + bloqueio no clique. (3) Prova de conflito em slot de capacidade 1 disfarça a falta de controle de capacidade (a recusa vem da duplicidade, não da lotação) — testar sempre um slot de capacidade > 1.
- Evidência: builds v0.0.32–v0.0.34 falharam com "active: Cannot be blank"; v0.0.35 passou sem `required`; slot cap 2 chegou a 3 reservas CONCLUIDO antes da correção; debug summary em 06_notas/debug/debug-2026-09-17-capacidade-por-slot.md.
- Regra reutilizável: em coleções PocketBase, nunca usar `required: true` em number que pode valer 0; todo limite de capacidade por recurso exige (a) contador materializado com regras de acesso, (b) filtro na oferta, (c) bloqueio no clique; roteiros de borda devem exercitar capacidade > 1.
- Quando aplicar: qualquer modelagem de lotação/vagas no Skip Cloud; qualquer roteiro RED/GREEN de capacidade.
- Quando não aplicar: campos de texto ou booleanos, onde required não colide com valores falsy.
- Confiança: alta — falha reproduzida pelo teste humano, causa demonstrada por 3 builds idênticos e correção verificada no pipeline.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
