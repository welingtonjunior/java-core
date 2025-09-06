# 🗃️ Guia Completo: Collections Framework em Java

## Índice
1. Visão Geral
2. Hierarquia das Interfaces
3. Listas
4. Conjuntos
5. Mapas
6. Coleções Ordenadas
7. Coleções Thread-Safe
8. Algoritmos Úteis
9. Exemplos Práticos

---

## Visão Geral

O Collections Framework é uma arquitetura unificada para representar e manipular coleções de objetos em Java. Fornece:

- **Interfaces**: Tipos abstratos que representam coleções
- **Implementações**: Classes concretas das interfaces
- **Algoritmos**: Métodos estáticos para operações comuns (busca, ordenação)

Principais vantagens:

- Reduz esforço de programação
- Aumenta qualidade e performance
- Promove reuso de código
- Fornece interoperabilidade

## Hierarquia das Interfaces

\`\`\`
Collection
├── List
├── Set
│   ├── SortedSet
│   └── NavigableSet
└── Queue
    └── Deque

Map
├── SortedMap
└── NavigableMap
\`\`\`

## Listas

Características:

- Mantêm ordem de inserção
- Permitem elementos duplicados
- Acesso por índice

### ArrayList

\`\`\`java
List<String> arrayList = new ArrayList<>();
arrayList.add("Elemento A");
arrayList.add(0, "Elemento B");
String elemento = arrayList.get(0);
arrayList.remove(0);
arrayList.remove("Elemento A");

for (String elemento : arrayList) {
    System.out.println(elemento);
}

arrayList.forEach(elemento -> System.out.println(elemento));
\`\`\`

### LinkedList

\`\`\`java
List<String> linkedList = new LinkedList<>();
LinkedList<String> linkedListEspecifica = (LinkedList<String>) linkedList;
linkedListEspecifica.addFirst("Primeiro");
linkedListEspecifica.addLast("Último");
String primeiro = linkedListEspecifica.getFirst();
String ultimo = linkedListEspecifica.getLast();
\`\`\`

### Vector vs ArrayList

| Característica | Vector | ArrayList |
|----------------|--------|-----------|
| Sincronizado   | Sim    | Não       |
| Performance    | Mais lento | Mais rápido |
| Crescimento    | Dobra o tamanho | Aumenta 50% |

## Conjuntos

Características:

- Não permitem elementos duplicados
- No máximo um elemento null

### HashSet

\`\`\`java
Set<String> hashSet = new HashSet<>();
hashSet.add("A");
hashSet.add("B");
hashSet.add("A"); // Não será adicionado
System.out.println(hashSet.contains("A")); // true
\`\`\`

### LinkedHashSet

\`\`\`java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("B");
linkedHashSet.add("A");
linkedHashSet.add("C");
linkedHashSet.forEach(System.out::println);
\`\`\`

### TreeSet

\`\`\`java
Set<String> treeSet = new TreeSet<>();
treeSet.add("C");
treeSet.add("A");
treeSet.add("B");
treeSet.forEach(System.out::println);

Set<String> treeSetReverso = new TreeSet<>(Comparator.reverseOrder());
treeSetReverso.addAll(Arrays.asList("A", "B", "C"));
\`\`\`

## Mapas

Características:

- Armazenam pares chave-valor
- Chaves únicas
- Valores podem ser duplicados

### HashMap

\`\`\`java
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("Alice", 25);
hashMap.put("Bob", 30);
hashMap.put("Charlie", 35);
int idade = hashMap.get("Alice");
boolean contem = hashMap.containsKey("Bob");

for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

hashMap.forEach((chave, valor) -> 
    System.out.println(chave + ": " + valor));
\`\`\`

### LinkedHashMap

\`\`\`java
Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
linkedHashMap.put("Zoe", 40);
linkedHashMap.put("Alice", 25);
linkedHashMap.put("Bob", 30);
\`\`\`

### TreeMap

\`\`\`java
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Zoe", 40);
treeMap.put("Alice", 25);
treeMap.put("Bob", 30);
\`\`\`

### ConcurrentHashMap

\`\`\`java
Map<String, Integer> concurrentMap = new ConcurrentHashMap<>();
concurrentMap.put("Key", 100);
concurrentMap.computeIfAbsent("NewKey", k -> 42);
concurrentMap.computeIfPresent("Key", (k, v) -> v + 1);
\`\`\`

## Coleções Ordenadas

### Comparable vs Comparator

\`\`\`java
class Pessoa implements Comparable<Pessoa> {
    private String nome;
    private int idade;
    
    @Override
    public int compareTo(Pessoa outra) {
        return this.nome.compareTo(outra.nome);
    }
}

List<Pessoa> pessoas = new ArrayList<>();
Collections.sort(pessoas);
\`\`\`

Comparator:

\`\`\`java
Comparator<Pessoa> porIdade = Comparator.comparingInt(Pessoa::getIdade);
Comparator<Pessoa> porNomeReverso = Comparator.comparing(Pessoa::getNome).reversed();
Comparator<Pessoa> multiplos = Comparator.comparing(Pessoa::getNome)
                                        .thenComparingInt(Pessoa::getIdade);
Collections.sort(pessoas, porIdade);
\`\`\`

## Coleções Thread-Safe

\`\`\`java
List<String> listaSync = Collections.synchronizedList(new ArrayList<>());
Set<String> setSync = Collections.synchronizedSet(new HashSet<>());
Map<String, Integer> mapSync = Collections.synchronizedMap(new HashMap<>());

synchronized(listaSync) {
    Iterator<String> it = listaSync.iterator();
    while (it.hasNext()) {
        System.out.println(it.next());
    }
}

List<String> copyOnWriteList = new CopyOnWriteArrayList<>();
ConcurrentHashMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();
concurrentMap.putIfAbsent("key", 100);
concurrentMap.replace("key", 100, 200);
concurrentMap.compute("key", (k, v) -> v + 50);
\`\`\`

## Algoritmos Úteis

\`\`\`java
List<Integer> numeros = Arrays.asList(3, 1, 4, 1, 5, 9);
Collections.sort(numeros);
Collections.sort(numeros, Collections.reverseOrder());
int posicao = Collections.binarySearch(numeros, 4);
Collections.shuffle(numeros);
Collections.fill(numeros, 0);
Integer min = Collections.min(numeros);
Integer max = Collections.max(numeros);
List<Integer> imutavel = Collections.unmodifiableList(numeros);
\`\`\`

### Stream API

\`\`\`java
List<String> nomes = Arrays.asList("Ana", "Bruno", "Carlos", "Daniel");
List<String> comA = nomes.stream()
    .filter(n -> n.startsWith("A"))
    .collect(Collectors.toList());

List<Integer> tamanhos = nomes.stream()
    .map(String::length)
    .collect(Collectors.toList());

List<String> ordenados = nomes.stream()
    .sorted()
    .collect(Collectors.toList());

Map<Integer, List<String>> porTamanho = nomes.stream()
    .collect(Collectors.groupingBy(String::length));
\`\`\`

## Exemplos Práticos

### Cache com LinkedHashMap

\`\`\`java
class SimpleCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;
    
    public SimpleCache(int capacity) {
        super(capacity, 0.75f, true);
        this.capacity = capacity;
    }
    
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
}

SimpleCache<String, Integer> cache = new SimpleCache<>(3);
cache.put("A", 1);
cache.put("B", 2);
cache.put("C", 3);
cache.put("D", 4);
\`\`\`

### Estatísticas com Streams

\`\`\`java
List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
IntSummaryStatistics stats = numbers.stream()
    .mapToInt(Integer::intValue)
    .summaryStatistics();

System.out.println("Máximo: " + stats.getMax());
System.out.println("Mínimo: " + stats.getMin());
System.out.println("Média: " + stats.getAverage());
System.out.println("Soma: " + stats.getSum());
System.out.println("Contagem: " + stats.getCount());
\`\`\`

### Transformação entre Coleções

\`\`\`java
List<String> listaComDuplicatas = Arrays.asList("A", "B", "A", "C");
Set<String> setSemDuplicatas = new HashSet<>(listaComDuplicatas);
String[] array = {"A", "B", "C"};
List<String> lista = Arrays.asList(array);

Map<String, Integer> mapa = new HashMap<>();
mapa.put("A", 1);
mapa.put("B", 2);
List<String> chaves = new ArrayList<>(mapa.keySet());
List<Integer> valores = new ArrayList<>(mapa.values());
\`\`\`

## Boas Práticas

1. Prefira declarar usando interfaces:
\`\`\`java
List<String> lista = new ArrayList<>();
\`\`\`
2. Considere capacidade inicial para grandes coleções
3. Use Collections.emptyList() para listas vazias
4. Prefira foreach para iterações simples
5. Use ConcurrentHashMap para acesso concorrente

## Recursos Adicionais

- Java Collections Framework (Oracle Docs)
- Java Collections Tutorial (Baeldung)
- Java Concurrency in Practice

