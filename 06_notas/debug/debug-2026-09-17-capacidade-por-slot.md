# DEBUG F2-IMP-004 — Falha de capacidade por slot (2026-09-17)

## Task e problema

**Task:** F2-IMP-004 (prova de conflito, idempotência, desistência e rollback)
**Problema relatado pelo consultor (Ricardo Junior):** "estou agendando no mesmo horário que tem informado 2 vagas e está permitindo mais de 2" — teste humano correto, falha real reproduzida.

## Reprodução

- Consulta à coleção `lead_appointments` com login de verificação confirmou: slot `slot-2026-09-21-1230` (capacidade 2) com **3 reservas CONCLUIDO**; slots cap 1 também excedidos (2 reservas).
- As reservas excedentes foram criadas pelo próprio teste humano do consultor via página `/agendar` — o fluxo aceitava qualquer reserva sem contar a ocupação.

## Causa raiz

**Nenhuma camada controlava a capacidade por slot.** O índice único `(lead_submission_id, slot_id)` impede apenas o **mesmo lead** reservar o **mesmo slot** duas vezes — não limita o total de leads por slot. A página `/agendar` ofertava todos os slots `ABERTO` sem verificar quantas reservas ativas já existiam. A regra RN-2.01 ("carregar somente slots com capacidade disponível") e a CA-2.02 (limite de confirmações por slot) não tinham enforcement.

**Lacuna da prova (transparência):** o roteiro da F2-IMP-004 testou conflito num slot de capacidade 1, onde o índice único disfarçou o controle de capacidade — a segunda reserva era recusada por duplicidade, não por lotação. O caso capacidade 2 não foi exercitado.

## Correção (3 camadas)

1. **Migração 0018 — coleção `agenda_slot_occupancy`:** 1 registro por slot (`slot_id`, `capacity`, `active` = reservas ativas), recalculada a partir das tentativas existentes. Leitura pública (a página precisa), escrita só `champion`/`consultor`. A ocupação é a fonte de verdade do "quantas vagas restam".
2. **Página `/agendar`:** carrega a ocupação junto com a grade; **esconde slots cheios** (`active >= capacity`), mostra **vagas restantes** no selo ("2 vagas" → "1 vaga") e **bloqueia o clique** em slot cheio (defesa em profundidade, caso a ocupação mude após o carregamento).
3. **Migrações 0019/0020 — limpeza:** removeram as reservas de prova e as do teste humano que reproduziram a falha, zerando a ocupação para o reteste. Observação de segurança positiva: a tentativa de apagar via API com login de consultor foi **recusada (HTTP 403)** — `deleteRule: null` funciona; a limpeza só foi possível via migração (superuser do JSVM), como o modelo manda.

## Verificação automática

- Pipeline completo ok (v0.0.40): setup, análise estática, build, integrações, testes.
- Ocupação recalculada corretamente: slots com reservas mostraram contagens exatas (2/1, 2/2, 1/2, 3/2, 1/2) antes da limpeza — a contagem funciona.
- Página `/agendar` HTTP 200 após a mudança.
- Ambiente final limpo: 248 slots, 4 fixtures, ocupação zerada.

**Nota de depuração técnica:** durante o desenvolvimento da 0018, o campo `active` como `number required: true` rejeitou o valor 0 ("Cannot be blank") em 3 builds — o PocketBase trata 0 como blank em number required. Corrigido removendo o `required` (0 é estado válido: slot vazio).

## Gate atual

**aguardando teste humano** — reteste pelo consultor: reservar 2 vagas num slot de capacidade 2 e confirmar que a 3ª é bloqueada (slot some da grade ou o clique é recusado).
