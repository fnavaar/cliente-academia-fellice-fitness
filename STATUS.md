# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — dashboard de conversão por formulário e campanha.
- **Progresso da Fase 3:** 3/9 tasks de topo concluídas documentalmente (33,3%): B3-01, B3-02 e B3-03; 6 tasks permanecem pendentes.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate atual:** B3-01, B3-02 e B3-03 foram concluídas documentalmente em 24/09/2026. B3-03 definiu preservar o vínculo da triagem no fluxo de agendamento; casos que ainda ficarem sem `lead_submission_id` permanecem visíveis como cobertura incompleta, sem atribuição por inferência. A SPEC-3-001 está liberada para o próximo ciclo de análise/implementação, mas ainda não foi implementada nem aceita. Permanecem pendentes B3-04 e B3-05; a SPEC-3-002 permanece bloqueada até B3-04 e B3-05, além do aceite da SPEC-3-001.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída documentalmente em 24/09/2026; `utm_source` separado por fonte; `utm_medium` separado por valor; `utm_campaign` agrupada por campanha; ausentes/não reconhecidos em grupo próprio; decisão registrada por Karol em `03_documentos/decisoes-fase-3.md`.
- **B3-02 — Fórmula e janela da métrica norte:** concluída documentalmente em 24/09/2026; numerador “Agendamentos concluídos no período”; denominador “Encaminhamentos humanos no mesmo período”; janela padrão “Últimos 30 dias corridos”; fórmula documental: agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhuma meta foi inferida e nenhum produto foi alterado.
- **B3-03 — Vínculo entre triagem e agendamento:** concluída documentalmente em 24/09/2026; preservar o vínculo da triagem e manter o `lead_submission_id` de origem quando a continuidade estiver disponível; casos sem vínculo seguem como cobertura incompleta, sem atribuição por inferência; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhum produto foi alterado.

## Pendências de decisão (bloqueios B3-04..B3-05)

- B3-04: matriz de acesso ao dashboard — Champion.
- B3-05: critério de congelamento do baseline e interpretação da métrica norte — Champion.

## Próxima ação

Em novo pedido, analisar a task de consolidação dos eventos das fases 1 e 2 na SPEC-3-001. A implementação deve ocorrer somente após análise e autorização explícita; nenhuma publicação de produção, mudança de permissão ou integração externa é autorizada nesta etapa.
