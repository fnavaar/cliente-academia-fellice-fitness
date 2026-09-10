# SPEC-2-001 — Agenda de disponibilidade e reserva de horário

**Fase:** 2  
**Status:** bloqueada — configuração operacional pendente  
**Dono:** Subgerente Comercial, Champion do cliente e liderança Comercial  
**Origem no escopo:** D-001, D-003, RQ-005 e Fase 2 de `03-Projeto/02-Escopo-Definitivo.md`  
**Degrau da solução:** recurso nativo da plataforma de pré-agendamento — a disponibilidade é configurada manualmente pela operação; não integra agenda externa, Kommo, Lóvavel ou qualquer conector nesta fase.

## Contexto e decisões fechadas

- **Estado atual:** leads qualificados chegam ao encaminhamento humano ou permanecem sem caminho de autoagendamento; a confirmação de horário depende de contato manual. Fontes: `03-Projeto/requisitos.md` §RQ-005; `03-Projeto/02-Escopo-Definitivo.md` §§Fase 1 e Fase 2.
- **Estado desejado:** um lead que concluiu a triagem da SPEC-1-001 (ou que está em encaminhamento da SPEC-1-002) pode ver os horários disponíveis, selecionar um e criar uma tentativa de agendamento rastreável, sem dupla reserva e com os dados mínimos aprovados pelo Comercial.
- **Decisões já fechadas:** a disponibilidade é configurada manualmente pela operação até que uma integração de agenda seja validada na Fase 4; não há confirmação automática D-1/D-0 nesta fase; não há integração de escrita com CRM ou agenda externa; falha de agenda encaminha para atendimento humano.
- **Bloqueios:** duração do slot, capacidade por horário, horários e dias iniciais disponíveis, responsável por manter e fechar a agenda, e campos mínimos obrigatórios para conclusão do agendamento não estão documentados nas fontes. O Ethos deve preparar o roteiro de teste, mas deve parar antes de criar slots, configurar disponibilidade ou registrar qualquer tentativa real até esses itens serem registrados pelos responsáveis.

## BLOQUEIOS executáveis

| Informação necessária | Dono da decisão | Por que bloqueia | Evidência para liberar |
|---|---|---|---|
| Duração padrão do slot de visita e capacidade por horário (máximo de reservas simultâneas) | Subgerente Comercial | Sem duração e capacidade, o executor não pode criar slots sem inventar regras de disponibilidade. | Duração em minutos e número máximo de reservas por slot registrados e aprovados pelo Subgerente. |
| Horários e dias disponíveis iniciais (grade mínima de funcionamento) | Subgerente Comercial | Sem a grade inicial, não há slots para o lead selecionar e o agendamento não pode ser testado. | Tabela de dias e horários aprovada pelo Subgerente registrada no plano. |
| Responsável por manter e fechar a agenda (quem bloqueia slots, adiciona datas e aprova publicação) | Champion do cliente | Sem dono da agenda, mudanças de disponibilidade seriam aplicadas sem autorização. | Nome do papel e usuário responsável registrados e aprovados pelo Champion. |
| Campos mínimos obrigatórios para declarar agendamento concluído (dados de contato, horário, vínculo com triagem) | Liderança Comercial | Sem o contrato de campos mínimos, o sistema não pode distinguir tentativa incompleta de agendamento confirmado. | Tabela de campos obrigatórios aprovada pelo Comercial registrada no plano. |

## Resultado observável

Um lead que conclui a triagem vê os horários disponíveis, seleciona um e recebe um identificador de tentativa. A operação enxerga `appointment_id`, `lead_submission_id`, `form_id`, `form_version`, horário escolhido, estado da tentativa (`TENTATIVA`, `CONCLUIDO`, `DESISTENCIA`, `ENCAMINHAMENTO_HUMANO`), dados de contato mínimos aprovados e se houve conflito de reserva. Conflito de horário é informado ao lead e não sobrescreve uma reserva existente. Falha ou ausência de horário encaminha para atendimento humano sem apagar a tentativa.

Nesta fase, "agendamento concluído" significa tentativa com os campos mínimos preenchidos e horário reservado; não significa confirmação de presença, envio de mensagem ou registro no CRM.

## Limites e dependências

- **Inclui:** grade de disponibilidade configurada manualmente, criação de tentativa de agendamento, controle de dupla reserva, estados da tentativa, fallback para encaminhamento humano e rastreamento de eventos.
- **Fora de escopo:** integração com agenda externa (Google Calendar, Calendly etc.), escrita em Kommo/Lóvavel/Polisystem, confirmações automáticas D-1/D-0, envio de mensagem, IA, remarcação pós-agendamento e pós-visita.
- **Entradas e pré-condições:** SPEC-1-001 testada e com aceite humano; SPEC-1-002 testada; grade de disponibilidade, duração, capacidade, responsável e campos mínimos registrados pelos donos de decisão; ambiente de teste isolado com usuário de teste autorizado.
- **Saídas/artefatos:** tentativas de agendamento rastreáveis com estado e contexto completo da triagem, configuração de disponibilidade versionada e roteiro de evidências da SPEC.
- **Dependências e responsáveis:** Subgerente Comercial aprova grade e capacidade; Liderança Comercial aprova campos mínimos; Champion indica responsável da agenda e autoriza publicação; executor não ativa ou modifica disponibilidade sem aprovação; Consultor Comercial recebe tentativas em `ENCAMINHAMENTO_HUMANO` via SPEC-2-002.
- **Atores e permissões mínimas:** Lead pode ver disponibilidade e criar tentativa; Consultor Comercial lê tentativas encaminhadas (via SPEC-2-002); Subgerente/Gestão lê todos os estados; responsável da agenda configura e bloqueia slots; Marketing não acessa dados de contato individuais ou tentativas individuais.
- **Superfícies/arquivos/configurações afetadas:** configuração de disponibilidade na plataforma de pré-agendamento; este arquivo; `01-SPECs/00-INDICE.md`; `02-Plano_de_acao/02.Fase_2/00-Tasks_Gerais.md`; `matriz-de-rastreabilidade.md`.
- **Risco e plano B:** se a plataforma não suportar controle de capacidade por slot, configurar cada slot como unidade única e registrar a limitação na evidência; não simular disponibilidade inventada. Se a grade não estiver aprovada, manter o fluxo de encaminhamento humano da Fase 1 e não publicar a agenda.
- **Rollback ou reversão:** fechar todos os slots da grade de teste sem apagar tentativas já registradas; redirecionar novos leads ao fluxo de encaminhamento humano da SPEC-1-002 até a correção ser aprovada e publicada.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Lead → plataforma de pré-agendamento (tentativa) | Plataforma, nesta fase | `appointment_id`, `lead_submission_id`, `form_id`, `form_version`, `slot_id`, `slot_datetime`, `slot_duration_min`, `nome`, `telefone_ou_canal_de_retorno`, `status` (`TENTATIVA` → `CONCLUIDO` / `DESISTENCIA` / `ENCAMINHAMENTO_HUMANO`), `conflict_detected`, `created_at`, `concluded_at`, `handoff_reason` | Lead sem acesso administrativo; responsável da agenda configura disponibilidade; Subgerente/Gestão lê todos; Consultor lê somente encaminhamentos (via SPEC-2-002) | Reenvio do mesmo `lead_submission_id` para o mesmo slot atualiza `appointment_id` existente; não cria segunda tentativa no mesmo slot. | Conflito de reserva informa o lead e não confirma; campos mínimos ausentes impedem transição para `CONCLUIDO`; falha de salvamento mostra erro sem confirmar; slot indisponível redireciona para encaminhamento humano. |
| Grade de disponibilidade → plataforma | Plataforma | `slot_id`, `slot_datetime`, `slot_duration_min`, `capacity`, `status` (`ABERTO` / `RESERVADO` / `BLOQUEADO`) | Responsável da agenda e Champion | Grade alterada pelo responsável aprovado; mudança de capacidade não retroage a tentativas já concluídas | Slot sem capacidade retorna disponibilidade vazia; falha de leitura encaminha para atendimento humano |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-2.01 | Lead abre a tela de agendamento | Carregar somente slots com status `ABERTO` e capacidade disponível; não mostrar slots `RESERVADOS` ou `BLOQUEADOS` | Se não houver slots disponíveis, apresentar opção de encaminhamento humano | Escopo definitivo §4; Fase 2 |
| RN-2.02 | Lead seleciona um slot disponível | Criar `appointment_id` com estado `TENTATIVA`, vincular ao `lead_submission_id` e reservar o slot | Se o slot for preenchido por outra tentativa no intervalo, informar conflito e não confirmar | RQ-005; Fase 2 |
| RN-2.03 | Lead preenche os campos mínimos e confirma | Transitar para `CONCLUIDO`, registrar `concluded_at` e fechar a reserva | Campos obrigatórios ausentes impedem a transição; a tentativa permanece em `TENTATIVA` até correção ou desistência | RQ-005; liderança Comercial |
| RN-2.04 | Lead desiste antes de concluir | Registrar estado `DESISTENCIA`, preservar eventos; slot retorna para `ABERTO` se capacidade permitir | Desistência não apaga a tentativa; histórico permanece rastreável | Escopo definitivo §4; Fase 2 |
| RN-2.05 | Falha de sistema, timeout ou ausência de slots disponíveis | Criar ou atualizar tentativa com estado `ENCAMINHAMENTO_HUMANO` e `handoff_reason` preenchido; não confirmar agendamento | Encaminhamento humano aciona SPEC-2-002; tentativa não é apagada | Escopo definitivo, Fase 2 |
| RN-2.06 | Dois pedidos simultâneos para o mesmo slot | O sistema aceita apenas um; o segundo recebe conflito e não é confirmado | Registrar ambas as tentativas; a não confirmada fica em `TENTATIVA` aguardando nova seleção ou desistência | RQ-005; escopo definitivo §4 |

## Fluxo e regras

1. Lead conclui a triagem da SPEC-1-001 (ou está em retomada via SPEC-1-002) e acessa a tela de agendamento.
2. A plataforma carrega apenas slots com `status=ABERTO` e capacidade disponível; ausência de slots apresenta encaminhamento humano imediato.
3. Lead seleciona um slot; a plataforma cria `appointment_id` com estado `TENTATIVA` e reserva temporariamente o slot.
4. Lead preenche os campos mínimos obrigatórios aprovados pelo Comercial e confirma.
5. Se os campos forem válidos e o slot ainda estiver disponível, a tentativa transita para `CONCLUIDO` e a reserva é fechada.
6. Se o slot foi tomado por outra tentativa, a plataforma informa o conflito, mantém a tentativa em `TENTATIVA` e apresenta novos slots disponíveis ou encaminhamento humano.
7. Se o lead abandonar antes da conclusão, a tentativa registra `DESISTENCIA` e o slot retorna para `ABERTO`.
8. Falha de sistema, timeout ou ausência de slots transitam a tentativa para `ENCAMINHAMENTO_HUMANO`, acionando SPEC-2-002.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Slot disponível; campos mínimos preenchidos | Tentativa `CONCLUIDO` com horário, contexto e eventos | N/A |
| Conflito | Dois leads simultâneos no mesmo slot | Apenas um confirma; o outro recebe aviso e opções alternativas | Tentativa não confirmada permanece em `TENTATIVA` |
| Sem disponibilidade | Grade vazia ou sem capacidade | Apresentar encaminhamento humano; tentativa registrada com `ENCAMINHAMENTO_HUMANO` | Acionar SPEC-2-002 |
| Desistência | Lead abandona antes de concluir | Tentativa `DESISTENCIA`; slot liberado; histórico preservado | Consultor pode ver o contexto via SPEC-2-002 |
| Falha | Campos mínimos ausentes ou salvamento falha | Não transitar para `CONCLUIDO`; mostrar qual campo falta ou erro de sistema | Corrigir e reenviar; confirmar que apenas uma tentativa foi criada |
| Rollback | Grade com defeito após publicação | Fechar todos os slots; redirecionar novos para encaminhamento humano; preservar tentativas já concluídas | Abrir incidente; aguardar aprovação para nova publicação |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** `02-Escopo-Definitivo.md` §§3–6 (Fase 2), esta SPEC, `spec-1-001-captura-e-triagem-rastreavel.md`, `spec-1-002-encaminhamento-humano-com-contexto.md`, `requisitos.md` §RQ-005 e `check-escopo.md`.
2. **Alterar somente:** configuração de disponibilidade, tentativas de agendamento e estados no ambiente autorizado pelo Champion; índice e matriz deste plano.
3. **Não alterar:** Kommo, Lóvavel, Polisystem, Google Calendar, Calendly, campanhas, mensagens comerciais, permissões de outros sistemas ou dados históricos.
4. **Executar nesta ordem:** confirmar grade/duração/capacidade/responsável → criar grade de teste em ambiente isolado → configurar campos mínimos → executar TDD com dados sintéticos → testar conflito, desistência, fallback e rollback → obter aceite humano → publicar somente a versão aprovada.
5. **Parar e pedir validação quando:** duração, capacidade, grade ou responsável não estiverem registrados; qualquer ação exigir escrever em agenda externa, CRM ou enviar mensagem; conflito de reserva não for detectado de forma confiável; plataforma não suportar controle de capacidade por slot.
6. **Estado válido ao parar:** grade de teste isolada; nenhuma tentativa real registrada; nenhum sistema externo foi alterado; grade de produção não foi publicada.

## Checklist de execução

- [ ] Subgerente Comercial registrou duração do slot, capacidade por horário e grade inicial de dias/horários.
- [ ] Champion indicou o responsável por manter e fechar a agenda.
- [ ] Liderança Comercial aprovou os campos mínimos obrigatórios para `CONCLUIDO`.
- [ ] Ambiente de teste criado com grade sintética; nenhum dado real foi usado.
- [ ] Cenários principal, conflito, sem disponibilidade, desistência, falha e rollback foram exercitados.
- [ ] Duas tentativas simultâneas no mesmo slot foram testadas e apenas uma foi confirmada.
- [ ] Evidências foram anexadas sem expor dados pessoais reais.
- [ ] Aceite humano da versão de produção foi registrado antes de publicar.

## Critérios de aceite

- [ ] **CA-2.01:** Uma tentativa concluída guarda `appointment_id`, `lead_submission_id`, `slot_id`, `slot_datetime`, campos mínimos aprovados e estado `CONCLUIDO`.
- [ ] **CA-2.02:** Duas reservas simultâneas no mesmo slot resultam em apenas uma com estado `CONCLUIDO`; a outra recebe conflito e não é confirmada.
- [ ] **CA-2.03:** Ausência de campos mínimos impede transição para `CONCLUIDO`; a tentativa permanece rastreável.
- [ ] **CA-2.04:** Desistência registra `DESISTENCIA`, preserva o histórico da tentativa e libera o slot sem apagar eventos.
- [ ] **CA-2.05:** Falha, timeout ou ausência de slots resultam em estado `ENCAMINHAMENTO_HUMANO` com `handoff_reason` e acionam SPEC-2-002; nenhuma confirmação falsa é exibida.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Tentar concluir sem campos mínimos e sem slot disponível | No ambiente de teste, submeter tentativa incompleta e simular grade vazia | Sem `CONCLUIDO`; campo ausente é apontado; sem slots apresenta encaminhamento humano | Captura de tela e lista de tentativas de teste |
| GREEN | Processar fixture `lead_valido_slot_disponivel` | Preencher todos os campos obrigatórios com dados sintéticos e slot aberto | Uma tentativa `CONCLUIDO` com `appointment_id`, slot, contexto e eventos | Captura da confirmação e registro da tentativa |
| REFACTOR/REGRESSÃO | Testar conflito simultâneo, desistência, fallback e rollback | Duas tentativas no mesmo slot; abandonar antes de concluir; simular ausência de slots; desativar a grade | Conflito detectado, desistência preservada, encaminhamento acionado, grade desativada sem apagar histórico | Roteiro assinado pelo Champion e evidências do ambiente |

**Dados/fixtures:** usar somente dados sintéticos — `Lead Teste B`, telefone fictício, campos mínimos preenchidos/ausentes, slots sintéticos com capacidade 1 e 2; UTMs válidas ou ausentes.  
**Caminhos de erro obrigatórios:** campo obrigatório vazio, slot indisponível, conflito de reserva, desistência, falha de salvamento, grade vazia, rollback da grade e encaminhamento humano.  
**Evidência exigida:** capturas do ambiente de teste, export/visualização sem dados pessoais reais, `appointment_id`/`slot_id` e aceite humano antes da publicação.

## Handoff e operação

- **Como demonstrar:** processar fixtures válidos, com conflito, com desistência e sem slots; mostrar estados, `appointment_id`, contexto e eventos; desativar a grade em teste e confirmar que histórico não foi apagado; acionar SPEC-2-002 no cenário de encaminhamento.
- **Como operar depois:** responsável da agenda (indicado pelo Champion) mantém e fecha slots; Subgerente ou Gestão monitora estado das tentativas; Liderança Comercial revisa campos mínimos antes de cada mudança de versão; Champion aprova toda publicação.
- **Como monitorar:** volume de tentativas por estado (`TENTATIVA`, `CONCLUIDO`, `DESISTENCIA`, `ENCAMINHAMENTO_HUMANO`), conflitos detectados, slots abertos e capacidade restante; conversão para agendamento não é interpretada até a Fase 3.
- **Pendência conhecida:** grade inicial, duração, capacidade e responsável devem ser fornecidos antes da execução; isso não autoriza conexão com agenda externa ou publicação por inferência.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F2-T001 | Registrar duração do slot, capacidade por horário e grade inicial de dias/horários | Subgerente Comercial | SPEC-2-001 | Duração em minutos, capacidade máxima e tabela de dias/horários estão registrados e aprovados. | Primeiro bloqueio executável. | Tabela de grade com duração e capacidade aprovadas pelo Subgerente. | Decisão do Subgerente Comercial. | bloqueada — aguarda decisão humana |
| F2-T002 | Registrar responsável por manter e fechar a agenda | Champion do cliente | SPEC-2-001 | Nome do papel e usuário responsável pela agenda estão registrados e aprovados. | Segundo bloqueio executável. | Papel e usuário identificados e aprovados pelo Champion. | Decisão do Champion. | bloqueada — aguarda decisão humana |
| F2-T003 | Registrar campos mínimos obrigatórios para conclusão do agendamento | Liderança Comercial | SPEC-2-001 | Tabela de campos obrigatórios para `CONCLUIDO` está aprovada e registrada. | Terceiro bloqueio executável. | Tabela de campos aprovada pela liderança Comercial. | Decisão da liderança Comercial. | bloqueada — aguarda decisão humana |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
