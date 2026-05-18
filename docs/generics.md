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


## Die PECS-Regel

**PECS** steht für <strong>P</strong>roducer <strong>E</strong>xtends, <strong>C</strong>onsumer <strong>S</strong>uper. Um diese Regel zu verstehen, führen wir zunächst zwei Begriffe ein: *Invarianz* und *Kovarianz*. 

> Kovarianz: Wenn `A` eine Kindklasse von `B` ist, dann ist `T(A)` auch eine Kindklasse von `T(B)`. Beispiel: `Interger` ist eine Kindklasse von `Number`. `Integer[]` ist eine Kindklasse von `Number[]`. Es ginge also `Number[] array = new Integer[5]`.

Das Problem dabei:

```java
Number[] numbers = new Integer[5];	// erlaubt Kovarianz
numbers[0] = 3.14;					// ArrayStoreException!!!
```

Deshalb hat man *Generics* invariant gemacht:

> Invarianz: Eine Klasse (Typ) ist invariant, wenn sie keine Kindklassen-Beziehung der zugrundeliegenden Klassen (Typen) übernimmt bzw. zulässt. Beispiel: `List<Integer>` ist **keine** `List<Number>`! 

Arrays sind kovariant, Generics nicht! Angenommen, wir haben eine Methode 

```java
public static double summe(List<Number> liste) 
{
    double sum = 0.0;
    for (Number n : liste) 
    {
        sum += n.doubleValue();
    }
    return sum;
}
```

, die eine `List<Number>` erwartet. Dann können wir **nicht**:

```java
List<Integer> numbers2 = List.of(1, 2, 3, 4, 5);
System.out.println(summe(numbers2));				// Compilerfehler!!!
```

Eine `List<Integer>` ist **keine** `List<Number>`, denn `List<T>` ist eine Generic und somit invariant.

Wir müssen stattdessen so implementieren:

```java
public static double summe(List<? extends Number> liste) 
{
    double sum = 0.0;
    for (Number n : liste) 
    {
        sum += n.doubleValue();
    }
    return sum;
}
```

Beim `?` spricht man von einer *Wildcard*. Bei `? extends Number` spricht man von einer `Upper-Bounded-Wildcard`.

Nun funktioniert `summe(numbers2)`! Mithilfe von `<? extends Number>` erzwingen wir *Kovarianz*. `<? extends Number>` besagt: *Diese Methode akzeptiert eine Liste von Objekten irgendeines Typs, solange dieser Typ `Number` ist oder von `Number` erbt.* 

**Aber Achtung!** Weil der Compiler nicht genau weiß, welcher Typ *konkret* in der Liste steckt, ist das Hinzufügen von Elementen so nicht erlaubt!

```java
public static void add(List<? extends Number> liste, Number element)
{
	liste.add(element);	// Compilerfehler!!! 
}
```

Es könnte ja sein, dass die Liste vom Typ `List<Integer>` ist, das `element` jedoch vom Typ `Double`. Hier kommt die **PECS**-Regel zur Anwendung. Während die Liste in `summe` ein *Producer* ist (wir lesen nur Werte aus, Werte werden geliefert), ist die Liste in `add` ein *Consumer* (wir schreiben Werte, nehmen Werte auf). 


```java
public static void add(List<? extends Number> liste, Number element)
{
	liste.add(element);	funktioniert nun 
}
```

Der Ausdruck `<? super Number>` bedeutet, dass die Liste Objekte von Typ `Number` oder einer ihrer Elternklassen (wie `Object`) aufnehmen kann. Man spricht von einer `Lower-Bounded-Wildcard`. Da jede Zahl (egal ob `Integer` oder `Double`) strukturell eine `Number` ist, ist es absolut sicher, jedes Objekt vom Typ `Number` in diese Liste einzufügen. Dafür kann man nun keine `List<Integer>` mehr als Parameter übergeben! 

```java
List<Integer> numbers2 = List.of(1, 2, 3, 4, 5);
System.out.println(summe(numbers2));
//add(numbers2, 6); 	// Compilerfehler!!!
List<Number> numbers3 = new ArrayList<>(numbers2);
add(numbers3, 6);		// klappt! List<Object> ginge auch
for(Number i : numbers3)
{
	System.out.print(i + " ");
}
```

beachten Sie auch, dass innerhalb der `add`-Methode z.B. nicht `Number n = liste.get(0)` aufgerufen werden könnte, da die Liste ja auch eine `List<Object>` sein könnte und ein `Object` keine `Number` ist.
	

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
public static <T extends Comparable<T>> void bubbleSort(T[] array) 
{
	for (int bubble = 1; bubble < array.length; bubble++) 
	{
	  for (int index = 0; index < array.length - bubble; index++) 
	  {
	    if (array[index].compareTo(array[index + 1]) > 0) 
	    {
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

- der Typ des Arrays ist ein Referenztyp (für Wertetypen müssen entsprechende Wrapperklassen verwendet werden),
- der Typ des Arrays implementiert das Interface `Comparable`. Wird ein Typ verwendet, der nicht `Comparable` implementiert hat, erhalten wir eine `ClassCastException`. 




