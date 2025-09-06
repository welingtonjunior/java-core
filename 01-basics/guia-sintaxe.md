# Guia de Sintaxe Básica em Java

Este guia apresenta a estrutura fundamental da linguagem Java, ideal
para quem está dando os primeiros passos.

------------------------------------------------------------------------

## Estrutura de um Programa Java

Um programa Java básico contém: - **Classe**: ponto de entrada -
**Método `main`**: início da execução - **Declarações**: comandos a
serem executados

``` java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Olá, mundo!");
    }
}
```

------------------------------------------------------------------------

## Convenções de Sintaxe

-   **Case-sensitive**: `idade` e `Idade` são diferentes.\
-   **Nomes de classes**: começam com maiúscula (`MinhaClasse`).\
-   **Nomes de métodos e variáveis**: começam com minúscula
    (`minhaVariavel`).\
-   **Arquivos**: devem ter o mesmo nome da classe pública principal
    (`HelloWorld.java`).

------------------------------------------------------------------------

## Estruturas Comuns

### Declaração de Variáveis

``` java
int numero = 10;
String nome = "Ana";
```

### Estruturas de Controle

``` java
if (numero > 5) {
    System.out.println("Maior que 5");
} else {
    System.out.println("Menor ou igual a 5");
}
```

### Laços

``` java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

### Métodos

``` java
public static int soma(int a, int b) {
    return a + b;
}
```

------------------------------------------------------------------------

## Entrada e Saída

### Saída no console

``` java
System.out.println("Mensagem");
```

### Entrada com Scanner

``` java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
System.out.print("Digite seu nome: ");
String nome = sc.nextLine();
System.out.println("Olá, " + nome);
sc.close();
```

------------------------------------------------------------------------

## Resumo Rápido

1.  Todo código Java está dentro de uma **classe**.\
2.  O método `main` é o **ponto de entrada**.\
3.  Respeite as **convenções de nomes**.\
4.  Use `System.out.println` para imprimir no console.\
5.  Utilize `Scanner` para ler dados do usuário.

------------------------------------------------------------------------
