## **JUnit: Cos'è e come funziona**

JUnit è un framework per il testing unitario in Java. È usato per verificare il corretto funzionamento del codice, scrivendo test automatizzati che eseguono unità di codice in modo indipendente.

---

## **Come usare JUnit**

### **1. Installazione**

JUnit è incluso in molte IDE come IntelliJ IDEA ed Eclipse, ma puoi anche aggiungerlo manualmente al progetto **Maven** o **Gradle**.

- **Con Maven** (nel file `pom.xml`):
    
    ```xml
    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.8.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    ```
    
- **Con Gradle** (nel file `build.gradle`):
    
    ```gradle
    dependencies {
        testImplementation 'org.junit.jupiter:junit-jupiter:5.8.1'
    }
    ```
    

---

## **2. Creazione di un Test con JUnit**

Un test in JUnit è una classe che contiene metodi annotati con `@Test`. Vediamo un esempio:

### **Classe da testare (`Calcolatrice.java`)**

```java
public class Calcolatrice {
    public int somma(int a, int b) {
        return a + b;
    }

    public int divisione(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Divisione per zero!");
        }
        return a / b;
    }
}
```

### **Classe di test (`CalcolatriceTest.java`)**

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

class CalcolatriceTest {

    @Test
    void testSomma() {
        Calcolatrice calc = new Calcolatrice();
        assertEquals(5, calc.somma(2, 3));  // Controlla se 2+3 è uguale a 5
    }

    @Test
    void testDivisione() {
        Calcolatrice calc = new Calcolatrice();
        assertEquals(2, calc.divisione(6, 3));  // Controlla se 6/3 è uguale a 2
    }

    @Test
    void testDivisionePerZero() {
        Calcolatrice calc = new Calcolatrice();
        assertThrows(IllegalArgumentException.class, () -> calc.divisione(5, 0));
    }
}
```

---

## **3. Metodi di asserzione principali (`Assertions`)**

JUnit fornisce diversi metodi per verificare i risultati:

|Metodo|Descrizione|
|---|---|
|`assertEquals(a, b)`|Verifica se `a` è uguale a `b`|
|`assertNotEquals(a, b)`|Verifica se `a` è diverso da `b`|
|`assertTrue(condizione)`|Verifica se `condizione` è vera|
|`assertFalse(condizione)`|Verifica se `condizione` è falsa|
|`assertNull(obj)`|Verifica se `obj` è `null`|
|`assertNotNull(obj)`|Verifica se `obj` NON è `null`|
|`assertThrows(Exception.class, lambda)`|Verifica se il codice lancia un'eccezione|

---

## **4. Annotazioni JUnit e Ciclo di Vita**

JUnit permette di eseguire codice prima e dopo i test grazie alle annotazioni.

|Annotazione|Descrizione|
|---|---|
|`@BeforeEach`|Eseguito prima di ogni test|
|`@AfterEach`|Eseguito dopo ogni test|
|`@BeforeAll`|Eseguito una sola volta prima di tutti i test (deve essere statico)|
|`@AfterAll`|Eseguito una sola volta dopo tutti i test (deve essere statico)|

Esempio:

```java
import org.junit.jupiter.api.*;

class EsempioTest {

    @BeforeAll
    static void setupGlobal() {
        System.out.println("Eseguito prima di tutti i test");
    }

    @BeforeEach
    void setup() {
        System.out.println("Eseguito prima di ogni test");
    }

    @Test
    void test1() {
        System.out.println("Eseguito test 1");
    }

    @Test
    void test2() {
        System.out.println("Eseguito test 2");
    }

    @AfterEach
    void teardown() {
        System.out.println("Eseguito dopo ogni test");
    }

    @AfterAll
    static void teardownGlobal() {
        System.out.println("Eseguito dopo tutti i test");
    }
}
```

**Output previsto:**

```
Eseguito prima di tutti i test
Eseguito prima di ogni test
Eseguito test 1
Eseguito dopo ogni test
Eseguito prima di ogni test
Eseguito test 2
Eseguito dopo ogni test
Eseguito dopo tutti i test
```

---

## **5. Testare Eccezioni**

Se vogliamo verificare che un metodo lanci un'eccezione, possiamo usare `assertThrows`:

```java
@Test
void testDivisionePerZero() {
    Calcolatrice calc = new Calcolatrice();
    assertThrows(IllegalArgumentException.class, () -> calc.divisione(5, 0));
}
```

---

## **6. Ignorare Test con `@Disabled`**

Se un test è ancora in fase di sviluppo o non deve essere eseguito, possiamo usare `@Disabled`:

```java
@Test
@Disabled("Da implementare in futuro")
void testDaFare() {
    // codice non ancora implementato
}
```

---

## **7. Testare Performance con `@Timeout`**

JUnit permette di verificare che un metodo non superi un certo tempo di esecuzione:

```java
import org.junit.jupiter.api.Timeout;
import java.util.concurrent.TimeUnit;

@Test
@Timeout(value = 2, unit = TimeUnit.SECONDS)
void testPerformance() throws InterruptedException {
    Thread.sleep(1000);  // Simula un'operazione lunga
}
```

---

## **Conclusione**

JUnit è uno strumento potente per testare il codice Java. I concetti fondamentali sono:

- Scrivere test con `@Test`
- Usare `Assertions` per verificare i risultati
- Utilizzare `@BeforeEach`, `@AfterEach`, `@BeforeAll`, `@AfterAll` per il setup e teardown
- Testare eccezioni con `assertThrows`
- Disabilitare test con `@Disabled`
- Impostare limiti di tempo con `@Timeout`
