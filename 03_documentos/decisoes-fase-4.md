# Decisões da Fase 4 — Integração direta e saúde da conversão

**Estado deste registro:** coleta parcial atualizada em 09/10/2026. B4-01 permanece pendente; B4-02 permanece pendente porque as contas informadas por Ricardo não são contas de teste, permissões e prova técnica não foram validadas, e a combinação Kommo + Lovable relatada diverge do escopo nominal da SPEC (Kommo e/ou Lóvavel); B4-05 permanece pendente porque o destino foi descrito como Lovable ou a própria plataforma no Skip, o identificador externo não foi definido e a regra de unificação não tem confirmação verificável dos aprovadores requeridos. Ricardo revisou e aprovou a versão parcial anterior em 09/10/2026 às 11:59 (America/Bahia); as respostas novas às 15:50 ainda aguardam revisão documental. Nenhum gate foi liberado.
**Criado em:** 02/10/2026.  
**Atualizado em:** 09/10/2026.  
**Referência:** SPEC-4-001 e task `7953f975-0f69-42a0-a9a1-b028429550cb`.

Este documento reúne perguntas e respostas sem preencher lacunas por inferência. As informações datadas de 09/10 foram fornecidas por Ricardo via chat/formulário; quando a fonte não é diretamente o Champion ou o Comercial, isso é registrado como relato de Ricardo e não como aprovação direta desses responsáveis. Campo vazio, proposta ou relato sem aprovador/evidência não libera integração. Não incluir senhas, tokens, chaves, credenciais ou dados reais de leads neste arquivo, no repositório ou no chat; segredos só podem ser tratados pelo mecanismo autorizado, depois das aprovações aplicáveis.

Em 09/10/2026 às 11:59 (America/Bahia), Ricardo declarou: “ok, então tudo revisado e aprovo o registro parcial”. Essa aprovação cobriu a revisão documental da versão parcial então existente; não confirmou valores pendentes nem liberou B4-01, B4-02 ou B4-05.

Em 09/10/2026 às 15:50, Ricardo enviou respostas adicionais: base legal e escopo de escrita continuam PENDENTES; informou preferência por Kommo + Lovable e que existem contas nos dois serviços, mas não são de teste; permissões, prova técnica e identificador externo continuam PENDENTES; descreveu o destino de dados como Lovable “ou dentro da própria plataforma no Skip”; e relatou como “aprovada” uma regra de verificar nome completo e telefone e, se iguais, unificar todo o histórico. A identidade/função dos aprovadores e evidência verificável da aprovação não foram fornecidas. As contas não foram acessadas e nenhuma leitura, escrita ou prova de conector foi executada.

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

- **Status:** PARCIAL/PENDENTE — Ricardo indicou Kommo + Lovable; informou que há contas nos dois serviços, mas não são de teste. Permissões e prova técnica não foram verificadas. O destino Lovable/Skip e a divergência com o nome “Lóvavel” da SPEC precisam de esclarecimento de escopo.
- **Decisor:** Champion técnico; responsável pelo processo/negócio informado como Champion.
- **Ferramentas indicadas por Ricardo em 09/10 às 15:50:** “Kommo + Lovable”. Isso é registrado como ferramenta pretendida, não como escolha validada para execução. A SPEC-4-001 nomeia Kommo e/ou Lóvavel; não presumir que “Lovable” e “Lóvavel” sejam o mesmo produto, nem ampliar a SPEC por inferência. Registrar DÚVIDA de requisito até confirmação do consultor/Champion.
- **Responsável técnico informado anteriormente:** Karol. Responsável pelo processo/negócio: Champion.
- **Contas/ambiente:** Ricardo informou que existem contas no Kommo e no Lovable, mas “não é de teste”, e que poderiam ser usadas. Essa proposta não satisfaz a SPEC, que exige prova timeboxed em conta de teste sem massa real. Não acessar, ler, escrever ou testar nas contas mencionadas; confirmar ambiente segregado de teste e ausência de dados reais antes de qualquer prova.
- **Permissões disponíveis:** PENDENTE — registrar apenas escopos efetivamente validados (leitura e escrita necessários), nunca valores de segredos. Nenhuma validação foi informada.
- **Prova técnica:** PENDENTE/NÃO EXECUTADA — a SPEC requer prova timeboxed de leitura e escrita com identificador externo em conta de teste. Nenhuma prova foi declarada; não executar contra as contas informadas que não são de teste.
- **Decisão final B4-02:** PENDENTE até esclarecer o produto/destino dentro do escopo aprovado, confirmar ambiente isolado de teste e permissões, e registrar resultado da prova técnica timeboxed.

## B4-05 — Mapeamento de campos, identificador externo e conflitos

- **Status:** PARCIAL/PENDENTE — Ricardo descreveu o destino como Lovable “para registar o contato e as informações como crm. ou dentro da própria plataforma no skip”; não selecionou claramente entre esses destinos nem especificou objetos/campos. O identificador externo segue PENDENTE. A regra de unificação foi relatada como aprovada, mas faltam aprovadores e evidência exigidos pela task.
- **Aprovadores requeridos:** Comercial e Champion. Não foi apresentada confirmação verificável direta deles para o destino, identificador ou regra abaixo.
- **Rascunho de mapeamento a validar (não aprovado):**

| Campo/categoria de origem indicada | Ferramenta e campo de destino | Finalidade/necessidade mínima | Identificador externo e escopo | Regra para conflito/unificação relatada | Aprovação (quem/data/evidência) |
|---|---|---|---|---|---|
| Lead capturado — nome | Lovable ou plataforma Skip: destino/objeto/campo real PENDENTE; esclarecer qual é o alvo | Registrar contato e informações para continuidade do atendimento, conforme relato de Ricardo | PENDENTE — nome não é identificador técnico validado | Ricardo relatou regra de comparar nome completo e telefone e, se ambos iguais, unificar histórico; confirmação/aprovador e semântica pendentes | PENDENTE — Comercial e Champion |
| Lead capturado — telefone/WhatsApp | Lovable ou plataforma Skip: destino/objeto/campo real PENDENTE; esclarecer qual é o alvo | Possibilitar contato comercial, sujeito à validação da necessidade e base legal | PENDENTE — telefone + nome é critério de correspondência relatado, não identificador técnico aprovado; unicidade e registros prévios não validados | Idem; não executar mesclagem nem sobrescrita automática | PENDENTE — Comercial e Champion |
| Lead capturado — origem | Lovable ou plataforma Skip: destino/objeto/campo real PENDENTE; esclarecer qual é o alvo | Manter contexto da origem, sujeito ao contrato de dados aprovado | PENDENTE — identificador técnico principal e escopo não definidos | Não descartar nem reatribuir origem/histórico; eventual regra necessita auditoria, proveniência e rollback definidos | PENDENTE — Comercial e Champion |

- **Identificador externo escolhido:** PENDENTE. A correspondência “nome completo + telefone” foi relatada como critério de decisão para unificar, mas não define por si só um identificador técnico estável, unicidade, escopo ou comportamento idempotente. Não registrar como chave técnica aprovada.
- **Regra de conflito/unificação relatada em 09/10 às 15:50:** Ricardo informou: “aprovada, deverá verificar o nome completo e o telefone, caso sejam os mesmos, unificar todo o histórico.” Registro: relato de Ricardo de que houve aprovação; responsável(es), função(ões), data da decisão original e confirmação verificável do Champion/Comercial não foram apresentados. Portanto, o critério formal de evidência B4-05 ainda não está atendido.
- **Risco e salvaguarda:** “unificar todo o histórico” não define quais registros/eventos entram na fusão, precedência em campos conflitantes, preservação de origem/proveniência, tratamento de agendamentos/encaminhamentos duplicados, trilha de auditoria ou reversão. Igualdade de nome e telefone pode ser insuficiente para comprovar identidade em todos os casos; fusão indevida pode associar histórico a pessoa errada ou alterar atribuição. Até que os aprovadores e a regra técnica sejam explicitados e validados, não mesclar, sobrescrever ou reatribuir histórico; preservar registros e encaminhar conflitos a reconciliação humana.
- **DÚVIDA bloqueante B4-05:** confirmar se o sistema-alvo é o Lovable, a plataforma já existente no Skip, ou outro destino; identificar campos/objetos reais, chave externa e aprovações do Comercial/Champion. Não alterar SPEC-4-001 sem validação do consultor.

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
- 09/10/2026, 15:50 — Ricardo enviou respostas adicionais: B4-01 continua PENDENTE; ferramenta pretendida Kommo + Lovable; contas existentes mas não de teste; permissões e prova técnica pendentes; destino Lovable ou a própria plataforma no Skip; identificador externo pendente; regra de comparar nome completo + telefone e unificar histórico relatada como aprovada, sem identificação/evidência dos aprovadores. As contas não foram acessadas; não houve teste nem escrita externa. A revisão/aceite humano desta atualização permanece pendente.

Atualizar as decisões finais somente após validação/confirmacão verificável dos responsáveis, sem preencher lacunas por inferência.
