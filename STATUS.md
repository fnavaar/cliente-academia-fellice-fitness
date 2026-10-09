# Status do plano

## Estado atual

- **Fase atual:** Fase 4 — integração direta e loop de saúde da conversão. Promovida em 01/10/2026 após aprovação das SPECs pelo consultor e autorização da promoção da fase. Unidade ativa: SPEC-4-001..003 + Jornada com 8 tasks + 1 subtarefa.
- **Progresso da Fase 4:** 0/8 tasks concluídas. Task ativa: “Definir contrato, acesso e fallback da integração” (`7953f975`), em andamento. `03_documentos/decisoes-fase-4.md` atualizado parcialmente em 09/10/2026 com novas respostas de Ricardo às 15:50; revisão humana desta atualização ainda pendente.
- **Gate anterior:** Fase 3 encerrada em 2026-09-30 — 9/9 tasks; SPEC-3-001 e SPEC-3-002 aceitas sem ressalva pelo consultor; Fase 3 arquivada em `05_entregas/fase-3/`.
- **Gate atual:** B4-01 segue pendente (base legal e escopo de escrita marcados como PENDENTE). B4-02 segue pendente: Ricardo escolheu/indicou Kommo + Lovable e disse que há contas, mas não são de teste; permissões e prova técnica seguem pendentes, e isso não atende à exigência da SPEC de prova em conta de teste. Não acessar as contas existentes nem realizar leitura/escrita. B4-05 segue pendente: destino Lovable versus plataforma Skip não foi decidido, identificador externo não está definido, e a regra de unificar histórico por nome completo + telefone foi relatada como aprovada sem aprovadores/evidência verificável; sem execução de mesclagem.
- **DÚVIDA de requisito:** a SPEC-4-001 descreve Kommo e/ou Lóvavel, enquanto as respostas falam em Lovable e também na plataforma Skip como destino. Confirmar escopo e destino pretendido com consultor/Champion antes de qualquer execução ou alteração da SPEC. Produção não publicada.

## Decisões concluídas

- **B3-01..B3-05 (Fase 3):** taxonomia, métrica norte, vínculo triagem→agendamento, matriz de acesso e critério do baseline foram decididos na Fase 3.
- **SPEC-3-001 e SPEC-3-002:** aceitas sem ressalva em 28/09 e 30/09/2026.
- **SPECs da Fase 4 (SPEC-4-001..003):** aprovadas pelo consultor em 30/09/2026.

## Ressalvas do fechamento da Fase 3

- Baseline operacional não congelado (Champion → B4-04 antes da ativação do loop); LGPD/autorização de escrita externa (Champion → B4-01); RN-2.06 e capacidade do sábado (Champion, F5 ou ciclo futuro); export sanitizado (task própria se virar requisito).

## Próxima ação

Resolver a DÚVIDA de escopo sobre Lovable versus plataforma Skip (e a divergência com Lóvavel na SPEC) com o consultor/Champion, obtendo também identificação e confirmação verificável dos responsáveis pela regra de unificação; até então manter B4-01/02/05 pendentes e não usar contas que não são de teste.
