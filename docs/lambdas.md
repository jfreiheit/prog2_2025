# Lambda-Ausdrücke

*Lambda*-Ausdrücke (*Lambdas*) sind anonyme Funktionen (Methoden), d.h. Funktionen (Methoden) ohne Namen. Im Kontext von *Lambdas* sprechen wir stets eher von Funktionen als von Methoden. Die prinzipielle Syntax von *Lambda*-Ausdrücken ist

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
void forEach(Consumer<? super T> action)
```

Das Interessante darin ist das [Consumer-Interface](https://docs.oracle.com/javase/8/docs/api/java/util/function/Consumer.html). Dieses stellt die Schnittstelle zu unseren *Lambda*-Ausdrücken dar. Das *Consumer*-interface repräsentiert eine *Funktion*, die einen einzelnen Parameter akzeptiert und keinen Wert zurückliefert. Wir können nun einen *Lambda*-Ausdruck als *Consumer* definieren, z.B.:

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

Wir haben nun bereits *Consumer* kennengelernt. 

## Methoden-Referenzen

Methoden-Referenzen sind eine syntaktische Abkürzung, um Methoden aufzurufen. Methoden-Referenzen sind somit ein spezieller Fall für Lambda-Ausdrücke. Methoden-Referenzen erkennen wir an folgender Syntax 

```java
::methode
```

Handelt es sich um eine statische Methode, steht vor dem `::` der Name der Klasse, bei einer Objektmethode steht die Referenzvariable des Objektes davor. 
Bei der Verwendung von Methoden-Referenzen können wir in Lambdas sogar ganz auf die Verwendung der Parameter verzichten. Der Code wird dadurch lesbarer:

```java
staedte.forEach(System.out::println);
```