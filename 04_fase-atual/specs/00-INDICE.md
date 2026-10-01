# Índice de SPECs — Fase 4

**Status:** SPECs geradas em 30/09/2026 na transição F3→F4 e aprovadas pelo consultor em 30/09–01/10 ("libero todas as specs, pode executar"); tasks geradas na Jornada da Fase 4.

## SPECs

| ID | Arquivo | Status | Dono |
|---|---|---|---|
| SPEC-4-001 | [spec-4-001-integracao-direta-ferramenta-comercial.md](spec-4-001-integracao-direta-ferramenta-comercial.md) | liberada — bloqueios B4-01, B4-02 e B4-05 (insumos embutidos nas tasks) | Champion do cliente |
| SPEC-4-002 | [spec-4-002-painel-saude-integracao-e-historico.md](spec-4-002-painel-saude-integracao-e-historico.md) | liberada — bloqueio B4-03 (insumo embutido na task) | Champion do cliente |
| SPEC-4-003 | [spec-4-003-loop-saude-da-conversao.md](spec-4-003-loop-saude-da-conversao.md) | liberada — bloqueio B4-04 + alvo aprovado (insumos embutidos na task) | Champion e Gestão |

## Dependências entre SPECs

- SPEC-4-001 (integração) é a base: SPEC-4-002 (painel) observa o estado da integração e SPEC-4-003 (loop) consome eventos da plataforma e o estado da integração.
- Sequência sugerida: SPEC-4-001 → SPEC-4-002 → SPEC-4-003.
- Todas dependem das fases 1–3 aceitas (SPEC-1-001/002, SPEC-2-001/002, SPEC-3-001/002).

## Bloqueios transversais da fase

| ID | Bloqueio | Dono | Especificado em | Origem |
|---|---|---|---|---|
| B4-01 | Base legal/consentimento LGPD e autorização de escrita externa | Champion | SPEC-4-001, SPEC-4-002, SPEC-4-003 | EV-F3-01 |
| B4-02 | Credenciais, permissões e capacidade do conector validados (Kommo e/ou Lóvavel) | Champion técnico | SPEC-4-001 | escopo F4 (call de setup) |
| B4-03 | Matriz de acesso ao painel de saúde | Champion | SPEC-4-002 | EV-F3-03 |
| B4-04 | Baseline operacional congelado (critério B3-05) | Champion | SPEC-4-003 | EV-F3-02 |
| B4-05 | Mapeamento de campos e regra de conflito/sobrescrita aprovados | Comercial/Champion | SPEC-4-001 | escopo F4 |

## Regras de construção (EV-F3-07)

- Allowlist explícita como autoridade de permissão (evitar dupla checagem por JSON — falso 403 de 30/09).
- Migrations aditivas e limpas (sem separadores de patch literais — migration 0054 de 30/09).
- Segredos fora do repositório; logs sanitizados; nenhuma escrita externa sem bloqueio liberado.

## Nota de liberação

Transição preparada em 30/09/2026 após o fechamento da Fase 3 (`check-fase-3.md` APROVADO COM RESSALVAS, active-sha256=7bbfdac4e985eac699880e3539ab59e529db3636fc77c8eec4af10377652ede3). SPECs aprovadas pelo consultor e tasks geradas em 01/10/2026; promoção F3→F4 neste repositório autorizada pelo consultor ("Confirmo o push: promova a Fase 4 no repositório da Fellice"). Nenhuma credencial, conector, escrita externa ou publicação de produção é autorizada por estas SPECs; execução uma task por vez com teste humano entre elas.
