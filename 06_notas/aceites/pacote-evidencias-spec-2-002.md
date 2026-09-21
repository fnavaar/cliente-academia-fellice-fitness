# Pacote de evidências — SPEC-2-002 (F2-IMP-009)

**Data:** 2026-09-21 · **Ambiente:** preview https://fellice-fitness-8733f--preview.goskip.app · **Versão:** v0.0.77 (`a3c644b`) · **Dados:** 100% sintéticos (fixtures da migração 0047, removíveis)

## Baseline da consolidação (v0.0.76, pré-task)

- Migrações 0001–0046 aplicadas; coleções `lead_appointments`, `lead_appointment_events`, `lead_queue_settings`, `lead_queue_control_events` com contrato e RLS conforme SPEC.
- Rotas `/`, `/agendar`, `/fila`, `/visao` respondendo 200 no preview.
- Logs sem erro novo — apenas bloqueios esperados das provas anteriores (logins sintéticos removidos, ações recusadas por design).

## Provas executadas nesta consolidação (24 verificações via API do backend)

### CA-2.06 — Toda tentativa aparece na visão com estado, contexto e dados

| # | Prova | Resultado |
|---|---|---|
| 1 | Champion lê todas as tentativas (6 fixtures 0047 + 4 fixtures-base) | PASSOU — 10 itens, 4 estados presentes |
| 2 | Gestão lê todos os estados | PASSOU — 10 itens |
| 3 | Contexto da triagem (objetivo, proximidade, ocupação, interesse) + origem/campanha (`attribution_status=recebida` + UTMs) + `form_version` | PASSOU |
| 4 | Dados de agendamento quando existem (`concluded_at`, duração 30 min) | PASSOU |
| 5 | Visibilidade do Consultor conforme matriz F2-T004: vê somente tentativas atribuídas a ele ou em `ENCAMINHAMENTO_HUMANO` | PASSOU — consultor B vê 4 itens, todos em `ENCAMINHAMENTO_HUMANO`; zero vazamento de `TENTATIVA`/`CONCLUIDO`/`DESISTENCIA`; filtro direto de estado fechado retorna 0 itens |
| 6 | Trilha de eventos coerente por tentativa (ex.: `CONCLUIDO` → `APPOINTMENT_CREATED` + `APPOINTMENT_CONCLUDED`) | PASSOU |

> Nota de transparência: a primeira rodada da prova 5 usou uma asserção mais restritiva que a matriz aprovada (esperava que o consultor não visse tentativa em `ENCAMINHAMENTO_HUMANO` assumida por outro consultor). A matriz F2-T004 prevê a fila única visível com dono exibido; a asserção foi corrigida e a regra confirmada. Nenhuma mudança de produto foi necessária.

### CA-2.07 — Dono inicial e assunção registram responsável e `assumed_at`

| # | Prova | Resultado |
|---|---|---|
| 7 | Consultor autorizado assume tentativa sem dono via ação atômica | PASSOU — HTTP 200, evento `APPOINTMENT_ASSUMED`, dono gravado |
| 8 | `dono` + `assumed_at` gravados; estado permanece `ENCAMINHAMENTO_HUMANO` | PASSOU |
| 9 | Segunda assunção do mesmo caso recusada | PASSOU — HTTP 400 "Caso já assumido." |

### CA-2.08 — Reprocessamento não duplica

| # | Prova | Resultado |
|---|---|---|
| 10 | Reenvio do mesmo `appointment_id` recusado | PASSOU — HTTP 400 (índice único `appointment_id` e `(lead_submission_id, slot_id)`) |
| 11 | Registro único preservado, sem alteração de conteúdo | PASSOU |

### CA-2.09 — Sem permissão / falha não muda estado; pendência visível

| # | Prova | Resultado |
|---|---|---|
| 12–14 | Consultor sem permissão em REASSIGN / ESCALATE / CLOSE | PASSOU — HTTP 403 nos três |
| 15 | PATCH direto de `dono` por não autorizado | PASSOU — HTTP 403 "Use a ação operacional autorizada" |
| 16 | Falha de ação (reassunção indevida) não confirma operação | PASSOU — HTTP 400 |
| 17 | Estado, dono e trilha intactos após as falhas (eventos 3 → 3) | PASSOU |

### CA-2.10 — Rollback/restore preserva registros e eventos

| # | Prova | Resultado |
|---|---|---|
| 18 | ROLLBACK desativa as ações da fila | PASSOU — HTTP 200, `enabled=false` |
| 19 | Ação de fila bloqueada durante rollback | PASSOU — HTTP 400 "ações da fila estão temporariamente desativadas" |
| 20 | Registros permanecem legíveis durante o rollback | PASSOU — 10 itens |
| 21 | Controle da fila registra estado e trilha de eventos | PASSOU |
| 22 | RESTORE reativa a fila | PASSOU — HTTP 200, `enabled=true` |
| 23–24 | Estado final das tentativas preservado após o ciclo completo | PASSOU |

**Resumo:** 24/24 verificações bem-sucedidas (23 na rodada única + asserção 5 corrigida conforme matriz F2-T004, sem mudança de produto).

## Provas históricas das tasks originais

- **F2-IMP-006** (CA-2.06/CA-2.08): criação da `/visao`, herança de contexto da triagem (prova 0031), idempotência — teste humano aprovado em 17/09/2026.
- **F2-IMP-007** (CA-2.07/CA-2.09): RBAC pelas regras das coleções + hook `protect_assumption`, fila única, dono/`assumed_at` — teste humano aprovado em 18/09/2026.
- **F2-IMP-008** (CA-2.09/CA-2.10): escalada visual, reatribuição formal, encerramento com motivo, papel `supervisora`, rollback/restore — teste humano aprovado em 21/09/2026.

## Pendências de decisão consciente no aceite (herdadas do aceite da SPEC-2-001)

1. **LGPD** — base legal do agendamento.
2. **RN-2.06** — semântica de reagendamento (reescolha de slot atualiza a mesma tentativa).
3. **Capacidade 2 no sábado** — interpretação da janela 11:30–16:30 [VALIDAR].
4. **Vínculo triagem → agendamento** — hoje apenas estrutural (o agendamento não herda o `lead_submission_id` da triagem).

## Limites

- Tudo em preview; produção não publicada; nenhuma integração externa; nenhum dado real de lead.
- Fixture 0047 e usuários sintéticos serão removidos em migração de limpeza após o aceite, no padrão 0046.
