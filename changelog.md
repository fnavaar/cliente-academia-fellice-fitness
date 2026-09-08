# Changelog

## 2026-09-08

- [champion] Task F1-T008 concluída: fila de encaminhamento humano com contexto preservado implementada no Skip 51806; autenticação de atendente, estados, eventos, idempotência e encerramento com motivo validados; QA 0.0.12 passou e teste humano aprovado no preview.
- [debug] DEBUG task F1-T008: lead era salvo, mas a fila não aparecia por falta de autenticação na visão do atendente; evento HANDOFF_CREATED falhava por regra de criação protegida; login autorizado e evento público de criação corrigidos, com leitura/ações protegidas.
- [champion] Task F1-T007 concluída: formulário de captura e triagem rastreável implementado no Skip 51806, com persistência no Skip Cloud, campos aprovados, UTMs, eventos e consentimento LGPD; QA 0.0.8 passou e teste humano foi aprovado no preview.
- [debug] DEBUG task F1-T007: falha no evento de conclusão corrigida usando `leadSubmissionId.current`; submissão e evento sintéticos retornaram HTTP 200.
- [liderança comercial] Task F1-T003 concluída: contrato de campos da triagem registrado — proximidade (1º, obrigatório), objetivo (2º, obrigatório), ocupacao (3º, opcional), interesse_em_visita (4º, obrigatório), com textos, opções e ordem aprovados.
- [liderança comercial] Task F1-T005 concluída: regras de distribuição e encerramento registradas — estados PENDENTE, ASSUMIDO e ENCERRADO_SEM_AGENDAMENTO; transições definidas (PENDENTE→ASSUMIDO por quem assume; ASSUMIDO→ENCERRADO com motivo obrigatório; ENCERRADO é estado final); reatribuição exclusiva da liderança/perfil autorizado com histórico preservado; encerramento pelo responsável ou gestão, com motivo livre obrigatório e registro completo (responsável, data/hora, motivo, responsável anterior).

## 2026-08-21

- Preparada a base operacional local da Fase 1, com tasks e SPECs da fase atual.
- [champion] Task F1-T001 concluída: plataforma Skip registrada, URLs de preview/produção definidas, Karol e Márcio como publicadores.
- [champion] Task F1-T002 concluída: canais de atendimento humano (WhatsApp, telefone, e-mail), cobertura por turno (manhã: Jaqueline, tarde: Camila, noite: Rodrigo), fim de semana por escala, supervisora Mel.
- [champion] Task F1-T004 concluída: texto de consentimento LGPD registrado — "O lead autoriza que a ACADEMIA se utilize dos meios eletrônicos (e-mail, telefone, mensagens SMS e Whatsapp) com o objetivo de enviar notícias, avisos, dicas, promoções e outras informações relevantes acerca do funcionamento da academia."
- [champion] Task F1-T006 concluída: matriz de permissões — Champion (ler/assumir/reatribuir/publicar: sim para todas); Consultor Comercial (ler: sim, assumir: sim, reatribuir: não, publicar: não).
