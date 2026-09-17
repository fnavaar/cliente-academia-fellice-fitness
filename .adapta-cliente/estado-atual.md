# Estado atual — Adapta Cliente

- fase: 2
- task_id: F2-IMP-007
- champion: Karol e Márcio
- spec: 04_fase-atual/specs/spec-2-002-visao-operacional-tentativas.md
- etapa: aguardando_teste_humano
- autorizacao_implementacao: confirmada — 2026-09-17, Ricardo Junior: "vamos prosseguir" (após relatório de análise da F2-IMP-007)
- teste_humano: pendente — entrar na /visao com o login consultor enviado no chat, clicar "Assumir caso" na tentativa "Lead Fila Teste" e conferir dono/hora; tentar com o login sem permissão e ver o bloqueio
- teste_humano_detalhe: botão Assumir na /visao (só ENCAMINHAMENTO_HUMANO sem dono — fila única); dono + assumed_at gravados pelo servidor + evento APPOINTMENT_ASSUMED na trilha; hook recusa troca/remoção de dono sem reatribuição formal (F2-IMP-008); papel gestao bloqueado na leitura e escrita (regra da coleção — 404, sem vazamento)
- verificacao_automatica: passou — v0.0.66, pipeline ok; provas ao vivo: assunção via API (dono+assumed_at gravados, status preservado), troca de dono recusada 400, remoção de dono recusada 400, evento APPOINTMENT_ASSUMED criado, papel gestao sem leitura (0 itens) e sem escrita (404), /visao 200
- aprendizado: pendente
- ultima_acao: F2-IMP-007 implementada — assunção com dono/assumed_at + bloqueio por papel (CA-2.07 + CA-2.09)
- proxima_acao: teste humano pelo consultor; após aceite, limpeza (0039: assunção da prova + tentativa de teste + usuários sintéticos) e liberação da F2-IMP-008
- gate: aceite humano antes de liberar F2-IMP-008
- limite: nenhuma publicação em produção, integração externa ou Fase 3 autorizada; reatribuição/escalada/rollback são a F2-IMP-008
- atualizado_em: 2026-09-17T18:10:00-03:00
