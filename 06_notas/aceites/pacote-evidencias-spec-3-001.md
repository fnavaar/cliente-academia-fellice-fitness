# Pacote de evidências — SPEC-3-001 (revisão de aceite)

**Data:** 2026-09-28 · **Ambiente:** preview https://fellice-fitness-8733f--preview.goskip.app · **Versão:** v0.0.81 (`96ce32e`) · **Dados:** 100% sintéticos (fixtures da migração 0051)  
**Task de revisão:** `4217198c-8077-4769-b2c0-7b7482136553` · **Resultado:** ACEITE COM RESSALVA — ver "Ressalvas formais".

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

## Evidências exigidas pela SPEC — situação na data

| Evidência | Situação | Detalhe |
|---|---|---|
| Capturas do ambiente de teste | **AUSENTE** (ressalva 1) | Nenhum artefato de captura em `06_notas/`; a conferência usou logs de runtime, inspeção de código e teste humano registrado |
| Conferência de contagens contra fixtures | PRESENTE | Teste humano 25/09 16:39 + log HTTP 200 de 19:38:30 UTC |
| Export sanitizado | **AUSENTE** (ressalva 2) | Não existe rota nem botão de export no produto (código inspecionado em 25/09); a não exposição de contatos foi verificada no código e no aviso da tela |
| Logs de rollback | **PARCIAL** (ressalva 3) | `POST /funnel/control` HTTP 200 em log de runtime do Skip Cloud; sem registro documental próprio no repositório |
| Aceite humano | REGISTRADO | Autorização de Ricardo Junior em 28/09/2026 09:41: "Registrar aceite com ressalva das evidências ausentes"; conferência humana do aceite pendente |

## Ressalvas formais do aceite

1. **Capturas do ambiente de teste** não foram produzidas/juntadas; a conferência apoiou-se em provas técnicas equivalentes (logs de runtime e código).
2. **Export sanitizado não existe no produto.** A SPEC o lista entre as evidências exigidas; como a implementação não o entregou, a ausência é registrada como ressalva e não como conformidade. Se o Champion entender o export como requisito de produto, criar task própria em novo ciclo.
3. **Logs de rollback** permanecem apenas como runtime do Skip Cloud, sem documento próprio no repositório.
4. O aceite vale para o ambiente de preview com dados sintéticos; produção não publicada.

## Pendências herdadas (não bloqueiam este aceite)

1. LGPD — base legal do agendamento.
2. RN-2.06 — semântica de reagendamento.
3. Capacidade 2 no sábado — interpretação da janela 11:30–16:30.
4. B3-04 e B3-05 — bloqueiam a SPEC-3-002 (dashboard e baseline).

## Limites

- Tudo em preview; produção não publicada; nenhuma integração externa; nenhum dado real de lead; consolidação somente leitura.
