# AP-2026-09-17-1527 — record.set(objeto) falha no JSVM; slot opcional em tentativa

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-001 / SPEC-2-001
- Sinal: (1) No JSVM do PocketBase, `record.set(objeto)` com objeto único não popula os campos — o seed da migração 0008 gravou registros vazios e o pipeline falhou com "Cannot be blank" em todos os campos obrigatórios. O padrão que funciona é `record.set(chave, valor)` por campo (confirmando o aprendizado da F1-T007 com `useRef.current`). (2) Modelar `slot_id` como obrigatório na tentativa contradiz a RN-2.05: o encaminhamento humano (ENCAMINHAMENTO_HUMANO) pode nascer sem slot (ausência de disponibilidade). Campos de contexto do slot devem ser opcionais na criação; a obrigatoriedade é do estado CONCLUIDO (regra de fluxo).
- Evidência: pipeline v0.0.15 falhou com "capacity: Cannot be blank..." e passou na v0.0.16 após correção; QA v0.0.16–v0.0.20 ok; provas de idempotência (HTTP 400) e criação pública executadas contra o backend real.
- Regra reutilizável: em migrações JSVM, sempre usar `record.set(chave, valor)` (nunca objeto único); ao modelar estados de tentativa, campos de contexto só são obrigatórios no banco quando presentes em TODOS os caminhos que criam o registro — exigências de estados finais ficam no fluxo.
- Quando aplicar: qualquer migração de seed/criação de registros no Skip Cloud; qualquer modelagem de coleção com estados que nascem de caminhos diferentes (ex.: fallback humano sem slot).
- Quando não aplicar: hooks fora do JSVM ou APIs REST diretas, onde o payload de objeto é o padrão.
- Confiança: alta — falha e correção observadas no pipeline do próprio projeto, com versões registradas.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
