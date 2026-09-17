# AP-2026-09-17-1608 — edição parcial de arquivo grande via MCP GitHub trunca o resto

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-003 / fechamento
- Sinal: Ao atualizar o changelog.md (arquivo grande, ~10KB), a nova entrada foi enviada como conteúdo completo do arquivo, mas sem o histórico anterior — o commit truncou o arquivo (de ~10KB para ~1.8KB), apagando as entradas de 2026-09-16 para trás. A ferramenta de edição do GitHub MCP substitui o arquivo inteiro; não existe edição parcial com âncora como em outros editores.
- Evidência: commit 8d39969 (truncado) seguido do commit 9053d7fa (restauração com verificação de 8/8 seções presentes via download do raw).
- Regra reutilizável: antes de atualizar arquivo grande no GitHub MCP, SEMPRE baixar o conteúdo atual primeiro e reenviar o arquivo inteiro (novo conteúdo + histórico preservado); após o commit, verificar por download do raw que as seções antigas continuam presentes. Prefira patch de bloco SEARCH/REPLACE quando a plataforma oferecer.
- Quando aplicar: qualquer atualização de STATUS.md, changelog.md, fase.md ou outro documento cumulativo no repositório do cliente.
- Quando não aplicar: arquivos pequenos criados do zero, onde não há histórico a preservar.
- Confiança: alta — truncamento observado no commit e restauração verificada por download.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
