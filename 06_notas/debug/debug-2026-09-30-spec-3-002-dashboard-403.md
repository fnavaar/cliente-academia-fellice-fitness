# Debug Summary — SPEC-3-002 dashboard 403

- Data: 2026-09-30
- Task: `124f370f-ea01-46d4-bdac-72c1cded2181`
- Sintoma: login autenticado bem-sucedido, mas POST `/backend/v1/dashboard` retornava 403 dizendo que o papel não estava na matriz confirmada.
- Reprodução/evidência: logs Skip Cloud do projeto 51806 registraram login HTTP 200 e rota do dashboard HTTP 403 em 2026-09-30 19:09–19:10 UTC; a rota havia respondido 200 em 2026-09-29 11:48 UTC. O hook possuía duas autorizações sequenciais: allowlist do papel `actor.getString` e uma segunda validação lendo `read_roles` (campo JSON) com `policy.get`/conversão no JSVM.
- Causa raiz: a leitura/conversão do campo JSON `read_roles` no fluxo de autorização não produzia uma lista que satisfizesse a comparação da segunda checagem, apesar de o papel autenticado passar pela allowlist aprovada. A validação duplicada negava o papel autorizado. Evidência sustenta a causa funcional; a representação interna exata do JSON no JSVM não foi registrada pelos logs.
- Correção: `pocketbase/hooks/dashboard_data.js` usa a allowlist canônica local (`champion`, `gestao`, `supervisora`, `subgerente`) como autoridade; remove a reinterpretação duplicada de `read_roles`. Mantida a exigência `b3_04_confirmed`; a role gate inicial continua negando `marketing` e `consultor`; somente `champion` pode congelar.
- Verificação: `node --check` passou no snapshot e checks estáticos focados passaram. Pipeline Skip desenvolvimento v0.0.85 (`c41cf7c`) passou em setup, análise estática, build, integrações e testes. Projeto não publicado em produção.
- Smoke de superfície: `/dashboard` abre a tela de autenticação no preview. POST direto sem token retornou 401, como esperado.
- Gate: aguardando novo teste humano autenticado no preview. Ainda pendentes os critérios CA-3.06..10, especialmente prova dos quatro papéis positivos, negativas para Marketing/Consultor e escrita não-Champion, cálculo/período/suficiência, não exposição de contatos e rollback sem perda.
