# Debug summary — SPEC-3-002 / migration 0054

- **Task:** `124f370f-ea01-46d4-bdac-72c1cded2181`
- **Data:** 2026-09-30
- **Sintoma reproduzido:** o working tree continha a migration 0054 com separadores literais `=======` entre os blocos de migração, tornando o arquivo inválido. A migration não estava aplicada; backend ainda estava em 0052–0053.
- **Causa raiz:** a migration 0054 no working tree misturava blocos `up/down` e marcadores de edição como conteúdo executável, não como delimitadores de patch. Na revisão, também foi detectado que ações de baseline propostas não pertenciam ao enum `action` existente (que aceita somente `FROZEN`); essa incompatibilidade foi corrigida antes de aplicação.
- **Correção:** substituída 0054 por migration aditiva limpa; mantido o evento existente `FROZEN`, armazenados estados detalhados nos campos/payload do baseline; hook e tela alinhados com B3-04/B3-05.
- **Verificação:** Skip project 51806, build de desenvolvimento v0.0.83 (`908e4d6`), pipeline setup/static analysis/build/integrations/test — todos passaram; migration `0054_apply_dashboard_decisions` consta como aplicada em 2026-09-30T18:00:50Z. Preview ativo: `https://fellice-fitness-8733f--preview.goskip.app`.
- **Limites/gate:** produção não publicada; task continua aberta em `aguardando_teste_humano`. O teste aprovado em 29/09 vale apenas para v0.0.82, não para esta versão. CA-3.09/3.10 ainda exigem prova humana/autenticada.
- **Working tree residual:** `.skip.config.json` permanece como única alteração pendente após o apply; já estava pendente antes desta correção e não foi editado manualmente nesta task.
