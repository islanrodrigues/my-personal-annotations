### _Annotations_ (Anotações)
As anotações (conhecidas também como metadados) são um recurso que permite embutir informações complementares no código fonte.
Essas informações podem ser consumidas de três maneiras diferentes:
+ Informações para o compilador
+ Em tempo de execução (_runtime_)
+ Em tempo de compilação ou deploy (compile or deploy-time)

As anotações são precedidas de um `@`.
Exemplo: `@Override`

**Declarando uma _annotation_** -- para declarar uma anotação se uma o `@interface`. Dentro do corpo da anotação é possível declarar a assinatura dos métodos. Note que uma anotação é uma variação especial de uma interface. Para os métodos declarados também é possível definir um valor padrão através da palava chave `default`. 

Exemplo:
```java
@interface MyAnnotation {
    String author() default "Islan";
    int age();
    String nationality() default "brazilian";
}
````

**Fazendo uso da _annotation_** -- para o uso da anotação basta chamá-la acima do elemento ao qual você deseja anotar. Lembrando que ao definir atributos dentro da anotação, eles precisarão ser implementados no momento do uso, caso não possuam valor padrão.

Exemplo:
```java
@MyAnnotation(age = 23) //author and nationality already have a default value
public class Test {
}

// OR

@MyAnnotation(author= "Islan Rodrigues, age = 23, nationality = "canadian") //replacing author and nationality values
public class Test2 {
}
```

É importante frisar que as anotações **NÃO FAZEM NADA** a não ser agregar novas informações sobre os elementos das classes. Para que elas tenham algum efeito sobre o funcionamento do programa, alguém precisa recuperar essas anotações e fazer alguma coisa a respeito, pois sozinhas as anotações não fazem nada.

**Definindo até quando a anotação está disponível** -- umas das principais configurações de uma _annotation_ é até quando ela estará disponível para ser recuperada. Dependendo de qual que seja o seu uso, mais de um tipo de retenção pode ser necessário.
+ `SOURCE` : tipo de retenção que significa dizer que uma anotação só ficará disponível apenas no código fonte. Ou seja, no momento em que a classe é compilada, a anotação não é transferida para o `.class`. É geralmente utilizado para fins de documentação e para uso de ferramentas que fazem processamento direto de código fonte;
+ `CLASS` : tipo de retenção que significa dizer que uma anotação será mantida também nos arquivos `.class`, mas nõa serão carregadas pela JVM (_Java Virtual Machine_). Nesse caso elas ficam disponíveis até o carregamento da classe. É utilizada por ferramentas que fazem processamento do _bytecode_ da classe, podendo este ser feito de forma estática como uma etapa posterior a compilação ou no momento do carregamento das classes;
+ `RUNTIME` : tipo de retenção que significa dizer que uma anotação estará disponível para recuperação em tempo de execução. A JVM irá carregar a anotação em memória e torná-la accessível via `Reflection`. É utilizada geralmente por frameworks que precisam de acesso a anotação em tempo de execução.

Para definir qual o tipo de retenção a anotação terá, é preciso anotá-la com uma outra anotação, chamada `@Retention`. Essa anotação recebe como parâmetro um `enum` do tipo `RetentionPolicy`. Esse `enum` irá possuir os três tipos de retenção descritos anteriormente.
Caso nenhum tipo de retenção seja declarado, o padrão é o `SOURCE`.

Exemplo:
```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    
}
```

**Definindo onde a _annotation_ precisa ser usada** -- no momento da declaração de uma anotação, é possível informar onde deverá ser o seu uso, se é em uma classe, método, atributo etc. Isso se dá através do uso da anotação `@Target`. Essa anotação recebe como parâmetro um `enum` do tipo `ElementType`. O `ElementType` terá as seguintes opções: 
+ `TYPE` : qualquer definição de tipos como classes, interfaces e enumeradores;
+ `PACKAGE` : pacotes;
+ `CONSTRUCTOR` : construtores;
+ `FIELD` : atributos;
+ `METHOD` : métodos;
+ `PARAMETER` : parâmetros de métodos e construtores;
+ `LOCAL_VARIABLE` : variáveis locais;
+ `ANNOTATION_TYPE` : anotações.

Essa anotação pode receber um array com mais de um tipo onde faz sentido ser usada. Se nenhum tipo for definido, a anotação pode ser aplicada pra qualquer tipo de elemento. Mesmo não sendo obrigatório o uso do `@Target` é bastante importante para que não seja feito mal uso da anotação criada, evitando assim que seja usada em um local indevido.

Exemplo: 
```java
//with array of elements
@Target({ElementType.TYPE, ElementType.METHOD, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface EJB {
}

//without array of elements
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Target {
}
```

Em relação ao tipo `LOCAL_VARIABLE`, como as variáveis locais não são acessíveis por reflexão, esse tipo de anotação só faz sentido com retenção do tipo `SOURCE` ou `CLASS`. Em relação à anotação do tipo `PACKAGE`; utilizada para aplicar metainformações em uma pacote, para adicioná-la, é preciso criar um arquivo no pacote chamado `package-info.java` para definir a anotação.
