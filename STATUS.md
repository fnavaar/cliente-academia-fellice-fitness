# Status do plano

## Estado atual

- **Fase atual:** Fase 4 — integração direta (Kommo/Lóvavel) e loop de saúde da conversão. Promovida em 01/10/2026 após aprovação das SPECs pelo consultor ("libero todas as specs, pode executar") e autorização do push ("Confirmo o push: promova a Fase 4 no repositório da Fellice"). Unidade ativa: SPEC-4-001..003 + Jornada com 8 tasks + 1 subtarefa.
- **Progresso da Fase 4:** 0/8 tasks concluídas. Task ativa: "Definir contrato, acesso e fallback da integração" (`7953f975`), em andamento. `03_documentos/decisoes-fase-4.md` atualizado em 09/10/2026 com insumos parciais recebidos de Ricardo e revisão documental parcial aprovada por ele às 11:59 (America/Bahia); base legal B4-01, detalhes de conta/permissões/prova de B4-02 e mapeamento/aprovações finais B4-05 seguem pendentes.
- **Gate anterior:** Fase 3 encerrada em 2026-09-30 — 9/9 tasks; SPEC-3-001 e SPEC-3-002 ACEITAS SEM RESSALVA pelo consultor Navaar (28/09 e 30/09); `check-fase-3.md` APROVADO COM RESSALVAS com active-sha256=7bbfdac4e985eac699880e3539ab59e529db3636fc77c8eec4af10377652ede3 (repo HEAD `b1c045a`); Fase 3 arquivada em `05_entregas/fase-3/`.
- **Gate anterior:** Fase 2 encerrada em 2026-09-21 — 14/14 tasks; SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09); `check-fase-2.md` APROVADO COM RESSALVAS em 21/09.
- **Gate atual:** transição F3→F4 publicada neste repositório. Nenhuma credencial, conector, escrita externa ou publicação de produção autorizada. A aprovação de Ricardo em 09/10 foi apenas da revisão do registro parcial e não libera B4-01/02/05: falta validar a base legal; confirmar se “lovable” significa Lóvavel ou Lovable e comprovar conta, permissões e prova; concluir mapeamento, identificador externo e aprovações do Comercial/Champion. O rascunho não libera integração. Produção não publicada.

## Decisões concluídas

- **B3-01..B3-05 (Fase 3):** taxonomia, métrica norte, vínculo triagem→agendamento, matriz de acesso e critério de baseline decididos pelo Champion (24–29/09/2026).
- **SPEC-3-001 e SPEC-3-002:** aceitas sem ressalva em 28/09 e 30/09/2026.
- **SPECs da Fase 4 (SPEC-4-001..003):** aprovadas pelo consultor em 30/09/2026.

## Ressalvas do fechamento da Fase 3 (dono/prazo em `.adapta/checks/check-fase-3.md`)

- Baseline operacional não congelado (Champion → B4-04 antes da ativação do loop); LGPD/autorização de escrita externa (Champion → B4-01); RN-2.06 e capacidade do sábado (Champion, F5 ou ciclo futuro); export sanitizado (task própria se virar requisito).

## Próxima ação

Obter e registrar, dentro da task `7953f975`, as validações e comprovações pendentes: base legal e confirmação do escopo B4-01; esclarecimento da segunda ferramenta, ambiente/permissões e prova timeboxed B4-02; destinos de campo, identificador externo e aprovações do Comercial/Champion B4-05. Até lá, não ativar credenciais/conector nem realizar escrita externa. Não iniciar outra task.
