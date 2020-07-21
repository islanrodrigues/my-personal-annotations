### Autoboxing e Unboxing
Processo de transformar um tipo primitivo em um tipo objeto e vice versa.

**Autoboxing** -- Capacidade de atribuição de um valor do tipo primitivo diretamente para o tipo de uma classe.

Exemplo:

```java
//autoboxing example
Integer intNumber = 10; //the same as new Integer(10);
```

**Unboxing** -- processo inverso ao do _autoboxing_. Ou seja, é a capacidade de atribuição de um tipo de uma classe para um tipo primitivo.

Exemplo:

```java
//unboxing example
Integer integerNumber = 10
int intNumber = integerNumber; // the same as integerNumber.getInt();
```

A funcionalidade de _autoboxing_ e _unboxing_ também podem ser aplicados em expressões e operações.

Exemplo:

```java
Integer num01 = new Integer(10);
int num02 = 20;

Integer count = num01 + num02;
count++;
```