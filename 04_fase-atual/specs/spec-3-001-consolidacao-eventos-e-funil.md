# SPEC-3-001 — Consolidação de eventos e funil de conversão rastreável

**Fase:** 3  
**Status:** implementação concluída e validada no preview v0.0.81; revisão formal de aceite pendente na task `4217198c-8077-4769-b2c0-7b7482136553`; produção não publicada.  
**Dono:** Champion do cliente (decisor dos bloqueios); Marketing/agência e Gestão podem ser consultados  
**Origem:** D-003, RQ-008 e Fase 3 do escopo definitivo  
**Degrau:** recurso nativo da plataforma de pré-agendamento, somente leitura, sem Kommo, Lóvavel ou fontes externas.

## Contexto e resultado

Os eventos das fases 1 e 2 já existem: submissões de triagem, encaminhamentos, tentativas de agendamento e trilha operacional. Ainda não existe consolidação. O resultado desejado é um funil único com entrada, início, conclusão da triagem, encaminhamento humano e agendamento concluído, sempre com período, numerador, denominador e cobertura de atribuição visíveis.

## BLOQUEIOS executáveis

| Bloqueio | Dono | Evidência para liberar |
|---|---|---|
| B3-01 — taxonomia de `utm_source`, `utm_medium`, `utm_campaign` e granularidade | Champion; Marketing/Gestão podem consultar | Decisão, data e confirmação verificável no `03_documentos/decisoes-fase-3.md` |
| B3-02 — numerador, denominador e janela da métrica norte | Champion; Gestão pode consultar | Decisão, data e confirmação verificável no registro canônico |
| B3-03 — tratamento do vínculo triagem → agendamento sem `lead_submission_id` | Champion | Decisão, data e confirmação verificável no registro canônico |

Nenhum GREEN começa com um bloqueio pendente. Não atribuir agendamentos por inferência.

## Limites, dados e permissões

Inclui consolidação somente leitura, funil por período, contagem de registros sem atribuição, contagem de agendamentos sem vínculo e recálculo determinístico. Ficam fora receita, matrícula, comparecimento, causalidade, integração de escrita, mensagens, alteração dos eventos originais e painel individual.

A fonte é a plataforma de pré-agendamento (`lead_submissions`, encaminhamentos, `lead_appointments` e eventos). Marketing e Gestão consultam agregados; nenhum papel recebe contatos individuais por esta SPEC. Falha de leitura marca o período como parcial e nunca apresenta taxa incompleta como completa.

Regras: todo indicador tem numerador, denominador e período; registros sem atribuição continuam visíveis; agendamento sem vínculo é cobertura incompleta; reagendamento/reprocessamento não duplica `appointment_id`; rollback desativa a consolidação sem apagar eventos.

## Fluxo de execução

1. Champion registra B3-01, B3-02 e B3-03.
2. Executor cria consolidação somente leitura com fixtures sintéticas das quatro coleções.
3. Prova contagens, cobertura, ausência de atribuição, ausência de vínculo, determinismo e rollback.
4. Obtém teste humano e aceite antes de qualquer publicação.

Estado válido enquanto bloqueado: nenhuma consolidação, dado real ou integração externa alterada; funil não publicado.

## Critérios de aceite

- **CA-3.01:** etapas de entrada, início, conclusão da triagem, encaminhamento e agendamento concluído aparecem por período.
- **CA-3.02:** toda taxa mostra numerador, denominador e período; sem esses três não há indicador.
- **CA-3.03:** registros sem `attribution_status` permanecem visíveis e entram na cobertura.
- **CA-3.04:** agendamento concluído sem submissão vinculada aparece como cobertura incompleta, sem atribuição inventada.
- **CA-3.05:** o mesmo período recalcula igual; reagendamento e reprocessamento não geram dupla contagem.

## TDD da SPEC

- **RED:** montagem manual demonstra que não há funil consolidado.
- **GREEN:** fixtures sintéticas com atribuição completa/parcial/ausente e todos os estados produzem contagens conferíveis, taxas e cobertura.
- **REGRESSÃO:** recalcular, reagendar, interromper leitura e executar rollback; resultado determinístico, sem duplicata, com período parcial sinalizado e eventos preservados.

Evidências exigidas: capturas do ambiente de teste, conferência de contagens contra fixtures, export sanitizado, logs de rollback e aceite humano. Nunca usar dados reais antes do gate.

## Tasks vinculadas

| ID | Task | Critério | Pré-condição |
|---|---|---|---|
| `45bb5d1b-b757-4d29-9afa-cee4d0077552` | Definir taxonomia | B3-01 registrado | Champion decide |
| `2ce9c4fb-c143-4519-ba1f-e0ce80807e9b` | Definir fórmula/janela | B3-02 registrado | Champion decide |
| `bcc00bba-0eb4-4821-9ccf-b74755969f43` | Decidir vínculo | B3-03 registrado | Champion decide |
| `ab9ce40f-304e-4ef6-929f-1efa7f7a0a87` | Consolidar funil | CA-3.01..05 | B3-01..03 completos |
| `4217198c-8077-4769-b2c0-7b7482136553` | Revisar aceite | CA-3.01..05 | implementação concluída |

**Gate antes do GREEN:** B3-01, B3-02 e B3-03 preenchidos com data e confirmação verificável.
