# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 ACEITA (sem ressalva, ratificada) e liberada em 28/09/2026. SPEC-3-002 implementada no preview v0.0.82; teste humano da prévia autenticada com fixtures sintéticas aprovado em 29/09/2026. B3-04 e B3-05 concluídas documentalmente. Task 124f370f permanece ativa: aplicar critérios no preview, provar matriz de runtime (CA-3.10), concluir critérios restantes e obter teste humano/aceite. Ainda não há baseline operacional congelado; produção não publicada.
- **Progresso da Fase 3:** 7/9 tasks de topo concluídas (77,8%): B3-01, B3-02, B3-03, B3-04, B3-05, implementação da SPEC-3-001 e revisão de aceite; 2 tasks permanecem abertas (SPEC-3-002 e revisão de seu aceite).
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate anterior:** SPEC-3-001 ACEITA SEM RESSALVA e liberada em 28/09/2026, por decisão do consultor Navaar, ratificada por Ricardo Junior às 16:11. CA-3.01..05 conferidos; evidência em `06_notas/aceites/pacote-evidencias-spec-3-001.md`; task `4217198c-8077-4769-b2c0-7b7482136553` encerrada.
- **Gate atual:** B3-04 e B3-05 registradas; B3-02 preservada. A SPEC-3-002 está implementada no preview v0.0.82, mas as novas regras de baseline/cobertura e a matriz técnica de acesso precisam de implementação e prova. O teste humano aprovado até agora foi apenas da prévia anterior com fixtures sintéticas; não há baseline operacional congelado, GREEN final nem publicação em produção.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída em 24/09/2026; fontes `utm_source` separadas, `utm_medium` separado por valor, `utm_campaign` agrupada; ausentes/não reconhecidos em grupos próprios.
- **B3-02 — Métrica norte:** concluída em 24/09/2026; agendamentos concluídos ÷ encaminhamentos humanos no mesmo período, janela padrão móvel dos últimos 30 dias corridos; nenhuma meta inferida.
- **B3-03 — Vínculo triagem→agendamento:** preservar o `lead_submission_id` de origem quando continuidade estiver disponível; sem vínculo fica cobertura incompleta, sem inferência.
- **B3-04 — Matriz de acesso:** Champion, Gestão, Supervisora e Subgerente podem ler agregados; Marketing/agência e Consultor sem acesso. Decisão documental confirmada em 29/09; CA-3.10 ainda precisa provar aplicação técnica.
- **B3-05 — Baseline:** Karol confirmou em 29/09 o mês civil completo mais recente no fuso local da unidade (`America/Bahia`), sem mudar a janela móvel de 30 dias de B3-02. Suficiência calculada por submissões com nome não vazio, telefone reconhecível em `canal_de_retorno` e proximidade em Itaigara/bairros vizinhos ou trabalho na região; limiar 50%. Abaixo de 50% permite salvar como `INSUFICIENTE`; denominador zero permite salvar como `NAO_CALCULAVEL`, taxa nula; nenhuma submissão gera cobertura de suficiência não calculável. Critérios não filtram numerador/denominador. Apurações novas criam versões append-only. Confirmação transmitida no chat: “Karol - 29/09/2026 - decisões confirmadas e autorizadas”.
- **SPEC-3-001:** implementação do funil aceita sem ressalva e revisão encerrada em 28/09/2026; produção não publicada.

## Próxima ação

Aplicar B3-04/B3-05 à task ativa `124f370f`: implementar mês civil local completo para congelamento, cobertura de suficiência agregada e estados `INSUFICIENTE`/`NAO_CALCULAVEL`, atualizar a matriz técnica com Subgerente e negar Marketing/Consultor; rodar QA completo no preview e comprovar CA-3.09/3.10. Depois solicitar novo teste humano da versão atualizada. Não publicar em produção.
