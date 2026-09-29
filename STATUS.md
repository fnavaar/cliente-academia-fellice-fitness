# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 ACEITA (sem ressalva, ratificada) e liberada em 28/09/2026. SPEC-3-002 implementada no preview v0.0.82; teste humano da prévia autenticada com fixtures sintéticas aprovado em 29/09/2026. B3-04 concluída documentalmente; B3-05 continua pendente. Task 124f370f permanece aberta; não há baseline operacional nem GREEN. Produção não publicada.
- **Progresso da Fase 3:** 6/9 tasks de topo concluídas (66,7%): B3-01, B3-02, B3-03, B3-04, implementação da SPEC-3-001 e a revisão de aceite (task `4217198c-8077-4769-b2c0-7b7482136553`, encerrada com aceite sem ressalva ratificado); 3 tasks permanecem em aberto.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate atual:** SPEC-3-001 ACEITA SEM RESSALVA e liberada em 28/09/2026 (decisão do consultor Navaar; ratificada pelo operador ETHOS, Ricardo Junior, às 16:11, com a conferência humana de 15:08 registrada no changelog). CA-3.01..05 conferidos e conformes; evidência considerada suficiente (logs de runtime do Skip Cloud, inspeção de código com não exposição de contatos e testes humanos de 25/09). Task de revisão `4217198c-8077-4769-b2c0-7b7482136553` encerrada. Para a SPEC-3-002, B3-04 está registrado, mas B3-05 permanece pendente; a matriz B3-04 ainda exige prova de aplicação técnica em CA-3.10. O teste humano da prévia sintética passou, mas não há GREEN nem baseline operacional. Produção não publicada.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída documentalmente em 24/09/2026; `utm_source` separado por fonte; `utm_medium` separado por valor; `utm_campaign` agrupada por campanha; ausentes/não reconhecidos em grupo próprio; decisão registrada por Karol em `03_documentos/decisoes-fase-3.md`.
- **B3-02 — Fórmula e janela da métrica norte:** concluída documentalmente em 24/09/2026; numerador “Agendamentos concluídos no período”; denominador “Encaminhamentos humanos no mesmo período”; janela padrão “Últimos 30 dias corridos”; fórmula documental: agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhuma meta foi inferida e nenhum produto foi alterado.
- **B3-03 — Vínculo entre triagem e agendamento:** concluída documentalmente em 24/09/2026; preservar o vínculo da triagem e manter o `lead_submission_id` de origem quando a continuidade estiver disponível; casos sem vínculo seguem como cobertura incompleta, sem atribuição por inferência; confirmação registrada: Karol — “Karol confirma, libere as tasks”. Nenhum produto foi alterado.
- **B3-04 — Matriz de acesso ao dashboard:** concluída documentalmente em 29/09/2026. Leitura agregada permitida para Champion, Gestão, Supervisora e Subgerente; negada para Marketing/agência e Consultor. Confirmação atribuída a Karol, transmitida por Ricardo Junior no chat às 11:44: “matriz correta e autorizada, não podem ler: marketing e consultor, os demais, autorizado”. O registro não comprova aplicação técnica da matriz em runtime. Nenhuma permissão de aplicação/produção foi alterada neste registro.
- **SPEC-3-001 — Implementação do funil:** concluída no preview v0.0.81 em 25/09/2026; ACEITA SEM RESSALVA em 28/09/2026 por decisão do consultor Navaar (CA-3.01..05 conformes; evidência considerada suficiente), ratificada pelo operador ETHOS (Ricardo Junior) em 28/09/2026; task `4217198c` encerrada e SPEC-3-001 liberada.

## Pendências de decisão

- **B3-05:** critério e interpretação do baseline congelado — Champion; registrar condição de suficiência dos dados, tratamento de cobertura insuficiente/denominador zero, versionamento e confirmação verificável.

## Próxima ação

Solicitar ao Champion (Karol e Márcio) a decisão B3-05 em `03_documentos/decisoes-fase-3.md`, com data e confirmação verificável. Depois, continuar a task 124f370f: validar em runtime a matriz B3-04, tratar o baseline conforme a decisão e concluir somente após as evidências e o teste humano exigidos. Não publicar em produção.
