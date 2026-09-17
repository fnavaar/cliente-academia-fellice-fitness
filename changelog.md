## 2026-09-17 — Implementação F2-IMP-002

- [champion via consultoria] Task F2-IMP-002 concluída: grade de disponibilidade de teste materializada no Skip 51806 (v0.0.23) — migração 0011 gerou 248 slots sintéticos cobrindo 14 dias: segunda a sexta das 08:00 às 19:30 e sábado das 09:00 às 13:30, blocos de 30 minutos, capacidade 1, com exceção de capacidade 2 nos blocos que começam entre 11:30 e 16:30 exatos (interpretação corrigida pelo consultor em 17/09/2026; 11 blocos por dia útil; aplica-se também aos 8 blocos de sábado dentro da janela — [VALIDAR NA CALL DE SETUP]).
- [verificação] Pipeline QA completo passou. Ciclo de vida da grade provado via API com usuário sintético temporário (0012): criar slot, editar capacidade (1→2), bloquear, reabrir e apagar — todos ok; prova negativa: sem login, nenhuma criação/alteração de slot é aceita (HTTP 400). Fixtures antigas da F2-IMP-001 removidas pela própria migração; rollback cirúrgico garantido pela âncora created_by='grade-teste' (down remove somente os slots gerados).
- [teste humano] Aprovado pelo consultor em 17/09/2026 ("funcionou") — grade conferida via API (248 slots, duração 30, status ABERTO, capacidade variável) e login do papel responsável pela agenda validado na rota /fila do preview.
- [segurança] Usuário sintético temporário criado (0012) para a prova do ciclo de vida e removido após o aceite (0013); senha provisória deixou de existir. Revalidação final: grade intacta (248 slots), acesso de teste recusado, janela de capacidade preservada (11 blocos cap 2 em 21/09).
- [limite] Nenhuma tela criada, nenhum dado real tratado, nenhuma integração externa, nenhuma publicação em produção. A grade é de teste; a seleção pelo lead é a F2-IMP-003.

## 2026-09-17 — Implementação F2-IMP-001

- [champion via consultoria] Task F2-IMP-001 concluída: contrato técnico e fixtures sintéticas de agenda/tentativa implementados no Skip 51806 (v0.0.20) — migração 0007 criou as coleções `agenda_slots` (slot, duração 30 min, capacidade 1/2, ABERTO/RESERVADO/BLOQUEADO), `lead_appointments` (TENTATIVA/CONCLUIDO/DESISTENCIA/ENCAMINHAMENTO_HUMANO, índice único lead_submission_id+slot_id como âncora de idempotência RN-2.05/CA-2.02) e `lead_appointment_events` (append-only); migração 0008 semeou fixtures 100% sintéticas cobrindo caminho válido, campos ausentes, slot bloqueado, capacidade 2, desistência e encaminhamento humano.
- [verificação] Pipeline QA completo passou (setup, análise estática, build, integrações, testes). Provas ao vivo via API: duplicata de reserva recusada pelo banco (HTTP 400), criação pública de tentativa aceita, leitura anônima de tentativas sem vazamento (lista vazia), leitura autenticada com login de consultor retornando 6 tentativas e 4 eventos. Teste humano do consultor aprovado em 17/09/2026 ("entrei e testado, está aparecendo. tudo ok, aprovado") — site sem rotas novas, dados protegidos, grade pública legível.
- [segurança] Usuário sintético de teste criado (0009) para a validação de leitura autenticada e removido após o aceite (0010); senha provisória deixou de existir.
- [limite] Nenhuma tela criada, nenhum dado real tratado, nenhuma integração externa, nenhuma publicação em produção. Contrato técnico completo registrado no workspace da consultoria; pendências LGPD (base legal do agendamento) e semântica de reagendamento (RN-2.06) registradas no STATUS para validação antes de F2-IMP-003.
- [correção de registro] A auditoria de 16/09 registrou "`/queue` retorna 404"; a rota real do atendente na Fase 1 é `/fila`, que existe e renderiza o login corretamente.

# Changelog

## 2026-09-16

- [liderança comercial] Task F2-T005 concluída: escalada de tentativas paradas registrada — papel responsável: Gestão/Subgerente Comercial + Supervisora Comercial (Mel); critério de parada: tentativa em ENCAMINHAMENTO_HUMANO sem ação até o fim do turno de origem; poderes: reatribuir ou encerrar com motivo obrigatório. Sinalização visual apenas, sem mudança automática de estado (RN-2.10). Com esta task, os 5/5 bloqueios documentais da Fase 2 estão resolvidos; implementação aguarda novo ciclo.
- [champion + liderança comercial] Task F2-T004 concluída: matriz de permissões da visão operacional registrada — Consultor Comercial lê e atualiza tentativas atribuídas a ele ou em ENCAMINHAMENTO_HUMANO e pode reatribuir dentro da visão operacional; Subgerente/Gestão leem todos os estados, editam estado e sinalizam escalada de tentativa parada; Marketing sem acesso a dados individuais. Regra de encaminhamento registrada — fila única, motivo de catálogo fixo + campo livre. Registro documental apenas; nenhuma permissão foi concedida no Skip.
- [liderança comercial] Task F2-T003 concluída: contrato de campos mínimos para concluir o agendamento registrado — nome, telefone/canal de retorno, localidade e profissão obrigatórios; e-mail opcional. Registro documental apenas; nenhum campo foi configurado no Skip.
- [champion] Task F2-T002 concluída: responsável por manter e fechar a agenda registrado — Consultores Comerciais Camila, Jaqueline e Rodrigo; Subgerente Comercial e Champion também podem exercer o papel. Nenhuma permissão foi concedida no Skip.
- [subgerente comercial] Task F2-T001 concluída: duração 30 min, capacidade 1, exceção 2 entre 11:30–16:30 e grade seg–sex 08:00–19:30/sáb 09:00–13:30. Registro documental apenas; nenhum slot ou agenda foi criado no Skip.

## 2026-09-16 — Reconciliação Fase 2 após auditoria do preview

- [auditoria] Comparado o GitHub com o preview `https://fellice-fitness-8733f--preview.goskip.app`: a triagem F1 está presente; agenda/seleção de slot/campos de agendamento não aparecem; `/queue` retorna 404; nenhuma entrega da Fase 2 foi comprovada no produto.
- [tasks] Criadas documentalmente as tasks F2-IMP-001..F2-IMP-009 para materializar SPEC-2-001 e SPEC-2-002. F2-IMP-001 é a única elegível; as demais dependem de provas e aceite humano.
- [limite] Nenhum arquivo de código, migration, schema, banco, configuração do Skip ou publicação foi alterado nesta reconciliação; a mudança é de documentação operacional no GitHub.

## 2026-09-10

- [consultoria] Fase 2 liberada documentalmente no repositório do cliente: autoagendamento assistido e continuidade da jornada.
- [consultoria] Publicadas SPEC-2-001 e SPEC-2-002 e as tasks F2-T001 a F2-T005.
- [limite] Nenhuma alteração foi feita no app, Skip, banco ou integrações; as cinco tasks ativas são decisões humanas de desbloqueio.

## 2026-09-08

- [champion] Task F1-T008 concluída: fila de encaminhamento humano com contexto preservado implementada no Skip 51806; autenticação de atendente, estados, eventos, idempotência e encerramento com motivo validados; QA 0.0.12 passou e teste humano aprovado no preview.
- [debug] DEBUG task F1-T008: lead era salvo, mas a fila não aparecia por falta de autenticação na visão do atendente; evento HANDOFF_CREATED falhava por regra de criação protegida; login autorizado e evento público de criação corrigidos, com leitura/ações protegidas.
- [champion] Task F1-T007 concluída: formulário de captura e triagem rastreável implementado no Skip 51806, com persistência no Skip Cloud, campos aprovados, UTMs, eventos e consentimento LGPD; QA 0.0.8 passou e teste humano foi aprovado no preview.
- [debug] DEBUG task F1-T007: falha no evento de conclusão corrigida usando leadSubmissionId.current; submissão e evento sintéticos retornaram HTTP 200.
- [liderança comercial] Task F1-T003 concluída: contrato de campos da triagem registrado — proximidade, objetivo, ocupacao e interesse_em_visita.
- [liderança comercial] Task F1-T005 concluída: regras de distribuição e encerramento registradas — PENDENTE, ASSUMIDO e ENCERRADO_SEM_AGENDAMENTO.

## 2026-08-21

- Preparada a base operacional local da Fase 1, com tasks e SPECs da fase atual.
- [champion] Task F1-T001 concluída: plataforma Skip registrada, URLs de preview/produção definidas, Karol e Márcio como publicadores.
- [champion] Task F1-T002 concluída: canais de atendimento humano, cobertura por turno e supervisora Mel.
- [champion] Task F1-T004 concluída: texto de consentimento LGPD registrado.
- [champion] Task F1-T006 concluída: matriz de permissões da Fase 1 registrada.
