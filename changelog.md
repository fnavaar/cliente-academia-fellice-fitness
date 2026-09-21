## 2026-09-21 — Debug r2 F2-IMP-008 (exibição do responsável anterior)

- [consultor] Reteste do passo 4 (21/09/2026): a reatribuição funcionou (dono → `lljzgyj2w6rimak`, `responsavel_anterior` preservado no banco, eventos ASSUMED + REASSIGNED na trilha), mas o card da `/visao` não exibia o responsável anterior.
- [causa raiz] A UI tinha o campo no tipo (`responsavel_anterior?`) e o dado gravado no servidor, porém nenhum elemento renderizava — o histórico da reatribuição era preservado, mas invisível na operação (F1-T005 exige histórico preservado).
- [correção] v0.0.75 (`6b9f0f1`): o card passa a exibir "Reatribuída — responsável anterior: …" quando `responsavel_anterior` existir. Pipeline QA completo OK.
- [limite] Reteste do passo 4 volta ao pendente; nenhuma publicação em produção.

## 2026-09-21 — Debug r1 F2-IMP-008 (reatribuição após assunção)