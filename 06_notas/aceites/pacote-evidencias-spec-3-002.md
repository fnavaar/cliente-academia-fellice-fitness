# Pacote de evidências — aceite da SPEC-3-002 (dashboard por formulário/campanha e baseline)

- **Task de revisão:** `e88283fc-42a2-48a5-9924-48b28dd4f0cb` — Revisar o aceite do dashboard
- **SPEC:** `04_fase-atual/specs/spec-3-002-dashboard-campanha-e-baseline.md`
- **Decisão:** ACEITE SEM RESSALVA — consultor Navaar, 30/09/2026 ("Aceitar a SPEC-3-002 sem ressalva")
- **Data do aceite:** 2026-09-30 17:50 (-03:00)

## O que foi conferido

| Item | Evidência |
|---|---|
| CA-3.06..10 (comparativo por vigência/origem/campanha; fórmula, período, cobertura e suficiência; não exposição de dados individuais; baseline append-only com estados `INSUFICIENTE`/`NAO_CALCULAVEL`; escrita exclusiva do Champion; rollback sem perda) | Conferidos no código e aceitos no teste humano do champion em 30/09/2026 |
| Verificação automática | QA completo Skip v0.0.85 (`c41cf7c`): setup, análise estática, build, integrações e testes; `node --check` e checks focados de RBAC/baseline |
| Prova de runtime autenticado | login `POST /api/collections/users/auth-with-password` HTTP 200 e `POST /backend/v1/dashboard` HTTP 200 em 30/09 20:05:58Z |
| Teste humano | champion: "Testei os critérios no preview e funcionou" (30/09/2026 17:07) |
| Matriz de acesso (B3-04) | allowlist explícita como autoridade após a correção do falso 403 (debug em `06_notas/debug/debug-2026-09-30-spec-3-002-dashboard-403.md`); papéis fora da matriz negados; somente Champion congela baseline |
| Regra de baseline (B3-05) | mês civil completo mais recente em `America/Bahia`, limiar de suficiência 50%, estados `INSUFICIENTE`/`NAO_CALCULAVEL`, apurações append-only |

## Notas do aceite (sem ressalva)

- **Baseline não congelado:** nenhuma versão operacional de baseline foi congelada nesta validação. O congelamento permanece como operação do Champion conforme B3-05 e não impede o aceite por decisão do consultor.
- **Conferência por evidência:** a matriz B3-04 nega acesso do Consultor ao dashboard; a revisão foi feita por código, QA, runtime e teste humano — mesmo padrão do aceite da SPEC-3-001.

## Estado

- Task `e88283fc` encerrada; SPEC-3-002 liberada; Fase 3 documentalmente concluída 9/9.
- Produção não publicada.
