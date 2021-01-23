### Multitarefas: processos e Threads 
**Processo** -- é um programa que está sendo executado.
**Thread** -- é a menor unidade de código que pode ser executada. 

Ou seja, em um programa (_processo_) podem ser executadas uma ou mais tarefas (_threads_) ao mesmo tempo.

**Ciclo de Vida de uma thread** 
+ **`NEW`** : criação da instância;
+ **`RUNNABLE`** : pronta para execução;
+ **`RUNNING`** : em execução;
+ **`WAITING`** : em estado de espera;
+ **`DEAD`** : _Thread_ terminada.

![life cycle illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/life-cycle-thread.png)

**Métodos importantes** -- basicamente são os métodos mais importantes dentro do ciclo de vida de uma _Thread_.
+ **`start`** : inicia a _Thread_, deixando pronta para ser executada;
+ **`run`** : executa a tarefa a qual a _Thread_ foi designada a realizar;
+ **`sleep`** : coloca a _Thread_ pra dormir por x milissegundos.

**Criação de uma Thread** -- existem duas maneiras de criação de uma _Thread_. 
+ Extendendo a classe Thread;
+ Implementando a interface Runnable.

**Criando uma Thread extendendo a classe Thread** -- nesse cenário, para que uma _Thread_ consiga ser executada, é necessário que o método `run` seja sobrecarregado e o método `start` executado.

Exemplo:
```java
public class MyThread extends Thread {
    private String nome;
    private int tempo;
    
    public MyThread(String nome, int tempo) {
        this.nome = nome;
        this.tempo = tempo;
        start(); // essa estratégia permite que a Thread seja iniciada a partir do momento em que uma instância seja criada
    }
    
    @Override
    public void run() {
        try {
            for (int i = 0; i < 10, i++) {
                System.out.println(nome + " -- Contador " + i);
                Thread.sleep(tempo); // faz com que a Thread "durma" por um determinado tempo e depois volte a executar
            }
            
        } catch(InterruptedException e) {
            e.printStackTrace();
        }
    }
    
}
    
public static void main(String[] args) { 
    MyThread myThread01 = new MyThread("#1 Thread", 200);
    MyThread myThread02 = new MyThread("#2 Thread", 400);
    MyThread myThread03 = new MyThread("#3 Thread", 800);
}
```

**Criando uma Thread implementando Runnable** -- nesse cenário o método `run` ainda deve ser implementado mas a execução do método `start` por parte da _Thread_ que está sendo criada deixa de existir. Para que seja caracterizado como de fato uma _Thread_, a classe que implementa Runnable precisa ser passada para uma instância de _Thread_. 

Exemplo:
```java
public class MyThread implements Runnable {
    private String nome;
    private int tempo;
    
    public MyThread(String nome, int tempo) {
        this.nome = nome;
        this.tempo = tempo;
        Thread t = new Thread(this); // atribuindo a classe para uma instância de Thread
        t1.start();                 // fazendo a execução da instância criada
    }
    
    @Override
    public void run() {
        try {
            for (int i = 0; i < 10, i++) {
                System.out.println(nome + " -- Contador " + i);
                Thread.sleep(tempo); // faz com que a Thread "durma" por um determinado tempo e depois volte a executar
            }
            
        } catch(InterruptedException e) {
            e.printStackTrace();
        }
    }
    
}
    
public static void main(String[] args) { 
    MyThread myThread01 = new MyThread("#1 Thread", 200);
    MyThread myThread02 = new MyThread("#2 Thread", 400);
    MyThread myThread03 = new MyThread("#3 Thread", 800);
}
```

**Método `isAlive`** -- o método tem como finalidade informar se a _Thread_ continua ativa ou não. O método retorna `true` caso o método `start` da _Thread_ tenha sido acionado e sua execução ainda não finalizada e retorna `false` caso contrário.

Exemplo:
```java
public static void main(String[] args) { 
    MyThread myThread01 = new MyThread("#1 Thread", 200);
    MyThread myThread02 = new MyThread("#2 Thread", 400);
    MyThread myThread03 = new MyThread("#3 Thread", 800);
    
    myThread01.start();
    myThread02.start();
    myThread03.start();
    
    while (myThread01.isAlive() || myThread02.isAlive() || myThread03.isAlive()) {
       try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    
    System.out.println("Programa Finalizado");
}
```


**Método `join`** -- o método tem como finalidade permitir que uma _Thread_ entre em um estado de espera, fazendo com que a próxima instrução do programa só seja executada após o encerramento da mesma. Em casos onde a _Thread_ for bloqueada ou tenha uma elevado tempo de resposta, esse comportamento pode ser problemático. Por conta disso, há sobrecargas no método `join`. São elas: `join(long millis)`; caso a execução da _Thread_ não seja encerrada dentro desse intervalo informado em `millis` (dado em millessegundos), o fluxo do programa é liberado e a próxima instrução é executada e `join(long millis, int nanos)`; onde é esperado `millis` (dado em milessegundos) + `nano` (dado em nanossegundos) para o fim da execução da _Thread_, caso contrário o fluxo do programa é liberado e a próxima instrução é executada.

Exemplo:
```java
public static void main(String[] args) { 
    MyThread myThread01 = new MyThread("#1 Thread", 500);
    MyThread myThread02 = new MyThread("#2 Thread", 1000);
    MyThread myThread03 = new MyThread("#3 Thread", 1500);
    
    myThread01.start();
    myThread02.start();
    myThread03.start();
    
    try {
        myThread01.join();
        myThread02.join();
        myThread03.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    
    System.out.println("Programa Finalizado");
}
```

