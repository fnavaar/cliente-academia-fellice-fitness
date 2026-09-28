# AP-2026-09-28-1611 — Aceites conflitantes: reler o estado do repositório antes de concluir

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: task `4217198c-8077-4769-b2c0-7b7482136553` (revisão de aceite da SPEC-3-001)
- Sinal: entre a entrega do aceite com ressalva (09:46) e a conferência humana (15:08), o dono da task registrou aceite sem ressalva superscrevendo o registro, reescreveu o pacote de evidências e marcou a task como concluída; concluir sobre a versão antiga geraria registro contraditório com o estado atual do repositório.
- Evidência: commits `871b35a` (aceite com ressalva), `acff4816`, `35380303`, `daea6a77` (aceite sem ressalva), `1ebc062e` e `b732d21c` (ajustes de processo) no repositório do cliente, com autores e horários verificáveis.
- Regra reutilizável: antes de concluir uma task, reler `fase.md`, estado, `STATUS.md` e o(s) arquivo(s)-alvo no momento da conclusão; se um aceite/registro foi superscrito por outro ator humano, interromper e perguntar qual registro prevalece antes de escrever.
- Quando aplicar: qualquer fechamento de task em repositório compartilhado onde consultor/Champion também escrevem.
- Quando não aplicar: repositórios de escrita exclusiva ou mudanças paralelas apenas cosméticas que não tocam o registro em conclusão.
- Confiança: alta — sequência de commits com horários e autores verificáveis.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
