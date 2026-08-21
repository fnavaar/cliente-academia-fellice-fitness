# SPEC-1-001 — Captura e triagem rastreável de lead de tráfego

**Fase:** 1  
**Status:** bloqueada — configuração operacional pendente  
**Dono:** Champion do cliente e liderança Comercial  
**Origem no escopo:** D-001, RQ-001 e Fase 1 de `03-Projeto/02-Escopo-Definitivo.md`  
**Degrau da solução:** recurso nativo da plataforma de pré-agendamento — a primeira entrega usa formulário, armazenamento de respostas, versões e eventos da própria plataforma; não integra Kommo, Lóvavel ou agenda nesta fase.

## Contexto e decisões fechadas

- **Estado atual:** leads de tráfego entram na jornada comercial por canais digitais; a triagem observada já usa nome, origem e objetivo, mas a atribuição de campanha e o contexto chegam de forma incompleta ao Comercial. Fontes: `03-Projeto/requisitos.md` §RQ-001 e `04-Mapeamento-Processos/01-Videos/Analise - Teste 2.md` §§2–3.
- **Estado desejado:** existe um formulário identificável e versionado que captura uma triagem estruturada, preserva parâmetros de origem/campanha quando recebidos e torna abandono, dado ausente e conclusão visíveis.
- **Decisões já fechadas:** o recorte é pré-agendamento de leads de tráfego; não há IA, integração de escrita externa, agenda confirmada, mudança de campanha ou descarte automático. Um pedido de ajuda humana nunca é bloqueado por regra de qualificação.
- **Bloqueios:** a plataforma, a URL de produção e o responsável por publicar a versão não estão registrados nas fontes. Também faltam o texto final e as opções fechadas de `objetivo`, `proximidade`, `ocupacao` e `interesse_em_visita`. O Ethos pode preparar o roteiro de teste, mas deve parar antes de criar, testar ou ativar formulário até o Champion e o Comercial registrarem esses itens.

## BLOQUEIOS executáveis

| Informação necessária | Dono da decisão | Por que bloqueia | Evidência para liberar |
|---|---|---|---|
| Plataforma, URL de teste/produção e publicador da versão | Champion | Sem a superfície autorizada, o executor teria de escolher tecnologia e destino. | Nome da plataforma, URL e papel/usuário de publicação registrados no plano. |
| Texto, ordem, opções e obrigatoriedade finais de `objetivo`, `proximidade`, `ocupacao` e `interesse_em_visita` | Liderança Comercial | Sem o contrato de respostas, a triagem e a validação seriam inventadas. | Tabela de campos aprovada pelo Comercial. |
| Texto de privacidade/consentimento aplicável à coleta de contato | Champion | O formulário coleta dado de contato e não pode publicar aviso por inferência. | Texto ou referência exata aprovada pela operação. |

## Resultado observável

Um lead consegue abrir uma versão identificada do formulário, informar o contexto mínimo da triagem e concluí-lo. A operação enxerga `form_id`, `form_version`, momento de início/conclusão, origem/campanha recebida ou sua ausência, respostas, estado de triagem e pedido de ajuda humana. Um abandono permanece identificável sem fabricar uma resposta.

Nesta fase, “qualificação estruturada” significa coleta consistente dos sinais abaixo; não significa reprovar comercialmente um lead nem confirmar uma visita. A confirmação de agenda pertence à Fase 2.

## Limites e dependências

- **Inclui:** formulário de entrada, validação local, controle de versão, captura de atribuição, registro de eventos e estados de triagem.
- **Fora de escopo:** criação/escrita em Kommo, Lóvavel ou Polisystem; agenda, reserva, envio de mensagem, IA, alteração de campanha, decisão automática de elegibilidade e exclusão de dados.
- **Entradas e pré-condições:** URL de ambiente de teste; plataforma e proprietário de publicação indicados pelo champion; texto de privacidade/consentimento aprovado pela operação; formulário anterior preservado quando houver substituição.
- **Saídas/artefatos:** formulário publicado somente após gate humano, tabela/visão de respostas e eventos, configuração de versão e roteiro de evidências da SPEC.
- **Dependências e responsáveis:** Champion fornece plataforma, URL e autorização de publicação; Comercial aprova a redação de perguntas e opções; executor registra a versão e a evidência; Consultor Comercial consome o contexto na SPEC-1-002.
- **Atores e permissões mínimas:** Lead pode preencher; Consultor Comercial lê somente registros encaminhados a ele; Champion pode aprovar/publicar versões; Marketing lê apenas agregados futuros, não dados de contato individuais.
- **Superfícies/arquivos/configurações afetadas:** configuração da plataforma de pré-agendamento; este arquivo; `01-SPECs/00-INDICE.md`; `matriz-de-rastreabilidade.md`. A ferramenta de produção específica será informada antes da ativação.
- **Risco e plano B:** se a plataforma ou a publicação não estiverem disponíveis, manter o formulário atual e registrar o inventário de campos/eventos para retomada; não coletar dados em planilha paralela sem autorização.
- **Rollback ou reversão:** desativar somente a versão nova, reativar a versão anterior e preservar registros/eventos já capturados com seu `form_version`.

## Dados e integrações

| Origem/destino | Fonte de verdade | Campos/contrato | Autenticação/permissão | Timeout/retry/idempotência | Tratamento de erro |
|---|---|---|---|---|---|
| Lead → plataforma de pré-agendamento | Plataforma, nesta fase | `lead_submission_id`, `form_id`, `form_version`, `started_at`, `submitted_at`, `nome`, `telefone_ou_canal_de_retorno`, `objetivo`, `proximidade`, `ocupacao`, `interesse_em_visita`, `precisa_de_ajuda_humana`, `utm_source`, `utm_medium`, `utm_campaign`, `attribution_status`, `triagem_status` | Lead sem acesso administrativo; Champion publica; Comercial lê somente encaminhamentos | Nenhuma chamada externa. Reenvio do formulário cria nova submissão identificada; não sobrescreve a anterior. | Campo obrigatório ausente impede conclusão; parâmetros todos ausentes geram `attribution_status=ausente`; parâmetros parciais geram `incompleta`; falha de salvamento mostra erro e não apresenta confirmação. |

| Regra de negócio | Condição | Ação/resultado | Exceção | Fonte |
|---|---|---|---|---|
| RN-1.01 | Formulário aberto | Registrar `started_at`, `form_id` e `form_version`; capturar parâmetros de campanha recebidos sem inventá-los | Sem parâmetros, marcar atribuição ausente; conjunto parcial, `incompleta` | Escopo definitivo §4; RQ-001 |
| RN-1.02 | Lead informa nome, canal de retorno e objetivo | Permitir envio quando os três forem válidos | Dado obrigatório ausente impede conclusão e explica qual campo corrigir | RQ-001; escopo base §10.3 |
| RN-1.03 | Lead informa proximidade, ocupação e interesse em visita | Persistir a resposta como sinal de triagem; não converter em reprovação automática | “Outro” ou resposta não prevista permanece legível para humano | Kickoff Call, linhas 65–69; escopo base §10.3 |
| RN-1.04 | Lead pede ajuda humana | Persistir `precisa_de_ajuda_humana=true` e entregar o fluxo à SPEC-1-002 | Nenhuma regra de qualificação bloqueia o pedido | Escopo definitivo §4 e Fase 1 |
| RN-1.05 | Lead abandona antes do envio | Manter apenas evento de início e estado `ABANDONADO` quando a plataforma o suportar; não criar lead qualificado | Se não houver suporte nativo a abandono, registrar esta limitação na evidência e não inferir abandono | Escopo definitivo, Fase 1 |

## Fluxo e regras

1. O lead abre a URL de uma versão ativa; a plataforma registra identificação, versão e parâmetros de atribuição recebidos.
2. O formulário mostra uma pergunta por etapa ou uma única tela simples, sem exigir cadastro externo; a apresentação precisa permanecer legível para público com menor familiaridade digital.
3. O lead informa nome, canal de retorno, objetivo, proximidade, ocupação, interesse em visita e se precisa de ajuda humana.
4. Ao enviar dados válidos, a plataforma cria uma submissão imutável, registra `TRIAGEM_CONCLUIDA` e apresenta o próximo passo: encaminhamento humano se solicitado; caso contrário, continuação de pré-agendamento sem confirmar horário.
5. Se o envio falhar, a tela não confirma recebimento e oferece nova tentativa sem duplicar silenciosamente a submissão anterior.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Todos os campos obrigatórios preenchidos | Submissão recebe identificador, versão, respostas e eventos; status `TRIAGEM_CONCLUIDA` | N/A |
| Limite | Origem/campanha ausente ou parcial | Submissão é aceita com `attribution_status=ausente` ou `incompleta`; o dado não é substituído | Relatório futuro mantém o registro sem atribuição visível |
| Falha | Nome, retorno ou objetivo ausente; ou salvamento falha | Não há confirmação; campo é apontado ou erro de salvamento é mostrado | Corrigir e reenviar; confirmar que apenas uma submissão foi criada |
| Recuperação | Nova versão apresenta defeito após publicação | Versão nova é desativada e a anterior reativada | Guardar a evidência e abrir incidente antes de nova publicação |

## Instruções de execução para o Ethos

1. **Ler antes de alterar:** `02-Escopo-Definitivo.md` §§3–6, esta SPEC, `requisitos.md` §RQ-001 e `check-escopo.md`.
2. **Alterar somente:** configuração de formulário, eventos e versão no ambiente autorizado pelo champion; índice e matriz deste plano.
3. **Não alterar:** Kommo, Lóvavel, Polisystem, campanhas, agenda, permissões de outros sistemas, mensagens comerciais ou dados históricos.
4. **Executar nesta ordem:** confirmar plataforma/URL/dono → criar versão de teste → configurar campos e estados → executar TDD com dados sintéticos → obter aceite humano → publicar somente a versão aprovada.
5. **Parar e pedir validação quando:** não houver plataforma/URL/dono; algum campo/opção não tiver sido aprovado pelo Comercial; a ação publicar, enviar mensagem ou conectar conta for solicitada; a plataforma não puder preservar versão e submissão.
6. **Estado válido ao parar:** versão anterior continua ativa ou ambiente de teste isolado; nenhum dado real foi encaminhado nem escrito em sistema externo.

## Checklist de execução

- [ ] Champion indicou plataforma, URL de teste/produção e responsável de publicação.
- [ ] Comercial aprovou texto, ordem, opções e obrigatoriedade de cada campo deste contrato.
- [ ] Champion aprovou o texto de privacidade/consentimento para a coleta de contato.
- [ ] Versão de teste identifica `form_id` e `form_version` em toda submissão.
- [ ] Cenários principal, atribuição ausente, dado inválido, pedido de ajuda e abandono foram exercitados.
- [ ] Evidências foram anexadas sem expor dados pessoais além do necessário.
- [ ] Aceite humano da versão de produção foi registrado antes de publicar.

## Critérios de aceite

- [ ] **CA-1.01:** Uma submissão válida guarda `form_id`, `form_version`, horários, respostas mínimas e estado `TRIAGEM_CONCLUIDA`.
- [ ] **CA-1.02:** Uma submissão sem `utm_source`, `utm_medium` ou `utm_campaign` continua identificável e exibe atribuição ausente, sem valor inventado.
- [ ] **CA-1.03:** Campo obrigatório ausente ou inválido não gera confirmação nem submissão concluída.
- [ ] **CA-1.04:** Pedido de ajuda humana fica explícito e preserva todas as respostas enviadas para a SPEC-1-002.
- [ ] **CA-1.05:** A troca de versão preserva registros anteriores e permite retornar à versão anterior sem apagar eventos.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Tentar enviar formulário sem nome, retorno e objetivo | No ambiente de teste, deixar cada campo obrigatório vazio em tentativas separadas | Envio bloqueado; campo e mensagem de correção visíveis; nenhuma submissão concluída | Captura de tela e lista de submissões de teste |
| GREEN | Enviar fixture `lead_valido_com_atribuicao` | Preencher todos os campos com dados sintéticos e UTM válidas | Uma submissão com identificador, versão, respostas, eventos e `TRIAGEM_CONCLUIDA` | Captura da confirmação e registro da submissão |
| REFACTOR/REGRESSÃO | Testar `lead_sem_atribuicao`, `pedido_humano`, abandono e troca de versão | Executar os quatro cenários em versão de teste e, após aprovação, comparar versão anterior/nova | Ausência é explícita, pedido humano é preservado, abandono não é confirmação e versão anterior continua consultável | Roteiro assinado pelo Champion e evidências do ambiente |

**Dados/fixtures:** usar somente dados sintéticos: `Lead Teste A`, telefone fictício, objetivo `saúde e bem-estar`, proximidade `trabalha na região`, ocupação `outro`, interesse `sim`, UTMs válidas ou ausentes.  
**Caminhos de erro obrigatórios:** campo obrigatório vazio, contato inválido, UTM ausente/inválida, falha de salvamento, submissão repetida, abandono e troca de versão.  
**Evidência exigida:** capturas do ambiente de teste, export/visualização sem dados pessoais reais, `form_id`/versão e aceite humano antes da publicação.

## Handoff e operação

- **Como demonstrar:** preencher os fixtures válidos, sem atribuição e com pedido de ajuda; mostrar a submissão, versão, estado e eventos; trocar para a versão anterior em teste.
- **Como operar depois:** Champion aprova publicações; Comercial revisa a configuração de campos antes de cada nova versão; Consultor Comercial usa somente o contexto entregue pela SPEC-1-002.
- **Como monitorar:** volume de início, conclusão, abandono, atribuição ausente e pedidos de ajuda; não interpretar conversão até a Fase 3.
- **Pendência conhecida:** plataforma, URL e dono de publicação devem ser fornecidos antes da execução; isso não autoriza conexão ou publicação por inferência.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F1-T001 | Registrar plataforma, URLs e papel de publicação | Champion do cliente | SPEC-1-001 | Plataforma, URLs e publicador estão registrados. | Primeiro bloqueio executável. | Referência da plataforma/URLs e papel publicador. | Decisão do Champion. | bloqueada |
| F1-T003 | Registrar contrato de campos da triagem | Liderança Comercial | SPEC-1-001 | Texto, ordem, opções e obrigatoriedade dos quatro campos estão aprovados. | Segundo bloqueio executável. | Tabela de campos aprovada. | Decisão da liderança Comercial. | bloqueada |
| F1-T004 | Registrar aviso de privacidade e consentimento | Champion do cliente | SPEC-1-001 | Aviso/consentimento aplicável ao contato está registrado. | Terceiro bloqueio executável. | Texto ou referência aprovada. | Decisão do Champion. | bloqueada |

## Emendas

<!-- Append-only (D19): mudanças aprovadas depois da geração. A história não é reescrita. -->

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
