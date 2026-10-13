# Status do plano

## Estado atual

- **Fase atual:** Fase 4 — integração direta e loop de saúde da conversão. Promovida em 01/10/2026 após aprovação das SPECs pelo consultor e autorização da promoção da fase. Unidade ativa: SPEC-4-001..003 + Jornada com 8 tasks + 1 subtarefa.
- **Progresso da Fase 4:** 0/8 tasks concluídas. A task `7953f975` (“Definir contrato, acesso e fallback da integração”) permanece ativa e **bloqueada**; em 13/10/2026 às 16:25 (America/Bahia) Ricardo respondeu ao roteiro de confirmação B4 (direção relatada Skip → Kommo; prevalência de conflito: nada se sobrescreve, com reconciliação humana; identificador externo e escopo da fusão ainda a definir; base legal indicada: Consentimento; conta de teste segregada ainda indisponível), mas a evidência apresentada (“Karol - 13/10/2026”) não atende ao padrão exigido — sem citação literal e sem hora — e os gates B4-01/02/05 seguem pendentes.
- **Gate anterior:** Fase 3 encerrada em 2026-09-30 — 9/9 tasks; SPEC-3-001 e SPEC-3-002 aceitas sem ressalva pelo consultor; Fase 3 arquivada em `05_entregas/fase-3/`.
- **Gate atual:** B4-01 pendente: base legal “Consentimento” indicada apenas como relato de Ricardo (13/10), sem validação do responsável interno por privacidade/LGPD nem confirmação verificável do Champion; escopo de escrita não informado. B4-02 pendente: direção Skip → Kommo relatada sem evidência direta; conta de teste segregada ainda não disponível (a conta Kommo informada não é de teste); permissões e prova técnica não validadas. Não acessar contas não-testes. B4-05 pendente: direção e prevalência de conflito relatadas sem evidência direta; escopo do “todo o histórico” da fusão e identificador externo ainda a definir; sem confirmação verificável do Comercial; não mesclar histórico enquanto isso persistir.
- **Dúvida residual de execução:** a direção Skip → Kommo foi relatada por Ricardo em 13/10/2026 atribuída à Champion, sem citação literal; o papel de cada sistema campo a campo e o descarte explícito de Lovable ainda não estão documentados por fonte direta. Não presumir a direção nem alterar a SPEC. Produção não publicada.

## Decisões concluídas

- **B3-01..B3-05 (Fase 3):** taxonomia, métrica norte, vínculo triagem→agendamento, matriz de acesso e critério do baseline foram decididos na Fase 3.
- **SPEC-3-001 e SPEC-3-002:** aceitas sem ressalva em 28/09 e 30/09/2026.
- **SPECs da Fase 4 (SPEC-4-001..003):** aprovadas pelo consultor em 30/09/2026.

## Ressalvas do fechamento da Fase 3

- Baseline operacional não congelado (Champion → B4-04 antes da ativação do loop); LGPD/autorização de escrita externa (Champion → B4-01); RN-2.06 e capacidade do sábado (Champion, F5 ou ciclo futuro); export sanitizado (task própria se virar requisito).

## Próxima ação

Obter a citação literal com data/hora da mensagem original da Champion (confirmação do destino e da direção Skip → Kommo) e do Comercial (regra de unificação — B4-05); criar conta de teste segregada para a prova técnica (B4-02) e validar a base legal “Consentimento” com o responsável por privacidade/LGPD (B4-01). Até lá, manter a task bloqueada e não acessar contas que não sejam de teste nem realizar escrita externa.
