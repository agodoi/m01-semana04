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

2. `constructor() { super('BemVindo') }`: O construtor da classe `Cena-01` é definido aqui. Quando uma nova instância de `Cena-01` é criada, o construtor da classe `Phaser.Scene` é chamado primeiro com o parâmetro `'BemVindo'`. Isso define o nome da cena como `'BemVindo'`. O construtor também chama o construtor da classe pai usando `super()`, garantindo que todas as inicializações necessárias da classe pai sejam feitas.

3. `create() { ... }`: é um método específico do Phaser chamado `create()`. Ele é chamado automaticamente quando a cena é iniciada e é onde você configura os elementos da cena, como sprites, textos, etc.

4. `this.add.text(20, 20, 'Carregando...')`: dentro do método `create()`, um texto é adicionado à cena na posição (20, 20) com o conteúdo `'Carregando...'`. Isso cria um texto na tela que diz "Carregando..." quando a cena é iniciada.

5. `setTimeout(() => { this.scene.start('game') }, 2000)`: dentro do método `create()`, um temporizador é configurado usando `setTimeout`. Isso faz com que uma função seja executada após um atraso de 2000 milissegundos (o correto é usar milisegundos). Dentro dessa função, `this.scene.start('game')` é chamado. Isso inicia a cena chamada `'game'`. Portanto, após 2 segundos da inicialização da cena `'BemVindo'`, a cena `'game'` será iniciada.

Em resumo, essa classe `Cena-01` define uma cena no jogo Phaser chamada `'BemVindo'`, onde um texto `'Carregando...'` é exibido e, após 2 segundos, a cena `'game'` é iniciada.

### 2.2) Entenda o que é um método

No código fornecido, um método é uma **função** que está definida **dentro de uma classe** e pode ser **chamada nos objetos dessa classe**. No contexto do código apresentado, temos o **método `create()` dentro da classe `Scene1`**. Este método é chamado automaticamente quando a cena é iniciada no jogo Phaser.

Dentro do método `create()`, estão sendo realizadas várias operações, como adicionar um texto à cena e configurar um temporizador para iniciar outra cena após um certo período de tempo. Essas operações específicas definem o comportamento inicial da cena `'BemVindo'` no jogo.

Em JavaScript, métodos são essenciais para encapsular a lógica relacionada a um objeto específico e promover a reutilização do código. Eles permitem que você defina o comportamento dos objetos em termos de como eles respondem a determinadas mensagens ou invocações. No contexto de uma classe em JavaScript, os métodos são apenas funções que estão definidas como propriedades da classe.

## 3) Criando Multi Cenas

Ao criar um jogo, provavelmente você terá mais de uma tela. Por exemplo, você pode ter uma tela de menu inicial, uma tela principal de jogo e uma tela de fim de jogo. Essas telas podem ser pensadas como cenas de um jogo, da mesma forma que você pode pensar nas cenas de um filme.

Cada cena que você tem no jogo representa uma lousa em branco ou um novo ponto de partida para aquela subseção específica de conteúdo.

Neste tutorial, veremos como criar múltiplas cenas, alternar entre elas e passar dados entre elas, usando Phaser e JavaScript simples.

A seguir, tem-se um exemplo HTML que integra 2 cenas, onde passaremos uma informação de uma cena para a outra.

### Exemplo de Multi Cenas

Então, nesse exemplo, temos a seguinte estrutura de arquivos:

* `index.html` que integra 3 arquivos JS e cria uma caixa de entrada com um botão de confirmação

* `cena01.js` que é a tela que pega o nome digitado ao clicar com mouse sobre o botão
  
* `cena02.js` que é a tela de fundo

* `game.js` que possui o arquivo **config** que constroi o Phaser

Começando com o arquivo `index.html` abaixo:

### 3.1) Arquivo index.html

```
<!doctype html>
<html lang="pt">
<html>
    <head>
        <meta name="viewport" content="width=device-width, initial-scale=1"> <!--adicione essa linha para aplicações web responsivas -->
        <meta charset="UTF-8" /> <!--adicione essa linha para acentos aparecerem corretamente -->
        <title>Mundado de Cenas</title>
        <style>
            body{
                display: flex;
                align-items: center;
                justify-content: center;
            }
            #inputOverlay {
                position: absolute;
                display: flex;
                align-items: center;
                justify-content: center;
                top: 250px;
                left: 50%;
                transform: translateX(-50%);
                display: none;
            }

            input, button {
                padding: 1px;
                font-size: 20px;
            }
        </style>
        <script src="https://cdn.jsdelivr.net/npm/phaser@3/dist/phaser.js"></script>
    </head>
    <body>
        
        <div id="inputOverlay">
            <div class="alinhartext">
                <input type="text" id="nameInput" placeholder="Digite seu nome">
            </div>
            <div class="alinharbotao">
                <button id="startButton">Confirma</button>
            </div>
        </div>

        <script src="Cena02.js"></script>
        <script src="Cena01.js"></script>
        <script src="game.js"></script>
    </body>
</html>
```

#### Explicando o HTML...

**Declaração do tipo de Documento:**

- `<!DOCTYPE html>`: declara o tipo de documento como HTML.

**Elemento `html`:**

- Define a estrutura básica da página web.

**Cabeçalho (`head`):**

- Contém informações metadados sobre a página:
    - `meta name="viewport" content="width=device-width, initial-scale=1"`: define uma meta tag para dispositivos móveis, garantindo que a página tenha a largura do dispositivo e a escala inicial seja 1 (zoom 100%). Isso é uma recomendação do Visual Code, serve para eliminar esse erro que você deve ter aí quando vai codar HTML.
    - `meta charset="UTF-8"`: define o charset da página como UTF-8, permitindo a exibição correta de acentos e caracteres especiais. Também resolve um problema no Visual Code.
    - `title>Mundando de Cenas</title>`: define o título da página como "Mundando de Cenas".

**Estilos (`style`):**

- Aplica estilos CSS à página:
    - `body`:
        - `display: flex`: define o corpo da página como um container flex.
        - `align-items: center`: alinha elementos filhos verticalmente ao centro.
        - `justify-content: center`: alinha elementos filhos horizontalmente ao centro.
    - `#inputOverlay`:
        - `position: absolute`: posiciona o overlay de entrada de forma absoluta.
        - `display: flex`: define o overlay como um container flex.
        - `align-items: center`: alinha elementos filhos do overlay verticalmente ao centro.
        - `justify-content: center`: alinha elementos filhos do overlay horizontalmente ao centro.
        - `top: 250px`: posiciona o overlay 250 pixels a partir do topo.
        - `left: 50%`: posiciona o overlay horizontalmente ao centro (50%).
        - `transform: translateX(-50%)`: desloca horizontalmente o overlay pela metade de sua largura para centralizá-lo corretamente.
        - `display: none`: inicialmente oculta o overlay.
    - `input, button`: estilos aplicados a ambos os elementos:
        - `padding: 1px`: define o espaçamento interno com 1 pixel.
        - `font-size: 20px`: define o tamanho da fonte como 20 pixels.

**Bibliotecas Javascript:**

- `<script src="https://cdn.jsdelivr.net/npm/phaser@3/dist/phaser.js"></script>`: inclui a biblioteca Phaser para desenvolvimento de jogos 2D.

**Conteúdo da Página (`body`):**

- `div id="inputOverlay"`:
    - Define a div do overlay de entrada com o identificador "inputOverlay".
    - Contém duas divs filhas para alinhar o campo de texto e o botão.
        - `div class="alinhartext"`:
            - Define a div para alinhar o texto (possível uso para estilos CSS).
            - `input type="text" id="nameInput" placeholder="Digite seu nome"`:
                - Cria um campo de texto (`<input type="text">`) com o identificador "nameInput".
                - `placeholder="Digite seu nome"`: define um texto de placeholder ("Enter your name") que aparece dentro do campo quando está vazio.
        - `div class="alinharbotao"`:
            - define a div para alinhar o botão (possível uso para estilos CSS).
            - `button id="startButton">Confirma</button>`:
                - Cria um botão (`<button>`) com o texto "Confirma" (Confirm) e o identificador "startButton".

**Scripts do Jogo:**

- `<script src="Cena02.js"></script>`: inclui o script do arquivo "Cena02.js"
- `<script src="Cena01.js"></script>`: inclui o script do arquivo "Cena01.js"
- `<script src="game.js"></script>`: inclui o script do arquivo "game.js"

**Finalização (`</html>`):**

- Fecha a tag `html` finalizando a estrutura da página.

### 3.2) Arquivo Cena01.js 

No arquivo **Cena01.js**, vai esse código:

```
class Cena01 extends Phaser.Scene {
    constructor() {
        super('Cena01');
    }

    create() {
        // Serve para exibir o overlay de entrada
        document.getElementById('inputOverlay').style.display = 'block';

        // Configura o evento de clique no botão
        document.getElementById('startButton').addEventListener('click', () => {
            const playerName = document.getElementById('nameInput').value;
            this.scene.start('Cena02', { playerName: playerName });
            // Oculta o overlay após iniciar
            document.getElementById('inputOverlay').style.display = 'none';
        });
    }
}
```

#### Explicando...

- O Cena01 é uma classe que estende a classe `Phaser.Scene`, indicando que se trata de uma cena dentro do jogo Phaser.
- O construtor (`constructor`) da classe:
    - `super('Cena01');`: chama o construtor da classe pai (`Phaser.Scene`) e define o nome da cena como "Cena01".

- O Método create() é chamado automaticamente pelo Phaser quando a cena é criada.
    - **Exibindo o overlay de entrada:**
        - `document.getElementById('inputOverlay').style.display = 'block';`:
            - Utiliza o método `getElementById` do documento (`document`) para obter o elemento HTML com o identificador "inputOverlay".
            - Acessa a propriedade `style` do elemento para manipular seu estilo CSS.
            - Define o valor da propriedade `display` como "block", tornando o elemento visível.
    - **Configurando o evento de clique no botão:**
        - `document.getElementById('startButton').addEventListener('click', () => { ... });`:
            - Similarmente, obtém o elemento "startButton" e configura um evento de escuta do tipo "click" usando o método `addEventListener`.
            - A função de callback associada ao evento é definida como uma arrow function (função de seta).
        - **Dentro da função de callback:**
            - `const playerName = document.getElementById('nameInput').value;`:
                - Obtém o elemento "nameInput" e acessa sua propriedade `value` para capturar o texto digitado pelo jogador.
                - Armazena o nome do jogador em uma constante `playerName`.
            - `this.scene.start('Cena01', { playerName: playerName });`:
                - Utiliza o método `start` do objeto `scene` (referenciando a cena atual) para iniciar a cena "Cena02".
                - Passa um objeto como argumento para a nova cena, contendo a propriedade `playerName` com o valor capturado anteriormente.
            - `document.getElementById('inputOverlay').style.display = 'none';`:
                - Após iniciar a cena "Cena02", novamente utiliza `getElementById` para obter o overlay.
                - Oculta o overlay definindo a propriedade `display` como "none".

**Resumo:**

A classe `Cena01` é responsável por:

1. Exibir o overlay de entrada inicial, que captura um nome que você dará entrada.
2. Configurar um evento de clique no botão "Iniciar" para:
    - Capturar o nome do jogador digitado.
    - Iniciar a cena "Cena01" e passar o nome do jogador como argumento.
    - Ocultar o overlay após a transição para a próxima cena.

### 3.3) Classe Cena02

No arquivo **cena-02.js**, vai esse código:

```
class Cena02 extends Phaser.Scene {
    constructor() {
        super('Cena02');
    }

    init(data) {
        this.playerName = data.playerName;
    }

    create() {
        this.text = this.add.text(-100, 700, `Olá ${this.playerName}, bão?`, { fill: '#333' });
    }

    update(){
        if(this.text.x < 400){
            this.text.x += 10;
        }
        if(this.text.y>300){
            this.text.y -=10;
        }
    }
}
```
#### Explicando...

**Classe Cena02**

- Classe Cena02: esta classe estende a classe `Phaser.Scene`, indicando que se trata de uma cena dentro do jogo Phaser.
- O construtor (`constructor`) da classe:
    - `super('Cena02');`: chama o construtor da classe pai (`Phaser.Scene`) e define o nome da cena como "Cena02".

**Método init(data):**

- Este método é chamado automaticamente pelo Phaser antes do método `create`.
- Ele recebe um objeto `data` como parâmetro, que possivelmente contém informações passadas de outra cena.
    - `this.playerName = data.playerName;`:
        - Acessa a propriedade `playerName` do objeto `data` e a armazena na propriedade interna `playerName` da classe.

**Método create():**

- Este método é chamado automaticamente pelo Phaser quando a cena é criada.
    - `this.text = this.add.text(-100, 700, `Olá ${this.playerName}, bão?`, { fill: '#333' });`:
        - Utiliza o método `add.text` da cena para criar um elemento de texto na tela.
        - Parâmetros do método `add.text`:
            - `-100`: coordenada X inicial do texto (fora da tela à esquerda).
            - `700`: coordenada Y inicial do texto (fora da tela na parte inferior).
            - ``Olá ${this.playerName}, bão?``: define o texto a ser exibido, usando template literal para incorporar o valor de `this.playerName`.
            - `{ fill: '#333' }`: define um objeto contendo as propriedades de estilo do texto em hexadecimal. As cores variam de #000000 (preto) até #ffffff (branco).
                - `fill: '#333'`: define a cor de preenchimento do texto como cinza escuro (#333) em hexadecimal.
        - A variável `this.text` armazena a referência ao elemento de texto criado para possível manipulação posterior.

**Método update():**

- Este método é chamado automaticamente pelo Phaser em cada frame de atualização do jogo.
    - `if(this.text.x < 400){`:
        - Verifica se a coordenada X do texto é menor que 400 (fora da tela à direita).
        - Se for verdade, o texto ainda não entrou na tela completamente.
    - `this.text.x += 10;`:
        - Incrementa a coordenada X do texto em 10 pixels, movendo-o da esquerda para a direita.
    - `if(this.text.y>300){`:
        - Verifica se a coordenada Y do texto é maior que 300 (fora da tela na parte superior).
        - Se for verdade, o texto ainda não atingiu sua posição final.
    - `this.text.y -=10;`:
        - Decrementa a coordenada Y do texto em 10 pixels, movendo-o de cima para baixo.

**Resumo:**

A classe `Cena02` é responsável por:

1. Armazenar o nome do jogador recebido na inicialização da cena.
2. Criar um elemento de texto na tela exibindo uma saudação personalizada ao jogador.
3. No loop de atualização do jogo:
    - Mover o texto horizontalmente da esquerda para a direita até a coordenada X de 400.
    - Mover o texto verticalmente de cima para a diagonal até a coordenada Y de 300.

### Arquivo Game.js

Criando um quarto arquivo chamado Game.js, temos:

```
window.onload = function() {
    const config = {
        type: Phaser.AUTO,
        parent: 'phaser-example',
        width: 800,
        height: 600,
        backgroundColor: "b9eaff",
        scene: [Cena01, Cena02]
    };

    const game = new Phaser.Game(config);
}

```

#### Explicando...

**Evento `window.onload`:**

- `window.onload = function() { ... };`: associa a função anônima ao evento `load` da janela do navegador.
    - Este evento é disparado quando a janela termina de carregar, garantindo que o código abaixo seja executado somente após o carregamento completo da página.

**Configuração do Jogo (`config`):**

- `const config = { ... };`: define um objeto `config` contendo as configurações do jogo Phaser.
    - `type: Phaser.AUTO`: define o tipo de renderizador como automático (escolherá WebGL ou Canvas).
    - `parent: 'phaser-example'`: define o elemento HTML que servirá como container do jogo (provavelmente um elemento com identificador "phaser-example").
    - `width: 800`: define a largura da janela do jogo em pixels (800).
    - `height: 600`: define a altura da janela do jogo em pixels (600).
    - `backgroundColor: "b9eaff"`: define a cor de fundo da janela do jogo como um código de cor hexagonal ("b9eaff").
    - `scene: [Cena01, Cena02]`: define um array contendo as classes das cenas que compõem o jogo.

**Instanciando o Jogo (`game`):**

- `const game = new Phaser.Game(config);`: cria uma nova instância do jogo Phaser passando a configuração definida anteriormente.

**Resumo:**

Este código define a configuração do jogo Phaser e cria uma nova instância do jogo utilizando as classes `Cena01` e `Cena02` como cenas.


## Conclusão

Com esse exemplo, você pode entender como as multi cenas são criadas e os valores de uma cena é passada para a outra.

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

## Exercício

### Descrição:

Você deve criar um jogo simples usando o exemplo acima onde você deve adicionar a 3ª cena e transmitir um dado. Você é livre para alterar o código da forma que quiser, desde que tenha 3 cenas, onde a primeira passa para a segunda, a segunda passa para a terceira. 

### Requisitos:

* Crie a 3ª cena usando Phaser.
* A cena 03 não pode ser idêntica à cena 02.
* Transmita um dado da segunda para a terceira cena.
* Exiba os dados da cena 02 e 03 na respectiva cena e no seu respectivo tempo, podendo ser apagada.
* Faça um código em grupo e apresente a solução no final da aula.

### Haverá uma votação da melhor solução entre os grupos da sala e haverá um prêmio que será pago assim que possível!
