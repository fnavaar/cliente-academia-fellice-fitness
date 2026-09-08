# Debug Summary — F1-T007 — 2026-09-08

- **Sintoma:** preview carregava uma tela em branco.
- **Reprodução:** `src/pages/Index.tsx` continha somente um `div` vazio; snapshot inicial não apresentava campos nem ações.
- **Causa raiz:** a rota `/` renderizava um placeholder vazio e não havia interface conectada ao backend.
- **Correção:** interface de triagem implementada em `src/pages/Index.tsx`; `VITE_POCKETBASE_URL` configurada pelo backend oficial do Skip; fixture idempotente de formulário e versão criada em `0003_seed_lead_capture_fixture.js`.
- **Verificação automática:** Skip QA 0.0.5 passou em setup, análise estática, build, integrações e testes. Migração 0003 aplicada. Preview renderiza os campos e opções aprovados. POST sintético direto para `lead_submissions` e `lead_submission_events` retornou HTTP 200.
- **Limitação:** a automação do navegador não exibiu a mensagem visual de confirmação após o clique, embora os POSTs diretos tenham sido aceitos; requer validação humana no navegador.
