### Classe `Throwable`
A classe mãe (superclasse) tanto dos erros quanto das exceptions.
```
Throwable
    ├─ Error
    └─ Exception
```

### Diferença entre erro e exceção
**Error** -- irá indicar um problema que a aplicação não conseguirá capturar para tratamento. É um erro que irá acontecer em tempo de execução (_runtime_) e vai fazer com que o programa seja encerrado. A maioria são condições anormais.

Exemplo:
`OutOfMemoryError` - Estouro de memória do Java.

**Exception** -- irá indicar um problema tratável dentro da aplicação, através do uso do `try/catch`. Existem dois tipos de exceções no Java: as não verificadas (_unchecked_) e as verificadas (_checked_). Exceções não verificadas são aquelas que acontecem em tempo de execução (_runtime_). Exceções verificads são aquelas que podem ser verificadas em tempo de compilação.

```
Exception
    ├─ Runtime Exception 
            ├─ ArrayIndexOutOfBoundsExceptiom
            ├─ NullPointerException
            ├─ ClassCastException
            ├─ ArithmeticException
            └─ ...
    ├─ IOException
    ├─ SQLException
    └─ ...
```
