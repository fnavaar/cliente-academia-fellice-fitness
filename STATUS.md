# Status do plano

## Estado atual

- **Fase atual:** Fase 4 — integração direta e loop de saúde da conversão. Promovida em 01/10/2026 após aprovação das SPECs pelo consultor e autorização da promoção da fase. Unidade ativa: SPEC-4-001..003 + Jornada com 8 tasks + 1 subtarefa.
- **Progresso da Fase 4:** 0/8 tasks concluídas. A task `7953f975` (“Definir contrato, acesso e fallback da integração”) permanece ativa, porém **bloqueada por DÚVIDA material de escopo**. Ricardo aprovou às 16:07 de 09/10/2026 somente o registro parcial das respostas; B4-01/02/05 seguem sem liberação.
- **Gate anterior:** Fase 3 encerrada em 2026-09-30 — 9/9 tasks; SPEC-3-001 e SPEC-3-002 aceitas sem ressalva pelo consultor; Fase 3 arquivada em `05_entregas/fase-3/`.
- **Gate atual:** B4-01 segue pendente (base legal e escopo de escrita marcados como PENDENTE). B4-02 segue pendente: Ricardo informou preferência por Kommo + Lovable e contas existentes que não são de teste; permissões e prova técnica seguem pendentes. Não acessar essas contas nem realizar leitura/escrita: a SPEC exige prova em conta de teste sem massa real. B4-05 segue pendente: destino Lovable ou plataforma Skip não foi decidido, identificador externo não está definido e a regra relatada de unificar histórico por nome completo + telefone não tem identificação/evidência verificável dos aprovadores nem semântica segura/auditável/reversível definida.
- **DÚVIDA bloqueante:** a SPEC-4-001 prevê Kommo e/ou Lóvavel, enquanto as respostas citam Lovable e também a plataforma Skip como possíveis destinos. Não presumir equivalência entre Lovable e Lóvavel, nem ampliar ou alterar a SPEC. Confirmar destino/escopo com consultor/Champion antes de avançar. Produção não publicada.

## Decisões concluídas

- **B3-01..B3-05 (Fase 3):** taxonomia, métrica norte, vínculo triagem→agendamento, matriz de acesso e critério do baseline foram decididos na Fase 3.
- **SPEC-3-001 e SPEC-3-002:** aceitas sem ressalva em 28/09 e 30/09/2026.
- **SPECs da Fase 4 (SPEC-4-001..003):** aprovadas pelo consultor em 30/09/2026.

## Ressalvas do fechamento da Fase 3

- Baseline operacional não congelado (Champion → B4-04 antes da ativação do loop); LGPD/autorização de escrita externa (Champion → B4-01); RN-2.06 e capacidade do sábado (Champion, F5 ou ciclo futuro); export sanitizado (task própria se virar requisito).

## Próxima ação

Obter do consultor/Champion esclarecimento verificável sobre o sistema-alvo (Lovable, Lóvavel ou plataforma Skip) e a regra de unificação; em seguida, completar as validações pendentes de B4-01/02/05. Até lá, manter a task bloqueada e não acessar contas que não são de teste nem realizar escrita externa.
