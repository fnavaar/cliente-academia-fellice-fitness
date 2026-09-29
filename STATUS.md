# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 ACEITA (sem ressalva, ratificada) e liberada em 28/09/2026. SPEC-3-002 implementada no preview v0.0.82; teste humano da prévia autenticada com fixtures sintéticas aprovado em 29/09/2026. Decisões B3-04 e B3-05 registradas documentalmente. Task 124f370f permanece ativa, mas bloqueada para alterações técnicas nesta sessão porque o builder Skip redirecionou ao login e não havia sessão autenticada. Não há baseline operacional; produção não publicada.
- **Progresso da Fase 3:** 7/9 tasks de topo concluídas (77,8%): B3-01, B3-02, B3-03, B3-04, B3-05, implementação da SPEC-3-001 e revisão de seu aceite; 2 tasks permanecem abertas (SPEC-3-002 e revisão de seu aceite).
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate anterior:** SPEC-3-001 ACEITA SEM RESSALVA e liberada em 28/09/2026, por decisão do consultor Navaar, ratificada por Ricardo Junior às 16:11. CA-3.01..05 conferidos; evidência em `06_notas/aceites/pacote-evidencias-spec-3-001.md`; task `4217198c-8077-4769-b2c0-7b7482136553` encerrada.
- **Gate atual:** B3-04 e B3-05 registradas. B3-02 mantém janela móvel padrão de 30 dias; baseline usa mês civil no fuso local da unidade. A implementação do preview v0.0.82 ainda não aplica o novo período, a cobertura mínima de 50%, estados insuficiente/não calculável, nem a matriz completa de runtime. A prévia sintética anterior teve teste humano aprovado, mas ainda não há GREEN final nem baseline operacional. O builder está bloqueado por login nesta sessão; produção não publicada.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída em 24/09/2026; fontes `utm_source` separadas, `utm_medium` separado por valor, `utm_campaign` agrupada; ausentes/não reconhecidos em grupos próprios.
- **B3-02 — Métrica norte:** concluída em 24/09/2026; agendamentos concluídos ÷ encaminhamentos humanos no mesmo período, janela padrão móvel dos últimos 30 dias corridos; nenhuma meta inferida.
- **B3-03 — Vínculo triagem→agendamento:** preservar o `lead_submission_id` de origem quando continuidade estiver disponível; sem vínculo fica cobertura incompleta, sem inferência.
- **B3-04 — Matriz de acesso:** Champion, Gestão, Supervisora e Subgerente podem ler agregados; Marketing/agência e Consultor sem acesso. Decisão documental confirmada em 29/09; CA-3.10 ainda precisa provar aplicação técnica.
- **B3-05 — Baseline:** Karol confirmou em 29/09/2026: mês civil completo mais recente no fuso local (`America/Bahia`), sem alterar a janela móvel de 30 dias de B3-02. Cobertura de suficiência baseada em nome, telefone reconhecível e proximidade permitida, limiar 50%; abaixo disso permite salvar como `INSUFICIENTE`; denominador zero permite salvar como `NAO_CALCULAVEL` com taxa nula. Critérios de completude não filtram a fórmula. Apurações novas são append-only. Confirmação transmitida no chat: “Karol - 29/09/2026 - decisões confirmadas e autorizadas”.
- **SPEC-3-001:** implementação do funil aceita sem ressalva e revisão encerrada em 28/09/2026; produção não publicada.

## Próxima ação

Restaurar acesso autenticado ao builder Skip ou disponibilizar as ferramentas Skip de edição/QA; depois continuar a task `124f370f` no preview: implementar B3-04/B3-05, atualizar o modelo/estados de baseline, provar CA-3.09/3.10, rodar QA completo e pedir novo teste humano. Não publicar em produção.
