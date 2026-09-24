# AP-2026-09-24-1434 — taxonomia UTM exige regra por parâmetro

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: B3-01 / SPEC-3-001
- Sinal: a decisão inicial deixou `utm_medium` ambígua; a task só pôde ser registrada depois que source, medium, campaign, granularidade, ausências e confirmação foram explicitados separadamente.
- Evidência: `03_documentos/decisoes-fase-3.md`, commit `e97835428403b5d6ef56c5d5eda27d2cc93abb15`.
- Regra reutilizável: não liberar taxonomia de atribuição por uma frase genérica; exigir regra operacional para cada parâmetro, granularidade, tratamento de ausências e confirmação verificável.
- Quando aplicar: em qualquer decisão de origem, campanha, UTM ou agrupamento que seja pré-condição para agregação ou dashboard.
- Quando não aplicar: não substitui a decisão humana sobre fórmula da métrica, janela, vínculo triagem→agendamento, matriz de acesso ou baseline.
- Confiança: alta — decisão registrada no documento canônico e task concluída sem implementação.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto