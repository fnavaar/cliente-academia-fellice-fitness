# AP-2026-09-25-0834 — autenticação antes do papel

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: `ab9ce40f-304e-4ef6-929f-1efa7f7a0a87` / SPEC-3-001
- Sinal: o PocketBase respondeu HTTP 400 `Failed to authenticate` em `auth-with-password`; o fluxo falhou antes da avaliação do papel. O texto original da interface misturava autenticação inválida com papel sem acesso.
- Evidência: log Skip 2026-09-25 (request `POST /api/collections/users/auth-with-password`, HTTP 400); schema live `users.role`; v0.0.81 distinguiu as mensagens e preview confirmou a mensagem de autenticação com identidade/senha sintéticas.
- Regra reutilizável: diagnosticar em ordem: (1) confirmar a autenticação no backend do mesmo ambiente; (2) só então verificar papel/RLS/endpoint. Mensagem de 400 `Failed to authenticate` não permite concluir se a conta não existe ou se a senha está incorreta; não inferir nem expor credenciais.
- Quando aplicar: testes de login PocketBase entre preview/produção ou quando a UI combinar credencial e autorização numa mensagem.
- Quando não aplicar: quando os logs provarem que a autenticação foi bem-sucedida e a recusa vier do papel, de uma regra RLS ou do endpoint protegido.
- Confiança: alta — sequência e mensagem são observáveis nos logs; motivo específico da falha das contas tentadas segue indeterminado.
- Privacidade: sem e-mail de usuário, senha, dado pessoal ou conteúdo bruto de conversa.
