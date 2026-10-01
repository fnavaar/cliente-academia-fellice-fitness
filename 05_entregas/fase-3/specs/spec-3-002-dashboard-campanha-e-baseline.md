# SPEC-3-002 — Dashboard por formulário e campanha com baseline congelado

**Fase:** 3  
**Status:** task de implementação/teste humano `124f370f` concluída por Ricardo Junior em 30/09/2026 no preview v0.0.85 (`c41cf7c`); login autenticado HTTP 200 e `POST /backend/v1/dashboard` HTTP 200. QA completo passou. A revisão formal independente do aceite na task `e88283fc` está pendente. Produção não publicada.

**Dono:** Champion do cliente (decisor dos bloqueios); Marketing/agência e Gestão podem ser consultados  
**Origem:** D-003, RQ-008, Fase 3 e §7 do escopo definitivo  
**Degrau:** dashboard nativo sobre a consolidação da SPEC-3-001, sem integração externa, causalidade ou decisão automática de campanha.

**Gate atual:** implementação/teste humano da task `124f370f` concluídos; aceite formal da SPEC-3-002 segue na task `e88283fc`.

## Contexto e resultado

Não existe comparação por formulário, versão ou campanha. O resultado desejado é dashboard comparativo por formulário, versão, origem e campanha quando disponível, com fórmula, período, cobertura e primeiro baseline congelado; matriz de leitura conforme B3-04. Marketing/agência e Consultor não têm acesso ao dashboard.

## BLOQUEIOS executáveis

| Bloqueio | Dono | Evidência para liberar |
|---|---|---|
| B3-01 — taxonomia de origem/campanha | Champion | Decisão, data e confirmação verificável no registro canônico |
| B3-02 — fórmula e janela da métrica norte | Champion | Decisão, data e confirmação verificável no registro canônico |
| B3-04 — matriz de acesso por papel | Champion | Matriz registrada com papéis permitidos e negados; Marketing/agência sem acesso |
| B3-05 — critério e interpretação do baseline congelado | Champion | Critério, data e confirmação verificável no registro canônico |

A SPEC-3-002 também depende de SPEC-3-001 testada e aceita. Nenhum bloqueio pendente autoriza GREEN.

## Limites, dados e permissões

Inclui dashboard por formulário/versão/origem/campanha, comparação respeitando vigência, baseline versionado e rollback para dados brutos. Ficam fora decisão automática de campanha, receita, matrícula, comparecimento, meta não aprovada, exportação individual e escrita externa.

**Matriz aprovada em B3-04:** Champion, Gestão, Supervisora e Subgerente podem ler o dashboard agregado; Marketing/agência e Consultor não têm acesso. O dashboard não expõe contatos nem registros individuais. Apenas Champion cria, corrige ou congela baseline; toda escrita por outro papel é recusada. Registro imutável contém numerador, denominador, período, cobertura e versão. Nova apuração cria nova versão, nunca altera retroativamente a anterior. O registro da decisão não comprova, por si só, a aplicação técnica da matriz no runtime; essa evidência de acesso permanece parte dos critérios de aceite da task.

## Fluxo de execução

1. Champion registra B3-01, B3-02, B3-04 e B3-05.
2. SPEC-3-001 é testada e aceita.
3. Executor constrói dashboard com fixtures sintéticas, respeita vigência, mostra não classificada e sem atribuição, prova leitura/escrita negada e congela baseline somente com Champion.
4. Obtém teste humano, aceite e autorização antes de publicar.

Estado após B3-05 e aprovação humana: Ricardo Junior confirmou em 30/09/2026 que testou e aprovou os critérios da task `124f370f` no preview. Os logs de runtime confirmam login e leitura autenticada do dashboard com HTTP 200; QA completo da versão v0.0.85 passou. Os critérios CA-3.06..10 foram conferidos no código e no teste humano conforme registro da task; nenhum baseline operacional foi congelado nesta validação. A revisão formal do aceite ainda está na task `e88283fc`; não publicar em produção antes do gate próprio.

## Critérios de aceite

- **CA-3.06:** conversão por formulário e versão respeita vigência.
- **CA-3.07:** origem/campanha segue taxonomia; faltas aparecem como grupo próprio.
- **CA-3.08:** cada indicador apresenta fórmula, período e cobertura; insuficiência é explícita.
- **CA-3.09:** Champion congela baseline com numerador, denominador, período, cobertura e versão; outro papel não escreve; nenhuma meta é inventada.
- **CA-3.10:** papel fora da matriz não acessa; rollback preserva consolidação e baseline.

## TDD da SPEC

- **RED:** comparação e baseline ainda exigem montagem manual.
- **GREEN:** duas versões em vigência, campanhas classificadas/não classificadas, registros sem atribuição e papéis sintéticos produzem dashboard correto.
- **REGRESSÃO:** congela com Champion, nega leitura/escrita não autorizada, testa período vazio e rollback sem apagar registros.

Evidências: capturas do dashboard, fixture/export sanitizado, registro versionado do baseline, provas negativas de acesso/escrita e aceite humano.

## Tasks vinculadas

| ID | Task | Critério | Pré-condição |
|---|---|---|---|
| `45bb5d1b-b757-4d29-9afa-cee4d0077552` | Definir taxonomia | B3-01 registrado | Champion decide |
| `2ce9c4fb-c143-4519-ba1f-e0ce80807e9b` | Definir fórmula/janela | B3-02 registrado | Champion decide |
| `617b477e-d9f6-4256-ab84-530b932596fc` | Definir acesso | B3-04 registrado | Champion decide |
| `d30d0144-19d9-421d-b2a4-5c6bf4942533` | Aprovar baseline | B3-05 registrado | governança |
| `124f370f-ea01-46d4-bdac-72c1cded2181` | Configurar dashboard/baseline | CA-3.06..10 | SPEC-3-001 aceita + gates |
| `e88283fc-42a2-48a5-9924-48b28dd4f0cb` | Revisar aceite | CA-3.06..10 | implementação concluída |

**Gate antes do GREEN:** B3-01, B3-02, B3-04 e B3-05 preenchidos com data e confirmação verificável do Champion.
