# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 com aceite formal registrado COM RESSALVA em 28/09/2026 (conferência humana pendente para encerrar a task de revisão). Dashboard por formulário e campanha não iniciado.
- **Progresso da Fase 3:** 4/9 tasks de topo concluídas (44,4%): B3-01, B3-02, B3-03 e implementação da SPEC-3-001; a revisão de aceite (task `4217198c-8077-4769-b2c0-7b7482136553`) tem aceite registrado e aguarda conferência humana para conclusão; 5 tasks permanecem em aberto.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate atual:** B3-01, B3-02 e B3-03 concluídas documentalmente em 24/09/2026. Implementação SPEC-3-001 concluída e validada no preview v0.0.81 em 25/09. Revisão formal de aceite executada pela task `4217198c-8077-4769-b2c0-7b7482136553` em 28/09/2026: CA-3.01..05 conferidos e conformes (prova técnica: migrações 0050–0051 aplicadas; logs de runtime com `GET /backend/v1/funnel` e `POST /backend/v1/funnel/control` HTTP 200; consulta anônima 401; inspeção de `src/pages/Funil.tsx` e `pocketbase/hooks/funnel_aggregate.js`; prova humana dos testes de 25/09 registrada no changelog). ACEITE REGISTRADO COM RESSALVA: (1) capturas do ambiente de teste ausentes do repositório; (2) export sanitizado inexistente — não há rota ou botão de export no produto; (3) logs de rollback existem apenas como runtime do Skip Cloud, sem registro documental próprio. Pacote em `06_notas/aceites/pacote-evidencias-spec-3-001.md`. Autorização: Ricardo Junior, 28/09/2026 09:41, “Registrar aceite com ressalva das evidências ausentes”. Conferência humana do aceite pendente para encerrar a task. Permanecem pendentes B3-04 e B3-05; a SPEC-3-002 segue bloqueada até os dois registros e a conclusão do aceite. Produção não publicada.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída documentalmente em 24/09/2026; `utm_source` separado por fonte; `utm_medium` separado por valor; `utm_campaign` agrupada por campanha; ausentes/não reconhecidos em grupo próprio; decisão registrada por Karol em `03_documentos/decisoes-fase-3.md`.
- **B3-02 — Fórmula e janela da métrica norte:** concluída documentalmente em 24/09/2026; numerador “Agendamentos concluídos no período”; denominador “Encaminhamentos humanos no mesmo período”; janela padrão “Últimos 30 dias corridos”; fórmula documental: agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhuma meta foi inferida e nenhum produto foi alterado.
- **B3-03 — Vínculo entre triagem e agendamento:** concluída documentalmente em 24/09/2026; preservar o vínculo da triagem e manter o `lead_submission_id` de origem quando a continuidade estiver disponível; casos sem vínculo seguem como cobertura incompleta, sem atribuição por inferência; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhum produto foi alterado.
- **SPEC-3-001 — Implementação do funil:** concluída no preview v0.0.81 em 25/09/2026; testes automatizados e humanos da task documentados no changelog. ACEITE COM RESSALVA registrado em 28/09/2026 pela task `4217198c-8077-4769-b2c0-7b7482136553` (CA-3.01..05 conformes; evidências ausentes registradas como ressalva em `06_notas/aceites/pacote-evidencias-spec-3-001.md`); conferência humana pendente.

## Pendências de decisão (bloqueios B3-04..B3-05)

- B3-04: matriz de acesso ao dashboard — Champion.
- B3-05: critério de congelamento do baseline e interpretação da métrica norte — Champion.
- Se o Champion entender o export sanitizado como requisito de produto, abrir task própria em novo ciclo (a ausência está registrada como ressalva do aceite da SPEC-3-001).

## Próxima ação

Conferência humana do aceite registrado da SPEC-3-001 para encerrar a task `4217198c-8077-4769-b2c0-7b7482136553` (marcar `04_fase-atual/fase.md` e fechar a SPEC). Não publicar em produção. A SPEC-3-002 só poderá ser analisada depois da conclusão do aceite da SPEC-3-001 e dos registros B3-04 e B3-05.
