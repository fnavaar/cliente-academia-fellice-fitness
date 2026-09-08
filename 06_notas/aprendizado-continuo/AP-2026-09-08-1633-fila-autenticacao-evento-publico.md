# AP-2026-09-08-1633 — Fila protegida exige autenticação e evento público separado

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T008 / SPEC-1-002
- Sinal: o handoff era criado com sucesso, mas a visão do atendente não mostrava o lead porque a coleção era protegida e não havia login; o evento de criação também nascia no formulário público.
- Evidência: `06_notas/debug/debug-2026-09-08-fila-sem-exibicao.md`; QA 0.0.12; prova sintética final com submissão, evento, handoff e HANDOFF_CREATED em HTTP 200; login de usuário consultor validado.
- Regra reutilizável: separar criação pública de eventos de entrada da leitura e das transições operacionais protegidas por autenticação e papel.
- Quando aplicar: filas internas que recebem dados de uma superfície pública e depois exigem ações de atendentes autorizados.
- Quando não aplicar: dados que não contenham contexto de lead ou superfícies sem necessidade de controle de acesso.
- Confiança: alta — causa reproduzida em logs e fluxo corrigido e validado.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
