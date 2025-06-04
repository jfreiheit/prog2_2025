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


??? success "mögliche Lösung für Übung 9"
	
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
		


##### Übung 11 (JUnit)

??? "Übung 11 (JUnit)"
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
	
