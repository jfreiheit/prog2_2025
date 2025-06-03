# Optionals

Ein [Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) kann man sich wie einen Container vorstellen, der eigentlich dafür da ist, einen Wert zu speichern, jedoch eventuell leer ist (keinen Wert hat). [Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) wurde eingeführt, um `NullPointerException`s zu vermeiden. Wir hatten bereits genügend Beispiele, in denen wir `null` zurückgeben mussten, falls kein geeigneter Wert für die Rückgabe existierte. Dies sollten wir jedoch dringend vermeiden, um der aufrufenden Methode eine mögliche `NullPointerException` zu ersparen. Mit dem Werfen geeigneter Exceptions lässt sich dieses Problem zwar bereits lösen, jedoch ist dann der Aufruf der Methode in einen `try-Catch`-Block erforderlich, was zu unschönem Code führt. Zudem sind solche Exceptions meistens `unchecked` und führen unbehandelt dann trotzdem zu einem Laufzeitfehler. 

Der Haupteinsatzzweck von [Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) ist als Methodenrückgabe, wobei durch die Verwendung von `Optional` sichergestellt wird, dass es möglich ist, dass **kein** Wert zurückgegeben wird. 

Angenommen, wir haben folgenden Code:

```java linenums="1"
Map<String, String> studiengänge = new HashMap<>();
studiengänge.put("fiw", "Informatik und Wirtschaft");
studiengänge.put("ai", "Angewandte Informatik");
studiengänge.put("imi", "Internationale Medieninformatik");
studiengänge.put("ikg", "Informatik, Kultur und Gesundheit");
System.out.println(studiengänge.get("ai").toUpperCase());
System.out.println(studiengänge.get("wi").toUpperCase());
```

Dann würde in Zeile `7` eine `NullPointerException` geworfen, das die `get(key)`-Methode aus `Map` eine `null` zurückgibt, falls der Schlüssel `key` nicht in der `Map` existiert. Prinzipiell müsste deshalb die `get()`-Methode aus `Map` entweder in einen `try-catch`-Block eingebettet oder vorab die `containsKey(key)`-Methode aufgerufen werden. 

Der folgende Code zeigt eine mögliche Implementierung für das Auslesen eines Wertes aus einer `Map` unter Verwendung von `Optional<T>`:


```java linenums="1"
public static Optional<String> getValue(Map<String, String> sgs, String key) {
    if (sgs.containsKey(key))
    {
        return Optional.of(sgs.get(key));
    }
    return Optional.empty();
}
```

Zunächst wird geprüft, ob der Schlüssel `key` in der Map `sgs` überhaupt existiert. Wenn nicht, wird ein leeres *Optional*  (`Optional.empty()`) zurückgegeben. Wenn doch, ermitteln wir mithilfe der `get(key)`-Methode aus `Map` den Wert und geben diesen mithilfe von `Optional.of()` zurück. 

Die aufrufende Methode kann nun mithilfe der Objektmethode `isPresent()` ermitteln, ob ein `Optional` einen Wert enthält (`true`) oder nicht (`false`). Ist ein Wert vorhanden, kann dieser mithilfe der Objektmethode `get()` extrahiert werden:


```java linenums="1"
Optional<String> optionalValue = getValue(studiengaenge, "ai");
if(optionalValue.isPresent()) {
    String value = optionalValue.get();
    System.out.println(value);
}

optionalValue = getValue(studiengaenge, "wi");
if(optionalValue.isPresent()) {
    String value = optionalValue.get();
    System.out.println(value);
} else {
    System.out.println("Schluessel wi nicht enthalten!");
}
```

Anstelle der `isPresent()-get()`-Kombination kann auch die Objektethode `orElse()` verwendet werden. Diese liefert den Wert, wenn er existiert und ansonsten den Wert, der als Parameter der Methode übergeben wird, z.B.


```java
System.out.println(optionalValue.orElse("kein Eintrag!"));
```

Beachten Sie, dass der als Parameter übergebene Wert vom dem Typ sein muss, mit dem das `Optional` typisiert ist (hier `String`). 

Die Methode `isPresent()` kann leicht mit der Methode `ifPresent()` verwechselt werden. Diese ist eine weitere Objektmethode von `Optional<T>`. `ifPresent()` erwartet jedoch einen `Consumer` als Parameterwert (`isPresent()` ist parameterlos). 

```java
optionalValue.ifPresent(System.out::println);
```

Der Wert wird ausgegeben, wenn er existiert. Ansonsten wird nichts ausgegeben. 

Die Objektmethode `map()` erwartet eine `Function` und gibt ein `Optional` zurück, z.B. 


```java
optionalValue.map(String::toUpperCase).ifPresent(System.out::println);
```

Einen Überblick über alle Methoden von `Optional<T>` erhalten Sie [hier](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html). Weitergehende Beispiele finden Sie z.B. [hier](https://forums.oracle.com/ords/apexds/post/optionals-patterns-and-good-practices-2540).


!!! tip "Beachte"
	Die Verwendung von `Optional<T>` ist einzig dafür gedacht, als Rückgabe einer Methode verwendet zu werden. Damit wird signalisiert, dass nicht zwingend ein Wert zurückgegeben wird, sondern eventuell auch `null`. Wir sollten jedoch keinesfalls `null` zurückgeben, sondern stattdessen `Optional<T>` verwenden. Als Parametertyp oder als Typ von Obejktvariablen ist `Optional` jedoch nicht geeignet. 

## `OptionalInt`, `OptionalDouble`, `OptionalLong`

So, wie es für [Stream<T>](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Stream.html) noch die speziellen Streams 

    - [IntStream](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/IntStream.html), 
    - [DoubleStream](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/DoubleStream.html) und 
    - [LongStream](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/LongStream.html) 

gibt, gibt es auch für [Optinal<T>](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Optional.html) noch die speziellen Optionals 

    - [OptionalInt](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/OptionalInt.html), 
    - [OptionalDouble](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/OptionalDouble.html) und
    - [OptionalLong](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/OptionalLong.html). 

Anstelle der `get()`-Methode aus `Stream<T>` existiert für diese speziellen Klassen die Methode `getAsInt()` bzw. `getAsDouble()` bzw. `getAsLong()`. 

