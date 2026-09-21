# AP-2026-09-21-1049 — Limpeza pós-aceite deve restaurar fixtures-base alteradas pelo teste

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-008 / SPEC-2-002
- Sinal: o teste humano operou uma fixture-base anterior à task; o fechamento precisou remover os dados da task e restaurar explicitamente os campos/eventos da fixture-base ao estado pós-task anterior.
- Evidência: migração 0046 aplicada no Skip (`fca545d`), com remoção seletiva de fixtures/debug/revalidação, preservação das fixtures-base e restauração de `appt-teste-0004`; logins sintéticos retornaram HTTP 400 após a limpeza.
- Regra reutilizável: antes da limpeza pós-aceite, separar dados criados pela task de fixtures-base apenas alteradas durante a prova; apagar os primeiros e restaurar os segundos por âncoras explícitas, preservando eventos de tasks anteriores.
- Quando aplicar: em toda task que usa fixtures compartilhadas e altera estado durante teste humano.
- Quando não aplicar: quando a fixture for criada exclusivamente pela task e tiver rollback/âncora própria, sem histórico anterior a preservar.
- Confiança: alta — limpeza aplicada e migração 0046 confirmada como `applied`.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
