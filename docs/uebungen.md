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

	5. Erstellen Sie in der `main()`-Methode eine `Map<Integer, Stadt> staedteMap = new HashMap<>();`. Fügen Sie der `staedteMap` einen fortlaufenden, eindeutigen `Integer`-Wert beginnend mit `1` als *Key* sowie alle alle Städte aus dem durch Aufruf der `staedte()`-Methode erzeugtem Array als *Value* hinzu.
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



##### Übung 8 (Interfaces)

??? "Übung 8"

	1. Wir beschäftigen uns nochmal mit der Übung 7, d.h. mit `Stadt` und `StadtTest`. Dieses Mal geht es uns aber mehr um die Verwendung des Interfaces `Comparable`. Zunächst sind die beiden Klassen `Stadt` und `StadtTest` wie folgt gegeben (das haben wir so in Übung 7 erarbeitet - es gibt eine Änderung in `StadtTest`, dort benutzen wir jetzt ): 

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

	- **Zusatz**: Schreiben Sie in `StadtTest.java` eine Methode `public static boolean contains(Map<MyInteger, Stadt> staedteMap, Stadt stadt)`, die ein `true` zurückgibt, wenn die Stadt `stadt` bereits in der `staedteMap` als ein `value` existiert. *Tipp*: Die Methode `get(Object key)` aus `Map` gibt den zu `key` gehörigen `value` zurück und mit `keySet()` bekommt man die Menge aller `keys` aus der `Map` ermittelt. Testen Sie die Methode, indem Sie zur Menge nur dann die `stadt` hinzufügen, wenn sie nicht bereits in der Menge aufgeführt ist. Sie sollten folgende Ausgabe erhalten: 

		```bash
		------------ Maps --------------
		5  Frankfurt/Main     248,31 km2      648.550     679.664     736.414
		4  Koeln              405,02 km2      962.884   1.007.119   1.075.935
		3  Muenchen           310,70 km2    1.210.223   1.353.186   1.464.301
		2  Hamburg            755,22 km2    1.715.392   1.786.448   1.810.438
		1  Berlin             891,68 km2    3.382.169   3.460.725   3.574.830
		```




##### Übung SWT (JUnit)

??? "Übung SWT (JUnit)"
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
	
