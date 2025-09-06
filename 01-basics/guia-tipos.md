# Guia de Tipos em Java

Este guia aborda os tipos de dados em Java, incluindo primitivos,
objetos e wrappers.

------------------------------------------------------------------------

## Tipos Primitivos

Java possui 8 tipos primitivos básicos:

  Tipo      Tamanho   Valor Padrão       Exemplo
  --------- --------- ------------------ ----------------------
  byte      8 bits    0                  byte b = 10;
  short     16 bits   0                  short s = 1000;
  int       32 bits   0                  int i = 5000;
  long      64 bits   0L                 long l = 100000L;
  float     32 bits   0.0f               float f = 3.14f;
  double    64 bits   0.0d               double d = 3.1415;
  char      16 bits   '`\u0`{=tex}000'   char c = 'A';
  boolean   1 bit     false              boolean flag = true;

### Observações

-   `float` e `double` são usados para números de ponto flutuante.\
-   `char` representa um único caractere Unicode.\
-   `boolean` só aceita `true` ou `false`.

------------------------------------------------------------------------

## Tipos Wrappers

Para cada tipo primitivo, existe uma classe wrapper que permite tratar o
valor como objeto:

  Primitivo   Wrapper
  ----------- -----------
  byte        Byte
  short       Short
  int         Integer
  long        Long
  float       Float
  double      Double
  char        Character
  boolean     Boolean

Exemplo de uso:

``` java
int numero = 10;
Integer numeroObj = Integer.valueOf(numero); // Autoboxing
int outro = numeroObj.intValue();            // Unboxing
```

------------------------------------------------------------------------

## Strings

-   `String` é uma classe imutável que representa texto.\
-   Operações comuns: concatenação, tamanho, substring, comparação.

``` java
String nome = "Java";
String saudacao = "Olá " + nome;
int tamanho = nome.length();
String sub = nome.substring(1,3); // "av"
boolean iguais = nome.equals("Java"); // true
```

------------------------------------------------------------------------

## Conversão de Tipos

-   **Casting implícito** (tipo menor → tipo maior):\

``` java
int i = 10;
long l = i; // ok
```

-   **Casting explícito** (tipo maior → tipo menor):\

``` java
double d = 9.78;
int j = (int)d; // 9
```

-   **Conversão entre String e números**:\

``` java
int num = Integer.parseInt("123");
String str = String.valueOf(456);
```

------------------------------------------------------------------------

## Resumo Rápido

1.  Java possui **8 tipos primitivos**.\
2.  Cada primitivo tem um **wrapper** correspondente.\
3.  `String` é imutável e possui métodos utilitários.\
4.  Casting permite conversão entre tipos numéricos.\
5.  Use wrappers quando precisar de objetos ou coleções.

------------------------------------------------------------------------
