# Fase 4 — Tarefas

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
| `- [ ]` / `- [/]` / `- [x]` | a fazer / em andamento / concluída | a fazer |
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
sincronização e voltam aqui com o `<!-- id:… -->` preenchido. **Não apague o marcador de id** das
tarefas que já têm um.

- [ ] Definir contrato, acesso e fallback da integração @Cliente !07/10/2026 #aculturamento [interno]  <!-- id:7953f975-0f69-42a0-a9a1-b028429550cb -->
  > SPEC-4-001 — bloqueios B4-01, B4-02 e B4-05 (seções "BLOQUEIOS executáveis" e "Limites, dados e permissões"). Insumos do Champion embutidos nesta task, para registrar em `03_documentos/decisoes-fase-4.md` com data e confirmação verificável: (1) B4-01 — qual base legal/consentimento e autorização de escrita externa para dados de lead? (2) B4-02 — qual ferramenta será integrada (Kommo, Lóvavel ou ambas) e quais credenciais/permissões existem para a call de setup? (3) B4-05 — tabela de campos origem→destino, identificador externo e regra de conflito (proposta: dado conflitante nunca é sobrescrito sem regra aprovada). Leva 1. Pré-condição: SPECs da Fase 4 aprovadas. Ponto de parada: nenhuma credencial é ativada e nenhuma escrita externa acontece antes de B4-01/02/05 liberados. Estado final: decisões registradas; encerrar somente após registro humano verificável.
- [ ] Configurar a integração em ambiente autorizado @Cliente !08/10/2026 [interno]  <!-- id:c86d168b-96c9-48ca-9eee-44e73a4ac648 -->
  > SPEC-4-001 — critérios CA-4-001..005 (seções "Fluxo de execução" e "Critérios de aceite"): campos, identificador externo, permissões, tratamento de erro e rollback documentados; evento repetido não cria duplicidade no destino; falha de escrita mantém a origem, entra em reconciliação com dono e nunca vira sucesso; dado conflitante não é sobrescrito sem regra aprovada; rollback suspende a escrita externa preservando a captura local. Recorte da prova: fixtures sintéticos (2 eventos iguais, 1 conflito, 1 falha de escrita) + prova negativa de permissão. Evidência esperada: contrato de campos aprovado, logs sanitizados, estado da fila, provas negativas e aceite humano. Leva 2. Pré-condição: B4-01, B4-02 e B4-05 liberados na task de contrato/acesso. Ponto de parada: nada roda contra ferramenta real fora de conta de teste autorizada. Estado final: integração demonstrada em ambiente autorizado; encerrar somente após registro humano verificável.
  - [ ] Provar o conector em conta de teste (timeboxed)
    > Leitura e escrita com identificador externo em conta de teste, sem massa real; registrar o resultado mesmo negativo — capacidade não validada bloqueia a leva seguinte.
- [ ] Registrar a matriz de acesso do painel de saúde @"Karol e Márcio" !07/10/2026 #aculturamento [interno]
  > SPEC-4-002 — bloqueio B4-03 (seção "BLOQUEIOS executáveis"). Insumo do Champion embutido nesta task: quem pode ler o painel de saúde da integração? Ponto de partida proposto (proposta — validar): mesma B3-04 (Champion, Gestão, Supervisora e Subgerente leem agregados; Marketing/agência e Consultor sem acesso). Evidência: matriz registrada com papéis permitidos e negados, data e confirmação verificável em `03_documentos/decisoes-fase-4.md`. Leva 1 (paralela às decisões da integração). Ponto de parada: nenhum dado real é exibido antes de B4-01 e B4-03. Estado final: decisão registrada; encerrar somente após registro humano verificável.
- [ ] Congelar o baseline e aprovar o alvo do loop @"Karol e Márcio" !07/10/2026 #aculturamento [interno]
  > SPEC-4-003 — bloqueios B4-04 e alvo quantitativo (seção "BLOQUEIOS executáveis"). Insumos do Champion embutidos nesta task: (1) congelar a versão operacional do baseline com numerador, denominador, período, cobertura e versão, conforme critério B3-05 (mês civil `America/Bahia`, limiar 50%) — a Fase 3 fechou sem versão congelada; (2) registrar o alvo quantitativo do ciclo aprovado junto com a Gestão (nenhum alvo é inferido). Evidência: versão de baseline e alvo com data e confirmação verificável em `03_documentos/decisoes-fase-4.md`. Leva 1 (paralela). Ponto de parada: o loop da Fase 4 não é ativado sem baseline congelado e alvo aprovado. Estado final: baseline e alvo registrados; encerrar somente após registro humano verificável.
- [ ] Configurar o loop de saúde da conversão @Cliente !09/10/2026 [interno]  <!-- id:31dae29a-884a-4ac6-a23a-2cfc5b0e56a8 -->
  > SPEC-4-003 — critérios CA-4-011..014 (seções "Fluxo de execução" e "Critérios de aceite"): ciclo semanal registra baseline, cobertura, achado e veredito humano (sem veredito, nenhuma recomendação vira ação); alvo só fica ativo após aprovação Champion+Gestão; loop e assistente não alteram formulário, regra, campanha ou integração (prova negativa de escrita externa); falha de medição ou conector interrompe recomendações e abre pendência para o responsável. Recorte da prova: fixture com baseline congelado e 2 ciclos sintéticos. Evidência esperada: registro dos ciclos, provas negativas de escrita e aceite humano. Leva 3. Pré-condição: baseline congelado e alvo aprovado; integração configurada. Ponto de parada: nenhum loop é ativado em produção sem autorização explícita. Estado final: loop configurado e demonstrado; encerrar somente após registro humano verificável.
- [ ] Configurar o painel de saúde da integração @"Karol e Márcio" !10/10/2026 [interno]
  > SPEC-4-002 — critérios CA-4-006..010 (seções "Fluxo de execução" e "Critérios de aceite"): estado da integração (fila, reprocessados, falhas com dono) e conversão por formulário/campanha com fórmula, período e cobertura; histórico somente-adição de alterações relevantes no encaminhamento e agendamento; divergência integração×plataforma vira pendência com responsável (nunca reconciliação silenciosa); falha do conector sinaliza degradação sem inventar dados. Recorte da prova: fixtures com fila (2 pendentes, 1 reprocessado, 1 falha) + provas negativas (papel fora da matriz negado em UI e URL; contato não exposto). Evidência esperada: capturas do painel, fixtures sanitizados, provas negativas e aceite humano. Leva 3 (paralela ao loop). Pré-condição: B4-03 registrado; integração configurada (CA-4-001..005). Ponto de parada: nenhum dado real antes de B4-01. Estado final: painel demonstrado; encerrar somente após registro humano verificável.
- [ ] Executar um ciclo e provar recuperação @Cliente !13/10/2026 #aculturamento [interno]  <!-- id:12bf95df-e79a-4ef2-b4f1-214fc65c3cbb -->
  > SPEC-4-003 — revalidação operacional de CA-4-011 e CA-4-014 (REGRESSÃO): executar um ciclo semanal do loop com registro de baseline, cobertura, achado e veredito humano; provar recuperação com falha simulada de medição ou conector (recomendações interrompidas e pendência aberta para o responsável). Evidência esperada: registro do ciclo, prova de recuperação e veredito humano. Leva 4. Pré-condição: loop configurado e demonstrado. Ponto de parada: o ciclo não executa alteração externa. Estado final: ciclo executado e recuperação provada; encerrar somente após registro humano verificável.
- [ ] Revisar os ciclos e decidir o fechamento da Fase 4 @"Felipe Navaar" !14/10/2026 #aculturamento [interno]  <!-- id:c5ccd038-0cae-4e1d-9d72-52e2d3ef935d -->
  > Revisão formal do consultor sobre a Fase 4: CA-4-001..014, evidências das tasks anteriores, provas negativas (sem escrita externa pelo loop, sem duplicidade, sem sucesso falso) e vereditos humanos dos ciclos. Registrar aceite ou correções antes de fechar a fase. Leva final. Pré-condição: tasks anteriores concluídas com evidência aprovada. Estado final: decisão de fechamento registrada; encerrar somente após registro humano verificável.
