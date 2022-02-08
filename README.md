
# [Passo-a-Passo] Implementação de Redux-React em um projeto
### Um guia bem humorado e conciso sobre a configuração dessa ferramenta maravilhosa para suas aplicações.

#### Puxando Papo 🗨️

<div align="justify">
  
Olá pessoa desenvolvedora, que assim como eu esta passando por um sufoco na hora de entender ou manusear o Redux dentro do React! te convido para uma leitura produzida intencionando a extinção dessas dúvidas, como sempre, ao final do texto estarão disponibilizadas as referências para você se aprofundar ainda mais, ***vamo nessa* ?**
#### Começando ▶️


Para estarmos na mesma página em relação a conceito, preciso que você já tenha uma noçãozinha do que é o redux, e uma boa noção do que é o React, tendo isso como norte, sua experiência com esse texto será a melhor possivel!


*Esse texto é formado como um complemento a lista de "redux-react-checks" disponibilizada pela Trybe.*

#### O que diabos é Redux  🤔
*Redux á uma biblioteca de centralização e armazenamento de estados para Javascript criada por Dan Abramov como uma implementação do Flux*

**Tá Gero, mas o que isso muda na minha vida?** Você deve estar me perguntando.

  

Bom...

Todo mundo que já mexeu o mínimo com react sabe da dor de cabeça que é comunicar estados e propriedades entre componentes parentes, sempre que quer jogar uma informação para um filho do filho do filho, varios componentes acabam acessando informação desnessesaria, se isso já é uma dor de cabeça em aplicações pequenas imagina em uma aplicação gigantesca, como não seria terrivel passar esses dados!

  

É ai que entra o nosso querido 💜**Redux**💜

Ele centraliza todos seus estados compartilhados em uma única Banca, dado que um componente precisa desses dados ele só precisa acessar essa página ao invés de cair em um complexo sistema de ***prop drilling*** (escavar propriedades) como citamos antes.

**A Gero, se essa ferramenta é tão simples, então por qual motivo todo mundo se atrapalha quando está estudando redux ?** você me perguntaria não é? eu sei, eu leio a sua mente!

  

Toda essa facilidade empenhada pela ferramenta requer um preço mínimo, uma configuração que deve ser executada uma vez durante a aplicação! É aí que as pessoas ficam com medo dessa caminhada! Mas, não se preocupe, eu conheço um atalho!


####  Instalando  🔧

Vamos começar com o mais óbvio, precisamos de uma aplicação <strong> React </strong>!

* Execute o seguinte código em seu terminal para iniciar:<br>

<code>npx create-react-app ???</code> <br><br>

* os "???" acima devem ser substituídos pelo nome que você dará ao seu projeto, seu console ira iniciar a montagem da aplicação, então simplemeste aguarde a mensagem de **"Happy Hacking"** que seu terminal vai te desejar quando a intalação estiver completa, enquanto isso ocorre, aproveita pra se conectar comigo no linkedin [Clicando Aqui!](https://www.linkedin.com/in/gerson-henrique/) Estou ansioso para gente bater um papo!

* Digite um *"ls" (List)* em seu console para ver a pasta que você acabou de criar, e com o comando *"cd **???**"* *(Change Directory)* vamos nos direcionar para dentro da pasta.

* Uma vez na pasta use o seguinte comando

npm install --save redux react-redux redux-devtools-extension

* Esse comando instalará as dependências que trabalharemos!

Tendo tudo isso em mãos, vamos para a parte divertida! Hora de ***codar***!

* No terminal digite o seguinte comando para abrir o vs code: <br>

<code> code .</code> <br><br>

  #### Configuração Padrão das Pastas 📁
  Toda a configuração do redux pode ser feita praticamente em um arquivo, mas como temos amor a nossas aplicações, organizaremos tudo de um jeito lógico e simples.

Dentro da nossa src criaremos uma pasta chamada **Store**, essa pagina vai ter três filhos. Um arquivo chamado index.js e duas pastas, uma com o nome de **Actions** e **Reducer**, ambas também com um arquivo indexis.js em seu interior.

  

Essa é a nossa estrutura mínima para trabalhar com a configuração, agora abstrairemos um pouco nosso projeto.

  #### Parte um :  Abstração 💭
  
Muita gente acha a parte de abstração desnecessária, mas entendam galera! **definir os detalhes do seu projeto ao invés de só ir jogando código na tela, é o que vai te fazer evoluir como programador**, além de prever problemas e evitar o código desnecessário. Não é atoa que os nossos dois primeiros tópicos da nossa checklist são associados a abstração!

1. Quais Informações terão seus dados alterados?

2. Quais ações da minha aplicação alterarão os dados?

Essas duas perguntas nos livram de toneladas de dor de cabeça!

  

a primeira nos responde quais States devemos criar, e a segunda, quais Actions devemos nos preocupar. Ainda muito Abstrato para você? Começaremos a dar um pouco de forma para nosso problema!

  

Imagina que temos uma aplicação react super simples! Ela tem duas páginas, a primeira são dois inputs (para nome e idade) e um botão (para submeter esses dados), assim que o botão é clicado, vamos para outra página que simplesmente diz “Olá NOME_DO_USUARIO me contaram que você tem IDADE_DO_USUARIO anos!”

  
Parede julgar minha falta de criatividade e foque na aplicação!

  

  

Responderemos às perguntas chamadas anteriormente!

  

1. Quais Informações terão seus dados alterados?

  

Parando pra analisar, as únicas informações que precisaremos para a aplicação funcionar são {nomeDoUsuario} e {idadeDoUsuario} que vamos simplesmente se referir como Nome e Idade de agora em diante. Logo temos os nossos States definidos

  

{

nome: ''

idade: 0

}

Agora, basta saber a resposta para nossa segunda pergunta

2. Quais ações da minha aplicação alterarão os dados?

Novamente, analisando nossa aplicação vemos que a única ação realizada é enviar os dados quando clicamos no botão! Ou seja

Nossa action também está definida! e podemos chama-la GET_DATA (letras maiúsculas nessas variáveis vem de convenção da comunidade).

  #### Parte dois :  Configuração ⚙️

Essa parte é fundamental para entender como o redux funciona! Então dobre a atenção e revisite esse tópico quantas vezes forem necessárias.

  

Vamos começar na nossa querida página

**reducer/indexs.js**

  

Dentro do redux, a função do **reducer** é de sobrescrever o valor dos states, com a lógica que varia dependendo de um tipo (Type) que for passado para ele pelas actions.

  

Aqui, a primeira coisa que precisamos definir são os states da aplicação, como foi combinado acima usaremos nome e idade

```jsx

const ESTADO_INICIAL = {

nome: ""

idade: 0

}

```

  
  
  

Agora precisamos chamar a nossa função reducer e atribuir-lhe um switch que sera responsável por definir o "tipo" da action, nosso switch por enquanto tratará somente o case default (Não se preocupe com essa parte, nós retornaremos aqui mais adiante.).

```jsx

const myReducer =(state = ESTADO_INICIAL, action) => {

switch(action.type){

default:

return state

}

}

```

e por fim precisamos somente concatenar os reducers criados.nesse exemplo, criamos apenas um reducer, mas vamos passar pelo concatenador somente para fins didáticos.

  

const rootReducer = combineReducer ({myReducer})

  

nossa função **combineReducer** deve ser importada do Redux, ela tem o objetivo de unir os reducers criados em um único elemento que atuara como um link para todos os outros, caso fossemos combinar mais de um usaríamos:

  

```jsx

const reducerCombinado = combineReducer ({

reducer1,

reducer2,

})

```

  

Mas, deixaremos de lado esse arquivo por alguns instantes, temos mais coisas pra definir antes de concluir nosso projeto.

no arquivo **store/index.js** (o que fica na camada superior) criaremos a nossa banca de informações, nosso galpão, nossa store!

  

A **Store** como já foi dito, é nossa fonte única da verdade, é aqui que tudo estará disponível para consulta, e por incrível que pareça, é uma das partes mais simples de se configurar!

  

Importaremos a **creteStore** do react e o **rootReducer** que criamos em reducer/index.js para cá e usando essa função para criar nossa banca

  

```jsx

import { createStore } from 'react'

import {composeWithDevTools } from 'redux-devtools-extension'

import rootReducer from './reducer/index'

const store = createStore(rootReduce, composeWithDevTools );

export default store;

```

A store se liga a um redutor e no nosso caso, também ligamos ela ao **composeWithDevTools**, ferramenta que parece com o ReactDevTools. tem um link sobre sua ultilização na área de referencias.

  

hora de criar nossas **actions** . Seguimos até **actions/index.js** aqui vamos criar e exportar as ações que alterarão os estados da aplicação por convenção criamos uma variável com o mesmo nome da action para evitar erros futuros e montamos a nossas funções de ação, uma função de ação recebe um **payload** (carga de dados) que sera passada mais a frente e retornara um objeto com essa carga e um **Type** (tipo) que nós guiara na hora de finalizar o **reducer**.

```jsx

export const SET_INFO = 'SET_INFO'

export const setInfo = (payload) => (

{

type: SET_INFO

}

);

```

Estamos dizendo que o tipo dessa ação se chama Set_Info "aplicar informação” que será recuperada ao clicar no botão do nosso pequeno formulário, agora que nossa store está pronta e já criamos nossas actions basta terminar nosso **reducer/index.js** de volta para essa página, importaremos nossa action! e criar um case especifico para isso no nosso switch.

```jsx

import { SET_INFO } from '../actions/index'

const myReducer =(state = ESTADO_INICIAL, action) => {

switch(action.type){

case SET_INFO:

return {...state,

nome: action.payload.nome

idade: action.payload.idade }

default:

return state;

}

}

```

  

Dentro de actions definimos apenas uma ação, e demos-lhe o tipo SET_INFO, agora dentro de Reducer dizemos que caso o tipo da ação tratada for SET_INFO, nos retornaremos o nosso estado anterior (...state) e passar para a variável os valores recuperados do payload.

  

Agora, fora da nossa pasta store, dentro de nossa SRC temos um último **index.js**. Este, responsável pela renderização do App.js e é nele que passaremos nossa última configuração!

Nele importaremos o **Provider** componente que dara a possibilidade do que ela englobar de acessar os states de uma store passada como propriedade

seu arquivo deve ter algo nesse formato no final

```jsx

import React from 'react';

import { Provider } from 'react-redux';

import ReactDOM from 'react-dom';

import store from './redux/store/store';

import App from './App';

import './index.css';ReactDOM.render(

<React.StrictMode>

<Provider store={ store }>

<App />

</Provider>

</React.StrictMode>,

document.getElementById('root'),

);

```


 
  
  #### Parte três: Conexão 🪡
  
  
e lá se vai a parte complexa do redux! Agora basta aproveitar da ferramenta dentro da nossa aplicação, a última coisa que falta é você entender o conceito de **connect**. Essa função tem duas passagens de parâmetros, na primeira podemos definir se vamos usar as funções mapStateToProps e mapDispatchToProps e na segunda passamos o componente que estamos exportando, isso conectara esse componente com a loja, seja pra atualizar states ou ler os states

```jsx

export default connect(mapStateToProps, mapDispatchToProps)(Component);

```

  

mapStateToProps é a função que vamos usar para transformar os states que recebemos pelo connect em propriedades para usarmos, ela é atribuída *Nos componentes que irão ler o estado* tendo em mente a nossa suposta aplicação que montamos lá em cima, usaremos o **mapStateToProps** na página que exibira a **mensagem** "Olá NOME_DO_USUARIO me contaram que você tem IDADE_DO_USUARIO anos!"

```jsx

const mapStateToProps = state => ({

info: state.rootReducer.payload});

```

  

e pronto, agora podemos acessar normalmente o payload (que contem nome e idade) com nossa prop **info** (lembre de usar this.props na desconstrução para acessar essa propriedade!)

  

```jsx

<h1> "Olá {this.pros.info.nome} me contaram que você tem {this.pros.info.idade} anos!" <h1>

```

E por fim **mapDispatchToProps** . essa função é a grande responsável por alterar os dados na nossa store, e deve ser aplicada no componente que passará os states, na nossa aplicação, seria a primeira página com os dois inputs, você capturar esses valores do input usando **state locais**! lembre-se, a chave do uso do redux é passar informações entre parentes, para rodar uma informação dentro de um componente apenas devemos continuar usando o nosso querido *this.setState.*

```jsx

const mapDispatchtoProps = (dispatch) => ({

payload: (value) => dispatch(setInfo(value))

});

  

export default connect(null, mapDispatchtoProps)(component);

```

  

Onde em nosso onclick teríamos

  

```jsx

onClick={ (event) => this.setState({ () => payload(textValue) }) }

```

aqui, payload se refere a callback que acabamos de mapear com a nossa mapDispatchtoProps e textValue seria o valor dos inputs,

  

e **PRONTO!** enfim está tudo configurado e pronto para ser usado!
  
   
   #### Despedida 💌
  
  Queria agradecer a você pessoa desenvolvedora que me acompanhou até aqui, obrigado por tirar esses minutinhos para investir em você, esse tutorial está longe de ser perfeito, mas se eu tiver conseguido  te ajudar a clarear minimamente um conceito que você não tinha pegado, já me valeu completamente a pena esse trabalho todo  <br><br>
  
  Se for do seu interesse, gostaria que você me desse aquela estrelinha nesse repositorio e me seguisse aqui no hub, vou procurar estar sempre ativo e trazendo mais materiais conforme eu for aprendendo!<br><br>
  
 siga em frente. nunca pare de aprender!<br><br>

   #### Referencias 🔍

https://qastack.com.br/programming/38202572/understanding-react-redux-and-mapstatetoprops
https://codesandbox.io/s/github/reduxjs/redux/tree/master/examples/shopping-cart?from-embed=&file=/src/reducers/products.js
https://redux.js.org/introduction/examples
 https://react-redux.js.org/
https://redux.js.org/usage/structuring-reducers/using-combinereducers
https://www.alura.com.br/artigos/prop-drilling-no-react-js?gclid=CjwKCAiAo4OQBhBBEiwA5KWu_-KvRW3oquKMnAju8rQMqUKmE3Gookhji0POKqHt6-EAipoNdz6EchoCP1wQAvD_BwE
https://www.treinaweb.com.br/blog/o-que-e-redux

  
  
  
  
</div>

