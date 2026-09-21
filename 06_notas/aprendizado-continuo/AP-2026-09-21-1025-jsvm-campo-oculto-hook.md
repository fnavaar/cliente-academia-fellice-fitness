# AP-2026-09-21-1025 — Campo oculto como flag de operação é invisível ao hook de modelo no JSVM

**Origem:** debug r1 F2-IMP-008 (reatribuição bloqueada em caso já assumido) · **Evidência:** reprodução via curl (ASSUME 200 → REASSIGN 400 "Caso já assumido…") + correção provada em v0.0.74.

## Padrão (causa, não sintoma)
No PocketBase JSVM (Skip Cloud), um campo **oculto** gravado no registro dentro da rota atômica (`queue_operation = 'REASSIGN'`) **não fica visível** a um hook `onRecordUpdate` de modelo durante aquele mesmo save — o hook lê `''` e trata a operação formal como escrita comum, bloqueando-a. A falha só aparece no caminho "caso já assumido" (o único que consulta a flag); provas em fixture sem dono mascaram o defeito.

## Orientação reutilizável
1. Não usar campo oculto como única flag de operação para gate em hook de modelo. Usar também uma "impressão digital" visível e blindada (aqui: `responsavel_anterior === dono anterior`, protegido contra PATCH por hook de request).
2. Ao provar operações com guarda condicional, cobrir **todos os caminhos que acionam o guarda** — não apenas o caminho feliz. Prova em estado que não passa pelo guarda não prova o guarda.
3. Reproduzir sempre por API (curl) antes de suspeitar da UI: o banner do front era só o eco do 400 do hook.
