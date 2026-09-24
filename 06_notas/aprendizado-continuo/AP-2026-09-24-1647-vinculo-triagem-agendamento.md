# AP-2026-09-24-1647 — vínculo de agendamento exige herança explícita

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: B3-03 / SPEC-3-001
- Sinal: as evidências da Fase 2 mostraram que a triagem concluída e o agendamento podem nascer com `lead_submission_id` distintos; o vínculo estrutural entre registros não garante herança do identificador de origem.
- Evidência: `06_notas/aceites/pacote-evidencias-spec-2-001.md`, `06_notas/aceites/pacote-evidencias-spec-2-002.md` e `03_documentos/decisoes-fase-3.md` (B3-03 concluída e aprovada por Ricardo).
- Regra reutilizável: distinguir vínculo estrutural de vínculo herdado; só atribuir agendamento à triagem quando o `lead_submission_id` de origem for preservado explicitamente; casos sem vínculo devem permanecer visíveis como cobertura incompleta, sem inferência.
- Quando aplicar: em qualquer consolidação ou funil que relacione triagem, encaminhamento e agendamento por identificador de origem.
- Quando não aplicar: não autoriza implementação técnica, não cria vínculo retroativo e não substitui decisão sobre tratamento de registros históricos sem `lead_submission_id`.
- Confiança: alta — a lacuna foi observada nas provas históricas e a regra foi registrada no documento canônico e aprovada humanamente.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto
