# Decisões da Fase 4 — Integração direta e saúde da conversão

**Estado deste registro:** coleta parcial atualizada em 09/10/2026. B4-01, B4-02 e B4-05 ainda não liberam integração: a base legal não foi validada; ferramenta/conta/permissões/prova técnica requerem confirmação; e o mapeamento completo e suas aprovações não foram apresentados. Ricardo aprovou a revisão documental do registro parcial em 09/10/2026 às 11:59 (America/Bahia), sem liberar esses gates.
**Criado em:** 02/10/2026.  
**Atualizado em:** 09/10/2026.  
**Referência:** SPEC-4-001 e task `7953f975-0f69-42a0-a9a1-b028429550cb`.

Este documento reúne as perguntas da task e as respostas recebidas, sem preencher lacunas por inferência. As informações de 09/10 abaixo foram fornecidas por Ricardo via chat; quando Ricardo atribui autorização a Karol, isso é registrado como relato de Ricardo, sem transformar a atribuição em citação direta da Karol. Campo vazio, proposta ou relato não equivale a aprovação verificável do Champion/Comercial nem libera integração. Não incluir senhas, tokens, chaves, credenciais ou dados reais de leads neste arquivo, no repositório ou no chat; segredos devem ser tratados somente pelo mecanismo autorizado, após aprovação aplicável.

Em 09/10/2026 às 11:59 (America/Bahia), Ricardo declarou: “ok, então tudo revisado e aprovo o registro parcial”. Essa aprovação se limita à revisão documental do estado parcial descrito aqui; não confirma os valores pendentes nem libera B4-01, B4-02 ou B4-05.

**Limite até liberação:** nenhuma credencial é ativada e nenhuma escrita externa é realizada com base neste rascunho. A integração também depende das pré-condições e provas técnicas definidas na SPEC-4-001; produção exige autorização própria.

## B4-01 — Base legal, minimização e autorização de escrita externa

- **Status:** PARCIAL — finalidade, categorias de dados e limite pretendido de teste recebidos como insumo de Ricardo em 09/10; base legal continua PENDENTE de validação pelo responsável interno de privacidade/LGPD. Não liberar escrita com leads reais nem produção.
- **Decisor:** Champion (Karol e Márcio); validação da base legal pelo responsável interno por privacidade/LGPD, a identificar.
- **Base legal:** PENDENTE — não determinar por inferência. A validação do responsável interno precisa ser registrada antes de qualquer uso de dados reais.
- **Finalidade recebida como insumo:** continuidade do atendimento comercial para leads recebidos por canais/formulários autorizados, incluindo registro, atualização e acompanhamento no CRM e eventual encaminhamento ao responsável pelo atendimento.
- **Dados mínimos pretendidos:** nome, telefone/WhatsApp e origem do lead. Outros dados só mediante necessidade operacional comprovada e aprovação correspondente.
- **Escopo de escrita pretendido:** inicialmente apenas ambiente de teste, sem massa real de leads, até que base legal, campos e escopo de escrita estejam formalmente validados. Limitar criação/atualização aos campos previamente aprovados e necessários. Sem exclusão de registros, alteração indiscriminada de dados existentes ou exportação ampla sem aprovação específica. Esta é a proposta recebida; não autoriza produção.
- **Atribuição e data informadas:** Ricardo informou em 09/10/2026: “autorizado por Karol”. A mensagem identifica Karol como fonte da autorização, mas não inclui uma fala/mensagem direta dela. Registrar como relato de Ricardo, não como citação direta verificável da Champion. O escopo de teste permanece sujeito à revisão documental; base legal continua pendente.
- **Decisão final B4-01:** PENDENTE — requer validação explícita da base legal pelo responsável interno e confirmação verificável do Champion sobre o escopo autorizado.

## B4-02 — Ferramenta, acesso e capacidade do conector

- **Status:** PARCIAL — responsável técnico e intenção de usar ambiente de teste informados; nome da segunda ferramenta, existência/disponibilidade da conta, permissões e prova técnica permanecem pendentes.
- **Decisor:** Champion técnico; responsável pelo processo/negócio informado como Champion.
- **Ferramentas mencionadas por Ricardo em 09/10:** Kommo CRM, que Ricardo informa ser utilizado pela R1, e “lovable”. O segundo nome está ambíguo: confirmar se significa **Lóvavel** (como escrito na SPEC-4-001) ou **Lovable**. Não selecionar nem integrar a segunda ferramenta até esclarecer.
- **Responsável técnico informado:** Karol. Responsável pelo processo/negócio: Champion.
- **Conta/ambiente de teste:** foi indicado que deverá ser usado um ambiente de teste sem massa real de leads. A existência, titularidade, URL/organização e disponibilidade efetiva de uma conta de teste ainda não foram confirmadas.
- **Permissões disponíveis:** PENDENTE — registrar apenas os escopos efetivamente validados (leitura e escrita necessários), nunca os valores dos segredos.
- **Prova técnica:** PENDENTE — a SPEC requer prova timeboxed de leitura e escrita com identificador externo em conta de teste. A intenção de usar teste não prova que a conta ou o conector funcionam; nenhuma prova é declarada como executada aqui.
- **Atribuição e data informadas:** Ricardo informou em 09/10/2026: “autorizado por Karol”. A mensagem não contém citação direta ou comprovante original de Karol. Nenhuma credencial foi recebida ou ativada.
- **Decisão final B4-02:** PENDENTE até esclarecer o nome da ferramenta, confirmar ambiente e permissões e registrar resultado da prova técnica timeboxed.

## B4-05 — Mapeamento de campos, identificador externo e conflitos

- **Status:** PARCIAL — foram informadas categorias pretendidas de dados e uma regra segura para conflitos; campos de destino, identificador técnico principal/escopo de unicidade e aprovações do Comercial/Champion continuam PENDENTES.
- **Aprovadores:** Comercial e Champion. Não foi apresentada confirmação verificável de aprovação deles para a tabela abaixo.
- **Rascunho de mapeamento a validar, baseado nas categorias mencionadas por Ricardo (não é mapeamento aprovado):**

| Campo/categoria de origem indicada | Ferramenta e campo de destino | Finalidade/necessidade mínima | Identificador externo e escopo | Regra para conflito (proposta recebida) | Aprovação (quem/data) |
|---|---|---|---|---|---|
| Lead capturado — nome | CRM e campo de nome: PENDENTE de confirmar nomes reais do objeto/campo | Continuidade do atendimento comercial | PENDENTE — não presumir que nome seja identificador | Não sobrescrever automaticamente informação existente sem regra previamente aprovada; preservar origem quando possível e encaminhar para reconciliação humana | PENDENTE — Comercial e Champion |
| Lead capturado — telefone/WhatsApp | CRM e campo de telefone: PENDENTE de confirmar nomes reais do objeto/campo | Possibilitar contato comercial, sujeito à validação da necessidade e base legal | Telefone normalizado foi citado como critério candidato de identificação; não é o identificador técnico principal aprovado. Regra de unicidade, escopo e tratamento de registros anteriores: PENDENTE | Não sobrescrever automaticamente informação existente sem regra previamente aprovada; identificar o caso e encaminhar para reconciliação humana | PENDENTE — Comercial e Champion |
| Lead capturado — origem | CRM e campo de origem: PENDENTE de confirmar campo/destino real | Manter contexto da origem do lead para atendimento | PENDENTE — identificador técnico principal não definido | Não sobrescrever automaticamente informação conflitante sem regra aprovada; preservar origem e encaminhar para avaliação humana | PENDENTE — Comercial e Champion |

- **Identificador externo escolhido:** PENDENTE. O telefone normalizado foi mencionado como critério a considerar junto da existência de registros anteriores para evitar duplicidade; não está aprovado como identificador técnico principal. A equipe técnica deve validar normalização, unicidade, escopo e comportamento com registros prévios antes da produção.
- **Regra de conflito recebida de Ricardo:** não sobrescrever automaticamente dado existente em conflito sem regra previamente aprovada; identificar o caso, preservar a informação de origem quando possível e encaminhar para reconciliação/avaliação humana. Isso é coerente com a salvaguarda da SPEC-4-001; o recebimento da proposta não substitui a aprovação de campo pelo Comercial/Champion.
- **Data e confirmação verificável:** insumo recebido de Ricardo em 09/10/2026; confirmação formal do Champion e do Comercial, com responsável, função e trecho verificável: PENDENTE.

## Fallbacks e limites já definidos pela SPEC-4-001

Estas salvaguardas são requisitos documentais da SPEC; não são evidência de integração configurada ou de aprovação de dados:

- Falha, timeout ou permissão insuficiente: manter a captura de origem; registrar erro sanitizado e pendência/fila de reconciliação com responsável; nunca sinalizar sucesso falso nem expor segredo.
- Dado conflitante sem regra aprovada aplicável: preservar a origem e encaminhar para reconciliação humana; não sobrescrever.
- Rollback: suspender a escrita externa e preservar a captura local.
- Nenhuma credencial, conector ou escrita externa é ativada por este documento.

## Histórico de confirmação

- 02/10/2026 — o rascunho foi criado sem respostas do Champion/Comercial.
- 09/10/2026 — Ricardo forneceu insumos parciais para B4-01, B4-02 e B4-05. A base legal, esclarecimento sobre “lovable”, disponibilidade/permissões da conta de teste, prova técnica, campos finais de destino, identificador externo e aprovações verificáveis permanecem pendentes. A atribuição “autorizado por Karol” foi registrada como relato de Ricardo, sem inventar fala direta de Karol. Nenhuma credencial, conector ou escrita externa foi ativada.
- 09/10/2026, 11:59 (America/Bahia) — Ricardo declarou “ok, então tudo revisado e aprovo o registro parcial”. A aprovação se restringe à revisão documental; não altera o estado PENDENTE dos gates B4-01/02/05 e não autoriza credenciais, conector ou escrita externa.

Atualizar as decisões finais somente após validação/confirmacão verificável dos responsáveis, sem preencher lacunas por inferência.
