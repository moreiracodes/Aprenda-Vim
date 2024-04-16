# Capítulo 02. Buffers, Janelas e Abas

Se você já usou um editor de texto moderno antes, provavelmente está familiarizado com janelas e abas. O Vim usa três abstrações de exibição em vez de duas: buffers, janelas e abas. Neste capítulo, explicarei o que são buffers, janelas e abas e como funcionam no Vim.

Antes de começar, certifique-se de ter a opção `set hidden` no vimrc. Sem ela, sempre que você trocar de buffers e o seu buffer atual não estiver salvo, o Vim solicitará que você salve o arquivo (você não quer isso se quiser se mover rapidamente). Eu ainda não cobri o vimrc. Se você não tiver um vimrc, crie um. Geralmente, ele é colocado no seu diretório home e é chamado de `.vimrc`. Eu tenho o meu em `~/.vimrc`. Para ver onde você deve criar seu vimrc, confira `:h vimrc`. Dentro dele, adicione:

```
set hidden
```

Salve e, em seguida, carregue (execute `:source %` de dentro do vimrc).

## Buffers

O que é um *buffer*?

Um buffer é um espaço na memória onde você pode escrever e editar algum texto. Quando você abre um arquivo no Vim, os dados são vinculados a um buffer. Quando você abre 3 arquivos no Vim, você tem 3 buffers.

Tenha dois arquivos vazios, `file1.js` e `file2.js`, disponíveis (se possível, crie-os com o Vim). Execute isso no terminal:

```bash
vim file1.js
```

O que você está vendo é o *buffer* `file1.js`. Sempre que você abre um novo arquivo, o Vim cria um novo buffer.

Saia do Vim. Desta vez, abra dois novos arquivos:

```bash
vim file1.js file2.js
```
O Vim atualmente exibe o buffer `file1.js` , mas na verdade cria dois buffers: buffer `file1.js` e buffer `file2.js`. Execute `:buffers` para ver todos os buffers (alternativamente, você pode usar `:ls` ou `:files` também). Você deve ver tanto `file1.js` quanto `file2.js` listados. Executar `vim file1 file2 file3 ... filen` cria n quantidade de buffers. Cada vez que você abre um novo arquivo, o Vim cria um novo buffer para esse arquivo.

Existem várias maneiras de atravessar buffers:

- `:bnext` para ir para o próximo buffer (`:bprevious` para ir para o buffer anterior).
- `:buffer` + nome do arquivo. O Vim pode autocompletar o nome do arquivo com `<Tab>`.
- `:buffer` + `n`, onde `n` é o número do buffer. Por exemplo, digitando - `:buffer 2` irá levá-lo ao buffer #2.
Pule para a posição anterior na lista de saltos com `Ctrl-O` e para a posição mais nova com `Ctrl-I`. Estes não são métodos específicos do buffer, mas podem ser usados para pular entre buffers diferentes. Eu explicarei saltos em mais detalhes no Capítulo 5.
Vá para o buffer editado anteriormente com `Ctrl-^`.

Uma vez que o Vim cria um buffer, ele permanecerá na sua lista de buffers. Para removê-lo, você pode digitar `:bdelete`. Ele também pode aceitar um número de buffer como parâmetro (`:bdelete 3` para excluir o buffer #3) ou um nome de arquivo (`:bdelete` e use `<Tab>` para autocompletar).

A coisa mais difícil para mim ao aprender sobre buffers foi visualizar como eles funcionavam porque minha mente estava acostumada a janelas ao usar um editor de texto convencional. Uma boa analogia é um baralho de cartas. Se eu tenho 2 buffers, tenho um conjunto de 2 cartas. A carta no topo é a única que vejo, mas sei que há cartas abaixo dela. Se vejo o buffer `file1.js` exibido, então a carta `file1.js` está no topo do baralho. Não consigo ver a outra carta, `file2.js` aqui, mas ela está lá. Se eu trocar de buffers para `file2.js`, então a carta `file2.js` está agora no topo do baralho e a carta `file1.js` está abaixo dela.

Se você nunca usou o Vim antes, este é um novo conceito. Tire um tempo para entendê-lo.

## Saindo do Vim

A propósito, se você tiver vários buffers abertos, pode fechar todos eles com quit-all:


```
:qall
```

Se você quiser fechar sem salvar suas alterações, basta adicionar `!` no final:

```
:qall!
```

Para salvar e sair de tudo, execute:

```
:wqall
```

## Janelas

Uma janela é uma visualização em um buffer. Se você vem de um editor convencional, este conceito pode lhe ser familiar. A maioria dos editores de texto tem a capacidade de exibir várias janelas. No Vim, você também pode ter várias janelas.

Vamos abrir `file1.js` no terminal novamente:


```bash
vim file1.js
```

Anteriormente, eu escrevi que você está olhando para o buffer `file1.js`. Embora isso estivesse correto, essa afirmação estava incompleta. Você está olhando para o buffer `file1.js`, exibido através de uma janela. Uma janela é como você está visualizando um buffer.

Não saia do Vim ainda. Execute:

```
:split file2.js
```

Agora você está olhando para dois buffers através de **duas janelas**. A janela superior exibe o buffer `file2.js`. A janela inferior exibe o buffer `file1.js`.

Se você quiser navegar entre janelas, use esses atalhos:

```
Ctrl-W H: Move o cursor para a janela à esquerda
Ctrl-W J: Move o cursor para a janela abaixo
Ctrl-W K: Move o cursor para a janela superior
Ctrl-W L: Move o cursor para a janela à direita
```

Agora execute:

```
:vsplit file3.js
```

Agora você está vendo três janelas exibindo três buffers. Uma janela exibe o buffer `file3.js`, outra janela exibe o buffer `file2.js` e outra janela exibe o buffer `file1.js`.

Você pode ter várias janelas exibindo o mesmo buffer. Enquanto estiver na janela superior esquerda, digite:

```
:buffer file2.js
```

Agora ambas as duas janelas estão exibindo o buffer `file2.js`. Se você começar a digitar em uma janela `file2.js`, verá que ambas as janelas que exibem buffers `file2.js` estão sendo atualizadas em tempo real.

Para fechar a janela atual, você pode executar `Ctrl-W C` ou digitar `:quit`. Quando você fecha uma janela, o buffer ainda estará lá (execute `:buffers` para confirmar isso).

Aqui estão alguns comandos úteis de janela no modo normal:

```
Ctrl-W V: Abre uma nova divisão vertical
Ctrl-W S: Abre uma nova divisão horizontal
Ctrl-W C: Fecha uma janela
Ctrl-W O: Torna a janela atual a única na tela e fecha as outras janelas
```

E aqui está uma lista de comandos úteis de janela na linha de comando:

```
:vsplit nome-do-arquivo: Divide a janela verticalmente
:split nome-do-arquivo: Divide a janela horizontalmente
:new nome-do-arquivo: Cria uma nova janela
```

Leve seu tempo para entendê-los. Para obter mais informações, confira `:h window`.


## Abas

Uma aba é uma coleção de janelas. Pense nisso como um layout para janelas. Na maioria dos editores de texto modernos (e navegadores de internet modernos), uma aba significa um arquivo / página aberto e quando você o fecha, esse arquivo / página desaparece. No Vim, uma aba não representa um arquivo aberto. Quando você fecha uma aba no Vim, você não está fechando um arquivo. Você está apenas fechando o layout. Os arquivos abertos nesse layout ainda não estão fechados, eles ainda estão abertos em seus buffers.

Vamos ver as abas do Vim em ação. Abra `file1.js`:

```bash
vim file1.js
```

Para abrir `file2.js` em uma nova aba:

```
:tabnew file2.js
```

Você também pode deixar o Vim autocompletar o arquivo que deseja abrir em uma nova aba pressionando `<Tab>`.

Abaixo está uma lista de navegações úteis de abas:

```
:tabnew file.txt: Abre file.txt em uma nova aba
:tabclose: Fecha a aba atual
:tabnext: Vai para a próxima aba
:tabprevious: Vai para a aba anterior
:tablast: Vai para a última aba
:tabfirst: Vai para a primeira aba
```

Você também pode executar `gt` para ir para a próxima página da aba (você pode ir para a aba anterior com `gT`). Você pode passar um número como argumento para `gt`, onde o número é o número da aba. Para ir para a terceira aba, faça `3gt`.

Uma vantagem de ter várias abas é que você pode ter disposições de janela diferentes em abas diferentes. Talvez você queira que sua primeira aba tenha 3 janelas verticais e a segunda aba tenha um layout de janelas mistas horizontais e verticais. A aba é a ferramenta perfeita para o trabalho!

Para iniciar o Vim com várias abas, você pode fazer isso a partir do terminal:

```bash
vim -p file1.js file2.js file3.js
```

## Movendo-se em 3D

Mover entre janelas é como viajar bidimensionalmente ao longo do eixo X-Y em coordenadas cartesianas. Você pode se mover para a janela superior, direita, inferior e esquerda com `Ctrl-W H/J/K/L`.

Mover entre buffers é como viajar pelo eixo Z em coordenadas cartesianas. Imagine que seus arquivos de buffer estão alinhados ao longo do eixo Z. Você pode percorrer o eixo Z um buffer de cada vez com `:bnext` e `:bprevious`. Você pode pular para qualquer coordenada no eixo Z com `:buffer nome-do-arquivo/número-do-buffer`.

Você pode se mover no espaço tridimensional combinando movimentos de janela e de buffer. Você pode se mover para a janela superior, direita, inferior ou esquerda (navegações X-Y) com movimentos de janela. Como cada janela contém buffers, você pode avançar e retroceder (navegações Z) com movimentos de buffer.

## Usando Buffers, Janelas e Abas de Maneira Inteligente

Você aprendeu o que são buffers, janelas e abas e como funcionam no Vim. Agora que você os entende melhor, pode usá-los em seu próprio fluxo de trabalho.

Cada pessoa tem um fluxo de trabalho diferente, aqui está o meu, por exemplo:

- Primeiro, eu uso buffers para armazenar todos os arquivos necessários para a tarefa atual. O Vim pode lidar com muitos buffers abertos antes de começar a ficar lento. Além disso, ter muitos buffers abertos não vai lotar minha tela. Eu estou vendo apenas um buffer (assumindo que tenho apenas uma janela) a qualquer momento, o que me permite focar em uma tela. Quando preciso ir a algum lugar, posso voar rapidamente para qualquer buffer aberto a qualquer momento.
- Eu uso múltiplas janelas para visualizar vários buffers de uma vez, geralmente ao diferenciar arquivos, ler documentos ou seguir um fluxo de código. Eu tento manter o número de janelas abertas em no máximo três, porque minha tela ficará lotada (eu uso um laptop pequeno). Quando termino, fecho quaisquer janelas extras. Menos janelas significa menos distrações.
- Em vez de abas, eu uso janelas do [tmux](https://github.com/tmux/tmux/wiki). Eu geralmente uso várias janelas do tmux ao mesmo tempo. Por exemplo, uma janela do tmux para códigos do lado do cliente e outra para códigos do backend.

Meu fluxo de trabalho pode parecer diferente do seu, com base no seu estilo de edição, e está tudo bem. Experimente para descobrir seu próprio fluxo, adequando ao seu estilo de codificação.
