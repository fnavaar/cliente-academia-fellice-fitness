# SPEC-3-002 — Dashboard por formulário e campanha com baseline congelado

**Fase:** 3  
**Status:** tarefas de decisão liberadas ao Champion — implementação bloqueada até os bloqueios desta SPEC serem resolvidos com registro humano  
**Dono:** Champion do cliente (decisor dos bloqueios); Marketing/agência e Gestão podem ser consultados  
**Origem:** D-003, RQ-008, Fase 3 e §7 do escopo definitivo  
**Degrau:** dashboard nativo sobre a consolidação da SPEC-3-001, sem integração externa, causalidade ou decisão automática de campanha.

## Contexto e resultado

Não existe comparação por formulário, versão ou campanha. O resultado desejado é dashboard comparativo por formulário, versão, origem e campanha quando disponível, com fórmula, período, cobertura e primeiro baseline congelado; Marketing vê apenas agregados.

## BLOQUEIOS executáveis

| Bloqueio | Dono | Evidência para liberar |
|---|---|---|
| B3-01 — taxonomia de origem/campanha | Champion | Decisão, data e confirmação verificável no registro canônico |
| B3-02 — fórmula e janela da métrica norte | Champion | Decisão, data e confirmação verificável no registro canônico |
| B3-04 — matriz de acesso por papel | Champion | Matriz registrada; Marketing sem contatos individuais |
| B3-05 — critério e interpretação do baseline congelado | Champion | Critério, data e confirmação verificável no registro canônico |

A SPEC-3-002 também depende de SPEC-3-001 testada e aceita. Nenhum bloqueio pendente autoriza GREEN.

## Limites, dados e permissões

Inclui dashboard por formulário/versão/origem/campanha, comparação respeitando vigência, baseline versionado e rollback para dados brutos. Ficam fora decisão automática de campanha, receita, matrícula, comparecimento, meta não aprovada, exportação individual e escrita externa.

Marketing/agência, Gestão, Subgerente e Consultor leem agregados conforme B3-04. Apenas Champion cria, corrige ou congela baseline; toda escrita por outro papel é recusada. Registro imutável contém numerador, denominador, período, cobertura e versão. Nova apuração cria nova versão, nunca altera retroativamente a anterior.

## Fluxo de execução

1. Champion registra B3-01, B3-02, B3-04 e B3-05.
2. SPEC-3-001 é testada e aceita.
3. Executor constrói dashboard com fixtures sintéticas, respeita vigência, mostra não classificada e sem atribuição, prova leitura/escrita negada e congela baseline somente com Champion.
4. Obtém teste humano, aceite e autorização antes de publicar.

Estado válido enquanto bloqueado: dashboard apenas em planejamento; nenhum baseline falso, permissão nova, dado real ou publicação.

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
