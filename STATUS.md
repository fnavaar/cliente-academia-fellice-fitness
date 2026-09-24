# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — dashboard de conversão por formulário e campanha.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate atual:** B3-01 e B3-02 foram concluídas documentalmente em 24/09/2026. B3-02 definiu numerador “Agendamentos concluídos no período”, denominador “Encaminhamentos humanos no mesmo período” e janela “Últimos 30 dias corridos”, com confirmação verificável de Karol. Permanecem pendentes B3-03, B3-04 e B3-05; a SPEC-3-001 permanece bloqueada até B3-03, e a SPEC-3-002 permanece bloqueada até B3-04 e B3-05, além do aceite da SPEC-3-001.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída documentalmente em 24/09/2026; `utm_source` separado por fonte; `utm_medium` separado por valor; `utm_campaign` agrupada por campanha; ausentes/não reconhecidos em grupo próprio; decisão registrada por Karol em `03_documentos/decisoes-fase-3.md`.
- **B3-02 — Fórmula e janela da métrica norte:** concluída documentalmente em 24/09/2026; numerador “Agendamentos concluídos no período”; denominador “Encaminhamentos humanos no mesmo período”; janela padrão “Últimos 30 dias corridos”; fórmula documental: agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhuma meta foi inferida e nenhum produto foi alterado.

## Pendências de decisão (bloqueios B3-03..B3-05)

- B3-03: decisão sobre vínculo triagem → agendamento (pendência herdada da F2) — Champion.
- B3-04: matriz de acesso ao dashboard — Champion.
- B3-05: critério de congelamento do baseline e interpretação da métrica norte — Champion.

## Próxima ação

Revisar e confirmar o registro documental da B3-02. Depois do aceite humano da B3-02, a próxima decisão é B3-03; somente após B3-03 revalidar a SPEC-3-001. Nenhuma implementação, publicação de produção, mudança de permissão ou integração externa é autorizada antes do gate aplicável.
