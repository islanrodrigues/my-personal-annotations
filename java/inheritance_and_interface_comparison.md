### Herança única e múltipla
Uma classe só permite herança única. Interface, por outro lado, permitem heranças múltiplas.

Exemplo:

```java
//Herança de classe - apenas única
public class Student extends Person {

}

// Herança de interface - única ou múltipla
public interface Animal extends Mammal, Bird, Fish, Reptile, Amphibian {

}
```

- - -

### Herança de classes abstratas 
Classes normais podem herdar de classes abstratas, desde de que esta última não tenha sido declarada com o modificador `final`.

Exemplo:

```java
// Pode ser estendida
public abstract class Person {
}

// Não pode ser estendida
public final abstract class Person {
}
```