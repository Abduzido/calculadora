This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Calculadora React

Esse foi um projeto de estudo de implementação de uma calculadora modelada em React

### Vamos por partes explicar como essa calculadora foi construída.

Foram criados 3 componentes, sendo um principal **(Calculator.jsx)** que monta toda a aplicação e outro que controla o display do que é exibido na tela **(Display.jsx)** e por fim o componente que imprime os botoões na tela **(Button.jsx)**.

#### Componente Button

O componente Button tem dois parametros, um que recebe a 'label' do botão e o outro que recebe um parametro de uma função arrow, que será ativada ao ser clicada e que é validada para ser executada caso exista tanto as props 'label' quanto 'click' setadas.

#### Componente Display

Esse é o componente mais simples da aplicação, mas seu controle maior será por meio do componente principal da aplicação, pois ele é que exibirá tudo o que acontece na aplicação para o usuário.

#### Componente Calculator

Esse é o componente que controla todos os outros e é onde acontece toda a parte lógica também além de onde acontece o controle de estado da aplicação. A seguir descreverei como ele funciona exatamente para que a calculadora cumpra seu objetivo : realizar operações básicas matematicas.

##### Guardando estado
Nesse ponto, para manter estado da aplicação, foi criada uma constante **( initialState )** com um objeto que contém as propriedades essenciais para a calculadora:

**displayValue** : A propriedade que altera o que é exibido no componente **Display**

**ClearDisplay** : A propriedade que sinaliza se será necessário limpar a tela .

**Operation** : A propriedade que sinaliza que operação atualmente está sendo aplicada, digitada pelo usuário.

**values** : Quais os dois valores que estão na memória para realizar operação no momento neste array.

**current** : Qual o indice do array de values atual, ou seja, em qual número atualmente está a operação.


É inicializado o estado (state) clonando o objeto **initialState** já dentro do escopo do bloco do componente.

Foi utilizada a estratégia de fazer o bind dos métodos *clearMemory()* , *setOperation()* e *addDigit()*.

**clearMemory()** : Esse método serve para setar o estado inicial novamente, clonando a constante **initialState**.

**setOperation()** : Esse método contém alguns testes e operações que são executados dependendo do que já foi digitado pelo usuário e enviado por meio do método *addDigit()*

1.  É feito um teste para ver se o número que está sendo digitado agora é o primeiro ( se é o de indice zero), se for o estado será alterado, passando o valor da operação que veio por parâmetro, sinaliza que atualmente está sendo trabalhado o segundo número e que a tela precisará ser limpa.

2. Se a afirmação anterior for falsa outro bloco será executado, nesse bloco é criada uma constante para sinalizar se a operação passada é um sinal de igual (=), dessa forma, o valor dessa constante dependerá desse resultado.

3. A operação que foi recebida agora é armazenada em uma constante.

4. É criada uma constante clocnando os valores de estado dos valores númericos digitados.

5. A operação é executada e o valor é armazenado no primeiro espaço para o **valor 1**(values[0]). Se qualquer problema ocorrer, será guardado novamente os dados do **valor 1** no espaço de **valor 1**.

6. Finalmente o estado é armazenado sendo que o valor exibido no display é sempre o resultado armazenado em **valor 1** (values[0]). Se a operação tiver valor de igual(=), então, o valor de *operation* será null senão, será o valor passado como parametro no método e esse valor também será usado no teste de qual numero atual esta sendo trabalhado, se for verdadeiro, será o **valor 1**(values[0]) senão o **valor 2**(values[1]). *ClearDisplay* também dependera de um teste com equals, mas dessa vez testando o seu valor avesso e por fim os valores *(values)* também serão atualizados.

**ddDigit()** : Este método recebe tudo o que é digitado nos botões da aplicação. Nela também serão feitos alguns testes antes de também mudar algum estado:

1. Se o valor digitado tiver ponto (.) e o valor de *displayValue* já contiver ponto também, então nada será computado dessa operação.

2. Uma constante vai sinalizar se será preciso limpar a tela ou não por meio de um teste que verifica se o valor de displayValue é zero ou se ClearDisplay já é true. Este teste serve também para que seja digitado zeros desnecessários na calculadora.

3. É feito um teste : Se *clearDisplay* for verdadeiro então o valor atual será vazio senão será o valor que está sendo exibido atualmente na tela.
4. O valor de displayValue será o valor do valor atual somado ao valor que veio como parâmetro.
5. O estado é então atualizado: *DisplayValue* (valor atual) é atualizado e *clearDisplay* é sinalizado para falso. 
6. E o último teste executará a operacão de atualizar o estado dos valores (values) caso o valor digitado não seja um ponto e atualizará conforme o número atual que estiver sendo trabalhado.