# Status do plano

## Estado atual

- **Fase atual:** Fase 4 — integração direta e loop de saúde da conversão. Promovida em 01/10/2026 após aprovação das SPECs pelo consultor e autorização da promoção da fase. Unidade ativa: SPEC-4-001..003 + Jornada com 8 tasks + 1 subtarefa.
- **Progresso da Fase 4:** 0/8 tasks concluídas. A task `7953f975` (“Definir contrato, acesso e fallback da integração”) permanece ativa e **bloqueada**; Ricardo forneceu nova atribuição de escopo às 16:24 de 09/10, mas os gates B4-01/02/05 seguem pendentes.
- **Gate anterior:** Fase 3 encerrada em 2026-09-30 — 9/9 tasks; SPEC-3-001 e SPEC-3-002 aceitas sem ressalva pelo consultor; Fase 3 arquivada em `05_entregas/fase-3/`.
- **Gate atual:** B4-01 continua pendente: base legal e escopo de escrita não informados. B4-02 continua pendente: Ricardo indicou Kommo + plataforma Skip e atribuiu a decisão a Karol (Champion), em 09/10; isso é relato de Ricardo, sem mensagem original. A conta Kommo foi anteriormente informada como não sendo de teste; permissões e prova em ambiente autorizado não foram validadas. Não acessar contas não-testes. B4-05 continua pendente: falta mapear direção/campos/identificador externo; a aprovação da regra de unificar histórico por nome completo + telefone foi atribuída por Ricardo a Karol, mas sem evidência direta ou aprovação verificável do Comercial, e sem definição de escopo, auditoria, proveniência e rollback.
- **Dúvida residual de execução:** o par mais recente é Kommo + plataforma Skip conforme relato de Ricardo; a direção da integração (Skip→Kommo, Kommo→Skip ou outra), o papel de cada sistema e se Lovable foi descartado ainda não estão documentados por fonte direta. Não presumir a direção nem alterar a SPEC. Produção não publicada.

## Decisões concluídas

- **B3-01..B3-05 (Fase 3):** taxonomia, métrica norte, vínculo triagem→agendamento, matriz de acesso e critério do baseline foram decididos na Fase 3.
- **SPEC-3-001 e SPEC-3-002:** aceitas sem ressalva em 28/09 e 30/09/2026.
- **SPECs da Fase 4 (SPEC-4-001..003):** aprovadas pelo consultor em 30/09/2026.

## Ressalvas do fechamento da Fase 3

- Baseline operacional não congelado (Champion → B4-04 antes da ativação do loop); LGPD/autorização de escrita externa (Champion → B4-01); RN-2.06 e capacidade do sábado (Champion, F5 ou ciclo futuro); export sanitizado (task própria se virar requisito).

## Próxima ação

Obter confirmação verificável da Champion/Comercial sobre o par e a direção Kommo↔Skip, além da regra de unificação (escopo, auditoria, proveniência e rollback); completar também B4-01 e os requisitos de conta/permissões/prova em ambiente de teste de B4-02. Até lá, manter a task bloqueada e não acessar contas que não sejam de teste nem realizar escrita externa.
