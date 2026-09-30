# Status do plano

## Estado atual

- **Fase atual:** Fase 3 — SPEC-3-001 ACEITA (sem ressalva, ratificada) e liberada em 28/09/2026. SPEC-3-002 em execução na task `124f370f`; preview v0.0.85 (`c41cf7c`) no Skip project 51806; QA completo passou em 30/09 e migration 0054 foi aplicada.
- **Progresso da Fase 3:** 7/9 tasks de topo concluídas (77,8%): B3-01, B3-02, B3-03, B3-04, B3-05, implementação da SPEC-3-001 e revisão do aceite. Permanecem abertas a implementação/teste humano da SPEC-3-002 e sua revisão formal de aceite.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks concluídas (F2-T001..T005 documentais + F2-IMP-001..009 de implementação); SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; `check-fase-2.md` APROVADO COM RESSALVAS em 21/09 com active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- **Gate anterior:** SPEC-3-001 ACEITA SEM RESSALVA e liberada em 28/09/2026, por decisão do consultor Navaar, ratificada por Ricardo Junior às 16:11. CA-3.01..05 conferidos; evidência em `06_notas/aceites/pacote-evidencias-spec-3-001.md`; task `4217198c-8077-4769-b2c0-7b7482136553` encerrada.
- **Gate atual:** B3-04 e B3-05 estão registradas e aplicadas no runtime de preview. B3-02 mantém janela móvel padrão de 30 dias; o baseline usa mês civil completo anterior em `America/Bahia`, com cobertura de suficiência a 50%, estados explícitos para insuficiência/denominador zero e versões append-only. A correção do 403 removeu a segunda validação da matriz que reabria `read_roles` JSON em runtime, usando a allowlist aprovada da rota e mantendo a confirmação `b3_04_confirmed`; papéis fora da allowlist seguem negados e só Champion congela. QA Skip v0.0.85 (`c41cf7c`) passou em setup, análise estática, build, integrações e testes; migration 0054 consta como aplicada. A task `124f370f` está em `aguardando_teste_humano`: falta validar autenticação e papéis positivos/negativos após a correção, cálculo/período/suficiência, não exposição de contatos, escrita não-Champion e rollback sem perda. Prévia abre a tela de autenticação; chamada sem token retornou 401. Não há baseline operacional congelado. Produção não publicada.
- **Run:** `20260924T142019775Z-0b177fbe` (liberação das tarefas de decisão da Fase 3 e transferência de responsabilidade ao Champion).

## Decisões concluídas

- **B3-01 — Taxonomia de origem e campanha:** concluída em 24/09/2026; fontes `utm_source` separadas, `utm_medium` separado por valor, `utm_campaign` agrupada; ausentes/não reconhecidos em grupos próprios.
- **B3-02 — Métrica norte:** concluída em 24/09/2026; agendamentos concluídos ÷ encaminhamentos humanos no mesmo período, janela padrão móvel dos últimos 30 dias corridos; nenhuma meta inferida.
- **B3-03 — Vínculo triagem→agendamento:** preservar o `lead_submission_id` de origem quando continuidade estiver disponível; sem vínculo fica cobertura incompleta, sem inferência.
- **B3-04 — Matriz de acesso:** Champion, Gestão, Supervisora e Subgerente podem ler agregados; Marketing/agência e Consultor sem acesso. Decisão documental confirmada em 29/09; a aplicação de código consta no preview v0.0.85, mas CA-3.10 ainda exige prova autenticada.
- **B3-05 — Baseline:** Karol confirmou em 29/09/2026: mês civil completo mais recente no fuso local (`America/Bahia`), sem alterar a janela móvel de 30 dias de B3-02. Cobertura de suficiência baseada em nome, telefone reconhecível e proximidade permitida, limiar 50%; abaixo disso permite salvar como `INSUFICIENTE`; denominador zero permite salvar como `NAO_CALCULAVEL` com taxa nula. Critérios de completude não filtram a fórmula. Apurações novas são append-only. Confirmação transmitida no chat: “Karol - 29/09/2026 - decisões confirmadas e autorizadas”.
- **SPEC-3-001:** implementação do funil aceita sem ressalva e revisão encerrada em 28/09/2026; produção não publicada.

## Próxima ação

Ricardo executar teste humano autenticado em `/dashboard` no preview v0.0.85, usando Champion, Gestão/Supervisora/Subgerente e papéis negativos aprovados. Validar leitura pelos quatro papéis, negativa para Marketing/Consultor, baseline com Champion e negativa de escrita para não-Champion; conferir período mensal, suficiência, baixa cobertura, denominador zero, não exposição de contatos e preservação no rollback. Registrar resultado/evidências sem publicar em produção. Se falhar, manter a mesma task aberta e depurar. A revisão de aceite `e88283fc` só começa depois da task `124f370f` passar o gate humano.
