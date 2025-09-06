# Guia de Orientação a Objetos em Java

Este guia apresenta os conceitos fundamentais de **Orientação a Objetos
(OO)** em Java.

------------------------------------------------------------------------

## 1. Classes e Objetos

-   **Classe**: modelo ou molde de um objeto.\
-   **Objeto**: instância da classe.

``` java
public class Pessoa {
    String nome;
    int idade;

    // Construtor
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }

    // Método
    public void apresentar() {
        System.out.println("Olá, meu nome é " + nome + " e tenho " + idade + " anos.");
    }
}

// Criando objetos
Pessoa p1 = new Pessoa("Ana", 25);
p1.apresentar(); // Olá, meu nome é Ana e tenho 25 anos.
```

------------------------------------------------------------------------

## 2. Encapsulamento

-   Princípio que protege os dados, controlando acesso a atributos.\
-   Usa **modificadores de acesso** (`private`, `public`, `protected`).\
-   Métodos getters e setters permitem acessar/alterar valores de forma
    segura.

``` java
public class Conta {
    private double saldo;

    public double getSaldo() {
        return saldo;
    }

    public void depositar(double valor) {
        if(valor > 0) saldo += valor;
    }
}
```

------------------------------------------------------------------------

## 3. Herança

-   Permite que uma classe **herde atributos e métodos** de outra.\
-   Usa a palavra-chave `extends`.

``` java
public class Animal {
    public void comer() {
        System.out.println("Comendo...");
    }
}

public class Cachorro extends Animal {
    public void latir() {
        System.out.println("Au Au!");
    }
}

Cachorro dog = new Cachorro();
dog.comer(); // Herdado da classe Animal
dog.latir();
```

### Observação

-   Java suporta **herança simples**, ou seja, uma classe só pode
    estender **uma outra classe**.

------------------------------------------------------------------------

## 4. Polimorfismo

-   Capacidade de **um objeto se comportar de diferentes formas**.\
-   Tipos:
    -   **Sobrescrita de métodos (Override)**
    -   **Sobrecarga de métodos (Overload)**

``` java
// Sobrecarga
public int soma(int a, int b) { return a + b; }
public double soma(double a, double b) { return a + b; }

// Sobrescrita
@Override
public void apresentar() {
    System.out.println("Apresentação personalizada");
}
```

------------------------------------------------------------------------

## 5. Abstração

-   Classes abstratas não podem ser instanciadas diretamente.\
-   Podem conter métodos abstratos (sem implementação) e concretos.

``` java
public abstract class Forma {
    public abstract double area();
}

public class Circulo extends Forma {
    private double raio;
    public Circulo(double raio) { this.raio = raio; }
    public double area() { return Math.PI * raio * raio; }
}
```

------------------------------------------------------------------------

## 6. Interfaces

-   Define **contratos** que classes devem seguir.\
-   Permite **herança múltipla** de comportamento.

``` java
public interface Voar {
    void voar();
}

public class Passaro implements Voar {
    public void voar() {
        System.out.println("O pássaro está voando");
    }
}
```

------------------------------------------------------------------------

## 7. Resumo Rápido

1.  **Classe** = molde; **Objeto** = instância.\
2.  **Encapsulamento** protege atributos com `private` +
    getters/setters.\
3.  **Herança** (`extends`) permite reutilização de código.\
4.  **Polimorfismo** = mesma assinatura, comportamentos diferentes.\
5.  **Abstração** (`abstract`) esconde detalhes e define contratos.\
6.  **Interfaces** permitem múltiplos comportamentos sem herança
    múltipla de classes.

------------------------------------------------------------------------
