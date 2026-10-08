# Detetive Digital

**Antes de clicar, investigue.**

Jogo educativo de segurança digital para pessoas idosas. O jogador assume o papel de detetive: recebe mensagens simuladas (SMS, e-mail, aplicativo de mensagens, ligação), investiga os sinais, decide o que fazer e recebe a explicação de por que a atitude é segura ou arriscada.

Projeto Integrador do curso de Análise e Desenvolvimento de Sistemas do Centro Universitário Adventista de São Paulo, em parceria com a Associação Cuidaris (Itapecerica da Serra, SP).

Alunos: Ana Carolina Souza Vieira e Dennys de Oliveira.

## Como abrir

Abra o arquivo `index.html` em um navegador (Chrome, Edge ou Firefox). Não é preciso instalar nada nem ter servidor.

O jogo funciona sem internet. Com internet, ele carrega duas fontes do Google Fonts; sem internet, usa fontes do próprio computador.

## Como se joga

Cada caso segue quatro etapas:

1. **Ler** a mensagem simulada.
2. **Investigar**, clicando nas partes marcadas com a lupa. Cada parte revela um sinal de alerta, um sinal de confiança ou uma observação, que vai para o caderno do detetive.
3. **Decidir** entre três atitudes.
4. **Entender**: o jogo mostra o que aconteceu depois da escolha, explica o porquê e apresenta a regra do detetive daquele caso.

Não há limite de tempo. O botão "Como jogar" fica sempre no alto da tela.

## Casos

São 12 casos em 3 níveis. Nove são golpes e três são mensagens verdadeiras, para que o jogador precise investigar em vez de desconfiar de tudo.

| Nível | Caso | Tipo |
|---|---|---|
| 1. Sinais claros | O prêmio de R$ 5.000 | Falso prêmio |
| | O lembrete da clínica | Mensagem verdadeira |
| | O código de seis números | Pedido de senha |
| | A corrente da família | Link suspeito |
| 2. Olhe com atenção | O aviso do banco | Falso banco |
| | O número novo do filho | Golpe envolvendo Pix |
| | A compra na farmácia | Mensagem verdadeira |
| | O vizinho em apuros | Perfil falso |
| 3. Golpes bem-feitos | A ligação da central | Falsa central telefônica |
| | A conta de luz | Boleto falso |
| | A mensagem da Júlia | Mensagem verdadeira |
| | A prova de vida | Falso atendimento do INSS |

Todas as mensagens, pessoas e empresas são inventadas para o jogo (Banco Aurora, Clínica Vida Plena, Luz do Vale, Farmácia Bem Viver).

## Recursos

- **Personagem guia:** a Lupita, uma coruja detetive, apresenta o jogo, os níveis e os casos.
- **Telas simuladas:** celular para SMS e aplicativo de mensagens, janela de e-mail, tela de chamada e tela de bloqueio com aviso.
- **Distintivos:** um por caso, conquistado ao tomar a boa decisão na primeira escolha.
- **Revisão:** ao final, o jogador pode rever só os casos em que não tomou a boa decisão.
- **Nome e progresso salvo:** o jogador entra com o primeiro nome, sem senha, e pode continuar de onde parou em outro dia.
- **Recorde pessoal:** a tela final compara o resultado apenas com o da própria pessoa. Não há ranking nem comparação entre jogadores.
- **Modo dupla:** duas pessoas jogam juntas, com os dois nomes. O jogo propõe uma pergunta para conversar antes de cada decisão. A dupla tem progresso e recorde próprios.
- **Certificado:** tela com o nome do jogador, para fotografar. Em dupla, cada pessoa tem o seu.
- **Área do instrutor:** resumo das partidas terminadas no computador (casos com mais dificuldade, decisões por caso, sinais de alerta mais ignorados) e texto pronto para copiar para o relatório.

## Acessibilidade

- Letras grandes, com botões "A−" e "A+" para ajustar o tamanho.
- Botões grandes, poucos elementos por tela e linguagem simples.
- Sem limite de tempo e sem pontuação negativa.
- Uso por mouse ou teclado, com foco visível.
- Retorno visual e textual em cada ação. As cores nunca são o único indicador.
- Leitura em voz alta pelo botão "Ouvir a leitura", quando o navegador oferece voz em português.
- Sons curtos opcionais, desligados por padrão.
- Tema claro e tema escuro, conforme a configuração do computador.

## Dados guardados

O jogo não envia nenhum dado pela internet. Tudo fica no navegador do computador em que se joga (`localStorage`):

| Chave | Conteúdo |
|---|---|
| `dd-jogadores` | Nomes, progresso salvo e recorde de cada jogador ou dupla |
| `dd-sessoes` | Registro das partidas terminadas, sem nomes (até 300) |
| `dd-escala` | Tamanho de letra escolhido |
| `dd-som` | Som ligado ou desligado |

Consequências:

- O progresso e o recorde valem só para aquele computador e aquele navegador.
- Limpar os dados do navegador apaga tudo.
- A área do instrutor tem botões para apagar os registros e os nomes salvos. Ela não tem senha.

## Tecnologias

HTML, CSS e JavaScript, sem bibliotecas e sem etapa de compilação. Todo o jogo está em `index.html`.

- Fontes: Atkinson Hyperlegible (texto) e Zilla Slab (títulos), via Google Fonts.
- Voz: Web Speech API do navegador.
- Sons: Web Audio API do navegador.

## Como alterar ou criar um caso

Os casos ficam na lista `CASOS`, dentro do `<script>` de `index.html`. Cada caso tem este formato:

```js
{
  nivel: 1,                      // 1, 2 ou 3
  golpe: true,                   // false para mensagem verdadeira
  titulo: "O prêmio de R$ 5.000",
  tipo: "Falso prêmio",          // aparece só na explicação
  canal: "Mensagem de texto (SMS)",
  intro: "Você recebe esta mensagem no celular.",
  remetente: { txt: "(11) 94002-7781", sub: "Número que não está nos seus contatos" },
  linhas: [
    { txt: "Texto da mensagem", a: { t: "Título do sinal de alerta", e: "Explicação" } },
    { txt: "Outro trecho",      b: { t: "Título do sinal de confiança", e: "Explicação" } },
    { txt: "Outro trecho",      n: "Observação neutra" },
    { txt: "Trecho sem clique" }
  ],
  opcoes: [
    { txt: "Atitude", tipo: "boa", depois: "O que aconteceu", porque: "Explicação" }
    // tipo: "boa", "risco" ou "excesso" (cuidado demais em mensagem verdadeira)
  ],
  regra: "Regra do detetive deste caso."
}
```

Ao mexer na lista, observe:

- Cada caso precisa de exatamente uma opção com `tipo: "boa"`.
- O `canal` define a aparência da tela: textos com "SMS", "E-mail", "Ligação" ou "Aviso" usam telas próprias; os demais usam a tela de aplicativo de mensagens.
- As listas `DIST` (nomes dos distintivos) e `PERG` (perguntas do modo dupla) têm um item por caso, na mesma ordem de `CASOS`. Ao criar ou remover um caso, ajuste as duas.
- O remetente e o campo `assunto` (usado nos e-mails) também aceitam `a`, `b` ou `n`.

## Limites conhecidos

- **Testes:** o jogo foi verificado em um navegador de teste (Chromium), no tema claro. Falta testar nos computadores da oficina, no tema escuro e com pessoas idosas.
- **Leitura em voz alta e sons:** dependem do navegador e não foram ouvidos nos testes.
- **Resumo da turma:** cada computador registra só as próprias partidas. Para um resumo geral, é preciso copiar o texto de cada máquina.
- **Nomes iguais:** duas pessoas com o mesmo primeiro nome no mesmo computador compartilham o progresso. Uma delas pode usar nome e sobrenome.
- **Impressão do certificado:** não há botão de imprimir. A tela foi pensada para ser fotografada.
- **Duração:** os 12 casos devem levar mais de meia hora. O progresso salvo permite dividir em encontros.
- **Textos:** os casos, as explicações e as perguntas do modo dupla devem ser revisados com o público e ajustados após a atividade inicial na Associação Cuidaris.

## Fora do escopo

Conforme a proposta do Projeto Integrador, o jogo não tem login com senha, cadastro de usuários, ranking, multiplayer online, banco de dados, inteligência artificial nem versão em aplicativo para celular.
