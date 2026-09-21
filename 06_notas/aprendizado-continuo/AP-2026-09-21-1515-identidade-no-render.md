# AP-2026-09-21-1515 — Identidade do usuário é leitura do render, não estado capturado

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-009 r1 / SPEC-2-002 (debug-2026-09-21-f2-imp-009-dono-exibido-errado.md)
- Sinal: na `/visao`, o `myUserId` capturado em `useState` no mount (e atualizado só na ação de assumir) ficou obsoleto quando o usuário trocou de conta na mesma montagem da página (logout → login sem recarregar): a comparação `dono === myUserId` exibia "Assumida por você" para o dono errado e o ID cru para o correto.
- Evidência: teste humano de 21/09/2026 (cenário 2) + prova no navegador reproduzindo A → Sair → B sem reload; correção v0.0.78 (`0bffd92`) lendo o authStore no render.
- Regra reutilizável: em página que permite login/logout sem remount, qualquer dado derivado da sessão (id, papel, permissões) deve ser lido do authStore no momento do render/ação — nunca guardado em estado capturado no mount. Padrão da mesma família do AP-2026-09-18-0940 (authStore lido fora do momento da ação): o eixo geral é "identidade/sessão se lê no momento de uso, não antes".
- Quando aplicar: qualquer página com troca de usuário na mesma montagem (login inline, logout sem redirect, sessão validada no bootstrap).
- Quando não aplicar: componentes que remontam a cada troca de rota (o mount revalida o estado) ou dados de servidor não derivados da sessão.
- Confiança: alta — causa demonstrada por reprodução e correção verificada no cenário exato da falha.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
