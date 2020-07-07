# Clean Code em JavaScript

## Panorama do Curso:
- Código Limpo em JavaScript: princípios gerais (30 minutos)
    - Apresentação dos Líderes;
    - Justificativa ;
    - Estudo de Caso;
    - Funções;
    - Objetos e Classes;
    - Atividade de correção de código;
- Programação Funcional (40 minutos)
    - Introdução a Programação funcional;
    - Funções puras;
    - Object.assign e o Operador Spread;
    - Map e Foreach;
    - Reduzindo e filtrando arrays;
    - Atividade de compreensão de conceitos;
- Módulos em JavaScript (20 minutos):
    - Justificativa dos módulos;
    - Padrão de módulos;
    - Gerenciador de Pacotes;
    - Tree-shaking com Webpack;
    - Atividade de replicação de tutorial;
- Padrões de Projetos (50 minutos):
    - Introdução
    - Princípio Single-responsibility;
    - Princípio Aberto/Fechado;
    - Princípio de segregação de interface;
    - Princípio de inversão de dependência;
    - Princípio Singleton;
    - Princípio Observer;
    - Princípio Strategy;
    - Atividade de compreensão de conceitos;
- Lidando com Erros (20 minutos):
    - Práticas utilizadas;
    - Estratégias para lidar com erros;
    - Logging;
    - Distribuição de PDF com Resumo e do repositório com os exemplos usados no curso;
    - Atividade de correção de código;


**Guia de Instalação do Node:** https://nodejs.org/pt-br/download/package-manager/#macos


# Código Limpo em JavaScript: princípios gerais:
----------
## Nomeando Variáveis:
1. Use nomes que possuam significado.

Imagine que você está escrevendo um sistema para uma empresa de entregas e precisa guardar o tempo de saída e chegada na variável. Muitos desenvolvedores escrevem variáveis como o exemplo abaixo:


    //Tempo de Saida
    var time1 = new Date(2020, 1, 18);
    
    //Tempo de Chegada
    var time2 = new Date(200, 1, 29);

Contudo, quando o seu código possui muitos comentários, significa que talvez ele possa explicar a si mesmo. Assim, nomear as variáveis “time1” e “time2” com “tempoDeSaída” e “tempoDeChegada” torna o script mais legível. A solução aqui seria refatorar o código. 

2. Além disso, preocupar-se com o noma de variáveis ajuda o programador a rapidamente encontrar arquivos e linhas de códigos. Assim, ter nomes de variáveis que são memoráveis nos ajuda a nos movimentarmos dentro de nosso projeto. Vejamos um exemplo:

Neste exemplo temos um componente que imita as funcionalidade de uma aplicação de uma página


    add (customerId, itemId){
      this.customerService.get(customerId).then(customer -> {
      });
    }


3. Neste exemplo,  temos nomes curtos para variáveis. Entretanto, mesmo que pareça contra intuitivo, um dica importante é favorecer nomes descritivos a nomes curtos.


    let person = {
      fName: 'John'
      lName: 'Smith'
      fatherName: 'Jake'
    }
    
    console.log('First name: ' + person.firstName);
    console.log('Father name: ', person.fatherName);

*Observação: Identificar o problema acima é fácil. Lembre-se de que a maioria os exemplo usados durante o curso serão assim. Porém, não devemos subestimar a importância dessas práticas uma vez que elas mostrarão suas utilidades em projetos maiores com muitas linha de código*


4. O próximo ponto é mais comum de ser visto no contexto de classes e objetos. Muitos programadores tendem a repetir o contexto para cada variável, propriedade e field name. Digamos que estamos exportanto uma classe Student:


    rt class Student{
      constructor(studentAcademicId, studentFirstName, studentLastName, studentUniversity){
        this.studentAcademicId = studentAcademicId;
        this.studentFirstName = studentFirstName;
        this.studentLastName = studentLastname;
        this.studentUniversity = studentUniversity;
      }
    }

Por qual razão colocar o prefixo “student”? Ora, não já estamos na classe Student? Talvez fizesse sentido caso tivéssemos que adicionar certa ID para cada student. O recomendado é escrever esta classe da seguinte forma:


    export class Student{
      constructor(acadeicId, firstName, lastName, university) {
        this.academicId = academicId;
        this.firstName = firstName;
        this.lastName = lastName;
        this.university = university;
      }
    }


5. Por último, mas não menos importante: seja consistente. Se você inicia um projeto com certa convenção de nomes para suas variáveis, mantenha-se nela até o fim. Estas convenções fazem o código ficar consistente. Isso pode ser visto em projetos de código livre. Contribuir para estes projetos muitas vezes requer passar por rígidas regras.


    export class Order{
      get(){
      
      }
      expor class Customer{
        getCustomer(){
        }
        get_customer(){
        }
    
        get(){
        }
    } 


## Escopo léxico e “let”

O escopo do JavaScript sempre incomodou muitos desenvolvedores, inclusive eu, assim como a nova keyword “let”. Nesta seção, vamos aprender como que o JavaScript procura por variável e também qual é a diferença entre escopo de funções e escopo lexical. As perguntas que tentaremos responder são:


    - Como o JavaScript  busca por variáveis?
    - Qual a diferença entre escopo de funções e escopos de blocos?
    - O que mudou no ES6 de var para let?

Antes de tudo, é preciso entender que estamos tratando de duas questões diferentes. A primeira é a de onde o JavaScript irá procurar pela variável e a segunda é onde a minha variável está definida. 


    function f1(){
      var a = 1;
      function f2(){
        var b = 2;
        function f3(){
          var c = 3;
          console.log(c);
          d = 23;
        }
      }
    }

O JavaScript busca as suas variáveis no escopo em que é chamada e em todos os escopos inclusos. Ou seja, a linguagem procura primeiro na sua função em todas as funções na qual ela está inclusa. No caso da variável “d” a linguagem apenas apresentará erro caso o usuário esteja com o strict mode ativado. O que sempre evita problemas de digitalização e possíveis erros.

Como já mencionado acima, não existe apenas o escopo de funções na linguagem. Introduzido no ES6, a palavra reservada “let” permite o programador criar escopos de bloco. Isso tem causado alguns equivoco por parte da comunidade. Por exemplo, o que acontece no exemplo abaixo?


    //var i;
    for (var i = -; i < 10; i++) {
      console.log(i);
    }
    console.log(i);


    var test = true;
    if(test){
      let a = 1;
    }
    console.log(a);

Assim, podemos concluir que “var” define variáveis no escopo da função e “let” que as define no escopo do bloco. O que nos faz pensar um pouco sobre o uso de var,  o qual deve ser usado em poucos casos.


## Funções

Agora vamos aprender a escrever funções mais limpas e também veremos como trabalhar com argumentos e valores de retorno, evitando erros comum.


1. As funções devem fazer um ação e uma ação apenas. Este é um dos princípios mais famosos na engenharia de software: o principio da responsabilidade única. Vamos ver um exemplo:


    var produtos = [
      {
        nome: 'CPU',
        preco: 228.99,
        comprado: true
      },
      {
        nome: 'RAM',
        preco: 140.99,
        comprado: false
      },
      {
        nome: 'Pen Drive',
        preco: 70.00,
        comprado: true
      },
      {
        nome: 'Teclado',
        preco: 22.50,
        comprado: false
      }
    ];
    
    function preparaDados(itens){
      for(let i = 0; i , itens.length; i++){
        itens[i].id = i + 1;
      }
      let itensComprados = [];
      for(let i = 0; i < itensComprardos.length; i++){
        if(itens[i].comprado){
          itensComprados.push(itens[i]);
        }
      }
      let custoTotal = 0;
      for(let i = 0; i < itensComprardos.length; i++){
        custoTotal += itensComprados[i].preco;
      }
      console.log('Custo Total: ${custoTotal}');
    } 
    
    preparaDados(produtos);

Obviamente a função preparaDados() está fazendo muito mais do que ela deveria fazer. Vamos dividi-la:


    preparaDados(itens){
      addIds(itens);
      let itensComprados = getItensComprados(itens);
      let custoTotal = calculaCustoTotal(itensComprados);
      console.log("Custo total: ${custoTotal}");
    }
    
    function addIds(itens){
      for(let i = 0; i , itens.length; i++){
        itens[i].id = i + 1;
      }
    }
    
    function getItensComprados(itens){
        let itensComprados = [];
      for(let i = 0; i < itensComprardos.length; i++){
        if(itens[i].comprado){
          itensComprados.push(itens[i]);
        }
      } return itensComprados;
    }
    
    function calculaCustoTotal(itens){
      let custoTotal = 0;
      for(let i = 0; i < itensComprardos.length; i++){
        custoTotal += itens[i].preco;
    }

*Regra de Ouro: tenha no máximo uma função com três argumentos. Funções com muitos argumentos tendem, em geral, a não seguir o princípio de responsabilidade única.*

Caso você tenha uma função com muitos argumentos, talvez seja o caso de que nem sempre todos os argumentos serão sempre utilizados. Para tanto, podemos utilizar o objeto config.


    function draw(element, config){
      element.style.width = config.width;
      element.style.height = config.height;
      element.style.backgroundColor = config.backgroundColor;
      element.style.color= config.color;
      return element;
    }
    
    draw(document.getElementById("logoHeader"),{
      width: 30,
      height: 40,
    })

Outra prática comum é colocar flags nos argumentos de uma função.  Vejamos o exemplo abaixo:


    let toDos = [
      {
        task: 'Comprar ovos'
        done: false
      },
    
      {
        task: 'Enviar pull request'
        done: true
      },
    
      {
        task: 'Me inscrever na eJIM'
        done: false
      }
    ];

Suponha que eu queira visualizar minha lista de afazeres. Para isso, eu posso escrever a seguinte função:


    //filter = 0 imprime todos os toDos
    //filter = 1 imprime toDos completos
    //filter = 2 imprime toDos pendentes
    function printToDos(toDos, filter){
      if(filter == 0){
        for(let todo of toDos){
          console.log(todo.task);
        }
      } else if (filter == 1) {
          for(let todo of toDos){
            if(todo.done){
              console.log(todo, task);
            }
          }
      } else {
          for(let todo of toDos) {
            if(!todo.done) {
              console.log(todo.task);
            }
          }
      }
    }

Esta solução além de quebrar princípios apresentados anteriormente, é suscetível a erros como o de definir a flag incorreta, por não possuir qualquer tipo de significado real. Um possível solução é dividir as funções (ex:  printAllToDos(), printCompletedToDos(), printPedingToDos() ).

Callback são coisas do passado. Com ferramentas como Babel no Typescript, não existe mais qualquer necessidade de utilizar callbacks. Até mesmo as novas ferramentas do ES7, como async e wait já resolvem a maioria dos problemas. No exemplo abaixo, imagina que estamos desenvolvendo uma aplicação IOT. Nela estamos recebendo dados três diferentes sensores. Estas funções recebem um callback como um argumento. 


    function getSensorAData(cb){
      setTimeout(() => {
        cb({
          min: 8,
          max: 118
        });
      }, 2000);
    }
    
    function getSensorBData(cb){
      setTimeout(() => {
        cb({
          temp: 78,
          value: 26
        });
      }, 500);
    }
    
    function getSensorCData(cb){
      setTimeout(() => {
        cb({
          min: 14,
          max: 92,
          temp: 64,
          value: 12
        });
      }, 500);
    }

Se precisamos com combinar os dados de todos os três sensores apenas depois que recebemos os dados dos três sensores, podemos pensar em uma solução como a da função abaixo:


    function combineSensorData() {
        getSensorAData((sensorAData) => {
          getSensorBData(sensorBData => { 
           getSensorCData(sensorCData => {
            //Aqui eu posso fazer qualquer 
            //coisa com os dados dos sensores
            });
          });
        });
    }

Note que estrutura é muito complexa. Alguns chamam esta forma de escrever código de a “pirâmide do inferno”. Uma forma muito mais legível de escrever este código é da forma abaixo utilizando promises:


    function getSensorAData(cb){
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve({
            min: 8,
            max: 118
          });
        }, 2000);
      }
    }
    function getSensorBData(cb){
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve({
            temp: 78,
            value: 26
          });
        }, 500);
      }
    }
    function getSensorCData(cb){
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve({
            min: 14,
            max: 92,
            temp: 64,
            value: 12
          });
        }, 500);
      }
    }
    
    function combineSensorData(){
      Promise.all(getSensorAData(), getSensorBData(), getSensorCDAta()).then(results => {
        let sensorAData = results[0];
        let sensorBData = results[1];
        let sensorCData = results[2];
    }

Os códigos fazem exatamente a mesma coisa. Porém, utilizando promises a função combineSensorData pode ser escrita de forma bem mais robusta. Usando Promise.all, a função recebe um vetor de promises e retorna uma única promise que irá ser cumprida após todas as promessas que fizemos serem cumpridas. Em outras palavras, recemos um vetor de resultados na ordem em que provemos e não na ordem de execução. 

Quando você quer ter argumentos padrões para valores escalares, você apenas precisa usar default, correto? E se eu quiser configurar propriedades padrões para o meu objeto? Você pode pensar em utilizar um  booleano para solucionar este problema, como no exemplo abaixo:


    function draw(element, config) {
      config.width = config.width || 200;
      config.height = config.width || 200;
      config.margin = config.width || 28;
      config.padding = config.width || 14;
      console.log(config);
    } 
    draw(null, {margin: 100, padding: 50});

O que acontece se executarmos esta função? Na primeira execução o resultado saiu como esperamos, mas caso troquemos margin e padding para 0 o resultado será o resultado padrão:

![](https://paper-attachments.dropbox.com/s_4C4C65252A232650106355FBD326B1B4BC45029001A648FA710FB25EDEFE3881_1592592818325_Screen+Shot+2020-06-19+at+15.53.17.png)


Além de ser mais legível, a criação de um objeto defaults soluciona este problema. Para tanto, usaremos o operador spread “…”:


    function draw(element, config) {
      let defaults = {
        width: 200,
        height: 200, 
        margin: 28,
        padding: 14,
    };
      config = {
        ...defaults,
        ...config    //Config precisa vir depois
      }
      console.log(config);
    } 
    draw(null, {margin: 0, padding: 0});


## Sobre o this

Agora vamos tentar entender o *this* faz e como evitar bugs relacionados ao *this*. Antes de tudo é preciso deixar claro que a definição de uma função não afeta o valor de this. O que afeta o valor de this é o local onde chamados this.


    var a = 92;
    
    var obj = {
      a: 1,
      b: 2,
      c: 3
    }
    function test(){
      console.log(this.a);
    }
    test();
    obj.test = test;
    obj.test();

No código acima, estamos chamando as funções de dois locais diferentes. Do escopo local e do objeto. Veja só o resultado:


![](https://paper-attachments.dropbox.com/s_4C4C65252A232650106355FBD326B1B4BC45029001A648FA710FB25EDEFE3881_1592593617808_Screen+Shot+2020-06-19+at+16.06.41.png)


Um está usando a variável e a segunda a propriedade do objeto. Agora se no lugar de var, declararmos a variável a com let, teremos um resultado diferente:


![](https://paper-attachments.dropbox.com/s_4C4C65252A232650106355FBD326B1B4BC45029001A648FA710FB25EDEFE3881_1592593753638_Screen+Shot+2020-06-19+at+16.08.58.png)


Isso ocorre, pois as variáveis declaradas com *let* não fazem parte do objeto global.  


## Objetos e Classes

Como visto no último tópico, JavaScript está cheio de objetos. Vamos agora estudar algumas formas de escrever as funções de maneira mais robusta.

Não é raro termos campos dos nossos objetos que deveriam apenas ser lidos. Para fazer isso de maneira explícita vamos usar descritores de propiedades:


    "use strict"
    
    var person = {
      firstName: 'Joao'
      lasName: 'Araujo'
    };
    Object.defineProperty(person, 'age', {
      value: 28,
      writable: false,
      enumerable: true,
      configurable: false
    });
    console.log(person);
    person.age = 44;
    console.log(person);

O código acima não funciona, pois estamos tentando modificar o valor de um objeto que foi feito apenas para ser lido. O que faz isto acontecer são as linhas 1, 10 e 11 do programa.

Outro problema que alguns desenvolvedores encontram no JavaScript é o uso de herança. Para isso, vamos tentar entender com a classe do exemplo abaixo:


    function Pet(name){
      this.name = name;
    }
    Pet.prototype.eat = function() {
      console.log('${this.name} esta comendo');
    }
    function Dog(name, breed){
      Pet.call(this, name);
      this.breed = breed;
    }
    Dog.prototype = Object.create(Pet.prototype);
    Dog.prototype.play = function(){
      console.log('${this.name} esta brincando');
    }
    var toby = new Dog('Toby', 'Vira Lara')
    toby.eat();
    toby.play();
    console.log(toby);

Se executarmos este programa, veremos no console que max é um Pet e não um Dog. Foram quase vinte linhas de código para conectar a classe Dog e Pet usando prototypal. Vamos tentar melhorar isso:


    class Pet{
      constructor(name){
        this.name = name;
      }
      eat(){
        console.log('${this.name} esta comendo');
      }
    }
    class Dog extends Pet{
      constructor(name, breed){
        super(name);  //Isso chama o construtor da classe base
        this.breed = breed;
      }
      play(){
        console.log('${this.name} esta brincando');
      }
    }
    let toby = new Dog('Toby', 'Vira lata');
    toby.eat();
    toby.play();
    console.log(toby);
![](https://paper-attachments.dropbox.com/s_4C4C65252A232650106355FBD326B1B4BC45029001A648FA710FB25EDEFE3881_1592595094535_Screen+Shot+2020-06-19+at+16.31.24.png)


Mesmo que o número de linhas de código aqui seja maior, o código se torna muito mais legível, além do Node ser capaz de identificar as Toby pertencente da classe Dog e não Pet, o que é mais correto.

## Usando linter

Existem muitos benefícios a usar linter. O uso de linter nos ajuda a encontrar erros em potencial antes que eles aconteçam. O que significa que podemos dedicar mais tempo sendo produtivos e menos tempo procurando erros. 

Linters podem ser encontrados de diversas formas e podem ser importados de diversas bibliotecas: JSLint, JSCS, JSHint e ESLint. Neste tutorial usaremos ESLint. Para instalar bastar usar o npm:


    nom install eslint --save--dev

*Usamos —save—dev, pois eslint é uma ferramenta usada somente pelo desenvolvedor e não deve ir para o deploy.* 

Após a instalação vamos copie o código abaixo:


    var todos = [
      {
        id: 1,
        task: "Comprar queijo",
        completed: true
      },
      {
        id: 2,
        task: "Reuniao do Lab",
        completed: false
      },  
      {
        id:
        task: "Fazer exercicios",
        completed: false
      }
    ];
    console.log("Todos os toDos: ");
    console.log(toDos);
    
    var completed = [];
    for(let toDo of toDos){
      if(todo.competed){
        completed.push(todo);
      }
    }


![Configuração do ESLint](https://paper-attachments.dropbox.com/s_4C4C65252A232650106355FBD326B1B4BC45029001A648FA710FB25EDEFE3881_1592596550107_Screen+Shot+2020-06-19+at+16.55.22.png)


Depois de configurar o ESLint, um arquivo será gerado com todas as configurações. Para mais informações você pode ler a documentação [aqui](https://eslint.org/). Tudo pode ser muito restrito, mas não necessariamente pode ser aqui. Para fins didádicos usaremos as configurações abaixo:

Assim, o código que escrevemos apresentará os seguintes erros:


![](https://paper-attachments.dropbox.com/s_4C4C65252A232650106355FBD326B1B4BC45029001A648FA710FB25EDEFE3881_1592596770129_Screen+Shot+2020-06-19+at+16.58.53.png)








