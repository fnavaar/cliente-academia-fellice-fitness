# AP-2026-09-17-1947 — filtro na página não substitui enforcement no servidor

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-004 / SPEC-2-001 (debug, rodada 2)
- Sinal: (1) Esconder slot cheio na página NÃO é controle de capacidade — o contador precisa ser atualizado por quem cria a reserva (hook de servidor em create/update/delete) e a recusa precisa acontecer no servidor, senão qualquer chamada direta à API contorna o limite. (2) No JSVM do PocketBase, callbacks de hook executam em pool separado: declarações de topo (funções/constantes) NÃO são visíveis dentro dos callbacks — o guardrail do Skip rejeita o deploy; toda a lógica deve ser inline em cada callback. (3) Hook de model (onRecordCreate/Update/Delete) roda em qualquer salvamento, inclusive migrações — usar e.next() antes dos efeitos pós-gravação e BadRequestError para recusar. (4) Contador materializado fica defasado quando a regra muda — migração de ressincronização após ativar o hook. (5) Fixture apontando para slot inexistente faz capacityOf() cair no default 1 — recusa "correta" por motivo errado; sanidade de referências faz parte do teste.
- Evidência: reteste humano reproduziu 3 reservas em slot cap 2 mesmo após a rodada 1 (página escondia, servidor aceitava); v0.0.41 rejeitada pelo guardrail de escopo do JSVM; v0.0.42/0.0.43 passaram com provas ao vivo (400 em slot cheio, 200/200 na capacidade exata, 400 na 3ª, desistência liberou vaga).
- Regra reutilizável: todo limite de capacidade/vaga tem três partes obrigatórias — (a) validação no servidor que recusa, (b) contador atualizado automaticamente em cada escrita, (c) filtro na oferta (página). A página sozinha é cosmética.
- Quando aplicar: qualquer regra de lotação no Skip Cloud/PocketBase (agenda, turmas, estoque, cupos).
- Quando não aplicar: regras que só filtram leitura sem risco de escrita concorrente.
- Confiança: alta — falha reproduzida pelo reteste humano, causa demonstrada, correção provada ao vivo em todos os caminhos (create, update, delete).
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
