# Übungen


##### Übung 1 (Codereview und static)

??? "Was ist an diesem Code alles falsch?"

	```java
	package uebungen.uebung1;

	/*
	 * °C = (°F - 32) * 5/9 (von Fahrenheit in Celsius)
	 * °F = °C * 1,8 + 32 (von Celsius nach Fahrenheit)
	 */

	public class Konvertierung {
		
		private double celsius;
		private double fahrenheit;
		
		public Konvertierung(double celsius) 
		{		
			this.celsius = celsius;
			this.fahrenheit = celsius * 1.8 + 32;		
		}
		
		public Konvertierung(double fahrenheit) 
		{		
			this.celsius = fahrenheit - 32 * 5/9;
			this.fahrenheit = fahrenheit;		
		}
		
		public void print()
		{
			System.out.println(this.celsius + "\u00B0C = " + this.fahrenheit + "\u00B0F");
		}
	}
	```


??? success "Eine mögliche Lösung für Übung 1"
	```java
	package uebungen.uebung1;

	/*
	 * °C = (°F - 32) * 5/9 (von Fahrenheit in Celsius)
	 * °F = °C * 1,8 + 32 (von Celsius nach Fahrenheit)
	 */

	public class Konvertierung {

		private Konvertierung() {
			
		}
	    
	    public static double celsiusToFahrenheit(double celsius) {
	    	final double FACTOR_CELSIUS_TO_FAHRENHEIT = 1.8;
	    	final int DIFFERENCE_CELSIUS_TO_FAHRENHEIT = 32;
	    	
	    	double fahrenheit = celsius * FACTOR_CELSIUS_TO_FAHRENHEIT 
	    			+ DIFFERENCE_CELSIUS_TO_FAHRENHEIT; 
	    	
	    	return fahrenheit;
	    }
	    
	    public static double fahrenheitToCelsius(double fahrenheit) {
	    	final double FACTOR_FAHRENHEIT_TO_CELSIUS = 5.0/9.0;
	    	final int DIFFERENCE_FAHRENHEIT_TO_CELSIUS = 32;
	    	
	    	double celsius = (fahrenheit - DIFFERENCE_FAHRENHEIT_TO_CELSIUS) * FACTOR_FAHRENHEIT_TO_CELSIUS;
	   
	    	return celsius;
	    }
	}
	```

##### Übung 2 (String und algorithmisches Denken)

??? "Übung 2"

	1. Erstellen Sie im Paket `uebungen.uebung2` eine Java-Klasse `Uebung2` mit `main()`-Methode. In diese Klasse implementieren wir statische Methoden. Öffnen Sie zum Lösen der Übung am besten die JavaDoc-Dokumentation der Klasse [String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html). Überlegen Sie sich, bevor Sie jeweils anfangen zu implementieren, genau, wie Sie vorgehen möchten.

	2. Implementieren Sie eine Methode `static boolean isBinaryNumber(String s)`. Diese Methode überprüft, ob der `String s` einer Binärzahl entspricht, d.h. ob er nur `0` und `1` enthält. 

	3. Testen Sie die Methode `isBinaryNumber(String s)` z.B. mit den folgenden Aufrufen:
	```java
	System.out.println(isBinaryNumber("101101"));	// true
	System.out.println(isBinaryNumber("0"));		// true
	System.out.println(isBinaryNumber("101a01"));	// false
	System.out.println(isBinaryNumber("101201"));	// false
	```

	4. Implementieren Sie eine Methode `static int binaryToDecimal(String s)`. Diese Methode wandelt den `String s` in eine Dezimalzahl um, wenn `s` einer Binärzahl entspricht. Wenn `s` keiner Binärzahl entspricht, wird `-1` zurückgegeben. 

	5. Testen Sie die Methode `binaryToDecimal(String s)` z.B. mit den folgenden Aufrufen:
	```java
	System.out.println(binaryToDecimal("101101"));	// 45
	System.out.println(binaryToDecimal("0"));		// 0
	System.out.println(binaryToDecimal("000001"));	// 1
	System.out.println(binaryToDecimal("100000"));	// 32
	System.out.println(binaryToDecimal("101a01"));	// -1
	System.out.println(binaryToDecimal("101201"));	// -1
	```

	6. Implementieren Sie eine Methode `static String toLowerCase(String input)`. Diese Methode wandelt alle Großbuchstaben ('A'...'Z') in Kleinbuchstaben um (und nur diese - alle anderen Zeichen bleiben erhalten). Schauen Sie sich dazu auch nochmal die [ASCII-Tabelle](https://freiheit.f4.htw-berlin.de/prog1/variablen/#char) an.

	7. Testen Sie die Methode `toLowerCase(String input)` z.B. mit den folgenden Aufrufen:
	```java
	System.out.println(toLowerCase("abcdEFG"));		// abcdefg
	System.out.println(toLowerCase("abcd123EFG"));	// abcd123efg
	System.out.println(toLowerCase("ABC XYZ !%"));	// abc xyz !%
	```

	**Zusatz:**

	8. Implementieren Sie eine Methode `static boolean isPalindrome(String input)`. Diese Methode prüft, ob es sich bei `input` um ein Palindrom handelt (also von vorne nach hinten genauso gelesen werden kann, wie von hinten nach vorne). Groß- und Kleinschreibung wird nicht berücksichtigt! Die Methode [substring(int,int)](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#substring(int,int)) aus `String` ist dabei wahrscheinlich nützlich!

	9. Testen Sie die Methode `isPalindrome(String input)` z.B. mit den folgenden Aufrufen:
	```java
	System.out.println(isPalindrome("Otto"));		// true
	System.out.println(isPalindrome("abc_CBA"));	// true
	System.out.println(isPalindrome("abc_-CBA"));	// false
	System.out.println(isPalindrome("-"));			// true
	System.out.println(isPalindrome("Dreh mal am Herd"));	// false 
	```

	8. Angenommen, Sie sollen für einen gegebenen `String` angeben, ob er korrekt geklammerte Ausdrücke enthält (nur die Klammern betrachten). Wie würden Sie vorgehen? Nicht implementieren, nur nachdenken. Folgende Beispiele:
	```
	((()))()(()) 		// korrekt
	((())				// nicht korrekt
	(()))				// nicht korrekt
	())(				// nicht korrekt
	```


??? success "Eine mögliche Lösung für Übung 2"
	```java
	package uebungen.uebung2.loesung;

	public class Uebung2 {
		
		public static boolean isBinaryNumber(String s)
		{
			for(int index=0; index < s.length(); index++)
			{
				char c = s.charAt(index);
				if(!(c=='0' || c=='1'))
				{
					return false;
				}
			}
			return true;
		}
		
		public static int binaryToDecimal(String s)
		{
			final int STRING_IS_NOT_A_BINARY_NUMBER = -1;
	        if(!isBinaryNumber(s))
	        {
	           return STRING_IS_NOT_A_BINARY_NUMBER;
	        }
	        int positionValue = 1;
			int decimalNumber = 0;
			int exp = 0;
			for(int index = s.length()-1; index >= 0; index--)
			{
				char c = s.charAt(index);
				int digit = c - '0';
				int value = digit * positionValue;
				decimalNumber += value;
				positionValue *= 2;
			}
			
			return decimalNumber;
		}
		
		public static String toLowerCase(String input)
		{
			String output = "";
			final int UPPER_TO_LOWER = 32;

			for(int index=0; index < input.length(); index++)
			{
				char c = input.charAt(index);
				if(c >= 'A' && c<= 'Z')
				{
					c += UPPER_TO_LOWER;	// "automatic" type cast c = (char)(c + UPPER_TO_LOWER)
				}
				output += c;
			}
			return output;
		}
			
		public static boolean isPalindrome(String input)
		{
			String s = toLowerCase(input);
			boolean palindrome = true;
			while(palindrome && s.length() > 1)
			{
				char c1 = s.charAt(0); 
				char c2 = s.charAt(s.length() - 1);
				if(c1 == c2)
				{
					s = s.substring(1,s.length() - 1);
				}
				else 
				{
					palindrome = false;
				}
			}
			return palindrome;
		}
			
		public static boolean checkBraces(String input)
		{
			int nrOpening = 0;	// man koennte auch fuer jede oeffnende ++ und
			int nrClosing = 0;	// jede schliessende -- und dann nur eine Variable
								// dann pruefen, ob nie negativ
			boolean correct = true;
			for(int index=0; correct && index < input.length(); index++)
			{
				char c = input.charAt(index);
				if(c== '(') 
				{
					nrOpening++;
				}
				else if(c== ')') 
				{
					nrClosing++;
				}
				
				if(nrClosing > nrOpening)	// dann waere hier < 0
				{
					correct = false;
				}
			}
			if(nrOpening != nrClosing) 		// dann waere hier == 0
			{
				correct = false;
			}
			return correct;
		}

		public static void main(String[] args) {
			System.out.println(isBinaryNumber("101101"));	// true
			System.out.println(isBinaryNumber("0"));		// true
			System.out.println(isBinaryNumber("101a01"));	// false
			System.out.println(isBinaryNumber("101201"));	// false

			System.out.println(binaryToDecimal("101101"));	// 45
			System.out.println(binaryToDecimal("0"));		// 0
			System.out.println(binaryToDecimal("000001"));	// 1
			System.out.println(binaryToDecimal("100000"));	// 32
			System.out.println(binaryToDecimal("101a01"));	// -1
			System.out.println(binaryToDecimal("101201"));	// -1
			
			System.out.println(toLowerCase("abcdEFG"));		// abcdefg
			System.out.println(toLowerCase("abcd123EFG"));	// abcd123efg
			System.out.println(toLowerCase("ABC XYZ !%"));	// abc xyz !%
		
			System.out.println(isPalindrome("Otto"));		// true
			System.out.println(isPalindrome("abc_CBA"));	// true
			System.out.println(isPalindrome("abc_-CBA"));	// false
			System.out.println(isPalindrome("-"));			// true
			System.out.println(isPalindrome("Dreh mal am Herd"));	// false
			// das letzte waere okay, wenn man bei der Pruefung
			// die Leerzeichen ignorieren wuerde, waere auch moeglich
		}

	}
	```

##### Übung 3 (enum und zweidimensionale Arrays)

??? "Übung 3"

	1. Gegeben ist die folgende Klasse `TicTacToe`:

		```java linenums="1"
		package uebungen.uebung3;

		public class TicTacToe 
		{
			enum State {EMPTY, RED, BLACK};
			State[][] field;

			public TicTacToe()
			{
				field = new State[3][3];
				for(int i=0; i<field.length; i++)
				  for(int j=0; j<field[i].length; j++)
				  	field[i][j]=State.EMPTY;
			}

			public void makeMove(int i, int j, State player)
			{
				if(field[i][j]==State.EMPTY && player!=State.EMPTY)   
					field[i][j]=player;
			}
		}
		```
	
	2. Fügen Sie alle notwendigen Klammern `{ }` ein, so dass die Anweisungsblöcke korrekt geklammert sind. 
	3. Erweitern Sie die Klasse `TicTacToe` um eine `print()`-Methode, die das Spielfeld auf die Konsole ausgibt (Setzen Sie z.B. für den Player `RED` ein `x` und für den Player `Black` ein `o` und für `EMPTY` ein Leerzeichen oder ein `-`). Die Ausgabe nach jeweils 2 Zügen von `RED` und `BLACK` könnte dann z.B. so aussehen: 

		```bash
		- o o 
		- x - 
		- - x 
		```

	4. Erweitern Sie die Klasse `TicTacToe` um eine `gewonnen()`-Methode (`true`, wenn ein Spieler drei Felder horizontal, diagonal oder vertikal belegt hat; ansonsten `false`).
	5. Erweitern Sie die Klasse `TicTacToe` um eine `unentschieden()`-Methode (`true`, wenn alle Felder besetzt sind, aber kein Spieler gewonnen hat; ansonsten `false`).
	6. Erstellen Sie eine Test-Klasse mit `main()`-Methode. Erstellen sie darin ein Objekt der Klasse `TicTacToe`. Führen Sie Züge aus (`makeMove()`) und prüfen Sie, ob gewonnen wurde oder unentschieden ist (mit entsprechenden Ausgaben). 
	7. Für 6. müssen Sie in der Testklasse Ihr `enum State` importieren. Warum ist das so? Was könnten Sie machen, damit das nicht notwendig ist?

	8. *Zusatz:* Sie können die Klasse `TicTacToe` beliebig erweitern, z.B.:
		- um Ausgaben, wenn gewonnen bzw. es unentschieden ist,
		- um Fehler in den Indizes `i` und `j` bei der `makeMove()`-Methode abzufangen,
		- eine Methode `spielen()` implementieren, die zufällig für die Spieler die Steine setzt usw.


??? success "Eine mögliche Lösung für Übung 3"
	=== "TicTacToe.java"
		```java
		package uebungen.uebung3;

		import java.util.Random;

		public class TicTacToe
		{
		    //enum State {EMPTY, RED, BLACK};
		    State[][] field;
		    State player;

		    public TicTacToe()
		    {
		        this.field = new State[3][3];
		        this.player = State.RED;
		        for(int row=0; row<this.field.length; row++)
		        {
		            for (int col = 0; col < this.field[row].length; col++)
		            {
		                this.field[row][col] = State.EMPTY;
		            }
		        }
		    }

		    private void swapPlayer()
		    {
		        this.player = (this.player == State.BLACK) ? State.RED : State.BLACK;
		    }

		    public void makeMove(int row, int col, State player)
		    {
		        if(this.field[row][col]==State.EMPTY && player!=State.EMPTY)
		        {
		            this.field[row][col] = player;
		        }
		    }

		    public void print()
		    {
		        for(int row=0; row<this.field.length; row++)
		        {
		            for (int col = 0; col < this.field[row].length; col++)
		            {
		                /*
		                if(this.field[row][col] == State.EMPTY)
		                {
		                    System.out.print("- ");
		                }
		                else if(this.field[row][col] == State.RED)
		                {
		                    System.out.print("x ");
		                }
		                else if(this.field[row][col] == State.BLACK)
		                {
		                    System.out.print("o ");
		                }

		                 */
		                /*
		                switch(this.field[row][col]) {
		                    case EMPTY: System.out.print("- "); break;
		                    case RED:   System.out.print("x "); break;
		                    case BLACK: System.out.print("o "); break;
		                }

		                 */
		                switch(this.field[row][col]) {
		                    case EMPTY -> { System.out.print("- "); }
		                    case RED -> { System.out.print("x "); }
		                    case BLACK -> { System.out.print("o "); }
		                }

		            }
		            System.out.println();
		        }
		        System.out.println();
		    }

		    private boolean won(State player)
		    {
		        // drei in einer Zeile ?
		        for(int row=0; row<this.field.length; row++)
		        {
		            if(this.field[row][0]==player && this.field[row][1]==player && this.field[row][2]==player)
		            {
		                return true;
		            }
		        }

		        // drei in einer Spalte ?
		        for(int col=0; col<this.field.length; col++)
		        {
		            if(this.field[0][col]==player && this.field[1][col]==player && this.field[2][col]==player)
		            {
		                return true;
		            }
		        }

		        // Diagonale von links oben nach rechts unten
		        if(this.field[0][0]==player && this.field[1][1]==player && this.field[2][2]==player)
		        {
		            return true;
		        }

		        // Diagonale von links unten nach rechts oben
		        if(this.field[2][0]==player && this.field[1][1]==player && this.field[0][2]==player)
		        {
		            return true;
		        }

		        return false;
		    }

		    public boolean won()
		    {
		        return this.won(State.RED) ||this.won(State.BLACK);
		    }

		    private boolean full()
		    {
		        for(int row=0; row<this.field.length; row++)
		        {
		            for(int col=0; col<this.field[row].length; col++)
		            {
		                if(this.field[row][col]==State.EMPTY)
		                {
		                    return false;
		                }
		            }
		        }
		        return true;
		    }

		    public boolean draw()
		    {
		        return this.full() && !this.won();
		    }

		    public void printResult()
		    {
		        if(this.won(State.RED))
		        {
		            System.out.println("Rot hat gewonnen!");
		        }
		        else if(this.won(State.BLACK))
		        {
		            System.out.println("Schwarz hat gewonnen!");
		        }
		        else if(this.draw())
		        {
		            System.out.println("Unentschieden!");
		        }
		    }

		    private boolean winPossible()
		    {
		        for(int row=0; row<this.field.length; row++)
		        {
		            for(int col=0; col<this.field[row].length; col++)
		            {
		                if(this.field[row][col]==State.EMPTY)
		                {
		                    this.field[row][col] = this.player;
		                    if(this.won(this.player))
		                    {
		                        this.field[row][col] = State.EMPTY;
		                        return true;
		                    }
		                    this.field[row][col] = State.EMPTY;
		                }
		            }
		        }
		        return false;
		    }

		    public void makeRandomMove()
		    {
		        Random r = new Random();
		        int row = r.nextInt(this.field.length);
		        int col = r.nextInt(this.field[row].length);
		        while(this.field[row][col] != State.EMPTY)
		        {
		            row = r.nextInt(this.field.length);
		            col = r.nextInt(this.field[row].length);
		        }
		        this.field[row][col] = this.player;
		        this.swapPlayer();
		    }
		}

		```
	=== "State.java"
		```java
		package uebungen.uebung3;

		public enum State
		{
		    EMPTY, RED, BLACK
		}
		```			
	=== "Programmklasse.java"
		```java
		package uebungen.uebung3;

		public class Programmklasse
		{
		    public static void main(String[] args)
		    {
		        TicTacToe ttt = new TicTacToe();
		        /*
		        ttt.print();
		        ttt.makeMove(1, 2, State.RED);
		        ttt.print();
		        ttt.makeMove(1, 1, State.BLACK);
		        ttt.print();

		         */
		        while(!( ttt.won() || ttt.draw() ))
		        {
		            ttt.makeRandomMove();
		            ttt.print();
		        }
		        ttt.printResult();
		    }
		}
		```	


##### Übung 4 (Exceptions)

??? "Übung 4"

	1. Schreiben Sie ein Programm zur Eingabe von zwei Zahlen mithilfe der Klasse `JOptionPane` und deren Division! Fangen Sie folgende Ausnahmen ab:
		- Falls die Eingabe keiner Zahl entspricht.
		- Falls die zweite Zahl eine 0 ist.

	2. **Scenario**:
		- Fenster zur Eingabe von Zahl 1 öffnet sich: <br/>
			![uebung2](./files/22_uebung2.png)
		- falsche Eingabe - keine Zahl:  <br/>
			![uebung2](./files/23_uebung2.png)
		- Fenster öffnet sich erneut (andere Nachricht!):  <br/>
			![uebung2](./files/24_uebung2.png)
		- Fenster zur Eingabe von Zahl 2 öffnet sich:  <br/>
			![uebung2](./files/25_uebung2.png)
		- die Division Zahl1/Zahl2 schlägt fehl (`ArithmeticException`), deshalb (andere Nachricht!):  <br/>
			![uebung2](./files/26_uebung2.png)
		- Ergebnis  <br/>
			![uebung2](./files/27_uebung2.png)

	**Zusatz**
	
	3. Lagern Sie eine solche Eingabemöglichkeit in eine wiederverwendbare Methode aus, z.B. `public int inputInt(int min, int max)`, welche die eingegebene Zahl zurückgibt, wobei die eingegebene Zahl im Bereich `[min, max]` liegen muss.


	**Viel Spaß!**


??? success "Eine mögliche Lösung für Übung 4"
	```java
	package uebungen.uebung4;

	import javax.swing.*;

	public class Uebung4
	{
	    public static int inputInt(String message)
	    {
	        boolean inputOk = false;
	        int number = 0;
	        while(!inputOk)
	        {
	            String input = JOptionPane.showInputDialog(message);

	            try {
	                number = Integer.parseInt(input);
	                inputOk = true;
	            }
	            catch(NumberFormatException e) {
	                message = "Es war keine Zahl! Bitte Zahl eingeben!";
	            }
	        }
	        return number;
	    }

	    public static int inputInt(int min, int max)
	    {
	        String message = "Zahl im Bereich zwischen " + min + " und " + max + ": ";
	        boolean inputOk = false;
	        int number = 0;
	        while(!inputOk)
	        {
	            String input = JOptionPane.showInputDialog(message);

	            try {
	                number = Integer.parseInt(input);
	                if(number >= min && number <= max) {
	                    inputOk = true;
	                }
	                else {
	                    message = "Zahl muss im Bereich zwischen " + min + " und " + max + " sein !";
	                }
	            }
	            catch(NumberFormatException e) {
	                message = "Es war keine Zahl! Bitte Zahl eingeben!";
	            }
	        }
	        return number;
	    }

	    public static int reverseNumber(int number)
	    {
	        int result = 0;
	        int copy = number;
	        while(copy != 0)
	        {
	            result = result * 10 + copy % 10;
	            copy /= 10;
	        }
	        return result;
	    }

	    public static int crossSum(int number)
	    {
	        int crossSum = 0;
	        int copy = number;
	        while(copy != 0)
	        {
	            crossSum += copy % 10;
	            copy /= 10;
	        }
	        return crossSum;
	    }



	    public static void main(String[] args)
	    {
	        int zahl1 = inputInt("Zahl 1");

	        boolean number2Valid = false;
	        String message = "Zahl 2";
	        int zahl2 = 0;
	        int divisor = 0;
	        while (!number2Valid) {
	            zahl2 = inputInt(message);
	            try {
	                divisor = zahl1 / zahl2;
	                number2Valid = true;
	            } catch (ArithmeticException e) {
	                message = "Zahl darf nicht 0 sein!";
	            }
	        }
	        message = zahl1 + " / " + zahl2 + " = " + divisor;
	        JOptionPane.showMessageDialog(null, message, "ERGEBNIS", JOptionPane.PLAIN_MESSAGE);

	        System.out.println(inputInt(1,6));
	    }
	}
	```


##### Übung 5 (try-with-resource und eigene Exception-Klassen)

??? "Übung 5"


	1. Laden Sie sich folgende Datei herunter: [**staedte.csv**](./files/staedte.csv), erstellen Sie in Ihrem Workspace einen `assets`-Ordner (direkt im Projektordner neben `src`und `out`).

	2. Erstellen Sie eine Klasse `Uebung5` mit `main`-Methode und kopieren Sie in die Klasse folgende statische Methode:

		```java
	    public static void printCSVFileUsingFileReader()
	    {
	        String filePath = "assets/staedte.csv";
	        FileReader fileReader = new FileReader(filePath);
	        BufferedReader bufferedReader = new BufferedReader(fileReader);
	        String line;
	        while ((line = bufferedReader.readLine()) != null) {
	            System.out.println(line);
	        }
	    }
		```

		Die Methode lässt sich so nicht übersetzen. Warum nicht? Ändern Sie die Methode so, dass sie ausführbar ist und rufen Sie sie in der `main`-Methode auf. 

	3. Eine andere Möglichkeit für das Einlesen einer Datei ist die Verwendung von `Scanner`:

		```java
	    public static void printCSVFileUsingScanner()
	    {
	        Scanner scanner = new Scanner(new File("assets/staedte.csv"));

	        while (scanner.hasNextLine()) {
	            System.out.println(scanner.nextLine());
	        }

	        scanner.close();
	    }
		```

		Auch diese Methode lässt sich so nicht übersetzen. Ändern Sie die Methode so, dass sie ausführbar ist und rufen Sie sie in der `main`-Methode auf. 

	4. (wenn die Zeit knapp ist, dann Zusatz ;-) Ändern Sie die Ausgabe so, dass folgende "Tabelle" auf der Konsole erscheint:

		```bash
		| Rang | Name                 |       1970 |       1980 |       1990 |       2000 |       2010 |       2020 |       2023 | Bundesland           | 
		|   1. | Berlin               |  3.208.719 |  3.048.759 |  3.433.695 |  3.382.169 |  3.460.725 |  3.664.088 |  3.662.381 | Berlin               | 
		|   2. | Hamburg              |  1.793.640 |  1.645.095 |  1.652.363 |  1.715.392 |  1.786.448 |  1.852.478 |  1.851.596 | Hamburg              | 
		|   3. | München              |  1.311.978 |  1.298.941 |  1.229.026 |  1.210.223 |  1.353.186 |  1.488.202 |  1.488.719 | Bayern               | 
		|   4. | Köln                 |    849.451 |    976.694 |    953.551 |    962.884 |  1.007.119 |  1.083.498 |  1.024.408 | Nordrhein-Westfalen  | 
		|   5. | Frankfurt am Main    |    666.179 |    629.375 |    644.865 |    646.550 |    679.664 |    764.104 |    749.596 | Hessen               | 
		|   6. | Düsseldorf           |    660.963 |    590.479 |    575.794 |    569.364 |    588.735 |    620.523 |    616.319 | Nordrhein-Westfalen  | 
		|   7. | Stuttgart            |    634.202 |    580.648 |    579.988 |    583.874 |    606.588 |    630.305 |    613.111 | Baden-Württemberg    | 
		|   8. | Leipzig              |    583.885 |    562.480 |    511.079 |    493.208 |    522.883 |    597.493 |    608.013 | Sachsen              | 
		|   9. | Dortmund             |    640.642 |    608.297 |    599.055 |    588.994 |    580.444 |    587.696 |    601.343 | Nordrhein-Westfalen  | 
		|  10. | Bremen               |    592.533 |    555.118 |    551.219 |    539.403 |    547.340 |    566.573 |    584.332 | Bremen               | 
		|  11. | Essen                |    696.419 |    647.643 |    626.973 |    595.243 |    574.635 |    582.415 |    574.082 | Nordrhein-Westfalen  | 
		|  12. | Dresden              |    502.432 |    516.225 |    490.571 |    477.807 |    523.058 |    556.227 |    563.019 | Sachsen              | 
		|  13. | Nürnberg             |    478.181 |    484.405 |    493.692 |    488.400 |    505.664 |    515.543 |    526.606 | Bayern               | 
		|  14. | Hannover             |    521.003 |    534.623 |    513.010 |    515.001 |    522.686 |    534.049 |    520.290 | Niedersachsen        | 
		|  15. | Duisburg             |    452.721 |    558.089 |    535.447 |    514.915 |    489.559 |    495.885 |    503.185 | Nordrhein-Westfalen  | 
		|  16. | Wuppertal            |    417.694 |    393.381 |    383.660 |    366.434 |    349.721 |    355.004 |    358.592 | Nordrhein-Westfalen  | 
		|  17. | Bochum               |    343.809 |    400.757 |    396.486 |    391.147 |    374.737 |    364.454 |    357.024 | Nordrhein-Westfalen  | 
		|  18. | Bielefeld            |    168.609 |    312.708 |    319.037 |    321.758 |    323.270 |    333.509 |    331.519 | Nordrhein-Westfalen  | 
		|  19. | Bonn                 |    275.722 |    288.148 |    292.234 |    302.247 |    324.899 |    330.579 |    321.680 | Nordrhein-Westfalen  | 
		|  20. | Mannheim             |    332.378 |    304.303 |    310.411 |    306.729 |    313.174 |    309.721 |    316.256 | Baden-Württemberg    | 
		```

	5. Implementieren Sie die Methode `public static Integer getInteger(Integer[] values, int index)`. Es können 2 Probleme auftreten

		- der `index` passt nicht zum Array,
		- das Element im Array zeigt auf kein Objekt (Referenz ist `null).

		Definieren Sie die Klassen `MyIndexOutOfBoundsException` und `MyNullPointerException`. Beide erben von `RuntimeException`. Wenn Sie in der `main`-Methode folgende Aufrufe haben

		```java
        Integer[] values = new Integer[3];
        values[0] = Integer.valueOf(0);
        values[2] = Integer.valueOf(2);
        for(int index = 0; index <= 3; index++) {
            try {
                System.out.println(getInteger(values, index));
            }
            catch (MyIndexOutOfBoundsException e) {
                System.out.println(e.getMessage());
            }
            catch (MyNullPointerException e) {
                System.out.println(e.getMessage());
            }
        }
        System.out.println("Ende");
		```

		dann soll die Ausgabe wie folgt sein:

		```bash
		0
		no object!
		2
		index 3 ist out of bounds! length = 3
		Ende
		```

		Wie implementieren Sie Ihre Exception-Klassen?

	6. Welchen Unterschied macht es, ob Ihre Exception-Klassen von `RuntimeException` erben oder von `Exception` ?

	**Advanced/Zusatz**

	1. Wir haben die `try-catch()`-Anweisung bisher wie folgt kennengelernt:

		```java
		try {
			// kritische Anweisung_en
		}
		catch(RuntimeException e) {
			//Behandlung der Exception
		}
		```

		Es gibt eine weitere Möglichkeit, die sogenannte `try-with-resources`-Anweisung:

		```java
		try ( // Ressource ) {
			// kritische Anweisung_en
		}
		catch(Exception e) {
			//Behandlung der Exception
		}
		```


		Hier haben wir nach `try` runde Klammern und darin werden sogenannte *Ressourcen* verwaltet. 

		>> Eine *Ressource* ist eine Objekt, das wieder geschlossen werden mussen, wenn die Nutzung der *Ressource* abgeschlossen ist.

		Typische Vertreter solcher *Ressourcen* sind [FileReader](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/FileReader.html) und [BufferedReader](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/BufferedReader.html). *Ressources* sind alle Klassen, die das Java-Interface [Closeable](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/io/Closeable.html) implementieren - zu *Interfaces* kommen wir später.

	2. Ändern Sie 2. und 3. so, dass Sie die `try-with-resources`-Anweisung verwenden.



??? success "Eine mögliche Lösung für Übung 5"
	=== "Uebung5.java"
		```java
		package uebungen.uebung5;

		import java.io.*;
		import java.util.Scanner;

		public class Uebung5
		{
		    public static void printCSVFileUsingFileReader()
		    {
		        String filePath = "assets/staedte.csv";
		        try {
		            FileReader fileReader = new FileReader(filePath);
		            BufferedReader bufferedReader = new BufferedReader(fileReader);
		            String line;
		            while ((line = bufferedReader.readLine()) != null) {
		                String[] data = line.split(";");
		                //System.out.println(data[0]);
		                System.out.printf("| %4s | %-20s | %10s | %10s | %10s | %10s | %10s | %10s | %10s | %-20s |%n",
		                        data[0], data[1], data[2], data[3], data[4], data[5], data[6], data[7], data[8], data[9]);
		                //System.out.println(line);
		            }
		        }
		        catch (FileNotFoundException e)
		        {
		            System.out.println(e.getMessage());
		        }
		        catch(IOException e)
		        {
		            System.out.println(e.getMessage());
		        }
		    }

		    public static void printCSVFileUsingScanner()
		    {
		        try {
		            Scanner scanner = new Scanner(new File("assets/staedte.csv"));
		            while (scanner.hasNextLine()) {
		                System.out.println(scanner.nextLine());
		            }
		            scanner.close();
		        }
		        catch (FileNotFoundException e) {
		            System.out.println(e.getMessage());
		        }
		    }

		    public static Integer getInteger(Integer[] values, int index) throws MyIndexOutOfBoundsException
		    {
		        if (index < 0 || index >= values.length) {
		            throw new MyIndexOutOfBoundsException(index, values.length);
		        }
		        Integer value =  values[index];
		        if(value == null) {
		            throw new MyNullPointerException();
		        }
		        return value;
		    }

		    public static void main(String[] args)
		    {
		        printCSVFileUsingFileReader();
		        //printCSVFileUsingScanner();

		        Integer[] values = new Integer[3];
		        values[0] = Integer.valueOf(0);
		        values[2] = Integer.valueOf(2);
		        for(int index = 0; index <= 3; index++) {
		            try {
		                System.out.println(getInteger(values, index));
		            }
		            catch (MyIndexOutOfBoundsException e) {
		                System.out.println(e.getMessage());
		            }
		            catch (MyNullPointerException e) {
		                System.out.println(e.getMessage());
		            }
		        }
		        System.out.println("Ende");
		    }
		}
		```
	=== "MyIndexOutOfBoundsException.java"
		```java
		package uebungen.uebung5;

		public class MyIndexOutOfBoundsException extends RuntimeException
		{
		    public MyIndexOutOfBoundsException(String message)
		    {
		        super(message);
		    }

		    public MyIndexOutOfBoundsException()
		    {
		        super("index out of bounds");
		    }

		    public MyIndexOutOfBoundsException(int index, int length)
		    {
		        super("index " + index + " ist out of bounds! length = " + length);
		    }
		}
		```
	=== "MyNullPointerException.java"
		```java
		package uebungen.uebung5;

		public class MyNullPointerException extends RuntimeException
		{
		    public MyNullPointerException(String message)
		    {
		        super(message);
		    }

		    public MyNullPointerException()
		    {
		        super("no object!");
		    }
		}
		```



##### Übung 6 (Listen und Mengen)

??? "Übung 6"

	1. Erstellen Sie eine Klasse `Uebung6` mit `main()`-Methode.
	2. Definieren Sie in der `main()`-Methode eine Variable `words` vom Typ `String[]` und weisen Sie dieser Variablen folgende Werte zu:
		```java
		String[] words = {"Linux", "Apple", "Facebook", "Amazon", "IBM", "Lenovo", "Google", "IBM", "Microsoft", "Apple", "Google", "Twitter", "Skype", "Chrome", "Linux", "Firefox"};
		```

	**A. Listen (`List`)**

	1. Erstellen Sie eine Methode `public static List<String> createArrayList(String[] words)`. In dieser Methode soll eine `ArrayList` erstellt werden. Alle Elemente in dieser Liste sind vom Typ `String`. Befüllen Sie diese Liste mit allen Wörtern aus dem `words`-Array. Die Methode gibt die befüllte Liste (`List`) zurück. 
	2. Erstellen Sie eine Methode `public static void printList(List<String> list)`. Diese Methode gibt alle Elemente der Liste `list` auf der Konsole aus. Geben Sie auch die Anzahl der Elemente der Liste aus. 
	3. Erstellen Sie in der `main()`-Methode mithilfe der Methode `createArrayList(words)` eine Liste und speichern Sie diese Liste in einer Variablen vom Typ `List<String>`. Geben Sie alle Elemente dieser Liste mithilfe der Methode `printList()` auf der Konsole aus. 
	4. Studieren Sie alle Methoden für `List` unter [https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/List.html](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/List.html).

		- Ermitteln Sie den Index in der Liste, in der `"Apple"` das **erste** Mal auftaucht. Erzeugen Sie folgende Ausgabe: 
			```bash
			Index des ersten Auftretens von Apple  : 1
			```

		- Ermitteln Sie den Index in der Liste, in der `"Apple"` das **letzte** Mal auftaucht. Erzeugen Sie folgende Ausgabe: 
			```bash
			Index des letzten Auftretens von Apple : 9
			```

		- Geben Sie den Wert des **ersten** Elementes der Liste aus. Erzeugen Sie folgende Ausgabe: 
			```bash
			erstes Element der Liste : Linux
			```	

		- Geben Sie den Wert des **letzten** Elementes der Liste aus. Erzeugen Sie folgende Ausgabe: 
			```bash
			letztes Element der Liste : Firefox
			```	

		- Löschen Sie die Werte `"Apple"`, `"Google"` und `"Facebook"`. Geben Sie die Liste erneut mithilfe der `printList(list)`-Methode aus.

	**B. Mengen (`Set`)**

	1. Erstellen Sie eine Methode `public static Set<String> createHashSet(String[] words)`. In dieser Methode soll eine `HashSet` erstellt werden. Alle Elemente in dieser Menge sind vom Typ `String`. Befüllen Sie diese Menge mit allen Wörtern aus dem `words`-Array. Die Methode gibt die befüllte Menge (`Set`) zurück. 
	2. Erstellen Sie eine Methode `public static void printSet(Set<String> set)`. Diese Methode gibt alle Elemente der Menge `set` auf der Konsole aus. Geben Sie auch die Anzahl der Elemente der Menge aus. 
	3. Erstellen Sie in der `main()`-Methode mithilfe der Methode `createHashSet(words)` eine Menge und speichern Sie diese Menge in einer Variablen vom Typ `Set<String>`. Geben Sie alle Elemente dieser Menge mithilfe der Methode `printSet()` auf der Konsole aus. Was beobachten Sie in Bezug auf die Anzahl der Elemente im Vergleich zur Anzahl der Elemente in der Liste? Warum ist das so?
	4. Erstellen Sie eine Methode `public static Set<String> createTreeSet(String[] words)`. In dieser Methode soll eine `TreeSet` erstellt werden. Alle Elemente in dieser Menge sind vom Typ `String`. Befüllen Sie diese Menge (`Set`) mit allen Wörtern aus dem `words`-Array. Die Methode gibt die befüllte Menge (`Set`) zurück. 
	5. Erstellen Sie in der `main()`-Methode mithilfe der Methode `createTreeSet(words)` eine Menge und speichern Sie diese Menge in einer Variablen. Geben Sie alle Elemente dieser Menge mithilfe der Methode `printSet()` auf der Konsole aus. Was beobachten Sie in Bezug auf die Sortierung der Elemente im Vergleich zur `HashSet`?

	**Zusatz**

	1. Erstellen Sie für die Liste eine Methode `public static List<String> findDoublets(List<String> list)`. Diese Methode erstellt eine Liste, in der alle Elemente enthalten sind, die in `list` doppelt vorkommen. Diese Elemente werden dann auch doppelt in die Resultat-Liste übernommen. Geben Sie diese Liste mithilfe der `printList()`-Methode in der `main()`-Methode aus.

	??? "Mögliche Ausgabe (je nach Reihenfolge des Aufrufs der Methoden)"

		```bash
		Liste mit 16 Elementen :
		--------------------------
		Linux
		Apple
		Facebook
		Amazon
		IBM
		Lenovo
		Google
		IBM
		Microsoft
		Apple
		Google
		Twitter
		Skype
		Chrome
		Linux
		Firefox
		Index des ersten Auftretens von Apple  : 1
		Index des letzten Auftretens von Apple : 9
		erstes Element in der Liste  : Linux
		letztes Element in der Liste : Firefox

		Liste mit 13 Elementen :
		--------------------------
		Linux
		Amazon
		IBM
		Lenovo
		IBM
		Microsoft
		Apple
		Google
		Twitter
		Skype
		Chrome
		Linux
		Firefox

		Doublets-
		Liste mit 4 Elementen :
		--------------------------
		Linux
		IBM
		IBM
		Linux

		ohne Doublets-
		Liste mit 9 Elementen :
		--------------------------
		Amazon
		Lenovo
		Microsoft
		Apple
		Google
		Twitter
		Skype
		Chrome
		Firefox

		Menge mit 12 Elementen :
		--------------------------
		Lenovo
		Google
		Apple
		Skype
		Linux
		IBM
		Twitter
		Chrome
		Microsoft
		Amazon
		Facebook
		Firefox

		Menge mit 12 Elementen :
		--------------------------
		Amazon
		Apple
		Chrome
		Facebook
		Firefox
		Google
		IBM
		Lenovo
		Linux
		Microsoft
		Skype
		Twitter
		```


??? success "Eine mögliche Lösung für Übung 6"
	=== "Uebung6.java"
		```java
		package uebungen.uebung6;

		import java.util.*;

		public class Uebung6
		{
		    public static List<String> createArrayList(String[] words)
		    {
		        List<String> list = new ArrayList<>();
		        for(String word : words)
		        {
		            list.add(word);
		        }
		        return list;
		    }

		    public static void printList(List<String> list)
		    {
		        System.out.printf("Liste mit %d Elementen : %n", list.size());
		        System.out.println("--------------------------");
		        for(String s : list)
		        {
		            System.out.println(s);
		        }
		        System.out.println();
		    }

		    public static Set<String> createHashSet(String[] words)
		    {
		        Set<String> set = new HashSet<>();
		        for(String word : words)
		        {
		            set.add(word);
		        }
		        return set;
		    }


		    public static Set<String> createTreeSet(String[] words)
		    {
		        Set<String> set = new TreeSet<>();
		        for(String word : words)
		        {
		            set.add(word);
		        }
		        return set;
		    }


		    public static Set<Integer> createIntegerSet(int from, int to)
		    {
		        Set<Integer> set = new HashSet<>();
		        for(Integer i = from; i <= to; i++)
		        {
		            set.add(i);
		        }
		        return set;
		    }

		    public static void printSet(Set<String> set)
		    {
		        System.out.printf("Menge mit %d Elementen : %n", set.size());
		        System.out.println("--------------------------");
		        for(String s : set)
		        {
		            System.out.println(s);
		        }
		        System.out.println();
		    }

		    public static void printIntegerSet(Set<Integer> set)
		    {
		        for(Integer i : set)
		        {
		            System.out.print(i + " ");
		        }
		        System.out.println();
		    }

		    public static List<String> findDoubletsTwice(List<String> list)
		    {
		        List<String> doublets = new ArrayList<>();
		        for(String currentValue : list)
		        {
		            if(list.indexOf(currentValue) != list.lastIndexOf(currentValue))
		            {
		                doublets.add(currentValue);
		            }
		        }
		        return doublets;
		    }

		    public static List<String> findDoubletsOnce(List<String> list)
		    {
		        List<String> doublets = new ArrayList<>();
		        for(int index = 0; index < list.size(); index++)
		        {
		            String currentValue = list.get(index);
		            if(contains(list, currentValue, index+1))
		            {
		                doublets.add(currentValue);
		            }
		        }
		        return doublets;
		    }

		    public static boolean contains(List<String> list, String currentValue, int index)
		    {
		        for(int i = index; i < list.size(); i++)
		        {
		            if(list.get(i).equals(currentValue))
		            {
		                return true;
		            }
		        }
		        return false;
		    }

		    public static void main(String[] args)
		    {
		        System.out.printf("%n%n------- Uebung6 -------%n%n");
		        String[] words = {"Linux", "Apple", "Facebook", "Amazon",
		                "IBM", "Lenovo", "Google", "IBM", "Microsoft",
		                "Apple", "Google", "Twitter", "Skype", "Chrome",
		                "Linux", "Firefox"};

		        System.out.printf("%n%n------- List -------%n%n");
		        List<String> wordsList = createArrayList(words);
		        printList(wordsList);
		        int indexFirst = wordsList.indexOf("Apple");
		        int indexLast = wordsList.lastIndexOf("Apple");
		        String firstWord = wordsList.get(0);
		        String lastWord = wordsList.get(wordsList.size() - 1);
		        System.out.println("Index des ersten Auftretens von Apple : " + indexFirst);
		        System.out.println("Index des letzten Auftretens von Apple : " + indexLast);
		        System.out.println("erstes Element der Liste : " + firstWord);
		        System.out.println("letztes Element der Liste : " + lastWord);
		        System.out.println("Loeschen von Apple : " + wordsList.remove("Apple"));
		        System.out.println("Loeschen von Google : " + wordsList.remove("Google"));
		        System.out.println("Loeschen von Facebook : " + wordsList.remove("Facebook"));
		        printList(wordsList);

		        System.out.printf("%n%n------- Set -------%n%n");
		        Set<String> wordsHashSet = createHashSet(words);
		        printSet(wordsHashSet);
		        Set<String> wordsTreeSet = createTreeSet(words);
		        printSet(wordsTreeSet);

		        System.out.printf("%n%n------- Zusatz -------%n%n");
		        printList(findDoubletsTwice(wordsList));
		        printList(findDoubletsOnce(wordsList));

		        System.out.printf("%n%n------- Operationen ueber Mengen -------%n%n");

		        Set<Integer> s2 = Set.of(5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15);    // immutable set

		        Set<Integer> s1 = createIntegerSet(1, 10);  // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
		        s1.addAll(s2);          // Vereinigung
		        printIntegerSet(s1);       // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15

		        Set<Integer> s3 = createIntegerSet(1, 10);  // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
		        s3.removeAll(s2);       // Differenz
		        printIntegerSet(s3);       // 1, 2, 3, 4

		        Set<Integer> s4 = createIntegerSet(1, 10);  // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
		        s4.retainAll(s2);       // Schnitt
		        printIntegerSet(s4);       // 5, 6, 7, 8, 9, 10
		    }
		}
		```


##### Übung 7 (Maps)

??? "Übung 7"

	1. Erstellen Sie eine Klasse `Stadt` mit folgenden Objektvariablen:
		- `String name;`
		- `List<Integer> bevoelkerung;`
		- `float flaeche;`

	2. Erstellen Sie für die Klasse `Stadt` einen parametrisierten Konstruktor `public Stadt(String name, List<Integer> bevoelkerung, float flaeche)`, der die Objektvariablen initialisiert.
	3. Erstellen Sie für die Klasse `Stadt` eine `print()`-Methode, so dass eine Ausgabe auf der Konsole in folgender Form erscheint (Bsp.):
		```bash
		Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		```
	4. Erstellen Sie eine Klasse `StadtTest` mit `main()`-Methode. Kopieren Sie in die Klasse die Methode `public static Stadt[] staedte()` hinein:
		```java
		public static Stadt[] staedte()
		{
			Stadt[] staedte = new Stadt[6];
			List<Integer> berlinBevoelkerung = new ArrayList<>();
			berlinBevoelkerung.add(3382169);	
			berlinBevoelkerung.add(3460725);	
			berlinBevoelkerung.add(3574830);
			staedte[0] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);
			
			List<Integer> hamburgBevoelkerung = new ArrayList<>();
			hamburgBevoelkerung.add(1715392);	
			hamburgBevoelkerung.add(1786448);	
			hamburgBevoelkerung.add(1810438);	
			staedte[1] = new Stadt("Hamburg", hamburgBevoelkerung, 755.22f);
			
			List<Integer> muenchenBevoelkerung = new ArrayList<>();
			muenchenBevoelkerung.add(1210223);	
			muenchenBevoelkerung.add(1353186);	
			muenchenBevoelkerung.add(1464301);
			staedte[2] = new Stadt("Muenchen", muenchenBevoelkerung, 310.70f);
			
			List<Integer> koelnBevoelkerung = new ArrayList<>();
			koelnBevoelkerung.add(962884);	
			koelnBevoelkerung.add(1007119);	
			koelnBevoelkerung.add(1075935);	
			staedte[3] = new Stadt("Koeln", koelnBevoelkerung, 405.02f);
			
			List<Integer> frankfurtBevoelkerung = new ArrayList<>();
			frankfurtBevoelkerung.add(648550);	
			frankfurtBevoelkerung.add(679664);	
			frankfurtBevoelkerung.add(736414);
			staedte[4] = new Stadt("Frankfurt/Main", frankfurtBevoelkerung, 248.31f);
			
			berlinBevoelkerung = new ArrayList<>();
			berlinBevoelkerung.add(3382169);	
			berlinBevoelkerung.add(3460725);	
			berlinBevoelkerung.add(3574830);
			staedte[5] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);
			
			return staedte;
		}		
		```

	**Liste**

	5. Erstellen Sie in der `main()`-Methode eine `List<Stadt> staedteListe = new ArrayList<>();`. Fügen Sie der `staedteListe` alle Städte aus dem durch Aufruf der `staedte()`-Methode erzeugtem Array zu.
	6. Geben Sie alle Informationen über alle Städte aus der Liste unter Verwendung der `print()`-Methode aus der Klasse `Stadt` aus.

	**Menge**

	5. Erstellen Sie in der `main()`-Methode eine `Set<Stadt> staedteMenge = new HashSet<>();`. Fügen Sie der `staedteMenge` alle Städte aus dem durch Aufruf der `staedte()`-Methode erzeugtem Array zu.
	6. Geben Sie alle Informationen über alle Städte aus der Menge unter Verwendung der `print()`-Methode aus der Klasse `Stadt` aus.
	7. Berlin erscheint doppelt, obwohl eine Menge keine doppelten Elemente enthalten darf. Warum?

	**Stadt - Teil 2**

	5. Implementieren Sie in der Klasse `Stadt` die `equals(Object)`- und die `hashCode()`-Methode.
	6. Führen Sie danach die `StadtTest`-Klasse erneut aus. Was hat sich an der Menge geändert?

	**Maps**

	5. Erstellen Sie in der `main()`-Methode eine `Map<Integer, Stadt> staedteMap = new HashMap<>();`. Fügen Sie der `staedteMap` einen fortlaufenden, eindeutigen `Integer`-Wert beginnend mit `1` als *Key* sowie alle Städte aus dem durch Aufruf der `staedte()`-Methode erzeugtem Array als *Value* hinzu.
	6. Geben Sie alle Informationen über alle Städte aus der Liste unter Verwendung der `print()`-Methode aus der Klasse `Stadt` aus. Beginnen Sie die Zeile jeweils mit der Ausgabe des *Keys*.

	**Ausgaben**

	```bash
	------------ Liste --------------
	Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
	Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
	Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
	Koeln              405,02 km2      962.884   1.007.119   1.075.935
	Frankfurt/Main     248,31 km2      648.550     679.664     736.414
	Berlin             891,68 km2    3.382.169   3.460.725   3.574.830

	------------ Menge --------------
	Frankfurt/Main     248,31 km2      648.550     679.664     736.414
	Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
	Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
	Koeln              405,02 km2      962.884   1.007.119   1.075.935
	Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438

	------------ Maps --------------
	1  Berlin            891,68 km2    3.382.169   3.460.725   3.574.830
	2  Hamburg           755,22 km2    1.715.392   1.786.448   1.810.438
	3  Muenchen          310,70 km2    1.210.223   1.353.186   1.464.301
	4  Koeln             405,02 km2      962.884   1.007.119   1.075.935
	5  Frankfurt/Main    248,31 km2      648.550     679.664     736.414
	6  Berlin            891,68 km2    3.382.169   3.460.725   3.574.830
	``` 


??? success "Eine mögliche Lösung für Übung 7"
	=== "Stadt.java"
		```java
		package uebungen.uebung7;

		import java.util.List;

		public class Stadt
		{
		    private String name;
		    private List<Integer> bevoelkerung;
		    private float flaeche;

		    public Stadt(String name, List<Integer> bevoelkerung, float flaeche)
		    {
		        this.name = name;
		        this.bevoelkerung = bevoelkerung;
		        this.flaeche = flaeche;
		    }

		    @Override
		    public String toString()
		    {
		        String s = String.format("%-15s %8.2f km%c", this.name, this.flaeche, '\u00B2');
		        for(Integer bevoelkerung : bevoelkerung)
		        {
		            s+=String.format(" %,10d", bevoelkerung);
		        }
		        return s;
		    }

		    public void print()
		    {
		        System.out.println(this.toString());
		    }

		    @Override
		    public boolean equals(Object o)
		    {
		        if (this == o) return true;
		        if (o == null || getClass() != o.getClass()) return false;
		        Stadt stadt = (Stadt) o;
		        return this.name.equals(stadt.name) && this.flaeche == stadt.flaeche;
		    }

		    @Override
		    public int hashCode()
		    {
		        return this.name.hashCode() + Float.valueOf(this.flaeche).hashCode();
		    }
		}

		```
	=== "StadtTest.java"
		```java
		package uebungen.uebung7;

		import java.util.*;

		public class StadtTest
		{
		    public static Stadt[] staedte()
		    {
		        Stadt[] staedte = new Stadt[6];
		        List<Integer> berlinBevoelkerung = new ArrayList<>();
		        berlinBevoelkerung.add(3382169);
		        berlinBevoelkerung.add(3460725);
		        berlinBevoelkerung.add(3574830);
		        staedte[0] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);

		        List<Integer> hamburgBevoelkerung = new ArrayList<>();
		        hamburgBevoelkerung.add(1715392);
		        hamburgBevoelkerung.add(1786448);
		        hamburgBevoelkerung.add(1810438);
		        staedte[1] = new Stadt("Hamburg", hamburgBevoelkerung, 755.22f);

		        List<Integer> muenchenBevoelkerung = new ArrayList<>();
		        muenchenBevoelkerung.add(1210223);
		        muenchenBevoelkerung.add(1353186);
		        muenchenBevoelkerung.add(1464301);
		        staedte[2] = new Stadt("Muenchen", muenchenBevoelkerung, 310.70f);

		        List<Integer> koelnBevoelkerung = new ArrayList<>();
		        koelnBevoelkerung.add(962884);
		        koelnBevoelkerung.add(1007119);
		        koelnBevoelkerung.add(1075935);
		        staedte[3] = new Stadt("Koeln", koelnBevoelkerung, 405.02f);

		        List<Integer> frankfurtBevoelkerung = new ArrayList<>();
		        frankfurtBevoelkerung.add(648550);
		        frankfurtBevoelkerung.add(679664);
		        frankfurtBevoelkerung.add(736414);
		        staedte[4] = new Stadt("Frankfurt/Main", frankfurtBevoelkerung, 248.31f);

		        berlinBevoelkerung = new ArrayList<>();
		        berlinBevoelkerung.add(3382169);
		        berlinBevoelkerung.add(3460725);
		        berlinBevoelkerung.add(3574830);
		        staedte[5] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);

		        return staedte;
		    }

		    public static void print(Collection<Stadt> staedte)
		    {
		        for(Stadt staedt : staedte)
		        {
		            System.out.println(staedt);
		        }
		        System.out.println();
		    }

		    public static void main(String[] args)
		    {
		        Stadt[] staedte = staedte();
		        System.out.printf("%n%n-------------- List ---------------------%n%n");
		        List<Stadt> staedteListe = Arrays.asList(staedte);
		        print(staedteListe);

		        System.out.printf("%n%n-------------- Set ---------------------%n%n");
		        Set<Stadt> staedteSet = new HashSet<>(Arrays.asList(staedte));
		        print(staedteSet);

		        System.out.printf("%n%n-------------- Map ---------------------%n%n");
		        Map<Integer, Stadt> staedteMap = new HashMap<>();
		        Integer key = 1;    // auto-boxing
		        for(Stadt stadt : staedte)
		        {
		            staedteMap.put(key, stadt);
		            key++;
		        }
		        for(Map.Entry<Integer, Stadt> entry : staedteMap.entrySet())        // all key-value-pairs
		        {
		            Integer entryKey = entry.getKey();          // the key of the pair
		            Stadt entryValue = entry.getValue();        // the value of the pair
		            System.out.println(entryKey + " " + entryValue);
		        }
		    }
		}

		```


##### Übung 8 (Interfaces)

??? "Übung 8"

	1. Wir beschäftigen uns nochmal mit der Übung 7, d.h. mit `Stadt` und `StadtTest`. Dieses Mal geht es uns aber mehr um die Verwendung des Interfaces `Comparable`. Zunächst sind die beiden Klassen `Stadt` und `StadtTest` wie folgt gegeben: (das haben wir so in Übung 7 erarbeitet - es gibt eine Änderung in `StadtTest`: dort benutzen wir jetzt in der `Map` `MyInteger` anstatt `Integer` - siehe 2.): 

		=== "Stadt.java" 
			```java
			import java.util.*;

			public class Stadt
			{
				String name;
				List<Integer> bevoelkerung;
				float flaeche;
				
				public Stadt(String name, List<Integer> bevoelkerung, float flaeche)
				{
					super();
					this.name = name;
					this.bevoelkerung = bevoelkerung;
					this.flaeche = flaeche;
				}
				
				void print()
				{
					System.out.printf("%-18s %.2f km%c", this.name, this.flaeche, '\u00B2');
					for(Integer anzahl : this.bevoelkerung)
					{
						System.out.printf("%,14d", anzahl);
					}
					System.out.println();
				}
				
				@Override
				public boolean equals(Object o)
				{
					if(o==null) return false;
					if(o==this) return true;
					if(this.getClass()!=o.getClass()) return false;
					
					Stadt other = (Stadt)o;
					return (this.name.equals(other.name));
				}
				
				@Override
				public int hashCode()
				{
					return this.name.hashCode();
				}

			}
			```

		=== "StadtTest.java" 
			```java
			import java.util.*;
			
			public class StadtTest
			{
				public static Stadt[] staedte()
				{
					Stadt[] staedte = new Stadt[6];
					List<Integer> berlinBevoelkerung = new ArrayList<>();
					berlinBevoelkerung.add(3382169);	
					berlinBevoelkerung.add(3460725);	
					berlinBevoelkerung.add(3574830);
					staedte[0] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);
					
					List<Integer> hamburgBevoelkerung = new ArrayList<>();
					hamburgBevoelkerung.add(1715392);	
					hamburgBevoelkerung.add(1786448);	
					hamburgBevoelkerung.add(1810438);	
					staedte[1] = new Stadt("Hamburg", hamburgBevoelkerung, 755.22f);
					
					List<Integer> muenchenBevoelkerung = new ArrayList<>();
					muenchenBevoelkerung.add(1210223);	
					muenchenBevoelkerung.add(1353186);	
					muenchenBevoelkerung.add(1464301);
					staedte[2] = new Stadt("Muenchen", muenchenBevoelkerung, 310.70f);
					
					List<Integer> koelnBevoelkerung = new ArrayList<>();
					koelnBevoelkerung.add(962884);	
					koelnBevoelkerung.add(1007119);	
					koelnBevoelkerung.add(1075935);	
					staedte[3] = new Stadt("Koeln", koelnBevoelkerung, 405.02f);
					
					List<Integer> frankfurtBevoelkerung = new ArrayList<>();
					frankfurtBevoelkerung.add(648550);	
					frankfurtBevoelkerung.add(679664);	
					frankfurtBevoelkerung.add(736414);
					staedte[4] = new Stadt("Frankfurt/Main", frankfurtBevoelkerung, 248.31f);
					
					berlinBevoelkerung = new ArrayList<>();
					berlinBevoelkerung.add(3382169);	
					berlinBevoelkerung.add(3460725);	
					berlinBevoelkerung.add(3574830);
					staedte[5] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);
					
					return staedte;
				}
				
				public static void main(String[] args)
				{
					System.out.printf("%n------------ Menge --------------%n");
					Set<Stadt> staedteMenge = new HashSet<>();
					for(Stadt s : staedte())
					{
						staedteMenge.add(s);
					}
					for(Stadt s : staedteMenge)
					{
						s.print();
					}
					
					System.out.printf("%n------------ Maps --------------%n");
					Map<MyInteger, Stadt> staedteMap = new HashMap<>();
					int i = 1;
					for(Stadt s : staedte())
					{
						staedteMap.put(new MyInteger(i++), s);
					}
					for(Map.Entry<MyInteger, Stadt> entry : staedteMap.entrySet())
					{
						MyInteger key = entry.getKey();
						System.out.printf("%-3d",key.intValue());
						entry.getValue().print();
					}
				}
			}
			```

	2. Für die Schlüssel in der `Map` benutzen wir die selbstgeschriebne Klasse `MyInteger`:

		=== "MyInteger.java" 
		```java
		public class MyInteger 
		{
			private int value;
			
			public MyInteger(int value)
			{
				this.value = value;
			}
			
			public int intValue()
			{
				return this.value;
			}
			
			public static MyInteger valueOf(int value)
			{
				return new MyInteger(value);
			}
		}
		```

	3. Ändern Sie in der `StadtTest.java` den Konstruktoraufruf der `Set` von `HashSet` nach `TreeSet` und führen Sie die Klasse aus - es wird eine Exception geworfen (`Stadt cannot be cast to class java.lang.Comparable`). Implementieren Sie für `Stadt` das Interface `Comparable<Stadt>` so, dass nach den Namen der Städte sortiert wird. Führen Sie dann erneut `StadtTest.java` aus. Es sollte folgende Ausgabe für die `Set` erzeugt werden:

		```bash
		------------ Menge --------------
		Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		Koeln              405,02 km2      962.884   1.007.119   1.075.935
		Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		```

	4. Ändern Sie `compareTo()` in `Stadt` so, dass die Namen der Städte **absteigend** sortiert werden und führen Sie dann `StadtTest.java` erneut aus. Es sollte folgende Ausgabe erzeugt werden:

		```bash
		------------ Menge --------------
		Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		Koeln              405,02 km2      962.884   1.007.119   1.075.935
		Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		```

	5. Ändern Sie `compareTo()` in `Stadt` so, dass die Städte **absteigend** nach ihrer Fläche sortiert werden und führen Sie dann `StadtTest.java` erneut aus. Es sollte folgende Ausgabe erzeugt werden:

		```bash
		------------ Menge --------------
		Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		Koeln              405,02 km2      962.884   1.007.119   1.075.935
		Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		```

	6. Ändern Sie in der `StadtTest.java` den Konstruktoraufruf der `Map` von `HashMap` nach `TreeMap` und führen Sie die Klasse aus - es wird eine Exception geworfen (`MyInteger cannot be cast to class java.lang.Comparable`). Implementieren Sie für `MyInteger` das Interface `Comparable<MyInteger>` so, dass nach den Größen der Werte sortiert wird. Führen Sie dann erneut `StadtTest.java` aus. Es sollte folgende Ausgabe für die `Map` erzeugt werden:

		```bash
		------------ Maps --------------
		1  Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		2  Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		3  Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		4  Koeln              405,02 km2      962.884   1.007.119   1.075.935
		5  Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		6  Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		```

	7. Ändern Sie `compareTo()` in `MyInteger` so, dass die Werte der Schlüssel **absteigend** sortiert werden und führen Sie dann `StadtTest.java` erneut aus. Es sollte folgende Ausgabe erzeugt werden:

		```bash
		------------ Maps --------------
		6  Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		5  Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		4  Koeln              405,02 km2      962.884   1.007.119   1.075.935
		3  Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		2  Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		1  Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		```

	- **Zusatz**: Schreiben Sie in `StadtTest.java` eine Methode `public static boolean contains(Map<MyInteger, Stadt> staedteMap, Stadt stadt)`, die ein `true` zurückgibt, wenn die Stadt `stadt` bereits in der `staedteMap` als ein `value` existiert. Testen Sie die Methode, indem Sie zur Menge nur dann die `stadt` hinzufügen, wenn sie nicht bereits in der Menge aufgeführt ist. Sie sollten folgende Ausgabe erhalten: 

		```bash
		------------ Maps --------------
		5  Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		4  Koeln              405,02 km2      962.884   1.007.119   1.075.935
		3  Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		2  Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		1  Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		```

??? success "mögliche Lösung für Übung 8"
	
	=== "Stadt.java"
		```java linenums="1"
		package uebungen.uebung8;

		import java.util.*;

		public class Stadt implements Comparable<Stadt>
		{
		    String name;
		    List<Integer> bevoelkerung;
		    float flaeche;

		    public Stadt(String name, List<Integer> bevoelkerung, float flaeche)
		    {
		        super();
		        this.name = name;
		        this.bevoelkerung = bevoelkerung;
		        this.flaeche = flaeche;
		    }

		    void print()
		    {
		        System.out.printf("%-18s %.2f km%c", this.name, this.flaeche, '\u00B2');
		        for(Integer anzahl : this.bevoelkerung)
		        {
		            System.out.printf("%,14d", anzahl);
		        }
		        System.out.println();
		    }

		    @Override
		    public boolean equals(Object o)
		    {
		        if(o==null) return false;
		        if(o==this) return true;
		        if(this.getClass()!=o.getClass()) return false;

		        Stadt other = (Stadt)o;
		        return (this.name.equals(other.name));
		    }

		    @Override
		    public int hashCode()
		    {
		        return this.name.hashCode();
		    }

			@Override
			public int compareTo(Stadt o) 
			{
				//return o.name.compareTo(this.name);
				if(this.flaeche > o.flaeche) return 1;
				else if(this.flaeche < o.flaeche) return -1;
				else return 0;
			}

		}

		```

	=== "MyInteger.java"
		```java linenums="1"
		package uebungen.uebung8;

		public class MyInteger implements Comparable<MyInteger>
		{
		    private int value;

		    public MyInteger(int value)
		    {
		        this.value = value;
		    }

		    public int intValue()
		    {
		        return this.value;
		    }

		    public static MyInteger valueOf(int value)
		    {
		        return new MyInteger(value);
		    }

			@Override
			public int compareTo(MyInteger o) 
			{
				return (this.value - o.value);
			}

		}

		```

	=== "StadtTest.java"
		```java linenums="1"
		package uebungen.uebung8;

		import java.util.*;

		public class StadtTest
		{
		    public static Stadt[] staedte()
		    {
		        Stadt[] staedte = new Stadt[6];
		        List<Integer> berlinBevoelkerung = new ArrayList<>();
		        berlinBevoelkerung.add(3382169);    
		        berlinBevoelkerung.add(3460725);    
		        berlinBevoelkerung.add(3574830);
		        staedte[0] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);

		        List<Integer> hamburgBevoelkerung = new ArrayList<>();
		        hamburgBevoelkerung.add(1715392);   
		        hamburgBevoelkerung.add(1786448);   
		        hamburgBevoelkerung.add(1810438);   
		        staedte[1] = new Stadt("Hamburg", hamburgBevoelkerung, 755.22f);

		        List<Integer> muenchenBevoelkerung = new ArrayList<>();
		        muenchenBevoelkerung.add(1210223);  
		        muenchenBevoelkerung.add(1353186);  
		        muenchenBevoelkerung.add(1464301);
		        staedte[2] = new Stadt("Muenchen", muenchenBevoelkerung, 310.70f);

		        List<Integer> koelnBevoelkerung = new ArrayList<>();
		        koelnBevoelkerung.add(962884);  
		        koelnBevoelkerung.add(1007119); 
		        koelnBevoelkerung.add(1075935); 
		        staedte[3] = new Stadt("Koeln", koelnBevoelkerung, 405.02f);

		        List<Integer> frankfurtBevoelkerung = new ArrayList<>();
		        frankfurtBevoelkerung.add(648550);  
		        frankfurtBevoelkerung.add(679664);  
		        frankfurtBevoelkerung.add(736414);
		        staedte[4] = new Stadt("Frankfurt/Main", frankfurtBevoelkerung, 248.31f);

		        berlinBevoelkerung = new ArrayList<>();
		        berlinBevoelkerung.add(3382169);    
		        berlinBevoelkerung.add(3460725);    
		        berlinBevoelkerung.add(3574830);
		        staedte[5] = new Stadt("Berlin", berlinBevoelkerung, 891.68f);

		        return staedte;
		    }
		    
		    public static boolean contains(Map<MyInteger, Stadt> staedteMap, Stadt stadt)
		    {
		    	/*
		    	// ueber alle Values
		    	Collection<Stadt> alleStaedte = staedteMap.values();
		    	for(Stadt s : alleStaedte)
		    	{
		    		if(s.equals(stadt)) return true;
		    	}
		    	return false;
		    	*/
		    	
		    	/*
		    	// ueber alle Keys
		    	Set<MyInteger> alleSchluessel = staedteMap.keySet();
		    	for(MyInteger schluessel : alleSchluessel)
		    	{
		    		Stadt s = staedteMap.get(schluessel);
		    		if(s.equals(stadt)) return true;
		    	}
		    	return false;
		    	*/
		    	
		    	// uber alle Schluessel-Werte-Paare
		    	Set<Map.Entry<MyInteger, Stadt>> alleEintraege = staedteMap.entrySet();
		    	for(Map.Entry<MyInteger, Stadt> eintrag : alleEintraege)
		    	{
		    		Stadt s = eintrag.getValue();
		    		if(s.equals(stadt)) return true;
		    	}
		    	return false;
		    }

		    public static void main(String[] args)
		    {
		        System.out.printf("%n------------ Menge --------------%n");
		        Set<Stadt> staedteMenge = new TreeSet<>();
		        for(Stadt s : staedte())
		        {
		            staedteMenge.add(s);
		        }
		        for(Stadt s : staedteMenge)
		        {
		            s.print();
		        }

		        System.out.printf("%n------------ Maps --------------%n");
		        Map<MyInteger, Stadt> staedteMap = new TreeMap<>();
		        int i = 1;
		        for(Stadt s : staedte())
		        {
		        	if(!contains(staedteMap, s)) {
		        		staedteMap.put(new MyInteger(i++), s);
		        	}
		        }
		        for(Map.Entry<MyInteger, Stadt> entry : staedteMap.entrySet())
		        {
		            MyInteger key = entry.getKey();
		            System.out.printf("%-3d",key.intValue());
		            entry.getValue().print();
		        }
		    }
		}

		```

##### Übung 9 (Lambdas + Functional Interface Comparator)

??? "Übung 9"

	**Vorbereitung**

	1. Kopieren Sie folgende Klassen in Ihr Package `uebungen.uebung9` (oder `package` anpassen):

		=== "Student.java"
			```java
			package uebungen.uebung9;

			public record Student(String name, String registrationNumber, int age, double gradePointAverage, int semester)
			{
			    // record besitzt automatisch alle Getter (aber ohne get im Namen :-( )
			    // record besitzt automatisch equals(), hashCode() und toString()
			    // toString() ueberschreiben wir aber lieber selbst:
			    @Override
			    public String toString()
			    {
			        return String.format("(%-8s, %s, %2d Jahre, %d. Semester, %c%.1f)",
			                this.name, this.registrationNumber, this.age, this.semester, '\u2300', this.gradePointAverage);
			    }

			    public void print()
			    {
			        System.out.println(this.toString());
			    }
			}
			```

		=== "Uebung9.java"
			```java
			package uebungen.uebung9;

			import java.util.*;

			public class Uebung9
			{
			    private static List<Student> generateMockupData(int length) {
			        List<Student> studentsList = new ArrayList<>();
			        String[] names = {"Alex", "Jamie", "Jordan", "Taylor", "Morgan",
			                "Riley", "Casey", "Drew", "Reese", "Quinn",
			                "Sydney", "Dakota", "Avery", "Blake", "Cameron",
			                "Harper", "Hayden", "Charlie", "Bailey", "Peyton",
			                "Skyler", "Jesse", "Kendall", "Logan", "Parker",
			                "Rowan", "Sawyer", "Finley", "Skylar", "Emerson"};  // hat ChatGPT gemacht
			        Random random = new Random();

			        for (int i = 0; i < length; i++) {
			            String name = names[random.nextInt(names.length)];
			            int number = 10000 + random.nextInt(90000);
			            String registrationNumber = "s05" + number;
			            int age = 18 + random.nextInt(20);                    // Alter zwischen 18 und 37
			            double gradePointAverage = 1.0 + random.nextDouble() * 3.0; // GPA zwischen 1.0 und 4.0
			            int semester = 1 + random.nextInt(9);                 // Semester zwischen 1 and 9
			            
			            studentsList.add(new Student(name, registrationNumber, age, gradePointAverage, semester));
			        }
			        return studentsList;
			    }

			    public static void printStudents(List<Student> students)
			    {
			        for(Student student : students)
			        {
			            student.print();
			        }
			    }

			    public static void main(String[] args)
			    {
			        List<Student> students = generateMockupData(15);
			        printStudents(students);

			        System.out.printf("%n%n----------- Namen aufsteigend --------------%n%n");

			    }
			}
			```


	**Vorbetrachtungen**

	2. In dem Interface [List](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/List.html) gibt es die Sortiermethode `sort(Comparator<T> c)`. Diese erwartet ein [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html)-Objekt.
	3. [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html) ist ein *Functional Interface* mit der *single abstract method (SAM)* `compare(T o1, T o2)`. Überall, wo ein `Comparator` erwartet wird (siehe [hier](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/class-use/Comparator.html)), kann also z.B. ein *Lambda* mit 2 Parametern, z.B. `(o1, o2) -> o1.compareTo(o2)` übergeben werden. 
	4. [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html) besitzt außerdem eine statische erzeugende `default`-Methode `comparing(Function keyExtractor, Comparator keyComparator)`. Diese gibt ein `Comparator`-Objekt zurück. Eine [Function](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/Function.html) wendet eine *Funktion* (Methode) auf ein Argument an, z.B. `o1 -> o1.name()` wendet den *getter* `name()` auf das `o1`-Objekt an. Hier bietet sich jedoch [Methodenreferenz](lambdas.md#methoden-referenzen) an, z.B. `Student::name`. Mit der `Function` kann definiert (extrahiert) werden, welche Schlüssel zum Vergleich verwendet werden. 


	**Aufgabe**

	1. Ändern Sie die `printStudents()` so, dass die `forEach(Consumer action)`-Methode für Listen angewendet wird (kommt aus [Iterable](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Iterable.html) - einem Interface, das Listen implementiert haben). Ein [Consumer](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/function/Consumer.html) ist ähnlich einer `Function` (erwartet ein Argument), gibt aber nichts zurück. Es bieten sich also die `System.out.println()`-Methode oder die `print()`-Methode aus `Student` an. 
	2. Sortieren Sie die `studentsList` nach jeweils Matrikelnummer und Namen, jeweils auf- und absteigend (4 Sortierungen). 
	3. Schauen Sie sich die `comparingDouble(ToDoubleFunction keyExtractor)`-Methode in [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html) an. Wie kann sie verwendet werden, um nach den Noten zu sortieren? Finden Sie in [Comparator](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Comparator.html) eine Möglichkeit, um nach Noten absteigend zu sortieren? 
	4. Die statische erzeugende Methode `naturalOrder()` erzeugt ein `Comparator`-Objekt, das verwendet werden kann, um Objekte in ihrer *"natürlichen Ordnung"* zu sortieren. Wenn wir jedoch `Comparator<Student> naturalOrder = Comparator.naturalOrder();` eingeben, erhalten wir einen Fehler. Warum und wie lässt er sich beheben? 


??? success "mögliche Lösung für Übung 9"
	
	=== "Uebung9.java"
		```java
		package uebungen.uebung9;

		import java.util.ArrayList;
		import java.util.Comparator;
		import java.util.List;
		import java.util.Random;

		public class Uebung9
		{
		    private static List<Student> generateMockupData(int length) {
		        List<Student> studentsList = new ArrayList<>();

		        String[] names = {"Alex", "Jamie", "Jordan", "Taylor", "Morgan",
		                "Riley", "Casey", "Drew", "Reese", "Quinn",
		                "Sydney", "Dakota", "Avery", "Blake", "Cameron",
		                "Harper", "Hayden", "Charlie", "Bailey", "Peyton",
		                "Skyler", "Jesse", "Kendall", "Logan", "Parker",
		                "Rowan", "Sawyer", "Finley", "Skylar", "Emerson"};  // hat ChatGPT gemacht

		        Random random = new Random();

		        for (int i = 0; i < length; i++) {
		            String name = names[random.nextInt(names.length)];
		            int number = 10000 + random.nextInt(90000);
		            String registrationNumber = "s05" + number;
		            int age = 18 + random.nextInt(20);                    // Alter zwischen 18 und 37
		            double gradePointAverage = 1.0 + random.nextDouble() * 3.0; // GPA zwischen 1.0 und 4.0
		            int semester = 1 + random.nextInt(9);                 // Semester zwischen 1 and 9

		            // Liste befuellen
		            studentsList.add(new Student(name, registrationNumber, age, gradePointAverage, semester));
		        }
		        return studentsList;
		    }

		    public static void printStudents(List<Student> students)
		    {
		        /*
		        for(Student student : students)
		        {
		            student.print();
		        }
		        */
		         students.forEach( s -> s.print() );
		    }

		    public static void main(String[] args)
		    {
		        List<Student> students = generateMockupData(15);
		        printStudents(students);

		        // das geht
		        Comparator<Student> nachNamenAufsteigend = (s1, s2) -> s1.name().compareTo(s2.name());

		        // oder das
		        nachNamenAufsteigend = new Comparator<Student>() {
		            @Override
		            public int compare(Student o1, Student o2)
		            {
		                return o1.name().compareTo(o2.name());
		            }
		        };

		        // oder das
		        nachNamenAufsteigend = Comparator.comparing( s -> s.name() );


		        System.out.printf("%n%n----------- Namen aufsteigend --------------%n%n");
		        students.sort( nachNamenAufsteigend );
		        printStudents(students);

		        System.out.printf("%n%n----------- Namen absteigend --------------%n%n");
		        //students.sort( (s1, s2) -> -s1.name().compareTo(s2.name()) );
		        students.sort( nachNamenAufsteigend.reversed() );
		        printStudents(students);

		        System.out.printf("%n%n----------- Noten aufsteigend --------------%n%n");
		        students.sort( (s1, s2) -> {
		            if (s1.gradePointAverage() > s2.gradePointAverage()) return 1;
		            else if (s1.gradePointAverage() < s2.gradePointAverage()) return -1;
		            else return 0;
		        } );

		        Comparator<Student> nachNotenAufsteigend = Comparator.comparingDouble( s -> s.gradePointAverage() );

		        System.out.printf("%n%n----------- Natural order --------------%n%n");
		        Comparator<Student> naturalOrder = Comparator.naturalOrder();
		        students.sort( naturalOrder );		// dazu muss Comparable>Student> in Student implementiert werden!!!
		        printStudents(students);
		    }
		}
		```



##### Übung 10 (Streams)

??? "Übung 10"

	**Vorbereitung**

	1. Wir nehmen wieder exakt die gleichen Klassen, wie in [Übung 9](uebungen.md#ubung-9-lambdas-functional-interface-comparator). Entweder Sie machen einfach in Übung 9 weiter oder Sie kopieren folgende Klassen in Ihr Package `uebungen.uebung10` (oder `package` anpassen):

		=== "Student.java"
			```java
			package uebungen.uebung10;

			public record Student(String name, String registrationNumber, int age, double gradePointAverage, int semester)
			{
			    // record besitzt automatisch alle Getter (aber ohne get im Namen :-( )
			    // record besitzt automatisch equals(), hashCode() und toString()
			    // toString() ueberschreiben wir aber lieber selbst:
			    @Override
			    public String toString()
			    {
			        return String.format("(%-8s, %s, %2d Jahre, %d. Semester, %c%.1f)",
			                this.name, this.registrationNumber, this.age, this.semester, '\u2300', this.gradePointAverage);
			    }

			    public void print()
			    {
			        System.out.println(this.toString());
			    }
			}
			```

		=== "Uebung10.java"
			```java
			package uebungen.uebung10;

			import java.util.*;

			public class Uebung10
			{
			    private static List<Student> generateMockupData(int length) {
			        List<Student> studentsList = new ArrayList<>();
			        String[] names = {"Alex", "Jamie", "Jordan", "Taylor", "Morgan",
			                "Riley", "Casey", "Drew", "Reese", "Quinn",
			                "Sydney", "Dakota", "Avery", "Blake", "Cameron",
			                "Harper", "Hayden", "Charlie", "Bailey", "Peyton",
			                "Skyler", "Jesse", "Kendall", "Logan", "Parker",
			                "Rowan", "Sawyer", "Finley", "Skylar", "Emerson"};  // hat ChatGPT gemacht
			        Random random = new Random();

			        for (int i = 0; i < length; i++) {
			            String name = names[random.nextInt(names.length)];
			            int number = 10000 + random.nextInt(90000);
			            String registrationNumber = "s05" + number;
			            int age = 18 + random.nextInt(20);                    // Alter zwischen 18 und 37
			            double gradePointAverage = 1.0 + random.nextDouble() * 3.0; // GPA zwischen 1.0 und 4.0
			            int semester = 1 + random.nextInt(9);                 // Semester zwischen 1 and 9
			            
			            studentsList.add(new Student(name, registrationNumber, age, gradePointAverage, semester));
			        }
			        return studentsList;
			    }

			    public static void printStudents(List<Student> students)
			    {
			        for(Student student : students)
			        {
			            student.print();
			        }
			    }

			    public static void main(String[] args)
			    {
			        List<Student> students = generateMockupData(15);
			        printStudents(students);

			        System.out.printf("%n%n----------- Liste von Namen erzeugen --------------%n%n");

			    }
			}
			```


	**Aufgabe**

	1. Erzeugen Sie eine Liste aller Namen aus `students`. Achten Sie darauf, dass kein Name doppelt vorkommt. 

	2. Erzeugen Sie eine Liste aller Studierenden aus `students`, die älter als 23 Jahre alt sind. 

	3. Ermitteln Sie die Studierende mit dem besten Notendurchschnitt. 

	4. Ermitteln Sie die Studierende mit dem besten Notendurchschnitt, die mindestens im 6. Semester ist. 

	5. Berechnen Sie den Altersdurchschnitt aller Studierenden aus `students`. 

	6. Erzeugen Sie eine `Map`, die alle Studierende aus `students` nach Semestern gruppiert.

	7. Wir denken uns noch weitere solcher Aufgaben aus, falls noch Zeit ist ...


??? success "mögliche Lösung für Übung 10"
	
	=== "Uebung10.java"
		```java
		package uebungen.uebung10b;

		import java.util.*;
		import java.util.stream.Collectors;

		public class Uebung10
		{
		    private static List<Student> generateMockupData(int length) {
		        List<Student> studentsList = new ArrayList<>();
		        String[] names = {"Alex", "Jamie", "Jordan", "Taylor", "Morgan",
		                "Riley", "Casey", "Drew", "Reese", "Quinn",
		                "Sydney", "Dakota", "Avery", "Blake", "Cameron",
		                "Harper", "Hayden", "Charlie", "Bailey", "Peyton",
		                "Skyler", "Jesse", "Kendall", "Logan", "Parker",
		                "Rowan", "Sawyer", "Finley", "Skylar", "Emerson"};  // hat ChatGPT gemacht
		        Random random = new Random();

		        for (int i = 0; i < length; i++) {
		            String name = names[random.nextInt(names.length)];
		            int number = 10000 + random.nextInt(90000);
		            String registrationNumber = "s05" + number;
		            int age = 18 + random.nextInt(20);                    // Alter zwischen 18 und 37
		            double gradePointAverage = 1.0 + random.nextDouble() * 3.0; // GPA zwischen 1.0 und 4.0
		            int semester = 1 + random.nextInt(9);                 // Semester zwischen 1 and 9

		            studentsList.add(new Student(name, registrationNumber, age, gradePointAverage, semester));
		        }
		        return studentsList;
		    }

		    public static void printStudents(List<Student> students) {
		        for(Student student : students)
		        {
		            student.print();
		        }
		    }

		    public static void main(String[] args)
		    {
		        List<Student> students = generateMockupData(15);
		        printStudents(students);

		        System.out.printf("%n%n----------- Liste von Namen erzeugen --------------%n%n");
		        List<String> namensListe = students.stream()
		                .map( s -> s.name() )  // Student-Stream nach String-Stream
		                .distinct()                     // doppelte Namen entfernen
		                .collect(Collectors.toList());
		        namensListe.forEach( s -> System.out.println(s) );

		        System.out.printf("%n%n----------- Liste von Namen erzeugen mit Doppelungen--------------%n%n");
		        students.stream()
		                .map( s -> s.name() )  // Student-Stream nach String-Stream
		                //.distinct()
		                .forEach( s -> System.out.println(s) );


		        System.out.printf("%n%n----------- Liste von Students älter als 23 --------------%n%n");
		        List<Student> studentsAelter23 = students.stream()
		                .filter( s -> s.age() > 23 )
		                .collect(Collectors.toList());
		        studentsAelter23.forEach( s -> System.out.println(s) );

		        System.out.printf("%n%n----------- Beste Studentin --------------%n%n");
		        Student beste = students.stream()
		                .min( Comparator.comparingDouble( s -> s.gradePointAverage() ) )
		                .get();
		        System.out.println(beste.toString());


		        System.out.printf("%n%n----------- Beste Studentin mind. 6 Semester--------------%n%n");
		        Student besteMind6Sem = students.stream()
		                .filter( s -> s.semester() >= 6 )
		                .min( Comparator.comparingDouble( s -> s.gradePointAverage() ) )
		                .get();
		        System.out.println(besteMind6Sem.toString());

		        System.out.printf("%n%n----------- Notendurchschnitt --------------%n%n");
		        double notendurchschnitt = students.stream()
		                .mapToDouble( s -> s.gradePointAverage() )
		                .average()
		                .getAsDouble();
		        System.out.println(notendurchschnitt);

		        System.out.printf("%n%n----------- Altersdurchschnitt --------------%n%n");
		        double altersdurchschnitt = students.stream()
		                .mapToInt( s -> s.age() )
		                .average()
		                .getAsDouble();
		        System.out.println(altersdurchschnitt);

		        System.out.printf("%n%n----------- gruppiert nach Semestern --------------%n%n");
		        Map<Integer, List<Student>> gruppiertNachSemester = students.stream()
		                .collect(Collectors.groupingBy(s -> s.semester()));

		        gruppiertNachSemester.entrySet()
		                .forEach( gruppiert -> System.out.println(
		                                gruppiert.getKey()
		                                + " : "
		                                + gruppiert.getValue()));

		        System.out.printf("%n%n----------- andere Ausgabe --------------%n%n");
		        for(Map.Entry<Integer, List<Student>> entry : gruppiertNachSemester.entrySet())
		        {
		            Integer key = entry.getKey();
		            List<Student> value = entry.getValue();
		            System.out.println("------- " + key + ". Semester -------------");
		            value.forEach( student -> System.out.println(student));
		            System.out.println();
		        }
		    }
		}

		```
		


##### Übung 11 (Streams)

??? "Übung 11 (Streams)"
	- Wir betrachten die Klasse [Random](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Random.html) aus dem `java.util`-Paket. 
	- Wie würden Sie vorgehen, um mithilfe dieser Klasse einen Stream mit `20` Zufallszahlen aus dem Bereich `[1 ... 99]` (beides inklusive) zu erzeugen? 
		- Geht es mit allen Varianten der `ints()`-Methode?
		- Für `IntStream` gibt es kein `collect(Collector c)`. Was tun?
	- Wenn wir mithilfe von `Random r = new Random();` ein `Random`-Objekt erzeugen, können wir die Methode `r.nextInt(int lowerBound, int upperBound)` anwenden. Diese Methode kommt aber in der Beschreibung von [Random](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Random.html) gar nicht vor. Woher kommt sie?
	- Während `groupingBy()` in [Collectors](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Collectors.html) eine `Function` erwartet, kann `partitioningBy()` ein `Predicate` übergeben werden. Erzeugen Sie mithilfe einer der `ints()`-Methoden einen `IntStream` von `20` Zufallszahlen aus dem Bereich `[1 ... 99]` (beides inklusive) und partitionieren Sie diesen in gerade und ungerade Zahlen mithilfe von `collect(Collectors.partitioningBy(Predicate p))`. Wie ist die entstehende `Map` typisiert? 
	- Für `Map` gibt es keine `stream()`-Methode, für `Set` aber schon. Erzeugen Sie aus der obigen `Map` wieder einen `Stream`! 
	- Wir erhalten einen Stream aus Listen. Mithilfe der Methode `flatMap(Function mapper)` kann ein solcher Stream wieder zu einem Stream aus Elementen "flachgedrückt" werden. Wie würde das aussehen? 
		- Speichern Sie den so erhaltenen Stream in eine `List<Integer>`.
		- Sorgen Sie dafür, dass in der Liste sowohl die ungeraden als auch die geraden Zahlen jeweils sortiert sind.
		- Sorgen Sie dafür, dass in der Liste erst alle geraden und dann erst alle ungeraden Zahlen aufgeführt sind. 


??? success "mögliche Lösung für Übung 11"
	
	=== "Uebung11.java"
		```java
		package uebungen.uebung11;

		import java.util.Comparator;
		import java.util.List;
		import java.util.Map;
		import java.util.Random;
		import java.util.stream.Collectors;
		import java.util.stream.IntStream;

		public class Uebung11
		{
		    public static void main(String[] args)
		    {
		        Random r = new Random();
		        IntStream s1 = r.ints(20, 1, 100);
		        s1.forEach(s -> System.out.print(s + " "));
		        System.out.println();

		        IntStream s2 = r.ints(1, 100).limit(20);
		        //s2.forEach(s -> System.out.print(s + " "));
		        List<Integer> listS2 = s2.boxed().collect(Collectors.toList());
		        listS2.forEach(s -> System.out.print(s + " "));
		        System.out.println();

		        IntStream s3 = r.ints().filter(i -> i > 0 && i < 100).limit(20);
		        Map<Boolean, List<Integer>> mapS3 = s3.boxed().collect(Collectors.partitioningBy(n -> n % 2 == 0 ));

		        mapS3.forEach( (k, v) -> System.out.print(k + " " + v));
		        System.out.println();
		        List<Integer> listMapS3 = mapS3.entrySet().stream()
		                .sorted( (e1, e2) -> e2.getKey().compareTo(e1.getKey()))
		                .flatMap( e -> e.getValue().stream().sorted() )
		                //.forEach( i -> System.out.print(i + " "));
		                .collect(Collectors.toList());
		        listMapS3.forEach( s -> System.out.print(s + " "));
		        System.out.println();
		        //s3.forEach(s -> System.out.print(s + " "));
		        System.out.println();

		        //r.nextInt(1,100);
		    }
		}

		```

##### Übung 12 (JUnit)

??? "Übung 12 (JUnit)"
	- Probieren Sie sich mit `JUnit` aus! Schreiben Sie Unit-Tests für Ihre `MyInteger`-Klasse aus [Aufgabe 2](aufgaben.md#aufgabe-2-myinteger).  
	- Testen Sie z.B. für `parseInt()`:
		```
			"1234" 			-> 1234
			"+1234"  		-> 1234
			"01234"  		-> 1234
			"-1234" 		-> -1234
			"-01234"  		-> -1234
			null			-> Exception (IAE) kein String
			""				-> Exception (IAE) leerer String
			"+"				-> Exception (IAE) nur '+' bzw. '-' --> keine Zahl
			"-"				-> Exception (IAE) nur '+' bzw. '-' --> keine Zahl
			"-00000000"		-> 0
			"+00000000"		-> 0
			"-00000001"		-> -1
			"+00000001"		->	1
			"123456a"		-> Exception (IAE) keine Zahl!
			"-123456a"		-> Exception (IAE) keine Zahl!
			"+123456a"		-> Exception (IAE) keine Zahl!
			"2147483648"	-> Exception (IAE) Zahl zu gross!
			"-2147483649"	-> Exception (IAE) Zahl zu klein!

		```

??? question "MyInteger.java"
	
	=== "MyInteger.java"
		```java linenums="1"
		package testen;

		public class MyInteger
		{
			public static final int MAX_VALUE = 2147483647;
			public static final int MIN_VALUE = -2147483648;

			private int value;

			public MyInteger(int value)
			{
				this.value=value;
			}

			public MyInteger(String s) throws IllegalArgumentException
			{
				this.value = parseInt(s);
			}

			private static boolean isDigit(char c)
			{
				return (c=='0' || c=='1' || c=='2' || c=='3' || c=='4' || c=='5' ||
						c=='6' || c=='7' || c=='8' || c=='9');
			}

			private static int charToInt(char c)
			{
				int asciivalue = c;
				int intvalue = asciivalue-48; // 0 ist 48 bis 9 ist 57
				return intvalue;
			}

			public static int parseInt(String s) throws IllegalArgumentException
			{
				if(s == null) throw new IllegalArgumentException("kein String");
				if(s.length()==0) throw new IllegalArgumentException("leerer String");
				// pruefe, ob erstes Zeichen + oder -
				// merken und weiter mit Rest
				boolean negativ = false;
				if(s.charAt(0)=='+') s = s.substring(1);
				else if(s.charAt(0)=='-')
				{
					s = s.substring(1);
					negativ = true;
				}
				if(s.length()==0) throw new IllegalArgumentException("nur '+' bzw. '-' --> keine Zahl");
				// entferne fuehrende Nullen
				while(s.length() > 0 && s.charAt(0)=='0')
				{
					s = s.substring(1);
				}
				if(s.length()==0) return 0;		// String bestand nur aus Nullen --> 0
				for(int i=0; i<s.length(); i++)
				{
					if(!isDigit(s.charAt(i))) throw new IllegalArgumentException("keine Zahl!");
				}
				
				int zahl = 0;
				for(int i = 0; i < s.length(); i++)
				{
					int ziffer = charToInt(s.charAt(i));
					if((!negativ && (MyInteger.MAX_VALUE - ziffer) / 10 < zahl) || (negativ && (MyInteger.MAX_VALUE+1 - ziffer) / 10 < zahl))
					{
						if(negativ) throw new IllegalArgumentException("Zahl zu klein!");
						else throw new IllegalArgumentException("Zahl zu gross!");
					}
					zahl = zahl * 10 + ziffer;
				}
				if(negativ) return -zahl;
				else return zahl;
			}

			public int intValue()
			{
				return this.value;
			}

			public double doubleValue()
			{
				return this.value;
			}

			public static MyInteger valueOf(String s) throws IllegalArgumentException
			{
				return new MyInteger(s);
			}

			public static MyInteger valueOf(int value)
			{
				return new MyInteger(value);
			}

			@Override
			public boolean equals(Object other)
			{
				if(other == null) return false;
				if(this == other) return true; 
				if(this.getClass() != other.getClass()) return false;   

				MyInteger otherInt = (MyInteger)other;  
				return (this.value == otherInt.value); 
			}

			@Override
			public int hashCode()
			{
				return this.value;
			}

			@Override
			public String toString()
			{
				return value+"";
			}

			public static int compare(int x, int y)
			{
				return (x < y) ? -1 : ((x == y) ? 0 : 1);
			}

			public int compareTo(MyInteger otherMyInteger)
			{
				return compare(this.value, otherMyInteger.value);
			}
		}
		```
	


??? success "eine mögliche Lösung für Übung 12 (JUnit)"

	=== "MyIntegerTest.java"
		```java linenums="1"
		package uebungen.uebung10.loesung;

		import static org.junit.jupiter.api.Assertions.*;

		import org.junit.jupiter.api.BeforeAll;
		import org.junit.jupiter.api.DisplayName;
		import org.junit.jupiter.api.Test;

		class MyIntegerTest {
			
		    static MyInteger mi1, mi2, mi3, mi4, mi5, mi6, mi7;

		    @BeforeAll
		    public static void setUpBeforeClass() throws Exception 
		    {
		        mi1 = new MyInteger("-2147483648");
		        mi2 = new MyInteger("+2147483647");
		        mi3 = new MyInteger(-1);
		        mi4 = new MyInteger(1);
		        mi5 = new MyInteger(0);
		        mi6 = new MyInteger("-1");
		        mi7 = new MyInteger(2147483647);

		    }
		    
			/*
			 * parseInt-Testfaelle:
			 * 	null		-> Exception (IAE) kein String
			 * 	""			-> Exception (IAE) leerer String
			 * 	"+"			-> Exception (IAE) nur '+' bzw. '-' --> keine Zahl
			 * 	"-"			-> Exception (IAE) nur '+' bzw. '-' --> keine Zahl
			 * 	"-00000000"	-> 0
			 * 	"+00000000"	-> 0
			 * 	"-00000001"	-> -1
			 * 	"+00000001"	->	1
			 * 	"123456a"	-> Exception (IAE) keine Zahl!
			 * 	"-123456a"	-> Exception (IAE) keine Zahl!
			 * 	"+123456a"	-> Exception (IAE) keine Zahl!
			 * 	"2147483648"	-> Exception (IAE) Zahl zu gross!
			 *  "-2147483649"	-> Exception (IAE) Zahl zu klein!
			 * 
			 */
			@Test
			void testParseIntPositiveInt() {
				
				assertEquals(1234, MyInteger.parseInt("1234"), "\"1234\" should be 1234");
				assertEquals(1234, MyInteger.parseInt("+1234"), "\"+1234\" should be 1234");
				assertEquals(1234, MyInteger.parseInt("01234"), "\"01234\" should be 1234");
			}
			
			@Test
			void testParseIntNegativeInt() {
				
				assertEquals(-1234, MyInteger.parseInt("-1234"), "\"-1234\" should be -1234");
				assertEquals(-1234, MyInteger.parseInt("-01234"), "\"-01234\" should be -1234");
			}
			
			@Test
			void testValueOfPositiveInt() {
				MyInteger m = MyInteger.valueOf(1234);
				
				assertNotNull(m, "shoul be an object");
				assertEquals(1234, m.intValue(), "1234 should be 1234");
			}
			
			@Test
			@DisplayName("Input-String is null")
			void testParseIntNull() {
				Exception exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt(null));
				
				assertEquals("kein String", exception.getMessage());
			}
			
			@Test
			@DisplayName("Input-String is leer")
			void testParseIntLeer() {
				Exception exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt(""));
				
				assertEquals("leerer String", exception.getMessage());
			}
			
			
			@Test
			@DisplayName("Nur Plus oder Minus")
			void testParseIntNurPlusOderMinus() {
				Exception exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt("+"));
				
				assertEquals("nur '+' bzw. '-' --> keine Zahl", exception.getMessage());
				
				exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt("-"));
				
				assertEquals("nur '+' bzw. '-' --> keine Zahl", exception.getMessage());
			}

			@Test
			@DisplayName("Keine Zahl")
			void testParseIntKeineZahl() {
				Exception exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt("+1234a"));
				
				assertEquals("keine Zahl!", exception.getMessage());

			}
			
			@Test
			@DisplayName("Zahl zu gross")
			void testParseIntZahlZuGross() {
				Exception exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt("2147483648"));
				
				assertEquals("Zahl zu gross!", exception.getMessage());
			}
			
			@Test
			@DisplayName("Zahl zu klein")
			void testParseIntZahlZuKlein() {
				Exception exception = assertThrows(IllegalArgumentException.class, () -> MyInteger.parseInt("-2147483649"));
				
				assertEquals("Zahl zu klein!", exception.getMessage());
			}
			
			@Test
			void testParseIntNurNullen() {
				assertEquals(0, MyInteger.parseInt("-000000000000"), "\"-000000000000\" should be 0");
				assertEquals(0, MyInteger.parseInt("+000000000000"), "\"+000000000000\" should be 0");
				assertEquals(0, MyInteger.parseInt("0000000000000"), "\"0000000000000\" should be 0");
			}
	
		    @Test
		    void testHashCode()
		    {
		        assertTrue(mi2.hashCode()==mi7.hashCode(), "hashCode of mi2 and mi7 should be equal");
		        assertEquals(-2147483648, mi1.hashCode(), "hashCode of mi1 should be -2147483648");
		        assertEquals(0, mi5.hashCode(), "hashCode of mi5 should be 0");
		    }

		    @Test
		    void testMyIntegerInt()
		    {
		        assertNotNull(mi4, "mi4 should be not null");
		        assertTrue(mi3.equals(mi6), "mi3 and mi6 should be equal");
		        assertTrue(mi7.equals(mi2), "mi7 and mi2 should be equal");
		    }

		    @Test
		    void testMyIntegerString()
		    {
		        assertNotNull(mi1, "mi1 should be not null");
		        assertNotNull(mi2, "mi2 should be not null");
		        assertNotNull(mi6, "mi6 should be not null");
		        assertTrue(mi3.equals(mi6), "mi3 and mi6 should be equal");
		        assertTrue(mi7.equals(mi2), "mi7 and mi2 should be equal");
		    }

		    @Test
		    void testParseInt()
		    {
		        assertEquals(-2147483648, MyInteger.parseInt("-2147483648"), "should be -2147483648");
		        assertEquals(+2147483647, MyInteger.parseInt("+00002147483647"), "should be +2147483647");
		        assertEquals(-1, MyInteger.parseInt("-0000001"), "should be -1");   
		    }


		    @Test
		    void testIntValue()
		    {
		        assertEquals(-2147483648, mi1.intValue(), "should be -2147483648");
		        assertEquals(+2147483647, mi2.intValue(), "should be +2147483647");
		        assertEquals(+2147483647, mi7.intValue(), "should be +2147483647");
		    }

		    @Test
		    void testDoubleValue()
		    {
		        assertEquals(-2147483648.0, mi1.doubleValue(), "should be -2147483648.0");
		        assertEquals(+2147483647.0, mi2.doubleValue(), "should be +2147483647.0");
		        assertEquals(+2147483647.0, mi7.doubleValue(), "should be +2147483647.0");
		    }

		    @Test
		    void testValueOfString()
		    {
		        assertTrue(mi1.equals(MyInteger.valueOf("-2147483648")), "should be equal to mi1");
		        assertTrue(mi2.equals(MyInteger.valueOf("2147483647")), "should be equal to mi2");
		        assertTrue(mi7.equals(MyInteger.valueOf("2147483647")), "should be equal to mi7");
		    }

		    @Test
		    void testValueOfInt()
		    {
		        assertTrue(mi1.equals(MyInteger.valueOf(-2147483648)), "should be equal to mi1");
		        assertTrue(mi2.equals(MyInteger.valueOf(2147483647)), "should be equal to mi2");
		        assertTrue(mi7.equals(MyInteger.valueOf(2147483647)), "should be equal to mi7");
		    }

		    @Test
		    void testEqualsObject()
		    {
		        assertTrue(mi3.equals(mi6), "mi3 and mi6 should be equal");
		        assertTrue(mi7.equals(mi2), "mi7 and mi2 should be equal");
		        assertFalse(mi3.equals(mi4), "mi3 and mi4 should not be equal");
		        assertFalse(mi3.equals(mi5), "mi3 and mi5 should not be equal");
		    }

		    @Test
		    void testToString()
		    {
		        assertEquals("-2147483648", mi1.toString(), "should be '-2147483648'");
		        assertEquals("2147483647", mi2.toString(), "should be '2147483647' mi2");
		        assertEquals("2147483647", mi7.toString(), "should be '2147483647' mi7");
		    }

		    @Test
		    void testCompare()
		    {
		        assertTrue(MyInteger.compare(5, 4)>0, "5,4 should be > 0");
		        assertTrue(MyInteger.compare(4, 4)==0, "4,4 should be == 0");
		        assertTrue(MyInteger.compare(4, 5)<0, "4,5 should be < 0");
		        assertTrue(MyInteger.compare(MyInteger.MAX_VALUE, MyInteger.MIN_VALUE)>0, "MAX,MIN should be > 0");
		        assertTrue(MyInteger.compare(MyInteger.MAX_VALUE, MyInteger.MAX_VALUE)==0, "MAX,MAX should be == 0");
		        assertTrue(MyInteger.compare(MyInteger.MIN_VALUE, MyInteger.MAX_VALUE)<0, "MIN,MAX should be > 0");
		    }

		    @Test
		    void testCompareTo()
		    {
		        assertTrue(mi1.compareTo(mi2)<0, "mi1, mi2 should be < 0");
		        assertTrue(mi2.compareTo(mi1)>0, "mi2, mi1 should be > 0");
		        assertTrue(mi2.compareTo(mi7)==0, "mi2, mi7 should be == 0");
		        assertTrue(mi3.compareTo(mi6)==0, "mi3, mi6 should be == 0");
		    }


		}

		```



##### Übung 13 (Collections Wiederholung)

??? "Übung 13 (Collections Wiederholung)"
	- Gegeben sind folgende Klassen:

		??? question "Klassen für Uebung13"

			=== "Uebung13.java"
				```java
				package uebungen.uebung13;

				import java.util.*;

				public class Uebung13
				{
				    static Random r =  new Random();

				    public static Circle createCircle(int bound)
				    {
				        int randNr = r.nextInt(bound);
				        if(randNr < 2)
				        {
				            return new Circle();
				        }
				        else
				        {
				            return new Circle(randNr);
				        }
				    }

				    public static List<Circle> setUpCircleList(int listLength, int bound)
				    {
				        List<Circle> list = new ArrayList<Circle>();
				        for(int i = 0; i < listLength; i++)
				        {
				            list.add(createCircle(bound));
				        }
				        return list;
				    }

				    /*
				     *   gibt eine Liste mit allen Elementen aus c1 UND c2 zurueck
				     *   in der Liste darf jedoch kein Element doppelt vorkommen, d.h.
				     *   wenn e1 in Liste und e2 in Liste, dann gilt !e1.equals(e2)
				     */
				    public static List<Circle> union(List<Circle> c1, List<Circle> c2)
				    {
				        return null; 	//TODO
				    }


				    /*
				     *   gibt eine Map zurueck
				     *   Schluessel sind die Flaecheninhalte (area) der Circles
				     *   Werte sind eine Liste aller Circle-Objekte mit diesem Flaecheninhalt
				     */
				    public static Map<Double, List<Circle>> createMap(List<Circle> circles)
				    {
				        return null; //TODO
				    }


				    /*
				     *   fuegt der map alle circles passend hinzu
				     */
				    public static void addListToMap(Map<Double, List<Circle>> map, List<Circle> circles)
				    {
				        //TODO
				    }

				    /*
				     *   - uebergeben wird eine map, deren keys vom Typ Double sind
				     *   - der Schluessel key ist vom Typ int
				     *   - in der map wird nach einem Schluessel gesucht, dessen ganzzahliger 
				     *      Wert dem int key entspricht, d.h. 
				     *          78,654... passt zu 78
				     *          79,012... passt nicht zu 78
				     *   - falls ein solcher Schluessel nicht in der map existiert, wird eine
				     *      IllegalArgumentException geworfen. Die Nachricht enthaelt den Wert des 
				     *      Schlussels, nach dem gesucht wurde, z.B. 'key 79 not found' 
				     *   - falls ein solcher Schluessel existiert, wird der erste Circle aus der 
				     *      Liste zu dem Schluessel zurueckgegeben
				     */
				    public static Circle getFirstCircleOfKey(Map<Double, List<Circle>> map, int key)
				    {
				    	//TODO
				    	return null;
				    }

				    public static void main(String[] args)
				    {
				        System.out.printf("%n%n ---------------------- list1 und list2 ----------------------%n%n");
				        List<Circle> list1 = setUpCircleList(10, 6);
				        List<Circle> list2 = setUpCircleList(10, 6);
				        System.out.println("list1: ");
				        list1.forEach(System.out::println);
				        System.out.println();
				        System.out.println("list2: ");
				        list2.forEach(System.out::println);

				        System.out.printf("%n%n -------------------- union(list1, list2) --------------------%n%n");
				        /* TODO: print List of union(list1, list2)
				        * z.B.:
				            Circle [radius=1.0] area=  3,14 circumference= 6,28
				            Circle [radius=3.0] area= 28,27 circumference=18,85
				            Circle [radius=4.0] area= 50,27 circumference=25,13
				            Circle [radius=5.0] area= 78,54 circumference=31,42
				        */

				        System.out.printf("%n%n -------------------- createMap(list1) --------------------%n%n");
				        /* TODO: print Map of createMap(list1)
				        * z.B.:
				            -- area =  28,27 --
				            Circle [radius=3.0]
				            Circle [radius=3.0]

				            -- area =  78,54 --
				            Circle [radius=5.0]

				            -- area =   3,14 --
				            Circle [radius=1.0]
				            Circle [radius=1.0]
				            Circle [radius=1.0]
				            Circle [radius=1.0]
				            Circle [radius=1.0]

				            -- area =  50,27 --
				            Circle [radius=4.0]

				            -- area =  12,57 --
				            Circle [radius=2.0]
				        */

				        System.out.printf("%n%n -------------------- addListToMap(map,list2) --------------------%n%n");
				        /* TODO: print Map of addListToMap(map,list2)
				        * z.B.:
				            -- area =  28,27 --
				            Circle [radius=3.0]
				            Circle [radius=3.0]

				            -- area =  78,54 --
				            Circle [radius=5.0]

				            -- area =   3,14 --
				            Circle [radius=1.0]
				            Circle [radius=1.0]
				            Circle [radius=1.0]
				            Circle [radius=1.0]
				            Circle [radius=1.0]

				            -- area =  50,27 --
				            Circle [radius=4.0]

				            -- area =  12,57 --
				            Circle [radius=2.0]
				        */

				        System.out.printf("%n%n -------------------- getFirstCircleOfKey(map,int) --------------------%n%n");
				        /* TODO: search in map for key=78 and print Circle
				        /* TODO: search in map for key=79 and print Exception-Message
				    }
				}

				```

			=== "Uebung13Test.java"
				```java
				package uebungen.uebung13;

				import org.junit.jupiter.api.BeforeAll;
				import org.junit.jupiter.api.DisplayName;
				import org.junit.jupiter.api.Test;

				import java.util.ArrayList;
				import java.util.HashMap;
				import java.util.List;
				import java.util.Map;

				import static org.junit.jupiter.api.Assertions.*;

				public class Uebung13Test
				{
				    static Circle c0, c1, c2, c3, c4, c5, c6;
				    @BeforeAll
				    public static void setup()
				    {
				        c0 = new Circle();
				        c1 = new Circle(1);     // c0.equals(c1) == true
				        c2 = new Circle(2);
				        c3 = new Circle(3);
				        c4 = new Circle(4);
				        c5 = new Circle(5);

				    }

				    @Test
				    @DisplayName("test union(list1, list2)")
				    public void testUnion()
				    {
				        System.out.printf("%n%n--------------- tests union(list1, list2) ------------------%n%n");
				        // given
				        List<Circle> l1 = List.of(c0, c1, c2);
				        List<Circle> l2 = List.of(c3, c4, c5);
				        List<Circle> l3 = List.of(c0, c1, c2);
				        List<Circle> l4 = List.of(c0, c1, c3);
				        List<Circle> l5 = List.of();

				        // when
				        List<Circle> list1 = Uebung13.union(l1, l2); list1.sort(Comparator.comparing(Circle::getRadius));
				        List<Circle> list2 = Uebung13.union(l3, l4); list2.sort(Comparator.comparing(Circle::getRadius));
				        List<Circle> list3 = Uebung13.union(l1, l3); list3.sort(Comparator.comparing(Circle::getRadius));
				        List<Circle> list4 = Uebung13.union(l2, l4); list4.sort(Comparator.comparing(Circle::getRadius));
				        List<Circle> list5 = Uebung13.union(l4, l5); list5.sort(Comparator.comparing(Circle::getRadius));

				        // then
				        List<Circle> expected1 = List.of(c0, c2, c3,  c4, c5);
				        List<Circle> expected2 = List.of(c0, c2, c3);
				        List<Circle> expected3 = List.of(c0, c2);
				        List<Circle> expected4 = List.of(c0, c3,  c4, c5);
				        List<Circle> expected5 = List.of(c0, c3);
				        assertEquals(expected1, list1, "list should contain circles with radius 1.0, 2.0, 3.0, 4.0 and 5.0, only");
				        assertEquals(expected2, list2, "list should contain circles with radius 1.0, 2.0 and 3.0, only");
				        assertEquals(expected3, list3, "list should contain circles with radius 1.0 and 2.0, only");
				        assertEquals(expected4, list4, "list should contain circles with radius 1.0, 3.0, 4.0 and 5.0, only");
				        assertEquals(expected5, list5, "list should contain circles with radius 1.0 and 3.0, only");
				    }

				    @Test
				    @DisplayName("test createMap(list)")
				    public void testCreateMap()
				    {
				        System.out.printf("%n%n------------------ tests createMap(list) ---------------------%n%n");
				        // given
				        List<Circle> l1 = List.of(c0, c1, c2, c3, c4, c5, c0, c1, c2, c3, c4, c5, c4, c5, c0);
				        List<Circle> l2 = List.of(c0, c1);

				        // when
				        Map<Double, List<Circle>> map1 = Uebung13.createMap(l1);
				        Map<Double, List<Circle>> map2 = Uebung13.createMap(l2);

				        // then
				        Map<Double, List<Circle>> expected1 = new HashMap<>();
				        expected1.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1, c0, c1, c0));
				        expected1.put(Math.PI * Math.pow(2.0, 2), List.of(c2, c2));
				        expected1.put(Math.PI * Math.pow(3.0, 2), List.of(c3, c3));
				        expected1.put(Math.PI * Math.pow(4.0, 2), List.of(c4, c4, c4));
				        expected1.put(Math.PI * Math.pow(5.0, 2), List.of(c5, c5, c5));
				        assertEquals(expected1, map1, "click on \"Click to see difference\" in IntelliJ");

				        Map<Double, List<Circle>> expected2 = new HashMap<>();
				        expected2.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1));
				        assertEquals(expected2, map2, "click on \"Click to see difference\" in IntelliJ");
				    }

				    @Test
				    @DisplayName("test addListToMap(list)")
				    public void testAddListToMap()
				    {
				        System.out.printf("%n%n------------------ tests addListToMap(list) ---------------------%n%n");
				        // given
				        Map<Double, List<Circle>> map1 = new HashMap<>();
				        List<Circle> l1 = new ArrayList<>();
				        l1.add(c0);
				        l1.add(c1);
				        map1.put(Math.PI * Math.pow(1.0, 2), l1);
				        List<Circle> l2 = new ArrayList<>();
				        l2.add(c2);
				        map1.put(Math.PI * Math.pow(2.0, 2), l2);
				        List<Circle> l3 = new ArrayList<>();
				        l3.add(c3);
				        map1.put(Math.PI * Math.pow(3.0, 2), l3);
				        List<Circle> l4 = new ArrayList<>();
				        l4.add(c4);
				        l4.add(c4);
				        map1.put(Math.PI * Math.pow(4.0, 2), l4);
				        List<Circle> list1 = List.of(c0, c1, c2, c3, c4, c5);

				        Map<Double, List<Circle>> map2 = new HashMap<>();
				        List<Circle> l5 = new ArrayList<>();
				        l5.add(c0);
				        l5.add(c1);
				        map2.put(Math.PI * Math.pow(1.0, 2), l5);
				        List<Circle> list2 = List.of(c0, c1, c2);

				        // when
				        Uebung13.addListToMap(map1, list1);
				        Uebung13.addListToMap(map2, list2);

				        // then
				        Map<Double, List<Circle>> expected1 = new HashMap<>();
				        expected1.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1, c0, c1));
				        expected1.put(Math.PI * Math.pow(2.0, 2), List.of(c2, c2));
				        expected1.put(Math.PI * Math.pow(3.0, 2), List.of(c3, c3));
				        expected1.put(Math.PI * Math.pow(4.0, 2), List.of(c4, c4, c4));
				        expected1.put(Math.PI * Math.pow(5.0, 2), List.of(c5));
				        assertEquals(expected1, map1, "click on \"Click to see difference\" in IntelliJ");

				        Map<Double, List<Circle>> expected2 = new HashMap<>();
				        expected2.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1, c0, c1));
				        expected2.put(Math.PI * Math.pow(2.0, 2), List.of(c2));
				        assertEquals(expected2, map2, "click on \"Click to see difference\" in IntelliJ");
				    }

				    @Test
				    @DisplayName("test getFirstCircleOfKey(map, key)")
				    public void testGetFirstCircleOfKey()
				    {
				        System.out.printf("%n%n------------------ tests getFirstCircleOfKey(map, key) ---------------------%n%n");
				        // given
				        Map<Double, List<Circle>> map = new HashMap<>();
				        map.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1));
				        map.put(Math.PI * Math.pow(2.0, 2), List.of(c2));
				        map.put(Math.PI * Math.pow(3.0, 2), List.of(c3));
				        map.put(Math.PI * Math.pow(4.0, 2), List.of(c4));
				        map.put(Math.PI * Math.pow(5.0, 2), List.of(c5));

				        //when
				        int key1 = 78;
				        int key2 = 79;
				        Circle c = Uebung13.getFirstCircleOfKey(map, key1);
				        Exception e = assertThrows(IllegalArgumentException.class, () -> Uebung13.getFirstCircleOfKey(map, key2));

				        // then
				        assertNotNull(c, "Circle should not be null");
				        assertEquals(c5, c, "Circle should have radius=5.0");
				        assertEquals("key 79 not found", e.getMessage());
				    }
				}

				```

			=== "Circle.java"
				```java
				package uebungen.uebung13;

				public class Circle
				{
				    double radius;

				    Circle()
				    {
				        this.radius = 1.0;
				    }

				    Circle(double radius)
				    {
				        this.radius = radius;
				    }

				    public double getRadius()
				    {
				        return this.radius;
				    }

				    public double area()
				    {
				        return Math.PI * this.radius * this.radius;
				    }

				    public double circumference()
				    {
				        return 2 * Math.PI * this.radius;
				    }

				    @Override
				    public String toString()
				    {
				        return "Circle [radius=" + this.radius + "]";
				    }

				    @Override
				    public boolean equals(Object o)
				    {
				        if (this == o) return true;
				        if (o == null || getClass() != o.getClass()) return false;
				        Circle circle = (Circle) o;
				        return circle.radius == this.radius;
				    }

				    @Override
				    public int hashCode()
				    {
				        return (int) this.radius;
				    }
				}
				```


	- siehe `TODO` in `Uebung13.java`
	- am Ende sollten alle Tests bestanden sein


??? success "mögliche Lösung für Übung 13"
	
	=== "Uebung13.java"
		```java
		package uebungen.uebung13;

		import java.util.*;
		import java.util.stream.Collectors;
		import java.util.stream.Stream;

		public class Uebung13
		{
		    static Random r =  new Random();

		    private static Circle createCircle(int bound)
		    {
		        int randNr = r.nextInt(bound);
		        if(randNr < 2)
		        {
		            return new Circle();
		        }
		        else
		        {
		            return new Circle(randNr);
		        }
		    }

		    private static List<Circle> setUpCircleList(int listLength, int bound)
		    {
		        List<Circle> list = new ArrayList<Circle>();
		        for(int i = 0; i < listLength; i++)
		        {
		            list.add(createCircle(bound));
		        }
		        return list;
		    }

		    /*
		     *   gibt eine Liste mit allen Elementen aus c1 UND c2 zurueck
		     *   in der Liste darf jedoch kein Element doppelt vorkommen, d.h.
		     *   wenn e1 in Liste und e2 in Liste, dann gilt !e1.equals(e2)
		     */
		    public static List<Circle> union(final List<Circle> c1, final List<Circle> c2)
		    {
		        /*
		        Set<Circle> set1 = new HashSet<>(c1);
		        set1.addAll(c2);
		        List<Circle> unionList = new ArrayList<>(set1);
		         */

		        List<Circle> unionList = Stream.concat(c1.stream(), c2.stream())
		                .distinct().collect(Collectors.toList());
		        return unionList;
		    }


		    /*
		     *   gibt eine Map zurueck
		     *   Schluessel sind die Flaecheninhalte (area) der Circles
		     *   Werte sind eine Liste aller Circle-Objekte mit diesem Flaecheninhalt
		     */
		    public static Map<Double, List<Circle>> createMap(List<Circle> circles)
		    {
		        Map<Double, List<Circle>> map = circles.stream().collect(Collectors.groupingBy(c -> c.area()));
		        return map;
		    }


		    /*
		     *   fuegt der map alle circles passend hinzu
		     */
		    public static void addListToMap(Map<Double, List<Circle>> map, List<Circle> circles)
		    {
		        for(Circle circle : circles)
		        {
		            double area = circle.area();
		            if(map.containsKey(area)) {
		                List<Circle> list = map.get(area);
		                list.add(circle);
		            } else {
		                List<Circle> list = new ArrayList<>();
		                list.add(circle);
		                map.put(area, list);
		            }
		        }
		    }

		    /*
		     *   - uebergeben wird eine map, deren keys vom Typ Double sind
		     *   - der Schluessel key ist vom Typ int
		     *   - in der map wird nach einem Schluessel gesucht, dessen ganzzahliger
		     *      Wert dem int key entspricht, d.h.
		     *          78,654... passt zu 78
		     *          79,012... passt nicht zu 78
		     *   - falls ein solcher Schluessel nicht in der map existiert, wird eine
		     *      IllegalArgumentException geworfen. Die Nachricht enthaelt den Wert des
		     *      Schlussels, nach dem gesucht wurde, z.B. 'key 79 not found'
		     *   - falls ein solcher Schluessel existiert, wird der erste Circle aus der
		     *      Liste zu dem Schluessel zurueckgegeben
		     */
		    public static Circle getFirstCircleOfKey(Map<Double, List<Circle>> map, int key) throws IllegalArgumentException
		    {
		        for(Double originalKey : map.keySet())
		        {
		            //int intKey = (int) originalKey;
		            if(originalKey.intValue() == key)
		            {
		                return map.get(originalKey).getFirst();
		            }
		        }
		        throw new IllegalArgumentException("key " + key + " not found");
		    }

		    public static void main(String[] args)
		    {
		        System.out.printf("%n%n ---------------------- list1 und list2 ----------------------%n%n");
		        List<Circle> list1 = setUpCircleList(10, 6);
		        List<Circle> list2 = setUpCircleList(10, 6);
		        System.out.println("list1: ");
		        list1.forEach(System.out::println);
		        System.out.println();
		        System.out.println("list2: ");
		        list2.forEach(System.out::println);

		        System.out.printf("%n%n -------------------- union(list1, list2) --------------------%n%n");
		        /* TODO: print List of union(list1, list2)
		        * z.B.:
		            Circle [radius=1.0] area=  3,14 circumference= 6,28
		            Circle [radius=3.0] area= 28,27 circumference=18,85
		            Circle [radius=4.0] area= 50,27 circumference=25,13
		            Circle [radius=5.0] area= 78,54 circumference=31,42
		        */
		        List<Circle> unionList = union(list1, list2);
		        for(Circle circle : unionList)
		        {
		            System.out.printf("%s area=%6.2f circumference=%5.2f %n",
		                    circle.toString(), circle.area(), circle.circumference());
		        }


		        System.out.printf("%n%n -------------------- createMap(list1) --------------------%n%n");
		        /* TODO: print Map of createMap(list1)
		        * z.B.:
		            -- area =  28,27 --
		            Circle [radius=3.0]
		            Circle [radius=3.0]

		            -- area =  78,54 --
		            Circle [radius=5.0]

		            -- area =   3,14 --
		            Circle [radius=1.0]
		            Circle [radius=1.0]
		            Circle [radius=1.0]
		            Circle [radius=1.0]
		            Circle [radius=1.0]

		            -- area =  50,27 --
		            Circle [radius=4.0]

		            -- area =  12,57 --
		            Circle [radius=2.0]
		        */
		        Map<Double, List<Circle>> map1 = createMap(list1);
		        map1.forEach( (k,v) -> {
		            System.out.printf("-- area = %.2f %n", k);
		            v.forEach(c -> System.out.println(c.toString()));
		            System.out.println();
		        });

		        System.out.printf("%n%n -------------------- addListToMap(map,list2) --------------------%n%n");
		        /* TODO: print Map of addListToMap(map,list2)
		        * z.B.:
		            -- area =  28,27 --
		            Circle [radius=3.0]
		            Circle [radius=3.0]

		            -- area =  78,54 --
		            Circle [radius=5.0]

		            -- area =   3,14 --
		            Circle [radius=1.0]
		            Circle [radius=1.0]
		            Circle [radius=1.0]
		            Circle [radius=1.0]
		            Circle [radius=1.0]

		            -- area =  50,27 --
		            Circle [radius=4.0]

		            -- area =  12,57 --
		            Circle [radius=2.0]
		        */
		        addListToMap(map1, list1);
		        for(Map.Entry<Double, List<Circle>> entry : map1.entrySet())
		        {
		            System.out.printf("-- area = %.2f %n", entry.getKey());
		            for(Circle circle : entry.getValue())
		            {
		                System.out.println(circle.toString());
		            }
		            System.out.println();
		        }

		        System.out.printf("%n%n -------------------- getFirstCircleOfKey(map,int) --------------------%n%n");
		        /* TODO: search in map for key=78 and print Circle */
		        /* TODO: search in map for key=79 and print Exception-Message */
		        for(int key = 78; key < 80; key++)
		        {
		            try {
		                Circle circle = getFirstCircleOfKey(map1, key);
		                System.out.println(circle.toString());
		            }
		            catch(IllegalArgumentException e) {
		                System.out.println(e.getMessage());
		            }
		        }

		    }
		}
		```



##### Probeklausur 1

??? "Probeklausur 1"

	***Vorbereitung***

	??? question "Gegeben sind folgende Klassen (auch als [download](./files/probeklausur1.zip) verfügbar):"

		=== "Probeklausur1.java"
			```java
			package probeklausuren.probeklausur1;

			import java.util.*;

			public class Probeklausur1
			{
			    static Random r =  new Random();

			    public static Circle createCircle(int bound)
			    {
			        int randNr = r.nextInt(bound);
			        if(randNr < 2)
			        {
			            return new Circle();
			        }
			        else
			        {
			            return new Circle(randNr);
			        }
			    }

			    public static List<Circle> setUpCircleList(int listLength, int bound)
			    {
			        List<Circle> list = new ArrayList<Circle>();
			        for(int i = 0; i < listLength; i++)
			        {
			            list.add(createCircle(bound));
			        }
			        return list;
			    }

			    /*
			     *   gibt eine Liste mit allen Elementen aus c1 UND c2 zurueck
			     *   in der Liste darf jedoch kein Element doppelt vorkommen, d.h.
			     *   wenn e1 in Liste und e2 in Liste, dann gilt !e1.equals(e2)
			     */
			    public static List<Circle> union(List<Circle> c1, List<Circle> c2)
			    {
			        return null; //TODO
			    }


			    /*
			     *   gibt eine Map zurueck
			     *   Schluessel sind die Flaecheninhalte (area) der Circles
			     *   Werte sind eine Liste aller Circle-Objekte mit diesem Flaecheninhalt
			     */
			    public static Map<Double, List<Circle>> createMap(List<Circle> circles)
			    {
			        return null; //TODO
			    }

			    /*
			     *   fuegt der map alle circles passend hinzu
			     */
			    public static void addListToMap(Map<Double, List<Circle>> map, List<Circle> circles)
			    {
			        //TODO
			    }

			    /*
			     *   - uebergeben wird eine map, deren keys vom Typ Double sind
			     *   - der Schluessel key ist vom Typ int
			     *   - in der map wird nach einem Schluessel gesucht, dessen ganzzahliger
			     *      Wert dem int key entspricht, d.h.
			     *          78,654 passt zu 78
			     *          79,01 passt nicht zu 78
			     *   - falls ein solcher Schluessel nicht in der map existiert, wird eine
			     *      IllegalArgumentException geworfen. Die Nachricht enthaelt den Wert des
			     *      Schlussels, nach dem gesucht wurde, z.B. 'key 79 not found'
			     *   - falls ein solcher Schluessel existiert, wird der erste Circle aus der
			     *      Liste zu dem Schluessel zurueckgegeben
			     */
			    public static Circle getFirstCircleOfKey(Map<Double, List<Circle>> map, int key)
			    {
			        return null; //TODO
			    }

			    /*
			     *   - uebergeben wird eine map, deren keys vom Typ Double sind (area())
			     *   - die Werte sind vom Typ List<Circle>
			     *   - in der map (in den values) wird nach einem Circle gesucht, dessen
			     *     Radius dem Parameterwert von double radius entspricht
			     *   - falls ein solcher Circle existiert, wird er dem Optional hinzugefuegt
			     *     und zurückgegeben
			     *   - falls ein solcher Circle nicht existiert, wird ein leeres Optional
			     *     zurueckgegeben
			     */
			    public static Optional<Circle> getFirstCircleOfRadius(Map<Double, List<Circle>> map, double radius)
			    {
			        return null; //TODO
			    }

		        /*
			     * uebergeben wird eine unsortierte Liste von Circle-Objekten
			     * zurueckgegeben wird eine sortierte Liste von Circle-Objekte
			     * sortiert nach "natural order" (compareTo)
			     */
			    public static List<Circle> createSortedListOfCircles(List<Circle> circles)
			    {
			        return null; //TODO
			    }

			    /*
			     * uebergeben wird eine unsortierte Liste von Circle-Objekten
			     * zurueckgegeben wird eine sortierte Liste von Circle-Objekte
			     * - sortiert nach "natural order" (compareTo)
			     * - gerade Radien zuerst!!!
			     */
			    public static List<Circle> createSortedListOfCirclesEvenRadiiFirst(List<Circle> circles)
			    {
			        return null; //TODO
			    }

			    /*
			     * Hilfsmethode zur Ausgabe einer Map<Double, List<Circle>>
			     */
			    private static void printMapOfCircles(Map<Double, List<Circle>> map)
			    {
			        // MUSS NICHT, KANN DIREKT IN MAIN, HILFT ABER
			    }

			    public static void main(String[] args)
			    {
			        System.out.printf("%n%n ---------------------- list1 und list2 ----------------------%n%n");
			        List<Circle> list1 = setUpCircleList(10, 6);
			        List<Circle> list2 = setUpCircleList(10, 6);
			        System.out.println("list1: ");
			        list1.forEach(System.out::println);
			        System.out.println();
			        System.out.println("list2: ");
			        list2.forEach(System.out::println);

			        System.out.printf("%n%n -------------------- union(list1, list2) --------------------%n%n");
			        /* print List of union(list1, list2)
			        * z.B.:
			            Circle [radius=1.0] area=  3,14 circumference= 6,28
			            Circle [radius=3.0] area= 28,27 circumference=18,85
			            Circle [radius=4.0] area= 50,27 circumference=25,13
			            Circle [radius=5.0] area= 78,54 circumference=31,42
			        */
			        //TODO

			        System.out.printf("%n%n -------------------- createMap(list1) --------------------%n%n");
			        /* print Map of createMap(list1)
			        * z.B.:
			            -- area =  28,27 --
			            Circle [radius=3.0]
			            Circle [radius=3.0]

			            -- area =  78,54 --
			            Circle [radius=5.0]

			            -- area =   3,14 --
			            Circle [radius=1.0]
			            Circle [radius=1.0]
			            Circle [radius=1.0]
			            Circle [radius=1.0]
			            Circle [radius=1.0]

			            -- area =  50,27 --
			            Circle [radius=4.0]

			            -- area =  12,57 --
			            Circle [radius=2.0]
			        */
			        //TODO

			        System.out.printf("%n%n -------------------- addListToMap(map,list2) --------------------%n%n");
			        /* print Map of addListToMap(map,list2)
			        * z.B.:
			            -- area =  28,27 --
			            Circle [radius=3.0]
			            Circle [radius=3.0]

			            -- area =  78,54 --
			            Circle [radius=5.0]

			            -- area =   3,14 --
			            Circle [radius=1.0]
			            Circle [radius=1.0]
			            Circle [radius=1.0]
			            Circle [radius=1.0]
			            Circle [radius=1.0]

			            -- area =  50,27 --
			            Circle [radius=4.0]

			            -- area =  12,57 --
			            Circle [radius=2.0]
			        */
			       //TODO

			        System.out.printf("%n%n -------------------- getFirstCircleOfKey(map,int) --------------------%n%n");
			        for(int key = 78; key < 80; key++) {

			        	//TODO

			        }

			        System.out.printf("%n%n -------------------- getFirstCircleOfRadius(map,double) --------------------%n%n");
			        for(double radius = 5.0; radius < 7.0; radius++) {

			        	//TODO

			        }

			        System.out.printf("%n%n -------------------- Circle is Comparable  --------------------%n%n");
			        Circle c1 = createCircle(3);
			        Circle c2 = createCircle(3);
			        System.out.println("c1: " + c1);
			        System.out.println("c2: " + c2);

			        //TODO

			        System.out.printf("%n%n -------------------- createSortedListOfCircles(list) --------------------%n%n");

			        //TODO


			        System.out.printf("%n%n -------------------- createSortedListOfCirclesEvenRadiiFirst(list) --------------------%n%n");

			        //TODO
			    }
			}

			```

		=== "Circle.java"
			```java
			package probeklausuren.probeklausur1;

			public class Circle
			{
			    double radius;

			    Circle()
			    {
			        this.radius = 1.0;
			    }

			    Circle(double radius)
			    {
			        this.radius = radius;
			    }

			    public double getRadius()
			    {
			        return this.radius;
			    }

			    public double area()
			    {
			        return Math.PI * this.radius * this.radius;
			    }

			    public double circumference()
			    {
			        return 2 * Math.PI * this.radius;
			    }

			    @Override
			    public String toString()
			    {
			        return "Circle [radius=" + this.radius + "]";
			    }

			    @Override
			    public boolean equals(Object o)
			    {
			        if (this == o) return true;
			        if (o == null || getClass() != o.getClass()) return false;
			        Circle circle = (Circle) o;
			        return circle.radius == this.radius;
			    }

			    @Override
			    public int hashCode()
			    {
			        return (int) this.radius;
			    }
			}
			```

		=== "Probeklausur1Test.java"
			```java
			package probeklausuren.probeklausur1;

			import org.junit.jupiter.api.BeforeAll;
			import org.junit.jupiter.api.DisplayName;
			import org.junit.jupiter.api.Test;

			import java.util.*;

			import static org.junit.jupiter.api.Assertions.*;

			public class Probeklausur1Test
			{
			    static Circle c0, c1, c2, c3, c4, c5, c6;
			    @BeforeAll
			    public static void setup()
			    {
			        c0 = new Circle();
			        c1 = new Circle(1);     // c0.equals(c1) == true
			        c2 = new Circle(2);
			        c3 = new Circle(3);
			        c4 = new Circle(4);
			        c5 = new Circle(5);

			    }

			    @Test
			    @DisplayName("test union(list1, list2)")
			    public void testUnion()
			    {
			        System.out.printf("%n------------------ tests union(list1, list2) ------------------%n");
			        // given
			        List<Circle> l1 = List.of(c0, c1, c2);
			        List<Circle> l2 = List.of(c3, c4, c5);
			        List<Circle> l3 = List.of(c0, c1, c2);
			        List<Circle> l4 = List.of(c0, c1, c3);
			        List<Circle> l5 = List.of();

			        // when
			        List<Circle> list1 = Probeklausur1.union(l1, l2); list1.sort(Comparator.comparing(Circle::getRadius));
			        List<Circle> list2 = Probeklausur1.union(l3, l4); list2.sort(Comparator.comparing(Circle::getRadius));
			        List<Circle> list3 = Probeklausur1.union(l1, l3); list3.sort(Comparator.comparing(Circle::getRadius));
			        List<Circle> list4 = Probeklausur1.union(l2, l4); list4.sort(Comparator.comparing(Circle::getRadius));
			        List<Circle> list5 = Probeklausur1.union(l4, l5); list5.sort(Comparator.comparing(Circle::getRadius));

			        // then
			        List<Circle> expected1 = List.of(c0, c2, c3,  c4, c5);
			        List<Circle> expected2 = List.of(c0, c2, c3);
			        List<Circle> expected3 = List.of(c0, c2);
			        List<Circle> expected4 = List.of(c0, c3,  c4, c5);
			        List<Circle> expected5 = List.of(c0, c3);
			        assertEquals(expected1, list1, "list should contain circles with radius 1.0, 2.0, 3.0, 4.0 and 5.0, only");
			        assertEquals(expected2, list2, "list should contain circles with radius 1.0, 2.0 and 3.0, only");
			        assertEquals(expected3, list3, "list should contain circles with radius 1.0 and 2.0, only");
			        assertEquals(expected4, list4, "list should contain circles with radius 1.0, 3.0, 4.0 and 5.0, only");
			        assertEquals(expected5, list5, "list should contain circles with radius 1.0 and 3.0, only");
			    }

			    @Test
			    @DisplayName("test createMap(list)")
			    public void testCreateMap()
			    {
			        System.out.printf("%n------------------ tests createMap(list) ---------------------%n");
			        // given
			        List<Circle> l1 = List.of(c0, c1, c2, c3, c4, c5, c0, c1, c2, c3, c4, c5, c4, c5, c0);
			        List<Circle> l2 = List.of(c0, c1);

			        // when
			        Map<Double, List<Circle>> map1 = Probeklausur1.createMap(l1);
			        Map<Double, List<Circle>> map2 = Probeklausur1.createMap(l2);

			        // then
			        Map<Double, List<Circle>> expected1 = new HashMap<>();
			        expected1.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1, c0, c1, c0));
			        expected1.put(Math.PI * Math.pow(2.0, 2), List.of(c2, c2));
			        expected1.put(Math.PI * Math.pow(3.0, 2), List.of(c3, c3));
			        expected1.put(Math.PI * Math.pow(4.0, 2), List.of(c4, c4, c4));
			        expected1.put(Math.PI * Math.pow(5.0, 2), List.of(c5, c5, c5));
			        assertEquals(expected1, map1, "click on \"Click to see difference\" in IntelliJ");

			        Map<Double, List<Circle>> expected2 = new HashMap<>();
			        expected2.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1));
			        assertEquals(expected2, map2, "click on \"Click to see difference\" in IntelliJ");
			    }

			    @Test
			    @DisplayName("test addListToMap(list)")
			    public void testAddListToMap()
			    {
			        System.out.printf("%n------------------ tests addListToMap(list) ---------------------%n");
			        // given
			        Map<Double, List<Circle>> map1 = new HashMap<>();
			        List<Circle> l1 = new ArrayList<>();
			        l1.add(c0);
			        l1.add(c1);
			        map1.put(Math.PI * Math.pow(1.0, 2), l1);
			        List<Circle> l2 = new ArrayList<>();
			        l2.add(c2);
			        map1.put(Math.PI * Math.pow(2.0, 2), l2);
			        List<Circle> l3 = new ArrayList<>();
			        l3.add(c3);
			        map1.put(Math.PI * Math.pow(3.0, 2), l3);
			        List<Circle> l4 = new ArrayList<>();
			        l4.add(c4);
			        l4.add(c4);
			        map1.put(Math.PI * Math.pow(4.0, 2), l4);
			        List<Circle> list1 = List.of(c0, c1, c2, c3, c4, c5);

			        Map<Double, List<Circle>> map2 = new HashMap<>();
			        List<Circle> l5 = new ArrayList<>();
			        l5.add(c0);
			        l5.add(c1);
			        map2.put(Math.PI * Math.pow(1.0, 2), l5);
			        List<Circle> list2 = List.of(c0, c1, c2);

			        // when
			        Probeklausur1.addListToMap(map1, list1);
			        Probeklausur1.addListToMap(map2, list2);

			        // then
			        Map<Double, List<Circle>> expected1 = new HashMap<>();
			        expected1.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1, c0, c1));
			        expected1.put(Math.PI * Math.pow(2.0, 2), List.of(c2, c2));
			        expected1.put(Math.PI * Math.pow(3.0, 2), List.of(c3, c3));
			        expected1.put(Math.PI * Math.pow(4.0, 2), List.of(c4, c4, c4));
			        expected1.put(Math.PI * Math.pow(5.0, 2), List.of(c5));
			        assertEquals(expected1, map1, "click on \"Click to see difference\" in IntelliJ");

			        Map<Double, List<Circle>> expected2 = new HashMap<>();
			        expected2.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1, c0, c1));
			        expected2.put(Math.PI * Math.pow(2.0, 2), List.of(c2));
			        assertEquals(expected2, map2, "click on \"Click to see difference\" in IntelliJ");
			    }

			    @Test
			    @DisplayName("test getFirstCircleOfKey(map, key)")
			    public void testGetFirstCircleOfKey()
			    {
			        System.out.printf("%n------------------ tests getFirstCircleOfKey(map, key) ---------------------%n");
			        // given
			        Map<Double, List<Circle>> map = new HashMap<>();
			        map.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1));
			        map.put(Math.PI * Math.pow(2.0, 2), List.of(c2));
			        map.put(Math.PI * Math.pow(3.0, 2), List.of(c3));
			        map.put(Math.PI * Math.pow(4.0, 2), List.of(c4));
			        map.put(Math.PI * Math.pow(5.0, 2), List.of(c5));

			        //when
			        int key1 = 78;
			        int key2 = 79;
			        Circle c = Probeklausur1.getFirstCircleOfKey(map, key1);
			        Exception e = assertThrows(IllegalArgumentException.class, () -> Probeklausur1.getFirstCircleOfKey(map, key2));

			        // then
			        assertNotNull(c, "Circle should not be null");
			        assertEquals(c5, c, "Circle should have radius=5.0");
			        assertEquals("key 79 not found", e.getMessage());
			    }

			    @Test
			    @DisplayName("test getFirstCircleOfRadius(map, radius)")
			    public void testGetFirstCircleOfRadius()
			    {
			        System.out.printf("%n------------------ tests getFirstCircleOfRadius(map, radius) ---------------------%n");
			        // given
			        Map<Double, List<Circle>> map = new HashMap<>();
			        map.put(Math.PI * Math.pow(1.0, 2), List.of(c0, c1));
			        map.put(Math.PI * Math.pow(2.0, 2), List.of(c2));
			        map.put(Math.PI * Math.pow(3.0, 2), List.of(c3));
			        map.put(Math.PI * Math.pow(4.0, 2), List.of(c4));
			        map.put(Math.PI * Math.pow(5.0, 2), List.of(c5));

			        //when
			        double radius1 = 5.0;
			        double radius2 = 6.0;
			        Optional<Circle> o1 = Probeklausur1.getFirstCircleOfRadius(map, radius1);
			        Optional<Circle> o2 = Probeklausur1.getFirstCircleOfRadius(map, radius2);

			        // then
			        assertTrue(o1.isPresent(), "Optional should not be empty");
			        assertTrue(o2.isEmpty(), "Optional should be empty");
			        assertEquals(c5, o1.get(), "Circle should have radius=5.0");
			    }

			    @Test
			    @DisplayName("test Circle is Comparable")
			    public void testCircleIsComparable()
			    {
			        System.out.printf("%n------------------ test Circle is Comparable ---------------------%n");
			        // given
			        Circle c1 = new Circle(1.0);
			        Circle c2 = new Circle(2.0);
			        Circle c3 = new Circle(1.0);

			        if(c1 instanceof Comparable co1 && c2 instanceof Comparable co2 && c3 instanceof Comparable co3) {
			            //when
			            int result1 = co1.compareTo(co2);
			            int result2 = co2.compareTo(co1);
			            int result3 = co3.compareTo(co1);

			            // then
			            assertTrue(c1 instanceof Comparable, "Circle should be Comparable");
			            assertTrue(result1 < 0, "if smaller then compareTo < 0");
			            assertTrue(result2 > 0, "if bigger then compareTo > 0");
			            assertTrue(result3 == 0, "if equals then compareTo == 0");
			        } else {
			            fail("Circle is not comparable");
			        }
			    }

			    @Test
			    @DisplayName("test createSortedListOfCircles(list)")
			    public void testCreateSortedListOfCircles()
			    {
			        System.out.printf("%n------------------ tests createSortedListOfCircles(list) ---------------------%n");
			        // given
			        List<Circle> l1 = List.of(c0, c1, c2, c3, c4, c5, c0, c1, c2, c3, c4, c5, c4, c5, c0);
			        
			        // when
			        List<Circle> sorted1 = Probeklausur1.createSortedListOfCircles(l1);

			        // then
			        for(int i = 0; i < sorted1.size() -1; i++) {
			            if(sorted1.get(i) instanceof Comparable co1 && sorted1.get(i+1) instanceof Comparable co2) {
			                assertTrue(co1.compareTo(co2) <= 0, "list should be sorted");
			            } else {
			                fail("Circle is not comparable");
			            }
			        }
			    }

			    @Test
			    @DisplayName("test createSortedListOfCirclesEvenRadiiFirst(list)")
			    public void testCreateSortedListOfCirclesEvenRadiiFirst()
			    {
			        System.out.printf("%n------------------ tests createSortedListOfCirclesEvenRadiiFirst(list) ---------------------%n");
			        // given
			        List<Circle> l1 = List.of(c0, c1, c2, c3, c4, c5, c0, c1, c2, c3, c4, c5, c4, c5, c0);
			        List<Circle> sorted = List.of(c2, c2, c4, c4, c4, c0, c1, c0, c1, c0, c3, c3, c5, c5, c5);
			        // when
			        List<Circle> sorted1 = Probeklausur1.createSortedListOfCirclesEvenRadiiFirst(l1);

			        // then
			        for(int i = 0; i < sorted1.size(); i++) {
			            assertTrue(sorted1.get(i).equals(sorted.get(i)), "list should be sorted, even radii first");
			        }
			    }
			}

			```

	***Aufgabe***

	2. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `union(List<Circle> li1, List<Circle> li2)`. Diese Methode gibt eine `List<Circle>` zurück. Die zurückgegebene Liste enthält alle Circle-Objekte aus der als Parameter übergebenen Listen `li1` **und** `li2`. Aber **Achtung!**: es soll kein Circle doppelt vorkommen, d.h. für alle `c1` und `c2`, die in der zurückgegebenen Liste vorkommen, gilt `!c1.equals(c2)`. <br/>
	--> In `Probeklausur1Test` siehe Testmethode `testUnion()`.

	3. Rufen Sie die `union()`-Methode in der `main`-Methode auf. Übergeben Sie die Listen `list1` und `list2`. Geben Sie die zurückgegebene Liste in der folgenden Form auf der Konsole aus:

		```bash
		Circle [radius=1.0] area=  3,14 circumference= 6,28 
		Circle [radius=2.0] area= 12,57 circumference=12,57 
		Circle [radius=3.0] area= 28,27 circumference=18,85 
		Circle [radius=4.0] area= 50,27 circumference=25,13 
		Circle [radius=5.0] area= 78,54 circumference=31,42 
		```

	4. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `createMap(List<Circle> circles)`. Diese Methode gibt eine `Map<Double, List<Circle>>` zurück. Die Schlüssel in der `Map` sind die Flächeninhalte (`area`) der Circles aus der Liste `circles`. Die Werte in der `Map` sind jeweils eine Liste aller Circle-Objekte aus der Liste `circles` mit diesem Flächeninhalt. <br/>
	--> In `Probeklausur1Test` siehe Testmethode `testCreateMap()`.

	5. Rufen Sie die `createMap()`-Methode in der `main`-Methode auf. Übergeben Sie die Liste `list1`. Geben Sie die zurückgegebene Map in der folgenden Form auf der Konsole aus (Reihenfolge egal und Zusatzwerte):

		```bash
		-- area =  78,54 --
		Circle [radius=5.0]
		Circle [radius=5.0]

		-- area =  28,27 --
		Circle [radius=3.0]
		Circle [radius=3.0]

		-- area =  50,27 --
		Circle [radius=4.0]
		Circle [radius=4.0]
		Circle [radius=4.0]

		-- area =  12,57 --
		Circle [radius=2.0]
		Circle [radius=2.0]

		-- area =   3,14 --
		Circle [radius=1.0]
		```

	6. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `addListToMap(Map<Double, List<Circle>> map, List<Circle> circles)`. Diese Methode fügt der `Map<Double, List<Circle>>` alle Circle-Objekte aus der Liste `circles` hinzu. Die Schlüssel in der `Map` sind die Flächeninhalte (`area`) der Circles. Die entsprechenden Werte in `map` sind jeweils eine Liste von Circle-Objekten mit diesem Flächeninhalt. Diesen Listen müssen passend die Circle-Objekte aus `circles` hinzugefügt werden. <br/>
	--> In `Probeklausur1Test` siehe Testmethode `testAddListToMap()`.

	7. Rufen Sie die `addListToMap()`-Methode in der `main`-Methode auf. Übergeben Sie die Liste `list2`. Geben Sie die zurückgegebene Map in der folgenden Form auf der Konsole aus (Reihenfolge egal und Zusatzwerte):

		```bash
		-- area =  78,54 --
		Circle [radius=5.0]
		Circle [radius=5.0]
		Circle [radius=5.0]

		-- area =  28,27 --
		Circle [radius=3.0]
		Circle [radius=3.0]
		Circle [radius=3.0]

		-- area =  50,27 --
		Circle [radius=4.0]
		Circle [radius=4.0]
		Circle [radius=4.0]
		Circle [radius=4.0]
		Circle [radius=4.0]

		-- area =  12,57 --
		Circle [radius=2.0]
		Circle [radius=2.0]
		Circle [radius=2.0]
		Circle [radius=2.0]
		Circle [radius=2.0]
		Circle [radius=2.0]

		-- area =   3,14 --
		Circle [radius=1.0]
		Circle [radius=1.0]
		Circle [radius=1.0]
		```

	8. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `getFirstCircleOfKey(Map<Double, List<Circle>> map, int key)`. Diese Methode gibt ein `Circle`-Objekt zurück oder wirft eine `IllegalArgumentException`. In der `map` wird nach einem Schlüssel gesucht, dessen ganzzahliger Wert dem `int key` entspricht, d.h.

     	- der Schlüssel `78,654...` in der `map` passt zu `key=78`
     	- der Schlüssel `79,01...` in der `map` passt nicht zu 78

     	Falls ein solcher Schlüssel nicht in der `map` existiert, wird eine `IllegalArgumentException` geworfen. Die Nachricht enthält den Wert des Schlüssels, nach dem gesucht wurde, z.B. 'key 79 not found'. <br>
		Falls ein solcher Schlüssel existiert, wird der erste `Circle` aus der `value`-Liste des Schlüssels zurückgegeben <br/>
		--> In `Probeklausur1Test` siehe Testmethode `testGetFirstCircleOfKey()`.

	9. Rufen Sie die `getFirstCircleOfKey()`-Methode in der `main`-Methode innerhalb der `for(int key = 78; key < 80; key++) {}` auf und verwenden Sie den `key`. Übergeben Sie die aktuelle `map`. Wird ein `Circle` zurückgegeben, geben Sie ihn auf der Konsole aus. Wird eine `IllegalArgumentException` geworfen, geben Sie die *Exception-Message* aus:

		```bash
		found : Circle [radius=5.0]
		key 79 not found
		```

	10. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `getFirstCircleOfRadius(Map<Double, List<Circle>> map, double radius)`. Diese Methode gibt ein `Optional<Circle>`-Objekt zurück. In der `map` wird in den `value`-Listen nach einem `Circle` mit dem Radius `radius` gesucht. Falls ein solcher `Circle` nicht in der `map` existiert, wird ein leeres `Optional` zurückgegeben. Falls ein solcher `Circle` existiert, wird er als Wert des `Optional`-Objektes zurückgegeben. <br/>
	--> In `Probeklausur1Test` siehe Testmethode `testGetFirstCircleOfRadius()`.

	11. Rufen Sie die `getFirstCircleOfRadius()`-Methode in der `main`-Methode innerhalb der `for(double radius = 5.0; radius < 7.0; radius++) {}` auf und verwenden Sie den `radius`. Übergeben Sie die aktuelle `map`. Enthält das zurückgegebene `Optional`-Objekt ein `Circle`-Objekt, geben Sie es auf der Konsole aus. Wird ein leeres `Optional` zurückgegeben, geben Sie `no circle with radius=7.0 found` (Wert von `radius` einsetzen) aus:

		```bash
		found for radius=5.0 : Circle [radius=5.0]
		no circle with radius=6.0 found
		```

	12. Implementieren Sie in der Klasse `Circle.java` das Interface [Comparable](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html), so dass ein `Circle` größer ist als ein anderer, wenn sein `radius` größer ist.<br/>
	--> In `Probeklausur1Test` siehe Testmethode `testCircleIsComparable()`.

	13. Rufen Sie in der `main`-Methode unterhalb von 

		```java
        Circle c1 = createCircle(3);
        Circle c2 = createCircle(3);
        System.out.println("c1: " + c1);
        System.out.println("c2: " + c2);
		```

		die `compareTo()`-Methode auf und erzeugen Sie je nach Resultat eine der drei Ausgaben:

		```bash
		c1 is equal to c2
		c1 is less than c2
		c1 is greater than c2
		```

	14. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `createSortedListOfCircles(List<Circle> circles)`. Diese Methode gibt eine `List<Circle>` zurück. Die übergebene Liste ist unsortiert. In der zurückgegebenen Liste sollen die `Circle`-Objekte unter Verwendung der *natural order* (`compareTo()`) aufsteigend sortiert sein (kleinster zuerst) <br/>
	--> In `Probeklausur1Test` siehe Testmethode `testCreateSortedListOfCircles()`.

	15. Rufen Sie die `createSortedListOfCircles()`-Methode in der `main`-Methode auf und verwenden Sie `list1` als Parameter. Geben Sie `list1` in der folgenden Form aus (die Radien der `Circle`-Objekte aus `list1` - Zufallswerte):

		```bash
		[ 3,0 3,0 1,0 5,0 1,0 1,0 1,0 1,0 1,0 5,0 ]
		```
		
		Geben Sie durch `createSortedListOfCircles()` erzeugte Liste ebenso aus:

		```bash
		[ 1,0 1,0 1,0 1,0 1,0 1,0 3,0 3,0 5,0 5,0 ]
		```

	16. Implementieren Sie in der Klasse `Probeklausur1.java` die Methode `createSortedListOfCirclesEvenRadiiFirst(List<Circle> circles)`. Diese Methode gibt eine `List<Circle>` zurück. Die übergebene Liste ist unsortiert. In der zurückgegebenen Liste sollen die `Circle`-Objekte unter Verwendung der *natural order* (`compareTo()`) aufsteigend sortiert sein (kleinster zuerst). Aber **Achtung!**. es sollen zuerst die `Circle`-Objekte mit *geraden* Radien und dann die `Circle`-Objekte mit ungeraden Radien kommen <br/>
	--> In `Probeklausur1Test` siehe Testmethode `testCreateSortedListOfCirclesEvenRadiiFirst()`.

	17. Rufen Sie die `createSortedListOfCirclesEvenRadiiFirst()`-Methode in der `main`-Methode auf und verwenden Sie `list1` als Parameter. Erzeugen Sie folgende Ausgaben (Zufallswerte):

		```bash
		[ 3,0 2,0 5,0 2,0 3,0 1,0 5,0 2,0 3,0 1,0 ]
		[ 2,0 2,0 2,0 1,0 1,0 3,0 3,0 3,0 5,0 5,0 ]
		```
		


??? success "mögliche Lösung für Probeklausur1"
	
	=== "Probeklausur1.java"
		```java
		package probeklausuren.probeklausur1;

		import java.util.*;
		import java.util.stream.Collectors;

		public class Probeklausur1
		{
		    static Random r =  new Random();

		    public static Circle createCircle(int bound)
		    {
		        int randNr = r.nextInt(bound);
		        if(randNr < 2)
		        {
		            return new Circle();
		        }
		        else
		        {
		            return new Circle(randNr);
		        }
		    }

		    public static List<Circle> setUpCircleList(int listLength, int bound)
		    {
		        List<Circle> list = new ArrayList<Circle>();
		        for(int i = 0; i < listLength; i++)
		        {
		            list.add(createCircle(bound));
		        }
		        return list;
		    }

		    /*
		     *   gibt eine Liste mit allen Elementen aus c1 UND c2 zurueck
		     *   in der Liste darf jedoch kein Element doppelt vorkommen, d.h.
		     *   wenn e1 in Liste und e2 in Liste, dann gilt !e1.equals(e2)
		     */
		    public static List<Circle> union(List<Circle> c1, List<Circle> c2)
		    {
		        Set<Circle> unionSet = new HashSet<>(c1);
		        unionSet.addAll(c2);
		        List<Circle> union = new ArrayList<>();
		        union.addAll(unionSet);
		        return union;
		    }


		    /*
		     *   gibt eine Map zurueck
		     *   Schluessel sind die Flaecheninhalte (area) der Circles
		     *   Werte sind eine Liste aller Circle-Objekte mit diesem Flaecheninhalt
		     */
		    public static Map<Double, List<Circle>> createMap(List<Circle> circles)
		    {
		        Map<Double, List<Circle>> map = new HashMap<>();
		        for(Circle c : circles)
		        {
		            double area = c.area();
		            if(!map.containsKey(area))
		            {
		                List<Circle> list = new ArrayList<>();
		                list.add(c);
		                map.put(area, list);
		            }
		            else
		            {
		                List<Circle> list = map.get(area);
		                list.add(c);
		            }
		        }
		        return map;
		    }

		    /*
		     *   fuegt der map alle circles passend hinzu
		     */
		    public static void addListToMap(Map<Double, List<Circle>> map, List<Circle> circles)
		    {
		        for(Circle c : circles)
		        {
		            double area = c.area();
		            if(!map.containsKey(area))
		            {
		                List<Circle> list = new ArrayList<>();
		                list.add(c);
		                map.put(area, list);
		            }
		            else
		            {
		                List<Circle> list = map.get(area);
		                list.add(c);
		            }
		        }
		    }

		    /*
		     *   - uebergeben wird eine map, deren keys vom Typ Double sind
		     *   - der Schluessel key ist vom Typ int
		     *   - in der map wird nach einem Schluessel gesucht, dessen ganzzahliger
		     *      Wert dem int key entspricht, d.h.
		     *          78,654 passt zu 78
		     *          79,01 passt nicht zu 78
		     *   - falls ein solcher Schluessel nicht in der map existiert, wird eine
		     *      IllegalArgumentException geworfen. Die Nachricht enthaelt den Wert des
		     *      Schlussels, nach dem gesucht wurde, z.B. 'key 79 not found'
		     *   - falls ein solcher Schluessel existiert, wird der erste Circle aus der
		     *      Liste zu dem Schluessel zurueckgegeben
		     */
		    public static Circle getFirstCircleOfKey(Map<Double, List<Circle>> map, int key)
		    {
		        Double doubleKey = 0.0;
		        for(Double key2 : map.keySet())
		        {
		            if(key2-key < 1 && key2-key > 0)
		            {
		                doubleKey = key2;
		            }
		        }
		        if(doubleKey > 0.0) {
		            return map.get(doubleKey).getFirst();
		        } else {
		            throw new IllegalArgumentException("key " + key + " not found");
		        }
		    }

		    /*
		     *   - uebergeben wird eine map, deren keys vom Typ Double sind (area())
		     *   - die Werte sind vom Typ List<Circle>
		     *   - in der map (in den values) wird nach einem Circle gesucht, dessen
		     *     Radius dem Parameterwert von double radius entspricht
		     *   - falls ein solcher Circle existiert, wird er dem Optional hinzugefuegt
		     *     und zurückgegeben
		     *   - falls ein solcher Circle nicht existiert, wird ein leeres Optional
		     *     zurueckgegeben
		     */
		    public static Optional<Circle> getFirstCircleOfRadius(Map<Double, List<Circle>> map, double radius)
		    {
		        Collection<List<Circle>> circles = map.values();
		        for(List<Circle> circleList : circles)
		        {
		            for(Circle circle : circleList)
		            {
		                if(Double.compare(circle.getRadius(), radius) == 0)
		                {
		                    return Optional.of(circle);
		                }
		            }
		        }
		        return Optional.empty();
		    }

		    /*
		     * uebergeben wird eine unsortierte Liste von Circle-Objekten
		     * zurueckgegeben wird eine sortierte Liste von Circle-Objekte
		     * sortiert nach "natural order" (compareTo)
		     */
		    public static List<Circle> createSortedListOfCircles(List<Circle> circles)
		    {
		        return circles.stream().sorted().collect(Collectors.toList());
		    }

		    /*
		     * uebergeben wird eine unsortierte Liste von Circle-Objekten
		     * zurueckgegeben wird eine sortierte Liste von Circle-Objekte
		     * - sortiert nach "natural order" (compareTo)
		     * - gerade Radien zuerst!!!
		     */
		    public static List<Circle> createSortedListOfCirclesEvenRadiiFirst(List<Circle> circles)
		    {
		        Map<Boolean, List<Circle>> map = circles.stream().collect(Collectors.partitioningBy(c -> c.getRadius() % 2 == 1));
		        List<Circle> circleList = map.values().stream().flatMap(v -> v.stream().sorted()).collect(Collectors.toList());
		        return circleList;
		    }

		    /*
		     * Hilfsmethode zur Ausgabe einer Map<Double, List<Circle>>
		     */
		    private static void printMapOfCircles(Map<Double, List<Circle>> map)
		    {
		        for(Map.Entry<Double, List<Circle>> entry : map.entrySet())
		        {
		            double area = entry.getKey();
		            System.out.printf("%n-- area = %6.2f --%n",area);
		            List<Circle> list = entry.getValue();
		            for(Circle c : list)
		            {
		                System.out.println(c);
		            }
		        }
		    }

		    public static void main(String[] args)
		    {
		        System.out.printf("%n%n ---------------------- list1 und list2 ----------------------%n%n");
		        List<Circle> list1 = setUpCircleList(10, 6);
		        List<Circle> list2 = setUpCircleList(10, 6);
		        System.out.println("list1: ");
		        list1.forEach(System.out::println);
		        System.out.println();
		        System.out.println("list2: ");
		        list2.forEach(System.out::println);

		        System.out.printf("%n%n -------------------- union(list1, list2) --------------------%n%n");
					        /* print List of union(list1, list2)
					        * z.B.:
					            Circle [radius=1.0] area=  3,14 circumference= 6,28
					            Circle [radius=3.0] area= 28,27 circumference=18,85
					            Circle [radius=4.0] area= 50,27 circumference=25,13
					            Circle [radius=5.0] area= 78,54 circumference=31,42
					        */
		        List<Circle> union = union(list1, list2);
		        for(Circle c : union)
		        {
		            System.out.printf("%s area=%6.2f circumference=%5.2f %n", c, c.area(), c.circumference());
		        }

		        System.out.printf("%n%n -------------------- createMap(list1) --------------------%n%n");
					        /* print Map of createMap(list1)
					        * z.B.:
					            -- area =  28,27 --
					            Circle [radius=3.0]
					            Circle [radius=3.0]

					            -- area =  78,54 --
					            Circle [radius=5.0]

					            -- area =   3,14 --
					            Circle [radius=1.0]
					            Circle [radius=1.0]
					            Circle [radius=1.0]
					            Circle [radius=1.0]
					            Circle [radius=1.0]

					            -- area =  50,27 --
					            Circle [radius=4.0]

					            -- area =  12,57 --
					            Circle [radius=2.0]
					        */
		        Map<Double, List<Circle>> map = createMap(list1);
		        printMapOfCircles(map);

		        System.out.printf("%n%n -------------------- addListToMap(map,list2) --------------------%n%n");
					        /* print Map of addListToMap(map,list2)
					        * z.B.:
					            -- area =  28,27 --
					            Circle [radius=3.0]
					            Circle [radius=3.0]

					            -- area =  78,54 --
					            Circle [radius=5.0]

					            -- area =   3,14 --
					            Circle [radius=1.0]
					            Circle [radius=1.0]
					            Circle [radius=1.0]
					            Circle [radius=1.0]
					            Circle [radius=1.0]

					            -- area =  50,27 --
					            Circle [radius=4.0]

					            -- area =  12,57 --
					            Circle [radius=2.0]
					        */
		        addListToMap(map, list2);
		        printMapOfCircles(map);

		        System.out.printf("%n%n -------------------- getFirstCircleOfKey(map,int) --------------------%n%n");
		        for(int key = 78; key < 80; key++) {
		            try {
		                Circle first = getFirstCircleOfKey(map, key);
		                System.out.println("found : " + first);
		            } catch (IllegalArgumentException e) {
		                System.out.println(e.getMessage());
		            }
		        }

		        System.out.printf("%n%n -------------------- getFirstCircleOfRadius(map,double) --------------------%n%n");
		        for(double radius = 5.0; radius < 7.0; radius++) {
		            Optional<Circle> first = getFirstCircleOfRadius(map, radius);
		            if(first.isPresent()) {
		                System.out.println("found for radius=" + radius +" : " + first.get());
		            } else {
		                System.out.println("no circle with radius=" + radius +" found");
		            }
		        }

		        System.out.printf("%n%n -------------------- Circle is Comparable  --------------------%n%n");
		        Circle c1 = createCircle(3);
		        Circle c2 = createCircle(3);
		        System.out.println("c1: " + c1);
		        System.out.println("c2: " + c2);

		        if(c1.compareTo(c2) == 0) System.out.println("c1 is equal to c2");
		        else if(c1.compareTo(c2) > 0) System.out.println("c1 is greater than c2");
		        else System.out.println("c1 is smaller than c2");

		        System.out.printf("%n%n -------------------- createSortedListOfCircles(list) --------------------%n%n");

		        List<Circle> sortedList = createSortedListOfCircles(list1);
		        sortedList.forEach(System.out::println);

		        System.out.printf("%n%n -------------------- createSortedListOfCirclesEvenRadiiFirst(list) --------------------%n%n");
		        List<Circle> circles = createSortedListOfCirclesEvenRadiiFirst(list1);
		        circles.forEach(System.out::println);
		    }
		}

		```


##### Probeklausur 2

??? "Probeklausur 2"

	1. Gegeben ist der `record Person` wie folgt: 

	    ```java
	    public record Person(String vorname, String nachname, int alter, String ort)
	    {
	        @Override
	        public String toString()
	        {
	            return String.format("%-8s %-9s aus %-9s ist %2d Jahre alt.",
	                    this.vorname, this.nachname, this.ort, this.alter);
	        }
	    }
	    ```

	2. Gegeben sind die Klassen `Probeklausur2` und `Probeklausur2Test` wie folgt:

	    === "Probeklausur2.java"
	        ```java
	        probeklausuren.probeklausur2;

	        import java.util.*;
	        import java.util.stream.Stream;

	        public class Probeklausur2
	        {
	            static Random r = new Random();

	            // Hilfsmethode - bleibt unveraendert (koenen Sie zuklappen)
	            private static Person createPerson()
	            {
	                String[] vornamen = { "Sophie", "Hannah", "Emma", "Mia", "Anna", "Elif",
	                        "Zeynep", "Fatma", "Aylin", "Derya", "Layla", "Aisha", "Noor",
	                        "Salma", "Mariam" };
	                String[] nachnamen = { "Schmidt", "Schneider", "Fischer", "Weber",
	                        "Wagner", "Becker", "Yilmaz", "Kaya", "Demir", "Polat",
	                        "Aydın", "Arslan", "Al-Haddad", "Al-Mufti", "Ibrahim", "Khalil",
	                        "Mansour" };
	                String[] orte = { "Berlin", "Hamburg", "Potsdam", "Dresden", "Magdeburg",
	                        "Stuttgart", "Leipzig", "Dortmund", "Essen", "Bremen"
	                };
	                String vorname = vornamen[r.nextInt(vornamen.length)];
	                String nachname = nachnamen[r.nextInt(nachnamen.length)];
	                String ort = orte[r.nextInt(orte.length)];
	                int alter = r.nextInt(10, 100);
	                return new Person(vorname, nachname, alter, ort);
	            }

	            // Hilfsmethode - bleibt unveraendert (koenen Sie zuklappen)
	            private static Set<Person> createSetOfPersonen(int numberOfPersonen)
	            {
	                Set<Person> personen = new HashSet<>();
	                for(int i = 0; i < numberOfPersonen; i++)
	                {
	                    personen.add(createPerson());
	                }
	                return personen;
	            }

	            // TODO siehe 3.
	            public static Set<Person> createSetAelterAls(int alter, Set<Person> personen1, Set<Person> personen2)
	            {
	                return null; // TODO siehe 3.
	            }

	            // TODO siehe 5.
	            public static Map<String, Set<Person>> createMapOrtPersonen(Set<Person> personen1, Set<Person> personen2)
	            {
	                return null; // TODO siehe 5.
	            }

	            // TODO siehe 10.
	            public static Person getPersonAusOrt(Set<Person> personen, String ort)
	            {
	                return null; // TODO siehe 10.
	            }

	            // TODO siehe 13.
	            public static Optional<Person> getPersonMitAlter(Set<Person> personen, int alter)
	            {
	                return null; // TODO siehe 13.
	            }

	            public static void main(String[] args)
	            {
	                // --------------- Vorbereitung - bleibt so ----------
	                Set<Person> personen1 = createSetOfPersonen(10);
	                Set<Person> personen2 = createSetOfPersonen(10);
	                System.out.printf("%n%n--------------- personen1 set---------------------%n%n");
	                personen1.forEach(System.out::println);
	                System.out.printf("%n%n--------------- personen2 set---------------------%n%n");
	                personen2.forEach(System.out::println);

	                // --------------- ab hier geht's los ----------------

	                System.out.printf("%n%n--------------- createSetAelterAls(alter, personen1, personen2) ---------------------%n%n");
	                int alter = r.nextInt(10, 100);
	                System.out.println("alle Personen aelter als " + alter + ": ");
	                // TODO siehe 4.

	                System.out.printf("%n%n--------------- createMapOrtPersonen(personen1, personen2) ---------------------%n%n");
	                // TODO siehe 6.

	                System.out.printf("%n%n--------------- sortieren von personen1 - compareTo ---------------------%n%n");
	                // TODO siehe 8.

	                System.out.printf("%n%n--------------- sortieren von personen2 - nach Alter ---------------------%n%n");
	                // TODO siehe 9.

	                System.out.printf("%n%n--------------- getPersonAusOrt(Set<Person> personen, String ort) ---------------------%n%n");
	                // TODO siehe 11.

	                System.out.printf("%n%n--------------- getPersonMitAlter(Set<Person> personen, int alter) ---------------------%n%n");
	                for(int alter1 = 20; alter1 < 30; alter1++) {
	                    // TODO siehe 14.
	                }

	                System.out.printf("%n%n--------------- stream Map Anfangsbuchstabe ---------------------%n%n");
	                Stream<Person> stream1 = Stream.generate(() -> createPerson()).limit(20);
	                // TODO siehe 15.

	                // TODO siehe 16.

	                // TODO siehe 17.

	            }

	        }
	        ```
	    === "Probeklausur2Test.java"
	        ```java
	        probeklausuren.probeklausur2;

	        import org.junit.jupiter.api.BeforeAll;
	        import org.junit.jupiter.api.DisplayName;
	        import org.junit.jupiter.api.Test;

	        import java.util.*;
	        import java.util.stream.Collectors;

	        import static org.junit.jupiter.api.Assertions.*;

	        public class Probeklausur2Test
	        {
	            static Person p1, p2, p3, p4, p5, p6, p7, p8, p9, p10,
	                    p11, p12, p13, p14, p15, p16, p17, p18, p19, p20;
	            static Set<Person> persons1,  persons2;

	            @BeforeAll
	            public static void setUp()
	            {
	                p1 = new Person("Zeynep", "Al-Haddad", 75, "Stuttgart");
	                p2 = new Person("Mia", "Wagner", 93, "Berlin");
	                p3 = new Person("Mariam", "Yilmaz", 33, "Berlin");
	                p4 = new Person("Zeynep", "Becker", 12, "Bremen");
	                p5 = new Person("Fatma", "Becker", 27, "Magdeburg");
	                p6 = new Person("Layla", "Aydın", 10, "Essen");
	                p7 = new Person("Emma", "Al-Haddad", 83, "Hamburg");
	                p8 = new Person("Mia", "Al-Mufti", 27, "Hamburg");
	                p9 = new Person("Anna", "Schmidt", 45, "Potsdam");
	                p10 = new Person("Elif", "Al-Mufti", 92, "Magdeburg");
	                p11 = new Person("Anna", "Ibrahim", 61, "Bremen");
	                p12 = new Person("Aisha", "Wagner", 78, "Potsdam");
	                p13 = new Person("Elif", "Fischer", 42, "Dortmund");
	                p14 = new Person("Emma", "Becker", 15, "Potsdam");
	                p15 = new Person("Aylin", "Khalil", 72, "Bremen");
	                p16 = new Person("Elif", "Ibrahim", 82, "Berlin");
	                p17 = new Person("Elif", "Fischer", 12, "Leipzig");
	                p18 = new Person("Noor", "Al-Mufti", 62, "Berlin");
	                p19 = new Person("Mariam", "Becker", 48, "Dresden");
	                p20 = new Person("Noor", "Schneider", 98, "Leipzig");

	                persons1 = Set.of(p1, p2, p3, p4, p5, p6, p7, p8, p9, p10);
	                persons2 = Set.of(p11, p12, p13, p14, p15, p16, p17, p18, p19, p20);
	            }

	            private Comparator<Person> helpSort()
	            {
	                return (o1, o2) -> (o1.nachname().compareTo(o2.nachname()) == 0) ?
	                        o1.vorname().compareTo(o2.vorname()) :
	                        o1.nachname().compareTo(o2.nachname());
	            }

	            @Test
	            @DisplayName("createSetAelterAls()")
	            public void testCreateSetAelterAls()
	            {
	                // given persons1 and persons2
	                int alter = 50;

	                // when
	                Set<Person> aelterAls50 = Probeklausur2.createSetAelterAls(alter, persons1, persons2);
	                List<Person> aelterAls50Sorted = aelterAls50.stream().sorted().collect(Collectors.toList());
	                Set<Person> expected = Set.of(p1, p2, p7, p10, p11, p12, p15, p16, p18, p20);
	                List<Person> expectedSorted = expected.stream().sorted().collect(Collectors.toList());

	                // then
	                assertEquals(expectedSorted, aelterAls50Sorted, "createSetAelterAls() doesn't seem to work properly yet");
	            }

	            @Test
	            @DisplayName("createMapOrtPersonen()")
	            public void testCreateMapOrtPersonen()
	            {
	                // given persons1 and persons2

	                // when
	                Map<String, Set<Person>> mapOrte = Probeklausur2.createMapOrtPersonen(persons1, persons2);
	                Set<String> orteSet = mapOrte.keySet();
	                List<String> orteSetSorted = orteSet.stream().sorted().collect(Collectors.toList());

	                Collection<Set<Person>> valuesColl = mapOrte.values();
	                List<List<Person>> valuesLists = new ArrayList<>();
	                for(Set<Person> set : valuesColl)
	                {
	                    valuesLists.add(set.stream().collect(Collectors.toList()));
	                }
	                List<Person> valuesListSorted = valuesLists.stream()
	                        .flatMap( l -> l.stream().sorted( helpSort()) )
	                        .sorted( (o1, o2) -> o1.ort().compareTo(o2.ort()) )
	                        .collect(Collectors.toList());

	                Set<String> orteExpected = Set.of("Stuttgart", "Berlin", "Bremen", "Magdeburg",
	                                "Essen", "Hamburg", "Potsdam", "Dortmund", "Leipzig", "Dresden");
	                List<String> orteExpectedSorted = orteSetSorted.stream().sorted().collect(Collectors.toList());
	                List<Person> stuttgart = List.of(p1);
	                List<Person> berlin = List.of(p2, p3, p16, p18);
	                List<Person> bremen = List.of(p4, p11, p15);
	                List<Person> magdeburg = List.of(p5, p10);
	                List<Person> essen = List.of(p6);
	                List<Person> hamburg = List.of(p7, p8);
	                List<Person> potsdam = List.of(p9, p12, p14);
	                List<Person> dortmund = List.of(p13);
	                List<Person> dresden = List.of(p19);
	                List<Person> leipzig = List.of(p17, p20);
	                List<List<Person>> expectedSets = List.of(stuttgart, berlin, bremen, magdeburg, essen, hamburg, potsdam,
	                        dortmund, dresden, leipzig);
	                List<Person> expectedSetsSorted = expectedSets.stream()
	                        .flatMap( l -> l.stream().sorted( helpSort()) )
	                        .sorted( (o1, o2) -> o1.ort().compareTo(o2.ort()) )
	                        .collect(Collectors.toList());

	                // then
	                assertTrue(mapOrte instanceof Map<String, Set<Person>>, "createMapOrtPersonen() doesn't seem to work properly yet (wrong return type)");
	                assertEquals(orteExpectedSorted, orteSetSorted, "createMapOrtPersonen() doesn't seem to work properly yet (wrong key set)");
	                assertEquals(expectedSetsSorted, valuesListSorted, "createMapOrtPersonen() doesn't seem to work properly yet (wrong value collection)");
	            }

	            @Test
	            @DisplayName("Person is Comparable")
	            public void testPersonIsComparable() {
	                // given
	                Set<Person> unsorted = Set.of(p1, p4, p5, p14, p19);
	                List<Person> expected = List.of(p1, p14, p5, p19, p4);

	                Object o = p1;
	                if(o instanceof Comparable) {
	                    // when
	                    List<Person> sorted = unsorted.stream().sorted().collect(Collectors.toList());

	                    // then
	                    assertEquals(expected, sorted, "compareTo of Person not working properly yet ");
	                }
	                else {
	                    fail("Person is not Comparable yet");
	                }
	            }

	            @Test
	            @DisplayName("getPersonMitAlter()")
	            public void testGetPersonMitAlter()
	            {
	                int alter = 42;
	                Optional<Person> result1 = Probeklausur2.getPersonMitAlter(persons1, alter);
	                Optional<Person> result2 = Probeklausur2.getPersonMitAlter(persons2, alter);
	                assertTrue(result1.isEmpty(),"getPersonMitAlter() doesn't seem to work properly yet");
	                assertEquals(result2.get(), p13, "getPersonMitAlter() doesn't seem to work properly yet");
	            }

	            /*
	             * Schreiben Sie hinter diesem Kommentar Ihre beiden Testfaelle fuer 12.
	             */
	        }

	        ```

	3. Implementieren Sie die Methode `createSetAelterAls(int alter, Set<Person> personen1, Set<Person> personen2)`. Diese Methode gibt eine `Set<Person>` zurück. Die zurückgegebene `Set` anthält alle `Person`-Objekte aus `personen1` **und** `personen2`, die älter als `alter` sind. 

	    --> siehe `testCreateSetAelterAls()` in `Probeklausur2Test` (Anzeige `createSetAelterAls()`)

	4. Rufen Sie die `createSetAelterAls()`-Methode in der `main`-Methode auf und geben Sie die zurückgegebene `Set` wie folgt auf der Konsole aus (Zufallswerte!):

	    ```bash
	    alle Personen aelter als 73: 
	    Zeynep   Mansour   aus Stuttgart ist 93 Jahre alt.
	    Elif     Arslan    aus Leipzig   ist 95 Jahre alt.
	    Anna     Al-Mufti  aus Hamburg   ist 95 Jahre alt.
	    Zeynep   Fischer   aus Leipzig   ist 76 Jahre alt.
	    Sophie   Demir     aus Berlin    ist 95 Jahre alt.
	    Salma    Schneider aus Magdeburg ist 96 Jahre alt.
	    ```

	5. Implementieren Sie die Methode `createMapOrtPersonen(Set<Person> personen1, Set<Person> personen2)`. Diese Methode gibt eine `Map<String, Set<Person>` zurück. Beachten Sie, dass der `value` in der `Map` eine `Set` und keine `List` ist! Die zurückgegebene `Set` anthält einmalig alle `Person`-Objekte aus `personen1` **und** `personen2`. Schlüssel der Map sind die `ort`-Eigenschaften der `Person`-Objekte. 

	    --> siehe `testCreateMapOrtPersonen()` in `Probeklausur2Test` (Anzeige `createMapOrtPersonen()`)

	6. Rufen Sie die `createMapOrtPersonen()`-Methode in der `main`-Methode auf und geben Sie die zurückgegebene `Map` wie folgt auf der Konsole aus (Zufallswerte!):

	    ```bash
	    aus Bremen kommen : 
	     Hannah Aydın

	    aus Stuttgart kommen : 
	     Zeynep Mansour
	     Mia Al-Mufti
	     Aylin Schneider
	     Layla Demir

	    aus Berlin kommen : 
	     Mia Fischer
	     Sophie Demir

	    aus Potsdam kommen : 
	     Elif Fischer

	    aus Leipzig kommen : 
	     Elif Arslan
	     Zeynep Fischer
	     Anna Schneider

	    aus Magdeburg kommen : 
	     Salma Schneider
	     Fatma Wagner

	    aus Dortmund kommen : 
	     Zeynep Demir
	     Mariam Wagner

	    aus Hamburg kommen : 
	     Emma Al-Haddad
	     Anna Al-Mufti
	     Layla Weber
	     Fatma Ibrahim

	    aus Essen kommen : 
	     Fatma Aydın
	    ```

	7. Implementieren Sie für die Klasse `Student` das `Comparable`-Interface so, dass eine Ordnung über die Nachnamen (`nachname`) entsteht. Bei gleichem Nachnamen, wird die Ordnung über den Vornamen (`vorname`) erweitert. 

	    --> siehe `testPersonIsComparable()` in `Probeklausur2Test` (Anzeige `Person is Comparable`)

	8. Erzeugen Sie in der `main`-Methode aus der Menge `personen1` eine sortierte Liste unter Verwendung von `compareTo()`. Geben Sie die sortierte Liste wie folgt aus (Zufallswerte!):

	    ```bash
	    Aylin    Aydın     aus Leipzig   ist 48 Jahre alt.
	    Hannah   Aydın     aus Magdeburg ist 37 Jahre alt.
	    Aisha    Becker    aus Berlin    ist 64 Jahre alt.
	    Fatma    Demir     aus Potsdam   ist 27 Jahre alt.
	    Salma    Kaya      aus Leipzig   ist 85 Jahre alt.
	    Sophie   Kaya      aus Berlin    ist 53 Jahre alt.
	    Derya    Polat     aus Dortmund  ist 41 Jahre alt.
	    Mariam   Schmidt   aus Stuttgart ist 61 Jahre alt.
	    Emma     Schneider aus Dortmund  ist 70 Jahre alt.
	    Layla    Yilmaz    aus Magdeburg ist 51 Jahre alt.
	    ```


	9. Erzeugen Sie in der `main`-Methode aus der Menge `personen2` eine nach Alter sortierte Liste. Geben Sie die sortierte Liste wie folgt aus (Zufallswerte!):

	    ```bash
	    Noor     Ibrahim   aus Hamburg   ist 30 Jahre alt.
	    Elif     Wagner    aus Leipzig   ist 35 Jahre alt.
	    Fatma    Weber     aus Dresden   ist 41 Jahre alt.
	    Aylin    Weber     aus Leipzig   ist 52 Jahre alt.
	    Layla    Khalil    aus Berlin    ist 58 Jahre alt.
	    Zeynep   Demir     aus Bremen    ist 60 Jahre alt.
	    Sophie   Arslan    aus Potsdam   ist 62 Jahre alt.
	    Hannah   Schneider aus Essen     ist 71 Jahre alt.
	    Noor     Yilmaz    aus Essen     ist 97 Jahre alt.
	    Emma     Wagner    aus Bremen    ist 98 Jahre alt.
	    ```

	10. Implementieren Sie die Methode `getPersonAusOrt(Set<Person> personen, String ort)`. Diese Methode gibt die (erste) `Person` aus der Menge `personen` zurück, die im Ort `ort` wohnt. Existiert eine solche `Person` in `personen` nicht, wird eine `IllegalArgumentException` mit der Nachricht `Keine Person aus <ort> gefunden.` geworfen, wobei `<ort>` durch den Ort ersetzt wird, nach dem gesucht wurde. 

	    --> *Tests schreiben Sie (siehe 12.)*

	11. Rufen Sie die `getPersonAusOrt(Set<Person> personen, String ort)` in der `main`-Methode auf. Es wird entweder die zurückgegebene Person ausgegeben (Zufallswert):

	    ```bash
	    Elif     Kaya      aus Dresden   ist 16 Jahre alt.
	    ```

	    oder die Nachricht aus der `IllegalArgumentException` (Zufallswert):

	    ```bash
	    Keine Person aus Aachen gefunden.
	    ```

	12. Erstellen Sie in der Klasse `Probeklausur2Test` zwei Tests für die Methode `getPersonAusOrt(Set<Person> personen, String ort)`. 

	    - Der erste Test soll prüfen, ob ein `Student`-Objekt korrekt aus einer gegebenen Menge für einen Ort ausgelesen wird, wenn ein passendes `Student`-Objekt existiert. 
	    - Der zweite Test soll prüfen, ob eine Exception geworfen wird, wenn ein solches Objekt nicht existiert. Außerdem soll für diesen Fall auch die Korrektheit der Exception-Message geprüft werden. 

	13. Implementieren Sie die Methode `getPersonMitAlter(Set<Person> personen, int alter)`. Diese Methode gibt ein `Optional` zurück. Dieses Optional enthält die (erste) `Person` aus der Menge `personen` mit dem Alter `alter`. Existiert eine solche `Person` in `personen` nicht, wird ein leeres `Optional` zurückgegeben. 

	    --> siehe `testGetPersonMitAlter()` in `Probeklausur2Test` (Anzeige `getPersonMitAlter()`)

	14. Rufen Sie die `getPersonMitAlter(Set<Person> personen, int alter)` in der `main`-Methode auf. Es wird entweder die im `Optional` enthaltene Person ausgegeben (Zufallswert):

	    ```bash
	    Elif     Kaya      aus Dresden   ist 16 Jahre alt.
	    ```

	    oder eine Nachricht der Form `Keine Person mit Alter <alter> gefunden.`, wobei `<alter>` durch das Alter ersetzt wird, nach dem gesucht wurde.

	15. Gegeben ist folgender Stream aus 20 `Person`-Objekten:

	    ```bash
	    Stream<Person> stream1 = Stream.generate(() -> createPerson()).limit(20);
	    ```

	    Speichern Sie diesen Stream in eine `Map`. Die Schlüssel der `Map` sind die Anfangsbuchstaben (als `Character`) der Nachnamen der jeweiligen `Person`-Objekte. Die Werte der `Map` sind Listen der Personen, deren Nachname mit dem jeweiligen Buchstaben beginnt. 

	16. Geben Sie die oben erzeugte `Map` wie folgt aus (Zufallswerte!):

	    ```bash
	    Anfangsbuchstabe A
	    Fatma    Al-Haddad aus Dortmund  ist 61 Jahre alt.
	    Salma    Arslan    aus Potsdam   ist 88 Jahre alt.
	    Layla    Al-Haddad aus Berlin    ist 16 Jahre alt.
	    Mia      Aydın     aus Dresden   ist 29 Jahre alt.
	    Anna     Aydın     aus Potsdam   ist 41 Jahre alt.
	    Mia      Al-Haddad aus Leipzig   ist 28 Jahre alt.

	    Anfangsbuchstabe F
	    Fatma    Fischer   aus Essen     ist 74 Jahre alt.
	    Emma     Fischer   aus Dresden   ist 67 Jahre alt.

	    Anfangsbuchstabe I
	    Emma     Ibrahim   aus Berlin    ist 41 Jahre alt.

	    Anfangsbuchstabe K
	    Noor     Kaya      aus Stuttgart ist 19 Jahre alt.
	    Anna     Khalil    aus Dresden   ist 63 Jahre alt.

	    Anfangsbuchstabe M
	    Fatma    Mansour   aus Magdeburg ist 63 Jahre alt.
	    Mariam   Mansour   aus Hamburg   ist 69 Jahre alt.

	    Anfangsbuchstabe P
	    Zeynep   Polat     aus Magdeburg ist 76 Jahre alt.

	    Anfangsbuchstabe S
	    Anna     Schneider aus Essen     ist 83 Jahre alt.
	    Sophie   Schmidt   aus Hamburg   ist 15 Jahre alt.
	    Fatma    Schneider aus Bremen    ist 13 Jahre alt.

	    Anfangsbuchstabe W
	    Hannah   Weber     aus Magdeburg ist 69 Jahre alt.
	    Sophie   Wagner    aus Dortmund  ist 11 Jahre alt.
	    Anna     Weber     aus Magdeburg ist 17 Jahre alt.
	    ``` 

	    - **Achtung**: Achten Sie darauf, dass die Ausgabe in sortierter Reihenfolge der Anfangsbuchstaben erfolgt.
	    - **Tip**: Speichern Sie die Menge der Schlüssel der Map in einer sortierten Liste und durchlaufen Sie dann die Liste.

	17. Passen Sie die Ausgabe der Map so an, dass die jeweiligen Wertelisten in "natürlicher Ordnung" (Nachname + Vorname) sortiert sind:

	    ```bash
	    Anfangsbuchstabe A
	    Anna     Al-Haddad aus Magdeburg ist 69 Jahre alt.
	    Derya    Al-Haddad aus Leipzig   ist 37 Jahre alt.
	    Mia      Al-Mufti  aus Hamburg   ist 45 Jahre alt.
	    Salma    Al-Mufti  aus Hamburg   ist 30 Jahre alt.
	    Salma    Al-Mufti  aus Leipzig   ist 90 Jahre alt.
	    Derya    Arslan    aus Potsdam   ist 83 Jahre alt.
	    Zeynep   Aydın     aus Dresden   ist 54 Jahre alt.

	    Anfangsbuchstabe B
	    Hannah   Becker    aus Dortmund  ist 96 Jahre alt.

	    Anfangsbuchstabe D
	    Aisha    Demir     aus Stuttgart ist 19 Jahre alt.
	    Elif     Demir     aus Bremen    ist 30 Jahre alt.

	    Anfangsbuchstabe F
	    Hannah   Fischer   aus Dortmund  ist 36 Jahre alt.
	    Salma    Fischer   aus Bremen    ist 44 Jahre alt.

	    Anfangsbuchstabe I
	    Aylin    Ibrahim   aus Berlin    ist 53 Jahre alt.

	    Anfangsbuchstabe K
	    Anna     Kaya      aus Potsdam   ist 82 Jahre alt.

	    Anfangsbuchstabe M
	    Noor     Mansour   aus Essen     ist 22 Jahre alt.

	    Anfangsbuchstabe P
	    Elif     Polat     aus Dresden   ist 51 Jahre alt.

	    Anfangsbuchstabe W
	    Aisha    Wagner    aus Hamburg   ist 25 Jahre alt.
	    Aisha    Weber     aus Stuttgart ist 10 Jahre alt.
	    Mia      Weber     aus Dortmund  ist 36 Jahre alt.

	    Anfangsbuchstabe Y
	    Sophie   Yilmaz    aus Potsdam   ist 53 Jahre alt.
	    ```

	### Punkte

	|<div style="min-width: 10em; width: 20em; max-width: 30em;">Aufgabe</div> |<div style="min-width: 10em; width: 25em; max-width: 30em;">Punkte</div> |
	|--------------|:-------------:|
	| 3. `createSetAelterAls()` | 3 Punkte | 
	| 4. Ausgabe | 2 Punkte | 
	| 5. `createMapOrtPersonen()` | 6 Punkte | 
	| 6. Ausgabe | 4 Punkte | 
	| 7. `Comparable` | 3 Punkte | 
	| 8. Sortieren und Ausgabe | 2 Punkte | 
	| 9. Sortieren und Ausgabe | 2 Punkte | 
	| 10. `getPersonAusOrt()` | 4 Punkte | 
	| 11. Aufruf und Ausgabe | 3 Punkte | 
	| 12. 2 JUnit-Tests | 6 Punkte | 
	| 13. `getPersonMitAlter()` | 3 Punkte | 
	| 14. Aufruf und Ausgabe | 3 Punkte | 
	| 15. Map Anfangsbuchstabe | 2 Punkte | 
	| 16. Ausgabe sortiert | 4 Punkte |
	| 17. Werte sortiert | 2 Punkte | 
	| korrektes Programm | 4 Punkte | 
	| <b>gesamt</b> | <b>53 Punkte</b>  |

	---



??? success "mögliche Lösung für Probeklausur2"
	
	=== "Probeklausur2.java"
		```java
		package probeklausuren.probeklausur2;

		import java.util.*;
		import java.util.stream.Collectors;
		import java.util.stream.Stream;

		public class Probeklausur2
		{
		    static Random r = new Random();

		    private static Person createPerson()
		    {
		        String[] vornamen = { "Sophie", "Hannah", "Emma", "Mia", "Anna", "Elif",
		                "Zeynep", "Fatma", "Aylin", "Derya", "Layla", "Aisha", "Noor",
		                "Salma", "Mariam" };
		        String[] nachnamen = { "Schmidt", "Schneider", "Fischer", "Weber",
		                "Wagner", "Becker", "Yilmaz", "Kaya", "Demir", "Polat",
		                "Aydın", "Arslan", "Al-Haddad", "Al-Mufti", "Ibrahim", "Khalil",
		                "Mansour" };
		        String[] orte = { "Berlin", "Hamburg", "Potsdam", "Dresden", "Magdeburg",
		                "Stuttgart", "Leipzig", "Dortmund", "Essen", "Bremen"
		        };
		        String vorname = vornamen[r.nextInt(vornamen.length)];
		        String nachname = nachnamen[r.nextInt(nachnamen.length)];
		        String ort = orte[r.nextInt(orte.length)];
		        int alter = r.nextInt(10, 100);
		        return new Person(vorname, nachname, alter, ort);
		    }

		    private static Set<Person> createSetOfPersonen(int numberOfPersonen)
		    {
		        Set<Person> personen = new HashSet<>();
		        for(int i = 0; i < numberOfPersonen; i++)
		        {
		            personen.add(createPerson());
		        }
		        return personen;
		    }

		    public static Set<Person> createSetAelterAls(int alter, Set<Person> personen1, Set<Person> personen2)
		    {
		        Set<Person> personen = new HashSet<>();
		        for(Person person : personen1)
		        {
		            if(person.alter() > alter) personen.add(person);
		        }
		        for(Person person : personen2)
		        {
		            if(person.alter() > alter) personen.add(person);
		        }
		        return personen;
		    }

		    public static Map<String, Set<Person>> createMapOrtPersonen(Set<Person> personen1, Set<Person> personen2)
		    {
		        Map<String, Set<Person>> mapOrtPersonen = new HashMap<>();
		        Set<Person> personen = new HashSet<>(personen1);
		        personen.addAll(personen2);
		        for(Person person : personen)
		        {
		            String key = person.ort();
		            if(mapOrtPersonen.containsKey(key))
		            {
		                mapOrtPersonen.get(key).add(person);
		            }
		            else
		            {
		                Set<Person> personenSet = new HashSet<>();
		                personenSet.add(person);
		                mapOrtPersonen.put(key, personenSet);
		            }
		        }
		        return mapOrtPersonen;
		    }

		    public static Person getPersonAusOrt(Set<Person> personen, String ort) throws IllegalArgumentException
		    {
		        for(Person person : personen)
		        {
		            if(person.ort().equals(ort)) return person;
		        }
		        throw new IllegalArgumentException("Keine Person aus " + ort + " gefunden.");
		    }

		    public static Optional<Person> getPersonMitAlter(Set<Person> personen, int alter)
		    {
		        for(Person person : personen)
		        {
		            if(person.alter() == alter) return Optional.of(person);
		        }
		        return Optional.empty();
		    }

		    public static void main(String[] args)
		    {
		        Set<Person> personen1 = createSetOfPersonen(10);
		        Set<Person> personen2 = createSetOfPersonen(10);
		        System.out.printf("%n%n--------------- personen1 set---------------------%n%n");
		        personen1.forEach(System.out::println);
		        System.out.printf("%n%n--------------- personen2 set---------------------%n%n");
		        personen2.forEach(System.out::println);

		        System.out.printf("%n%n--------------- createSetAelterAls(alter, personen1, personen2) ---------------------%n%n");
		        int alter = r.nextInt(10, 100);
		        System.out.println("alle Personen aelter als " + alter + ": ");
		        //TODO
		        // Aufruf von createSetAelterAls(alter, personen1, personen2);
		        // Ausgabe der zurueckgegebenen Set
		        Set<Person> aelterAls = createSetAelterAls(alter, personen1, personen2);
		        aelterAls.forEach(System.out::println);

		        System.out.printf("%n%n--------------- createMapOrtPersonen(personen1, personen2) ---------------------%n%n");
		        //TODO
		        // Aufruf von createMapOrtPersonen(personen1, personen2);
		        // Ausgabe der zurueckgegebenen Map
		        Map<String, Set<Person>> mapOrtPersonen = createMapOrtPersonen(personen1, personen2);
		        mapOrtPersonen.forEach((k,v) -> {
		            System.out.println("aus " + k + " kommen : ");
		            v.forEach(p -> System.out.println(" " + p.vorname() + " " + p.nachname()));
		            System.out.println();
		        });

		        System.out.printf("%n%n--------------- sortieren von personen1 - compareTo ---------------------%n%n");
		        List<Person> sortiert1 = personen1.stream().sorted().collect(Collectors.toList());
		        sortiert1.forEach(System.out::println);

		        System.out.printf("%n%n--------------- sortieren von personen2 - nach Alter ---------------------%n%n");
		        List<Person> sortiert2 = personen2.stream().sorted(Comparator.comparingInt(p -> p.alter())).collect(Collectors.toList());
		        sortiert2.forEach(System.out::println);

		        System.out.printf("%n%n--------------- getPersonAusOrt(Set<Person> personen, String ort) ---------------------%n%n");
		        try {
		            Person personAusOrt = getPersonAusOrt(personen1, "Aachen");
		            System.out.println(personAusOrt.toString());
		        } catch (IllegalArgumentException e) {
		            System.out.println(e.getMessage());
		        }

		        System.out.printf("%n%n--------------- getPersonMitAlter(Set<Person> personen, int alter) ---------------------%n%n");
		        for(int alter1 = 20; alter1 < 30; alter1++) {
		            Optional<Person> personMitAlter = getPersonMitAlter(personen2, alter1);
		            if (personMitAlter.isPresent()) {
		                System.out.println(personMitAlter.get().toString());
		            }
		            else {
		                System.out.println("Keine Person mit Alter " + alter1 + " gefunden.");
		            }
		        }

		        System.out.printf("%n%n--------------- stream ---------------------%n%n");
		        Stream<Person> stream1 = Stream.generate(() -> createPerson()).limit(20);
		        Map<Character, List<Person>> startsWithCharMap = stream1
		                .collect(Collectors.groupingBy(p -> p.nachname().charAt(0)));
		        List<Character> sortedKeyList = startsWithCharMap.keySet().stream()
		                .sorted().collect(Collectors.toList());
		        for(Character key : sortedKeyList)
		        {
		            System.out.println("Anfangsbuchstabe " + key);
		            List<Person> sortedValue = startsWithCharMap.get(key);
		            sortedValue.sort(Comparator.naturalOrder()); // Aufgabe 17
		            for(Person person : sortedValue)
		            {
		                System.out.println(person.toString());
		            }
		            System.out.println();
		        }

		    }

		}
		```
	
	=== "Probeklausur2Test.java"
		```java
		package probeklausuren.probeklausur2;

		import org.junit.jupiter.api.BeforeAll;
		import org.junit.jupiter.api.DisplayName;
		import org.junit.jupiter.api.Test;

		import java.util.*;
		import java.util.stream.Collectors;

		import static org.junit.jupiter.api.Assertions.*;

		public class Probeklausur2Test
		{
		    static Person p1, p2, p3, p4, p5, p6, p7, p8, p9, p10,
		            p11, p12, p13, p14, p15, p16, p17, p18, p19, p20;
		    static Set<Person> persons1,  persons2;

		    @BeforeAll
		    public static void setUp()
		    {
		        p1 = new Person("Zeynep", "Al-Haddad", 75, "Stuttgart");
		        p2 = new Person("Mia", "Wagner", 93, "Berlin");
		        p3 = new Person("Mariam", "Yilmaz", 33, "Berlin");
		        p4 = new Person("Zeynep", "Becker", 12, "Bremen");
		        p5 = new Person("Fatma", "Becker", 27, "Magdeburg");
		        p6 = new Person("Layla", "Aydın", 10, "Essen");
		        p7 = new Person("Emma", "Al-Haddad", 83, "Hamburg");
		        p8 = new Person("Mia", "Al-Mufti", 27, "Hamburg");
		        p9 = new Person("Anna", "Schmidt", 45, "Potsdam");
		        p10 = new Person("Elif", "Al-Mufti", 92, "Magdeburg");
		        p11 = new Person("Anna", "Ibrahim", 61, "Bremen");
		        p12 = new Person("Aisha", "Wagner", 78, "Potsdam");
		        p13 = new Person("Elif", "Fischer", 42, "Dortmund");
		        p14 = new Person("Emma", "Becker", 15, "Potsdam");
		        p15 = new Person("Aylin", "Khalil", 72, "Bremen");
		        p16 = new Person("Elif", "Ibrahim", 82, "Berlin");
		        p17 = new Person("Elif", "Fischer", 12, "Leipzig");
		        p18 = new Person("Noor", "Al-Mufti", 62, "Berlin");
		        p19 = new Person("Mariam", "Becker", 48, "Dresden");
		        p20 = new Person("Noor", "Schneider", 98, "Leipzig");

		        persons1 = Set.of(p1, p2, p3, p4, p5, p6, p7, p8, p9, p10);
		        persons2 = Set.of(p11, p12, p13, p14, p15, p16, p17, p18, p19, p20);
		    }

		    private boolean checkTowSetsSameElements(Set<Person> set1, Set<Person> set2)
		    {
		        if(set1.size() != set2.size()) return false;
		        for(Person p : set1) if(!set2.contains(p)) return false;
		        for(Person p : set2) if(!set1.contains(p)) return false;
		        return true;
		    }

		    private Comparator<Person> helpSort()
		    {
		        return (o1, o2) -> (o1.nachname().compareTo(o2.nachname()) == 0) ?
		                o1.vorname().compareTo(o2.vorname()) :
		                o1.nachname().compareTo(o2.nachname());
		    }

		    @Test
		    @DisplayName("createSetAelterAls()")
		    public void testCreateSetAelterAls()
		    {
		        // given persons1 and persons2
		        int alter = 50;

		        // when
		        Set<Person> aelterAls50 = Probeklausur2.createSetAelterAls(alter, persons1, persons2);
		        List<Person> aelterAls50Sorted = aelterAls50.stream().sorted().collect(Collectors.toList());
		        Set<Person> expected = Set.of(p1, p2, p7, p10, p11, p12, p15, p16, p18, p20);
		        List<Person> expectedSorted = expected.stream().sorted().collect(Collectors.toList());

		        // then
		        assertEquals(expectedSorted, aelterAls50Sorted, "createSetAelterAls() doesn't seem to work properly yet");
		    }

		    @Test
		    @DisplayName("createMapOrtPersonen()")
		    public void testCreateMapOrtPersonen()
		    {
		        // given persons1 and persons2

		        // when
		        Map<String, Set<Person>> mapOrte = Probeklausur2.createMapOrtPersonen(persons1, persons2);
		        Set<String> orteSet = mapOrte.keySet();
		        List<String> orteSetSorted = orteSet.stream().sorted().collect(Collectors.toList());

		        Collection<Set<Person>> valuesColl = mapOrte.values();
		        List<List<Person>> valuesLists = new ArrayList<>();
		        for(Set<Person> set : valuesColl)
		        {
		            valuesLists.add(set.stream().collect(Collectors.toList()));
		        }
		        List<Person> valuesListSorted = valuesLists.stream()
		                .flatMap( l -> l.stream().sorted( helpSort()) )
		                .sorted( (o1, o2) -> o1.ort().compareTo(o2.ort()) )
		                .collect(Collectors.toList());

		        Set<String> orteExpected = Set.of("Stuttgart", "Berlin", "Bremen", "Magdeburg",
		                        "Essen", "Hamburg", "Potsdam", "Dortmund", "Leipzig", "Dresden");
		        List<String> orteExpectedSorted = orteSetSorted.stream().sorted().collect(Collectors.toList());
		        List<Person> stuttgart = List.of(p1);
		        List<Person> berlin = List.of(p2, p3, p16, p18);
		        List<Person> bremen = List.of(p4, p11, p15);
		        List<Person> magdeburg = List.of(p5, p10);
		        List<Person> essen = List.of(p6);
		        List<Person> hamburg = List.of(p7, p8);
		        List<Person> potsdam = List.of(p9, p12, p14);
		        List<Person> dortmund = List.of(p13);
		        List<Person> dresden = List.of(p19);
		        List<Person> leipzig = List.of(p17, p20);
		        List<List<Person>> expectedSets = List.of(stuttgart, berlin, bremen, magdeburg, essen, hamburg, potsdam,
		                dortmund, dresden, leipzig);
		        List<Person> expectedSetsSorted = expectedSets.stream()
		                .flatMap( l -> l.stream().sorted( helpSort()) )
		                .sorted( (o1, o2) -> o1.ort().compareTo(o2.ort()) )
		                .collect(Collectors.toList());

		        // then
		        assertTrue(mapOrte instanceof Map<String, Set<Person>>, "createMapOrtPersonen() doesn't seem to work properly yet (wrong return type)");
		        assertEquals(orteExpectedSorted, orteSetSorted, "createMapOrtPersonen() doesn't seem to work properly yet (wrong key set)");
		        assertEquals(expectedSetsSorted, valuesListSorted, "createMapOrtPersonen() doesn't seem to work properly yet (wrong value collection)");
		    }

		    @Test
		    @DisplayName("Person is Comparable")
		    public void testPersonIsComparable() {
		        // given
		        Set<Person> unsorted = Set.of(p1, p4, p5, p14, p19);
		        List<Person> expected = List.of(p1, p14, p5, p19, p4);

		        assertTrue(p1 instanceof Comparable, "Person is not Comparable yet");
		        if(p1 instanceof Comparable) {

		            // when
		            List<Person> sorted = unsorted.stream().sorted().collect(Collectors.toList());

		            // then
		            assertEquals(expected, sorted, "compareTo of Person not working properly yet ");
		        }
		    }

		    @Test
		    @DisplayName("getPersonMitAlter()")
		    public void testGetPersonMitAlter()
		    {
		        int alter = 42;
		        Optional<Person> result1 = Probeklausur2.getPersonMitAlter(persons1, alter);
		        Optional<Person> result2 = Probeklausur2.getPersonMitAlter(persons2, alter);
		        assertTrue(result1.isEmpty(),"getPersonMitAlter() doesn't seem to work properly yet");
		        assertEquals(result2.get(), p13, "getPersonMitAlter() doesn't seem to work properly yet");
		    }

		    /*
		     * Schreiben Sie hinter diesem Kommentar Ihre beiden Testfaelle fuer 12.
		     */

		    @Test
		    @DisplayName("getPersonAusOrt() - Student")
		    public void testGetPersonAusOrt()
		    {
		        Person result = Probeklausur2.getPersonAusOrt(persons1, "Essen");
		        assertEquals(p6, result, "getPersonAusOrt(persons1, Essen)");
		    }

		    @Test
		    @DisplayName("getPersonAusOrt() - Exception")
		    public void testGetPersonAusOrtException()
		    {
		        Exception e = assertThrows(IllegalArgumentException.class, () -> Probeklausur2.getPersonAusOrt(persons1, "Leipzig"));
		        assertEquals("Keine Person aus Leipzig gefunden.", e.getMessage(), "getPersonAusOrt(persons1, Leipzig)");
		    }
		}
		```
	
	=== "Person.java"
		```java
		package probeklausuren.probeklausur2;

		public record Person(String vorname, String nachname, int alter, String ort) implements Comparable<Person>
		{
		    @Override
		    public String toString()
		    {
		        return String.format("%-8s %-9s aus %-9s ist %2d Jahre alt.",
		                this.vorname, this.nachname, this.ort, this.alter);
		    }

		    @Override
		    public int compareTo(Person o)
		    {
		        if(this.nachname.compareTo(o.nachname) != 0) return this.nachname.compareTo(o.nachname);
		        else return this.vorname.compareTo(o.vorname);
		    }
		}
		```



