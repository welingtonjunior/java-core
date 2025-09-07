# Guia de Programação Funcional em Java: Streams e Lambda Expressions

Este guia apresenta os conceitos fundamentais de **programação funcional em Java**, com foco em **expressões lambda** e **Streams API**.

---

## 📌 1. O que é Programação Funcional?

A programação funcional em Java permite escrever código mais conciso, expressivo e paralelo, usando funções como **objetos de primeira classe**.

Principais características:
- Uso de **funções como parâmetros**.
- **Imutabilidade** (preferência por objetos imutáveis).
- **Operações declarativas** em vez de imperativas.

---

## 📌 2. Expressões Lambda

Uma **lambda expression** é uma forma compacta de implementar interfaces funcionais (interfaces com **apenas um método abstrato**).

### 🔹 Sintaxe básica
```java
(parametros) -> expressão
```

### 🔹 Exemplo 1: Runnable com Lambda
```java
public class LambdaExemplo {
    public static void main(String[] args) {
        Runnable r = () -> System.out.println("Executando com Lambda!");
        new Thread(r).start();
    }
}
```

### 🔹 Exemplo 2: Comparator com Lambda
```java
import java.util.*;

public class ComparatorLambda {
    public static void main(String[] args) {
        List<String> lista = Arrays.asList("Banana", "Abacaxi", "Uva");
        lista.sort((a, b) -> a.compareToIgnoreCase(b));
        lista.forEach(System.out::println);
    }
}
```

---

## 📌 3. Interfaces Funcionais

Algumas interfaces funcionais da biblioteca Java:
- `Runnable` → sem parâmetros, sem retorno.
- `Callable<T>` → sem parâmetros, com retorno.
- `Consumer<T>` → recebe valor, sem retorno.
- `Function<T,R>` → recebe valor, retorna valor.
- `Predicate<T>` → recebe valor, retorna boolean.

Exemplo com `Predicate`:
```java
import java.util.function.Predicate;

public class PredicateExemplo {
    public static void main(String[] args) {
        Predicate<Integer> isPar = x -> x % 2 == 0;
        System.out.println(isPar.test(4)); // true
    }
}
```

---

## 📌 4. Streams API

Uma **Stream** representa uma sequência de elementos que podem ser processados em **cadeia** de operações.

Exemplo de fluxo:
```java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5);
numeros.stream()
       .filter(n -> n % 2 == 0)    // mantém pares
       .map(n -> n * 2)           // multiplica por 2
       .forEach(System.out::println); // imprime
```

---

## 📌 5. Operações em Streams

### 🔹 Intermediárias (retornam outra Stream)
- `filter()` → filtra elementos.
- `map()` → transforma elementos.
- `sorted()` → ordena.

### 🔹 Terminais (encerram a Stream)
- `forEach()` → iteração final.
- `collect()` → coleta resultado.
- `reduce()` → reduz a um único valor.

Exemplo:
```java
import java.util.*;
import java.util.stream.*;

public class StreamOperacoes {
    public static void main(String[] args) {
        List<String> nomes = Arrays.asList("Ana", "Pedro", "João", "Paula");

        List<String> resultado = nomes.stream()
                .filter(n -> n.startsWith("P"))
                .map(String::toUpperCase)
                .sorted()
                .collect(Collectors.toList());

        System.out.println(resultado);
    }
}
```

---

## 📌 6. Paralelismo com Streams

Streams podem ser executadas em paralelo para melhor desempenho:

```java
import java.util.stream.*;
import java.util.*;

public class StreamParalela {
    public static void main(String[] args) {
        List<Integer> numeros = IntStream.rangeClosed(1, 10).boxed().toList();

        numeros.parallelStream()
               .forEach(n -> System.out.println(n + " - " + Thread.currentThread().getName()));
    }
}
```

---

## 📌 7. Conclusão

- Lambdas tornam o código mais conciso.  
- Interfaces funcionais são a base da programação funcional em Java.  
- Streams permitem operações declarativas e paralelas em coleções.  

👉 Programação funcional aumenta a legibilidade e desempenho do código moderno em Java.
