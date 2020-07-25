### _Annotations_ (Anotações)
As anotações (conhecidas também como metadados) são um recurso que permite embutir informações complementares no código fonte.
Essas informações podem ser consumidas de três maneiras diferentes:
+ Informações para o compilador
+ Em tempo de execução (_runtime_)
+ Em tempo de compilação ou deploy (compile or deploy-time)

As anotações são precedidas de um `@`.
Exemplo: `@Override`

**Declarando uma _annotation_** -- para declarar uma anotação se usa o `@interface`. Dentro do corpo da anotação é possível declarar a assinatura dos atributos. Para a declaração de atributos é necessário abrir e fechar parênteses. Note que uma anotação é uma variação especial de uma interface. Para os atributos declarados também é possível definir um valor padrão através da palava chave `default`. 

Exemplo:
```java
@interface MyAnnotation {
    String author() default "Islan";
    int age();
    String nationality() default "brazilian";
}
```
Diferentemente de um atributo de classe, apenas atributos do tipo primitivo,`enum`, `Class`, `String`, outras anotações e arrays de qualquer um dos tipos citados.

**Fazendo uso da _annotation_** -- para o uso da anotação basta chamá-la acima do elemento ao qual deseja anotar. Lembrando que ao declarar atributos dentro da anotação, eles precisarão ser definidos no momento do uso, caso não possuam valor padrão.

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
Dentro da criação de uma anotação, existe um nome especial para atributo chamado `value`. Caso esse seja o único atributo declarado ou os outros atributos existentes já tenham um valor `default`, é possível fazer uso da anotação omitindo o nome do atributo e passando apenas a sua definição de valor.

Exemplo:
```java
public @interface MyAnnotation1 {
	int value(); 
}

public @interface MyAnnotation2 {
	int value(); 
	String description() default "Learning annotations in Java";
}

public @interface MyAnnotation3 {
	int value(); 
	String description();
}


@MyAnnotation1(13) //** VALID ** - the same as (value=13)
@MyAnnotation2(14) // ** VALID ** - the same as (value=14)
@MyAnnotation3(15) // ** INVALID ** - the correct would be (value=15, description="It's correct now");
public class Test {
}
```
É importante frisar que as anotações **NÃO FAZEM NADA** a não ser agregar novas informações sobre os elementos das classes. Para que elas tenham algum efeito sobre o funcionamento do programa, alguém precisa recuperar essas anotações e fazer alguma coisa a respeito, pois sozinhas as anotações não fazem nada.

**Definindo até quando a anotação está disponível** -- umas das principais configurações de uma _annotation_ é até quando ela estará disponível para ser recuperada. Dependendo de qual que seja o seu uso, mais de um tipo de retenção pode ser necessário.
+ **`SOURCE`** : tipo de retenção que significa dizer que uma anotação só ficará disponível apenas no código fonte. Ou seja, no momento em que a classe é compilada, a anotação não é transferida para o `.class`. É geralmente utilizado para fins de documentação e para uso de ferramentas que fazem processamento direto de código fonte;
+ **`CLASS`** : tipo de retenção que significa dizer que uma anotação será mantida também nos arquivos `.class`, mas não serão carregadas pela JVM (_Java Virtual Machine_). Nesse caso elas ficam disponíveis até o carregamento da classe. É utilizada por ferramentas que fazem processamento do _bytecode_ da classe, podendo este ser feito de forma estática como uma etapa posterior a compilação ou no momento do carregamento das classes;
+ **`RUNTIME`** : tipo de retenção que significa dizer que uma anotação estará disponível para recuperação em tempo de execução. A JVM irá carregar a anotação em memória e torná-la accessível via `Reflection`. É utilizada geralmente por frameworks que precisam de acesso a anotação em tempo de execução.

Para definir qual o tipo de retenção a anotação terá, é preciso anotá-la com uma outra anotação, chamada `@Retention`. Essa anotação recebe como parâmetro um `enum` do tipo `RetentionPolicy`. Esse `enum` irá possuir os três tipos de retenção descritos anteriormente.
Caso nenhum tipo de retenção seja declarado, o padrão é o `SOURCE`.

Exemplo:
```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    
}
```

**Definindo onde a _annotation_ precisa ser usada** -- no momento da declaração de uma anotação, é possível informar onde deverá ser o seu uso, se é em uma classe, método, atributo etc. Isso se dá através do uso da anotação `@Target`. Essa anotação recebe como parâmetro um `enum` do tipo `ElementType`. O `ElementType` terá as seguintes opções: 
+ **`TYPE`** : qualquer definição de tipos como classes, interfaces e enumeradores;
+ **`PACKAGE`** : pacotes;
+ **`CONSTRUCTOR`** : construtores;
+ **`FIELD`** : atributos;
+ **`METHOD`** : métodos;
+ **`PARAMETER`** : parâmetros de métodos e construtores;
+ **`LOCAL_VARIABLE`** : variáveis locais;
+ **`ANNOTATION_TYPE`** : anotações.

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

**Outras definições** -- além das anotações `@Retention` e `@Target`, outras podem vir a ser usadas, que são elas: 
+ **`@Documented`** : quando houver a necessidade da anotação anotada ser incorporada junto à documentação dos elementos anotados;
+ **`@Inherited`**: a anotação anotada será propagada para as subclasses que herdam da classe a qual possui essa anotação. Como é caso de herança de anotações, o uso dessa configuração só fará sentido para anotações do tipo `TYPE`. Um método sobrescrito por uma subclasse não irá herdar as anotações do tipo `@Inherited` do método que está sobrescrevendo.

**Recuperando as anotações em tempo de execução** -- existe uma interface chamada `AnnotatedElement` que define os métodos para a recuperação das anotações. Todas as classes que representam os elementos que podem ser anotados, isto é, as classes `Class`, `Method`, `Field`, `Package` e `Constructor` implementam essa interface.
+ `isAnnotationPresent()` : pode ser utilizado para verificar se uma determinada anotação está presente ou não no elemento. Recebe como parâmetro a classe da anotação (`.class`) e retorna um `boolean` informando se a anotação existe ou não. 
+ `getAnnotation()` : recebe como parâmetro a classe da anotação (`.class`) e retorna a anotação desejada. A instância retornada possui o tipo da anotação, e seus atributos podem ser recuperados através dos métodos com seus nomes.

Exemplo:
```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
	String name();
	int number();
}

@MyAnnotation(name="Learn Annotation", number=23)
public class MyClass {

	public static void main(String[] args) {
		Class<MyClass> c = MyClass.class;

		//verify if the annotation exists in the element
		if(c.isAnnotationPresent(MyAnnotation.class)) {
			MyAnnotation annotation = c.getAnnotation(MyAnnotation.class);
			System.out.println("Name Propertie = " + annotation.name());
			System.out.println("Number Propertie = " + annotation.number());
		}
	}
}
```

+ `getAnnotations()` : irá retornar uma lista com todas as anotações de um determinado elemento.
+ `getDelcaredAnnotations()` : irá retornar somente as anotações que foram diretamente declaradas no elemento, excluindo as que foram herdadas através do `@Inherited`. Como a questão de herançcas de anotações só se aplica a elementos do tipo `Class`, o retorno para os outros tipos de elementos será o mesmo para ambos os métodos.

**Recuperando anotações de parâmetros** -- estas anotações são recuperadas de forma diferente simplesmente pelo fato da `API Reflection` não possuir uma classe que represente um parâmetro. 
+ `getParameterAnnotations()` : esse método está presente nos elementos `Method` e `Constructor` e retorna um array bidimensional de `Annotation`. A primeira dimensão representa os parâmetros daquele elemento e a segunda dimensão representa as anotações contidas naquele parâmetro.

As anotações em parâmetro se tornam úteis quando há a necessidade de identificar qual informação precisa ser passada ele.

Exemplo:
```java
@Retention(RetentionPolicy.RUNTIME)
@Element(ElementType.PARAMETER)
public @interface Param {
	String value();
}


public static Object invokeMethod(Method m, Object obj, Map<String, Object> info) throws Exception {
	Annotation[][] paramAnnot = m.getParametersAnnotations();
	Object[] paramValues = new Object[paramAnnot.length];

	for (int i=0; i < paramValues.length; i++) {
		String name = getParameterName(paramAnnot[i]);
		paramValues[i] = info.get(name);
	}

	return m.invoke(obj, paramValues);
}


public static String getParameterName(Annotation[] annotations) {
	for (Annotation a : annotations) {
		if (a instanceof Param) {
			return ((Param)a).value();
		}
	}

	throw new RuntimeException("@Param Annotation not found.");
}


public class TestParameterAnnotation {

	public static void main(String[] args) throws Exception {
		Map<String, Object> info = new HashMap<>();
		info.put("int", 20);
		info.put("text", "Hello, World");
		info.put("String", "Hi, there");
		info.put("number", 30);

		TestParameterAnnotation testClass = new TestParameterAnnotation();
		Method testMethod = test.getClass().getMethod("testMethod", Integer.class, String.class);
		invokeMethod(testMethod, testClass, info);
	}

	public void testMethod(@Param("number") Integer i, @Param("text") String s) {
		System.out.println("Number parameter = " + i);
		System.out.println("Text parameter = " + s);
	}
}

```
