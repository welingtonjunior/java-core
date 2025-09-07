# Generics em Java

## 1. O que são Generics?
Generics permitem criar **classes, interfaces e métodos parametrizados por tipo** em Java.  
Eles aumentam a **segurança de tipos**, evitam casts desnecessários e tornam o código mais legível e reutilizável.

**Exemplo sem Generics (Java < 5):**
```java
List lista = new ArrayList();
lista.add("Texto");
String valor = (String) lista.get(0); // Necessário cast
```

**Exemplo com Generics:**
```java
List<String> lista = new ArrayList<>();
lista.add("Texto");
String valor = lista.get(0); // Sem cast, mais seguro
```

---

## 2. Sintaxe Básica

### Classe Genérica
```java
class Caixa<T> {
    private T valor;
    public void setValor(T valor) { this.valor = valor; }
    public T getValor() { return valor; }
}

Caixa<Integer> caixaInt = new Caixa<>();
caixaInt.setValor(10);
System.out.println(caixaInt.getValor()); // 10
```

### Interface Genérica
```java
interface Repositorio<T> {
    void salvar(T entidade);
}

class UsuarioRepositorio implements Repositorio<String> {
    public void salvar(String usuario) {
        System.out.println("Salvando " + usuario);
    }
}
```

### Método Genérico
```java
public static <T> void imprimirArray(T[] array) {
    for (T elemento : array) {
        System.out.println(elemento);
    }
}

String[] nomes = {"Ana", "Pedro"};
imprimirArray(nomes);
```

---

## 3. Generics em Collections

```java
List<String> nomes = new ArrayList<>();
nomes.add("Ana");
nomes.add("Carlos");

for (String nome : nomes) {
    System.out.println(nome.toUpperCase());
}
```

- Sem Generics → risco de erro em runtime.  
- Com Generics → erro detectado em **compile-time**.

---

## 4. Wildcards (`?`)

- `?` → curinga que representa um tipo desconhecido.

### `? extends T` (limite superior)
Aceita **subtipos** de T:
```java
public static void imprimirNumeros(List<? extends Number> lista) {
    for (Number num : lista) {
        System.out.println(num);
    }
}
```

### `? super T` (limite inferior)
Aceita **supertipos** de T:
```java
public static void adicionar(List<? super Integer> lista) {
    lista.add(10);
    lista.add(20);
}
```

---

## 5. Bounded Types

Restrição de tipos usando `extends`:

```java
class Calculadora<T extends Number> {
    public double soma(T a, T b) {
        return a.doubleValue() + b.doubleValue();
    }
}

Calculadora<Integer> calc = new Calculadora<>();
System.out.println(calc.soma(5, 10)); // 15.0
```

Múltiplas restrições:
```java
class Ordenador<T extends Comparable & Serializable> {
    // ...
}
```

---

## 6. Métodos Genéricos

```java
public static <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
}

System.out.println(max(10, 20)); // 20
System.out.println(max("Ana", "Pedro")); // Pedro
```

---

## 7. Boas Práticas e Armadilhas

- **Type Erasure**: o tipo genérico é apagado em runtime.
- Não é possível instanciar tipos genéricos diretamente:
  ```java
  // Caixa<T> caixa = new Caixa<T>(); // ok
  // T valor = new T(); // ERRO
  ```
- Não usar tipos primitivos diretamente (usar wrappers como `Integer`, `Double`).
- Usar nomes significativos (`T`, `E`, `K`, `V`).

---

## 8. Referências

- [Oracle Docs – Generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)  
- [Baeldung – Guide to Generics](https://www.baeldung.com/java-generics)  
- [GeeksforGeeks – Java Generics](https://www.geeksforgeeks.org/generics-in-java/)  

---

> Este guia faz parte do repositório `java-core-concepts`, seção 03-generics.
