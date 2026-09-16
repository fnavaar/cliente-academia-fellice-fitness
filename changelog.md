## 2026-09-16 — Reconciliação Fase 2 após auditoria do preview

- [auditoria] Comparado o GitHub com o preview `https://fellice-fitness-8733f--preview.goskip.app`: a triagem F1 está presente; agenda/seleção de slot/campos de agendamento não aparecem; `/queue` retorna 404; nenhuma entrega da Fase 2 foi comprovada no produto.
- [tasks] Criadas documentalmente as tasks F2-IMP-001..F2-IMP-009 para materializar SPEC-2-001 e SPEC-2-002. F2-IMP-001 é a única elegível; as demais dependem de provas e aceite humano.
- [limite] Nenhum arquivo de código, migration, schema, banco, configuração do Skip ou publicação foi alterado nesta reconciliação; a mudança é de documentação operacional no GitHub.

# Changelog

## 2026-09-16

- [liderança comercial] Task F2-T005 concluída: escalada de tentativas paradas registrada — papel responsável: Gestão/Subgerente Comercial + Supervisora Comercial (Mel); critério de parada: tentativa em ENCAMINHAMENTO_HUMANO sem ação até o fim do turno de origem; poderes: reatribuir ou encerrar com motivo obrigatório. Sinalização visual apenas, sem mudança automática de estado (RN-2.10). Com esta task, os 5/5 bloqueios documentais da Fase 2 estão resolvidos; implementação aguarda novo ciclo.
- [champion + liderança comercial] Task F2-T004 concluída: matriz de permissões da visão operacional registrada — Consultor Comercial lê e atualiza tentativas atribuídas a ele ou em ENCAMINHAMENTO_HUMANO e pode reatribuir dentro da visão operacional; Subgerente/Gestão leem todos os estados, editam estado e sinalizam escalada de tentativa parada; Marketing sem acesso a dados individuais. Regra de encaminhamento registrada — fila única, motivo de catálogo fixo + campo livre. Registro documental apenas; nenhuma permissão foi concedida no Skip.
- [liderança comercial] Task F2-T003 concluída: contrato de campos mínimos para concluir o agendamento registrado — nome, telefone/canal de retorno, localidade e profissão obrigatórios; e-mail opcional. Registro documental apenas; nenhum campo foi configurado no Skip.
- [champion] Task F2-T002 concluída: responsável por manter e fechar a agenda registrado — Consultores Comerciais Camila, Jaqueline e Rodrigo; Subgerente Comercial e Champion também podem exercer o papel. Nenhuma permissão foi concedida no Skip.
- [subgerente comercial] Task F2-T001 concluída: duração 30 min, capacidade 1, exceção 2 entre 11:30–16:30 e grade seg–sex 08:00–19:30/sáb 09:00–13:30. Registro documental apenas; nenhum slot ou agenda foi criado no Skip.

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
