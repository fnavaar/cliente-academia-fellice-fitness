# Tasks gerais — Fase 4

Tabela operacional da Fase 4 (projeção compatível com `00.tasks_per_fase/fase_4.md`, fonte canônica dos cards). Tasks novas aguardam UUID do sincronizador ("id pendente").

## Tasks

| ID | Task | Dono | SPEC | Critério | Checklist-aceite | Recorte da prova | Status | Evidência |
|---|---|---|---|---|---|---|---|---|
| `7953f975-0f69-42a0-a9a1-b028429550cb` | Definir contrato, acesso e fallback da integração | Cliente | SPEC-4-001 | B4-01, B4-02, B4-05 | [ ] base legal/escrita externa registrada [ ] ferramenta (Kommo/Lóvavel/ambas) + credenciais registradas [ ] campos/identificador/regra de conflito registrados | Decisões documentais com data e confirmação verificável | A fazer | — |
| `c86d168b-96c9-48ca-9eee-44e73a4ac648` | Configurar a integração em ambiente autorizado | Cliente | SPEC-4-001 | CA-4-001..005 | [ ] contrato documentado [ ] replay idempotente [ ] conflito não sobrescrito [ ] falha em reconciliação com dono [ ] rollback preserva captura | Fixtures sintéticos (2 iguais, 1 conflito, 1 falha) + conta de teste autorizada | A fazer | — |
| id pendente | Registrar a matriz de acesso do painel de saúde | Karol e Márcio | SPEC-4-002 | B4-03 | [ ] papéis permitidos e negados registrados | Decisão documental com data e confirmação verificável | A fazer | — |
| id pendente | Congelar o baseline e aprovar o alvo do loop | Karol e Márcio | SPEC-4-003 | B4-04 + alvo | [ ] versão de baseline congelada (B3-05) [ ] alvo aprovado com a Gestão | Decisão documental com data e confirmação verificável | A fazer | — |
| `31dae29a-884a-4ac6-a23a-2cfc5b0e56a8` | Configurar o loop de saúde da conversão | Cliente | SPEC-4-003 | CA-4-011..014 | [ ] ciclo registra baseline/cobertura/achado/veredito [ ] alvo inativo sem aprovação [ ] prova negativa de escrita externa [ ] falha interrompe e abre pendência | Fixture com baseline congelado + 2 ciclos sintéticos | A fazer | — |
| id pendente | Configurar o painel de saúde da integração | Karol e Márcio | SPEC-4-002 | CA-4-006..010 | [ ] fila/falhas/donos visíveis [ ] histórico somente-adição [ ] papel fora da matriz negado (UI/URL) [ ] divergência vira pendência [ ] degradação sem dado inventado | Fixtures de fila (2 pendentes, 1 reprocessado, 1 falha) + provas negativas | A fazer | — |
| `12bf95df-e79a-4ef2-b4f1-214fc65c3cbb` | Executar um ciclo e provar recuperação | Cliente | SPEC-4-003 | CA-4-011/014 (regressão) | [ ] ciclo real registrado com veredito [ ] falha simulada interrompe recomendações [ ] pendência aberta com responsável | Ciclo semanal real + falha simulada de medição/conector | A fazer | — |
| `c5ccd038-0cae-4e1d-9d72-52e2d3ef935d` | Revisar os ciclos e decidir o fechamento da Fase 4 | Felipe Navaar | Fase 4 (todas) | CA-4-001..014 | [ ] evidências conferidas [ ] provas negativas conferidas [ ] vereditos humanos conferidos [ ] aceite ou correções registrados | Revisão documental do consultor | A fazer | — |
