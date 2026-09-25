# Fase 3 — Tarefas

<!-- fase-format:2 -->

Cada linha é uma tarefa da Jornada de Execução. **Tudo que cabe num card cabe nesta linha** — se um
campo não estiver aqui, ele não tem como ser preenchido, porque é este arquivo que cria a tarefa.

```
- [ ] Título da tarefa @responsável !30/09/2026 #projeto [interno]   <!-- id:… -->
      > descrição da tarefa, uma ou mais linhas
  - [ ] subtarefa (basta indentar 2 espaços)                         <!-- id:… -->
    - [ ] sub-subtarefa (indente mais 2)                             <!-- id:… -->
```

| marcador | o que define | se você não escrever |
|---|---|---|
| `- [ ]` / `[/]` / `[x]` | a fazer / em andamento / concluída | a fazer |
| `@nome` | responsável (`@"Nome Composto"` com aspas) | fica **sem responsável** |
| `!dd/mm/aaaa` | prazo | fica **sem prazo** |
| `#projeto` / `#aculturamento` | tipo | Projeto de IA |
| `[interno]` | o cliente **não** vê esta tarefa | o cliente vê |
| `> texto` na linha de baixo | descrição (aparece ao abrir o card) | sem descrição |
| indentar 2 espaços | vira subtarefa da tarefa acima (vale em qualquer profundidade) | tarefa de topo |

Os marcadores só valem **no fim da linha** — `Revisar #3 do contrato` continua sendo um título.
Um título que TERMINA na forma de um marcador sai escapado com `\\` (`Ligar para \\@joao`); a barra é
só para o parser e nunca aparece no card. Você não precisa escrever isso à mão.
Marque `[x]` para concluir e adicione linhas novas à vontade: elas entram no quadro na próxima
sincronização e voltam aqui com o `<!-- id:… -->` preenchido. **Não apague o marcador de id**
das tarefas que já têm um.

- [x] Definir a taxonomia de origem e campanha @"Karol e Márcio" !28/09/2026 #aculturamento [interno]  <!-- id:45bb5d1b-b757-4d29-9afa-cee4d0077552 -->
  > O Champion preenche B3-01 em `03-Projeto/decisoes-fase-3.md` com agrupamento de `utm_source`, `utm_medium` e `utm_campaign`, granularidade, data e confirmação verificável. Marketing/agência e Gestão podem ser consultados; nenhuma configuração é criada. Concluída documentalmente em 24/09/2026; nenhuma configuração foi criada.
- [x] Consolidar os eventos das fases 1 e 2 no funil de conversão @"Karol e Márcio" !01/10/2026 [interno]  <!-- id:ab9ce40f-304e-4ef6-929f-1efa7f7a0a87 -->
  > Implementação da SPEC-3-001 concluída e validada no preview v0.0.81 em 25/09/2026: QA completo; teste humano confirmou os valores da janela isolada de 23/09, o recálculo determinístico e rollback/reativação; teste isolado do contrato confirmou leitura parcial e taxa nula quando uma fonte falha. Migrações 0050–0051 aplicadas. Produção não publicada; aceite formal da SPEC permanece na task separada 4217198c-8077-4769-b2c0-7b7482136553.
- [ ] Configurar o dashboard por formulário e campanha e congelar o baseline @"Karol e Márcio" !05/10/2026 [interno]  <!-- id:124f370f-ea01-46d4-bdac-72c1cded2181 -->
  > Iniciar somente depois de B3-01, B3-02, B3-04 e B3-05 estarem registrados pelo Champion em `03-Projeto/decisoes-fase-3.md` e de a SPEC-3-001 estar aceita. No ambiente de teste, executar a SPEC-3-002: dashboard comparativo por formulário, versão e campanha conforme taxonomia, matriz de acesso registrada, baseline congelado com aprovação do Champion; encerrar somente após teste humano da task.
- [ ] Revisar o aceite da consolidação @"Felipe Navaar" !06/10/2026 #aculturamento [interno]  <!-- id:4217198c-8077-4769-b2c0-7b7482136553 -->
  > Conferir a SPEC-3-001, CA-3.01 a CA-3.05, seus testes humanos e as evidências de consolidação; registrar aceite ou correções antes de encerrar esta SPEC. A SPEC exige captura do ambiente de teste, conferência das contagens contra fixtures, export sanitizado, logs de rollback e aceite humano; conferir a presença do pacote de evidências nesta revisão.
- [x] Definir a fórmula e a janela da métrica norte @"Karol e Márcio" #aculturamento [interno]  <!-- id:2ce9c4fb-c143-4519-ba1f-e0ce80807e9b -->
  > B3-02 concluída documentalmente em 24/09/2026: numerador “Agendamentos concluídos no período”, denominador “Encaminhamentos humanos no mesmo período”, janela “Últimos 30 dias corridos” e confirmação verificável de Karol. Nenhuma métrica foi configurada e nenhum produto foi alterado.
- [x] Decidir o vínculo entre triagem e agendamento @"Karol e Márcio" #aculturamento [interno]  <!-- id:bcc00bba-0eb4-4821-9ccf-b74755969f43 -->
  > B3-03 concluída documentalmente em 24/09/2026: preservar o vínculo da triagem; o agendamento deve manter o `lead_submission_id` de origem quando a continuidade estiver disponível; casos sem vínculo permanecem como cobertura incompleta, sem atribuição por inferência. Nenhum código, banco, configuração, integração ou produto foi alterado.
- [ ] Definir a matriz de acesso ao dashboard @"Karol e Márcio" #aculturamento [interno]  <!-- id:617b477e-d9f6-4256-ab84-530b932596fc -->
  > O Champion preenche B3-04 em `03-Projeto/decisoes-fase-3.md` com os papéis de leitura, preservando a proibição de dados de contato individuais para Marketing, data e confirmação verificável. Nenhuma permissão é concedida nesta tarefa.
- [ ] Aprovar o critério de congelamento do baseline @"Karol e Márcio" #aculturamento [interno]  <!-- id:d30d0144-19d9-421d-b2a4-5c6bf4942533 -->
  > O Champion preenche B3-05 em `03-Projeto/decisoes-fase-3.md` com o critério de congelamento e interpretação, data e confirmação verificável. Esta decisão não define a fórmula nem valores de B3-02 e pode ser registrada em paralelo. Nenhum baseline é criado ou congelado nesta tarefa.
- [ ] Revisar o aceite do dashboard @"Felipe Navaar" !06/10/2026 #aculturamento [interno]  <!-- id:e88283fc-42a2-48a5-9924-48b28dd4f0cb -->
  > Conferir a SPEC-3-002, CA-3.06 a CA-3.10, seus testes humanos e o baseline congelado; registrar aceite ou correções antes de encerrar esta SPEC.
