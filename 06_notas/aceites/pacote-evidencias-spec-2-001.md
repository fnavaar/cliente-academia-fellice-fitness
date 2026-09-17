# PACOTE DE EVIDÊNCIAS — F2-IMP-005 · SPEC-2-001 (Agenda, disponibilidade e reserva)

**Data:** 2026-09-17 · **Preparado por:** Thor (copiloto operacional) · **Para:** Champion Karol e Márcio
**Natureza:** consolidação de evidências para aceite formal da SPEC-2-001. Todas as provas foram executadas no ambiente de teste do Skip 51806 com dados 100% sintéticos — nenhum dado pessoal real foi usado.

---

## 1. Estado do ambiente no fechamento

| Item | Valor | Verificado em |
|---|---|---|
| Projeto Skip | 51806 — Terrazzo R1 Sports Club (Zeus) | 2026-09-17 |
| Versão atual | v0.0.45 (pipeline QA completo ok) | 2026-09-17 |
| Preview | https://fellice-fitness-8733f--preview.goskip.app | HTTP 200 |
| Produção | https://fellice-fitness-8733f.goskip.app — **não publicada** | 2026-09-17 |
| Grade de teste | 248 slots (14 dias, seg–sex 08:00–19:30, sáb 09:00–13:30, blocos 30 min) | contagem via API |
| Reservas na base | 4 fixtures sintéticas (appt-teste-0001..0004) | contagem via API |
| Slots ocupados | 0 (ambiente limpo) | consulta via API |
| Rotas | / (triagem), /agendar (agenda do lead), /fila (atendente) | HTTP 200 |

## 2. Matriz critério de aceite → prova executada

### CA-2.01 — Tentativa concluída guarda todos os dados
- **Prova (F2-IMP-003, aceite humano 17/09):** página /agendar cria reserva `CONCLUIDO` com `appointment_id`, `lead_submission_id`, `slot_id`, `slot_datetime`, nome, telefone/canal, localidade e profissão; e-mail opcional.
- **Prova de baseline (17/09, hoje):** fixture `appt-teste-0001` conferida campo a campo via API autenticada — todos os campos presentes.
- **Resultado:** ✅ CUMPRIDO

### CA-2.02 — Concorrência: apenas uma confirmação por slot
- **Prova (F2-IMP-004, rodadas 1 e 2 de debug, 17/09):** fechadura de capacidade no servidor (hook `enforce_slot_capacity.js` em create/update/delete de `lead_appointments`) + índice único `(lead_submission_id, slot_id)` + página esconde slot cheio e bloqueia clique.
- **Resultados ao vivo:** 1ª e 2ª reserva em slot cap 2 → HTTP 200/200; 3ª no mesmo slot → **HTTP 400 "Este horário acabou de encher. Escolha outro, por favor."**; cenário do reteste humano (slot com 3 reservas em cap 2) reproduzido e recusado sem criar registro.
- **Resultado:** ✅ CUMPRIDO

### CA-2.03 — Campos mínimos impedem CONCLUIDO
- **Prova (F2-IMP-003, aceite humano 17/09):** a página /agendar recusa a confirmação sem nome, telefone/canal, localidade e profissão ("Preencha nome, canal de retorno, localidade e profissão para confirmar."); a tentativa permanece rastreável.
- **Observação registrada (não bloqueia):** a validação hoje é no fluxo da página (cliente). Via API direta, o servidor não rejeita CONCLUIDO sem campos mínimos — mesma natureza da falha de capacidade corrigida na F2-IMP-004. Recomendação de fortalecimento pós-aceite (nova task, novo ciclo).
- **Resultado:** ✅ CUMPRIDO no fluxo do lead (com observação)

### CA-2.04 — Desistência preserva histórico e libera o slot
- **Prova (F2-IMP-004, 17/09):** PATCH para `DESISTENCIA` → HTTP 200; eventos preservados; nova reserva no mesmo slot aceita (HTTP 200); contador de ocupação ressincronizado automaticamente pelo hook (2/2 após A+D).
- **Resultado:** ✅ CUMPRIDO

### CA-2.05 — Falha, timeout ou ausência de slots → ENCAMINHAMENTO_HUMANO
- **Prova (F2-IMP-003, aceite humano 17/09):** grade vazia → botão "Quero falar com um atendente"; falha de salvamento → fallback automático com `handoff_reason`; **nenhuma confirmação falsa é exibida**; estado `ENCAMINHAMENTO_HUMANO` com motivo registrado (fixture appt-teste-0004).
- **Resultado:** ✅ CUMPRIDO

## 3. Provas de segurança (transversais)

| Prova | Resultado |
|---|---|
| Leitura anônima de tentativas não vaza dados (lista vazia) | ✅ HTTP 200, 0 itens |
| Leitura autenticada (papel consultor) enxerga tentativas e eventos | ✅ |
| DELETE de reserva via API (mesmo autenticado) recusado — histórico protegido | ✅ HTTP 403 |
| Criação/alteração de slot sem login recusada | ✅ HTTP 400 |
| Escrita na ocupação restrita a champion/consultor | ✅ |

## 4. Pendências [VALIDAR NA CALL DE SETUP] — destacadas para decisão consciente do Champion

1. **LGPD — base legal do agendamento:** o consentimento da F1-T004 cobre comunicações; a base legal dos campos do agendamento (execução de serviço solicitado) precisa de validação com compliance. Flagrada desde a F2-IMP-001.
2. **RN-2.06 — semântica de reagendamento:** reescolha de slot atualiza a mesma tentativa (decisão de implementação); confirmar se é a semântica desejada pelo negócio.
3. **Capacidade 2 no sábado:** a regra da janela 11:30–16:30 é aplicada também aos blocos de sábado dentro da janela — confirmar se é a intenção do Subgerente Comercial.

## 5. Como este pacote foi verificado

- Pipeline QA completo do Skip a cada mudança (setup, análise estática, build, integrações, testes) — última execução v0.0.45, sem erros.
- Provas executadas por API contra o backend de teste do projeto, com login de verificação sintético.
- Commits de referência: fechadura de capacidade (hook + migrações 0018–0023), debug summaries em `06_notas/debug/`, aprendizados em `06_notas/aprendizado-continuo/`.
