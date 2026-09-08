# Debug Summary — 2026-09-08 — fila-sem-exibicao

- **Task:** F1-T008 — fila de encaminhamento humano, SPEC-1-002
- **Sintoma:** o formulário era preenchido, mas o lead não aparecia na fila na visão do atendente.
- **Reprodução:** logs mostraram `POST /lead_handoffs/records` com HTTP 200; a fila não tinha autenticação de atendente e não conseguia ler dados protegidos. A prova do evento `HANDOFF_CREATED` retornava HTTP 400.
- **Causas:** (1) a visão `/fila` não oferecia login para Champion/Consultor; (2) a regra de criação de `lead_handoff_events` exigia autenticação, embora `HANDOFF_CREATED` nasça no formulário público.
- **Correções:** adicionada tela de login autorizada na `/fila`; leitura e ações permanecem protegidas por papel; criada migração 0006 permitindo somente criação pública de eventos; `HANDOFF_CREATED` passou a ser gravado após o handoff.
- **Verificação:** QA Skip v0.0.12 passou em setup, análise estática, build, integrações e testes. Prova sintética final: submissão HTTP 200, evento de submissão HTTP 200, handoff HTTP 200 e evento HANDOFF_CREATED HTTP 200. `/fila` carregou com login protegido.
- **Produção:** não publicada.
