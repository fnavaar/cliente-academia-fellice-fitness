# Fase 2 — Tarefas

<!-- fase-format:2 -->

> A Fase 2 tem duas levas: desbloqueios documentais já concluídos e implementação do autoagendamento/visão operacional ainda não iniciada. F2-IMP-001 é a única task elegível. Tasks novas entram sem UUID; o sincronizador/portal deve gerar os IDs.

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

- [ ] Preparar o contrato técnico e as fixtures de agenda @"Karol e Márcio" #projeto
  > F2-IMP-001 / SPEC-2-001. Critérios: modelo cobre slot, capacidade, tentativa, estados, vínculo com triagem e idempotência; fixtures sintéticas cobrem caminho válido, campos ausentes, indisponibilidade, desistência e encaminhamento. Evidência: migration/modelo revisável, schema sanitizado, fixtures e RED/GREEN inicial. Pré-condições: F2-T001..T003 concluídas. Leva 2. Ponto de parada: qualquer regra/arquitetura não definida ou dado real. Estado final: contrato e fixtures prontos em teste, sem slot real. **Única task elegível.**
- [ ] Configurar a grade de disponibilidade em ambiente de teste @"Karol e Márcio" #projeto
  > F2-IMP-002 / SPEC-2-001. Critérios: slot 30 min; capacidade 1 e exceção 2 entre 11:30–16:30; grade seg–sex 08:00–19:30 e sáb 09:00–13:30; manutenção limitada aos papéis decididos. Evidência: criar/editar/bloquear/reabrir fixture e rollback. Pré-condição: F2-IMP-001 aceita e teste humano. Leva 3. Ponto de parada: exposição pública ou grade de produção. Estado final: grade sintética controlável e não publicada.
- [ ] Implementar a seleção e conclusão do agendamento @"Karol e Márcio" #projeto
  > F2-IMP-003 / SPEC-2-001. Critérios: slots abertos visíveis; appointment vinculado à triagem; nome, telefone/canal, localidade e profissão exigidos; e-mail opcional; conclusão somente com campos mínimos; fallback sem confirmação falsa. Evidência: fixtures válida/incompleta e estados observáveis. Pré-condição: F2-IMP-002 aceita. Leva 4. Ponto de parada: mensagem externa, CRM ou agenda externa. Estado final: fluxo sintético de tentativa implementado no teste.
- [ ] Provar conflito, idempotência, desistência e rollback da agenda @"Karol e Márcio" #projeto
  > F2-IMP-004 / SPEC-2-001. Critérios: concorrência deixa no máximo uma confirmação; reprocessamento não duplica; desistência preserva eventos/libera capacidade; falha/timeout/sem slots encaminha; rollback preserva histórico. Evidência: roteiro RED/GREEN/regressão com IDs sintéticos. Pré-condição: F2-IMP-003 aceita. Leva 5. Estado final: bordas da agenda demonstradas em teste.
- [ ] Consolidar o TDD e aceitar a agenda de teste @"Karol e Márcio" #projeto
  > F2-IMP-005 / SPEC-2-001. Critérios: CA-2.01..CA-2.05 demonstrados; evidências sanitizadas; preview pronto para teste do Champion. Evidência: RED/GREEN/regressão, recibo e aceite humano. Pré-condição: F2-IMP-004 aceita. Leva 6. Ponto de parada: reprovação mantém a task aberta e encaminha debug. Estado final: SPEC-2-001 aceita ou reprovada explicitamente.
- [ ] Criar a visão operacional de tentativas @"Karol e Márcio" #projeto
  > F2-IMP-006 / SPEC-2-002. Critérios: visão mostra estado, contexto da triagem, origem, versão e horário; reprocessamento atualiza sem duplicar; visão não conclui por conta própria; falha conserva estado anterior. Evidência: lista/detalhe, fixtures e trilha de eventos; rota acessível no preview. Pré-condição: F2-IMP-005 aceita. Leva 7. Estado final: visão interna funcional em teste, sem publicação.
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

## Marco da Fase 2 (2026-09-16)

- **5/5 tasks de desbloqueio concluídas** — todos os bloqueios documentais das SPEC-2-001 e SPEC-2-002 estão resolvidos.
- **Implementação não iniciada:** nenhuma slot, agenda, visão, conta, permissão ou publicação foi criada no Skip.
- **Próxima etapa possível:** implementação da agenda de disponibilidade (SPEC-2-001) e da visão operacional (SPEC-2-002), em novo ciclo, com análise, autorização explícita e teste humano. Nada nesta documentação autoriza publicação de produção.
