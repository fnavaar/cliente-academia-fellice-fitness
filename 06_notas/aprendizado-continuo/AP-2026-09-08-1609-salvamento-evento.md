# AP-2026-09-08-1609 — Referência do useRef precisa ser um valor ao persistir

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F1-T007 / SPEC-1-001
- Sinal: o endpoint de submissão aceitava o registro, mas o evento de conclusão falhava quando o objeto `useRef` era enviado em vez de seu valor string.
- Evidência: Debug Summary em `06_notas/debug/debug-2026-09-08-falha-salvamento-evento.md`; QA 0.0.8; submissão e evento sintéticos retornaram HTTP 200 após a correção.
- Regra reutilizável: ao enviar IDs mantidos por `useRef` para APIs, usar explicitamente `.current` e validar separadamente cada requisição dependente.
- Quando aplicar: fluxos em que uma submissão grava um registro e depois grava eventos relacionados.
- Quando não aplicar: valores que não sejam refs ou APIs que recebam deliberadamente um objeto estruturado.
- Confiança: alta — causa reproduzida nos logs e correção confirmada por teste sintético.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
