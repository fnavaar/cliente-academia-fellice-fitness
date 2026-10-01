# SPEC-4-002 — Painel de saúde da integração e histórico de alterações

**Fase:** 4
**Status:** SPEC aprovada pelo consultor em 30/09/2026 ("libero todas as specs, pode executar"); tasks geradas. Nenhum dado real é carregado antes de B4-01.

**Dono:** Champion do cliente (decisor de B4-03); Gestão e Marketing/agência podem ser consultados conforme matriz
**Origem:** Fase 4 e §7 do escopo definitivo; EV-F3-03 (B4-03); EV-F3-07 (regras de construção)
**Degrau:** visibilidade da saúde da integração e da conversão sobre os eventos já consolidados, com histórico append-only; sem decisão automática, sem exportação individual e sem escrita externa.

**Gate atual:** tasks de decisão (B4-03) e de implementação liberadas na Jornada da Fase 4; execução uma por vez com teste humano.

## Contexto e resultado

Hoje não existe visão do estado da integração (fila, falhas, reprocessamentos) nem histórico das alterações relevantes no encaminhamento e no agendamento. O resultado desejado é um painel de saúde da integração e da conversão por formulário/campanha, com fórmula, período e cobertura na mesma disciplina da Fase 3, e um histórico atribuível e somente-adição das alterações relevantes.

## BLOQUEIOS executáveis

| Bloqueio | Dono | Evidência para liberar |
|---|---|---|
| B4-03 — matriz de acesso ao painel de saúde (proposta EV-F3-03 — validar) | Champion | Matriz registrada com papéis permitidos e negados (ponto de partida: B3-04 — Champion, Gestão, Supervisora e Subgerente leem agregados; Marketing/agência e Consultor sem acesso) |
| B4-01 — base legal/consentimento LGPD (proposta EV-F3-01 — validar) | Champion | Necessário antes de exibir ou replicar dado real de lead |

## Limites, dados e permissões

Inclui estado da integração (fila, reprocessados, falhas com dono), conversão por formulário/versão/origem/campanha com fórmula, período e cobertura, sinalização de degradação do conector e histórico append-only de alterações relevantes no encaminhamento e agendamento. Ficam fora exportação de dados individuais, exposição de contatos, reconciliação silenciosa, escrita externa e decisão automática de campanha.

Regras: papel fora da matriz não acessa (prova negativa em UI e URL); dado individual não é exposto; divergência entre integração e plataforma vira pendência com responsável, nunca reconciliação silenciosa; falha do conector sinaliza degradação sem inventar dados. Allowlist explícita como autoridade (EV-F3-07).

## Fluxo de execução

1. Champion registra B4-03; B4-01 decidido antes de dado real.
2. Executor constrói o painel com fixtures sintéticos sobre os eventos consolidados (F3) e o estado simulado da fila.
3. Provas negativas: papel fora da matriz não acessa; contatos não aparecem; falha do conector não gera número.
4. Teste humano do Champion; aceite formal em task separada; publicação somente após autorização explícita.

## Critérios de aceite

- **CA-4-006:** o painel mostra estado da integração (fila, reprocessados, falhas com dono) e conversão por formulário/campanha com fórmula, período e cobertura.
- **CA-4-007:** histórico de alterações relevantes no encaminhamento e agendamento é somente-adição e atribuído.
- **CA-4-008:** papel fora da matriz não acessa (UI e URL); dado individual/contato não é exposto.
- **CA-4-009:** divergência integração×plataforma aparece como pendência com responsável, nunca reconciliada silenciosamente.
- **CA-4-010:** falha do conector sinaliza degradação no painel sem inventar dados.

## TDD da SPEC

- **RED:** hoje não há visão de saúde da integração nem histórico; fila e falhas são invisíveis para a operação.
- **GREEN:** fixture com fila (2 pendentes, 1 reprocessado, 1 falha) e eventos da F3 produz painel correto com cobertura e fórmula visíveis; histórico registra alterações com autor e data.
- **REGRESSÃO:** papel fora da matriz negado em UI e URL; consulta sem dado devolve cobertura incompleta (nunca zero fabricado); falha do conector marca degradação; rollback não apaga histórico.

Evidências: capturas do painel, fixtures sanitizados, provas negativas de acesso e aceite humano.

## Tasks vinculadas

| ID | Task | Critério | Pré-condição |
|---|---|---|---|
| id pendente | Registrar a matriz de acesso do painel de saúde | B4-03 | decisão do Champion |
| id pendente | Configurar o painel de saúde da integração | CA-4-006..010 | B4-03 registrado + integração configurada |
