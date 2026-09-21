# Debug r1/r2 — F2-IMP-008 — Reatribuição: bloqueio e exibição do responsável anterior

**Data:** 2026-09-21 · **Versões:** v0.0.73 → v0.0.74 (`feae808`) → v0.0.75 (`6b9f0f1`) · **Gate:** aguardando reteste final (passo 4)

## Task e problema
No teste humano da F2-IMP-008, o passo 4 (Reatribuir) falhou em duas rodadas:
- **r1:** banner "Caso já assumido — a reatribuição deve usar a ação formal da Gestão." — a ação formal nem chegou a gravar.
- **r2:** a reatribuição gravou tudo (dono, `responsavel_anterior`, eventos ASSUMED + REASSIGNED), mas o card da `/visao` não exibia o responsável anterior.

## Reprodução
- **r1:** via `curl`, fluxo fiel à UI: fixture pública → ASSUME (Consultor, 200) → REASSIGN (Gestão, **400** com a mensagem do banner).
- **r2:** estado do registro `appt-debug-008r5` provado via API: `dono = lljzgyj2w6rimak`, `responsavel_anterior = gkvsbcin21wpgyv` — dado existia, UI não mostrava.

## Causa raiz
- **r1:** a rota atômica grava `queue_operation = 'REASSIGN'` (campo **oculto**) e o hook `protect_assumption` decide a liberação lendo essa flag; no JSVM, o hook não enxerga o campo oculto durante esse save e trata a reatribuição formal como troca direta de dono. A prova de 18/09 usou fixture **sem dono** (caminho que não passa pelo guarda) — o caso já assumido é o único que o aciona.
- **r2:** o tipo do frontend tinha `responsavel_anterior?` e o servidor gravava o campo, mas nenhum elemento do card o renderizava — histórico preservado, porém invisível (F1-T005 exige histórico preservado).

## Correção
- **r1 (v0.0.74):** o hook reconhece também a impressão digital da rota formal — `responsavel_anterior === dono anterior` (campo visível, blindado contra PATCH pela `protect_queue_update`).
- **r2 (v0.0.75):** o card da `/visao` exibe "Reatribuída — responsável anterior: …" quando `responsavel_anterior` existir.

## Verificação automática
Pipeline Skip completo OK nas duas versões. Provas ao vivo r1: caso assumido pela Gestão → Supervisora reatribuiu (HTTP 200), dono → `lljzgyj2w6rimak`, status manteve `ENCAMINHAMENTO_HUMANO`, eventos na trilha; PATCH direto de dono segue bloqueado (403). Provas r2: `responsavel_anterior` confirmado no banco e renderização adicionada; `/visao` HTTP 200.

## Gate atual
aguardando teste humano — reteste final do passo 4: recarregar a `/visao` (Ctrl+F5, v0.0.75) e confirmar a linha "Reatribuída — responsável anterior" no card "Lead Reteste Passo 4".
