---
name: nota-de-conexao
description: >
  Escreve a nota de conexão do LinkedIn (o convite com mensagem) lead a lead, a partir de uma
  base enriquecida e da matriz de ângulos do playbook. Escolhe o gancho mais forte disponível
  (ponto em comum, sinal recente, conteúdo do lead), aplica uma das estruturas abaixo e valida
  limite de caracteres, ausência de pitch e voz 1:1. Gatilhos: "nota de conexão", "convite do
  LinkedIn", "mensagem do convite", "connection note", "escreve o convite pro lead".
---

# Nota de conexão

A nota tem um único trabalho: fazer a pessoa aceitar o convite. Vender é trabalho do FUP, depois do aceite. Toda regra abaixo serve a isso.

## Antes de escrever (carregar, sem perguntar)

- `brand/voice-outbound.md`: registro 1:1 e lista de proibidos.
- `brand/background.md`: seus pontos de contato (ex-empresas, escolas, cidades, comunidades, eventos). É daqui que sai o gancho de background em comum.
- `playbook.md` da campanha: §3 (Dados, filtros e sinais) para saber quais sinais existem e §4 (Matriz de ângulos) para o ângulo do cargo.
- A linha do lead na `lista-qualificada.csv` (headline, sobre, sinal, sinal_fonte, sinal_data).

## Regras duras

1. **Até 300 caracteres**, contando espaço. Conta gratuita: até 200. Mire em 180 a 250: nota curta é lida inteira na notificação.
2. **Zero pedido.** Nada de reunião, call, demo, link, material ou "posso te mostrar". Isso é FUP.
3. **Um motivo específico** que só vale para ESTA pessoa. Se o texto serve para outro lead trocando o nome, reescreva.
4. **Fato verificável**, nunca elogio. "Vi seu post sobre X" com o X real. Nunca "adorei seu perfil" ou "admiro seu trabalho".
5. **Primeiro nome**, sem "Olá, tudo bem?", sem "espero que esteja bem".
6. **No máximo uma pergunta**, fechada e de baixo atrito, ou nenhuma. Pergunta aberta demais ("como vocês fazem X?") vira tarefa para o lead.
7. **Sinal com data dentro da janela.** Sinal de mais de 90 dias não vira gancho de "vi que agora".
8. **Nada inventado.** Gancho sem fonte na base ou no `background.md` não entra. Se não há gancho, use o ângulo do cargo (tipo 7 abaixo) e marque `gancho=fraco`.
9. Sem travessão, sem emoji, sem "não só X, mas Y", sem hashtag.

## Ganchos, do mais forte para o mais fraco

Use o primeiro que existir para o lead. Um gancho por nota.

| # | Gancho | Onde achar | Exemplo de abertura |
|---|---|---|---|
| 1 | **Interagiu com você** (curtiu, comentou, viu o perfil) | Nuvia, notificações, comment-gate | "Vi seu comentário no meu post sobre lista de ICP." |
| 2 | **Background em comum**: mesma ex-empresa, faculdade, cidade, país de origem | perfil do lead × `background.md` | "Também passei pela Totvs, no time de dados." |
| 3 | **Grupo ou comunidade em comum** (grupo do LinkedIn, comunidade de WhatsApp, associação) | aba Interesses › Grupos, `background.md` | "Somos os dois do grupo RevOps Brasil." |
| 4 | **Evento em comum** (palestrou, participou, vai participar) | posts do lead, página do evento | "Vi que você vai estar no RD Summit também." |
| 5 | **Conteúdo do lead** (post, artigo, podcast, comentário recente) | Apify posts, sinal_fonte | "Li seu post sobre ramp de SDR em 30 dias." |
| 6 | **Sinal da empresa ou do cargo** (troca de cargo, rodada, contratação, expansão) | §3 do playbook, colunas `sinal*` | "Parabéns pela chegada na Acme como Head de Vendas." |
| 7 | **Ângulo do cargo** (sem gancho pessoal) | §4 do playbook | "Converso bastante com heads de vendas sobre qualidade de lista." |
| 8 | **Conexões em comum** (só nome citado se a pessoa for próxima de verdade) | perfil | "A Ana Souza comentou que vocês estão estruturando outbound." |

Conexão em comum só vale citando alguém que você conhece; "temos 12 conexões em comum" não é gancho.

## Estruturas

Escolha uma. Na dúvida, escreva nas duas primeiras e compare.

**A. Gatilho → relevância → pergunta** (quando há sinal ou conteúdo recente)
> {{Nome}}, vi que {{gatilho}}. {{Por que isso importa no ângulo do cargo, 1 frase}}. {{Pergunta fechada}}?

**B. Observação → problema → pergunta** (quando o ângulo do cargo é mais forte que o sinal)
> {{Nome}}, {{observação sobre o cargo/empresa}}. Nesse momento, {{problema típico, 1 frase}}. {{Pergunta fechada}}?

**C. Ponto em comum → ponte** (background, grupo ou evento; sem pergunta)
> {{Nome}}, {{ponto em comum}}. {{Ponte: o que você faz que conversa com o trabalho dele}}. Bom ter você na rede.

## Exemplos (fictícios, só para mostrar a forma)

A (sinal): "Carla, vi que a Nexa abriu 4 vagas de SDR este mês. Quando o time dobra, o gargalo costuma virar a lista, não o volume. Vocês já medem quantos leads por SDR são ICP?" (166 caracteres)

B (cargo): "Rafael, quem lidera marketing em SaaS de ticket alto costuma herdar o MQL que vendas não aceita. Isso acontece por aí também?" (126 caracteres)

C (background): "Júlia, também fiz Insper e passei 3 anos em dados na Stone. Hoje monto máquinas de outbound com IA, seu trabalho em RevOps conversa muito com isso. Bom ter você na rede." (171 caracteres)

Anti-exemplo: "Olá Pedro, tudo bem? Adorei seu perfil! Ajudo empresas como a sua a gerar mais reuniões com IA. Podemos conversar 15 min?" (elogio genérico, pitch, pedido, serve para qualquer lead)

## Checklist antes de entregar

- [ ] Contagem de caracteres ≤ limite, informada ao lado da nota
- [ ] Gancho usado e a fonte dele (coluna da base ou linha do `background.md`)
- [ ] Nenhum pedido, link ou nome de produto
- [ ] Trocar o nome não faz a nota servir para outro lead
- [ ] Bate com o ângulo do cargo da §4 e com a voz do `voice-outbound.md`

## Saída

Em lote, uma linha por lead com: `nota_conexao`, `caracteres`, `gancho` (tipo da tabela), `gancho_fonte`, `estrutura` (A, B ou C). Para lead único, entregue as variantes pedidas lado a lado e diga qual você mandaria e por quê.
