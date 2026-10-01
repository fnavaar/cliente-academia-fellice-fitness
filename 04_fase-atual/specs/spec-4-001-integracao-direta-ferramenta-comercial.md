# SPEC-4-001 — Integração direta com a ferramenta comercial (Kommo/Lóvavel)

**Fase:** 4
**Status:** SPEC aprovada pelo consultor em 30/09/2026 ("libero todas as specs, pode executar"); tasks geradas. Nenhuma credencial, conector ou escrita externa é ativada por esta SPEC.

**Dono:** Champion do cliente (decisor dos bloqueios); Comercial aprova o mapeamento de campos
**Origem:** Fase 4 e §7 do escopo definitivo; EV-F3-01 (B4-01); EV-F3-07 (regras de construção)
**Degrau:** integração de escrita controlada entre a plataforma e a ferramenta comercial validada, com idempotência, reconciliação e rollback; sem negociação autônoma, sem substituição do Kommo/Lóvavel/Polisystem e sem automação de pós-venda.

**Gate atual:** tasks `7953f975` (decisões) e `c86d168b` (implementação) liberadas na Jornada da Fase 4; execução uma por vez com teste humano.

## Contexto e resultado

Lead e agendamento aprovado hoje não saem da plataforma sem cópia manual. O resultado desejado é que passem entre a plataforma e a ferramenta comercial definida (Kommo e/ou Lóvavel, conforme capacidade validada) sem duplicidade silenciosa: campos mapeados, identificador externo, idempotência por evento, registro de falhas e fila de reconciliação com responsável.

## BLOQUEIOS executáveis

| Bloqueio | Dono | Evidência para liberar |
|---|---|---|
| B4-01 — base legal/consentimento LGPD e autorização de escrita externa (proposta EV-F3-01 — validar) | Champion | Registro de base legal, minimização de dados e autorização de escrita em ferramenta externa, com data e confirmação verificável |
| B4-02 — credenciais, permissões e capacidade do conector validados | Champion técnico | Call de setup com credenciais validadas + prova técnica timeboxed de leitura/escrita em conta de teste (Kommo e/ou Lóvavel); nenhum conector é ativado sem isso |
| B4-05 — mapeamento de campos e regra de conflito/sobrescrita aprovados | Comercial/Champion | Tabela de campos (origem→destino), identificador externo e regra: dado conflitante nunca é sobrescrito sem regra aprovada |

Nenhum bloqueio pendente autoriza escrita externa real.

## Limites, dados e permissões

Inclui mapeamento aprovado de campos, identificador externo, idempotência por evento, registro de falhas, fila de reconciliação com responsável e reprocessamento controlado, e rollback que suspende a escrita externa mantendo a captura local. Ficam fora negociação autônoma, alteração automática de campanhas, automação de pós-venda, substituição do Kommo/Lóvavel/Polisystem e escrita em ferramenta não validada.

Regras: a integração não sobrescreve dado conflitante sem regra aprovada; evento repetido não cria nova oportunidade; erro de escrita mantém a origem, entra na fila de reconciliação e nunca é marcado como sucesso. Segredos ficam fora do repositório (secret manager); logs são sanitizados (sem credencial ou token). Allowlist explícita como autoridade de permissão (EV-F3-07); migrations aditivas e limpas.

## Fluxo de execução

1. Champion registra B4-01, B4-02 e B4-05 (decisões humanas; insumos embutidos na task `7953f975`).
2. Prova técnica timeboxed do conector em conta de teste: leitura e escrita com identificador externo, sem massa real.
3. Executor implementa a sincronização com fixtures sintéticos: evento repetido idempotente, conflito não sobrescrito, falha → fila de reconciliação, rollback suspende escrita e mantém captura local.
4. Teste humano do Champion; aceite formal em task separada; publicação somente após autorização explícita.

## Critérios de aceite

- **CA-4-001:** cada integração ativa possui campos, identificador externo, permissões, tratamento de erro e rollback documentados.
- **CA-4-002:** um evento repetido não cria duplicidade no destino validado (idempotência provada por replay).
- **CA-4-003:** falha de escrita mantém a origem, entra em reconciliação com dono e evidência, e não é marcada como sucesso.
- **CA-4-004:** dado conflitante não é sobrescrito sem regra aprovada.
- **CA-4-005:** rollback suspende a escrita externa e preserva a captura local; permissão insuficiente é recusada com registro.

## TDD da SPEC

- **RED:** hoje não há integração — lead/agendamento não chegam à ferramenta comercial sem cópia manual; não existe fila nem rollback.
- **GREEN:** fixture sintético (2 eventos iguais, 1 conflito, 1 falha de escrita) produz exatamente 1 oportunidade no destino, conflito preservado na origem com pendência, falha na fila com dono e nenhum sucesso falso.
- **REGRESSÃO:** replay do mesmo lote não duplica; rollback suspende escrita mantendo a captura; credencial inválida ou permissão negada registra erro sem vazar segredo; timeout entra na fila.

Evidências: contrato de campos aprovado, logs sanitizados, estado da fila, provas negativas e aceite humano.

## Tasks vinculadas

| ID | Task | Critério | Pré-condição |
|---|---|---|---|
| `7953f975-0f69-42a0-a9a1-b028429550cb` | Definir contrato, acesso e fallback da integração | B4-01, B4-02, B4-05 | SPECs F4 aprovadas |
| `c86d168b-96c9-48ca-9eee-44e73a4ac648` | Configurar a integração em ambiente autorizado (subtarefa: provar conector em conta de teste) | CA-4-001..005 | B4-01/02/05 liberados |
