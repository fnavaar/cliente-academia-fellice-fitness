# Debug Summary — 2026-09-08 — falha-salvamento-evento

- **Task:** F1-T007 — formulário de triagem, SPEC-1-001
- **Sintoma:** o formulário parecia salvar parcialmente, mas não concluía o fluxo de confirmação.
- **Reprodução:** logs do Skip Cloud mostraram POST de `lead_submissions` com HTTP 200 seguido de POST de `lead_submission_events` com HTTP 400.
- **Causa raiz:** o fluxo de conclusão enviava o objeto `useRef` `leadSubmissionId` no campo `lead_submission_id` do evento, em vez do valor string `leadSubmissionId.current`.
- **Correção:** substituição mínima em `src/pages/Index.tsx` para enviar `leadSubmissionId.current`.
- **Verificação:** QA Skip v0.0.8 passou em setup, análise estática, build, integrações e testes. Reprodução direta com payload sintético retornou HTTP 200 para submissão e evento.
- **Limitação do teste de tela:** a automação do navegador concatenou comandos em um campo durante a tentativa de preenchimento; a validação final foi feita diretamente no endpoint com o payload do formulário. O teste humano de tela continua obrigatório.
- **Produção:** não publicada.
