# Decisões da Fase 4 — Integração direta e saúde da conversão

**Estado deste registro:** coleta parcial atualizada em 09/10/2026. B4-01 permanece PENDENTE (base legal e escopo de escrita); B4-02 permanece PENDENTE (conta de teste, permissões e prova técnica não validadas); B4-05 permanece PENDENTE (mapeamento, identificador externo e evidência/detalhes da regra de unificação incompletos). Às 16:24, Ricardo informou Kommo + plataforma Skip e atribuiu a decisão a Karol (Champion), em 09/10; isto é relato de Ricardo, sem mensagem original da Karol e sem direção do fluxo definida. Nenhum gate foi liberado.
**Criado em:** 02/10/2026.  
**Atualizado em:** 09/10/2026.  
**Referência:** SPEC-4-001 e task `7953f975-0f69-42a0-a9a1-b028429550cb`.

Este documento reúne perguntas e respostas sem preencher lacunas por inferência. As informações datadas de 09/10 foram fornecidas por Ricardo via chat/formulário; quando a fonte não é diretamente o Champion ou o Comercial, isso é registrado como relato de Ricardo e não como aprovação direta desses responsáveis. Campo vazio, proposta ou relato sem aprovador/evidência não libera integração. Não incluir senhas, tokens, chaves, credenciais ou dados reais de leads neste arquivo, no repositório ou no chat; segredos só podem ser tratados pelo mecanismo autorizado, depois das aprovações aplicáveis.

Em 09/10/2026 às 11:59 (America/Bahia), Ricardo declarou: “ok, então tudo revisado e aprovo o registro parcial”. Essa aprovação cobriu a revisão documental da versão parcial então existente; não confirmou valores pendentes nem liberou B4-01, B4-02 ou B4-05.

Em 09/10/2026 às 15:50, Ricardo enviou respostas adicionais: base legal e escopo de escrita continuam PENDENTES; informou preferência por Kommo + Lovable e que existem contas nos dois serviços, mas não são de teste; permissões, prova técnica e identificador externo continuam PENDENTES; descreveu o destino de dados como Lovable “ou dentro da própria plataforma no Skip”; e relatou como “aprovada” uma regra de verificar nome completo e telefone e, se iguais, unificar todo o histórico. A identidade/função dos aprovadores e evidência verificável da aprovação não foram fornecidas. As contas não foram acessadas e nenhuma leitura, escrita ou prova de conector foi executada.

Em 09/10/2026 às 16:07 (America/Bahia), Ricardo declarou: “Revisei e aprovo somente como registro parcial”. A aprovação se limita à revisão documental das respostas registradas; não resolve a DÚVIDA de destino/escopo, não valida a autoridade nem os detalhes da regra de unificação e não libera B4-01, B4-02 ou B4-05.

Em 09/10/2026 às 16:24 (America/Bahia), Ricardo informou como destino “Kommo + plataforma Skip”. Para essa confirmação e para a aprovação da regra de unificação anteriormente relatada (conferir nome completo e telefone e, se iguais, unificar todo o histórico), atribuiu a decisão a “Karol - Champion - 09/10/2026”. Registro como informação relatada por Ricardo: não foi apresentada mensagem/citação original de Karol nem confirmação direta do Comercial. A resposta não define a direção do fluxo (Skip→Kommo, Kommo→Skip ou bidirecional), o mapeamento de campos, o identificador técnico, nem a semântica auditável e reversível da fusão. Nenhum gate foi liberado.

**Limite até liberação:** nenhuma credencial é ativada e nenhuma escrita externa é realizada com base neste rascunho. Contas que não são de teste não satisfazem a pré-condição de prova técnica em ambiente de teste da SPEC-4-001. Produção exige autorização própria.

## B4-01 — Base legal, minimização e autorização de escrita externa

- **Status:** PENDENTE — Ricardo respondeu “PENDENTE” tanto para validação da base legal quanto para escopo de escrita autorizado. Os insumos anteriores de finalidade e categorias de dados continuam sendo intenção/proposta, não decisão liberada.
- **Decisor:** Champion (Karol e Márcio); validação da base legal pelo responsável interno por privacidade/LGPD, ainda a identificar.
- **Base legal:** PENDENTE — não determinar por inferência. A validação do responsável interno precisa ser registrada antes de qualquer uso de dados reais.
- **Finalidade recebida anteriormente como insumo:** continuidade do atendimento comercial para leads recebidos por canais/formulários autorizados, incluindo registro, atualização e acompanhamento no CRM e eventual encaminhamento ao responsável pelo atendimento.
- **Dados mínimos pretendidos anteriormente:** nome, telefone/WhatsApp e origem do lead. Outros dados só mediante necessidade operacional comprovada e aprovação correspondente.
- **Escopo de escrita:** PENDENTE — nenhuma autorização verificável para dados de teste ou reais, campos/operações permitidos ou produção foi fornecida nesta resposta.
- **Atribuição anterior:** Ricardo informou em 09/10/2026: “autorizado por Karol”. A mensagem identificava Karol como fonte relatada, mas não incluía fala/mensagem direta verificável dela. Isso permanece como relato, não como confirmação direta da Champion.
- **Decisão final B4-01:** PENDENTE — requer validação explícita da base legal pelo responsável interno e confirmação verificável do Champion sobre minimização e escopo autorizado.

## B4-02 — Ferramenta, acesso e capacidade do conector

- **Status:** PARCIAL/PENDENTE — a resposta mais recente de Ricardo (16:24) indica Kommo + plataforma Skip e atribui a decisão a Karol (Champion) em 09/10; a fonte original não foi apresentada. Direção do fluxo, campos, ambiente de teste, permissões e prova técnica continuam pendentes. A conta Kommo havia sido informada por Ricardo como não sendo de teste.
- **Decisor:** Champion técnico; responsável pelo processo/negócio informado como Champion.
- **Ferramentas indicadas por Ricardo em 09/10 às 15:50:** “Kommo + Lovable”. Isso é registrado como ferramenta pretendida, não como escolha validada para execução. A SPEC-4-001 nomeia Kommo e/ou Lóvavel; não presumir que “Lovable” e “Lóvavel” sejam o mesmo produto, nem ampliar a SPEC por inferência. Registrar DÚVIDA de requisito até confirmação do consultor/Champion.
- **Atualização de 16:24:** Ricardo indicou o par “Kommo + plataforma Skip”, atribuindo a confirmação à Champion Karol em 09/10. Isto corrige a seleção mais recente relatada, mas permanece como atribuição de Ricardo até validação pela fonte original. A direção do fluxo e se a menção anterior a Lovable foi descartada ainda precisam de registro explícito; não presumir nem alterar a SPEC.
- **Responsável técnico informado anteriormente:** Karol. Responsável pelo processo/negócio: Champion.
- **Contas/ambiente:** Ricardo informou anteriormente que a conta Kommo (e a conta Lovable, então mencionada) não é de teste. A nova seleção Kommo + plataforma Skip não confirma a existência de conta/ambiente de teste para o Kommo, nem satisfaz a exigência da SPEC. Não acessar, ler, escrever ou testar nas contas existentes; confirmar ambiente segregado de teste e ausência de massa real antes de qualquer prova.
- **Permissões disponíveis:** PENDENTE — registrar apenas escopos efetivamente validados (leitura e escrita necessários), nunca valores de segredos. Nenhuma validação foi informada.
- **Prova técnica:** PENDENTE/NÃO EXECUTADA — a SPEC requer prova timeboxed de leitura e escrita com identificador externo em conta de teste. Nenhuma prova foi declarada; não executar contra as contas informadas que não são de teste.
- **Decisão final B4-02:** PENDENTE até registrar diretamente/validar a seleção Kommo + plataforma Skip, definir direção e escopos, confirmar ambiente isolado de teste e permissões, e registrar resultado da prova timeboxed. Nenhuma conta não-testes será usada.

## B4-05 — Mapeamento de campos, identificador externo e conflitos

- **Status:** PARCIAL/PENDENTE — a resposta mais recente de Ricardo indica Kommo + plataforma Skip e atribui a decisão à Karol/Champion (09/10); a mensagem original da Champion não foi apresentada. Direção Skip/Kommo, campos de destino, identificador externo e semântica da fusão seguem pendentes. A regra de unificação continua sendo um relato de aprovação, sem evidência original nem validação do Comercial.
- **Aprovadores requeridos:** Comercial e Champion. Ricardo atribuiu a confirmação do destino e a aprovação da regra à Karol (Champion), em 09/10; não apresentou a mensagem original/citação da Karol. Não há confirmação verificável do Comercial. Destino e regra permanecem relatos atribuídos, não evidência direta suficiente para liberar B4-05.
- **Rascunho de mapeamento a validar (não aprovado):**

| Campo/categoria de origem indicada | Ferramenta e campo de destino | Finalidade/necessidade mínima | Identificador externo e escopo | Regra para conflito/unificação relatada | Aprovação (quem/data/evidência) |
|---|---|---|---|---|---|
| Lead capturado — nome | Kommo + plataforma Skip informados; lado de origem/destino, objeto e campo real PENDENTES | Registrar contato e informações para continuidade do atendimento, conforme relato de Ricardo | PENDENTE — nome não é identificador técnico validado | Regra anteriormente relatada por Ricardo: conferir nome completo + telefone e, se iguais, unificar histórico; aprovação atribuída a Karol/Champion em 09/10, sem fonte original verificável e sem semântica detalhada | PENDENTE — validação direta do Champion e aprovação/evidência Comercial |
| Lead capturado — telefone/WhatsApp | Kommo + plataforma Skip informados; lado de origem/destino, objeto e campo real PENDENTES | Possibilitar contato comercial, sujeito à validação da necessidade e base legal | PENDENTE — nome + telefone é critério de correspondência relatado, não identificador técnico aprovado; unicidade e registros prévios não validados | Idem; não executar mesclagem nem sobrescrita automática | PENDENTE — validação direta do Champion e aprovação/evidência Comercial |
| Lead capturado — origem | Kommo + plataforma Skip informados; lado de origem/destino, objeto e campo real PENDENTES | Manter contexto da origem, sujeito ao contrato de dados aprovado | PENDENTE — identificador técnico principal e escopo não definidos | Não descartar nem reatribuir origem/histórico; eventual regra necessita auditoria, proveniência e rollback definidos | PENDENTE — validação direta do Champion e aprovação/evidência Comercial |

- **Identificador externo escolhido:** PENDENTE. A resposta das 16:24 indica o par Kommo + plataforma Skip, mas não identifica a chave técnica, unicidade, escopo ou comportamento idempotente. A correspondência “nome completo + telefone” permanece critério de associação relatado; não é identificador técnico aprovado.
- **Regra de conflito/unificação relatada:** Ricardo informou às 15:50: “aprovada, deverá verificar o nome completo e o telefone, caso sejam os mesmos, unificar todo o histórico.” Às 16:24, atribuiu essa aprovação a Karol (Champion), em 09/10/2026. Registro a autoria/aprovação como relato de Ricardo, pois não veio a mensagem original/citação da Champion; não foi apresentada validação do Comercial. A regra ainda não define escopo do “todo o histórico”, prevalência em conflitos, duplicidades, trilha de auditoria, proveniência, reversão nem o identificador técnico. Portanto, o critério formal de evidência B4-05 não está atendido.
- **Risco e salvaguarda:** “unificar todo o histórico” não define quais registros/eventos entram na fusão, precedência em campos conflitantes, preservação de origem/proveniência, tratamento de agendamentos/encaminhamentos duplicados, trilha de auditoria ou reversão. Igualdade de nome e telefone pode ser insuficiente para comprovar identidade em todos os casos; fusão indevida pode associar histórico a pessoa errada ou alterar atribuição. Até que os aprovadores e a regra técnica sejam explicitados e validados, não mesclar, sobrescrever ou reatribuir histórico; preservar registros e encaminhar conflitos a reconciliação humana.
- **DÚVIDA bloqueante B4-05:** a seleção mais recente relatada por Ricardo é Kommo + plataforma Skip; direção da sincronização, lado de origem/destino, objetos/campos reais, chave externa e evidência direta das aprovações ainda faltam. A menção anterior a Lovable fica preservada como histórico, mas não se assume que faça parte do destino atual. Não alterar a SPEC-4-001 nem executar integração até a confirmação verificável do consultor/Champion.

## Fallbacks e limites já definidos pela SPEC-4-001

Estas salvaguardas são requisitos documentais da SPEC; não são evidência de integração configurada ou de aprovação de dados:

- Falha, timeout ou permissão insuficiente: manter a captura de origem; registrar erro sanitizado e pendência/fila de reconciliação com responsável; nunca sinalizar sucesso falso nem expor segredo.
- Dado conflitante sem regra aprovada e tecnicamente definida aplicável: preservar a origem e encaminhar para reconciliação humana; não sobrescrever nem mesclar automaticamente.
- Rollback: suspender a escrita externa e preservar a captura local; qualquer futura estratégia de unificação precisará permitir auditoria e reversão aprovadas.
- Nenhuma credencial, conector, leitura de conta não-testes ou escrita externa é ativada por este documento.

## Histórico de confirmação

- 02/10/2026 — o rascunho foi criado sem respostas do Champion/Comercial.
- 09/10/2026 — Ricardo forneceu insumos parciais para B4-01/02/05. A base legal, esclarecimento sobre “lovable”, disponibilidade/permissões da conta de teste, prova técnica, campos finais de destino, identificador externo e aprovações verificáveis permaneceram pendentes. A atribuição “autorizado por Karol” foi registrada como relato de Ricardo, sem inventar fala direta de Karol. Nenhuma credencial, conector ou escrita externa foi ativada.
- 09/10/2026, 11:59 (America/Bahia) — Ricardo declarou “ok, então tudo revisado e aprovo o registro parcial”. A aprovação se restringiu à revisão documental da versão parcial daquele horário; não alterou o estado PENDENTE dos gates B4-01/02/05.
- 09/10/2026, 15:50 — Ricardo enviou respostas adicionais: B4-01 continua PENDENTE; ferramenta pretendida Kommo + Lovable; contas existentes mas não de teste; permissões e prova técnica pendentes; destino Lovable ou a própria plataforma no Skip; identificador externo pendente; regra de comparar nome completo + telefone e unificar histórico relatada como aprovada, sem identificação/evidência dos aprovadores. As contas não foram acessadas; não houve teste nem escrita externa.
- 09/10/2026, 16:07 (America/Bahia) — Ricardo declarou “Revisei e aprovo somente como registro parcial”. A revisão documental desta atualização está aprovada; B4-01/02/05 seguem pendentes, a DÚVIDA de escopo permanece bloqueante e nenhuma credencial, conta, conector, teste ou escrita externa foi autorizada.
- 09/10/2026, 16:24 (America/Bahia) — Ricardo informou “Kommo + plataforma Skip” como destino e atribuiu a confirmação a Karol (Champion), datada de 09/10/2026; atribuiu também a Karol a aprovação da regra anteriormente relatada de comparar nome completo + telefone e unificar o histórico. A origem foi registrada como relato de Ricardo, sem mensagem original da Champion nem confirmação do Comercial. Direção do fluxo, campos, identificador técnico, escopo/auditoria/reversão da unificação, base legal, conta de teste, permissões e prova seguem pendentes. Nenhuma conta foi acessada nem houve teste ou escrita externa.

Atualizar as decisões finais somente após validação/confirmacão verificável dos responsáveis, sem preencher lacunas por inferência.
