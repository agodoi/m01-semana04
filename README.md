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
