# Índice de SPECs — Fase 3

## SPECs liberadas

| ID | Arquivo | Status | Dono |
|---|---|---|---|
| SPEC-3-001 | [spec-3-001-consolidacao-eventos-e-funil.md](spec-3-001-consolidacao-eventos-e-funil.md) | tarefas de decisão liberadas ao Champion — implementação bloqueada por B3-01, B3-02 e B3-03 | Champion do cliente |
| SPEC-3-002 | [spec-3-002-dashboard-campanha-e-baseline.md](spec-3-002-dashboard-campanha-e-baseline.md) | tarefas de decisão liberadas ao Champion — implementação bloqueada por B3-01, B3-02, B3-04 e B3-05 | Champion do cliente |

## Dependências entre SPECs

- SPEC-3-002 depende de SPEC-3-001 testada e com aceite humano.
- Ambas dependem das SPECs das fases 1 e 2 aceitas: SPEC-1-001 e SPEC-1-002 (Fase 1 encerrada em 2026-09-10), SPEC-2-001 (aceita 2026-09-17) e SPEC-2-002 (aceita 2026-09-21).
- Os bloqueios de taxonomia (B3-01) e fórmula/janela (B3-02) são compartilhados: resolvidos uma vez, liberam as duas SPECs.

## Bloqueios transversais da fase

| ID | Bloqueio | Dono | Especificado em | Task de desbloqueio |
|---|---|---|---|---|
| B3-01 | Taxonomia de origem/campanha decidida e registrada | Champion | SPEC-3-001 e SPEC-3-002 | `45bb5d1b-b757-4d29-9afa-cee4d0077552` |
| B3-02 | Fórmula da métrica norte e janela padrão decididas e registradas | Champion | SPEC-3-001 e SPEC-3-002 | `2ce9c4fb-c143-4519-ba1f-e0ce80807e9b` |
| B3-03 | Decisão sobre vínculo triagem → agendamento (pendência herdada da F2) | Champion | SPEC-3-001 | `bcc00bba-0eb4-4821-9ccf-b74755969f43` |
| B3-04 | Matriz de acesso ao dashboard | Champion | SPEC-3-002 | `617b477e-d9f6-4256-ab84-530b932596fc` |
| B3-05 | Critério de congelamento do baseline decidido e registrado | Champion | SPEC-3-002 | `d30d0144-19d9-421d-b2a4-5c6bf4942533` |

## Nota de liberação

SPECs liberadas documentalmente no repositório do cliente em 2026-09-23. Em 2026-09-24, as cinco tarefas de decisão B3-01 a B3-05 foram liberadas ao Champion do cliente, que as registra em `03-Projeto/decisoes-fase-3.md`; Marketing/agência e Gestão podem ser consultados. A SPEC-3-001 aguarda B3-01..B3-03; a SPEC-3-002 aguarda B3-01, B3-02, B3-04 e B3-05, além do aceite da SPEC-3-001.
