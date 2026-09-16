# Fase 2 — Tarefas gerais

> Leva 1: tarefas de desbloqueio autorizadas. Elas não criam slot, agenda, conta, conector ou publicação; registram as decisões humanas exigidas pelas SPECs. São independentes entre si.

## Tasks

| ID | Task | Dono | SPEC | Critério | Subseção da SPEC | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Status |
|---|---|---|---|---|---|---|---|---|---|---|
| F2-T001 | Registrar duração do slot, capacidade por horário e grade inicial de dias/horários | Subgerente Comercial | SPEC-2-001 | Duração em minutos, capacidade máxima por slot e tabela de dias/horários disponíveis estão registrados e aprovados pelo Subgerente. | `## BLOQUEIOS executáveis` (duração, capacidade e grade) | Conferência documental do primeiro bloqueio da SPEC-2-001; nenhum slot ou agenda é criado. | Subgerente tem a decisão de grade e capacidade operacional. | Pare se duração, capacidade ou grade não forem informados; não inventar horários nem duração padrão. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-09-16 |
| F2-T002 | Registrar responsável por manter e fechar a agenda | Champion do cliente | SPEC-2-001 | Nome do papel e usuário responsável pela agenda estão registrados e aprovados pelo Champion. | `## BLOQUEIOS executáveis` (responsável da agenda) | Conferência documental do segundo bloqueio da SPEC-2-001; nenhuma permissão é concedida. | Champion tem a decisão sobre quem gerencia a disponibilidade. | Pare se papel ou usuário não forem informados; não apontar usuário sem aprovação explícita. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-09-16 |
| F2-T003 | Registrar campos mínimos obrigatórios para conclusão do agendamento | Liderança Comercial | SPEC-2-001 | Tabela de campos obrigatórios para que uma tentativa transite para `CONCLUIDO` está aprovada e registrada. | `## BLOQUEIOS executáveis` (contrato de campos mínimos) | Conferência documental do terceiro bloqueio da SPEC-2-001; nenhum campo é configurado na plataforma. | Liderança Comercial fornece as escolhas aprovadas. | Pare se qualquer campo obrigatório ou critério de conclusão estiver ausente ou ambíguo; não inventar campo mínimo. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-09-16 |
| F2-T004 | Registrar papéis, permissões e regra de encaminhamento para humano | Champion + Liderança Comercial | SPEC-2-002 | Matriz de leitura/escrita por papel (Consultor, Subgerente, Gestão, Champion) e regra de atribuição inicial para tentativas em `ENCAMINHAMENTO_HUMANO` estão registradas e aprovadas. | `## BLOQUEIOS executáveis` (papéis e regra de encaminhamento) | Conferência documental do primeiro e segundo bloqueios da SPEC-2-002; nenhuma permissão é concedida na plataforma. | Champion e liderança Comercial fornecem as decisões de acesso e encaminhamento. | Pare se qualquer papel, permissão ou regra de atribuição estiver ausente; não conceder acesso por inferência. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-09-16 |
| F2-T005 | Registrar responsável por encerrar ou reatribuir tentativas paradas | Liderança Comercial | SPEC-2-002 | Papel responsável pela escalada e critério de parada estão registrados e aprovados pela liderança Comercial. | `## BLOQUEIOS executáveis` (escalada e encerramento) | Conferência documental do terceiro bloqueio da SPEC-2-002; nenhum estado é configurado na plataforma. | Liderança Comercial fornece o papel e o critério de parada. | Pare se papel de escalada ou critério de parada não forem informados; não definir prazo automático. | bloqueada — aguarda decisão humana | pendente |

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
