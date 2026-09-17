# Fase 2 — Tarefas

<!-- fase-format:2 -->

> A Fase 2 tem duas levas: desbloqueios documentais concluídos em 2026-09-16 e a implementação do autoagendamento/visão operacional em curso — F2-IMP-001..F2-IMP-004 concluídas com aceite humano em 2026-09-17; F2-IMP-005 concluída em 2026-09-17 com veredito ACEITO do Champion — **SPEC-2-001 aceita**; F2-IMP-006 concluída em 2026-09-17 com teste humano aprovado; F2-IMP-007 é a próxima elegível.

## Tasks documentais concluídas

- [x] Registrar a grade inicial da agenda @"Karol e Márcio" #projeto
  > F2-T001 / SPEC-2-001. Critério: duração, capacidade e grade inicial registradas. Evidência: decisão do Subgerente registrada em 16/09/2026. Pré-condição: decisão humana recebida. Leva 1 documental. Estado final: regras disponíveis para implementação; nenhum slot criado.
- [x] Registrar o responsável pela agenda @"Karol e Márcio" #projeto
  > F2-T002 / SPEC-2-001. Critério: papel e usuários responsáveis registrados. Evidência: decisão do Champion registrada em 16/09/2026. Pré-condição: aprovação do Champion. Leva 1 documental. Estado final: responsável definido; nenhuma permissão concedida.
- [x] Registrar os campos mínimos do agendamento @"Karol e Márcio" #projeto
  > F2-T003 / SPEC-2-001. Critério: nome, telefone/canal, localidade e profissão obrigatórios; e-mail opcional. Evidência: decisão da Liderança Comercial registrada em 16/09/2026. Pré-condição: decisão humana recebida. Leva 1 documental. Estado final: contrato de campos definido; nenhum campo configurado.
- [x] Registrar permissões e encaminhamento humano @"Karol e Márcio" #projeto
  > F2-T004 / SPEC-2-002. Critério: matriz de acesso e fila única registradas. Evidência: decisões do Champion e da Liderança Comercial registradas em 16/09/2026. Pré-condição: decisões humanas recebidas. Leva 1 documental. Estado final: regras disponíveis para implementação; nenhuma permissão concedida.
- [x] Registrar a escalada de tentativas paradas @"Karol e Márcio" #projeto
  > F2-T005 / SPEC-2-002. Critério: Gestão/Subgerente + Supervisora Mel, parada no fim do turno, reatribuição ou encerramento com motivo. Evidência: decisão da Liderança Comercial registrada em 16/09/2026. Pré-condição: decisão humana recebida. Leva 1 documental. Estado final: regra disponível para implementação; nenhuma automação criada.

## Tasks de implementação — novo ciclo

- [x] Preparar o contrato técnico e as fixtures de agenda @"Karol e Márcio" #projeto
  > F2-IMP-001 / SPEC-2-001. Critérios: modelo cobre slot, capacidade, tentativa, estados, vínculo com triagem e idempotência; fixtures sintéticas cobrem caminho válido, campos ausentes, indisponibilidade, desistência e encaminhamento. Evidência: migrações 0007 (coleções agenda_slots, lead_appointments, lead_appointment_events) e 0008 (seed sintético) no Skip 51806 v0.0.20; pipeline QA completo ok; provas ao vivo — duplicata recusada (HTTP 400, índice único lead_submission_id+slot_id), criação pública aceita, leitura anônima sem vazamento, leitura autenticada com 6 tentativas/4 eventos; contrato técnico revisado e aprovado; teste humano do consultor aprovado em 17/09/2026 ("entrei e testado, está aparecendo. tudo ok, aprovado"); usuário sintético de teste removido após validação (0010). Pré-condições: F2-T001..T003 concluídas. Leva 2. Estado final: contrato e fixtures prontos em teste, sem slot real, sem publicação.
- [x] Configurar a grade de disponibilidade em ambiente de teste @"Karol e Márcio" #projeto
  > F2-IMP-002 / SPEC-2-001. Critérios: slot 30 min; capacidade 1 e exceção 2 entre 11:30–16:30; grade seg–sex 08:00–19:30 e sáb 09:00–13:30; manutenção limitada aos papéis decididos. Evidência: migração 0011 no Skip 51806 v0.0.23 gerou 248 slots sintéticos (14 dias; seg–sex 23 blocos 08:00–19:00, sáb 9 blocos 09:00–13:00; capacidade 2 nos blocos que começam entre 11:30 e 16:30 exatos — interpretação corrigida pelo consultor em 17/09/2026, 11 blocos/dia útil; capacidade 2 também nos 8 blocos de sábado dentro da janela [VALIDAR NA CALL DE SETUP]); ciclo de vida provado via API com usuário sintético temporário — criar, editar capacidade, bloquear, reabrir e apagar ok; sem login não cria slot (HTTP 400); fixtures antigas removidas; rollback cirúrgico por created_by='grade-teste'; teste humano do consultor aprovado em 17/09/2026 ("funcionou" — grade conferida via API e login do papel de agenda validado na /fila); usuário sintético removido após validação (0013). Pré-condição: F2-IMP-001 aceita e teste humano. Leva 3. Estado final: grade sintética controlável e não publicada.
- [x] Implementar a seleção e conclusão do agendamento @"Karol e Márcio" #projeto
  > F2-IMP-003 / SPEC-2-001. Critérios: slots abertos visíveis; appointment vinculado à triagem; nome, telefone/canal, localidade e profissão exigidos; e-mail opcional; conclusão somente com campos mínimos; fallback sem confirmação falsa. Evidência: página /agendar criada no Skip 51806 v0.0.26 (grade agrupada por dia com selo "2 vagas" → formulário de campos mínimos → confirmação com código de reserva), rota registrada em App.tsx e link "Prefere escolher um horário? Agende aqui" na triagem; pipeline QA completo ok; provas ao vivo — 248 slots ABERTO carregados, tentativa válida → CONCLUIDO com concluded_at e evento APPOINTMENT_CONCLUDED, fallback ENCAMINHAMENTO_HUMANO com handoff_reason, reescolha de slot atualiza a mesma tentativa sem duplicar (RN-2.06), página HTTP 200 no preview; teste humano do consultor aprovado em 17/09/2026 ("teste realizado e funcionou" — fluxo completo percorrido no preview); usuário de verificação removido após aceite (0015). Pré-condição: F2-IMP-002 aceita. Leva 4. Estado final: fluxo sintético de tentativa implementado no teste, sem mensagem externa, sem CRM, sem agenda externa.
- [x] Provar conflito, idempotência, desistência e rollback da agenda @"Karol e Márcio" #projeto
  > F2-IMP-004 / SPEC-2-001. Critérios: concorrência deixa no máximo uma confirmação; reprocessamento não duplica; desistência preserva eventos/libera capacidade; falha/timeout/sem slots encaminha; rollback preserva histórico. Evidência: fechadura de capacidade no servidor (hook enforce_slot_capacity.js em create/update/delete + contador agenda_slot_occupancy sincronizado) e na página /agendar (esconde slot cheio, mostra vagas restantes); 2 rodadas de debug documentadas em 06_notas/debug/ (debug-2026-09-17-capacidade-por-slot.md); provas ao vivo — 2 reservas aceitas em slot cap 2 (HTTP 200/200), 3ª recusada (HTTP 400), desistência libera vaga, rollback preserva histórico, DELETE via API recusado (403); teste humano aprovado em 17/09/2026 ("testado e funcionou") após 2 rodadas de debug; ambiente limpo (v0.0.45: 4 fixtures, 248 slots, 0 ocupados). Pré-condição: F2-IMP-003 aceita. Leva 5. Estado final: bordas da agenda demonstradas em teste. **Concluída.**
- [x] Consolidar o TDD e aceitar a agenda de teste @"Karol e Márcio" #projeto
  > F2-IMP-005 / SPEC-2-001. Critérios: CA-2.01..CA-2.05 demonstrados; evidências sanitizadas; preview pronto para teste do Champion. Evidência: pacote de evidências publicado em 06_notas/aceites/pacote-evidencias-spec-2-001.md (CA-2.01..CA-2.05 com provas executadas, dados 100% sintéticos) e roteiro de teste do Champion em 06_notas/aceites/roteiro-teste-champion-spec-2-001.md (5 cenários no preview); recibo de aceite neste arquivo. Pré-condição: F2-IMP-004 aceita. Leva 6. Ponto de parada: reprovação mantém a task aberta e encaminha debug. Teste humano: 5/5 cenários — cenários 1, 2, 3 e 5 executados pelo Champion via consultor em 17/09/2026 (todos passaram); cenário 4 (desistência) provado pelo operador via API conforme o próprio roteiro previa (PATCH DESISTENCIA 200, evento ABANDONED, 3 eventos preservados, contador 2→1) — a tela de desistência é escopo da SPEC-2-002 (F2-IMP-006/007). Veredito do Champion: **ACEITO** (2026-09-17, via consultor Ricardo Junior). Revalidação independente no fechamento: CA-2.01 campos completos, CA-2.02 fechadura ativa (200/200/400), CA-2.04 eventos preservados, CA-2.05 fallback ok, páginas 200, ambiente limpo (v0.0.48: 4 fixtures, 248 slots, 0 ocupados). **SPEC-2-001 aceita.**
- [x] Criar a visão operacional de tentativas @"Karol e Márcio" #projeto
  > F2-IMP-006 / SPEC-2-002. Critérios: visão mostra estado, contexto da triagem, origem, versão e horário; reprocessamento atualiza sem duplicar; visão não conclui por conta própria; falha conserva estado anterior. Evidência: página /visao no Skip 51806 v0.0.59 (login autenticado, lista com filtros por estado e contadores, cards com objetivo/origem/horário, motivo do encaminhamento em destaque, modal "Ver contexto completo" com contexto da triagem + dados do agendamento + versão do formulário); campos de contexto em lead_appointments (0029) preenchidos nas fixtures (0030); hook copia o contexto da triagem no create (prova 0031: herança completa triagem→appointment); CA-2.08 provado (recriação de appointment_id recusada 400 — reprocessamento não duplica); debug de sessão órfã corrigido (bootstrap valida com authRefresh — página nunca finge autenticação); teste humano do consultor aprovado em 17/09/2026 ("verificado" — 4 tentativas, filtros corretos, contexto completo, sem botões de ação); usuário sintético removido após aceite (0034). Pré-condição: F2-IMP-005 aceita. Leva 7. Estado final: visão de leitura funcional em teste — assunção/permissões são a F2-IMP-007; sem publicação.
- [ ] Aplicar permissões, fila e assunção de tentativas @"Karol e Márcio" #projeto
  > F2-IMP-007 / SPEC-2-002. Critérios: Consultor limitado; Subgerente/Gestão veem todos; Champion configura; Marketing não vê dados individuais; primeiro Consultor assume; dono, assumed_at e motivo são registrados; não autorizado não altera. Evidência: usuários sintéticos autorizado/não autorizado e auditoria. Pré-condição: F2-IMP-006 aceita. Leva 8. Estado final: RBAC e fila demonstrados em teste.
- [ ] Implementar a escalada visual e o rollback da fila @"Karol e Márcio" #projeto
  > F2-IMP-008 / SPEC-2-002. Critérios: parada até o fim do turno sinaliza; Gestão/Subgerente/Supervisora Mel reatribuem ou encerram com motivo; nenhum estado muda automaticamente; rollback preserva registros. Evidência: turnos sintéticos, parada, sinalização, reatribuição, encerramento e rollback. Pré-condição: F2-IMP-007 aceita. Leva 9. Estado final: escalada demonstrada sem automação indevida.
- [ ] Consolidar o TDD e aceitar a visão operacional @"Karol e Márcio" #projeto
  > F2-IMP-009 / SPEC-2-002. Critérios: CA-2.06..CA-2.10 demonstrados; permissões negativas, reprocessamento, assunção, escalada e rollback evidenciados; Champion aprova ou reprova. Evidência: pacote sanitizado e recibo humano. Pré-condição: F2-IMP-008 aceita. Leva 10. Estado final: SPEC-2-002 aceita ou reprovada explicitamente; Fase 2 ainda não avança sem liberação formal.

## Gate Fase 2 → Fase 3

A Fase 3 só pode ser considerada depois que F2-IMP-001..F2-IMP-009 forem concluídas com evidências e aceites humanos, CA-2.01..CA-2.10 forem demonstrados e o handoff/manifesto estiver reconciliado. Este arquivo não autoriza abertura da Fase 3.

## Decisão registrada — F2-T001 (2026-09-16)

- **Duração do slot:** 30 minutos
- **Capacidade padrão por slot:** 1 atendimento simultâneo
- **Grade inicial:**
  - Segunda a sexta: das 08:00 às 19:30
  - Sábado: das 09:00 às 13:30
- **Exceção de capacidade:** nos horários das 11:30 às 16:30, a operação suporta 2 atendimentos simultâneos
- **Aprovado por:** Subgerente Comercial (decisão informada via consultoria em 2026-09-16)
- **Limite:** registro documental apenas — nenhum slot, agenda, conta ou publicação foi criado no Skip

## Decisão registrada — F2-T002 (2026-09-16)

- **Papel responsável por manter e fechar a agenda:** Consultor Comercial
- **Usuários que exercem o papel:** Camila, Jaqueline e Rodrigo (turnos manhã, tarde e noite, conforme F1-T002)
- **Podem também exercer o papel:** Subgerente Comercial e Champion
- **Aprovado por:** Champion (decisão informada via consultoria em 2026-09-16)
- **Nota de fronteira:** esta decisão cobre a manutenção da agenda de disponibilidade (bloquear slots, adicionar datas, aprovar publicação da grade). A publicação de versões do aplicativo permanece regida pela matriz da F1-T006 (apenas Champion publica); a eventual concessão de acesso de escrita à configuração de agenda na plataforma será tratada na fase de implementação, com autorização própria do Champion.
- **Limite:** registro documental apenas — nenhuma permissão, conta ou configuração foi criada no Skip

## Decisão registrada — F2-T003 (2026-09-16)

**Contrato de campos mínimos para a tentativa transitar de `TENTATIVA` para `CONCLUIDO`:**

| Ordem | Campo | Obrigatório? | Observação |
|---|---|---|---|
| 1º | `nome` (nome do lead) | Sim | Sem nome, a tentativa não vira `CONCLUIDO` |
| 2º | `telefone_ou_canal_de_retorno` | Sim | Sem retorno, a operação não consegue confirmar a visita |
| 3º | `localidade` (residencial ou comercial, o que for mais perto da sede) | Sim | Campo adicional aprovado pela Liderança Comercial; o lead informa qual endereço (residencial ou comercial) está mais perto da academia |
| 4º | `profissao` | Sim | Campo adicional aprovado pela Liderança Comercial |
| 5º | `email` | Não — opcional | Coletado apenas se o lead quiser informar |

- **Justificativa registrada pela Liderança Comercial:** "Nosso lead potencial mora ou trabalha próximo a nossa empresa" — a localidade e a profissão qualificam a proximidade do lead em relação à academia.
- **Vínculos e estados:** `appointment_id`, `lead_submission_id`, `form_id`, `form_version`, `slot_id`, `slot_datetime`, `slot_duration_min`, `status`, `conflict_detected`, `created_at`, `concluded_at` e `handoff_reason` seguem o contrato da SPEC-2-001 e não são objeto de decisão nesta task.
- **Regra aplicável:** campos obrigatórios ausentes impedem a transição para `CONCLUIDO` (RN-2.03 / CA-2.03); a tentativa permanece em `TENTATIVA` até correção ou desistência.
- **LGPD:** os campos obrigatórios entram sob o consentimento aprovado na F1-T004; o e-mail, por ser opcional, só é coletado com fornecimento voluntário do lead.
- **Aprovado por:** Liderança Comercial (decisão informada via consultoria em 2026-09-16)
- **Limite:** registro documental apenas — nenhum campo foi configurado no Skip; a implementação do formulário de agendamento ocorre na fase de implementação, com autorização própria.

## Decisão registrada — F2-T004 (2026-09-16)

**Matriz de permissões da visão operacional de tentativas (aprovada pelo Champion):**

| Papel | Ler | Atualizar estado | Reatribuir | Sinalizar escalada |
|---|---|---|---|---|
| Consultor Comercial | Tentativas atribuídas a ele ou em `ENCAMINHAMENTO_HUMANO` (mínimo da SPEC) | Sim — tentativas atribuídas a ele | **Sim** — dentro da visão operacional | — |
| Subgerente Comercial / Gestão | Todos os estados (mínimo da SPEC) | **Sim** — editar estado de tentativas | — | **Sim** — sinalizar escalada de tentativa parada |
| Champion | Tudo — configura e consulta (mínimo da SPEC) | Configura a visão | — | — |
| Marketing | **Não** — sem acesso a dados de contato individuais nem tentativas individuais (mínimo da SPEC) | Não | Não | Não |

- Células com "—" não foram objeto de decisão nesta task; onde a SPEC-2-002 já fixa o mínimo, o mínimo prevalece.

**Regra de encaminhamento para humano (aprovada pela Liderança Comercial):**

- **Atribuição inicial:** fila única — a tentativa entra em `ENCAMINHAMENTO_HUMANO` sem dono fixo e é assumida pelo primeiro consultor disponível; a assunção registra dono e `assumed_at` (RN-2.08).
- **Motivo do encaminhamento:** catálogo fixo (ex.: sem horário disponível, falha de sistema, dúvida) + campo livre complementar.
- **Estado de destino:** `ENCAMINHAMENTO_HUMANO` (já fixado pela SPEC-2-002).

**Notas de fronteira:**

- A permissão de reatribuição do Consultor vale para a **visão operacional da Fase 2** (SPEC-2-002). A matriz da F1-T006 continua regendo a **fila de encaminhamento humano da Fase 1** (SPEC-1-002), onde o Consultor não reatribui nem publica. Divergência entre superfícies registrada deliberadamente pelo Champion.
- A edição de estado por Subgerente/Gestão não substitui a transição para `CONCLUIDO`, que vem exclusivamente da SPEC-2-001 (RN-2.09).
- A sinalização de escalada pelo Subgerente/Gestão é permissão da matriz; o **critério de parada** e o **responsável por encerrar/reatribuir tentativas paradas** seguem pendentes na F2-T005 (terceiro bloqueio da SPEC-2-002).
- **Aprovado por:** Champion (matriz de permissões) e Liderança Comercial (regra de encaminhamento) — decisões informadas via consultoria em 2026-09-16.
- **Limite:** registro documental apenas — nenhuma permissão, conta ou configuração foi criada no Skip.

## Decisão registrada — F2-T005 (2026-09-16)

**Escalada de tentativas paradas (aprovada pela Liderança Comercial):**

| Item | Decisão |
|---|---|
| Papel responsável pela escalada | **Gestão/Subgerente Comercial + Supervisora Comercial (Mel)** |
| Critério de parada | Tentativa em `ENCAMINHAMENTO_HUMANO` **sem ação até o fim do turno de origem** (turnos conforme F1-T002: manhã, tarde, noite) |
| Poderes do responsável | **Ambos** — reatribuir a outro consultor **ou** encerrar com motivo obrigatório |

- **Coerência com a matriz da F2-T004:** o papel decidido encaixa na permissão já registrada — Subgerente/Gestão sinalizam escalada e agora também respondem por ela; a Supervisora Comercial (Mel), que na F1-T002 acompanha toda a equipe, integra o papel de escalada.
- **Coerência com F1-T005:** reatribuição e encerramento permanecem nas mãos de liderança (Gestão/Subgerente/Supervisora), como na Fase 1; a fronteira entre superfícies (fila da Fase 1 × visão da Fase 2) segue a nota da F2-T004.
- **Sem ação automática:** o critério de parada alimenta **sinalização visual** para o responsável (RN-2.10); nenhum estado muda automaticamente. O encerramento exige motivo obrigatório, coerente com RN-2.09 e F1-T005.
- **Aprovado por:** Liderança Comercial (decisão informada via consultoria em 2026-09-16)
- **Limite:** registro documental apenas — nenhuma regra de escalada foi configurada no Skip; a implementação da sinalização ocorre na fase de implementação, com autorização própria.

## Recibo de aceite — SPEC-2-001 (aberto em 2026-09-17)

- **Task:** F2-IMP-005 — Consolidar o TDD e aceitar a agenda de teste.
- **Pacote de evidências:** `06_notas/aceites/pacote-evidencias-spec-2-001.md` (CA-2.01..CA-2.05 com provas executadas; dados 100% sintéticos).
- **Roteiro de teste do Champion:** `06_notas/aceites/roteiro-teste-champion-spec-2-001.md` (5 cenários no preview, 10–15 min).
- **Veredito do Champion (Karol e Márcio):** ✅ **ACEITO** — 2026-09-17, registrado via consultor Ricardo Junior ("aceito"), após 5/5 cenários do roteiro cumpridos (cenário 4 provado pelo operador via API, conforme roteiro).
- **Pendências destacadas para decisão consciente:** LGPD (base legal do agendamento), RN-2.06 (semântica de reagendamento), capacidade 2 no sábado e continuidade triagem → agendamento (achado do consultor em 17/09: botão "Agende aqui" no painel lateral; lead redigita nome/canal na /agendar; agendamento não herda o lead_submission_id da triagem — critério "appointment vinculado à triagem" é hoje apenas estrutural).
- **Ponto de parada:** reprovação mantém a task aberta e encaminha debug; aceite encerra a SPEC-2-001 e libera F2-IMP-006.

## Marco da Fase 2 (2026-09-16)

- **5/5 tasks de desbloqueio concluídas** — todos os bloqueios documentais das SPEC-2-001 e SPEC-2-002 estão resolvidos.
- **Implementação não iniciada:** nenhuma slot, agenda, visão, conta, permissão ou publicação foi criada no Skip.
- **Próxima etapa possível:** implementação da agenda de disponibilidade (SPEC-2-001) e da visão operacional (SPEC-2-002), em novo ciclo, com análise, autorização explícita e teste humano. Nada nesta documentação autoriza publicação de produção.
