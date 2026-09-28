# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 ACEITA (sem ressalva, ratificada) e liberada em 28/09/2026. Dashboard por formulário e campanha (SPEC-3-002) não iniciado; aguarda B3-04 e B3-05.
- **Progresso da Fase 3:** 5/9 tasks de topo concluídas (55,6%): B3-01, B3-02, B3-03, implementação da SPEC-3-001 e a revisão de aceite (task `4217198c-8077-4769-b2c0-7b7482136553`, encerrada com aceite sem ressalva ratificado); 4 tasks permanecem em aberto.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate atual:** SPEC-3-001 ACEITA SEM RESSALVA e liberada em 28/09/2026 (decisão do consultor Navaar; ratificada pelo operador ETHOS, Ricardo Junior, às 16:11, com a conferência humana de 15:08 registrada no changelog). CA-3.01..05 conferidos e conformes; evidência considerada suficiente (logs de runtime do Skip Cloud, inspeção de código com não exposição de contatos e testes humanos de 25/09). Task de revisão `4217198c-8077-4769-b2c0-7b7482136553` encerrada. Pacote em `06_notas/aceites/pacote-evidencias-spec-3-001.md`. A SPEC-3-002 permanece bloqueada até os registros B3-04 e B3-05. Produção não publicada.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída documentalmente em 24/09/2026; `utm_source` separado por fonte; `utm_medium` separado por valor; `utm_campaign` agrupada por campanha; ausentes/não reconhecidos em grupo próprio; decisão registrada por Karol em `03_documentos/decisoes-fase-3.md`.
- **B3-02 — Fórmula e janela da métrica norte:** concluída documentalmente em 24/09/2026; numerador “Agendamentos concluídos no período”; denominador “Encaminhamentos humanos no mesmo período”; janela padrão “Últimos 30 dias corridos”; fórmula documental: agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhuma meta foi inferida e nenhum produto foi alterado.
- **B3-03 — Vínculo entre triagem e agendamento:** concluída documentalmente em 24/09/2026; preservar o vínculo da triagem e manter o `lead_submission_id` de origem quando a continuidade estiver disponível; casos sem vínculo seguem como cobertura incompleta, sem atribuição por inferência; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhum produto foi alterado.
- **SPEC-3-001 — Implementação do funil:** concluída no preview v0.0.81 em 25/09/2026; ACEITA SEM RESSALVA em 28/09/2026 por decisão do consultor Navaar (CA-3.01..05 conformes; evidência considerada suficiente), ratificada pelo operador ETHOS (Ricardo Junior) em 28/09/2026; task `4217198c` encerrada e SPEC-3-001 liberada.

## Pendências de decisão (bloqueios B3-04..B3-05)

- B3-04: matriz de acesso ao dashboard — Champion.
- B3-05: critério de congelamento do baseline e interpretação da métrica norte — Champion.

## Próxima ação

Solicitar ao Champion (Karol e Márcio) os registros B3-04 (matriz de acesso) e B3-05 (critério de congelamento do baseline) em `03_documentos/decisoes-fase-3.md`, com data e confirmação verificável, para liberar a SPEC-3-002. Não publicar em produção.
