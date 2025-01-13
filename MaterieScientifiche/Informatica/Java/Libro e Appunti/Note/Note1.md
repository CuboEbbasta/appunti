> [!PDF|yellow] [[JavaIO.pdf#page=3&selection=8,0,21,9&color=yellow|JavaIO, p.3]]
> > Uno stream (in italiano flusso) è un canale di comunicazione attraverso cui passano dati in una sola direzione
> 


# Java I/O and Object Serialization

Java's Input/Output (I/O) framework provides a comprehensive system for handling data streams. A **stream** is essentially a conduit through which data flows in one direction, facilitating the reading or writing of data.

## Streams Overview

### InputStream Class

- **Role**: Serves as the ancestor for input byte streams.
- **Nature**: Abstract class with minimal method definitions.
- **Key Methods**:
  - `public abstract int read() throws IOException`: Reads a single byte from the stream. This method must be implemented by concrete subclasses to specify how bytes are read.
  - `public int available() throws IOException`: Returns an estimate of the number of bytes that can be read without blocking, defaulting to 0 if unimplemented.
  - `public void close() throws IOException`: Closes the stream and releases any system resources associated with it.

### OutputStream Class

- **Role**: Acts as the precursor for output byte streams.
- **Nature**: Abstract class providing a foundational structure.
- **Key Methods**:
  - `public abstract void write(int b) throws IOException`: Writes a single byte to the stream, requiring concrete implementation in subclasses.
  - `public void flush() throws IOException`: Flushes any buffered output bytes to the stream.
  - `public void close() throws IOException`: Closes the stream and releases resources.

## Object Serialization

Serialization is the process of converting an object into a byte stream, enabling it to be easily saved or transmitted. Java's serialization mechanism involves:

- **Serializable Interface**: Classes that implement this interface can be serialized. The Java compiler enforces its implementation for serializable classes.
  
- **Data Handling**:
  - All non-static and non-transient fields of an object are serialized, including inherited private and protected fields.
  - Transient variables are omitted from serialization.

- **Recursive Serialization**: If an object contains references to other objects, `writeObject()` is recursively called on each reference. This results in the serialization of a complete graph of objects.
  
- **Handling Duplicate References**: To prevent infinite recursion, if multiple references point to the same object within the graph, it is serialized only once.

### Example: Serializable Class

```java
public class PuntoCartesiano implements java.io.Serializable {
    private int x;
    private int y;

    public PuntoCartesiano(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public PuntoCartesiano() { 
        x = y = 0; 
    }

    public float getAscissa() { return x; }
    public float getOrdinata() { return y; }
}
```

### Writing to a File

```java
import java.io.*;

public class ScriviPunto {
    public static void scriviPunto(String filename) throws IOException {
        PuntoCartesiano point = new PuntoCartesiano(3, 10);
        try (FileOutputStream fos = new FileOutputStream(filename);
             ObjectOutputStream oos = new ObjectOutputStream(fos)) {
            oos.writeObject(point);
            oos.flush();
        }
    }

    public static void main(String[] args) {
        try {
            scriviPunto("punto.dat");
        } catch (IOException e) {
            System.out.println("Errore di I/O.");
            System.exit(1);
        }
    }
}
```

### Reading from a File

```java
import java.io.*;

public class LeggiPunto {
    public static void leggiPunto(String filename) throws IOException, ClassNotFoundException {
        try (FileInputStream fis = new FileInputStream(filename);
             ObjectInputStream ois = new ObjectInputStream(fis)) {
            PuntoCartesiano point = (PuntoCartesiano) ois.readObject();
            System.out.println("Ascissa: " + point.getAscissa() + ", Ordinata: " + point.getOrdinata());
        }
    }

    public static void main(String[] args) {
        try {
            leggiPunto("punto.dat");
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Errore di I/O o di classe non trovata.");
            System.exit(1);
        }
    }
}
```

## File Class

The `File` class in Java provides methods to interact with file systems, offering functionalities such as:

- **Constructors**:
  - `public File(String path)`: Creates a new `File` instance by converting the given pathname string into an abstract pathname.

- **Useful Methods**:
  - `public String getName()`: Retrieves the name of the file or directory.
  - `public String getAbsolutePath()`: Returns the absolute pathname string.
  - `public boolean exists()`: Checks if the file or directory denoted by this abstract pathname exists.
  - `public boolean isDirectory()`: Determines whether the file object represents a directory.
  - `public long length()`: Provides the size of the file in bytes.
  - `public boolean renameTo(File dest)`: Renames the file to the specified pathname.
  - `public boolean delete()`: Deletes the file or directory denoted by this abstract pathname.
  - `public boolean mkdir()`: Creates a new directory named by this abstract pathname.
  - `public String[] list()`: Returns an array of strings naming the files and directories in the directory.

This comprehensive overview illustrates how Java's I/O system and serialization capabilities enable efficient data management, allowing developers to seamlessly save, transmit, and manipulate object states across different environments.
