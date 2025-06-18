# Generics

Ein *generischer Typ* (*generic type*) ist eine Klasse oder ein Interface, die mit einem oder mehreren Typen *parametrisiert* ist. Wir kennen die Anwendung von *Generics* bereits aus Collections. So sind z.B. die Typen `List` und `Set` mit dem generischen Typen `E` parametrisiert. Generell gilt also `List<E>` und `Set<E>`, wobei `E` für einen beliebigen (Referenz-)Typen für die Elemente in der Liste bzw. der Menge stehen. Den konkreten Typ der Elemente gibt man dann bei der Deklaration an:

```java
List<String> words = new ArrayList<>();		// Liste, die Strings enthaelt
Set<Integer> numbers = new HashSet<>(); 	// menge, die Integer enthaelt
```

Wir zeigen hier nun, wie wir uns eine eigene generische Klasse schreiben können:

=== "MyGenericClass<T>.java"
	```java
	public class MyGenericClass<T>
	{
	    T value;

	    public MyGenericClass(T value)
	    {
	        this.value = value;
	    }

	    public T getValue()
	    {
	        return value;
	    }
	}
	```

Wir parametrisieren im Klassenkopf die Klasse `MyGenericClass` einfach mittels `<T>` mit einem Typen und verwenden diesen Platzhalter `T` überall dort, wo der Typ verwendet wird, z.B. bei der Deklaration der Objektvariablen `value`, beim Parameter im Konstruktor und beim Rückgabetyp des Getters.

Bei der Objekterzeugung kann nun jeder beliebige (Referenz-)Typ anstelle von `T` gesetzt werden. Dazu typisieren wir:

```java
MyGenericClass<String> testMitString = new MyGenericClass<>("Hallo");
System.out.println(testMitString.getValue());

MyGenericClass<Integer> testMitInteger = new MyGenericClass<>(42);
System.out.println(testMitInteger.getValue());
```

Zur Typisierung kann jeder beliebige Referenztyp, also auch `Konto`, `Rectangle`, `Person`, `Student` usw. verwendet werden, nicht aber Wertetypen. Beachten Sie, dass wenn wir unsere Klasse mit `String` typisieren, dann muss im Konstruktor auch ein `String` übergeben werden und wenn `Integer` dann dort auch ein `Integer`. Andernfalls lässt sich das Programm nicht übersetzen. Eine Klasse (bzw. ein Interface) kann mit beliebig vielen generischen Typen parametrisiert werden. 

Welche Bezeichnungen Sie für die generischen Typen verwenden, bleibt Ihnen überlassen. Könnte z.B. auch `Hallo` sein. es gibt aber Konventionen, an die Sie sich ruhig halten sollten:

| Platzhalter | Bedeutung |
|-------------|----------------|
| `E` | Element |
| `K` | Key | 
| `N` | Number |
| `T` | Type |
| `V` | Value | 
| `S`, `U` | 2. und 3. Typ |

Manchmal werden an die generischen Typen spezielle Anforderungen gestellt. Angenommen, wir wollen die Klasse `MyGenericClass<T>` um folgende Methode erweitern:

	```java linenums="18"
    public boolean isBigger(MyGenericClass<T> other)
    {
        return this.value.compareTo(other.value) > 0;
    }
	```

Dann bräuchten wir die Zusicherung, dass der Typ `T` auch `Comparable` implementiert hat, denn sonst könnten wir `compareTo()` gar nicht aufrufen. Eine solche Zusicherung lässt sich mittels `<T extends Comparable<T>>` beschreiben: 


=== "MyGenericClass<T extends Comparable<T>>.java"
	```java
	public class MyGenericClass<T extends Comparable<T>>
	{
	    T value;

	    public MyGenericClass(T value)
	    {
	        this.value = value;
	    }

	    public T getValue()
	    {
	        return value;
	    }

	    public boolean isBigger(MyGenericClass<T> other)
	    {
	        return this.value.compareTo(other.value) > 0;
	    }
	}
	```


## Beispiel einfaches Interface

Angenommen, wir haben folgendes einfaches funktionales Interface:

=== "Addable.java"
	```java
	@FunctionalInterface
	public interface Addable<T, R>
	{
	    public R add(T t1, T t2);
	}
	```

Dann könnten wir uns beliebige Methoden schreiben, die ein `Addable` erwarten, z.B.

```java
public static String concat(Addable<String, String> addable, String first, String second)
{
    return addable.add(first, second);
}

public static Integer add(Addable<Integer, Integer> addable, Integer first, Integer second)
{
    return addable.add(first, second);
}

public static List<Integer> insert(Addable<Integer, List<Integer>> addable, Integer first, Integer second)
{
    return addable.add(first, second);
}
```

und bei Aufruf der Methoden jeweils mithilfe von Lambdas die Implementierung von `R add(T t1, T t2)` angeben:

```java
System.out.println(concat( (s1, s2) -> s1 + s2, "Hallo ", "FIW!"));
System.out.println(add( (s1, s2) -> s1 + s2, 3, 4));
System.out.println(insert( (s1, s2) -> List.of(s1, s2), 3, 4));
```

??? question "Wie könnte das Zusammenfügen zweier Sets aussehen?"
	```java
    public static Set<String> addAll(Addable<Set<String>, Set<String>> addable, Set<String> first, Set<String> second)
    {
        return addable.add(first, second);
    }

    System.out.println(addAll( (s1, s2) -> {
        Set<String> all = new HashSet<>(s1);
        all.addAll(s2);
        return all;
    }, new HashSet<>(List.of("A", "B", "C", "D")), new HashSet<>(List.of("C", "D", "E", "F"))));
	```


## Eine generische Sortiermethode

Wir haben uns im ersten Semester verschiedene Sortiermethoden für Arrays unterschiedlichen Typs geschrieben. Eine generische Methode könnte wie folgt aussehen:

```java
public static <T extends Comparable<T>> void bubbleSort(T[] array) {
for (int bubble = 1; bubble < array.length; bubble++) {
  for (int index = 0; index < array.length - bubble; index++) {
    if (array[index].compareTo(array[index + 1]) > 0) {
      swap(index, index + 1, array);
    }
  }
}
}

public static <T> void swap(int i, int j, T[] a) {
	T t = a[i];
	a[i] = a[j];
	a[j] = t;
}
```

Diese Methode stellt 2 Anforderungen:

- der Typ des Arrays ist ein Referenztyp (üfr Wertetypen müssen entsprechende Wrapperklassen verwendet werden),
- der Typ des Arrays implementiert das Interface `Comparable`. Wird ein Typ verwendet, der nicht `Comparable` implementiert hat, erhalten wir eine `ClassCastException`. 


## Wildcards

Ein Typ kann mit der Wildcard `?` angegeben werden, dann ist jeder beliebige (Referenz-)Typ möglich. Beispiel:

```java
List<?> list = new ArrayList<String>();
list = new ArrayList<Integer>(); // Works with any type
```

Eine solche Wildcard wird jedoch meistens nicht wie oben, sondern entweder als *Upper-Bounded-Wildcard*  oder als *Lower-Bounded-Wildcard*. Mit der **PECS**-Eselsbrücke kann man sich merken, ob `extends` (*Upper-Bounded-Wildcard*) oder `super` (*Lower-Bounded-Wildcard*) verwendet werden soll. **PECS** steht für *Producer-Extends, Consumer-Super*.

### Upper-Bounded-Wildcard

```java
public void printNumbers(List<? extends Number> list) {
    for (Number n : list) {
        System.out.println(n);
    }
}
```

Es wird eine Liste erwartet, deren Typ mindestens von `Number` abgeleitet wurde (also z.B. `Interger`, `Double`, `Long`). `String` oder `Boolean` ginge z.B. nicht. Die Liste *produziert* die Input-Werte.

### Lower-Bounded-Wildcard

```java
public void addNumbers(List<? super Integer> list) {
    list.add(10); // You can add Integer or its subclass
}
```



