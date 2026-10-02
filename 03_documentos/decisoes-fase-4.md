# Decisões da Fase 4 — Integração direta e saúde da conversão

**Estado deste registro:** rascunho de coleta — decisões B4-01, B4-02 e B4-05 pendentes de confirmação verificável do Champion (e, para o mapeamento, do Comercial).  
**Criado em:** 02/10/2026.  
**Referência:** SPEC-4-001 e task `7953f975-0f69-42a0-a9a1-b028429550cb`.

Este documento reúne as perguntas da task e o espaço para registrar as respostas sem inferi-las. Campo vazio, proposta ou registro deste rascunho não equivale a decisão nem libera integração. Registrar cada decisão com data, responsável/decisor, citação literal verificável e escopo. Não incluir senhas, tokens, chaves, credenciais ou dados reais de leads neste arquivo, no repositório ou no chat; segredos devem ser tratados somente pelo mecanismo autorizado, após aprovação aplicável.

**Limite até liberação:** nenhuma credencial é ativada e nenhuma escrita externa é realizada com base neste rascunho. A integração também depende das pré-condições e provas técnicas definidas na SPEC-4-001; produção exige autorização própria.

## B4-01 — Base legal, minimização e autorização de escrita externa

- **Status:** PENDENTE — nenhuma decisão verificável do Champion foi registrada neste ciclo.
- **Decisor:** Champion (Karol e Márcio).
- **Perguntas a responder:** qual base legal e, quando aplicável, qual forma de consentimento cobre a finalidade pretendida? Qual é a finalidade do envio e quais categorias mínimas de dados podem ser escritas? A escrita externa está autorizada ou não; em qual ferramenta, ambiente e escopo operacional? A resposta deve ser validada pelo responsável do cliente; este registro não faz uma determinação jurídica.
- **Decisão do Champion:** PENDENTE — preencher após resposta explícita.
- **Data e confirmação verificável:** PENDENTE — registrar data, nome/função e citação literal da confirmação do Champion.

## B4-02 — Ferramenta, acesso e capacidade do conector

- **Status:** PENDENTE — ferramenta, escopos e disponibilidade de conta de teste não confirmados neste ciclo.
- **Decisor:** Champion técnico (identidade a confirmar).
- **Perguntas a responder:** escolher Kommo, Lóvavel, ambas ou nenhuma por ora; identificar quem validará tecnicamente o acesso; informar se existe conta de teste autorizada e se há acesso de leitura/escrita com escopos mínimos para a prova. Registrar apenas a existência/escopos e o método aprovado de entrega de segredo — nunca os valores das credenciais.
- **Ferramenta escolhida:** PENDENTE.
- **Conta de teste e permissões disponíveis:** PENDENTE — sem segredo ou dado real.
- **Prova técnica:** PENDENTE — a SPEC requer prova timeboxed de leitura e escrita com identificador externo em conta de teste; esta entrada documental, sozinha, não prova capacidade nem ativa o conector.
- **Data e confirmação verificável:** PENDENTE — registrar data, nome/função e citação literal da confirmação do Champion técnico.

## B4-05 — Mapeamento de campos, identificador externo e conflitos

- **Status:** PENDENTE — mapeamento e aprovação do Champion/Comercial ainda não registrados.
- **Aprovadores:** Comercial e Champion.
- **Tabela a preencher, uma linha por campo autorizado:**

| Entidade/campo de origem | Ferramenta e campo de destino | Finalidade/necessidade mínima | Identificador externo e escopo | Regra aprovada para conflito | Aprovação (quem/data) |
|---|---|---|---|---|---|
| PENDENTE | PENDENTE | PENDENTE | PENDENTE | PENDENTE | PENDENTE |

- **Identificador externo escolhido:** PENDENTE — definir entidade, origem e regra de unicidade/idempotência com o Comercial/Champion; nenhum identificador é presumido neste rascunho.
- **Regra segura enquanto não houver aprovação aplicável:** não sobrescrever dado conflitante sem regra explícita aprovada. Preservar o dado de origem, registrar pendência para reconciliação humana e não reportar a operação como sucesso. Esta é a salvaguarda exigida pela SPEC-4-001, não uma confirmação de que o mapeamento ou a integração estejam aprovados.
- **Data e confirmação verificável:** PENDENTE — registrar data, nome/função e citação literal da confirmação do Champion e do Comercial.

## Fallbacks e limites já definidos pela SPEC-4-001

Estas salvaguardas são requisitos documentais da SPEC; não são evidência de integração configurada ou de aprovação de dados:

- Falha, timeout ou permissão insuficiente: manter a captura de origem; registrar erro sanitizado e pendência/fila de reconciliação com responsável; nunca sinalizar sucesso falso nem expor segredo.
- Dado conflitante sem regra aprovada aplicável: preservar a origem e encaminhar para reconciliação humana; não sobrescrever.
- Rollback: suspender a escrita externa e preservar a captura local.
- Nenhuma credencial, conector ou escrita externa é ativada por este documento.

## Histórico de confirmação

Nenhuma resposta do Champion/Comercial foi recebida ou registrada ao criar este rascunho em 02/10/2026. Atualizar cada seção somente após a confirmação verificável, sem preencher por inferência.
