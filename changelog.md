## 2026-09-21 — Debug r1 F2-IMP-008 (reatribuição após assunção)

- [consultor] Teste humano do Ricardo (21/09/2026): passos 1–3 e 5–7 OK; passo 4 (Reatribuir) falhou com "Caso já assumido — a reatribuição deve usar a ação formal da Gestão." — evidência em screenshot.
- [causa raiz] A rota atômica grava a flag formal `queue_operation` (campo oculto) e o hook `protect_assumption` não a enxergava durante o save no JSVM — a reatribuição formal era bloqueada como troca direta de dono. A prova de 18/09 não expôs o defeito porque a fixture 0045 estava sem dono (caminho que não passa pelo guarda); o caso já assumido é o único que o aciona.
- [correção] v0.0.74 (`feae808`): o hook passa a reconhecer também a impressão digital da rota formal (`responsavel_anterior` = dono anterior, campo visível e blindado contra PATCH). Pipeline QA completo OK.
- [verificação] Provas ao vivo: caso assumido pela Gestão → Supervisora reatribuiu (HTTP 200), dono passou a `lljzgyj2w6rimak`, `responsavel_anterior` preservou o dono anterior, status manteve `ENCAMINHAMENTO_HUMANO`, eventos ASSUMED + REASSIGNED na trilha; PATCH direto de dono segue bloqueado (403).
- [limite] Teste humano volta ao pendente para reteste do passo 4; nenhuma publicação em produção.

## 2026-09-18 — Fechamento F2-IMP-007 (permissões, fila e assunção de tentativas)