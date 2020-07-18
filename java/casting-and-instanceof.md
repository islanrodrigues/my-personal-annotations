### Casting
A conversão (_casting_) em Java é permitido porque existe o conceito de herança entre classes. 
Por conta disso, é possível converter uma subclasse pra um tipo superclasse e vice versa.

**Upcasting** -- instância de uma superclasse recebendo a referência de uma subclasse. Geralmente é automático. Não há a necessidade de _casting_ manual, embora possa.
	
Exemplo:
```java
Person person = new Person();
Object newPerson = person; //upcasting

Person student = new Student(); //o mesmo que Person student = (Person) new Student();
```

**Downcasting** -- instância de uma subclasse recebendo a referência de uma superclasse.
Precisa se atentar a esse tipo de _casting_, uma vez que uma _exception_ (_ClassCastException_) pode ser disparada.
Em outras palavras, o _downcasting_ só funciona se você estiver referenciado aquele tipo em particular.

Exemplo:
```java
Person person = new Person();
Student student = (Student) person; //downcasting

public static void main(String[] args) {
	Object object01 = obterString();
	String string01 = (String) objet01; //downcasting funciona

	Object object02 = new Object();
	String string02 = (String) object02; //dispara erro em tempo de execução (runtime). object02 não referencia String		
}

		
public static String obterString() {
	return "Teste de Downcasting"; 
}
```

- - - 

### Operador instaceOf
O operador `<instaceof>` é utilizado quando há a necessidade de verificar qual a classe de uma instância de um objeto.

Exemplo:
```java		
public static void main(String[] args) {
    Person person = new Person();
	Student student = new Student();
			
	if (person instaceof Person) {
		System.out.println("Its a Person instance");
	}
			
	if (student instaceof Student) {
		System.out.println("Its a Student instance");
	}
}
```

