### Classes aninhadas: internas, locais e anônimas
**Classes internas** -- uma classe declarada internamente dentro de uma outra classe. As classes declaradas internas têm a possibilidade de acessar os atributos da classe externa.
Nesse caso, como a classe interna não foi declarada como estática, para que seja possível acessar os atributos da classe interna é necessário haver uma instância da classe externa.

Exemplo:
```java
public class External {
    private String text = "External text";
    
    public class Internal {
        private String text = "Intenal text";
        
        public void printText() {
            System.out.println(text);
            
            //Can access external class attributes
            System.out.println(External.this.text);
        }
    }
}

public static void main(String[] args) {
    External external = new External();
    Internal internal = external.new Internal();
    
    internal.printText(); 
}
```

**Classes locais** -- classes declaradas dentro de um método de uma classe externa. Essa classe só terá escopo dentro do método ao qual foi declarada. Ou seja, não é possível chamá-la ou instanciá-la fora do método como acontece com as classes internas.  

Exemplo: 
```java
public class External {
    
    public void anyMethod() {
        class LocalClass {
            private String text = "Local Class text";
            
            public void printText() {
                System.out.println(text);
             }
        }
        
        LocalClass local = new LocalClass();
        local.printText();
    }
}

public static void main(String[] args) {
    External external = new External();
    external.anyMethod(); //output -> "Local Class text"
}
```

**Classes anônimas** -- classes que têm o seu comportamento modificado no momento em que é instanciada. Ou seja, no momento em que a classe é instanciada (após o `new Class()`) é definido um corpo com `{}` e dentro dele é sobrescrito algum comportamento em tempo de execução (_runtime_).

Exemplo:
```java
public class Anonymous {
    
    public void printText() {
        System.out.println("Any Text");
    }
}

public static void main(String[] args) {
    Anonymous anonymous = new Anonymous() {
        public void printText() {
            System.out.println("Any text modified");
        }
        
        anonymous.printText(); //outuput -> "Any text modified"
    }
}
```

É interessante analisar que uma interface pode ser instanciada como uma classe anônima. 

Exemplo:
```java
public interface Text() {
    void printText();
}

public static void main(String[] args) {
    
    //Using interface   
    Text text = new Text() {
        @Override
        public void printText() {
            System.out.println("Any Text - using Interface with Anonymous class")
        }
        
        text.printText(); output -> "Any Text - using Interface with Anonymous class"
    }
}
```
