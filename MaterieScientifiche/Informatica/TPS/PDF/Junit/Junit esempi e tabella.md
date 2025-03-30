### Comandi e annotazioni JUnit

|**Azione**|**Annotazione/Metodo**|**Descrizione**|
|---|---|---|
|**🔹 Importare JUnit**|`import org.junit.jupiter.api.*;`|Importa le classi di JUnit 5.|
|**🔹 Dichiarare la classe di test**|`@Test`|Indica che il metodo è un test.|
|**🔹 Setup iniziale (eseguito una sola volta prima di tutti i test)**|`@BeforeAll`|Metodo statico eseguito una volta prima di tutti i test.|
|**🔹 Setup prima di ogni test**|`@BeforeEach`|Eseguito prima di ogni test per inizializzare lo stato.|
|**🔹 Teardown dopo ogni test**|`@AfterEach`|Eseguito dopo ogni test per pulire lo stato.|
|**🔹 Teardown finale (eseguito una sola volta dopo tutti i test)**|`@AfterAll`|Metodo statico eseguito una volta dopo tutti i test.|
|**🔹 Testare l'uguaglianza di valori**|`Assertions.assertEquals(expected, actual);`|Controlla se `expected == actual`.|
|**🔹 Testare se un valore è `true`**|`Assertions.assertTrue(condizione);`|Controlla se la condizione è vera.|
|**🔹 Testare se un valore è `false`**|`Assertions.assertFalse(condizione);`|Controlla se la condizione è falsa.|
|**🔹 Testare se un oggetto è `null`**|`Assertions.assertNull(obj);`|Controlla se l'oggetto è nullo.|
|**🔹 Testare se un oggetto NON è `null`**|`Assertions.assertNotNull(obj);`|Controlla se l'oggetto non è nullo.|
|**🔹 Testare se due oggetti sono la stessa istanza**|`Assertions.assertSame(expected, actual);`|Controlla se i due riferimenti puntano allo stesso oggetto.|
|**🔹 Testare se due oggetti NON sono la stessa istanza**|`Assertions.assertNotSame(expected, actual);`|Controlla se i due riferimenti puntano a oggetti diversi.|
|**🔹 Testare se un'eccezione viene lanciata**|`Assertions.assertThrows(NomeEccezione.class, () -> { ... });`|Verifica se viene lanciata un'eccezione specifica.|
|**🔹 Ignorare (saltare) un test**|`@Disabled`|Il test non verrà eseguito.|
|**🔹 Eseguire test con più valori (Test parametrico)**|`@ParameterizedTest``@ValueSource(ints = {1, 2, 3})`|Permette di eseguire il test con valori diversi.|

---

### **📌 Esempio di test con JUnit 5**

```java
import org.junit.jupiter.api.*;

import static org.junit.jupiter.api.Assertions.*;

class CalcolatriceTest {
    
    private Calcolatrice calcolatrice;

    @BeforeAll
    static void setupOnce() {
        System.out.println("Setup globale (eseguito una sola volta)");
    }

    @BeforeEach
    void setup() {
        calcolatrice = new Calcolatrice();
        System.out.println("Inizializzazione prima di ogni test");
    }

    @Test
    void testSomma() {
        int risultato = calcolatrice.somma(2, 3);
        assertEquals(5, risultato, "La somma di 2 e 3 deve essere 5");
    }

    @Test
    void testDivisione() {
        assertThrows(ArithmeticException.class, () -> calcolatrice.dividi(10, 0), "Deve lanciare un'eccezione se si divide per zero");
    }

    @AfterEach
    void teardown() {
        System.out.println("Pulizia dopo ogni test");
    }

    @AfterAll
    static void teardownOnce() {
        System.out.println("Pulizia finale (eseguita una sola volta)");
    }
}

// Classe da testare
class Calcolatrice {
    int somma(int a, int b) {
        return a + b;
    }

    int dividi(int a, int b) {
        return a / b;
    }
}
```
