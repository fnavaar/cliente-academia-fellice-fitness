# Estado atual — Adapta Cliente

- task_id: nenhuma
- champion: Karol e Márcio
- spec: nenhuma task ativa; SPEC-3-001 implementada no preview, aguardando revisão formal de aceite `4217198c-8077-4769-b2c0-7b7482136553`
- etapa: sem_task
- autorizacao_implementacao: confirmada — 2026-09-24 17:00, Ricardo Junior: "Autorizo implementar a consolidação da SPEC-3-001 conforme o plano analisado."
- teste_humano: aprovado — 2026-09-25 16:39, Ricardo: "Conferi a janela isolada de 23/09: os valores batem com as fixtures da SPEC-3-001."; 2026-09-25 16:43, Ricardo: "Conferi o recálculo determinístico e o rollback/reativação da SPEC-3-001 no preview; os dois passaram."
- verificacao_automatica: passou — Skip preview v0.0.81 (96ce32e), QA completo; migrações 0050–0051 aplicadas; logs registram consulta autenticada da janela 23/09 e chamadas de controle com HTTP 200; harness isolado do hook confirmou partial=true, taxa nula e identificação da fonte quando a leitura de lead_submissions falha, sem escrita.
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-09-25-1646-janelas-isoladas-fixtures-funil.md
- ultima_acao: task `ab9ce40f-304e-4ef6-929f-1efa7f7a0a87` concluída no preview e registrada em 25/09/2026; produção continua não publicada; evidências da task em `changelog.md` e revalidação resumida em `STATUS.md`
- proxima_acao: em novo pedido, revisar formalmente a aceitação da SPEC-3-001 pela task `4217198c-8077-4769-b2c0-7b7482136553`, conferindo inclusive a captura do teste e o export sanitizado pedidos pela SPEC; não publicar em produção
- atualizado_em: 2026-09-25T16:56:40-03:00
