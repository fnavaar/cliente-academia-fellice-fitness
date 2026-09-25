# Debug — SPEC-3-001: login recusado no funil

- **Data:** 2026-09-25
- **Task:** `ab9ce40f-304e-4ef6-929f-1efa7f7a0a87`
- **Ambiente:** projeto Skip 51806, preview v0.0.81 (`96ce32e`), produção não publicada.

## Sintoma

Na rota `/funil`, usuários tentados pelo responsável não conseguem entrar; a interface original dizia “login inválido ou papel sem acesso aos agregados da consolidação”. Não foram solicitadas, registradas nem usadas credenciais do responsável.

## Evidência e reprodução

- Logs do Skip registraram três `POST /api/collections/users/auth-with-password` com HTTP 400 e `Failed to authenticate`, em 2026-09-25, antes da execução da rota `/backend/v1/funnel` ou da validação de papel.
- Um ensaio separado com endereço e senha fictícios recebeu o mesmo 400 esperado e verificou no preview a nova mensagem de autenticação recusada.
- O endpoint do funil respondeu 401 sem autenticação, conforme esperado.
- Schema live de `users.role`: `champion`, `consultor`, `gestao`, `supervisora`. Endpoint da SPEC-3-001 permite Champion, Gestão e Supervisora.
- Migrações de limpeza 0010, 0013, 0034, 0041 e 0046 removem usuários sintéticos de testes anteriores. As migrações 0050/0051 da SPEC-3-001 não criam usuário de acesso.

## Diagnóstico

Causa confirmada do texto enganoso: a tela combinava erro de autenticação e papel não autorizado numa única mensagem, embora o log indique que a tentativa falhou antes da checagem de papel. A resposta genérica 400 do PocketBase não permite distinguir conta inexistente de senha incorreta. Portanto, a causa específica da falha das contas reais permanece **não determinada**; não atribuir a erro de implementação de roles sem conta autenticada.

## Correção e verificação

- Atualizada `src/pages/Funil.tsx` para separar autenticação recusada de sessão autenticada sem papel autorizado.
- Skip v0.0.81: setup, análise estática, build, integrações e testes passaram.
- Preview confirmou a mensagem específica com uma tentativa sintética inválida; nenhuma conta, senha, permissão, schema de usuários ou publicação foi alterada.

## Bloqueio / próxima ação segura

Teste humano autenticado permanece pendente. Um responsável pelo ambiente deve confirmar/corrigir uma conta **ativa no backend de preview** com papel permitido e testar novamente. Não compartilhar senha no chat. Não criar usuários nem ampliar permissões sem autorização explícita separada.
