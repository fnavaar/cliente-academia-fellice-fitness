# Fase 2 — Tarefas gerais

> Leva 1: tarefas de desbloqueio autorizadas. Elas não criam slot, agenda, conta, conector ou publicação; registram as decisões humanas exigidas pelas SPECs. São independentes entre si.

## Tasks

| ID | Task | Dono | SPEC | Critério | Subseção da SPEC | Recorte da prova | Evidência esperada | Pré-condições | Ponto de parada | Status |
|---|---|---|---|---|---|---|---|---|---|---|
| F2-T001 | Registrar duração do slot, capacidade por horário e grade inicial de dias/horários | Subgerente Comercial | SPEC-2-001 | Duração em minutos, capacidade máxima por slot e tabela de dias/horários disponíveis estão registrados e aprovados pelo Subgerente. | `## BLOQUEIOS executáveis` (duração, capacidade e grade) | Conferência documental do primeiro bloqueio da SPEC-2-001; nenhum slot ou agenda é criado. | Subgerente tem a decisão de grade e capacidade operacional. | Pare se duração, capacidade ou grade não forem informados; não inventar horários nem duração padrão. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-09-16 |
| F2-T002 | Registrar responsável por manter e fechar a agenda | Champion do cliente | SPEC-2-001 | Nome do papel e usuário responsável pela agenda estão registrados e aprovados pelo Champion. | `## BLOQUEIOS executáveis` (responsável da agenda) | Conferência documental do segundo bloqueio da SPEC-2-001; nenhuma permissão é concedida. | Champion tem a decisão sobre quem gerencia a disponibilidade. | Pare se papel ou usuário não forem informados; não apontar usuário sem aprovação explícita. | bloqueada — aguarda decisão humana | ✅ concluída — 2026-09-16 |
| F2-T003 | Registrar campos mínimos obrigatórios para conclusão do agendamento | Liderança Comercial | SPEC-2-001 | Tabela de campos obrigatórios para que uma tentativa transite para `CONCLUIDO` está aprovada e registrada. | `## BLOQUEIOS executáveis` (contrato de campos mínimos) | Conferência documental do terceiro bloqueio da SPEC-2-001; nenhum campo é configurado na plataforma. | Liderança Comercial fornece as escolhas aprovadas. | Pare se qualquer campo obrigatório ou critério de conclusão estiver ausente ou ambíguo; não inventar campo mínimo. | bloqueada — aguarda decisão humana | pendente |
| F2-T004 | Registrar papéis, permissões e regra de encaminhamento para humano | Champion + Liderança Comercial | SPEC-2-002 | Matriz de leitura/escrita por papel (Consultor, Subgerente, Gestão, Champion) e regra de atribuição inicial para tentativas em `ENCAMINHAMENTO_HUMANO` estão registradas e aprovadas. | `## BLOQUEIOS executáveis` (papéis e regra de encaminhamento) | Conferência documental do primeiro e segundo bloqueios da SPEC-2-002; nenhuma permissão é concedida na plataforma. | Champion e liderança Comercial fornecem as decisões de acesso e encaminhamento. | Pare se qualquer papel, permissão ou regra de atribuição estiver ausente; não conceder acesso por inferência. | bloqueada — aguarda decisão humana | pendente |
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
