# JAVA

## Généralités

### Java 8 (LTS)

- Lambdas expressions
- streams (map, reduce)
- Référence de méthode => Faire référence à une méthode d'une interface fonctionnelle
- Interface optinnelle => Interface qui ne contient qu'une seule méthode abstraite
- Optional => Utilisé pour traiter les NPE, fournit des méthodes pour vérifier la présence d'une valeur

### Java 9 (Umbrella)

- Jigsaw pour rendre modulaire l'application et réduire la taille sur les env.
- Méthodes privées dans les interfaces
- try-with-resources
- API Flow

### Java 10 (Project Kona)

- Inférence de type => Utilisation de var afin de gagner en lisiblité

### Java 11 (LTS)

- Inférence de type pour les paramètres de lambdas => utilisation de var dans les lambdas
<details>
  <summary>Exemple</summary>
  
```java
import java.util.Arrays;
import java.util.List;
import java.util.function.BiConsumer;
import java.util.function.Consumer;
import java.util.function.Predicate;
import javax.validation.constraints.NotNull; // Exemple d'annotation

public class VarInLambdaExample {

    public static void main(String[] args) {

        // --- Exemple 1: Cas simple sans annotation ---
        // Avant Java 11, il fallait spécifier le type si on voulait une inférence forte
        // Consumer<String> printer = (String s) -> System.out.println(s.toUpperCase());
        // Avec 'var', le type est inféré
        Consumer<String> printer = (var s) -> System.out.println(s.toUpperCase());
        printer.accept("hello world");


        // --- Exemple 2: Utilisation de 'var' avec plusieurs paramètres ---
        // Le type des deux paramètres est inféré à partir de BiConsumer<String, Integer>
        BiConsumer<String, Integer> logger = (var message, var level) ->
            System.out.println("Log: " + message + " (Level: " + level + ")");
        logger.accept("Application started", 1);


        // --- Exemple 3: Le cas le plus utile - 'var' avec des annotations ---
        // Imaginez que @NotNull est une annotation de validation personnalisée
        // Avant Java 11, si vous vouliez annoter le paramètre, vous deviez spécifier le type :
        // Predicate<String> isNotNullAndNotEmptyOld = (@NotNull String s) -> s != null && !s.isEmpty();
        // Avec 'var', le type est inféré et vous pouvez toujours annoter :
        Predicate<String> isNotNullAndNotEmpty = (@NotNull var s) -> s != null && !s.isEmpty();

        System.out.println("Is 'hello' not null and not empty? " + isNotNullAndNotEmpty.test("hello"));
        System.out.println("Is '' not null and not empty? " + isNotNullAndNotEmpty.test(""));
        System.out.println("Is null not null and not empty? " + isNotNullAndNotEmpty.test(null)); // Peut lancer une exception si @NotNull est activement validée


        // --- Exemple 4: Itération avec 'var' dans un forEach (bien que ce ne soit pas une lambda directe) ---
        // Juste pour montrer la cohérence de 'var' dans les contextes où l'inférence de type est utilisée
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        names.forEach((var name) -> System.out.println("Name: " + name));
    }
}
```
</details>

- Nouveau client HTTP compatible avec la version 2 de HTTP
- Nouvelles méthodes pour la classe String
<details>
  <summary>Exemple</summary>
  
```java
  
"  ".isBlank();    // true
"".isBlank();     // true
"hello".isBlank(); // false
"  \t\n".isBlank(); // true


String multiLineText = "Ligne 1\nLigne 2\r\nLigne 3";
multiLineText.lines()
             .forEach(System.out::println);
// Output:
// Ligne 1
// Ligne 2
// Ligne 3

String s1 = "  Hello World  ";
System.out.println(s1.strip()); // "Hello World"

// Caractère d'espacement Unicode (non supprimé par trim())
String s2 = "\u2005 Hello \u2005"; // U+2005 est un espace "Four-per-em space"
System.out.println("Trimmed: '" + s2.trim() + "'");   // "Trimmed: ' Hello '"
System.out.println("Stripped: '" + s2.strip() + "'"); // "Stripped: 'Hello'"
```
</details>

- Exécution simplifiée de programme à fichier unique
- Nouvelles méthodes dans Files
<details>
  <summary>Cliquez ici pour voir l'exemple de code Java</summary>
  
```java

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class ReadFileToStringExample {

    public static void main(String[] args) {
        Path filePath = Paths.get("monFichier.txt");

        try {
            // Créer un fichier temporaire pour l'exemple
            Files.writeString(filePath, "Ceci est la première ligne.\n" +
                                       "Ceci est la deuxième ligne.");

            // Lire le contenu du fichier en tant que String (UTF-8 par défaut)
            String content = Files.readString(filePath);
            System.out.println("Contenu du fichier (UTF-8 par défaut):");
            System.out.println(content);

            // Lire le contenu du fichier avec un encodage spécifique (par exemple, ISO-8859-1)
            Path anotherFilePath = Paths.get("monFichierLatin1.txt");
            String latin1Content = "Caractères accentués: éàçü";
            Files.writeString(anotherFilePath, latin1Content, StandardCharsets.ISO_8859_1);

            String readLatin1Content = Files.readString(anotherFilePath, StandardCharsets.ISO_8859_1);
            System.out.println("\nContenu du fichier (ISO-8859-1):");
            System.out.println(readLatin1Content);

            // Supprimer les fichiers temporaires
            Files.delete(filePath);
            Files.delete(anotherFilePath);

        } catch (IOException e) {
            System.err.println("Erreur lors de la lecture du fichier: " + e.getMessage());
        }
    }
}
```
</details>

### Java 17 (LTS)

- Classes scellées (Sealed Classes) :
  -  Permet de contrôler quelle classe ou interface peuvent étendre ou implémenter une classe ou une interface donnée
  -  Améliore la sécurité du code, la maintenabilité

<details>
  <summary>Exemple 1</summary>
  
```java 

// Classe abstraite scellée représentant une forme
public sealed abstract class Shape permits Circle, Rectangle, Triangle {
    // Méthodes communes aux formes
    public abstract double area();
}

// Sous-classe finale : ne peut pas être étendue
public final class Circle extends Shape {
    private final double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

// Sous-classe non-scellée : peut être étendue par n'importe quelle classe
public non-sealed class Rectangle extends Shape {
    private final double width;
    private final double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

// Sous-classe scellée : elle-même restreint ses sous-types
public sealed class Triangle extends Shape permits EquilateralTriangle, IsoscelesTriangle {
    private final double base;
    private final double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return 0.5 * base * height;
    }
}

// Sous-classe finale du Triangle scellé
public final class EquilateralTriangle extends Triangle {
    // ... constructeur et méthodes spécifiques
    public EquilateralTriangle(double side) {
        super(side, side * Math.sqrt(3) / 2); // Calcul de la hauteur pour un triangle équilatéral
    }
}

// Une autre sous-classe finale du Triangle scellé
public final class IsoscelesTriangle extends Triangle {
    // ... constructeur et méthodes spécifiques
    public IsoscelesTriangle(double base, double height) {
        super(base, height);
    }
}

// Utilisation (par exemple, avec le Pattern Matching dans les switch, une fonctionnalité complémentaire)
public class ShapeProcessor {
    public static void processShape(Shape shape) {
        // Avec Java 17+, les classes scellées peuvent être utilisées avec le pattern matching for switch,
        // ce qui permet au compilateur de garantir l'exhaustivité des cas.
        String description = switch (shape) {
            case Circle c -> "Cercle de rayon " + c.radius;
            case Rectangle r -> "Rectangle de " + r.width + "x" + r.height;
            case Triangle t -> "Triangle de base " + t.base + " et hauteur " + t.height;
            // Pas besoin de 'default' si tous les types permis sont couverts et si le switch est exhaustif
        };
        System.out.println(description);
    }

    public static void main(String[] args) {
        processShape(new Circle(5));
        processShape(new Rectangle(4, 6));
        processShape(new EquilateralTriangle(7));
    }
}

```

</details>

<details>
  <summary>Exemple 2</summary>
  
```java

// Interface scellée pour un type de message dans un système
public sealed interface Message permits TextMessage, ImageMessage, ErrorMessage {
    String getSender();
}

// Implémentation finale
public final class TextMessage implements Message {
    private final String sender;
    private final String content;

    public TextMessage(String sender, String content) {
        this.sender = sender;
        this.content = content;
    }

    @Override
    public String getSender() { return sender; }
    public String getContent() { return content; }
}

// Implémentation non-scellée
public non-sealed class ImageMessage implements Message {
    private final String sender;
    private final byte[] imageData;

    public ImageMessage(String sender, byte[] imageData) {
        this.sender = sender;
        this.imageData = imageData;
    }

    @Override
    public String getSender() { return sender; }
    public byte[] getImageData() { return imageData; }
    // Cette classe peut être étendue par d'autres classes comme JpegImageMessage, PngImageMessage, etc.
}

// Implémentation finale
public final class ErrorMessage implements Message {
    private final String sender;
    private final String errorCode;

    public ErrorMessage(String sender, String errorCode) {
        this.sender = sender;
        this.errorCode = errorCode;
    }

    @Override
    public String getSender() { return sender; }
    public String getErrorCode() { return errorCode; }
}

public class MessageProcessor {
    public static void processMessage(Message message) {
        String info = switch (message) {
            case TextMessage tm -> "Texte de " + tm.getSender() + ": " + tm.getContent();
            case ImageMessage im -> "Image de " + im.getSender() + " (" + im.getImageData().length + " bytes)";
            case ErrorMessage em -> "Erreur de " + em.getSender() + " (Code: " + em.getErrorCode() + ")";
        };
        System.out.println(info);
    }

    public static void main(String[] args) {
        processMessage(new TextMessage("Alice", "Salut tout le monde !"));
        processMessage(new ErrorMessage("System", "CODE_001"));
    }
}

```

</details>

- Pattern Matching pour switch

<details>
  <summary>Exemple 1 : simple</summary>

```java

// Ancien style avec if-else if et instanceof
public String processLegacyObject(Object o) {
    if (o instanceof Integer) {
        Integer i = (Integer) o; // Cast nécessaire
        return "C'est un entier : " + i;
    } else if (o instanceof String) {
        String s = (String) o; // Cast nécessaire
        return "C'est une chaîne : " + s.toUpperCase();
    } else if (o instanceof Double) {
        Double d = (Double) o; // Cast nécessaire
        return "C'est un double : " + d * 2;
    } else {
        return "Type inconnu";
    }
}

public class NewSwitchExample {

    // Méthode avec Pattern Matching for switch (Java 17+)
    public String processObject(Object o) {
        return switch (o) {
            case Integer i -> "C'est un entier : " + i; // 'i' est automatiquement de type Integer
            case String s  -> "C'est une chaîne : " + s.toUpperCase(); // 's' est automatiquement de type String
            case Double d  -> "C'est un double : " + d * 2; // 'd' est automatiquement de type Double
            case null      -> "C'est null"; // Gestion explicite de null (Java 17+)
            default        -> "Type inconnu";
        };
    }

    public static void main(String[] args) {
        NewSwitchExample example = new NewSwitchExample();

        System.out.println(example.processObject(10));
        System.out.println(example.processObject("bonjour"));
        System.out.println(example.processObject(5.5));
        System.out.println(example.processObject(true)); // Type inconnu
        System.out.println(example.processObject(null)); // C'est null
    }
}

```

</details>

<details>
  <summary>Exemple 2 : avec des classes scellées</summary>

```java

// La classe scellée Shape (dupliquée ici pour un exemple autonome)
public sealed abstract class Shape permits Circle, Rectangle, Triangle {}

public final class Circle extends Shape {
    final double radius;
    public Circle(double radius) { this.radius = radius; }
    public double area() { return Math.PI * radius * radius; }
}

public non-sealed class Rectangle extends Shape {
    final double width;
    final double height;
    public Rectangle(double width, double height) { this.width = width; this.height = height; }
    public double area() { return width * height; }
}

public sealed class Triangle extends Shape permits EquilateralTriangle, IsoscelesTriangle {
    final double base;
    final double height;
    public Triangle(double base, double height) { this.base = base; this.height = height; }
    public double area() { return 0.5 * base * height; }
}

public final class EquilateralTriangle extends Triangle {
    public EquilateralTriangle(double side) { super(side, side * Math.sqrt(3) / 2); }
}

public final class IsoscelesTriangle extends Triangle {
    public IsoscelesTriangle(double base, double height) { super(base, height); }
}


public class SealedClassSwitchExample {

    public String getDescription(Shape shape) {
        // Le compilateur sait que Circle, Rectangle, et Triangle sont les seuls sous-types directs
        // Donc, pas besoin de 'default' si tous sont couverts.
        return switch (shape) {
            case Circle c -> "Cercle de rayon " + c.radius + " et aire " + c.area();
            case Rectangle r -> "Rectangle de " + r.width + "x" + r.height + " et aire " + r.area();
            // Pour Triangle, nous pouvons traiter ses sous-types scellés séparément
            case EquilateralTriangle et -> "Triangle équilatéral et aire " + et.area();
            case IsoscelesTriangle it -> "Triangle isocèle et aire " + it.area();
            // Note: Si nous avions juste 'case Triangle t -> ...', cela couvrirait aussi les sous-types
            // Mais ici, nous voulons un traitement spécifique pour les sous-types de Triangle.
            // Si Triangle était 'non-sealed', il faudrait un 'default' si ses sous-types n'étaient pas gérés.
        };
    }

    public static void main(String[] args) {
        SealedClassSwitchExample example = new SealedClassSwitchExample();

        System.out.println(example.getDescription(new Circle(5)));
        System.out.println(example.getDescription(new Rectangle(4, 6)));
        System.out.println(example.getDescription(new EquilateralTriangle(7)));
        System.out.println(example.getDescription(new IsoscelesTriangle(3, 4)));
    }
}

```

</details>

- Suppression de l'API Applet et du Security Mananger
- Renforcement de l'encapsulation des données

<details>
  <summary>Exemple</summary>
  
```java

// Seules Circle, Rectangle et Triangle peuvent étendre Shape
public sealed interface Shape permits Circle, Rectangle, Triangle {
    double area();
}

public final class Circle implements Shape { /* ... */ }
public final class Rectangle implements Shape { /* ... */ }
public final class Triangle implements Shape { /* ... */ }

// Si une classe en dehors de 'permits' tente d'implémenter Shape, le compilateur refusera.
// public class Pentagon implements Shape { /* ... ERREUR DE COMPILATION */ }

```

</details>

### Java 21 (LTS)

- Virtual Threads : Threads virtuels sont des threads légées qui réduisent considérablement le coût de la concurrence élevée.
  - Avoir des applications hautement concurrentes sans avoir recour à des paradigmes asynchrones complexes

 <details>
  <summary>Créer un Virtual Thread simple</summary>
   
```java

import java.time.Duration;
import java.util.concurrent.Executors;
import java.util.stream.IntStream;

public class SimpleVirtualThreadExample {

    public static void main(String[] args) throws InterruptedException {
        System.out.println("Démarrage du programme principal avec Virtual Threads.");

        // Créer et démarrer un Virtual Thread
        Thread.ofVirtual().start(() -> {
            System.out.println("Bonjour depuis un Virtual Thread !");
            try {
                Thread.sleep(Duration.ofSeconds(1)); // Pause le Virtual Thread, pas le Thread de plateforme
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            System.out.println("Virtual Thread a terminé son exécution.");
        });

        // Le programme principal continue son exécution
        System.out.println("Le programme principal continue...");

        // Attendre un peu pour que le virtual thread ait le temps de s'exécuter
        Thread.sleep(Duration.ofSeconds(2));
        System.out.println("Fin du programme principal.");
    }
}

```

</details>

 <details>
  <summary>Utilisation d'un ExecutorService pour Virtual Threads</summary>
   
```java

import java.time.Duration;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
import java.util.stream.IntStream;

public class VirtualThreadExecutorExample {

    public static void main(String[] args) throws InterruptedException {
        System.out.println("Démarrage du programme avec Virtual Thread Executor.");

        // Créer un ExecutorService qui démarre un nouveau Virtual Thread pour chaque tâche
        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {

            IntStream.range(0, 10).forEach(i -> {
                executor.submit(() -> {
                    System.out.println("Tâche " + i + " exécutée par Virtual Thread: " + Thread.currentThread());
                    try {
                        Thread.sleep(Duration.ofMillis(100)); // Simule un travail I/O bloquant
                    } catch (InterruptedException e) {
                        Thread.currentThread().interrupt();
                    }
                });
            });

            // L'ExecutorService se fermera automatiquement à la sortie du bloc try-with-resources
            // Ou vous pouvez l'arrêter manuellement et attendre sa terminaison :
            // executor.shutdown();
            // executor.awaitTermination(1, TimeUnit.MINUTES);

        } // Le bloc try-with-resources assure que executor.shutdown() est appelé

        System.out.println("Toutes les tâches soumises. Le programme principal va se terminer.");
        // Attendre un peu pour s'assurer que les messages des Virtual Threads s'affichent
        Thread.sleep(Duration.ofSeconds(1));
    }
}

```

</details>

 <details>
  <summary>Comparaison avec les Platform Threads (pour illustrer la scalabilité)</summary>
   
```java

import java.time.Duration;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;
import java.util.stream.IntStream;

public class ScaleComparisonExample {

    private static void performBlockingOperation(int taskId) {
        System.out.println("Démarrage tâche " + taskId + " sur Thread: " + Thread.currentThread());
        try {
            Thread.sleep(Duration.ofMillis(100)); // Simule une opération I/O bloquante
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        System.out.println("Fin tâche " + taskId);
    }

    public static void main(String[] args) throws InterruptedException {
        final int numberOfTasks = 50_000; // Essayez avec 1000 pour Platform Threads vs 50000+ pour Virtual Threads

        System.out.println("--- Démarrage avec Virtual Threads ---");
        long startTimeVirtual = System.currentTimeMillis();
        try (ExecutorService virtualExecutor = Executors.newVirtualThreadPerTaskExecutor()) {
            IntStream.range(0, numberOfTasks).forEach(i -> {
                virtualExecutor.submit(() -> performBlockingOperation(i));
            });
        }
        long endTimeVirtual = System.currentTimeMillis();
        System.out.println("Temps écoulé avec Virtual Threads: " + (endTimeVirtual - startTimeVirtual) + " ms");
        System.out.println("Nombre de tâches: " + numberOfTasks);


        // Attention : Exécuter ceci avec un grand nombre de tâches peut faire planter votre JVM
        // ou la rendre très lente si le nombre est trop élevé pour vos ressources système.
        // Décommentez pour tester, mais commencez avec un nombre beaucoup plus petit (ex: 1000-2000).
        /*
        System.out.println("\n--- Démarrage avec Platform Threads (attention aux ressources) ---");
        long startTimePlatform = System.currentTimeMillis();
        // Un FixedThreadPool avec un petit nombre de threads pour simuler un serveur web
        try (ExecutorService platformExecutor = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors())) {
            IntStream.range(0, Math.min(numberOfTasks, 2000)).forEach(i -> { // Limiter pour éviter l'épuisement des threads
                 platformExecutor.submit(() -> performBlockingOperation(i));
            });
            platformExecutor.shutdown();
            platformExecutor.awaitTermination(5, TimeUnit.MINUTES);
        }
        long endTimePlatform = System.currentTimeMillis();
        System.out.println("Temps écoulé avec Platform Threads: " + (endTimePlatform - startTimePlatform) + " ms");
        System.out.println("Nombre de tâches: " + Math.min(numberOfTasks, 2000));
        */
    }
}

```

</details>

- Pattern Matching : Eliminer les if-else if avec instanceof. Dans les classes scellées, le compilateur peut vérifier l'exhaustivité des cas dans un switch, garantissant qu'aucun sous type n'est oublié.
- Record Patterns : Permet de déstructurer des instances de claees record directement dans le pattern matching

</details>

 <details>
  <summary>Comparaison avec les Platform Threads (pour illustrer la scalabilité)</summary>
   
```java

// Définition des records
public record Point(int x, int y) {}
public record Circle(Point center, int radius) {}
public record Rectangle(Point topLeft, Point bottomRight) {}

public class ShapeProcessor {

    public String describeShape(Object shape) {
        return switch (shape) {
            case Circle(Point center, int r) -> // Record Pattern pour Circle
                "Cercle centré en (" + center.x() + ", " + center.y() + ") avec rayon " + r;
            case Rectangle(Point tl, Point br) -> // Record Pattern pour Rectangle
                "Rectangle du point (" + tl.x() + ", " + tl.y() + ") au point (" + br.x() + ", " + br.y() + ")";
            case Point p -> // Pattern de type simple pour Point
                "Juste un Point en (" + p.x() + ", " + p.y() + ")";
            default -> "Forme inconnue";
        };
    }

    // Exemple avec Record Patterns imbriqués
    public String describeShapeNested(Object shape) {
        return switch (shape) {
            // Décomposition du Circle, et décomposition imbriquée de Point
            case Circle(Point(int cx, int cy), int r) ->
                "Cercle centré en (" + cx + ", " + cy + ") avec rayon " + r;
            // Décomposition du Rectangle, et décomposition imbriquée de Point pour topLeft
            case Rectangle(Point(int tlx, int tly), Point bottomRight) ->
                "Rectangle dont le coin supérieur gauche est (" + tlx + ", " + tly + ") " +
                "et le coin inférieur droit est (" + bottomRight.x() + ", " + bottomRight.y() + ")";
            default -> "Forme inconnue ou non gérée.";
        };
    }

    public static void main(String[] args) {
        ShapeProcessor processor = new ShapeProcessor();

        System.out.println(processor.describeShape(new Circle(new Point(0, 0), 5)));
        // Output: Cercle centré en (0, 0) avec rayon 5

        System.out.println(processor.describeShape(new Rectangle(new Point(1, 1), new Point(10, 10))));
        // Output: Rectangle du point (1, 1) au point (10, 10)

        System.out.println(processor.describeShape(new Point(5, 5)));
        // Output: Juste un Point en (5, 5)

        System.out.println("\n--- Exemples avec Records imbriqués ---");
        System.out.println(processor.describeShapeNested(new Circle(new Point(10, 20), 15)));
        // Output: Cercle centré en (10, 20) avec rayon 15

        System.out.println(processor.describeShapeNested(new Rectangle(new Point(0, 0), new Point(5, 5))));
        // Output: Rectangle dont le coin supérieur gauche est (0, 0) et le coin inférieur droit est (5, 5)
    }
}


```

</details>

- Collections séquencées (Sequenced Collections) : Ajout d'une interface unifiée entre Set et List pour gérer l'ordre, accéder aux premiers et derniers éléments (SequencedCollection, SequencedSet ...)

### Java 25 (LTS) prévu pour septembre 2025

## Dernière version de Java

Dernière version LTS (Long Time Support) => 21

### Java 22

- Variables non nommées
- Class File API
- String template
- ...

## Programmation fonctionnelle

Java 8 et JST355 introduisent les bases du fonctionnel dans Java.
Le résultat de traitements est décrit mais pas la façon dont ils sont réalisés.
@FunctionalInterface pour créer une interface fonctionelle. Celle-ci possède une seule méthode abstraite.

Les 4 conceps de la PF sont :

- La pureté : Une fontion pure, au sens mathématique, est une fonction qui ne change pas l'état du monde
- L'immutabilité (ou immuabilié) : Il s'agit d'un concept allant de pair avec la pureté. Nous ne voulons pas changer l'état du monde, et ainsi nous ne changerons pas non plus l'état des paramètres passés à une fonction.
  En java, nous utiliserons le mot clé final.
- L'expressivité : Cela correspond à l'utilisation de fonctions d'ordre supérieur, c'es à dire ds fonctions qui prendront d'autres fonctions en paramètre.
- Composabilité : Il s'agit de la capacité à composer des fonctions ensemble pour obtenir une autre fonction.

## Fonction dite pure

Une fonction pure prend une ou des données en entrée et retourne un résultat en sorir.
Quel que soit le moment ou la fonction est jouée avec des données identiques en entrée, la sortie restera la même.
Pas de risque d'effet de bord à utiliser ces fonctions. Elles peuvent être rejouées à l'infini

## Différence entre List et tableau classique

- Un tableau peut contenit à la fois des valeurs primitives et des objets, mais ArrayList ne peut contenir que des objets.
- Un tableau utilise un opérateur d'affection pour stocker les éléments
- Arraylist utilise add() pour insérer des éléments

## List/Set/Map

- List = Doublons possibles et garde l'ordre avec index
- Set = pas de doublon, pas d'ordre
- Dans un Map, on a 2 objets par entrée, une clé et une valeur et on peut avoir des doublons mais les clés restent toujours uniques.

## Méthode filter()

L'opération filter() permet de ne conserver que les éléments du stream respectant une certaine condition.

## Méthode map()

L'opération map() renvoie un stream qui contient le résultat de l'application de la fonction sur chaque élément du stream.

## Méthode reduce()

L'opération reduce() applique de manière répétée une opération sur chacun des éléments pour les combiner afin de produire un résultat unique

## Méthode collect()

L'opération collect() est une opération terminale qui permet de réaliser une aggrégation de mutable des éléments.

## Méthode flatMap()

L'opération flatMap() permet d'appliquer une fonction à chaque élément du tableau puis d'aplati le résultat en un tableau.

## Les exceptions

C'est le mécanisme de gestion des erreurs.
Les exceptions représentent le mécanisme de gestion des erreurs intégrées au langage Java.
Il se compose d'objets représentant les erreurs et d'un ensemble de trois mots clés qui permettent de détecter et de traiter ces erreurs (try, catch et finally ...) mais aussi de les lever ou les propager aux couches suspérieures (throw et throws)
RuntimeException > Exception > Throwable > Object

## Exceptions gérées et non gérées

- Les exceptions gérées sont celles qui sont prises en compte dans la méthode afin que la méthode appelante puisse les gérer.
- Les exceptions non gérées vont apparaitre lorsqu'un morceau de code buggé est exécuté.
- Les exceptions non gérées sont dans la sous classe RuntimeException : ArithmeticException, ArrayStoreExceptions, ClassCastException ...

## Classe abstraite vs interface

Une classe abstraite permet de factoriser le code
class Fille extends une seule classe mère et doit juste implémenter les méthodes abstraites.
Une interface défini des services visibles depuis l'extérieur.

## Opérations terminales

Une opération terminale renvoie une valeur qui correspond au résultat de l'exécution du pipeline d'opérations sur les données.
Il n'est pas possible de réutiliser un Stream une fois que son opération terminale a été invoquée

## Sérialization/Désérialization

Sérialiser un objet consiste à le convertir en untableau d'octets, que l'on peut ensuite écrire ans un fichier, l'envoyer sur un réseau au travers d'un socket etc ...
La désérialization suit le processus inverse.
Pour sérialiser un objet, on utilise l'interface Serializable.

## Equals/Hashcode

- Ce sont 2 méthodes de classe d'objet. Tous les objets sont des Object.
- Deux objets égaux doivent présenter le même hashcode. Le hash code est la valeur de hachage de l'objet en question.
- Si 2 objets identique avec un hashcode différent alors on aura des "doublons" dans un Set
- Si equals n'est pas défini, on compare les adresses avec ==

## Final/Static

- static signifie qu'il n'y a qu'une seule copie de la variable en mémoire et celle ci est partagée par toutes les instance sde la classe.
- final signifie simplement que la valeur ne peut pas être modifiée. Sans final, tout objet peut modifier la valeur de la variable.
