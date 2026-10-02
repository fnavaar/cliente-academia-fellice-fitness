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
- Atualizados o índice da Fase 1, a matriz de rastreabilidade e o `STATUS.md`; tasks continuam vazias até o bloqueio ser resolvido e a etapa `gerar-tasks` ser autorizada.
- Autorizada a primeira leva de tasks de desbloqueio: F1-T001 a F1-T006 registram, separadamente, plataforma/publicação, canal/cobertura, campos, consentimento, distribuição/encerramento e permissões. Todas permanecem bloqueadas até decisão humana, sem criar superfícies, contas, conectores ou publicação.
- Criada e validada a pasta operacional local `../Cliente — Academia Fellice Fitness/`, contendo somente a base pública, tasks e SPECs da Fase 1; não foi criado repositório, commit, push, convite ou publicação.
- Criado `03-Projeto/scorecard-comparativo-mapa-mental-r1.md` para comparar o mapa mental R1 recebido com o processo, sistemas e limites aprovados.

## 2026-09-10

- Registrada conclusão da Fase 1: F1-T001 a F1-T006 resolvidas com evidências humanas; gate da Fase 1 encerrado.
- Geradas as SPECs da Fase 2: agenda de disponibilidade e reserva (SPEC-2-001) e visão operacional de tentativas (SPEC-2-002). Ambas marcadas como bloqueadas até resolução das tasks de desbloqueio.
- O painel serial confirmou que grade de disponibilidade, duração, capacidade, responsável da agenda, campos mínimos de agendamento, papéis, permissões, regra de encaminhamento e critério de escalada não constam nas fontes. As duas SPECs foram marcadas como bloqueadas para evitar decisões ou configurações inventadas.
- Autorizada a primeira leva de tasks de desbloqueio da Fase 2: F2-T001 a F2-T005 registram, separadamente, grade/duração/capacidade, responsável pela agenda, campos mínimos, papéis/permissões/regra de encaminhamento e critério de escalada. Todas permanecem bloqueadas até decisão humana, sem criar slots, agenda, contas, conectores ou publicação.
- Atualizados o índice da Fase 2 (`00-INDICE.md`), as tasks gerais da Fase 2 (`00-Tasks_Gerais.md`) e o `STATUS.md`; fase atual passa a ser Fase 2.

## 2026-09-21

- Registrado o encerramento da Fase 2: F2-T001..T005 (documentais, 16/09) e F2-IMP-001..009 (implementação, 17–21/09) concluídas com testes humanos; SPEC-2-001 ACEITA (17/09) e SPEC-2-002 ACEITA (21/09) pelo Champion via consultor Ricardo Junior; implementação 9/9 no ambiente de teste, sem publicação em produção.
- Registrado `.adapta/checks/check-fase-2.md` APROVADO COM RESSALVAS com o digest ativo do estado encerrado (active-sha256=9baf0925…, repo HEAD 1287e3d) e ressalvas com dono e prazo (LGPD, capacidade do sábado, vínculo triagem→agendamento, fortalecimento server-side do CA-2.03).
- Mapeadas e decididas as evoluções do fechamento da F2 em `.adapta/evolucoes/delta-fase-3.md`: EV-F2-01 (vínculo triagem→agendamento) promovida a bloqueio B3-03 da Fase 3; LGPD, capacidade do sábado e CA-2.03 adiadas com dono e prazo; aprendizados técnicos registrados como notas de construção.
- Geradas as SPECs da Fase 3 em modo onda: SPEC-3-001 (consolidação somente leitura dos eventos das fases 1 e 2 em funil com numerador/denominador/período e cobertura) e SPEC-3-002 (dashboard por formulário, versão e campanha com baseline congelado e matriz de acesso). Ambas bloqueadas por B3-01..B3-05 (taxonomia, fórmula/janela, vínculo, matriz de acesso, baseline).
- Atualizados o índice da Fase 3, as tasks gerais da Fase 3, a matriz de rastreabilidade, a Jornada `fase_3.md` (4 tasks de decisão/fechamento com UUIDs preservados) e o `STATUS.md`; fase atual passa a ser Fase 3. Nenhuma task de implementação foi gerada; `gerar-tasks` aguarda aprovação das SPECs.

## 2026-09-23

- Registrada autorização do consultor para liberação da Fase 3 das SPECs da Fellice Fitness.
- Publicadas SPEC-3-001 e SPEC-3-002 no repositório operacional do cliente (`Cliente — Academia Fellice Fitness/04_fase-atual/specs/`).
- Autorizada a primeira leva de tarefas de desbloqueio da Fase 3: F3-T001 a F3-T005 registram taxonomia de origem/campanha, fórmula/janela da métrica norte, decisão de vínculo triagem-agendamento, matriz de acesso e critério de aprovação do baseline congelado. Todas permanecem bloqueadas até decisão humana, sem criar dashboard, agregações, banco ou publicação externa.
- Atualizados o índice da Fase 3 (`00-INDICE.md`), as tarefas gerais da Fase 3 (`00-Tasks_Gerais.md`), a matriz de rastreabilidade e o `STATUS.md` no Plano; resolvidos arquivos duplicados de conflito.
- Repositório do cliente atualizado com handoff-manifest v1 (Fase 3), `fase.md`, `STATUS.md` e `README.md`.

## 2026-09-24

- Por autorização humana registrada nesta sessão, as cinco tarefas de decisão da Fase 3 (B3-01 a B3-05) foram liberadas e atribuídas ao Champion do cliente.
- Registrada a decisão P1: o Champion decide e registra taxonomia, fórmula/janela, vínculo triagem → agendamento, matriz de acesso e critério do baseline; Marketing/agência e Gestão podem ser consultados, mas não são aprovadores obrigatórios.
- Criado `03-Projeto/decisoes-fase-3.md` como registro canônico dos cinco vereditos, com decisão, data e confirmação verificável obrigatórias. Atualizadas as duas SPECs, índice, matriz, tarefas gerais, cards canônicos e `STATUS.md`. A SPEC-3-001 continua bloqueada até B3-01..B3-03; a SPEC-3-002, até B3-01, B3-02, B3-04 e B3-05 mais o aceite da SPEC-3-001. Nenhuma permissão, integração, publicação ou dado de produção foi alterado.

## 2026-09-30

- Registrado o fechamento da Fase 3: 9/9 tasks concluídas; SPEC-3-001 e SPEC-3-002 ACEITAS SEM RESSALVA pelo consultor Navaar (28/09 e 30/09), com testes humanos do Champion registrados, QA v0.0.85 (`c41cf7c`) e runtime autenticado; produção não publicada. `.adapta/checks/check-fase-3.md` registrado APROVADO COM RESSALVAS com active-sha256=7bbfdac4e985eac699880e3539ab59e529db3636fc77c8eec4af10377652ede3 (repo HEAD `b1c045a`); ressalvas com dono e prazo (baseline não congelado, LGPD/escrita externa, RN-2.06, capacidade do sábado, export sanitizado).
- Mapeadas as evoluções do fechamento da F3 em `.adapta/evolucoes/delta-fase-4.md`: EV-F3-01 (LGPD/autorização de escrita externa → B4-01), EV-F3-02 (baseline operacional não congelado → B4-04) e EV-F3-03 (matriz de acesso do painel de saúde → B4-03) propostas como bloqueios da Fase 4; EV-F3-04..06 propostas como adiadas/rejeitadas; EV-F3-07 (allowlist explícita como autoridade; migrations aditivas limpas) proposta como regra de construção. Decisão humana (aceitar/adiar/rejeitar) pendente.
- Geradas as SPECs da Fase 4 em modo onda: SPEC-4-001 (integração direta com a ferramenta comercial — Kommo e/ou Lóvavel conforme capacidade validada; identificador externo, idempotência, fila de reconciliação e rollback), SPEC-4-002 (painel de saúde da integração e histórico somente-adição de alterações relevantes) e SPEC-4-003 (loop semanal de saúde da conversão com baseline, alvo aprovado e veredito humano). Bloqueios B4-01..B4-05 registrados no índice; nenhuma credencial, conector, escrita externa ou publicação de produção foi autorizada.
- Registrada a aprovação do consultor sobre as três SPECs da Fase 4 ("libero todas as specs, pode executar") e geradas as tasks da Fase 4: 8 tasks + 1 subtarefa (5 UUIDs do portal preservados; 3 tasks novas aguardam UUID do sincronizador), com cobertura CA-4-001..014 = 14/14 e insumos do Champion (B4-01..B4-05 e alvo do loop) embutidos nos cards. Validador `phase-tasks.mjs` PASS.

## 2026-10-01

- 2026-10-01 · Navaar (consultor) · LIBERAÇÃO DA FASE 4: consultor aprovou as três SPECs da Fase 4 ("libero todas as specs, pode executar") e autorizou a promoção F3→F4 neste repositório ("Confirmo o push: promova a Fase 4 no repositório da Fellice"). Fase 3 arquivada em `05_entregas/fase-3/` (README, Jornada e as duas SPECs aceitas sem ressalva); SPECs F3 removidas da unidade ativa (histórico Git preserva). Unidade ativa promovida para a Fase 4: Jornada `04_fase-atual/fase.md` com 8 tasks + 1 subtarefa (5 UUIDs preservados: `7953f975`, `c86d168b`, `31dae29a`, `12bf95df`, `c5ccd038`; 3 tasks novas aguardam UUID do sincronizador), `00-Tasks_Gerais.md`, `specs/00-INDICE.md` e SPEC-4-001/002/003. Insumos do Champion (B4-01..B4-05, matriz do painel de saúde e alvo do loop) embutidos nos cards para registro em `03_documentos/decisoes-fase-4.md`. Nenhuma implementação, credencial, conector, escrita externa ou publicação de produção foi iniciada. Produção não publicada.

## 2026-10-02

- Ricardo Junior autorizou a implementação da task `7953f975` ("pode implementar") após análise e plano apresentados; estado persistente atualizado e task marcada em andamento.
- Criado `03_documentos/decisoes-fase-4.md` como rascunho da task: inclui os espaços de decisão B4-01 (base legal, minimização e autorização de escrita), B4-02 (ferramenta, escopos e conta de teste) e B4-05 (mapeamento, identificador externo e conflitos), além das salvaguardas de falha, reconciliação, rollback e tratamento de segredos da SPEC-4-001. As decisões e confirmações verificáveis do Champion/Comercial permanecem pendentes; nenhum valor foi inferido.
- Registrada a situação no `STATUS.md` e na Jornada da Fase 4: 0/8 tasks concluídas, `7953f975` em andamento. Nenhuma credencial, conector, escrita externa ou publicação foi ativada; task aguarda respostas/validação humana para completar seu critério documental.
- 2026-10-02 · Ricardo Junior · DEBUG task `7953f975`: regravação de documentos cumulativos alterou texto histórico; changelog reconstruído diretamente do blob-base verificado. Diff revisado; nenhuma entrada histórica foi alterada.
