# Ch01. Iniciando Vim

Neste capítulo você vai aprender diferentes maneiras de iniciar o vim a partir do terminal. Esse guia foi escrito com base no vim 8.2. Se você usa o Neovim ou alguma outra versão do Vim, você deve ficar quase sempre bem, mas fique atento que alguns comandos podem não estar disponíveis.

## Instalando

Eu não vou por meio de detalhes instruir como instalar Vim em uma máquina específica. A boa notícia é que muitos dos computadores baseados em Unix já vem com o Vim instalado. Caso não, muitas distros devem ter alguma instrução instalando o Vim.

Para baixar mais informações sobre o processo de instalação do Vim, cheque no website de download oficial do Vim ou no repositório oficial do Vim:

- [Vim website](https://www.vim.org/download.php)
- [Vim github](https://github.com/vim/vim)

## Os comandos Vim

Agora que você tem o Vim instalado, rode esse comando no terminal:

```bash
vim
```
Você deve ver uma tela introdutória, essa é onde você estará trabalhando em seus novos arquivos. Diferente da maioria dos editores de texto e IDEs, Vim é um editor modal. Se você quiser digitar "hello", você precisa trocar para o modo de inserção (insert mode) clicando no `i`. Digite `ihello<Esc>` para inserir o texto "hello".

## Saindo do Vim

Existem várias formas de sair do Vim, a mais comum é digitar:

```
:quit
```

Você também pode digitar `:q` para abreviar. Esse é um comando do modo linha de comando (command-line mode). Se você digitar `:` no modo normal (normal mode), o cursor irá deslocar-se para a parte inferior da tela onde você pode digitar alguns comandos. Você aprenderá sobre a linha de comando mais tarde no capítulo 15. Se você está no modo de inserção, digitar `:` produzirá literalmente o carácter ":" na tela. Nesse caso, você precisa mudar para o modo normal, pressione `<Esc>` para trocar. Portanto, você pode retornar ao modo normal estando modo linha de comando pressionando `<Esc>`. Você notará que você pode sair de vários modos do Vim de volta ao modo normal pressionando `<Esc>`.

## Salvando um arquivo

Para salvar suas alterações, digite:

```
:write
```

Você também pode digitar `:w` para abreviar. Se esse é um arquivo novo, você precisa dar um nome a ele antes para poder salva-lo. Vamos nomeia-lo `file.txt`. Rode:

```
:w file.txt
```

Para salvar e sair, você pode combinar os comandos `:w` e `:q`:

```
:wq
```

Para sair sem salvar nenhuma mudança, adicione `!` depois do `:q` para forçar a saída:

```
:q!
```

Há outras maneiras de sair do Vim, mas essas são as que você usará diariamente.

## Ajuda
Ao longo deste guia, vou remetê-lo para várias páginas de ajuda do Vim. Você pode ir para a página de ajuda digitando `:help {algum-comando}` (`:h` para abreviar). Você pode passar para o comando `:h` um tópico ou nome de um comando como argumento. Por exemplo, para aprender diferentes formas de sair do vim, digite:

```
:h write-quit
```

Como é que eu sabia que devia procurar por "write-quit"? Eu na verdade não sabia. Eu só digitei `:h`, depois "quit", então `<Tab>`. O vim apresenta palavras chaves relevantes para escolher. Se alguma hora você precisar procurar alguma coisa ("Eu acho que o Vim pode fazer isso..."), só digite `:h`, alguma palavra chave e então pressione `<Tab>`.

## Abrindo um arquivo

Para abrir um arquivo (`hello1.txt`) no Vim pelo terminal, rode:

```bash
vim hello1.txt
```

Você também pode abrir multiplos arquivos de uma vez:

```bash
vim hello1.txt hello2.txt hello3.txt
```

O vim vai abrir `hello1.txt`, `hello2.txt` e `hello3.txt`  em buffers separados. Você vai aprender sobre buffers no próximo capítulo.


## Argumentos
Você pode passar o comando `vim` no terminal com diferentes flags e opções.

Para checar a versão corrente do vim, execute:

```bash
vim --version
```
Isso chama a versão corrente do vim e todas funcionalidades disponíveis marcadas com `+` ou `-`. Algumas funcionalidades neste guia requerem que certas funcionalidades estejam disponíveis. Por exemplo, você vai explorar o histórico da linha de comando do Vim no próximo capítulo com o comando `:history`. Seu Vim precisa ter a funcionalidade `+cmdline_history` para funcionar. Há uma boa chance que o Vim que você instalou tenha todas as funcionalidades necessárias, especialmente se foi por uma fonte de download popular.

Muitas coisas que você pode fazer no terminal também podem ser feitas dentro do Vim. Para ver a versão *dentro* do Vim, você pode rodar isso:

```
:version
```

Se você quer abrir um arquivo `hello.txt` e imediatamente executar um comando Vim, você pode passar para o comando `vim` a opção `+{cmd}`.

No vim, você pode substituir palavras com o comando `:s` (abreviação de `:substitute`). Se você quer abrir `hello.txt` e substituir todos "pancake" por "bagel", rode:

```bash
vim +%s/pancake/bagel/g hello.txt
```

Esses comandos Vim pode ser empilhados:

```bash
vim +%s/pancake/bagel/g +%s/bagel/egg/g +%s/egg/donut/g hello.txt
```

Vim substituirá todas instâncias de "pancake" por "bagel", então substitui "bagel" por "egg", então substitui "egg" por "donut" (você vai aprender substituições em um capítulo posterior).

Você também pode passar a opção `-c` seguido de um comando Vim em vez da sintaxe `+`:

```bash
vim -c %s/pancake/bagel/g hello.txt
vim -c %s/pancake/bagel/g -c %s/bagel/egg/g -c %s/egg/donut/g hello.txt
```

## Abrindo Multiplas Janelas

Você pode iniciar o Vim em janelas divididas no horizontal e vertical com as opções `-o` e `-O`, respectivamente. 

Para abrir o Vim com duas janelas horizontais, execute:

```bash
vim -o2
```

Para abrir o Vim com 5 janelas horizontais, execute:

```bash
vim -o5
```

Abra o Vim com 5 janelas horizontais e preencha as duas primeiras com `hello1.txt` e `hello2.txt`, execute:

```bash
vim -o5 hello1.txt hello2.txt
```

Para abrir o Vim com 2 janelas verticais, 5 janelas verticais e 5 janelas verticais com 2 arquivos: 

```bash
vim -O2
vim -O5
vim -O5 hello1.txt hello2.txt
```

## Suspendendo

Se você precisa suspender o Vim enquanto está no meio da edição, você pode pressionar `Ctrl-z`. Você pode executar também os comandos `:stop` ou `:suspend`. Para retornar ao Vim suspenso, execute o comando `fg` no terminal. 

## Iniciando o Vim de Forma Inteligente

O comando `vim` pode ter várias opções diferentes, bem como qualquer outro comando de terminal. Duas opções permitem você passar um comando Vim como parâmetros: `+{cmd}` e `-c cmd`. À medida que você aprende mais comandos ao longo desse guia, tente aplicá-los quando iniciar o Vim. Por ser um comando de terminal, você pode combinar `vim` com muitos outros comandos de terminais. Por exemplo, você pode redirecionar a saida do comando `ls` para ser editada no Vim com `ls -l | vim -`.

Aprenda mais sobre comandos `vim` no terminal, verifique o `man vim`. Aprenda mais sobre o editor vim, continue lendo esse guia juntamente com o comando `:help`.