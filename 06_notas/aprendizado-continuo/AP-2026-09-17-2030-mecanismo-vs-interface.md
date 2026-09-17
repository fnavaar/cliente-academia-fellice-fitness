# AP-2026-09-17-2030 — aceite de SPEC com cenário sem tela: provar o mecanismo, não a interface

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-005 / SPEC-2-001 (fechamento)
- Sinal: em aceite de SPEC por cenários, um cenário pode depender de operação que ainda não tem tela (ex.: registrar desistência antes da visão operacional existir). Nesse caso o roteiro deve prever a prova pelo operador via API (o mecanismo existe, a interface vem depois) — e o aceite vale para o mecanismo, não para a tela. Documentar no roteiro qual cenário é do Champion e qual é do operador evita falso "pendente" no teste.
- Evidência: cenário 4 do roteiro da SPEC-2-001 marcado "pendente, não tem a opção de registrar desistência" pelo Champion via consultor; prova via API imediata (PATCH DESISTENCIA 200, evento ABANDONED, 3 eventos preservados, contador 2→1); aceite formal registrado com a ressalva explícita.
- Regra reutilizável: ao montar roteiro de aceite, separar cenários de interface (Champion) de cenários de mecanismo (operador via API) e declarar o escopo de cada um; nunca marcar um cenário como falha quando a lacuna é de escopo de outra SPEC.
- Quando aplicar: roteiros de aceite de SPEC com dependência entre SPECs da mesma fase.
- Quando não aplicar: quando a interface é exatamente o objeto do aceite.
- Confiança: alta — situação real do teste, resolvida sem retrabalho e documentada no recibo.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
