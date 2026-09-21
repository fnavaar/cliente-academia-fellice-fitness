# Debug r1 — F2-IMP-008 — Reatribuição bloqueada em caso já assumido

**Data:** 2026-09-21 · **Versão:** v0.0.73 → v0.0.74 (`feae808`) · **Gate:** aguardando reteste humano (passo 4)

## Task e problema
No teste humano da F2-IMP-008, o passo 4 (Reatribuir) falhou: a ação formal da Gestão/Supervisora sobre "Lead Teste B" (appt-teste-0004, assumido por `h2ki0bsobuz7780`) retornou o banner "Caso já assumido — a reatribuição deve usar a ação formal da Gestão." Os demais 6 passos passaram.

## Reprodução
Com `curl`, fluxo fiel ao da UI: fixture pública nova → ASSUME (Consultor, 200) → REASSIGN (Gestão, **400** com a mesma mensagem do banner). Reproduzido sem UI.

## Causa raiz
A rota atômica `/backend/v1/queue/action` grava `queue_operation = 'REASSIGN'` (campo oculto) antes de salvar e o hook `protect_assumption` decide a liberação lendo essa flag no registro em edição. No JSVM, durante o save vindo da rota, o hook não enxerga a flag (campo oculto não fica visível ao hook de modelo nesse caminho) e trata a reatribuição formal como troca direta de dono — e bloqueia. A prova de 18/09 não expôs o defeito porque a fixture 0045 estava **sem dono** (caminho que não passa pelo guarda); "caso já assumido" é o único caminho que o aciona.

## Correção
`protect_assumption.js` (v0.0.74): além da flag, o hook reconhece a impressão digital da rota formal — `responsavel_anterior === dono anterior` (campo visível, e blindado contra PATCH pela `protect_queue_update`). Correção mínima, sem mudança de SPEC, rotas ou contrato.

## Verificação automática
Pipeline Skip completo OK (setup, análise estática, build, integrações, testes). Provas ao vivo: caso assumido pela Gestão → Supervisora reatribuiu (HTTP 200), dono passou a `lljzgyj2w6rimak`, `responsavel_anterior` preservou o dono anterior, status manteve `ENCAMINHAMENTO_HUMANO`, eventos ASSUMED + REASSIGNED na trilha; PATCH direto de dono segue bloqueado (403).

## Gate atual
aguardando teste humano — reteste do passo 4 (Reatribuir) no preview v0.0.74.
