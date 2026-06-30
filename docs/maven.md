# Apache Maven

- Das **Problem**: Wie haben wir bisher externe Bibliotheken hinzugefügt? (Manuelles Herunterladen von .jar-Dateien, Hinzufügen zum Klassenpfad in der IDE).
- Die **Nachteile**: Versionskonflikte ("JAR-Hölle"), mangelnde Portabilität (Projekt baut auf Rechner A, aber nicht auf Rechner B), fehlende Automatisierung für Tests.
- Die **Lösung**: Ein Build-Management-Tool wie Maven (oder Gradle). Es standardisiert die Projektstruktur und automatisiert das Herunterladen von Abhängigkeiten.

## Kernkonzepte von Maven

1. Convention over Configuration: Maven gibt eine feste Ordnerstruktur vor. Wenn man sich daran hält, muss man fast nichts konfigurieren.

	- `src/main/java` -> Anwendungscode
	- `src/test/java` -> Testcode (JUnit)

2. Die `pom.xml` (Project Object Model): Das Herzstück.

	- *Koordinaten* : `groupId`, `artifactId`, `version` (Das "GAV"-Prinzip zur eindeutigen Identifizierung).
	- *Dependencies* : Deklaration von externen Bibliotheken.

3. Repositories: 

	- *Local Repository*: Lokaler Cache ( z.B. auf dem Mac `~/.m2/repository`).
	- *Central Repository*: Das globale Online-Archiv, von dem Maven alles lädt.

4. Der Build-Lifecycle: Phasen, die sequentiell durchlaufen werden:

	- `validate` -> `compile` -> `test` -> `package` -> `verify` -> `install` -> `deploy`
	- Wichtig: Wenn ich `mvn test` aufrufe, wird vorher automatisch `compile` ausgeführt.


## Beispiel

1. Eclipse: `File` -> `New` -> `New Maven Project` (Häkchen bei `Create a simple project (skip archetype selection)`)
2. IntelliJ

