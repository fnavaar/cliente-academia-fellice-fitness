# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 ACEITA (sem ressalva, ratificada) e liberada em 28/09/2026. SPEC-3-002 implementada e task `124f370f` concluída no preview; preview v0.0.85 (`c41cf7c`) no Skip project 51806; QA completo passou em 30/09 e migration 0054 foi aplicada.
- **Progresso da Fase 3:** 8/9 tasks de topo concluídas (88,9%): B3-01..B3-05, implementação da SPEC-3-001, implementação/teste humano da SPEC-3-002 e revisão do aceite da SPEC-3-001. Permanece aberta a revisão formal de aceite da SPEC-3-002.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate anterior:** SPEC-3-001 ACEITA SEM RESSALVA e liberada em 28/09/2026, por decisão do consultor Navaar, ratificada por Ricardo Junior às 16:11. CA-3.01..05 conferidos; evidência em `06_notas/aceites/pacote-evidencias-spec-3-001.md`; task `4217198c-8077-4769-b2c0-7b7482136553` encerrada.
- **Gate atual:** task `124f370f` concluída por Ricardo Junior em 30/09/2026 no preview v0.0.85 (`c41cf7c`), após aprovação humana (“Testei os critérios no preview e funcionou”). Logs Skip Cloud confirmam login HTTP 200 e `POST /backend/v1/dashboard` HTTP 200 às 20:05:58Z. QA completo passou em setup, análise estática, build, integrações e testes; `node --check` e checks focados de RBAC/baseline passaram. A correção usa a allowlist B3-04 aprovada como autoridade; papéis fora da matriz seguem negados e só Champion congela. Migration 0054 está aplicada. Nenhuma versão operacional de baseline foi congelada. Revisão formal independente do aceite da SPEC-3-002 permanece pendente na task `e88283fc` (Felipe Navaar). Produção não publicada.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída em 24/09/2026; fontes `utm_source` separadas, `utm_medium` separado por valor, `utm_campaign` agrupada; ausentes/não reconhecidos em grupos próprios.
- **B3-02 — Métrica norte:** concluída em 24/09/2026; agendamentos concluídos ÷ encaminhamentos humanos no mesmo período, janela padrão móvel dos últimos 30 dias corridos; nenhuma meta inferida.
- **B3-03 — Vínculo triagem→agendamento:** preservar o `lead_submission_id` de origem quando continuidade estiver disponível; sem vínculo fica cobertura incompleta, sem inferência.
- **B3-04 — Matriz de acesso:** Champion, Gestão, Supervisora e Subgerente podem ler agregados; Marketing/agência e Consultor sem acesso. Decisão documental confirmada em 29/09; aplicação no preview v0.0.85 e teste autenticado da task `124f370f` aprovados; revisão formal de aceite ainda pendente.
- **B3-05 — Baseline:** Karol confirmou em 29/09/2026: mês civil completo mais recente no fuso local (`America/Bahia`), sem alterar a janela móvel de 30 dias de B3-02. Cobertura de suficiência baseada em nome, telefone reconhecível e proximidade permitida, limiar 50%; abaixo disso permite salvar como `INSUFICIENTE`; denominador zero permite salvar como `NAO_CALCULAVEL` com taxa nula. Critérios de completude não filtram a fórmula. Apurações novas são append-only. Confirmação transmitida no chat: “Karol - 29/09/2026 - decisões confirmadas e autorizadas”.
- **SPEC-3-001:** implementação do funil aceita sem ressalva e revisão encerrada em 28/09/2026; produção não publicada.

## Próxima ação

Felipe Navaar executar a revisão formal de aceite da SPEC-3-002 na task `e88283fc`: conferir CA-3.06..10, aprovação humana autenticada e QA do preview v0.0.85; registrar aceite ou correções. Não publicar em produção.
