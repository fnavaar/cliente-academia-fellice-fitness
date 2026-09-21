## 2026-09-21 — Fechamento F2-IMP-009 (veredito ACEITO — SPEC-2-002 aceita; implementação da Fase 2 completa)

- [champion] Task F2-IMP-009 concluída (9/9 da implementação da Fase 2): veredito **ACEITO** do Champion (Karol e Márcio) registrado via consultor Ricardo Junior em 21/09/2026 — **SPEC-2-002 encerrada**. Consolidação v0.0.77 (a3c644b): migração 0047 (6 fixtures sintéticas em todos os estados + 4 usuários temporários) e 24/24 provas ao vivo via API (CA-2.06..CA-2.10); pacote de evidências em 06_notas/aceites/pacote-evidencias-spec-2-002.md e roteiro do Champion em 06_notas/aceites/roteiro-teste-champion-spec-2-002.md.
- [debug r1] Cenário 2 do teste humano falhou (card exibia "Assumida por você" para o caso assumido pelo Consultor A após troca de usuário na mesma montagem) — causa raiz: `myUserId` capturado em useState no mount; correção v0.0.78 (0bffd92) lendo o authStore no render; fixtures de reteste na migração 0048; prova no navegador reproduzindo a falha exata. Aprendizado AP-2026-09-21-1515.
- [debug r2] Reteste ainda exibia o sintoma — investigação provou servidor íntegro (trilha com actor correto), bundle v0.0.78 servido com a correção e comportamento correto em navegador novo; causa: cache do navegador executando o bundle anterior (mesmo padrão da F2-IMP-008 r2). Nenhuma mudança de código. Aprendizado AP-2026-09-21-1725.
- [teste humano] Aprovado pelo consultor em 21/09/2026 — "Passo 2 ok após o hard refresh" (passos 1, 3, 4 e 5 aprovados na rodada anterior); cenário 5 validado com a fixture dedicada e o roteiro ajustado (durante o rollback o botão de assunção some por design — bloqueio server-side provado via API).
- [verificação] Revalidação independente de fechamento (do zero, v0.0.79): 19/19 provas refazeitas — visibilidade por papel sem vazamento, trilha ASSUMED com actor correto nos dois casos, reprocessamento recusado 400, ações negadas 403/400, controle da fila ativo e negado a consultor, rotas / /agendar /fila /visao 200.
- [limpeza pós-aceite] Migração 0049 (v0.0.79, 23f7e39): 9 fixtures da consolidação/reteste, 4 usuários sintéticos e eventos de controle removidos; logins sintéticos retornam 400; fila ativa; fixtures-base 0001..0004 preservadas.
- [limite] Nenhuma publicação em produção, nenhuma integração externa, nenhum dado real. Pendências de decisão consciente registradas no STATUS (LGPD, RN-2.06, capacidade 2 no sábado, continuidade triagem→agendamento, fortalecimento do CA-2.03). O gate Fase 2 → Fase 3 exige reconciliação do handoff/manifesto e liberação formal do Champion.

## 2026-09-21 — Debug r2 F2-IMP-009 (sintoma persistiu no reteste — bundle antigo em cache)

- [consultor] Reteste (21/09/2026): passos 1, 3, 4 e 5 ok; passo 2 ainda exibia "Assumida por você" após trocar para o Consultor B (screenshot anexado ao relato).
- [investigação] Servidor íntegro: trilha de eventos mostra APPOINTMENT_ASSUMED único com actor `z5wgyiffrdnv028` (Consultor A, 14:07:40) e dono correto no registro; o bundle servido no preview (`index-B7eLHk-R.js`, v0.0.78) contém a correção e não contém o marcador antigo (`setMyUserId`); prova em navegador novo (sem cache) exibiu o comportamento correto.
- [causa raiz] Cache do navegador: a aba do teste continuou executando o bundle da v0.0.77 — mesmo padrão do reteste da F2-IMP-008 r2, resolvido com Ctrl+F5. Nenhuma mudança de produto nesta rodada.
- [procedimento] Reteste do passo 2 com Ctrl+F5 (hard refresh) após entrar com o Consultor B; se persistir, capturar screenshot com o console aberto.
- [limite] Nenhuma publicação em produção; nenhum código alterado nesta rodada.

## 2026-09-21 — Debug r1 F2-IMP-009 (dono exibido errado após troca de usuário na /visao)

- [consultor] Teste humano da consolidação (21/09/2026): cenários 1, 3 e 4 OK; cenário 2 falhou — ao sair do Consultor A e entrar com o Consultor B (na mesma montagem da página), o card assumido pelo A exibia "Assumida por você" e o "responsável anterior" do B aparecia como ID cru; cenário 5 parcial (o roteiro pedia assunção durante o rollback, mas a UI esconde o botão por design — o bloqueio server-side já estava provado via API).
- [causa raiz] `myUserId` era estado React capturado no mount (e na assunção); login/logout na mesma montagem não remonta a página e a comparação `dono === myUserId` ficava obsoleta — mesma família do debug da F2-IMP-007 r1 (authStore lido fora do momento do render/ação).
- [correção] v0.0.78 (`0bffd92`): a identidade passa a ser lida do authStore no render (`myUserId` derivado, sem useState); migração 0048 criou fixtures de reteste (caso assumido pelo Consultor A + 2 casos sem dono, incluindo um dedicado ao cenário 5). Pipeline QA completo OK.
- [verificação] Prova no navegador reproduzindo a falha exata: Consultor A → Sair → Consultor B sem recarregar a página — o card do A agora exibe "Assumida por z5wgyiffrdnv028" (ID correto, não "você") e o card reatribuído ao B exibe "por você" + responsável anterior corretos.
- [limite] Reteste humano do cenário 2 e do cenário 5 (com a fixture "Lead Reteste Rollback r1") volta ao pendente; nenhuma publicação em produção.

## 2026-09-21 — Debug r2 F2-IMP-008 (exibição do responsável anterior)

- [consultor] Reteste do passo 4 (21/09/2026): a reatribuição funcionou (dono → `lljzgyj2w6rimak`, `responsavel_anterior` preservado no banco, eventos ASSUMED + REASSIGNED na trilha), mas o card da `/visao` não exibia o responsável anterior.
- [causa raiz] A UI tinha o campo no tipo (`responsavel_anterior?`) e o dado gravado no servidor, porém nenhum elemento renderizava — o histórico da reatribuição era preservado, mas invisível na operação (F1-T005 exige histórico preservado).
- [correção] v0.0.75 (`6b9f0f1`): o card passa a exibir "Reatribuída — responsável anterior: …" quando `responsavel_anterior` existir. Pipeline QA completo OK.
- [limite] Reteste do passo 4 volta ao pendente; nenhuma publicação em produção.

## 2026-09-21 — Debug r1 F2-IMP-008 (reatribuição após assunção)

- [consultor] Teste humano do Ricardo (21/09/2026): passos 1–3 e 5–7 OK; passo 4 (Reatribuir) falhou com "Caso já assumido — a reatribuição deve usar a ação formal da Gestão." — evidência em screenshot.
- [causa raiz] A rota atômica grava a flag formal `queue_operation` (campo oculto) e o hook `protect_assumption` não a enxergava durante o save no JSVM — a reatribuição formal era bloqueada como troca direta de dono. A prova de 18/09 não expôs o defeito porque a fixture 0045 estava sem dono (caminho que não passa pelo guarda); o caso já assumido é o único que o aciona.
- [correção] v0.0.74 (`feae808`): o hook passa a reconhecer também a impressão digital da rota formal (`responsavel_anterior` = dono anterior, campo visível e blindado contra PATCH). Pipeline QA completo OK.
- [verificação] Provas ao vivo: caso assumido pela Gestão → Supervisora reatribuiu (HTTP 200), dono passou a `lljzgyj2w6rimak`, `responsavel_anterior` preservou o dono anterior, status manteve `ENCAMINHAMENTO_HUMANO`, eventos ASSUMED + REASSIGNED na trilha; PATCH direto de dono segue bloqueado (403).
- [limite] Teste humano volta ao pendente para reteste do passo 4; nenhuma publicação em produção.

## 2026-09-18 — Fechamento F2-IMP-007 (permissões, fila e assunção de tentativas)

- [consultor] Task F2-IMP-007 concluída (7/9 da implementação da Fase 2): teste humano aprovado pelo consultor em 18/09/2026 ("Testei e funcionou") — assunção na /visao com dono e hora exibidos no card e bloqueio do papel sem permissão confirmados.
- [verificação] Revalidação independente no fechamento (do zero, v0.0.71): 7/7 provas refazeitas — papel gestao lê 0 itens (sem vazamento), consultor lê a fila (200), troca de dono em caso assumido recusada 400, remoção de dono recusada 400, update sem tocar no dono 200 (estado preservado), eventos APPOINTMENT_ASSUMED na trilha (incluindo os das assumções do teste humano com actor correto), páginas / /agendar /visao 200.
- [debug registrado] Sessão de teste do reteste: a fixture 007 foi assumida nas provas via API e o hook (corretamente) não permite desfazer — reteste humano criou a 007b (0039); no reteste os 3 primeiros eventos APPOINTMENT_ASSUMED saíram com actor_id vazio (authStore lido de estado capturado no mount, vazio porque o login acontece na mesma página sem remount) — corrigido lendo o authStore no momento do clique; assumções finais com actor correto. Documentado em 06_notas/debug/.
- [limpeza pós-aceite] Migração 0040 aplicou-se como no-op silencioso ($app é global de hooks, não de migrações — o try/catch engoliu o erro); corrigida pela 0041 (v0.0.71) com o parâmetro `app` e log de remoções: usuários sintéticos fila.teste@ e marketing.teste@ removidos (login recusado 400 — senhas provisórias deixam de existir), tentativas 007/007b e seus eventos removidos; preservadas as fixtures 0001..0004, o evento APPOINTMENT_ASSUMED da 0004 e o valor 'gestao' no select role (necessário na F2-IMP-008). Aprendizado capturado em 06_notas/aprendizado-continuo/AP-2026-09-18-0940-migracao-jsvm-app-parametro.md.
- [limite] Reatribuição, escalada visual, encerramento e rollback são a F2-IMP-008 (próxima elegível); a restrição de leitura por atribuição (consultor vê só o dele) entra na F2-IMP-008. Nenhuma publicação em produção, nenhum dado real.

## 2026-09-17 — Implementação F2-IMP-007 (permissões, fila e assunção de tentativas)

- [champion via consultoria] Task F2-IMP-007 implementada (autorização do consultor Ricardo: "vamos prosseguir"): botão **"Assumir caso"** na `/visao` (Skip 51806, v0.0.66) — visível apenas em tentativas `ENCAMINHAMENTO_HUMANO` sem dono (fila única da F2-T004: primeiro consultor disponível assume); a assunção registra `dono` + `assumed_at` (gravados pelo servidor) + evento `APPOINTMENT_ASSUMED` na trilha; o card mostra "Assumida por você em …" ou "Sem dono — disponível para assunção". Migração 0035 (campos dono/assumed_at/responsavel_anterior + tipo de evento), hook `protect_assumption.js` (defesa em profundidade), 0036 (usuário sem permissão), 0037 (tentativa de teste sem dono), 0038 (usuário consultor de teste).
- [verificação] Pipeline QA completo passou. Provas ao vivo: CA-2.07 — assunção via API gravou dono e assumed_at com status preservado em ENCAMINHAMENTO_HUMANO (RN-2.08) e evento na trilha; CA-2.09 — troca de dono em caso já assumido recusada (HTTP 400 "Caso já assumido — a reatribuição é feita pela Gestão (F2-IMP-008)"), remoção de dono recusada (400), papel `gestao` bloqueado na leitura e na escrita (regra da coleção responde 404 — sem vazamento: 0 itens visíveis), tentativa de update com papel não autorizado não muda estado.
- [nota técnica] O campo `role` da coleção users é um select com valores fixos — o papel 'marketing' da matriz F2-T004 é inválido no select atual; a migração 0036 expandiu o select com 'gestao' (Subgerente/Gestão), que nesta task não tem permissão de assunção (reatribuição/escalada são a F2-IMP-008) e serve para a prova negativa. O valor 'gestao' permanece no select para a próxima task.
- [limite] Reatribuição, escalada visual e rollback são a F2-IMP-008; a restrição de leitura por atribuição (consultor vê só o dele) entra na F2-IMP-008 junto da escalada. Nenhuma publicação em produção, nenhum dado real. Usuários sintéticos de teste criados (0036/0038) e serão removidos após o aceite.

## 2026-09-17 — Fechamento F2-IMP-006 (visão operacional de tentativas)

- [consultor] Task F2-IMP-006 concluída (6/9 da implementação da Fase 2): teste humano aprovado pelo consultor em 17/09/2026 ("verificado") — a /visao mostra as 4 tentativas com filtros por estado e contadores corretos, contexto da triagem completo (objetivo, proximidade, ocupação, interesse, origem/campanha), motivo do encaminhamento em destaque e modal de contexto completo; sem botões de ação (leitura — assunção é a F2-IMP-007).
- [verificação] Revalidação final (v0.0.59): 4 fixtures com contexto completo, grade 248 slots, /visao /agendar e / respondendo 200; usuário sintético da visão removido após o aceite (0034) — login recusado (HTTP 400), senha provisória deixa de existir.
- [debug registrado] Sessão órfã: a /visao abria "logada" com token em cache de usuário já removido (lista vazia, estado fantasma) — corrigido com validação da sessão no bootstrap (authRefresh); a página agora limpa a sessão inválida e exige login, nunca fingindo autenticação. Correção aprovada no mesmo teste humano.
- [limite] Visão somente leitura; assunção (dono/assumed_at) e permissões negativas são a F2-IMP-007; escalada e rollback a F2-IMP-008. Nenhuma publicação em produção, nenhum dado real. Próxima task elegível: F2-IMP-007 — exige novo ciclo de análise + autorização explícita.

## 2026-09-17 — Implementação F2-IMP-006 (visão operacional de tentativas)

- [champion via consultoria] Task F2-IMP-006 implementada (autorização do consultor Ricardo: "vamos prosseguir"): nova página `/visao` no Skip 51806 (v0.0.57) — visão operacional de tentativas com login autenticado (padrão da /fila), lista com filtros por estado (Todos/TENTATIVA/CONCLUIDO/DESISTENCIA/ENCAMINHAMENTO_HUMANO com contadores), cards com nome, canal, horário, objetivo e origem/campanha, destaque do motivo do encaminhamento e modal "Ver contexto completo" (contexto da triagem + dados do agendamento + versão do formulário). Rota registrada em App.tsx.
- [contexto da triagem] Migração 0029 adicionou os campos de contexto em `lead_appointments` (objetivo, proximidade, ocupacao, interesse_em_visita, utm_source/medium/campaign, attribution_status); hook de servidor copia o contexto da `lead_submissions` para o appointment no momento da criação (lead_submissions é superuser-only — o contexto viaja com o registro, padrão da fila F1); migração 0030 semeou o contexto nas 4 fixtures; migração 0031 provou a herança ao vivo (submission sintética → appointment criado herdou objetivo, proximidade, ocupação, interesse, UTMs e attribution completos); 0032 removeu os registros da prova.
- [verificação] Pipeline QA completo passou. Provas ao vivo: CA-2.06 — as 4 fixtures aparecem com contexto completo na coleção e na página; CA-2.08 — recriar um `appointment_id` existente é recusado pelo índice único (HTTP 400, "Value must be unique" — reprocessamento não duplica); páginas /visao, /agendar e / HTTP 200; usuário sintético de teste (0033) faz login e lê as 4 tentativas.
- [nota técnica] `new Field(nome, tipo, max)` posicional falha no JSVM ("could not convert [object Object] to core.Field"); a forma correta é `new Field({ name, type, max })` — 2 builds falhos até a causa (v0.0.50→v0.0.52).
- [limite] Visão somente leitura — nenhum botão de assumir/atualizar estado (assunção e permissões negativas são a F2-IMP-007; escalada e rollback a F2-IMP-008); a visão não conclui tentativa (RN-2.09); sem integração externa, sem publicação em produção, sem dado real. Usuário sintético de teste criado (0033) para o teste humano e removido após o aceite (0034).

## 2026-09-17 — Fechamento F2-IMP-005 (veredito ACEITO — SPEC-2-001 aceita)

- [champion] Task F2-IMP-005 concluída (5/9 da implementação da Fase 2): veredito **ACEITO** do Champion (Karol e Márcio) registrado via consultor Ricardo Junior ("aceito") em 17/09/2026 — **SPEC-2-001 encerrada**.
- [verificação] Revalidação independente no fechamento (do zero, v0.0.48): CA-2.01 campos completos na fixture e na criação pela página; CA-2.02 fechadura ativa (2ª reserva 200, 3ª recusada 400); CA-2.04 eventos preservados (CREATED+CONCLUDED+ABANDONED) e vaga liberada; CA-2.05 fallback com handoff_reason; páginas / e /agendar 200; ambiente limpo — 4 fixtures, 248 slots, 0 ocupados (migrações 0024–0026 removeram os registros dos testes do Champion).
- [achado do consultor] Continuidade triagem → agendamento registrada como pendência #4: botão "Agende aqui" no painel lateral da triagem; lead redigita nome/canal na /agendar; agendamento não herda o lead_submission_id da triagem (vínculo hoje apenas estrutural). Decisão do Champion pendente: aceitar como está, mover o botão para o final do fluxo e/ou implementar a passagem de contexto.
- [limite] Nenhum código de produto alterado nesta task (apenas documentos de aceite e migrações de limpeza de dados de teste). Nenhuma publicação em produção. Próxima task elegível: F2-IMP-006 (visão operacional, SPEC-2-002) — exige novo ciclo de análise + autorização explícita.

## 2026-09-17 — Implementação F2-IMP-005 (consolidação e aceite da SPEC-2-001)

- [champion via consultoria] Task F2-IMP-005 implementada (autorização do consultor Ricardo: "vamos prosseguir"): pacote de evidências sanitizadas da SPEC-2-001 publicado em `06_notas/aceites/pacote-evidencias-spec-2-001.md` — CA-2.01..CA-2.05 com provas executadas (dados 100% sintéticos, v0.0.45), provas de segurança transversais e pendências destacadas; roteiro de teste do Champion publicado em `06_notas/aceites/roteiro-teste-champion-spec-2-001.md` — 5 cenários no preview (reserva válida, limite de vagas, campos obrigatórios, desistência, fallback humano); recibo de aceite aberto no `04_fase-atual/fase.md` com veredito pendente.
- [observação registrada] CA-2.03 é cumprido no fluxo do lead (página); via API direta o servidor ainda não rejeita CONCLUIDO sem campos mínimos — registrada como recomendação de fortalecimento pós-aceite (nova task, novo ciclo), não bloqueia o aceite.
- [teste humano] 5/5 cenários do roteiro cumpridos em 17/09/2026: cenários 1, 2, 3 e 5 executados pelo Champion via consultor (reserva válida com código, horário some ao esgotar, bloqueio de campos obrigatórios, fallback humano); cenário 4 (desistência) provado pelo operador via API conforme o roteiro previa — PATCH DESISTENCIA 200, evento ABANDONED, 3 eventos preservados, contador 2→1 (a tela de desistência é escopo da SPEC-2-002, F2-IMP-006/007).
- [limite] Nenhum código, migração ou configuração do Skip foi alterada nesta task; apenas documentos de aceite. Nenhuma publicação em produção.

## 2026-09-17 — Fechamento F2-IMP-004 (conflito, idempotência, desistência e rollback)

- [consultor] Task F2-IMP-004 concluída (4/9 da implementação da Fase 2): teste humano aprovado pelo consultor em 17/09/2026 ("testado e funcionou") após duas rodadas de debug — a fechadura de capacidade por slot está ativa no servidor (hook `enforce_slot_capacity.js` em `lead_appointments` create/update/delete) e na página `/agendar` (esconde slot cheio, mostra vagas restantes, bloqueia clique).
- [verificação] Revalidação final 5/5 (v0.0.45): apenas as 4 fixtures sintéticas na base, 0 slots ocupados, grade intacta (248 slots), /agendar e triagem respondendo 200; fechadura reprovada ativa após a limpeza (reserva em slot vazio aceita, slot cheio recusada com HTTP 400).
- [segurança] Migrações 0022/0023 removeram todas as reservas dos testes humanos e provas (deleteRule null provado novamente: DELETE via API recusado com HTTP 403); nenhuma senha ou credencial registrada; usuário sintético de verificação permanece para o ciclo de fechamento e será removido no próximo aceite.
- [limite] Nenhuma publicação em produção, nenhuma integração externa, nenhum dado real. Pendências para a call de setup: LGPD (base legal do agendamento), RN-2.06 e capacidade 2 no sábado. Próxima task elegível: F2-IMP-005 (aceite final da SPEC-2-001 pelo Champion), que exige novo ciclo de análise + autorização explícita.

## 2026-09-17 — DEBUG F2-IMP-004 (rodada 2) — fechadura de capacidade no servidor

- [consultor] DEBUG task F2-IMP-004 (rodada 2): reteste humano reproduziu a falha — a página escondia slot cheio, mas o contador de ocupação nunca era atualizado por nenhuma camada e o servidor aceitava reservas acima da capacidade via API direta; consultor também reportou que era possível agendar mais de uma pessoa nos demais horários → causa raiz: filtro cosmético na página sem enforcement no servidor → **corrigido** com hook `enforce_slot_capacity.js` em `lead_appointments` (create/update/delete): conta as reservas ativas (CONCLUIDO+TENTATIVA) do slot, rejeita acima da capacidade com HTTP 400 "Este horário acabou de encher. Escolha outro, por favor." e mantém `agenda_slot_occupancy` sincronizada após cada escrita; migração 0021 ressincronizou todos os contadores e limpou as provas (v0.0.43). Provas ao vivo: 1ª e 2ª reservas aceitas em slot cap 2 (HTTP 200/200), 3ª recusada (400), desistência libera a vaga (PATCH 200 + nova reserva 200, contador 2/2), cenário exato do reteste (slot 1200 com 3 ativas) reproduzido e recusado sem criar registro. Gate: aguardando 2º reteste humano.
- [nota técnica] O guardrail do Skip rejeitou a primeira versão do hook (v0.0.41): callbacks do JSVM executam em pool separado e não enxergam declarações de topo — toda a lógica foi movida para dentro de cada callback. Fixture antiga apontando para slot inexistente fazia a capacidade cair no default 1 — recusa "correta" por motivo errado, detectada e contornada nas provas.

## 2026-09-17 — DEBUG F2-IMP-004 (rodada 1) — capacidade por slot

- [consultor] DEBUG task F2-IMP-004: teste humano reproduziu falha real — slot com "2 vagas" aceitava 3+ reservas (o índice único só impede o MESMO lead no MESMO slot; nenhuma camada contava a ocupação) → causa raiz: ausência de controle de capacidade por slot (RN-2.01/CA-2.02 sem enforcement); a prova de conflito da task usava slot cap 1, onde o índice disfarçava o limite → **corrigido** em 3 camadas: migração 0018 criou `agenda_slot_occupancy` (ocupação por slot, recalculada, leitura pública, escrita só champion/consultor); página /agendar esconde slot cheio, mostra vagas restantes e bloqueia clique; migrações 0019/0020 limparam as reservas de teste (deleteRule null provado: API recusou DELETE com HTTP 403 — correto). Ambiente limpo: 248 slots, 4 fixtures, ocupação zerada (v0.0.40). Nota técnica: campo number `required` no PocketBase rejeita 0 ("Cannot be blank") — 3 builds falhos até a causa; corrigido sem `required` (0 é estado válido). Gate: aguardando reteste humano.

## 2026-09-17 — Implementação F2-IMP-003

- [champion via consultoria] Task F2-IMP-003 concluída: seleção e conclusão do agendamento implementadas no Skip 51806 (v0.0.26) — nova página `/agendar` com fluxo de 3 passos: grade de slots ABERTO agrupada por dia (com selo "2 vagas" na janela 11:30–16:30), formulário dos campos mínimos aprovados (nome, telefone/canal, localidade residencial/comercial, profissão; e-mail opcional) e confirmação com código de reserva. Rota registrada em App.tsx e link "Prefere escolher um horário? Agende aqui" adicionado à tela da triagem.
- [verificação] Pipeline QA completo passou. Provas ao vivo: 248 slots ABERTO carregados pela página; tentativa válida criada e concluída (CONCLUIDO com concluded_at e evento APPOINTMENT_CONCLUDED); fallback RN-2.05 provado (ENCAMINHAMENTO_HUMANO com handoff_reason, sem confirmação falsa); reescolha de slot RN-2.06 provada (a mesma tentativa é atualizada com o novo slot — 1 registro, sem duplicar); página /agendar responde HTTP 200 no preview.
- [teste humano] Aprovado pelo consultor em 17/09/2026 ("teste realizado e funcionou") — fluxo completo percorrido no preview: escolha de horário, bloqueio de confirmação sem campos, confirmação com dados e fallback para atendimento humano.
- [segurança] Usuário sintético de verificação criado (0014) para conferir as provas de leitura e removido após o aceite (0015); senha provisória deixou de existir. Revalidação final: página HTTP 200, grade intacta (248 slots), acesso de teste recusado, endpoint de tentativas sem vazamento anônimo.
- [limite] Sem mensagem externa, sem CRM, sem agenda externa, sem publicação em produção, sem dado real. A prova de concorrência simultânea real é a F2-IMP-004.

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