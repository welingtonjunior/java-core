# Guia Completo de Streams e Lambda Expressions em Java (Java 8+)

## 1. Introdução

Com o Java 8, duas grandes funcionalidades foram adicionadas:
**expressões lambda** e a **Streams API**.\
Esses recursos permitem escrever código mais conciso, legível e
eficiente, aproveitando conceitos de programação funcional.

------------------------------------------------------------------------

## 2. Expressões Lambda

### 2.1. O que são?

Uma expressão **lambda** é uma forma curta de implementar interfaces
funcionais (interfaces com **um único método abstrato**).\
Sintaxe básica:

``` java
(parâmetros) -> expressão
(parâmetros) -> { bloco de código }
```

### 2.2. Exemplo

``` java
// Antes do Java 8
new Thread(new Runnable() {
    public void run() {
        System.out.println("Executando...");
    }
}).start();

// Com lambda
new Thread(() -> System.out.println("Executando...")).start();
```

### 2.3. Interfaces Funcionais

-   **Exemplos já disponíveis no Java:**
    -   `Runnable`\
    -   `Comparator<T>`\
    -   `Predicate<T>` (retorna boolean)\
    -   `Function<T,R>` (transforma um tipo em outro)\
    -   `Consumer<T>` (consome um valor, não retorna)\
    -   `Supplier<T>` (fornece um valor, sem entrada)

``` java
Predicate<String> isEmpty = s -> s.isEmpty();
Function<String, Integer> length = s -> s.length();
```

------------------------------------------------------------------------

## 3. Streams API

### 3.1. O que são Streams?

Uma forma de **processar coleções de dados** (listas, arrays, etc.) de
maneira declarativa e funcional.\
Fluxo típico:\
1. Criar um Stream (`list.stream()`)\
2. Aplicar operações intermediárias (`filter`, `map`, `sorted`, ...)\
3. Encerrar com uma operação terminal (`collect`, `forEach`, `reduce`,
...)

### 3.2. Exemplo simples

``` java
List<String> nomes = Arrays.asList("Ana", "Pedro", "Carlos");

nomes.stream()
     .filter(n -> n.startsWith("C"))
     .map(String::toUpperCase)
     .forEach(System.out::println);
// Saída: CARLOS
```

------------------------------------------------------------------------

## 4. Operações de Stream

### 4.1. Intermediárias (retornam outro Stream)

-   `filter(Predicate)` → filtra elementos\
-   `map(Function)` → transforma cada elemento\
-   `sorted()` → ordena elementos\
-   `distinct()` → remove duplicados\
-   `limit(n)` / `skip(n)` → pega ou pula elementos

### 4.2. Terminais (encerram o Stream)

-   `forEach(Consumer)` → itera sobre elementos\
-   `collect(Collectors.toList())` → coleta resultado em lista\
-   `reduce()` → reduz a um único valor\
-   `count()` → conta elementos\
-   `findFirst()`, `findAny()` → busca elemento

### 4.3. Exemplos

``` java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);

// Filtrar pares e somar
int soma = numeros.stream()
                  .filter(n -> n % 2 == 0)
                  .mapToInt(n -> n)
                  .sum(); // 12

// Converter lista em outra lista
List<String> upper = nomes.stream()
                          .map(String::toUpperCase)
                          .collect(Collectors.toList());
```

------------------------------------------------------------------------

## 5. Parallel Streams

Permite processar em paralelo, aproveitando múltiplos núcleos.

``` java
List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6);

numeros.parallelStream()
       .forEach(System.out::println);
```

⚠️ Use com cuidado: pode haver problemas de sincronização ou ordem
indesejada.

------------------------------------------------------------------------

## 6. Benefícios

-   Código mais **legível** e **declarativo**.\
-   Menos loops manuais (`for`, `while`).\
-   Suporte simplificado a **processamento paralelo**.\
-   Integração com **interfaces funcionais** já existentes.

------------------------------------------------------------------------

## 7. Exemplo Completo

``` java
import java.util.*;
import java.util.stream.*;

public class StreamsLambdaExample {
    public static void main(String[] args) {
        List<String> nomes = Arrays.asList("Ana", "Pedro", "Carlos", "João", "Amanda");

        // Exemplo: Filtrar nomes com A, transformar em maiúsculas e ordenar
        List<String> resultado = nomes.stream()
                                      .filter(n -> n.startsWith("A"))
                                      .map(String::toUpperCase)
                                      .sorted()
                                      .collect(Collectors.toList());

        System.out.println(resultado); // [AMANDA, ANA]
    }
}
```

------------------------------------------------------------------------

## 8. Resumo Rápido (Tabela)

  ----------------------------------------------------------------------------------
  Recurso         Exemplo                           Descrição
  --------------- --------------------------------- --------------------------------
  Lambda          `(x, y) -> x + y`                 Função anônima

  Predicate       `s -> s.isEmpty()`                Retorna boolean

  Function        `s -> s.length()`                 Transforma de um tipo para outro

  Stream criação  `list.stream()`                   Cria um Stream a partir da lista

  Intermediária   `.filter(n -> n > 0)`             Retorna outro Stream

  Terminal        `.collect(Collectors.toList())`   Gera resultado final

  Paralelo        `list.parallelStream()`           Processa em paralelo
  ----------------------------------------------------------------------------------

------------------------------------------------------------------------

## 9. Referências

-   [Oracle Docs --
    Streams](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)\
-   [Baeldung -- Guide to Java
    Streams](https://www.baeldung.com/java-8-streams)\
-   [GeeksforGeeks -- Stream API in
    Java](https://www.geeksforgeeks.org/stream-in-java/)\
-   [Oracle Docs -- Lambda
    Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)
