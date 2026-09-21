# AP-2026-09-21-1725 — Reteste de preview UI exige hard refresh (Ctrl+F5)

- Status: candidato
- Escopo: projeto do cliente
- Task/SPEC: F2-IMP-009 r2 / SPEC-2-002 (debug-2026-09-21-f2-imp-009-dono-exibido-errado.md)
- Sinal: reteste humano repetiu um sintoma já corrigido porque a aba do navegador continuou executando o bundle anterior em cache (v0.0.77) — o servidor já servia a v0.0.78 com a correção. Mesmo padrão do reteste da F2-IMP-008 r2 (resolvido com Ctrl+F5): 2ª ocorrência confirmada.
- Evidência: trilha de eventos correta no banco (actor `z5wgyiffrdnv028`), bundle no preview sem o marcador antigo e com o novo, prova em navegador novo sem cache exibindo o comportamento correto.
- Regra reutilizável: antes de debugar (ou reabrir correção) por sintoma de UI em preview, exigir hard refresh (Ctrl+F5) ou janela anônima na versão mais recente; confirmar no relato qual build estava em execução. Servidor e bundle provados corretos deslocam a suspeita para o cache do cliente.
- Quando aplicar: qualquer reteste de UI no preview após nova versão publicada pelo pipeline.
- Quando não aplicar: falhas de servidor/API (não passam por cache de bundle) ou sintomas reproduzidos também em navegador novo.
- Confiança: alta — causa demonstrada por eliminação (servidor, bundle e navegador limpo) e precedência idêntica na F2-IMP-008 r2.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
