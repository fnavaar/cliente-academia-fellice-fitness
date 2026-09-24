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
- **Status:** PENDENTE
- **Decisor:** Champion do cliente
- **Decisão:** [preencher tratamento de agendamentos sem lead_submission_id]
- **Data/confirmação verificável:** [preencher]

## B3-04 — Matriz de acesso ao dashboard
- **Status:** PENDENTE
- **Decisor:** Champion do cliente
- **Decisão:** [preencher papéis de leitura; Marketing não acessa contatos individuais]
- **Data/confirmação verificável:** [preencher]

## B3-05 — Critério de congelamento do baseline
- **Status:** PENDENTE
- **Decisor:** Champion do cliente
- **Decisão:** [preencher quando e como congelar/versionar/interpretar]
- **Data/confirmação verificável:** [preencher]
