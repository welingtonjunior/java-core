# Guia de I/O e Manipulação de Arquivos em Java

Este guia tem como objetivo apresentar os principais conceitos e práticas de **I/O (Input/Output)** e **manipulação de arquivos** em Java.  

---

## 📌 1. Introdução ao I/O em Java

O Java fornece APIs para **entrada** (Input) e **saída** (Output) de dados, que podem ser usados para:
- Ler e escrever em arquivos.
- Ler e escrever no console.
- Manipular fluxos de dados (streams).

Principais pacotes utilizados:
- `java.io`
- `java.nio.file`

---

## 📌 2. Tipos de Streams

- **Byte Streams (`InputStream`, `OutputStream`)**
  - Manipulam dados em formato binário.
  - Ex.: leitura de imagens, vídeos, áudios.

- **Character Streams (`Reader`, `Writer`)**
  - Manipulam dados em formato de caracteres (texto).
  - Ex.: leitura e escrita de arquivos `.txt`.

---

## 📌 3. Leitura de Arquivos

### 🔹 Usando `FileReader` e `BufferedReader`
```java
import java.io.*;

public class LeituraArquivo {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("exemplo.txt"))) {
            String linha;
            while ((linha = br.readLine()) != null) {
                System.out.println(linha);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 🔹 Usando `Files.readAllLines` (Java 8+)
```java
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class LeituraNIO {
    public static void main(String[] args) throws IOException {
        List<String> linhas = Files.readAllLines(Paths.get("exemplo.txt"));
        linhas.forEach(System.out::println);
    }
}
```

---

## 📌 4. Escrita em Arquivos

### 🔹 Usando `FileWriter` e `BufferedWriter`
```java
import java.io.*;

public class EscritaArquivo {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("saida.txt"))) {
            bw.write("Primeira linha");
            bw.newLine();
            bw.write("Segunda linha");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 🔹 Usando `Files.write` (Java 8+)
```java
import java.nio.file.*;
import java.io.IOException;
import java.util.Arrays;

public class EscritaNIO {
    public static void main(String[] args) throws IOException {
        Path path = Paths.get("saida.txt");
        Files.write(path, Arrays.asList("Linha 1", "Linha 2"));
    }
}
```

---

## 📌 5. Manipulação de Arquivos com `File`

```java
import java.io.File;

public class ManipulacaoArquivo {
    public static void main(String[] args) {
        File arquivo = new File("exemplo.txt");

        if (arquivo.exists()) {
            System.out.println("Nome: " + arquivo.getName());
            System.out.println("Caminho: " + arquivo.getAbsolutePath());
            System.out.println("Pode ser lido? " + arquivo.canRead());
            System.out.println("Tamanho: " + arquivo.length() + " bytes");
        } else {
            System.out.println("Arquivo não encontrado.");
        }
    }
}
```

---

## 📌 6. Conclusão

- `java.io` é mais tradicional, mas poderoso.  
- `java.nio.file` é mais moderno e simplifica operações comuns.  
- Sempre feche os recursos ou use **try-with-resources**.  

👉 Este guia cobre os fundamentos para leitura, escrita e manipulação de arquivos em Java.
