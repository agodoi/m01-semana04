# Horários de Atendimento do Prof. André Godoi

* Plantão de dúvidas, toda terça e quinta-feira, das 8h30 às 10h, e das 14h às 15h30.

* Demais dias, deixar mensagem no Slack que respondo assim que possível, pois o professor não é 40h no Inteli, e por isso, assim que possível, ele responderá as mensagens.

* Final de semana: é dia de maldade, sem atendimento urgente! Eventualmente, poderei responder.

* Monitorias:
  *   Turma 11: Filipi Kikuchi (filipi.kikuchi@sou.inteli.edu.br), que atenderá quartas e sextas-feiras, das 8h30 às 9h30 e das 12h45 às 13h45 no ateliê da turma.
  *   Turma 13: Fernando Vasconcellos (fernando.vasconcellos@sou.inteli.edu.br), atenderá nas segundas e quartas-feiras, das 8h30 às 9h30 no ateliê da turma e outras 2h de atendimento será por pedidos feitas no e-mail dele.


# Gerenciando Cenas e Recursos: Phaser com múltiplas cenas

# Descrição
Interações e desenvolvimento do jogo quando há múltiplas cenas e classes, incluindo o gerenciamento de variáveis globais e parâmetros. Além disso, exemplificação da importância das convenções para desenvolvimento de códigos de mais fácil entendimento.

# Assuntos relacionados
Programação orientada a objetos

## 1) Introdução

Phaser é uma plataforma incrível para a criação de jogos. Propociona uma relativa facilidade, além de suporte à física do jogo. É popular o suficiente para que você possa encontrar plug-ins e ferramentas para criar jogos melhores e mais rápido. É baseado em tecnologias HTML5, o que significa que você pode criar jogos que podem ser distribuídos pela Web, mas também empacotados como aplicativos de desktop ou móveis, se desejar.

## 2) Como criar um cenário simples

```
function preload() {}

function create() {}

new Phaser.Game({
  width: 450,
  height: 600,
  scene: {
    preload,
    create
  }
})
```

Explicação das linhas:

1. `function preload() {}`: aqui é definida uma função vazia chamada `preload`. No Phaser, a função `preload` é usada para carregar recursos do jogo, como imagens, áudios, etc. Mas neste exemplo, a função está vazia, o que significa que nenhum recurso está sendo carregado durante a fase de pré-carregamento do jogo.

2. `function create() {}`: similarmente, uma função vazia chamada `create` é definida. A função `create` no Phaser é usada para configurar elementos do jogo, como criar personagens, adicionar obstáculos, etc. Neste exemplo, a função também está vazia, o que significa que nenhum elemento do jogo está sendo criado ou configurado inicialmente.

3. `new Phaser.Game({})`: nessa linha é criada uma nova instância de jogo usando a classe `Phaser.Game`. Este é o ponto de entrada para criar um jogo Phaser.

4. `{ width: 450, height: 600, scene: { preload, create } }`: dentro do construtor de `Phaser.Game`, um objeto de configuração é passado. Este objeto de configuração define várias propriedades do jogo:
   - `width`: define a largura do jogo como 450 pixels.
   - `height`: define a altura do jogo como 600 pixels.
   - `scene`: define as cenas do jogo. Uma cena no Phaser é onde a lógica do jogo acontece. Neste caso, a cena é definida como um objeto que tem duas propriedades: `preload` e `create`, que são referências para as funções `preload` e `create` definidas anteriormente. Isso significa que essas duas funções serão chamadas automaticamente durante a execução do jogo, conforme especificado pela estrutura do Phaser.

Resumindo, esse código define um jogo Phaser com uma largura de 450 pixels e altura de 600 pixels, mas sem carregar nenhum recurso ou criar nenhum elemento do jogo inicialmente. As funções `preload` e `create` estão vazias, então nada é carregado ou criado durante a inicialização do jogo.
```

Um jogo geralmente tem várias cenas. Você pode criar cada cena em seu arquivo separado e passá-las para a propriedade scene, mas desta vez como um array.

Neste caso as cenas são criadas estendendo o objeto Phaser.Scene.

Por exemplo, você pode criar uma cena de boas-vindas num arquivo ```bem-vindo.js```. Exemplo:

```
export default class Scene1 extends Phaser.Scene {
  constructor() {
    super('welcome')
  }

  create() {
    this.add.text(20, 20, 'Loading..')

    setTimeout(() => {
      this.scene.start('game')
    }, 2000)
  }
}
```

E daí, o jogo ficaria numa outra cena, em um outro arquivo ```java.js```. Exemplo:

```
export default class Scene2 extends Phaser.Scene {
  constructor() {
    super('game')
  }

  create() {
    this.add.text(20, 20, 'Playing game!')
  }
}
```

Note that we have the create() method here. We can also have preload() and update() like we did previously.

And we import them and pass them to the scene property into our main game file:

```
import Phaser from 'phaser'
import Welcome from './Welcome'
import Game from './Game'

const config = {
  width: 800,
  height: 600,
  backgroundColor: 0x000000,
  scene: [Welcome, Game]
}

const game = new Phaser.Game(config)
```

O que acontece agora é que temos a primeira cena listada (Bem-vindo) começando e chamamos this.scene.start('game') para passar para a cena do jogo após 2 segundos.
