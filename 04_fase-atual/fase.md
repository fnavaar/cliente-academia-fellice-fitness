# Fase 1 — Tarefas gerais

> Leva 1: tarefas de desbloqueio autorizadas. Elas não criam formulário, fila, conta, conector ou publicação; registram as decisões humanas exigidas pelas SPECs. São independentes entre si.

## Tasks

| ID | Task | Dono | SPEC | Critério | Subseção da SPEC | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Status |
|---|---|---|---|---|---|---|---|---|---|---|
| F1-T001 | Registrar plataforma, URLs e papel de publicação | Champion do cliente | SPEC-1-001 | Nome da plataforma, URLs de teste/produção e papel/usuário que publica versões estão registrados. | `## BLOQUEIOS executáveis` (plataforma/publicação) | Conferência documental do primeiro bloqueio da SPEC-1-001; nenhum formulário ou conta é criado. | Champion tem a decisão e referência da plataforma. | Pare se nome, URL ou publicador não forem informados; não escolher tecnologia ou destino. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-08-21 |
| F1-T002 | Registrar canal humano e cobertura por turno | Champion do cliente | SPEC-1-002 | Canal operacional está nomeado e cada turno tem responsável identificado. | `## BLOQUEIOS executáveis` (canal e responsável por turno) | Conferência documental do primeiro bloqueio da SPEC-1-002; nenhuma fila, webhook ou mensagem é criada. | Champion tem a decisão de canal e cobertura. | Pare se houver canal ou turno sem responsável; não apontar WhatsApp, CRM ou outro destino. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-08-21 |
| F1-T003 | Registrar contrato de campos da triagem | Liderança Comercial | SPEC-1-001 | A tabela aprovada define texto, ordem, opções e obrigatoriedade de `objetivo`, `proximidade`, `ocupacao` e `interesse_em_visita`. | `## BLOQUEIOS executáveis` (contrato de respostas) | Conferência documental do segundo bloqueio da SPEC-1-001; nenhum campo é configurado na plataforma. | Liderança Comercial fornece as escolhas aprovadas. | Pare se qualquer campo/valor/opção estiver ausente ou ambíguo; não inventar resposta padrão. | bloqueada — aguarda decisão humana | pendente |
| F1-T004 | Registrar aviso de privacidade e consentimento | Champion do cliente | SPEC-1-001 | Texto ou referência exata do aviso/consentimento aplicável ao contato está aprovado e registrado. | `## BLOQUEIOS executáveis` (privacidade/consentimento) | Conferência documental do terceiro bloqueio da SPEC-1-001; nenhum dado real é coletado. | Champion fornece o texto ou a referência aprovada. | Pare se o aviso não cobrir a coleta de contato; não redigir ou publicar por inferência. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-08-21 |
| F1-T005 | Registrar regras de distribuição e encerramento humano | Liderança Comercial | SPEC-1-002 | Estados permitidos, responsável por transição e regra de reatribuição/encerramento estão aprovados. | `## BLOQUEIOS executáveis` (distribuição e encerramento) | Conferência documental do segundo bloqueio da SPEC-1-002; nenhum estado é configurado em ferramenta. | Liderança Comercial fornece as regras aprovadas. | Pare se uma transição, reatribuição ou encerramento não tiver responsável; não criar regra automática. | bloqueada — aguarda decisão humana | pendente |
| F1-T006 | Registrar permissões mínimas do encaminhamento humano | Champion do cliente | SPEC-1-002 | Matriz curta define permissões de leitura, assunção, reatribuição e publicação para Champion e Consultor Comercial. | `## BLOQUEIOS executáveis` (papéis mínimos) | Conferência documental do terceiro bloqueio da SPEC-1-002; nenhuma permissão é concedida. | Champion confirma os papéis mínimos. | Pare se uma permissão ou papel estiver ausente; não alterar acesso de sistema. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-08-21 |

## Decisão registrada — F1-T001

- **Plataforma:** Skip
- **URL de teste/produção:** https://fellice-fitness-8733f--preview.goskip.app (preview) / https://fellice-fitness-8733f.goskip.app (produção)
- **Builder:** https://goskip.dev/rifelice-a3196/builder/09feac62-d564-4c83-969d-b786af1576ff
- **Publicadores:** Karol e Márcio (ambos podem publicar versões)

## Decisão registrada — F1-T002

- **Canal operacional:** WhatsApp, telefone e e-mail
- **Turno manhã:** Jaqueline
- **Turno tarde:** Camila
- **Turno noite:** Rodrigo
- **Fim de semana:** regime de escala, alternando entre Jaqueline, Camila e Rodrigo
- **Supervisora comercial:** Mel

## Decisão registrada — F1-T004

- **Base legal:** Lei Geral de Proteção de Dados (LGPD)
- **Texto de consentimento:** "O lead autoriza que a ACADEMIA se utilize dos meios eletrônicos (e-mail, telefone, mensagens SMS e Whatsapp) com o objetivo de enviar notícias, avisos, dicas, promoções e outras informações relevantes acerca do funcionamento da academia."
- **Cobertura:** e-mail, telefone, SMS e WhatsApp

## Decisão registrada — F1-T006

| Ação | Champion (Karol/Márcio) | Consultor Comercial |
|---|---|---|
| Ler a fila | ✅ | ✅ |
| Assumir caso | ✅ | ✅ |
| Reatribuir caso | ✅ | ❌ |
| Publicar versões | ✅ | ❌ |
