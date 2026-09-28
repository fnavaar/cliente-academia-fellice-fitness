# Pacote de evidências — SPEC-3-001 (revisão de aceite)

**Data:** 2026-09-28 · **Ambiente:** preview https://fellice-fitness-8733f--preview.goskip.app · **Versão:** v0.0.81 (`96ce32e`) · **Dados:** 100% sintéticos (fixtures da migração 0051)  
**Task de revisão:** `4217198c-8077-4769-b2c0-7b7482136553` · **Resultado:** ACEITO — sem ressalva (decisão do consultor Navaar em 28/09/2026).

## Baseline da revisão

- Implementação concluída e validada no preview v0.0.81 em 25/09/2026 (QA completo; migrações 0050–0051 aplicadas; testes humanos registrados no changelog).
- B3-01, B3-02 e B3-03 registradas em `03_documentos/decisoes-fase-3.md` (24/09/2026).
- Produção não publicada; nenhuma integração externa; consolidação somente leitura.

## Provas executadas nesta revisão (28/09/2026)

### Prova técnica (Skip Cloud, projeto 51806)

| # | Prova | Resultado |
|---|---|---|
| 1 | Migrações 0050 (`create_funnel_control`) e 0051 (`seed_spec3001_fixtures`) aplicadas | PASSOU — status `applied` na listagem do Skip Cloud |
| 2 | Consulta autenticada do funil | PASSOU — logs `GET /backend/v1/funnel?from=2026-09-23&to=2026-09-23` HTTP 200 (19:38:30 UTC e repetições 19:42–19:43 UTC) e janelas de 30 dias (`from=2026-08-27&to=2026-09-25`) HTTP 200 |
| 3 | Proteção da consulta | PASSOU — `GET /backend/v1/funnel` sem token retornou 401 (24/09 20:13 UTC) |
| 4 | Rollback/reativação com motivo obrigatório | PASSOU — `POST /backend/v1/funnel/control` HTTP 200 (19:42:34 e 19:42:49 UTC) |
| 5 | Inspeção do backend (`pocketbase/hooks/funnel_aggregate.js`) | PASSOU — RBAC champion/gestão/supervisora; janela padrão de 30 dias; leitura parcial marca `partial` e zera a taxa; deduplicação por `appointment_id` e chaves de encaminhamento; resposta só com agregados |
| 6 | Inspeção do frontend (`src/pages/Funil.tsx`) | PASSOU — 5 etapas do funil; numerador/denominador/taxa/período; grupos de cobertura incluindo "Status ausente/não reconhecido"; vínculo triagem→agendamento como cobertura incompleta; controle com motivo obrigatório; aviso "sem nome, telefone, e-mail ou registros individuais" |

### Prova humana (registrada em 25/09/2026 no changelog)

| # | Prova | Resultado |
|---|---|---|
| 7 | Contagens da janela isolada 23/09 contra fixtures | PASSOU — "os valores batem com as fixtures da SPEC-3-001" (16:39) |
| 8 | Recálculo determinístico e rollback/reativação | PASSOU — "os dois passaram" (16:43) |

## Matriz critério → prova (CA-3.01..05)

| Critério | Conforme | Prova |
|---|---|---|
| CA-3.01 — etapas entrada, início, conclusão da triagem, encaminhamento e agendamento concluído por período | SIM | provas 2, 5, 6, 7 |
| CA-3.02 — toda taxa mostra numerador, denominador e período; sem os três não há indicador | SIM | provas 5, 6 (taxa nula quando parcial) |
| CA-3.03 — registros sem `attribution_status` permanecem visíveis e entram na cobertura | SIM | provas 5, 6 |
| CA-3.04 — agendamento concluído sem submissão vinculada = cobertura incompleta, sem atribuição inventada | SIM | provas 5, 6 |
| CA-3.05 — mesmo período recalcula igual; reagendamento/reprocessamento não duplica | SIM | provas 5, 8 |

## Evidência considerada no aceite

| Evidência | Situação | Detalhe |
|---|---|---|
| Conferência de contagens contra fixtures | PRESENTE | Teste humano 25/09 16:39 + log HTTP 200 (19:38:30 UTC) |
| Recálculo determinístico e rollback/reativação | PRESENTE | Teste humano 25/09 16:43 + logs `POST /funnel/control` HTTP 200 |
| Não exposição de contatos (objeto do "export sanitizado") | PRESENTE | Verificada em `src/pages/Funil.tsx` e `funnel_aggregate.js` (somente agregados) e no aviso da tela |
| Proteção da consulta | PRESENTE | `GET /funnel` sem token → HTTP 401 |
| Aceite humano | REGISTRADO | Decisão do consultor Navaar, 28/09/2026 (sem ressalva); task `4217198c` encerrada |

Meio de evidência: logs de runtime do Skip Cloud, inspeção de código e testes humanos de 25/09. Capturas de tela e logs documentais de rollback não foram produzidos e foram dispensados por decisão do consultor.

## Aceite

**ACEITO — sem ressalva.** Decisão do consultor (Navaar) em 28/09/2026: a evidência disponível — logs de runtime do Skip Cloud, inspeção de código confirmando não exposição de contatos e testes humanos de 25/09 — foi considerada suficiente para o aceite da SPEC-3-001. A task `4217198c-8077-4769-b2c0-7b7482136553` está encerrada e a SPEC-3-001 está liberada. O export sanitizado não existe no produto e foi tratado como fora do produto; se vier a ser requisito, deve virar task própria em ciclo futuro. Produção não publicada.

## Pendências herdadas (não bloqueiam este aceite)

1. LGPD — base legal do agendamento.
2. RN-2.06 — semântica de reagendamento.
3. Capacidade 2 no sábado — interpretação da janela 11:30–16:30.
4. B3-04 e B3-05 — bloqueiam a SPEC-3-002 (dashboard e baseline).

## Limites

- Tudo em preview; produção não publicada; nenhuma integração externa; nenhum dado real de lead; consolidação somente leitura.