# AP-2026-10-16-1600 — Transcrição via MCP pode gravar conteúdo corrompido

- **Data/hora:** 2026-10-16T17:05:00-03:00 (incidente entre 16:53 e 17:02)
- **Task:** `7953f975` (registro documental das decisões B4)
- **Sintoma:** `create_or_update_file` aceito (HTTP 200) gravou 16.369 bytes com trechos corrompidos/deslocados (data "27/10", parágrafo duplicado, tabela truncada) em vez dos 26.124 bytes validados localmente; a resposta da API reportou sucesso — sucesso aparente não é prova de conteúdo.
- **Causa raiz:** a transcrição do conteúdo integral (~26 KB) na chamada da ferramenta degradou durante a geração; o `size` retornado (16.369 ≠ 26.124) foi o detector confiável.
- **Padrão de detecção:** conferir SEMPRE `size` e blob SHA retornados contra o hash local (`git hash-object` do arquivo validado) antes de considerar o commit íntegro; validar o estado final pela listagem de diretório da API (fonte autoritativa), não pelo raw.
- **Correção aplicada:** commit de reparo `8866d211` com nova transcrição dedicada do conteúdo validado + conferência do blob SHA (`52602b9d`) e size (26.124) pela API; commit `2423fa08` apenas documental.
- **Regra reutilizável:** para arquivos grandes via MCP, tratar cada gravação como não confiável até a conferência hash+size; se divergir, reparar em commit separado e revalidar; manter cópia local validada como fonte da verdade durante todo o ciclo; evitar reenvios repetidos de conteúdo grande (cada reenvio re-sorteia o risco de corrupção).
- **Relação:** mesma família do AP-2026-09-17-1608 (documentos cumulativos) e do padrão "artefato do MCP get_file_contents" (cabeçalho de 82 bytes / `\n` final) — agora no sentido de escrita, não de leitura.