# Ch00. Leia isso primeiro

## Por que esse guia foi escrito

Há muitos lugares para aprender Vim: o `vimtutor` é um grante lugar para começar e o manual `:help` tem todas as referencias que você pode precisar.

Contudo, o usuário médio precisa de algo mais que `vimtutor` e menos que o manual `:help`. Esse guia busca preencher esse espaço destacando apenas as funções chave para aprender as partes mais úteis do Vim no menor tempo possível.

Provavelmente você não precisará de 100% das funcões do Vim. Você provavelmente somente precisará saber uns 20% delas para se tormar um poderoso Vimmer. Esse guia irá te mostrar quais funções do Vim você achará mais uteis.

Esse é um guia opinativo. Ele cobrirá técnicas que eu frequentemente uso quando uso Vim. Os capítulos são sequenciados baseados no que eu acho que faria mais sentido para um iniciante aprender Vim.

Esse guia é cheio de exemplos. Quando aprendemos uma nova habilidade, exemplos são indispensáveis, ter numerosos exemplos solidificará os conceitos mais efetivamente.

Alguns de vocês podem imaginar o por que você precisa aprender Vimscript? No meu primeiro ano usando Vim, eu estava contente apenas sabendo como usar Vim. O tempo passou e eu comecei a precisar de Vimscript mais e mais para escrever comandos personalizados para minhas necessidades de edição específicas. Conforme você vai dominando Vim, cedo ou tarde você precisará aprender Vimscript. Então por que não cedo? Vimscript é a uma pequena linguagem. Você pode aprender o básico em apenas 4 capítulos desse guia.

Você pode ir longe usando Vim sem saber nada de Vimscript, mas saber disso o ajudará a se destacar ainda mais.

Esse guia é escrito para ambos, Vimmers iniciantes e avançados. Ele começa com amplos e simples conceitos e termina com conceitos específicos e avançados. Se você já for um usuário avançado, eu te encorajaria a ler esse guia do começo ao fim do mesmo jeito, porque você irá aprender alguma coisa nova!

## Como fazer a transição para o Vim usando um editor de texto diferente

Aprender Vim é uma experiência satisfatória, embora difícil. Há duas principais abordagens para aprender Vim:

1. Cold turkey 
2. Gradual

Indo pela cold turkey significa parar de usar qualquer editor / IDE que você tem usado e usar exclusivamente o Vim a partir de agora. O contra desse método é que você terá uma séria perda de produtividade durante a primeira ou segunda semana. Se você é um programador de tempo integral, esse método pode não ser viável. Esse é o porque para a maioria das pessoas, eu acredito que o melhor jeito de fazer essa transição para Vim é usá-lo gradualmente.

Para gradualmente usar Vim, durante as primeiras duas semanas, gaste 1 hora do dia usando Vim como seu editor enquanto o resto do tempo voce pode usar outros editores. Muitos editores modernos vem com plugins Vim. Quando eu comecei, eu usei o popular plugin Vim do VSCode por uma hora por dia. Eu gradualmente aumentei o tempo com o plugin Vim até eu finalmente usá-lo o dia todo. Tenha em mente que esses plugins podem apenas emular uma parte das funções do Vim. Para ter uma experiência do completo poder do Vim como Vimscript, comandos de linha de comando (Ex), e integração de comandos externos, você precisará usar o próprio Vim.

Houveram dois momentos cruciais que me fizeram começar usar Vim 100%: quando eu percebi que Vim tem uma estrutura semelhante a uma gramática (ver capítulo 4) e o plugin [fzf.vim](https://github.com/junegunn/fzf.vim) (ver capítulo 4).

O primeiro, quando eu percebi a estrutura semelhante a uma gramática do Vim, foi o momento definidor que eu finalmente entendi o que aqueles usuários Vim falavam. Eu não precisei aprender centenas de comandos únicos. Eu só tive que aprender poucos e úteis comandos e eu pude encadear de uma forma muito intuitiva para fazer muitas coisas.

A segunda, a habilidade de executar rapidamente uma pesquisa difusa de arquivos foi a função IDE que eu mais usei. Quando eu aprendi como fazer isso no Vim, eu ganhei um grande aumento de velocidade e nunca mais olhei pra trás.

Todo mundo programa diferentemente. Após introspecção, você encontrará uma ou duas funções
do seu editor/IDE favoritos que você usa o tempo todo. Talvez seja a pesquisa difusa, pular-para, ou compilação rápida. Seja o que for que eles possam ter, identifique eles rapidamente e aprenda como implementá-lo no Vim (Provavelmente o Vim possa tê-las também). Seu editor rapidamente receberá um grande impulso.

Uma vez que você edite na metade da velocidade original, é hora de ir para o Vim em tempo integral.

## Como ler este guia

Este é um guia prático. Para se tornar bom em Vim você precisa desenvolver memória muscular, mas não antes de aprender.

Você não aprende como andar de bicicleta lendo um guia sobre como andar de bicicleta. Você precisa de fato andar de bicicleta.

Você precisa digitar cada comando referido nesse guia. Não apenas isso, mas você precisa repeti-lo várias vezes e tentar diferentes combinações. Veja quais outros recursos o comando que você acabou de aprender possui. O comando `:help` e mecanismos de busca são seus melhores amigos. Seu objetivo não é saber tudo sobre um comando, mas ser capaz de executá-lo natural e instintivamente.

Por mais que eu tente moldar esse guia para ser linear, alguns conceitos nesse guia precisam ser apresentados fora de ordem No capítulo 1, por exemplo, eu mencionei o comando de substituição (`:s`), apesar de não ser abordando até o capítulo 12. Para remediar isso, sempre que um novo conceito que ainda não foi abordado for mencionado, eu farei uma rápida explicação sem muitos detalhes. Então por favor tenha paciência comigo :).

## Mais ajuda

Aqui está mais uma dica extra para usar o manual help: suponha que você quer aprender mais sobre o que `Ctrl-P` faz no modo de inserção. Se você apenas procurar por `:h CTRL-P`, você será direcionado para o modo normal de `CTRL-P`. Esse não é a ajuda `CTRL-P` que você está procurando. Nesse caso, procure por 
`:h i_CTRL-P`. O prefixo `i_` representa o modo de inserção. Preste atenção a qual modo ele pertence.

## Síntaxe

A maioria dos comandos ou frases relacionadas a código são exibidas (`assim`)

Strings estão entre um par de aspas duplas ("assim").

Comandos Vim pode ser abreviados. Por exemplo, `:join` pode ser abreviado como `:j`. Através do guia, eu irei misturar formas curtas e longas das descrições. Para comandos que não são frequentemente usados nesse guia eu usarei a  versão longa. Para comandos frequentemente usados, eu usarei a versão curta. Me desculpem pela inconsistência. Em geral, sempre que você encontrar um novo comando, verifique-o em `:help` para ver suas abreviações.

## Vimrc

Em vários pontos no guia eu vou me referir às opções vimrc. Se você é novo com Vim, um vimrc é como um arquivo de configuração.

Vimrc não será abordado até o capítulo 21. Por uma questão de clareza, eu mostrarei brevemente como configurá-lo.

Suponha que você precise configurar o número de opções (`set number`). Se você ainda não tem um vimrc, crie-o. Ele normalmente é chamado `.vimrc` e fica no diretório home. Dependendo do seu sistema operacional a localização pode diferir. No macOS, ele está em `~/.vimrc`. Para ver ver onde você deve colocar o seu, verifique `:h vimrc`.

Dentro dele, adicione `set number`. Salve-o (`:w`), então obtenha ele (`:source %`). Agora você deverá ver o número das linhas mostrado no lado esquerdo.  

Alternativamente, se você não quiser fazer uma configuração permanente, você sempre pode executar a linha de comando, executando `:set number`. O contra dessa abordagem é que essa configuração é temporária. Quando você fechar o Vim, a opção desaparecerá.

Já que estamos aprendendo sobre o Vim e não Vi, uma configuração que você deve ter é a opção `nocompatible`. Adicione `set nocompatible` no seu vimrc. Muitas características específicas do Vim são desabilitadas quando ele está executando no modo de compatibilidade `compatible`.  

No geral, sempre que uma passagem mencionar uma opção vimrc, apenas adicione ela no seu vimrc, salve e obtenha ele.

## Futuro, Erros e Dúvidas

Espere mais atualizações no futuro. Se você encontrar erros ou tiver qualquer dúvida, sinta-se livre para me contatar.

Eu também planejei mais alguns capítulos futuros, então fique ligado!

## Eu quero mais truques do Vim

Para aprender mais sobre Vim, por favor siga [@learnvim](https://twitter.com/learnvim) (em inglês).

## Agradecimentos - Versão original

Esse guia não seria possível sem Bram Moleenar por criar o Vim, minha esposa por ter sido muito paciente e solidária durante essa jornada, a todos os [contribuidores](https://github.com/iggredible/Learn-Vim/graphs/contributors) do learn-vim project, a comunidade Vim, e muitos, muitos outros que não foram mencionados.

Obrigado. Vocês todos ajudaram a fazer esse texto divertido :)
