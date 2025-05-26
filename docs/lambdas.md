# Lambda-Ausdrücke

*Lambda*-Ausdrücke (*Lambdas*) sind anonyme Funktionen (Methoden), d.h. Funktionen (Methoden) ohne Namen. *Lambdas* werden im Zusammenhang von [Functional Interfaces](interfaces.md#functional-interfaces) verwendet. Im Kontext von *Lambdas* sprechen wir stets eher von Funktionen als von Methoden. Die prinzipielle Syntax von *Lambda*-Ausdrücken ist

```java
(params) -> {body}
```

*Lambda*-Ausdrücke bestehen aus drei Teilen:

1. einer Liste von keinem, einem oder merhrern Parametern, durch Komma getrennt und in runden Klammern `()`. Diesen Parametern muss kein Typ zugewiseen werden. Der jeweilige Tp des Parameters wird aus dem Kontext ermittelt. Besteht die Parameterliste aus genau einem Parameter, können die runden Klammern weggelassen werden.
2. dem Pfeil `->`, der die Parameterliste mit dem Funktionskörper verbindet.
3. Dem Funktionskörper, der nur dann in geschweiften Klammern eingefasst ist, wenn er aus mehr als einer Anweissung besteht. Wir können also auch so schreiben:


```java
(params) -> anweisung
```

Beachten Sie, dass hinter der einzelnen Anweisung kein Semikolon steht. 

## Erstes Beispiel

Wir betrachten ein erstes einfaches Beispiel zur Verwendung von *Lambdas*. Angenommen, wir haben folgende einfache Liste 

```java
List<String> staedte = List.of("Berlin", "Hamburg", "München", "Köln", "Frankfurt am Main", "Düsseldorf",
                "Stuttgart", "Leipzig", "Dortmund", "Bremen", "Essen" ,"Dresden");
```

und wollen jedes einzelne Element aus dieser Liste ausgeben. Das hätten wir bis jetzt mit einer `for`-Schleife erledigt. Für Collections steht uns die `forEach()`-Methode aus dem [Iterable-Interface](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html) zur Verfügung. Die `forEach()`-Methode ist wie folgt deklariert:

```java
void forEach(Consumer<T> action)
```

Das Interessante darin ist das [Consumer-Interface](https://docs.oracle.com/javase/8/docs/api/java/util/function/Consumer.html). Dieses stellt die Schnittstelle zu unseren *Lambda*-Ausdrücken dar. Das *Consumer*-Interface repräsentiert eine *Funktion*, die einen einzelnen Parameter akzeptiert und keinen Wert zurückliefert. Wir können nun einen *Lambda*-Ausdruck als *Consumer* definieren, z.B.:

```java
staedte.forEach((stadt)  -> System.out.println(stadt));
``` 

Da wir nur genau einen Parameter haben, können wir auch die runden Klammern weglassen: 

```java
staedte.forEach(stadt  -> System.out.println(stadt));
``` 

Sollte unsere Funktion aus mehreren Anweisungen bestehen, verwenden wir geschweifte Klammern (und Semikolon):

```java
staedte.forEach(stadt  -> {
        System.out.printf("%2d : ", (staedte.indexOf(stadt) + 1) );
        stadt= stadt.toUpperCase();
        System.out.println(stadt);
});
```

Wir könnten uns den `Consumer` auch zunächst explizit definieren und dann wiederverwenden:

```java
Consumer<String> printStadt = stadt  -> {
    System.out.printf("%2d : ", (staedte.indexOf(stadt) + 1) );
    stadt= stadt.toUpperCase();
    System.out.println(stadt);
};
staedte.forEach(printStadt);
```

## Functional Interfaces

Wir haben nun bereits *Consumer* kennengelernt. *Consumer* ist ein [Functional Interface](interfaces.md#functional-interfaces), d.h. es besitzt genau eine abstrakte Methode (`accept()`). *Lambdas* lassen sich nur in Verbindung mit *Functional Interfaces* verwenden, denn nur dann ist eindeutig, welche Methode durch den *Lambda-Ausdruck* implementiert wird. Wir betrachten folgendes Beispiel zur Klärung (siehe [Functional Interfaces](interfaces.md#functional-interfaces)):

```java
@FunctionalInterface
public interface Printable
{
    void print(String s);

    default void print()
    {
        print("default");
    }
}
```

`Printable` ist ein funktionales Interface, da es nur genau eine abstrakte Methode, nämlich `print(String)` enthält. Die `print()`-Methode ist eine sogenannte *default*-Methode und bereits implementiert. 

Wir könnten uns nun eine Klasse definieren, die `Printable` implementiert, z.B. 

```java
public class UseInterface implements Printable
{

    @Override
    public void print(String s)
    {
        System.out.println(s);
    }
}
```

und wenn wir nun irgendwo eine Methode haben, die ein `Printable` erwartet, kann dieser Methode ein Objekt von `UseInterface` übergeben werden:

```java
public class Programmklasse
{
    public static void printSomething(Printable p, String s)
    {
        p.print(s);
    }

    public static void main(String[] args)
    {
        UseInterface useInterface = new UseInterface();
        printSomething(useInterface, "hallo");
    }
}
```

Das ist natürlich alles sehr aufwändig:

- wir benötigen eine Klasse, die `Printable` implementiert (hier: `UseInterface`),
- wir benötigen ein Objekt dieser Klasse 

und das alles nur, um `printSomething()` auszuführen. Einfacher wäre es, wir würden direkt in `printSomething()` die `print()`-Methode des Interfaces `Printable` implementieren. Das geht und zwar unter Verwendung von *Lambdas*:

```java
public class Programmklasse
{
    public static void printSomething(Printable p, String s)
    {
        p.print(s);
    }

    public static void main(String[] args)
    {
        // UseInterface useInterface = new UseInterface();
        // printSomething(useInterface, "hallo");
        printSomething((s) -> System.out.println(s), "hallo" );
    }
}
```


Mithilfe von `(s) -> System.out.println(s)` wird also die abstrakte `print(s)`-Methode aus dem (Functional) Interface `Printable` implementiert. Wir benötigen keine extra Klasse, die `Printable` implementiert und somit auch kein Objekt dieser Klasse. 

Das `Printable`-Interface aus unserem Beispiel ist vergleichbar mit dem [Consumer](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/function/Consumer.html)-Interface, da eine Methode implementiert wird, die keinen Wert zurückgibt. Die funktionale Methode heißt `accept(T)`. Es folgt ein kurzer Überblick über die wesentlichen *Functional Interfaces*  aus dem Paket `java.util.function`.



## java.util.function.Consumer<T>

Das Functional Interface [Consumer](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/function/Consumer.html) repräsentiert eine *Funktion* (Methode), die einen Parameter vom Typ `T` akzeptiert, die Methode ausführt und keinen Wert zurückgibt. Die funktionale Methode heißt `void accept(T)`. 

Einfaches `Consumer`-Beispiel:

```java
Consumer<String> print = message -> System.out.println(message);
print.accept("Hallo FIW!");
```

## java.util.function.Function<T, R>

Das Functional Interface [Function](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/function/Function.html) repräsentiert eine *Funktion* (Methode), die einen Parameter vom Typ `T`akzeptiert und durch Ausführung der Methode ein Resultat vom Typ `R` zurückgibt. Die funktionale Methode heißt `R apply(T)`. 

Einfaches `Function`-Beispiel:

```java
Function<String, Integer> stringLength = str -> str.length();
System.out.println(stringLength.apply("Hallo FIW!"));           // Output: 10
```


Für den Fall, dass zwei Parameter erwartet werden, gibt es das Functional Interface [BiFunction](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/BiFunction.html). 


Einfaches `BiFunction`-Beispiel:

```java
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
System.out.println(add.apply(3,4));                             // Output: 7
```

Auf diese Weise können Sie sich auch eigene Functional Interfaces bauen (siehe z.B. [hier](https://medium.com/@malvin.lok/5-lambda-skills-every-java-developer-should-master-java-11-bc3e04dce912)), z.B.:

```java
@FunctionalInterface
interface TriFunction<T, U, V, R> {
    R apply(T t, U u, V v);
}
```

und dann

```java
// Using custom TriFunction
TriFunction<String, String, String, String> concat = 
    (a, b, c) -> a + b + c;

String result = concat.apply("Hello", " ", "World");
System.out.println(result); // Output: Hello World

// More practical example
TriFunction<Double, Double, Double, Double> calculateVolume = 
    (length, width, height) -> length * width * height;

Double volume = calculateVolume.apply(2.0, 3.0, 4.0);
System.out.println("Volume: " + volume); // Output: Volume: 24.0
```



Das Functional Interface `Function` besitzt neben der *SAM* (*single abstract method*) `apply(T t)` auch noch die *default*-Methoden `andThen(Function after)` und `compose(Function before)`. Damit lassen sich Funktionen "zusammenbauen" (siehe z.B. [hier](https://medium.com/@malvin.lok/5-lambda-skills-every-java-developer-should-master-java-11-bc3e04dce912)):

```java
Function<Integer, Integer> multiply = x -> x * 2;
Function<Integer, Integer> add = x -> x + 3;

// Using andThen (first multiply, then add)
Function<Integer, Integer> multiplyThenAdd = multiply.andThen(add);
System.out.println(multiplyThenAdd.apply(5)); // Output: 13

// Using compose (first add, then multiply)
Function<Integer, Integer> addThenMultiply = multiply.compose(add);
System.out.println(addThenMultiply.apply(5)); // Output: 16

// andThen() and compose() are default-methods in Function
```


## java.util.function.Predicate<T>

Das Functional Interface [Predicate](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/Predicate.html) repräsentiert eine *Funktion* (Methode), die einen Parameter vom Typ `T`akzeptiert und durch Ausführung der Methode ein Resultat vom Typ `boolean` zurückgibt. Die funktionale Methode heißt `boolean test(T)`. 

Einfaches `Predicate`-Beispiel:

```java
Predicate<Integer> isEven = number -> number % 2 == 0;
System.out.println(isEven.test(4));                             // Output: true
```

Für den Fall, dass zwei Parameter erwartet werden, gibt es das Functional Interface [BiPredicate](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/BiPredicate.html). 


Einfaches `BiPredicate`-Beispiel:

```java
BiPredicate<String, String> equalsIgnoreCases = (str1, str2) -> str1.toLowerCase().equals(str2.toLowerCase());
System.out.println(equalsIgnoreCases.test("Hallo FIW!", "HALLO fiw!"));                             // Output: true
```


Das Functional Interface `Predicate` besitzt neben der *SAM* (*single abstract method*) `test(T t)` auch noch die *default*-Methoden `and(Predicate other)`, `not(Predicate target)` und `or(Predicate other)`. Damit lassen sich Bedingungen "zusammenbauen" (siehe z.B. [hier](https://medium.com/@malvin.lok/5-lambda-skills-every-java-developer-should-master-java-11-bc3e04dce912)):

```java
Predicate<Person> isAdult = person -> person.getAge() >= 18;
Predicate<Person> isFromGermany = person -> "GER".equals(person.getCountry());
Predicate<Person> isNameStartsWithJ = person -> person.getName().startsWith("J");

// Combining predicates
Predicate<Person> isAdultFromGermanyWithJName = isAdult
    .and(isFromUGermany)
    .and(isNameStartsWithJ);

// and() ist default-method in Predicate (or(), negate())
```


## java.util.function.Supplier<T>

Das Functional Interface [Supplier](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/Supplier.html) repräsentiert eine *Funktion* (Methode), die durch Ausführung der Methode ein Resultat vom Typ `T` zurückgibt. Die funktionale Methode heißt `T get()`. `Supplier` wird z.B. benutzt, um sogenannte *Fabrik-Methoden* zu definieren. *Fabrik-Methoden* erzeugen neue Objekte. Dafür schauen wir uns den folgenden Abschnitt [Methode-Referenzen](#methoden-referenzen) genauer an:


## Methoden-Referenzen

Methoden-Referenzen sind eine syntaktische Abkürzung, um Methoden aufzurufen. Methoden-Referenzen sind somit ein spezieller Fall für Lambda-Ausdrücke. Methoden-Referenzen erkennen wir an folgender Syntax 

```java
::methode
```

Handelt es sich um eine statische Methode, steht vor dem `::` der Name der Klasse, bei einer Objektmethode steht die Referenzvariable des Objektes davor. 
Bei der Verwendung von Methoden-Referenzen können wir in Lambdas sogar ganz auf die Verwendung der Parameter verzichten. Der Code wird dadurch lesbarer (siehe `staedte`-Beispiel oben):

```java
staedte.forEach(System.out::println);
```

Einfaches Beispiel für `Supplier`:

```java
Supplier<List<String>> listSupplier = ArrayList::new;
List<String> list = listSupplier.get();
```

Zu weiteren Informationen über Methodenreferenzen siehe z.B. [hier](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html).



