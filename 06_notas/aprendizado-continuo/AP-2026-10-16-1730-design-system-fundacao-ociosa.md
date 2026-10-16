# AP-2026-10-16-1730 — Fundação de UI pronta e ociosa: conferir o que o projeto já tem antes de instalar biblioteca

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: ciclo paralelo de design system (A+B, v0.0.89, commit 3a3bd99) — fora da task `7953f975`
- Sinal: o projeto Skip já trazia shadcn/ui completo em `src/components/ui/` (40+ componentes), ThemeProvider claro/escuro/system, react-hook-form + zod e Tailwind 3.4 mapeando tokens HSL; as 8 páginas usavam apenas classes manuais. A pesquisa de design systems externos (tweakcn, Origin UI, ReUI, Mantine, MUI) foi concluída antes de confirmar a stack interna.
- Evidência: listagem de `src/components/ui/` no projeto 51806; `package.json` (react-hook-form ^7.80.0, zod ^4.4.3, lucide-react); `components.json`; QA Skip completo passou em v0.0.89 (setup, estática, build, integrações); provas no preview (renderização, validação zod por campo, popover do select, modo escuro).
- Regra reutilizável: antes de pesquisar ou instalar biblioteca de UI nova, inventariar a fundação já presente no template (`src/components/ui/`, `components.json`, `package.json`) e medir o uso real por página; a melhoria visual mais barata costuma be adotar o que já existe, com tema via tokens CSS em vez de classes manuais.
- Quando aplicar: pedidos de "melhorar a interface" ou "integrar design system" em projetos Skip/React; auditoria de consistência visual.
- Quando não aplicar: quando a fundação instalada não cobre o caso (ex.: máscaras de input, data grid) — aí sim complementar com bibliotecas no padrão shadcn (Origin UI/ReUI) copiando arquivos.
- Confiança: alta — verificação direta do repositório e pipeline de QA verde.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
