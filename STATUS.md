# Status do plano

## Estado atual

- **Fase atual:** Fase 4 — integração direta (Kommo/Lóvavel) e loop de saúde da conversão. Promovida em 01/10/2026 após aprovação das SPECs pelo consultor ("libero todas as specs, pode executar") e autorização do push ("Confirmo o push: promova a Fase 4 no repositório da Fellice"). Unidade ativa: SPEC-4-001..003 + Jornada com 8 tasks + 1 subtarefa.
- **Progresso da Fase 4:** 0/8 tasks concluídas. Primeira elegível: "Definir contrato, acesso e fallback da integração" (`7953f975`), com as decisões B4-01/02/05 embutidas.
- **Gate anterior:** Fase 3 encerrada em 2026-09-30 — 9/9 tasks; SPEC-3-001 e SPEC-3-002 ACEITAS SEM RESSALVA pelo consultor Navaar (28/09 e 30/09); `check-fase-3.md` APROVADO COM RESSALVAS com active-sha256=7bbfdac4e985eac699880e3539ab59e529db3636fc77c8eec4af10377652ede3 (repo HEAD `b1c045a`); Fase 3 arquivada em `05_entregas/fase-3/`.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks; SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09); `check-fase-2.md` APROVADO COM RESSALVAS em 21/09.
- **Gate atual:** transição F3→F4 publicada neste repositório. Nenhuma credencial, conector, escrita externa ou publicação de produção autorizada. Bloqueios B4-01..B4-05 são insumos do Champion (Karol e Márcio) embutidos nas tasks, com registro em `03_documentos/decisoes-fase-4.md`. Produção não publicada.

## Decisões concluídas

- **B3-01..B3-05 (Fase 3):** taxonomia, métrica norte, vínculo triagem→agendamento, matriz de acesso e critério de baseline decididos pelo Champion (24–29/09/2026).
- **SPEC-3-001 e SPEC-3-002:** aceitas sem ressalva em 28/09 e 30/09/2026.
- **SPECs da Fase 4 (SPEC-4-001..003):** aprovadas pelo consultor em 30/09/2026.

## Ressalvas do fechamento da Fase 3 (dono/prazo em `.adapta/checks/check-fase-3.md`)

- Baseline operacional não congelado (Champion → B4-04 antes da ativação do loop); LGPD/autorização de escrita externa (Champion → B4-01); RN-2.06 e capacidade do sábado (Champion, F5 ou ciclo futuro); export sanitizado (task própria se virar requisito).

## Próxima ação

Executar a task `7953f975` ("Definir contrato, acesso e fallback da integração") uma por vez, com as decisões B4-01/02/05 respondidas pelo Champion dentro da própria task; teste humano entre tasks; nenhuma escrita externa antes de B4-01/02/05 liberados. Revisão do consultor (`c5ccd038`) ao fim da fase.
