# Decisões humanas da Fase 3

Preencher uma seção por vez. Uma seção pendente, incompleta ou sem confirmação verificável não libera implementação.

## B3-01 — Taxonomia de origem e campanha
- **Status:** CONCLUÍDA — 2026-09-24
- **Decisor:** Champion do cliente — Karol
- **Decisão:**
  - `utm_source`: manter cada fonte separada.
  - `utm_medium`: manter cada valor separado.
  - `utm_campaign`: usar de maneira agrupada por campanha.
  - valores ausentes ou não reconhecidos: cada valor fica em seu próprio grupo.
  - granularidade: campanha, conforme agrupamento definido acima.
- **Data/confirmação verificável:** 24/09/2026 — Karol: “Karol confirma, libere as tasks”; regra complementar confirmada no chat: “mantenha cada valor separado”.

## B3-02 — Fórmula e janela da métrica norte
- **Status:** CONCLUÍDA — 2026-09-24
- **Decisor:** Champion do cliente — Karol
- **Decisão:**
  - **Numerador:** contar os agendamentos concluídos no período.
  - **Denominador:** contar os encaminhamentos humanos no mesmo período.
  - **Janela temporal padrão:** últimos 30 dias corridos.
  - **Fórmula:** agendamentos concluídos no período ÷ encaminhamentos humanos no mesmo período.
  - **Meta:** não definida nesta decisão; nenhuma meta foi inferida.
  - **Escopo:** definição documental da métrica norte; nenhuma métrica, configuração ou produto foi alterado nesta task.
- **Data/confirmação verificável:** 24/09/2026 — Karol: “Karol confirma, libere as tasks”.

## B3-03 — Vínculo entre triagem e agendamento
- **Status:** CONCLUÍDA — 2026-09-24
- **Decisor:** Champion do cliente — Karol
- **Decisão:**
  - **Tratamento aprovado:** preservar o vínculo da triagem no fluxo de agendamento.
  - **Regra complementar:** nenhuma.
  - O agendamento deverá manter o `lead_submission_id` da triagem de origem, em vez de criar ou aceitar automaticamente um vínculo substituto quando a continuidade estiver disponível.
  - Se um agendamento permanecer sem `lead_submission_id`, ele deve continuar visível como cobertura incompleta e não pode ser atribuído à triagem por inferência.
  - **Escopo:** decisão documental do tratamento do vínculo; nenhuma alteração de código, banco, configuração, integração ou produto foi realizada nesta task.
- **Data/confirmação verificável:** 24/09/2026 — Karol: “Karol confirma, libere as tasks”.

## B3-04 — Matriz de acesso ao dashboard
- **Status:** CONCLUÍDA — 2026-09-29
- **Decisor:** Champion do cliente — Karol
- **Decisão:**
  - **Podem ler o dashboard agregado:** Champion, Gestão, Supervisora e Subgerente.
  - **Não podem ler o dashboard:** Marketing/agência e Consultor.
  - Marketing/agência não tem acesso ao dashboard; esta decisão é mais restritiva do que somente ocultar contatos individuais. O dashboard não deve expor contatos ou registros individuais.
  - A permissão de escrita/criação/correção/congelamento de baseline continua restrita ao Champion, conforme a SPEC; esta decisão define leitura e não altera essa regra.
- **Data/confirmação verificável:** 29/09/2026, 11:44 — confirmação atribuída a Karol e transmitida por Ricardo Junior no histórico desta conversa. Citação fornecida: “matriz correta e autorizada, não podem ler: marketing e consultor, os demais, autorizado”. “Os demais” corresponde aos papéis permitidos explicitados no contexto desta decisão: Champion, Gestão, Supervisora e Subgerente.
- **Escopo:** registro documental da decisão. Esta atualização, isoladamente, não alterou permissões de runtime, código, configuração ou publicação.

## B3-05 — Critério de congelamento do baseline
- **Status:** PENDENTE
- **Decisor:** Champion do cliente
- **Decisão:** [preencher quando e como congelar/versionar/interpretar]
- **Data/confirmação verificável:** [preencher]
