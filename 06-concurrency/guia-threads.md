# Guia de Concorrência em Java

Este guia apresenta os conceitos fundamentais de **concorrência e threads em Java**, desde o básico até o uso de APIs mais modernas.

---

## 📌 1. O que é Concorrência?

Concorrência permite que várias tarefas sejam executadas de forma **simultânea** ou **paralela**, aproveitando melhor os recursos do sistema.

Exemplos de uso:
- Processar múltiplas requisições de usuários em um servidor.
- Ler e escrever arquivos enquanto processa dados.
- Melhorar desempenho em máquinas com múltiplos núcleos.

---

## 📌 2. Criando Threads

### 🔹 Estendendo a classe `Thread`
```java
class MinhaThread extends Thread {
    public void run() {
        System.out.println("Thread em execução: " + Thread.currentThread().getName());
    }

    public static void main(String[] args) {
        MinhaThread t1 = new MinhaThread();
        t1.start(); // Inicia a execução
    }
}
```

### 🔹 Implementando `Runnable`
```java
class MinhaRunnable implements Runnable {
    public void run() {
        System.out.println("Thread em execução: " + Thread.currentThread().getName());
    }

    public static void main(String[] args) {
        Thread t1 = new Thread(new MinhaRunnable());
        t1.start();
    }
}
```

---

## 📌 3. Controle de Threads

- **`sleep(ms)`** → pausa a execução.
- **`join()`** → aguarda outra thread terminar.
- **`setPriority()`** → define prioridade (não garante ordem).
- **`isAlive()`** → verifica se a thread ainda está em execução.

Exemplo:
```java
public class ControleThread {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("Execução " + i);
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            }
        });
        t1.start();
        t1.join(); // Espera t1 finalizar
        System.out.println("Thread finalizada!");
    }
}
```

---

## 📌 4. Problemas de Concorrência

Quando múltiplas threads acessam recursos compartilhados, podem ocorrer problemas como:
- **Condição de corrida** (race condition).
- **Inconsistência de dados**.
- **Deadlocks**.

---

## 📌 5. Sincronização

### 🔹 Usando `synchronized`
```java
class Contador {
    private int valor = 0;

    public synchronized void incrementar() {
        valor++;
    }

    public int getValor() {
        return valor;
    }
}

public class TesteSync {
    public static void main(String[] args) throws InterruptedException {
        Contador contador = new Contador();

        Runnable tarefa = () -> {
            for (int i = 0; i < 1000; i++) contador.incrementar();
        };

        Thread t1 = new Thread(tarefa);
        Thread t2 = new Thread(tarefa);
        t1.start(); t2.start();
        t1.join(); t2.join();

        System.out.println("Valor final: " + contador.getValor());
    }
}
```

---

## 📌 6. Concorrência com `ExecutorService`

O `ExecutorService` gerencia pools de threads automaticamente.

```java
import java.util.concurrent.*;

public class ExemploExecutor {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Future<Integer> resultado = executor.submit(() -> {
            return 42;
        });

        System.out.println("Resultado: " + resultado.get());
        executor.shutdown();
    }
}
```

---

## 📌 7. Classes Avançadas de Concorrência (pacote `java.util.concurrent`)

- **`ExecutorService`** → gerenciamento de threads.
- **`Future` e `Callable`** → resultados assíncronos.
- **`ScheduledExecutorService`** → agendamento de tarefas.
- **`ConcurrentHashMap`** → mapa thread-safe.
- **`CountDownLatch`, `Semaphore`, `CyclicBarrier`** → coordenação de threads.

---

## 📌 8. Conclusão

- Use `Thread` e `Runnable` para aprender o básico.  
- Prefira **Executors e APIs de alto nível** para projetos reais.  
- Sincronize recursos compartilhados para evitar erros de concorrência.  

👉 Dominar concorrência é essencial para aplicações performáticas e escaláveis.
