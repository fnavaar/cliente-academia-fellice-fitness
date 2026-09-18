# Debug — 2026-09-18 — F2-IMP-007 reteste (actor_id vazio na assunção)

## Sintoma
No reteste humano da F2-IMP-007 (2026-09-18), os 3 primeiros eventos `APPOINTMENT_ASSUMED`
criados pela página /visao saíram com `actor_id` vazio na trilha, embora o `dono` do
appointment tenha sido gravado corretamente.

## Causa raiz
O `userId` usado no payload do evento vinha de estado React capturado no `useEffect` de
mount (`myUserId`). Como o login acontece NA MESMA página (sem remount), esse estado
estava vazio no momento do clique — o `dono` vinha direto do `authStore` (correto), mas o
`actor_id` do evento vinha do estado (vazio).

## Correção
`assume()` passou a ler `pb.authStore.record?.id` NO MOMENTO do clique e a recusar a
assunção sem sessão válida. As assunções finais do teste (007 e 007b) gravaram
`actor_id` correto (verificado via API: eventos com actor = id do consultor de teste).

## Evidência
- 3 eventos com actor vazio (12:02 UTC) seguidos de 2 eventos com actor correto
  (12:07 e 12:11 UTC) na trilha `lead_appointment_events` — registrados antes da
  limpeza da 0041.
- Correção aprovada no teste humano ("Testei e funcionou", 2026-09-18).

## Nota de limpeza
Os eventos com actor vazio foram removidos junto com as tentativas de teste na
migração 0041 (a 0040 aplicou-se como no-op silencioso — ver aprendizado
AP-2026-09-18-0940-migracao-jsvm-app-parametro.md).
