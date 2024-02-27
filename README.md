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


### 2.1) Entenda o que é uma classe em JavaScript

Em JavaScript, uma classe é uma estrutura que define um tipo de objeto, especificando os membros (propriedades e métodos) que os objetos desse tipo terão. Classes em JavaScript foram introduzidas na especificação ECMAScript 2015 (também conhecida como ES6) e são uma forma de implementar o paradigma de programação orientada a objetos (OOP) na linguagem.

Aqui está um exemplo básico de como definir uma classe em JavaScript:

```
class Pessoa {
  constructor(nome, idade) {
    this.nome = nome;
    this.idade = idade;
  }

  saudacao() {
    console.log(`Olá, meu nome é ${this.nome} e eu tenho ${this.idade} anos.`);
  }
}

// Exemplo de uso da classe Pessoa
const pessoa1 = new Pessoa('Alice', 30);
pessoa1.saudacao(); // Saída: Olá, meu nome é Alice e eu tenho 30 anos.
```

Neste exemplo, `Pessoa` é uma classe que tem dois membros: `nome` e `idade`, definidos no construtor, e um método chamado `saudacao`. Podemos criar objetos (`pessoa1`) a partir dessa classe usando a palavra-chave `new` e acessar seus membros e métodos.

Classes em JavaScript oferecem uma sintaxe mais clara e familiar para a criação de tipos de objetos e herança de protótipos em comparação com as abordagens anteriores baseadas em funções construtoras e protótipos. No entanto, é importante notar que, apesar do uso da palavra-chave `class`, JavaScript ainda é uma linguagem orientada a protótipos, e as classes são uma camada de abstração sobre a herança prototípica existente na linguagem.

**Continuando com os conceitos de cenas do Phaser...**

Um jogo geralmente tem várias cenas. Você pode criar cada cena em seu arquivo ```*.js``` separado e passá-las para a propriedade scene, mas desta vez como um array.

Neste caso as cenas são criadas estendendo o objeto ```Phaser.Scene```, como abaixo.

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

export default class Cena-01 extends Phaser.Scene {
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

Temos uma classe chamada `Cena-01`, que estende a classe `Phaser.Scene`. Esta classe representa uma cena no jogo Phaser. Então note:

1. `export default class Scene1 extends Phaser.Scene {`: aqui, estamos exportando (tornando disponível para outros arquivos) uma classe chamada `Cena-01` como o padrão da exportação. Essa classe estende `Phaser.Scene`, o que significa que `Cena-01` é uma subclasse de `Phaser.Scene`. Isso permite que `Cena-01` herde todas as funcionalidades e métodos de `Phaser.Scene`.

2. `constructor() { super('BemVindo') }`: O construtor da classe `Scene1` é definido aqui. Quando uma nova instância de `Scene1` é criada, o construtor da classe `Phaser.Scene` é chamado primeiro com o parâmetro `'BemVindo'`. Isso define o nome da cena como `'BemVindo'`. O construtor também chama o construtor da classe pai usando `super()`, garantindo que todas as inicializações necessárias da classe pai sejam feitas.

3. `create() { ... }`: é um método específico do Phaser chamado `create()`. Ele é chamado automaticamente quando a cena é iniciada e é onde você configura os elementos da cena, como sprites, textos, etc.

4. `this.add.text(20, 20, 'Carregando...')`: dentro do método `create()`, um texto é adicionado à cena na posição (20, 20) com o conteúdo `'Carregando...'`. Isso cria um texto na tela que diz "Carregando..." quando a cena é iniciada.

5. `setTimeout(() => { this.scene.start('game') }, 2000)`: dentro do método `create()`, um temporizador é configurado usando `setTimeout`. Isso faz com que uma função seja executada após um atraso de 2000 milissegundos (o correto é usar milisegundos). Dentro dessa função, `this.scene.start('game')` é chamado. Isso inicia a cena chamada `'game'`. Portanto, após 2 segundos da inicialização da cena `'BemVindo'`, a cena `'game'` será iniciada.

Em resumo, essa classe `Cena-01` define uma cena no jogo Phaser chamada `'BemVindo'`, onde um texto `'Carregando...'` é exibido e, após 2 segundos, a cena `'game'` é iniciada.

### 2.2) Entenda o que é um método

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

## 3) Outro exemplo de Múltiplas Cenas usando HTML

```
<!DOCTYPE html>
<html>
    <head>
        <script src="//cdn.jsdelivr.net/npm/phaser@3.24.1/dist/phaser.min.js"></script>
        <script src="cena-01.js"></script>
        <script src="cena-02.js"></script>
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

### 3.1) Criando os Arquivos JS

No arquivo **cena-01.js**, vai esse código:

 ```
var Cena-01 = new Phaser.Class({
    Extends: Phaser.Scene,
    initialize: function() {
        Phaser.Scene.call(this, { "key": "Cena-01" });
    },
    init: function() {},
    preload: function() {
        this.load.image("plane", "plano.png"); //aqui você coloca a imagem desejada
    },
    create: function() {
        this.plane = this.add.image(640, 360, "plane");
    },
    update: function() {}
});
```

No arquivo **cena-02.js**, vai esse código:

```
var Cena-02 = new Phaser.Class({
    Extends: Phaser.Scene,
    initialize: function() {
        Phaser.Scene.call(this, { "key": "Cena-02" }); //presta a atenção nessa CHAVE pois ela será utilizada no chaveamento de cenas
    },
    init: function() {},
    preload: function() {},
    create: function() {
        var text = this.add.text(
            640, 
            360, 
            "Olá Mundo", 
            {
                fontSize: 50,
                color: "#000000",
                fontStyle: "bold"
            }
        ).setOrigin(0.5);
    },
    update: function() {}
});
```

No arquivo ```index.html```, vamos modificar o ```phaserConfig``` conforme a seguir:

```
const phaserConfig = {
    type: Phaser.AUTO,
    parent: "game",
    width: 1280,
    height: 720,
    backgroundColor: "#5DACD8",
    scene: [ Cena-01, Cena-02 ]
};
```

Observe que as 2 cenas foram adicinadas num array [vetor]. A ordem é importante porque a primeira cena do array será a cena padrão. Você sempre pode navegar entre eles, mas é importante saber qual deles será exibido primeiro.

Agora que temos várias cenas, cada uma com seus próprios eventos de ciclo de vida, provavelmente desejaremos alternar entre elas e até mesmo passar dados entre elas. Antes de nos preocuparmos com o lado dos dados, vamos nos concentrar apenas na mudança.

A ideia é a seguinte:

1) Mostre a primeira cena do SceneOne.
2) Espere um certo tempo.
3) Navegue até a segunda cena do Cena-02.
4) Idealmente, você provavelmente desejaria alternar cenas com base em alguma interação de objeto do jogo, mas para fins de demonstração, um cronômetro será suficiente.

Na função ```create``` do arquivo **Cena-01.js**, altere-o para ficar assim:

```
create: function() {
    this.plane = this.add.image(640, 360, "plane");
    this.time.addEvent({
        delay: 3000,
        loop: false,
        callback: () => {
            this.scene.start("Cena-02");
        }
    })
},
```

Observe o uso do cronômetro. Após três segundos, a próxima cena nomeada começará. Quando a próxima cena começa, ela passa por cada um dos eventos do ciclo de vida necessários para configurar e renderizar a cena.

Se não fizéssemos mais nada, nosso código funcionaria. No entanto, pode fazer sentido passar dados de uma cena para outra. Um exemplo é com informações de pontuação. Talvez a primeira cena seja a cena do jogo e você esteja acumulando pontuação. Então talvez a segunda cena seja uma cena de fim de jogo que deve exibir a pontuação. 

Bem, você precisará transferir a pontuação para a nova cena, então este exemplo pode ser útil.

Dentro da função ```create``` do arquivo **Cena-01.js**, altere ligeiramente o ```scene.start``` para ficar assim:

```
this.scene.start("Cena-02", { 
    "message": "Game Over" 
});
```

Observe que desta vez estamos passando um objeto. A chave e os valores neste objeto podem ser o que você quiser.

Como estamos passando valores, precisamos de uma forma de recebê-los na próxima cena. Na função ```init``` do arquivo **Cena-02.js**, altere-o para ficar assim:

```
init: function(data) {
    this.message = data.message;
},
```

Observe que esta função está aceitando um parâmetro. Esse parâmetro são os dados da cena anterior. Precisamos configurá-lo para uma variável de cena com escopo local para que possa ser acessado durante todos os eventos do ciclo de vida de nossa cena.

Agora vamos modificar a função ```create``` no mesmo arquivo:

```
create: function() {
    var text = this.add.text(
        640, 
        360, 
        this.message, 
        {
            fontSize: 50,
            color: "#000000",
            fontStyle: "bold"
        }
    ).setOrigin(0.5);
},
```

Observe que em vez de renderizar “Olá Mundo”, agora estamos renderizando a mensagem que foi passada na cena anterior.

## 4) Casos de Testes

Para elaborar um caso de teste para o programa anterior, vamos considerar que o programa envolve a configuração e início de um jogo Phaser simples, conforme mostrado no código HTML fornecido. Aqui está um caso de teste possível:

### Caso de Teste: Configuração e Início do Jogo Phaser

#### Descrição:
Este caso de teste avalia se o jogo Phaser é configurado corretamente e se é iniciado com sucesso na página web.

#### Pré-condições:
- O navegador da web está aberto e carregou a página HTML contendo o código do jogo Phaser.

#### Passos:
1. Verificar se a página HTML foi carregada corretamente no navegador.
2. Verificar se a biblioteca Phaser foi carregada corretamente a partir do CDN fornecido.
3. Verificar se os arquivos "cena-01.js" e "cena-02.js" foram carregados corretamente.
4. Verificar se a `div` com o id "game" está presente na página HTML.
5. Verificar se o jogo Phaser é iniciado corretamente.

#### Resultados Esperados:
- Todos os passos do caso de teste são bem-sucedidos.
- O jogo Phaser é iniciado com sucesso dentro da `div` com o id "game".
- Não há erros visíveis na execução do jogo na página web.

#### Observações:
- Este caso de teste é uma verificação básica para garantir que o jogo Phaser seja carregado e iniciado corretamente na página web.
- Testes adicionais podem ser elaborados para verificar o comportamento do jogo, interações do usuário, funcionalidades específicas das cenas, entre outros aspectos, dependendo dos requisitos do jogo e do projeto.

Para adicionar mais detalhes ao seu GDD, se inspire nessa tabela da [web.dev](https://web.dev/articles/ta-test-cases?hl=pt-br).

## 5) Mapa de Ladrilhos

Ao criar um mapa de ladrilhos (tiles) para um jogo, é importante considerar vários conceitos e técnicas para garantir um design eficiente e visualmente agradável. Aqui estão alguns conceitos importantes a serem considerados durante a edição do mapa de ladrilhos:

1. **Grade de Ladrilhos (Tile Grid)**:
   - Utilizar uma grade de ladrilhos (grid) para organizar o mapa. Cada célula da grade corresponde a um ladrilho (tile) no mapa do jogo.

2. **Ladrilhos (Tiles)**:
   - Escolher uma variedade de ladrilhos que representem diferentes tipos de terreno, objetos, elementos decorativos, etc., dependendo do estilo e tema do jogo.

3. **Paleta de Cores (Color Palette)**:
   - Selecionar uma paleta de cores consistente e harmoniosa para os ladrilhos, garantindo que eles se encaixem bem visualmente e criem uma atmosfera coesa no jogo.

4. **Consistência Visual**:
   - Manter uma consistência visual em todo o mapa, garantindo que os ladrilhos se encaixem sem problemas e que o estilo artístico seja uniforme.

5. **Reutilização de Ladrilhos**:
   - Reutilizar ladrilhos sempre que possível para otimizar o uso de recursos e reduzir a carga no desempenho do jogo.

6. **Camadas (Layers)**:
   - Utilizar camadas para organizar elementos diferentes do mapa, como terrenos, objetos, fundos, etc., e para criar efeitos de profundidade e paralaxe.

7. **Colisão**:
   - Definir áreas de colisão nos ladrilhos, se necessário, para que os personagens e objetos do jogo possam interagir corretamente com o ambiente.

8. **Detalhamento Gradual**:
   - Adicionar detalhes progressivamente ao mapa, começando com uma estrutura básica e adicionando detalhes finos e decorações conforme necessário.

9. **Testes e Ajustes**:
   - Testar o mapa em diferentes resoluções de tela e dispositivos para garantir que os ladrilhos se ajustem corretamente e que não haja problemas visuais ou de jogabilidade.

10. **Feedback dos Jogadores**:
    - Solicitar feedback dos jogadores sobre o design do mapa, especialmente em relação à jogabilidade, clareza visual e estética geral.

Ao considerar esses conceitos durante a edição do mapa de ladrilhos, é possível criar um ambiente de jogo visualmente atraente, funcional e envolvente para os jogadores.

Um exemplo pode ser baixado [AQUI](https://drive.google.com/file/d/1cbRfl5-EBkD18Sf_7WHttUZ965aCNqJc/view?usp=drive_link)
