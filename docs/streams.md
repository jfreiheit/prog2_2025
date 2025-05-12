# Streams

Die [Java Streams API](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/package-summary.html) ermöglicht die Erzeugung, Manipulation und Verwendung eines "Stroms" von Objekten. Während [Collections]() zum Speichern von Objekten verwendet werden, wird die [Java Streams API](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/package-summary.html) zur Verarbeitung dieser Objekte verwendet, speichert die Objekte selbst jedoch nicht. 

- Ein Stream ist keine Datenstruktur, sondern ein Stream erhält *Input* von Collections, Arrays, Dateien usw.
- Streams verändern nicht die Datenstruktur, aus der sie stammen, sondern erzeugen ein Resultat, indem Operationen *verkettet* werden.
- *Intermediate Operations* erzeugen selbst wieder einen Stream. Dadurch können *intermediate operations* verkettet werden.
- *Terminal Operations* sind am Ende eines Streams und erzeugen das Resultat.

![streams](./files/197_streams.png)

Es gibt also zwei Arten von Operationen in *Streams* 

- *Terminal Operations* und  
- *Intermediate Operations*.

Bevor wir uns die einzelnen Operationen näher anschauen, betrachten wir zunächst einige [Beispiele](https://medium.com/javarevisited/java-interview-12-java-stream-api-programming-tips-for-developers-c3a5e5ddc539), um eine Gefühl für *Streams* zu bekommen:


##### Maximum einer Liste von Zahlen berechnen

```java
List<Integer> age = Arrays.asList(12, 4, 16, 5, 27);

int maxAge = age.stream()
        .mapToInt(Integer::intValue)
        .max()
        .orElse(-1);
System.out.println("Max age is: " + maxAge);	// 27
```


##### Produkt einer Liste von Zahlen berechnen

```java
List<Integer> numList = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
int product = numList.stream()
        .reduce(1, (a, b) -> a * b);
System.out.println("Product: " + product);		// 5040
```


##### Doppelungen in einer Liste von Zahlen entfernen

```java
List<Integer> age = Arrays.asList(12, 22, 12, 27, 31, 45, 31, 31, 51);
List<Integer> distinctAge = age.stream()
        .distinct()
        .collect(Collectors.toList());
System.out.println("Distinct Age List: " + distinctAge);	// [12, 22, 27, 31, 45, 51]
```


##### Summe aller geraden Zahlen aus einer Liste berechnen

```java
List<Integer> numList = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);
int evenSum = numList.stream()
        .filter(n -> n%2 == 0)
        .mapToInt(Integer::intValue)
        .sum();
System.out.println("Sum of even numbers: " + evenSum);		// 20
```


##### Summe und Durchschnitt einer Liste von Zahlen berechnen

```java
List<Integer> numList = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
int sum = numList.stream()
        .mapToInt(Integer::intValue)
        .sum();
double average = numList.stream()
        .mapToDouble(Integer::doubleValue)
        .average()
        .getAsDouble();
System.out.printf("Sum : %d and Average: %f",sum,average);	// 28 and 4.0
```

## Streams erzeugen

#### `stream()`

In allen obigen Beispielen werden die Streams mithilfe von `stream()` erzeugt. Diese Methode wird durch das Interface [Collection](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) zur Verfügung gestellt und lässt sich immer dort anwenden, wo aus einer Collection (`List`, `Set`, `Map`, ...) ein Stream erzeugt werden soll. Ein einfaches Beispiel (sihe aber auch oben) ist

```java
List<String> l1 = List.of("eins", "zwei", "drei", "vier", "fuenf");
Stream<String> s1 = l1.stream();
s1.forEach(System.out::println);		// eins \n zwei \n drei \n vier \n fuenf \n
```

Die Methode `stream()` existiert nicht nur für Collections, sondern auch für [Arrays](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html). Dort ist sie aber eine statische Methode, die ein Array erwartet:

```java
String[] array = {"a", "b", "c"};
Stream<String> stream = Arrays.stream(array);
```

Neben `stream()` gibt es noch weitere Stream-erzeugende Methoden, die wir hier kurz betrachten wollen:


#### `Stream.of()`

Die statische `of()`-Methode aus [Stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) erwartet ein oder mehrere Elemente, die als Stream zurückgegeben werden, z.B.:

```java
Stream<String> s2 = Stream.of("eins", "zwei", "drei", "vier", "fuenf");
s2.forEach(System.out::println);		// eins \n zwei \n drei \n vier \n fuenf \n
```

#### `Stream.generate()`

Die statische `generate()`-Methode aus [Stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) erwartet einen `Supplier` und erzeugt daraus einen **undendlichen** Stream, z.B.:

```java
Random random = new Random();
Stream<Integer> s3 = Stream.generate(random::nextInt);
s3.forEach(System.out::println);     // hoert nicht auf !!!
```

Eine einfache Möglichkeit, die Anzahl der erzeugten Objekte zu begrenzen, ist die Verwendung der Methode `limit(long)` aus [Stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html), z.B.:


```java
Random random = new Random();
Stream<Integer> s3 = Stream.generate(random::nextInt).limit(10);
s3.forEach(System.out::println);     // 10 zufaellig erzeugte int-Werte
```

#### `Stream.iterate()`

Die statische `iterate()`-Methode aus [Stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) erwartet zwei Parameter: einen sogenannten `seed` und eine Funktion `f` (einen [UnaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/UnaryOperator.html) aus `java.util.function`). Die Idee ist, dass iterativ die Funktion `f` auf `seed` angewendet wird, d.h.:

1. `f(seed)`,
2. `f(f(seed))`, 
3. `f(f(f(seed)))`,
4. ...

```java
Stream<Integer> s4 = Stream.iterate(0, n -> n + 2);
s4.forEach(System.out::println);	// hoert nicht auf, gerade positive Zahlen zu erzeugen !!!
```

Auch hier kann z.B. wieder `limit(long)` helfen, um den Stream zu begrenzen:

```java
Stream<Integer> s4 = Stream.iterate(0, n -> n + 2).limit(10);
s4.forEach(System.out::println);	// 0 2 4 6 8 10 12 14 16 18
```


## Intermediate Operations

Wir haben in den Beispielen bereits einige Beispiele für *intermediate operations* gesehen. Folgende Tabelle gibt einen [Überblick](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) über einige der meistverwendeten *intermediate operations*. *Intermediate Operations*

- können miteinander "verkettet" werden,
- erwarten einen *Stream* und erzeugen einen einen *Stream*, d.h. sie transformieren einen *Stream* in einen anderen.


| Operation |Bedeutung |Wirkung |
|-----------|--------------|----|
| `map(Function mapper)` |Wendet auf alle Elemente (Objekte) des Streams die `mapper`-Funktion an. |Ändert die Anzahl der Objekte des Streams nicht. |
| `filter(Predicate predicate)` |Filtert aus einem Stream alle die Objekte, für die `predicate` den Wert `true` hat. |Ändert die Anzahl der Objekte und gibt nur die Objekte als Stream weiter, für die das `predicate` gilt. |
| `sorted(Comparator comparator)` | Sortiert alle Elemente (Objekte) eines Streams wie durch `comparator` vorgegeben. Gibt es auch als `sorted()`, dann wird `Comparable` genutzt.|Anzahl der Objekte bleibt gleich, Ausgabestream sortiert. |
| `distinct()` | Entfernt alle doppelten Elemente (Objekte) aus dem Stream. Doppelungen werden mittels `equals()` erkannt. | Ändert die Anzahl der Objekte, jedes Objekt kommt im Ausgabestream nur noch einmal vor. |
| `peek(Consumer action)` |Wendet eine `action` auf alle Elemente (Objekte) eines Streams an. Im Unterschied zu `map()` werden hier die Elemente nicht verändert. | Ändert die Anzahl der Elemente nicht. |
| `flatMap(Function mapper)` |Wird typischerweise dafür eingesetzt, um aus einem Stream von Collections einen Stream aller Elemente dieser Collections zu erzeugen. | Ändert nicht die Gesamtanzahl der involvierten Objekte. Aus einem Collections-Stream wird eine Elemente-Stream. | 

Wir betrachten die genannten intermediären Operationen an Beispielen, um ein Verständnis darüber zu erlangen:

#### `map(Function mapper)`

Die Methode `map()` erwartet einen Stream und gibt einen Stream mit gleich vielen Elementen weiter, ersetzt jedoch alle eingehenden Elemente unter Anwendung einer Funktion:

!!! question "Was wird ausgegeben?"
	```java
    int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    Arrays.stream(numbers)
            .map(x -> x * x)
            .forEach(System.out::println);
	```


!!! question "Was wird ausgegeben?"
	```java
    List<String> words = List.of("eins", "zwei", "drei", "vier", "fuenf");
    words.stream()
            .map(x -> x.toUpperCase())
            .forEach(System.out::println);
	```



!!! question "Was wird ausgegeben?"
	```java
    List<String> words = List.of("abc", "a", "abcd", "abcde", "ab");
    words.stream()
            .map(x -> x.length())
            .sorted()
            .forEach(System.out::println);
	```



!!! question "Was wird ausgegeben? - Beachten Sie die Reihenfolge der Ausgaben!"
	```java
    public record Rectangle(int width, int length)
    {
        public int area()
        {
            return this.width * this.length;
        }
    }
    Set<Rectangle> rectangles = new HashSet<>();
    rectangles.add(new Rectangle(1, 2));
    rectangles.add(new Rectangle(3, 2));
    rectangles.add(new Rectangle(1, 4));
    rectangles.add(new Rectangle(3, 4));
    rectangles.add(new Rectangle(2, 5));
    rectangles.add(new Rectangle(4, 2));
    rectangles.stream()
            .peek(s -> System.out.println(s.length() + " x " + s.width() + " = " + s.area()))
            .map(x -> x.area())
            .peek(r -> System.out.println(r))
            .filter(x -> x < 5)
            .forEach(System.out::println);
	```


#### `filter(Predicate predicate)`

Die Methode `filter()` erwartet einen Stream und gibt einen Stream weiter, lässt jedoch nur die Elemente durch, für die das `predicate` den Wert `true` ergibt. Die Elemente selbst bleiben unverändert:


!!! question "Was wird ausgegeben?"
	```java
    int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    Arrays.stream(numbers)
            .filter(x -> x %2 == 0)
            .forEach(System.out::println);
	```


!!! question "Was wird ausgegeben?"
	```java
    List<String> l1 = List.of("abc", "a", "abcd", "abcde", "ab");
    l1.stream()
            .filter(x -> x.length() < 3)
            .forEach(System.out::println);
	```


!!! question "Was wird ausgegeben?"
	```java
    Stream<String> s2 = Stream.of("eins", "zwei", "drei", "vier", "fuenf");
    s2.filter(x -> x.contains("ei"))
      .forEach(System.out::println);
	```


#### `sorted(Comparator comparator)`

Es gibt auch eine Methode `sorted()`. Diese kann auf Klassen angewendet werden, die das [Comparable](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)-Interface implementiert haben (z.B. String, alle Wrapper-Klassen usw.). Es wird die `compareTo()`-Methode verwendet, um die Elemente zu sortieren. Mit der Methode `sorted(Comparator comparator)` kann ein eigener [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html) implementiert werden. Dabei handelt es sich um ein *Functional Interface* mit der *SAM* `int compare(T o1, T o2)`.

Es gibt verschiedene Möglichkeiten, [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html) anzuwenden. Eine ist, die statischen Methoden des Interfaces zu verwenden, z.B. `Comparator.comparingInt(ToIntFunction keyExtractor)` (es gibt auch `comparingDouble(), ComparingLong()`):


!!! question "Was wird ausgegeben? - Beachten Sie die Reihenfolge der Ausgaben!"
	```java
    public record Rectangle(int width, int length)
    {
        public int area()
        {
            return this.width * this.length;
        }
    }
    Set<Rectangle> rectangles = new HashSet<>();
    rectangles.add(new Rectangle(1, 2));
    rectangles.add(new Rectangle(3, 2));
    rectangles.add(new Rectangle(1, 4));
    rectangles.add(new Rectangle(3, 4));
    rectangles.add(new Rectangle(2, 5));
    rectangles.add(new Rectangle(4, 2));
    rectangles.stream()
                .sorted(Comparator.comparingInt(Rectangle::area))
                .forEach(System.out::println);
	```


