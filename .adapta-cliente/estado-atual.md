# Estado atual — Adapta Cliente

- task_id: ab9ce40f-304e-4ef6-929f-1efa7f7a0a87
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-3-001-consolidacao-eventos-e-funil.md
- etapa: bloqueada
- autorizacao_implementacao: confirmada — 2026-09-24 17:00, Ricardo Junior: "Autorizo implementar a consolidação da SPEC-3-001 conforme o plano analisado."
- teste_humano: falhou — 2026-09-25 08:20, Ricardo Junior relatou HTTP 400 no login dos usuários; teste autenticado do funil continua pendente. Em 2026-09-25 15:26, Ricardo confirmou três contas permanentes no backend compartilhado, mapeamento Champion→champion, Gestão→gestao, Supervisão→supervisora e criação via painel administrativo.
- verificacao_automatica: passou para a correção de diagnóstico — v0.0.81 (96ce32e), setup, análise estática, build, integrações e testes passaram; preview atualizado; usuário fictício com senha inválida confirmou a mensagem específica de falha de autenticação. A verificação não comprova autenticação de usuário real nem acesso ao endpoint agregado.
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-25-0834-autenticacao-antes-do-papel.md
- ultima_acao: confirmação do usuário registrada: três contas permanentes no backend compartilhado, papéis confirmados e provisionamento pelo painel Skip Cloud; painel do builder redirecionou para login nesta sessão; nenhuma conta, permissão ou credencial foi criada/alterada
- proxima_acao: administrador autenticado no painel Skip Cloud deve criar as três contas no projeto/backend compartilhado e fornecer as credenciais fora do chat; depois Ricardo retoma o teste autenticado de SPEC-3-001
- atualizado_em: 2026-09-25T15:26:00-03:00
