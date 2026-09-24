# Changelog

## 2026-08-20

- Criado `03-Projeto/requisitos.md` pela rota padrão da análise crítica.
- Registrados nove requisitos verificáveis, suas fontes, limites, dependências e decisões humanas pendentes.
- Criado `03-Projeto/revisao-do-escopo.md` com painel serial, achados calibrados, alternativas e riscos residuais.
- Criado `03-Projeto/conselho-de-decisao.md` com recomendação não vinculante para a sequência C.
- Criados `03-Projeto/analise-critica.md` e `03-Projeto/analise-do-consultor.md`; o segundo permanece integralmente pendente de autoria humana.
- Criado `STATUS.md` com o gate atual e a próxima ação segura.
- Consolidado `03-Projeto/02-Escopo-Definitivo.md` em cinco fases, incorporando a decisão humana de pré-agendamento e integração direta tardia.
- Criados a matriz de rastreabilidade e o controle interno `.adapta/checks/check-escopo.md` com status PENDENTE.
- Registrada a revisão serial do escopo definitivo; aplicada correção segura de rastreabilidade para não reintroduzir requisitos fora do recorte de pré-agendamento.
- Gerado `03-Projeto/03-Setup-Ethos/` em estado RASCUNHO, incluindo persona, sugestões de conectores, mapa operacional e dois loops candidatos sem ativação.

## 2026-08-21

- Registrada aprovação humana do escopo em `.adapta/checks/check-escopo.md`.
- Geradas e revisadas as SPECs da Fase 1: captura/triagem rastreável (SPEC-1-001) e encaminhamento humano com contexto preservado (SPEC-1-002).
- O painel serial confirmou que plataforma/publicação/consentimento, contrato final de campos, canal humano, distribuição/encerramento e permissões não constam nas fontes. As duas SPECs foram marcadas como bloqueadas para evitar decisões ou acessos inventados.
- Autorizada a primeira leva de tasks de desbloqueio: F1-T001 a F1-T006 registram, separadamente, plataforma/publicação, canal/cobertura, campos, consentimento, distribuição/encerramento e permissões. Todas permanecem bloqueadas até decisão humana, sem criar superfícies, contas, conectores ou publicação.
- Criada e validada a pasta operacional local `../Cliente — Academia Fellice Fitness/`, contendo somente a base pública, tasks e SPECs da Fase 1; não foi criado repositório, commit, push, convite ou publicação.
- Criado `03-Projeto/scorecard-comparativo-mapa-mental-r1.md` para comparar o mapa mental R1 recebido com o processo, sistemas e limites aprovados.

## 2026-09-10

- Registrada conclusão da Fase 1: F1-T001 a F1-T006 resolvidas com evidências humanas; gate da Fase 1 encerrado.
- Geradas as SPECs da Fase 2: agenda de disponibilidade e reserva (SPEC-2-001) e visão operacional de tentativas (SPEC-2-002). Ambas marcadas como bloqueadas até resolução das tasks de desbloqueio.
- O painel serial confirmou que grade de disponibilidade, duração, capacidade, responsável da agenda, campos mínimos de agendamento, papéis, permissões, regra de encaminhamento e critério de escalada não constam nas fontes. As duas SPECs foram marcadas como bloqueadas para evitar decisões ou configurações inventadas.
- Autorizada a primeira leva de tasks de desbloqueio da Fase 2: F2-T001 a F2-T005 registram, separadamente, grade/duração/capacidade, responsável da agenda, campos, consentimento, distribuição/encerramento e permissões. Todas permanecem bloqueadas até decisão humana, sem criar slots, agenda, contas, conectores ou publicação.
- Atualizados o índice da Fase 2 (`00-INDICE.md`), as tasks gerais da Fase 2 (`00-Tasks_Gerais.md`) e o `STATUS.md`; fase atual passa a ser Fase 2.

## 2026-09-21

- Registrado o encerramento da Fase 2: F2-T001..T005 (documentais, 16/09) e F2-IMP-001..009 (implementação, 17–21/09) concluídas com testes humanos; SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; implementação 9/9 no ambiente de teste, sem publicação em produção.
- Registrado `.adapta/checks/check-fase-2.md` APROVADO COM RESSALVAS com o digest ativo do estado encerrado (active-sha256=9baf0925b3663386dbb5a97365d4436bd38bde528799905afdb0aa0567025c32 (repo HEAD 1287e3d).
- Mapeadas e decididas as evoluções do fechamento da F2 em `.adapta/evolucoes/delta-fase-3.md`: EV-F2-01 (vínculo triagem→agendamento) promovida a bloqueio B3-03 da Fase 3; LGPD, capacidade do sábado e CA-2.03 adiadas com dono e prazo; aprendizados técnicos registrados como notas de construção.
- Geradas as SPECs da Fase 3 em modo onda: SPEC-3-001 (consolidação somente leitura dos eventos das fases 1 e 2 em funil com numerador/denominador/período e cobertura) e SPEC-3-002 (dashboard por formulário, versão e campanha com baseline congelado e matriz de acesso). Ambas bloqueadas por B3-01..B3-05 (taxonomia, fórmula/janela, vínculo, matriz de acesso, baseline).
- Atualizados o índice da Fase 3, as tasks gerais da Fase 3, a matriz de rastreabilidade, a Jornada `fase_3.md` (4 tasks de decisão/fechamento com UUIDs preservados) e o `STATUS.md`; fase atual passa a ser Fase 3. Nenhuma task de implementação foi gerada; `gerar-tasks` aguarda aprovação das SPECs.

## 2026-09-24

- Reconciliada a liberação documental da Fase 3 com o estado atual do Plano: cinco decisões B3-01..B3-05 liberadas ao Champion, 10 cards na Jornada e decisão P1 registrada.
- Promovida a Fase 3 para a unidade ativa; a Fase 2 foi arquivada em `05_entregas/fase-2/`.
- Mantidos os bloqueios: nenhuma implementação começa antes das decisões humanas e dos aceites previstos nas SPECs.
- **B3-01 concluída documentalmente:** Karol decidiu manter `utm_source` separado por fonte, `utm_medium` separado por valor, agrupar `utm_campaign` por campanha e colocar valores ausentes/não reconhecidos em grupo próprio. Decisão registrada em `03_documentos/decisoes-fase-3.md`; nenhuma configuração, agregação ou código foi criado.
- **DÚVIDA — B3-02 permanece bloqueada:** a resposta recebida em 24/09/2026 informou “Agendamentos concluídos no período” como numerador, “Fase de agendamentos comparecidos” como denominador e “Últimos 30 dias corridos, semana ou mês civil” como janela. A janela contém três alternativas e não define uma janela padrão; o denominador não identifica inequivocamente o evento/status a contar; e a confirmação foi informada como “24/09/2026, Karol confirmou”, sem citação literal ou referência ao registro verificável. Nenhuma decisão foi escrita no registro canônico e nenhum produto foi alterado. Necessário retornar uma única janela, esclarecer o denominador e fornecer confirmação verificável do Champion.
- **DÚVIDA atualizada — B3-02 continua bloqueada:** a correção recebida em 24/09/2026 definiu a janela como “Últimos 30 dias corridos” e o denominador como “Status visita agendada comparecida”. A janela ficou válida, mas o denominador usa comparecimento, explicitamente fora do escopo atual da SPEC-3-001; mantê-lo requer decisão formal separada para alteração de escopo. A confirmação “24/09/2026 - Karol” ainda não contém citação literal nem referência verificável. Nenhuma decisão foi escrita no registro canônico e nenhum produto foi alterado.
- **B3-02 — denominador corrigido, decisão ainda pendente:** o denominador foi alterado para “Encaminhamentos humanos no mesmo período”. Com o numerador “Agendamentos concluídos no período” e a janela “Últimos 30 dias corridos”, o conteúdo ficou compatível com a SPEC-3-001. A confirmação atribuída a Karol em 24/09/2026 ainda precisa de citação literal ou referência verificável; por isso, a decisão não foi registrada no documento canônico e nenhum produto foi alterado.
- **B3-02 concluída documentalmente:** em 24/09/2026, Karol confirmou “Karol confirma, libere as tasks”. O registro canônico passou a definir numerador como “Agendamentos concluídos no período”, denominador como “Encaminhamentos humanos no mesmo período”, janela padrão de “Últimos 30 dias corridos” e a fórmula documental correspondente. Nenhuma meta foi inferida, nenhum produto foi alterado e a implementação da SPEC-3-001 permanece bloqueada até B3-03.
- 2026-09-24 · Karol (Champion) · Task B3-02 concluída: decisão documental aprovada após conferência humana de Ricardo; fórmula definida como agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período, com janela de últimos 30 dias corridos. Evidência em `03_documentos/decisoes-fase-3.md`; nenhum produto foi alterado.
