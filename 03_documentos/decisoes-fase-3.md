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
- **Status:** DECISÃO REGISTRADA — 2026-09-29
- **Decisor:** Champion do cliente — Karol
- **Decisão:**
  - **Período do baseline:** mês civil completo, do primeiro ao último dia do mês, no fuso local da unidade (`America/Bahia`). A métrica norte definida em B3-02 permanece com janela móvel padrão dos últimos 30 dias corridos; o mês civil é específico do baseline e não altera a fórmula nem a janela padrão de B3-02.
  - **Quando congelar:** somente o Champion pode congelar a apuração do mês civil já completo mais recente. Congelar cria uma fotografia imutável com período, numerador, denominador, cobertura e versão. Nova apuração cria nova versão append-only; versões antigas não são sobrescritas.
  - **Cobertura de suficiência:** contar submissões do período que, simultaneamente, têm nome não vazio, um número de telefone reconhecível no campo `canal_de_retorno` e uma resposta de proximidade exatamente igual a “Moro no Itaigara ou em bairros vizinhos” ou “Trabalho na região do Itaigara”; dividir essa contagem pelo total de submissões do mesmo período. Os valores individuais não são retornados nem exibidos.
  - **Limiar:** cobertura de suficiência igual ou superior a 50% é suficiente. Abaixo de 50%, o Champion ainda pode salvar uma versão, que deve ser marcada claramente como `INSUFICIENTE`; a versão insuficiente não deve ser confundida com baseline de qualidade suficiente.
  - **Denominador zero:** permitir salvar a versão com estado explícito `NAO_CALCULAVEL`, taxa nula (não zero), preservando período, numerador, denominador zero, coberturas e versão. Se também houver baixa cobertura, registrar essa condição de cobertura separadamente.
  - **Sem submissões no mês:** cobertura de suficiência fica não calculável; se o denominador da métrica for zero, a versão fica marcada `NAO_CALCULAVEL` e preserva os contadores disponíveis, sem inventar taxa.
  - **Fórmula e escopo:** nome, telefone e proximidade servem somente para medir cobertura/suficiência e marcar o estado da versão. Não filtram numerador ou denominador nem alteram a fórmula aprovada em B3-02. Sem meta, causalidade ou ação de campanha inferida.
  - **Integridade da fonte:** se uma fonte necessária estiver indisponível ou houver leitura parcial, não congelar a apuração incompleta; permitir estado insuficiente é para dados lidos por completo que não atingem o limiar de cobertura.
- **Data/confirmação verificável:** 29/09/2026 — confirmação atribuída a Karol e transmitida por Ricardo Junior nesta conversa: “Karol - 29/09/2026 - decisões confirmadas e autorizadas”. A mensagem também confirmou explicitamente mês civil do baseline sem mudar B3-02, limiar 50%, campos mínimos, salvamento como insuficiente e estado não calculável para denominador zero.
- **Escopo:** decisão registrada para orientar implementação na task `124f370f`; registro documental não afirma por si só que a regra já esteja aplicada no runtime.
