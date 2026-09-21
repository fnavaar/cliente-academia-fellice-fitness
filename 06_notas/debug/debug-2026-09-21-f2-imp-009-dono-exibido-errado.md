# Debug Summary — F2-IMP-009 r1 (2026-09-21)

## Task e problema

**Task:** F2-IMP-009 — Consolidação do TDD e aceite da SPEC-2-002 (visão operacional).
**Sintoma relatado no teste humano (Ricardo, 21/09/2026):** cenário 2 — após sair do Consultor A e entrar com o Consultor B, o card "Lead Consolidação Encaminhamento" (assumido pelo Consultor A) exibia "Assumida por **você**", e o "responsável anterior" do próprio B aparecia como ID cru. Cenário 5 parcial — o botão "Assumir caso" não aparecia para o consultor tentar assumir durante o rollback.

## Reprodução

Reproduzido pelo operador no Chromium (preview v0.0.78): login Consultor A → "Sair" → login Consultor B **na mesma montagem da página** (sem recarregar) → card assumido pelo A exibia "Assumida por você" e o dono do caso do B aparecia cru. Screenshot do estado corrigido: `artifacts/prova-009r1-consultor-b-ve-dono-correto.png` (workspace ETHOS).

## Causa raiz

`myUserId` era **estado React capturado no mount** (e atualizado só na ação de assumir). O login/logout acontece na mesma montagem — o componente não remonta — e a comparação `dono === myUserId` usada para exibir "por você" ficava obsoleta: o B herdava o ID do A em `myUserId`, invertendo a exibição. Mesma família do debug da F2-IMP-007 r1 (authStore lido fora do momento do render/ação), agora no eixo render em vez de ação.

## Correção

v0.0.78 (`0bffd92`): `myUserId` deixa de ser `useState` e passa a ser **derivado do authStore no render** (`pb.authStore.isValid ? pb.authStore.record?.id : ''`) — a identidade exibida nunca fica obsoleta entre trocas de usuário na mesma montagem. Migração 0048 criou fixtures de reteste: caso já assumido pelo Consultor A (reverifica a exibição do B) e dois casos sem dono ("Lead Reteste Fila r1" para o cenário 2 e "Lead Reteste Rollback r1" para o cenário 5). Pipeline QA completo OK.

## Verificação automática

- Prova no navegador reproduzindo a falha exata (A → Sair → B sem reload): card do A exibe "Assumida por z5wgyiffrdnv028" (ID correto, não "você"); card reatribuído ao B exibe "Assumida por você" + "responsável anterior: z5wgyiffrdnv028" — ambos corretos.
- Bloqueio do cenário 5 confirmado como comportamento por design: com a fila em rollback a UI esconde o botão e o servidor recusa a ação (HTTP 400 "ações da fila estão temporariamente desativadas", provado via API na consolidação). O roteiro foi ajustado para o consultor apenas **verificar** a ausência do botão durante o rollback.
- Nota sobre o cenário 2 original: a fixture "Lead Consolidação Encaminhamento" já tinha sido assumida pelo Consultor A no próprio teste (comportamento correto da fila única), razão pela qual o card não oferecia "Assumir caso" para o A repetir — a nova fixture "Lead Reteste Fila r1" cobre o fluxo limpo.

## Rodada r2 (mesmo dia) — sintoma persistiu no reteste; causa: cache do navegador

- **Relato:** passos 1, 3, 4 e 5 ok; passo 2 ainda exibia "Assumida por você" após trocar para o Consultor B (screenshot anexado ao relato).
- **Investigação:** servidor íntegro — trilha de eventos mostra `APPOINTMENT_ASSUMED` único com actor `z5wgyiffrdnv028` (Consultor A, 14:07:40) e dono correto no registro; o bundle servido no preview (`index-B7eLHk-R.js`, v0.0.78) contém a correção e não contém o marcador antigo (`setMyUserId`); prova em navegador novo (sem cache) exibiu o comportamento correto.
- **Causa raiz r2:** cache do navegador — a aba do teste continuou executando o bundle da v0.0.77. Mesmo padrão do reteste da F2-IMP-008 r2, resolvido com Ctrl+F5. Nenhuma mudança de produto nesta rodada.
- **Procedimento de reteste:** Ctrl+F5 (hard refresh) na `/visao` após entrar com o Consultor B — ou abrir o preview em janela anônima/aba nova; se persistir, capturar screenshot com o console aberto.

## Gate atual

aguardando teste humano — reteste do passo 2 com hard refresh (cenário 5 já reprovado/aprovado no r2: passos 3, 4 e 5 ok).
