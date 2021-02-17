### Multitarefas: processos e _Threads_ 
**Processo** -- é um programa que está sendo executado.   
**_Thread_** -- é a menor unidade de código que pode ser executada. 

Ou seja, em um programa (_processo_) podem ser executadas uma ou mais tarefas (_Threads_) ao mesmo tempo.

**Ciclo de Vida de uma _Thread_** 
+ **`NEW`** : criação da instância;
+ **`RUNNABLE`** : pronta para execução;
+ **`RUNNING`** : em execução;
+ **`WAITING`** : em estado de espera;
+ **`DEAD`** : _Thread_ terminada.

![life cycle illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/java/life-cycle-thread.png)

**Métodos importantes** -- basicamente são os métodos mais importantes dentro do ciclo de vida de uma _Thread_.
+ **`start`** : inicia a _Thread_, deixando pronta para ser executada (o método `run` é chamado);
+ **`run`** : executa a tarefa a qual a _Thread_ foi designada a realizar;
+ **`sleep`** : coloca a _Thread_ pra dormir por x milissegundos.

**Criação de uma _Thread_** -- existem duas maneiras de criação de uma _Thread_. 
+ Extendendo a classe `Thread`;
+ Implementando a interface `Runnable`.

**Criando uma _Thread_ extendendo a classe `Thread`** -- nesse cenário, para que uma _Thread_ consiga ser executada, é necessário que o método `run` seja sobrecarregado e o método `start` executado.

Exemplo:
```java
public class MyThread extends Thread {
    private String nome;
    private int tempo;
    
    public MyThread(String nome, int tempo) {
        this.nome = nome;
        this.tempo = tempo;
        start(); // essa estratégia permite que a Thread seja iniciada a partir do momento em que uma instância for criada
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

**Criando uma _Thread_ implementando `Runnable`** -- nesse cenário o método `run` ainda deve ser implementado mas a execução do método `start` por parte da classe criada deixa de existir. Para que seja caracterizado como de fato uma _Thread_, a classe que implementa `Runnable` precisa ser passada para uma instância de `Thread`. 

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
    // Thread t1 = new Thread(myThread01) --> caso a estratégia de instanciar e executar a Thread no construtor não fosse usada

    MyThread myThread02 = new MyThread("#2 Thread", 400);
    // Thread t2 = new Thread(myThread02) --> caso a estratégia de instanciar e executar a Thread no construtor não fosse usada

    MyThread myThread03 = new MyThread("#3 Thread", 800);
    // Thread t3 = new Thread(myThread03) --> caso a estratégia de instanciar e executar a Thread no construtor não fosse usada
}
```

**Método `isAlive`** -- o método tem como finalidade informar se a _Thread_ continua ativa ou não. Retorna `true` caso o método `start` da _Thread_ tenha sido acionado e sua execução ainda não finalizada ou `false` caso contrário.

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


**Método `join`** -- o método tem como finalidade permitir que uma _Thread_ entre em um estado de espera, fazendo com que a próxima instrução do processo só seja executada após o encerramento da mesma. Em casos onde a _Thread_ for bloqueada ou tenha um elevado tempo de resposta, esse comportamento pode ser problemático. Por conta disso, existem sobrecargas no método `join`. São elas: `join(long millis)`; caso a execução da _Thread_ não seja encerrada dentro desse intervalo informado em `millis` (dado em millessegundos), o fluxo do processo é liberado e a próxima instrução é executada e `join(long millis, int nanos)`; onde é esperado `millis` (dado em milessegundos) + `nano` (dado em nanossegundos) para o fim da execução da _Thread_, caso contrário o fluxo do processo é liberado e a próxima instrução é executada.

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

**Definindo prioridades de execução das _Threads_** -- as _Threads_ têm a possibilidade de setar a prioridade de execução, através do método `setPriority`. Caso essa informação não seja informada, é entendido que a _Thread_ terá prioridade normal. É permitido setar essa informação de prioridade com os valores de 1 a 10 ou com as constantes de prioridade existentes da classe `Thread`.

Exemplo:
```java
    MyThread myThread01 = new MyThread("#1 Thread", 500);
    MyThread myThread02 = new MyThread("#2 Thread", 1000);
    MyThread myThread03 = new MyThread("#3 Thread", 1500);
    
    myThread01.start();
    myThread02.start();
    myThread03.start();
    
    // with int values
    myThread01.setPriority(1);
    myThread02.setPriority(2);
    myThread03.setPriority(3);
    
    // with constants
    myThread01.setPriority(Thread.MAX_PRIORITY);
    myThread02.setPriority(Thread.NORM_PRIORITY);
    myThread03.setPriority(Thread.MIN_PRIORITY);
    
```

**Métodos e blocos sincronizados** -- é o ato de coordenar as atividades de duas ou mais _Threads_. Quando duas ou mais _Threads_ precisam um recurso compartilhado, isso garante que somente uma _Thread_ pode acessar o recurso por vez. É usado a palavra `synchronized` em assinaturas de métodos ou em blocos de código.

Exemplo:
```java
public Calculator {
    private int sum;

    public synchronized sumArray(int[] array) {
        sum = 0;

        for(inti = 0; i < array.length; i++) {
            sum += array[i];
        }   

        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

**Métodos `notify`, `wait` e `notifyAll`** -- são métodos que permitem um revezamento de um determinado recurso entre _Threads_. Isso impede que um determinado recurso fique bloqueado por muito tempo sendo passível da ocorrência de um _deadlock_. A utilização destes métodos deve ser dentro de um bloco de código sincronizado (`synchronized`).
+ **`wait`** : bloqueia a execução da _Thread_ temporariamente, colocando-a em um estado de espera. A _Thread_ fica em modo de espera até que seja notificada;
+ **`notify`** : notifica uma _Thread_ que estava esperando para resumir a sua execução, ou seja, retornar a sua execução;
+ **`notifyAll`** : caso exista mais de uma _Thread_ a ser notificada, onde a que possuir prioridade mais alta terá acesso ao recurso.

Exemplo:
```java
//Simple Class
public class TicTac {
	boolean tic;

	synchronized void tic(boolean isExecute) {
		if (!isExecute) {
			tic = true;
			notify();
			return;
		}

		System.out.print("Tic ");
		tic = true;
		notify();

		try {
			while (tic) {
				wait();
			}
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
	
	synchronized void tac(boolean isExecute) {
		if (!isExecute) {
			tic = false;
			notify();
			return;
		}

		System.out.println("Tac");
		tic = false;
		notify();

		try {
			while (!tic) {
				wait();
			}
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
}


// Thread
public class ThreadTicTac implements Runnable {

	TicTac tictac;
	Thread t;
	
	final int NUM = 5;
	
	public ThreadTicTac(String name, TicTac tt) {
		this.tictac = tt;
		t = new Thread(this, name);
		t.start();
	}

	@Override
	public void run() {
		if (t.getName().equalsIgnoreCase("Tic")) {
			for (int i=0; i<NUM; i++) {
				tictac.tic(true);
			}

			tictac.tic(false);

		} else {
			for (int i=0; i<NUM; i++) {
				tictac.tac(true);
			}

			tictac.tac(false);
		}		
	}
}


// Main method
public static void main(String[] args) {
		
    TicTac tictac = new TicTac();
    ThreadTicTac tic = new ThreadTicTac("Tic", tictac);
    ThreadTicTac tac = new ThreadTicTac("Tac", tictac);
    
    try {
        tic.t.join();
        tac.t.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```

**Métodos `resume`, `suspend` e `stop`** -- são métodos que existiam até o Java 2. O método `suspend` foi removido pelo fato de poder causar _dedlocks_. O método `resume`, como depende do método anterior, também foi removido. E por fim, o método `stop` foi substituído pelo método `interrupt` (por este motivo que existe a `InterruptedException`). Mesmo não existindo mais na classe `Thread`, é possível implementar estes métodos de uma forma segura.
+ **`suspend`** : suspende (pausa) temporariamente a execução da _Thread_;
+ **`resume`** : resume (despausa) a execução da _Thread_;
+ **`stop`** : termina a execução da _Thread_.

Exemplo: 
```java
public class MyThread implements Runnable {

	private String name;
	private boolean isSuspend;
	private boolean wasTerminated;

	public MyThread(String name){
		this.name = name;
		this.isSuspend = false;
		new Thread(this, name).start();
	}

	@Override
	public void run() {
		System.out.println("Run " + this.name);

		try {
			for (int i=0; i<10; i++) {
				System.out.println("Thread " + name + ", " + i);
				Thread.sleep(300);

				synchronized (this) {
					while (isSuspend){
						wait();
					}
					if (this.wasTerminated){
						break;
					}
				}
			}
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		System.out.println("Thread " + this.name + " terminated.");
	}
	
	void suspend() {
		this.isSuspend = true;
	}

	synchronized void resume() {
		this.isSuspend = false;
		notify();
	}
	
	synchronized void stop() {
		this.wasTeminated = true;
		notify();
	}
}


public static void main(String[] args) {
    MinhaThread t1 = new MinhaThread("#1");
    MinhaThread t2 = new MinhaThread("#2");
    
    System.out.println("Suspend Thread #1");
    t1.suspend();
    
    try {
        Thread.sleep(200);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    
    System.out.println("suspend Thread #2");
    t2.suspend();
    
    System.out.println("Resume Thread #1");
    t1.resume();
    
    try {
        Thread.sleep(200);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    
    System.out.println("Resume Thread #2");
    t2.resume();
    
    System.out.println("Stop Thread #2");
    t2.stop();
}
```




