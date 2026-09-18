# AP-2026-09-18-0940 — migração no JSVM usa o parâmetro `app`; `$app` é só de hook

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-007 / SPEC-2-002 (fechamento/limpeza pós-aceite)
- Sinal: migração de limpeza escrita com `$app.findRecordsByFilter(...)`/`$app.delete(...)` foi aplicada como no-op silencioso — QA ok, status "applied", mas NENHUM registro foi removido. Em migração, o acesso ao app vem do PARÂMETRO da callback (`migrate((app) => ...)`); `$app` é global apenas em hooks. Os `try/catch` de tolerância a "registro já removido" engoliram o ReferenceError de `$app is not defined` e esconderam a falha.
- Evidência: v0.0.70 aplicada e verificação ao vivo mostrou os 2 usuários sintéticos ainda autenticando (200), as 2 tentativas de teste ainda na lista do consultor e os 5 eventos de teste intactos; logs não mostraram erro (o catch engoliu). Correção na 0041 (v0.0.71) usando `app.` + `console.log` do que removeu — verificação pós-apply: logins recusados (400) e páginas 200.
- Regra reutilizável: em migração PocketBase/Skip, usar SEMPRE o parâmetro `app` da callback — nunca `$app` (global exclusiva de hooks). Em migrações de limpeza, não silenciar erro e não-encontrado da mesma forma: logar cada remoção (e cada falha) e provar o efeito por verificação externa após o apply (login recusado, lista sem o registro). "Migração applied + QA ok" não prova efeito.
- Quando aplicar: qualquer migração de dados no JSVM (criar, editar, remover registros), especialmente limpezas pós-aceite.
- Quando não aplicar: hooks (lá `$app` é o caminho correto); migrações de schema que usam `new Field(...)`/`app.save(collection)` já seguem o parâmetro.
- Confiança: alta — falha reproduzida (0040 no-op) e correção provada ao vivo (0041).
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
