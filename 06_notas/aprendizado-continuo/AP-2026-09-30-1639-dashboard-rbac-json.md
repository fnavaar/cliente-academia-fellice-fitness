# AP-2026-09-30-1639 — autorização de rota não deve duplicar allowlist com JSON runtime

- Status: confirmado após reteste humano em 30/09/2026
- Escopo: projeto do cliente
- Task/SPEC: `124f370f-ea01-46d4-bdac-72c1cded2181` / SPEC-3-002
- Sinal: o papel passou pela allowlist explícita da rota, mas uma segunda checagem derivada do campo JSON `read_roles` negou a mesma sessão autenticada (403). Remover a validação duplicada e reutilizar a matriz explícita resolve a divergência sem ampliar papéis.
- Evidência: logs Skip Cloud de 2026-09-30 às 19:09–19:10 UTC; hook antes/depois em `pocketbase/hooks/dashboard_data.js`; QA v0.0.85 completo. Teste autenticado aprovado por Ricardo Junior em 30/09/2026; logs mostram login HTTP 200 e dashboard HTTP 200. QA completo v0.0.85 passou.
- Regra reutilizável: mantenha uma única fonte de verdade de RBAC em cada handler; se a policy precisar permanecer dinâmica, logue seu tipo/valor de forma segura e prove a conversão com teste mínimo antes de usá-la para negar acesso.
- Quando aplicar: rota PocketBase com matriz aprovada já declarada e segunda checagem baseada em JSON do JSVM gera falso 403.
- Quando não aplicar: requisitos determinam papéis dinâmicos por tenant/policy ou a matriz precisa ser administrável sem deploy; nesse caso validar o formato de runtime e manter policy dinâmica com teste cobrindo representação JSON.
- Confiança: alta quanto à correção funcional — o mesmo fluxo autenticado que antes recebia 403 retornou HTTP 200 após remover a checagem duplicada. O valor interno do JSON no JSVM segue sem instrumentação, mas não é mais autoridade de autorização nesta implementação.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
