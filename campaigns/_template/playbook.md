# Playbook: {{PÚBLICO-ALVO}}

Documento mestre da campanha. Conteúdo, ads e outbound são uma máquina só: nenhuma subpasta (`conteudo/`, `ads/creative/`, `outbound/`, `signals/`, `scripts/`) pode divergir do que está aqui. Preencha de cima pra baixo; o que ainda não sabe, escreva "A definir" (não apague a linha).

## 1. ICP

| Campo | Definição |
|---|---|
| **Empresa** | {{segmento, tamanho, geografia}} |
| **Sinal técnico/comportamental de fit** | {{ex: *site multi-idioma, contratando SDR*}} |
| **Pessoa (decisor)** | {{cargo, senioridade}} |
| **Dor comum** | {{a dor que a oferta resolve, em uma frase}} |
| **Quem fica de fora** | {{critério de exclusão}} |
| **Lista de negativação** | {{clientes atuais, concorrentes diretos, parceiros: onde está a lista?}} |

Fonte de verdade da base: `signals/` e `outbound/` ({{nome do arquivo}}).

## 2. Estratégia e canais

- **Oferta:** {{o que você vende para esse público}}
- **Prova ou artefato:** {{o que o lead vê antes de comprar; se é construído sob demanda, só depois da resposta}}
- **Escopo da entrega:** {{o que está incluído e o que não está}}
- **CTA único:** {{ex: *agendar 20 min*}}
- **Champion interno:** {{quem precisa existir na conta para a entrega se sustentar, e como checar}}
- **Ímã (material rico):** {{o que gera o sinal; vive em `conteudo/`}}
- **Ideia da campanha:** {{o quebra-gelo: por que essa pessoa responderia}}
- **Objetivo (60-90 dias):** {{ex: *30 reuniões em 8 semanas*}}
- **Métrica norte:** {{...}}

**Canais:**

| Canal | Papel | Pasta | Status |
|---|---|---|---|
| Conteúdo (orgânico) | ímã, gera sinal | `conteudo/` | {{...}} |
| Ads | amplifica o mesmo ângulo pro mesmo público | `ads/creative/` | {{...}} |
| Outbound LinkedIn | canal primário? | `outbound/` | {{...}} |
| Outbound e-mail | paralelo? | `outbound/` | {{...}} |
| Comment-gate | sinal de post vira DM | `signals/` | {{sim/não; ver `playbook/comment-gate.md`}} |

## 3. Dados, filtros e sinais

Log rastreável de como a base bruta virou a lista final. Um passo por linha, com o número antes e depois.

| Passo | O que foi feito | Antes → depois | Arquivo |
|---|---|---|---|
| 1 | {{coleta nas fontes + dedup}} | {{N}} | {{lista-bruta.csv}} |
| 2 | {{filtro de ICP, exclusão, negativação}} | {{N → N}} | {{lista-loop.csv}} |
| 3 | {{sinais (Apify, site, Nuvia)}} | {{N → N}} | {{enriquecida.csv}} |
| 4 | {{corte por score}} | {{N → N}} | {{lista-qualificada.csv}} |

### Sinais e priorização

| Sinal | Peso | Fonte | Como medir |
|---|---|---|---|
| {{sinal 1}} | {{alto/médio/baixo}} | {{Apify, site, Nuvia}} | {{regra}} |
| {{sinal 2}} | | | |

Critério de corte da lista qualificada: {{score mínimo, ou top N}}. Arquivo: `signals/{{...}}`.

**Enriquecimento antes do disparo** (campos por lead; todo sinal com fonte e data):

| Campo | Fonte | Para que serve |
|---|---|---|
| Nome, cargo, headline e sobre do decisor | {{Apify / LinkedIn}} | personalizar o gancho |
| Sinal de champion interno | {{perfil, empresa}} | decidir se avança para a reunião |
| {{outro campo}} | | |

O que **não** entra no enriquecimento pré-disparo: {{ex: *link do artefato, gerado só após a resposta*}}.

Triagem de ICP: `automations/leads/triagem_icp.py`. Campos de ICP e cargo gravados no contato da Nuvia antes de ativar a campanha.

## 4. Matriz de ângulos (dor × cargo)

Uma linha por cargo da lista qualificada. O ângulo só pode usar sinal que existe na seção 3.

| Cargo | Dor específica | Ângulo da mensagem | Sinal que usa | Prova |
|---|---|---|---|---|
| {{cargo 1}} | {{dor}} | {{o que a mensagem toca}} | {{sinal da seção 3}} | {{case, número, artefato}} |
| {{cargo 2}} | | | | |

## 5. Sequência (cadência)

Máximo de toques: {{N LinkedIn + N e-mails}}. Cada toque parte de um ângulo da seção 4.

| Toque | Canal | Ação / mensagem | Arquivo |
|---|---|---|---|
| D0 | LinkedIn | conexão com nota personalizada | `outbound/` |
| D+2 | LinkedIn / e-mail | msg 1 | `outbound/` |
| D+4 | LinkedIn / e-mail | msg 2 | `outbound/` |
| D+7 | LinkedIn / e-mail | msg 3 (último toque) | `outbound/` |
| Ao responder | | {{próxima ação: CTA, reunião, prévia}} | |
| Sem resposta | | {{vai pra conteúdo/ads como reforço passivo}} | |

Regra de saída: {{o que interrompe a cadência: resposta, aceite sem resposta, descadastro}}. Se a resposta muda o fluxo (ex: dispara um build), a cadência não ganha toques extras.

Voz: `brand/voice-outbound.md` (1:1, registro de WhatsApp, curto).

## 6. Leads de exemplo e mensagens

3 a 5 leads reais da base, com a mensagem que cada um receberia. Serve de teste antes do disparo: se a mensagem não soa certa pra esses, não sai pra lista toda.

| Lead | Cargo / empresa | Gancho (atividade ou fato do perfil) | Mensagem enviada |
|---|---|---|---|
| {{nome}} | {{cargo, empresa}} | {{o que você viu}} | {{texto da DM}} |
| {{nome}} | | | |
| {{nome}} | | | |

Checar antes do disparo: variáveis `empresa` e `primeiro nome` carregando em todos os canais, testando cada canal separadamente (o bug costuma carregar no e-mail e falhar no LinkedIn).

**Pontos de atenção da campanha:**
- {{ex: *toda mensagem tem personalização; não existe versão genérica*}}
- {{ex: *o claim da copy precisa ter processo rápido o bastante para não furar a promessa; SLA interno: X horas*}}
- {{o que não fazer antes da resposta, para não gastar esforço em conta que não responde}}

## 7. Ficha operacional

| Campo | Definição |
|---|---|
| **Data de início** | {{AAAA-MM-DD}} |
| **Duração do ciclo** | {{X dias após o primeiro disparo por lead}} |
| **Data de fim** | {{AAAA-MM-DD}} |
| **Ferramenta / bot** | {{Nuvia, LinkedIn, e-mail}} |
| **List ID (Nuvia)** | {{...}} |
| **Campaign ID (Nuvia)** | {{...}} |
| **Agent ID (Nuvia)** | {{...}} |
| **Responsável** | {{...}} |

## 8. Metas, resultados e debriefing

Metas preenchidas antes do disparo; resultados ao fim do primeiro ciclo. A métrica norte vem da seção 2.

| Métrica | Meta | Resultado |
|---|---|---|
| Leads abordados | | |
| Taxa de aceite de conexão | | |
| Taxa de resposta | | |
| Tempo entre resposta e próxima ação (SLA) | | |
| % de respondentes com champion identificado | | |
| Reuniões agendadas | | |
| Custo / tempo por reunião | | |

**O que funcionou:** {{...}}
**O que não funcionou:** {{...}}
**Próximo experimento:** {{link para `playbook/experimentos/`}}
