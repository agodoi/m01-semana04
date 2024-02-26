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


Um jogo geralmente tem várias cenas. Você pode criar cada cena em seu arquivo separado e passá-las para a propriedade scene, mas desta vez como um array.

Neste caso as cenas são criadas estendendo o objeto Phaser.Scene.

Por exemplo, você pode criar uma cena de boas-vindas num arquivo ```BemVindo.js```. Exemplo:

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

export default class Scene1 extends Phaser.Scene {
  constructor() {
    super('BemVindo')
  }

  create() {
    this.add.text(20, 20, 'Carregando...')

    setTimeout(() => {
      this.scene.start('game')
    }, 2000)
  }
}
```

Explicando as linhas anteriores:

Temos uma classe chamada `Scene1`, que estende a classe `Phaser.Scene`. Esta classe representa uma cena no jogo Phaser. Então note:

1. `export default class Scene1 extends Phaser.Scene {`: aqui, estamos exportando (tornando disponível para outros arquivos) uma classe chamada `Scene1` como o padrão da exportação. Essa classe estende `Phaser.Scene`, o que significa que `Scene1` é uma subclasse de `Phaser.Scene`. Isso permite que `Scene1` herde todas as funcionalidades e métodos de `Phaser.Scene`.

2. `constructor() { super('BemVindo') }`: O construtor da classe `Scene1` é definido aqui. Quando uma nova instância de `Scene1` é criada, o construtor da classe `Phaser.Scene` é chamado primeiro com o parâmetro `'BemVindo'`. Isso define o nome da cena como `'BemVindo'`. O construtor também chama o construtor da classe pai usando `super()`, garantindo que todas as inicializações necessárias da classe pai sejam feitas.

3. `create() { ... }`: é um método específico do Phaser chamado `create()`. Ele é chamado automaticamente quando a cena é iniciada e é onde você configura os elementos da cena, como sprites, textos, etc.

4. `this.add.text(20, 20, 'Loading..')`: dentro do método `create()`, um texto é adicionado à cena na posição (20, 20) com o conteúdo `'Carregando...'`. Isso cria um texto na tela que diz "Carregando..." quando a cena é iniciada.

5. `setTimeout(() => { this.scene.start('game') }, 2000)`: dentro do método `create()`, um temporizador é configurado usando `setTimeout`. Isso faz com que uma função seja executada após um atraso de 2000 milissegundos (o correto é usar milisegundos). Dentro dessa função, `this.scene.start('game')` é chamado. Isso inicia a cena chamada `'game'`. Portanto, após 2 segundos da inicialização da cena `'BemVindo'`, a cena `'game'` será iniciada.

Em resumo, essa classe `Scene1` define uma cena no jogo Phaser chamada `'BemVindo'`, onde um texto `'Carregando...'` é exibido e, após 2 segundos, a cena `'game'` é iniciada.

### O que é um método?

No código fornecido, um método é uma **função** que está definida **dentro de uma classe** e pode ser **chamada nos objetos dessa classe**. No contexto do código apresentado, temos o **método `create()` dentro da classe `Scene1`**. Este método é chamado automaticamente quando a cena é iniciada no jogo Phaser.

Dentro do método `create()`, estão sendo realizadas várias operações, como adicionar um texto à cena e configurar um temporizador para iniciar outra cena após um certo período de tempo. Essas operações específicas definem o comportamento inicial da cena `'BemVindo'` no jogo.

Em JavaScript, métodos são essenciais para encapsular a lógica relacionada a um objeto específico e promover a reutilização do código. Eles permitem que você defina o comportamento dos objetos em termos de como eles respondem a determinadas mensagens ou invocações. No contexto de uma classe em JavaScript, os métodos são apenas funções que estão definidas como propriedades da classe.

Continuando com o código anterior, além do jogo ter uma tela de saudação, o jogo ficaria numa outra cena, em um outro arquivo ```jogo.js```. Exemplo:

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

Observe que temos o método ``create()`` aqui. E também podemos ter ```preload()``` e ```update()``` como vimos anteriormente.

Mas agora, os importamos e os passamos para a propriedade ```scene``` em nosso arquivo principal do jogo:

```
import Phaser from 'phaser'
import BemVindo from './BemVindo'
import Game from './Game'

const config = {
  width: 800,
  height: 600,
  backgroundColor: 0x000000,
  scene: [BemVindo, Game]
}

const game = new Phaser.Game(config)
```

O que acontece agora é que temos a primeira cena listada (BemVindo) iniciando e chamamos ```this.scene.start('game')``` para passar para a cena do jogo após 2 segundos.

**Portanto, agora você já sabe como fazer múltiplas classes (cenas)**.


Ao criar um jogo, provavelmente você terá mais de uma tela. Por exemplo, você pode ter uma tela de menu inicial, uma tela principal de jogo e uma tela de fim de jogo. Essas telas podem ser pensadas como cenas de um jogo, da mesma forma que você pode pensar nas cenas de um filme.

Cada cena que você tem no jogo representa uma lousa em branco ou um novo ponto de partida para aquela subseção específica de conteúdo.

Neste tutorial, veremos como criar múltiplas cenas, alternar entre elas e passar dados entre elas, usando Phaser 3.x e JavaScript simples.

## 3) Outro exemplo Múltiplas Cenas usando HTML

```
<!DOCTYPE html>
<html>
    <head>
        <script src="//cdn.jsdelivr.net/npm/phaser@3.24.1/dist/phaser.min.js"></script>
        <script src="scene-one.js"></script>
        <script src="scene-two.js"></script>
    </head>
    <body>
        <div id="game"></div>
        <script>

            const phaserConfig = {
                type: Phaser.AUTO,
                parent: "game",
                width: 1280,
                height: 720,
                backgroundColor: "#5DACD8",
                scene: [ ]
            };

            const game = new Phaser.Game(phaserConfig);

        </script>
    </body>
</html>
```

**Explicando...**

Este é um exemplo básico de como configurar um jogo usando a biblioteca Phaser dentro de uma página HTML. Detalhes:

1. `<!DOCTYPE html>`: declaração do tipo de documento para especificar que o documento é um HTML5.

2. `<html>...</html>`: elemento raiz que envolve todo o conteúdo HTML.

3. `<head>...</head>`: contém metadados e referências a recursos utilizados pela página.

4. `<script src="//cdn.jsdelivr.net/npm/phaser@3.24.1/dist/phaser.min.js"></script>`: importa a biblioteca Phaser. Neste caso, está sendo utilizado o CDN (Content Delivery Network) fornecido pelo jsDelivr para incluir a versão 3.24.1 da biblioteca Phaser.

5. `<script src="cena-01.js"></script>`: importa um arquivo JavaScript chamado "cena-01.js". Presumivelmente, este arquivo contém a definição de uma cena para o jogo.

6. `<script src="cena-02.js"></script>`: importa outro arquivo JavaScript chamado "cena-02.js". Da mesma forma que o anterior, este arquivo provavelmente contém a definição de outra cena para o jogo.

7. `<body>...</body>`: contém todo o conteúdo visível da página HTML.

8. `<div id="game"></div>`: define uma `div` com o id "game". É dentro desta `div` que o jogo Phaser será renderizado. Uma "div" é um elemento HTML que serve como um contêiner genérico para outros elementos HTML. Ela é frequentemente usada para agrupar e organizar conteúdo dentro de uma página da web. A palavra "div" é uma abreviação de "division" (divisão), e é usada para dividir o conteúdo da página em seções distintas.

9. `<script>...</script>`: contém o código JavaScript que configura e inicia o jogo Phaser.

    - `const phaserConfig = { ... };`: define um objeto de configuração para o jogo Phaser. As propriedades desse objeto incluem o tipo de renderização (`type`), o elemento pai onde o jogo será renderizado (`parent`), as dimensões do jogo (`width` e `height`), a cor de fundo do jogo (`backgroundColor`) e a lista de cenas (`scene`). Por enquanto, a lista de cenas está vazia.

    - `const game = new Phaser.Game(phaserConfig);`: cria uma nova instância do jogo Phaser com as configurações especificadas no objeto `phaserConfig`. Esta instância é armazenada na variável `game`.

De forma geral, este código HTML configura uma página web para carregar e executar um jogo criado com Phaser, especificando o tamanho do jogo, a cor de fundo e os scripts que contêm as definições das cenas do jogo.

