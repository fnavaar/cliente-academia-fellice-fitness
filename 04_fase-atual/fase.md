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
| `#projeto` / `#aculturamento` | tipo (`Projeto de IA` ou `Aculturamento`) | Projeto de IA |
| `[interno]` | tarefa invisível para o cliente | tarefa visível |
| `<!-- id:UUID -->` | identificador estável da tarefa | — |

- [x] Definir a taxonomia de origem e campanha @"Karol e Márcio" !28/09/2026 #aculturamento [interno]  <!-- id:45bb5d1b-b757-4d29-9afa-cee4d0077552 -->
  > O Champion preenche B3-01 em `03_documentos/decisoes-fase-3.md` com agrupamento de `utm_source`, `utm_medium` e `utm_campaign`, granularidade, data e confirmação verificável. Marketing/agência e Gestão podem ser consultados; nenhuma configuração é criada. Concluída documentalmente em 24/09/2026; nenhuma configuração foi criada.
- [x] Consolidar os eventos das fases 1 e 2 no funil de conversão @"Karol e Márcio" !01/10/2026 [interno]  <!-- id:ab9ce40f-304e-4ef6-929f-1efa7f7a0a87 -->
  > Implementação da SPEC-3-001 concluída e validada no preview v0.0.81 em 25/09/2026: QA completo; teste humano confirmou os valores da janela isolada de 23/09, o recálculo determinístico e rollback/reativação; teste isolado do contrato confirmou leitura parcial e taxa nula quando uma fonte falha. Migrações 0050–0051 aplicadas. Produção não publicada; aceite formal da SPEC permanece na task separada 4217198c-8077-4769-b2c0-7b7482136553.
- [ ] Configurar o dashboard por formulário e campanha e congelar o baseline @"Karol e Márcio" !05/10/2026 [interno]  <!-- id:124f370f-ea01-46d4-bdac-72c1cded2181 -->
  > Executar a SPEC-3-002 (dashboard comparativo por formulário, versão e campanha) no ambiente de teste. **Responda as duas decisões abaixo JUNTO com esta task e execute — não marque como bloqueada.** B3-04 (matriz de acesso): quais papéis têm leitura no dashboard (Champion, Gestão, Supervisora, Marketing) e confirmação de que Marketing/agência não recebe nome, telefone, e-mail ou registros individuais. B3-05 (congelamento do baseline): quando o baseline congela e a leitura da métrica norte (agendamentos concluídos ÷ encaminhamentos humanos, janela de 30 dias). Registre as duas em `03_documentos/decisoes-fase-3.md` com data e confirmação de Karol. Com as respostas em mãos, congelar o baseline e encerrar somente após teste humano da task.
- [x] Revisar o aceite da consolidação @"Felipe Navaar" !06/10/2026 #aculturamento [interno]  <!-- id:4217198c-8077-4769-b2c0-7b7482136553 -->
  > ACEITE SEM RESSALVA registrado por decisão do consultor (Navaar) em 28/09/2026. CA-3.01 a CA-3.05 conferidos e conformes; a evidência disponível (logs de runtime do Skip Cloud, inspeção de código com não exposição de contatos e testes humanos de 25/09) foi considerada suficiente. Task encerrada e SPEC-3-001 liberada. Pacote em `06_notas/aceites/pacote-evidencias-spec-3-001.md`. Ratificado pelo operador ETHOS (Ricardo Junior) em 28/09/2026 às 16:11, com a conferência humana de 15:08 registrada no changelog.
- [x] Definir a fórmula e a janela da métrica norte @"Karol e Márcio" #aculturamento [interno]  <!-- id:2ce9c4fb-c143-4519-ba1f-e0ce80807e9b -->
  > B3-02 concluída documentalmente em 24/09/2026: numerador “Agendamentos concluídos no período”, denominador “Encaminhamentos humanos no mesmo período”, janela “Últimos 30 dias corridos” e confirmação verificável de Karol. Nenhuma métrica foi configurada e nenhum produto foi alterado.
- [x] Decidir o vínculo entre triagem e agendamento @"Karol e Márcio" #aculturamento [interno]  <!-- id:bcc00bba-0eb4-4821-9ccf-b74755969f43 -->
  > B3-03 concluída documentalmente em 24/09/2026: preservar o vínculo da triagem; o agendamento deve manter o `lead_submission_id` de origem quando a continuidade estiver disponível; casos sem vínculo permanecem como cobertura incompleta, sem atribuição por inferência. Nenhum código, banco, configuração, integração ou produto foi alterado.
- [x] Definir a matriz de acesso ao dashboard @"Karol e Márcio" #aculturamento [interno]  <!-- id:617b477e-d9f6-4256-ab84-530b932596fc -->
  > B3-04 concluída documentalmente em 29/09/2026: Champion, Gestão, Supervisora e Subgerente podem ler o dashboard agregado; Marketing/agência e Consultor não podem ler. Confirmação atribuída a Karol, transmitida por Ricardo Junior no chat às 11:44: “matriz correta e autorizada, não podem ler: marketing e consultor, os demais, autorizado”. A aplicação técnica da matriz ainda será provada dentro da task 124f370f; nenhuma permissão de runtime/produção foi alterada por este registro.
- [ ] Aprovar o critério de congelamento do baseline @"Karol e Márcio" #aculturamento [interno]  <!-- id:d30d0144-19d9-421d-b2a4-5c6bf4942533 -->
  > B3-05 — responder JUNTO com a task de dashboard (124f370f), sem travar o projeto: critério de congelamento do baseline e leitura da métrica norte. Registrar em `03_documentos/decisoes-fase-3.md` com data e confirmação de Karol.
- [ ] Revisar o aceite do dashboard @"Felipe Navaar" !06/10/2026 #aculturamento [interno]  <!-- id:e88283fc-42a2-48a5-9924-48b28dd4f0cb -->
  > Conferir a SPEC-3-002, CA-3.06 a CA-3.10, seus testes humanos e o baseline congelado; registrar aceite ou correções antes de encerrar esta SPEC.
