# Exceptions em Java

## 1. O que são Exceptions?
Exceptions são eventos que interrompem o fluxo normal de execução de um programa.  
No Java, elas são usadas para lidar com erros de forma estruturada e previsível.

---

## 2. Hierarquia de Exceptions

- **Throwable**
  - **Error** → erros graves, geralmente não tratados (ex: `OutOfMemoryError`)
  - **Exception**
    - **Checked Exceptions** → devem ser tratadas ou declaradas com `throws`
    - **Unchecked Exceptions (RuntimeException)** → erros em tempo de execução

**Exemplo:**
```java
try {
    int resultado = 10 / 0; // ArithmeticException (unchecked)
} catch (ArithmeticException e) {
    System.out.println("Erro: " + e.getMessage());
}
```

---

## 3. Checked vs Unchecked

### Checked (verificadas)
Devem ser tratadas com `try/catch` ou declaradas com `throws`.
```java
public void lerArquivo(String caminho) throws IOException {
    FileReader fr = new FileReader(caminho);
}
```

### Unchecked (não verificadas)
Não precisam ser tratadas obrigatoriamente.
```java
int[] numeros = {1, 2, 3};
System.out.println(numeros[5]); // ArrayIndexOutOfBoundsException
```

---

## 4. Blocos Try-Catch-Finally

```java
try {
    int valor = Integer.parseInt("abc"); // NumberFormatException
} catch (NumberFormatException e) {
    System.out.println("Não é um número válido");
} finally {
    System.out.println("Bloco finally sempre executa");
}
```

---

## 5. Criando Exceções Personalizadas

```java
class SaldoInsuficienteException extends Exception {
    public SaldoInsuficienteException(String mensagem) {
        super(mensagem);
    }
}

class Conta {
    private double saldo = 100;
    public void sacar(double valor) throws SaldoInsuficienteException {
        if (valor > saldo) {
            throw new SaldoInsuficienteException("Saldo insuficiente!");
        }
        saldo -= valor;
    }
}
```

---

## 6. Try-with-Resources (Java 7+)

Usado para liberar recursos automaticamente.

```java
try (BufferedReader br = new BufferedReader(new FileReader("arquivo.txt"))) {
    System.out.println(br.readLine());
} catch (IOException e) {
    e.printStackTrace();
}
```

---

## 7. Boas Práticas

- Tratar exceções específicas primeiro, depois as genéricas.
- Não usar `Exception` de forma ampla sem necessidade.
- Usar exceções personalizadas para regras de negócio.
- Evitar lógica complexa dentro de blocos `catch`.
- Preferir `try-with-resources` para recursos que precisam ser fechados.

---

## 8. Referências

- [Oracle Docs – Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/)  
- [Baeldung – Exceptions in Java](https://www.baeldung.com/java-exceptions)  
- [GeeksforGeeks – Java Exceptions](https://www.geeksforgeeks.org/exceptions-in-java/)  

---

> Este guia faz parte do repositório `java-core-concepts`, seção 04-exceptions.
