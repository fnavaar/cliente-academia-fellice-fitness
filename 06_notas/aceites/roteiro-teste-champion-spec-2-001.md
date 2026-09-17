# ROTEIRO DE TESTE DO CHAMPION — SPEC-2-001 (Agenda, disponibilidade e reserva)

**Para:** Karol e Márcio (Champions) · **Ambiente:** preview — https://fellice-fitness-8733f--preview.goskip.app
**Duração estimada:** 10–15 minutos · **Dados:** use nomes/telefones fictícios (ex.: "Teste Champion", "71 90000-0000")

---

## Cenário 1 — Reserva válida (CA-2.01)

1. Abra o **preview** e faça a triagem na página inicial (responda o formulário).
2. Na tela final da triagem, clique em **"Prefere escolher um horário? Agende aqui"**.
3. Na grade, escolha um horário com **"2 vagas"**.
4. Preencha nome, telefone, localidade (residencial/comercial) e profissão → **Confirmar meu horário**.
5. **Esperado:** tela verde "Horário reservado!" com **código da reserva**. Anote o código.
6. **Falha se:** não mostrar código, ou permitir confirmar sem os campos obrigatórios.

## Cenário 2 — Limite de vagas (CA-2.02)

7. Abra `/agendar` em **outra aba/anonimato** e repita a reserva **no mesmo horário** do passo 4.
8. **Esperado:** o horário agora mostra **"1 vaga"**; a reserva confirma (2ª vaga).
9. Recarregue `/agendar`: o horário deve ter **sumido da grade** (esgotado).
10. **Falha se:** o horário ainda aparecer com vaga, ou aceitar uma 3ª reserva.

## Cenário 3 — Campos obrigatórios (CA-2.03)

11. Escolha outro horário e, no formulário, deixe a **profissão vazia** e tente confirmar.
12. **Esperado:** mensagem pedindo os campos obrigatórios; **sem** reserva criada.

## Cenário 4 — Desistência libera a vaga (CA-2.04)

13. Peça ao operador (Ricardo) registrar a **desistência** da reserva do Cenário 1 (via painel/API) — ou pule este cenário se preferir ver depois.
14. **Esperado:** recarregar `/agendar` mostra o horário **disponível de novo**.

## Cenário 5 — Sem horário → atendimento humano (CA-2.05)

15. Na `/agendar`, role até o fim e clique **"Não encontrei um bom horário — prefiro falar com um atendente"**.
16. **Esperado:** tela "Vamos combinar o horário com você" — **sem** confirmação de reserva.

## Veredito

Ao final, responda no repositório (ou ao Ricardo registrar):
- **[ ] ACEITO** — a agenda de teste atende; SPEC-2-001 aceita.
- **[ ] REPROVADO** — descreva o que falhou; a task permanece aberta e vai para correção.

> Observação: o ambiente é de **teste** (grade sintética, dados fictícios). Nada é publicado em produção neste ciclo.
