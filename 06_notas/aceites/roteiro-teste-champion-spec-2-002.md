# Roteiro de teste do Champion — SPEC-2-002 (F2-IMP-009)

**Onde:** https://fellice-fitness-8733f--preview.goskip.app/visao
**Quanto tempo:** 10–15 min · **Dados:** todos sintéticos (fixtures F2-IMP-009)

## Credenciais de teste (temporárias — removidas após o aceite)

| Papel | E-mail | Senha |
|---|---|---|
| Champion | `champion.f2imp009@fellice-fitness.local` | `ChampionF2Imp009@2026` |
| Consultor A | `consultor.a.f2imp009@fellice-fitness.local` | `ConsultorAF2Imp009@2026` |
| Consultor B | `consultor.b.f2imp009@fellice-fitness.local` | `ConsultorBF2Imp009@2026` |
| Gestão | `gestao.f2imp009@fellice-fitness.local` | `GestaoF2Imp009@2026` |

## Cenário 1 — Visão completa (CA-2.06) · ~3 min

1. Entre na `/visao` com o **Champion**.
2. Confira os contadores: **Todos (10)** com os 4 estados — `TENTATIVA`, `CONCLUIDO`, `DESISTENCIA`, `ENCAMINHAMENTO_HUMANO`.
3. Clique em cada filtro de estado e confira os contadores.
4. Abra "Ver contexto completo" no card **Lead Consolidação Concluído**: objetivo, proximidade, ocupação, interesse, origem/campanha (facebook/cpc/consolidacao-f2-009), versão do formulário e dados do agendamento.
5. **Falha se:** algum estado sumir da visão, contador errado, ou contexto incompleto no modal.

## Cenário 2 — Fila única e assunção (CA-2.07) · ~3 min

1. Saia e entre com o **Consultor A**.
2. No card **Lead Consolidação Encaminhamento** (sem dono), clique **Assumir caso**.
3. O card passa a exibir "Assumida por você em <data/hora>".
4. Saia e entre com o **Consultor B**: a mesma tentativa aparece como assumida pelo ID do Consultor A (fila única — dono visível), e a **Lead Consolidação Fila** (sem dono) mostra o botão "Assumir caso".
5. **Falha se:** dois consultores conseguirem assumir o mesmo caso, ou dono/`assumed_at` não aparecerem.

## Cenário 3 — Ações de liderança (CA-2.09/escalada) · ~3 min

1. Entre com a **Gestão**.
2. No card **Lead Consolidação Fila**, preencha o motivo e clique **Sinalizar escalada** → aparece "Escalada em <data/hora>" em vermelho.
3. Ainda como Gestão, no card **Lead Consolidação Encaminhamento** (assumido pelo Consultor A), preencha o campo "ID do novo responsável" com o ID do **Consultor B** (`ijik9wxk0nu8zcy`) e clique **Reatribuir** → o card passa a exibir "Reatribuída — responsável anterior: <ID do Consultor A>".
4. Opcional: **Encerrar sem agendamento** na **Lead Consolidação Fila** com motivo → "Encerrada em …" com o motivo.
5. **Falha se:** qualquer ação mudar o estado para algo diferente de `ENCAMINHAMENTO_HUMANO`, ou faltar o motivo obrigatório.

## Cenário 4 — Bloqueio de papel sem permissão (CA-2.09) · ~2 min

1. Entre com o **Consultor B**.
2. Confirme que nos cards **não aparecem** os botões "Sinalizar escalada", "Reatribuir" nem "Encerrar sem agendamento" (só "Assumir caso" em tentativas sem dono).
3. **Falha se:** qualquer botão de Gestão/Supervisora aparecer para o Consultor.

## Cenário 5 — Rollback da fila (CA-2.10) · ~3 min

1. Entre com o **Champion**.
2. No bloco "Fila: ativa", preencha o motivo e clique **Desativar ações** → o selo muda para "Fila: em rollback".
3. Como **Consultor A**, tente **Assumir caso** na **Lead Consolidação Fila** → deve aparecer erro ("ações da fila estão temporariamente desativadas").
4. Volte ao **Champion**, clique **Reativar ações** → selo volta a "Fila: ativa".
5. Confirme que todos os registros continuam listados, sem perda.
6. **Falha se:** registros sumirem, ou a fila voltar sozinha sem o RESTORE.

## Após o teste

- **Aprovado:** o Champion registra o aceite ("aceito") e a SPEC-2-002 é encerrada; a limpeza das fixtures e usuários de teste é executada em seguida.
- **Reprovado:** descreva o passo e o comportamento observado — a task permanece aberta e entra em debug, sem concluir nada.
