## BIBLIOTHEQUE LOMBOK
Lombok est une bibliothèque Java populaire qui vise à réduire le code boilerplate en générant automatiquement des méthodes courantes, des constructeurs et d'autres éléments du code à l'aide d'annotations. En utilisant Lombok, vous pouvez rendre votre code plus concis, lisible et facile à maintenir.

### **Principales Fonctionnalités de Lombok**

Voici un aperçu complet des principales annotations fournies par Lombok, leurs rôles et des exemples d'utilisation.

#### 1. **Annotations pour les Getters et Setters**

- **`@Getter`**
  - **Rôle** : Génère des méthodes getter pour tous les champs de la classe.
  - **Exemple :**
    ```java
    @Getter
    public class Person {
        private String name;
        private int age;
    }
    ```

- **`@Setter`**
  - **Rôle** : Génère des méthodes setter pour tous les champs de la classe.
  - **Exemple :**
    ```java
    @Setter
    public class Person {
        private String name;
        private int age;
    }
    ```

- **`@Data`**
  - **Rôle** : Combine `@Getter`, `@Setter`, `@EqualsAndHashCode`, `@ToString`, et `@RequiredArgsConstructor`. Fournit une implémentation complète de la classe avec des méthodes pour les getters, setters, `equals()`, `hashCode()`, `toString()` et un constructeur pour les champs `final`.
  - **Exemple :**
    ```java
    @Data
    public class Person {
        private final String name;
        private int age;
    }
    ```

#### 2. **Annotations pour les Constructeurs**

- **`@AllArgsConstructor`**
  - **Rôle** : Génère un constructeur avec un paramètre pour chaque champ.
  - **Exemple :**
    ```java
    @AllArgsConstructor
    public class Person {
        private String name;
        private int age;
    }
    ```

- **`@NoArgsConstructor`**
  - **Rôle** : Génère un constructeur sans arguments.
  - **Exemple :**
    ```java
    @NoArgsConstructor
    public class Person {
        private String name;
        private int age;
    }
    ```

- **`@RequiredArgsConstructor`**
  - **Rôle** : Génère un constructeur avec des paramètres pour tous les champs `final` et ceux marqués avec `@NonNull`.
  - **Exemple :**
    ```java
    @RequiredArgsConstructor
    public class Person {
        private final String name;
        private int age;
    }
    ```

#### 3. **Annotations pour les Méthodes**

- **`@ToString`**
  - **Rôle** : Génère la méthode `toString()` en incluant les champs de la classe.
  - **Exemple :**
    ```java
    @ToString
    public class Person {
        private String name;
        private int age;
    }
    ```

- **`@EqualsAndHashCode`**
  - **Rôle** : Génère les méthodes `equals()` et `hashCode()` en fonction des champs de la classe.
  - **Exemple :**
    ```java
    @EqualsAndHashCode
    public class Person {
        private String name;
        private int age;
    }
    ```

- **`@Synchronized`**
  - **Rôle** : Fournit une version thread-safe d'une méthode en utilisant un verrou. Cela remplace l'utilisation de `synchronized` directement dans le code.
  - **Exemple :**
    ```java
    @Synchronized
    public void doSomething() {
        // Code thread-safe
    }
    ```

#### 4. **Annotations pour le Pattern Builder**

- **`@Builder`**
  - **Rôle** : Génère un modèle de construction (Builder Pattern) pour la classe annotée, permettant de créer des objets avec une syntaxe fluide.
  - **Exemple :**
    ```java
    @Builder
    public class Person {
        private String name;
        private int age;
    }
    ```

#### 5. **Annotations pour la Gestion des Exceptions**

- **`@Getter` / `@Setter` sur les Exceptions**
  - **Rôle** : Génère des getters et setters pour les attributs des exceptions, facilitant leur gestion et utilisation dans les applications.
  - **Exemple :**
    ```java
    @Getter
    public class CustomException extends RuntimeException {
        private final int errorCode;
        
        public CustomException(String message, int errorCode) {
            super(message);
            this.errorCode = errorCode;
        }
    }
    ```

#### 6. **Annotations pour la Gestion des Loggings**

- **`@Slf4j`**
  - **Rôle** : Génère un logger SLF4J statique pour la classe, ce qui facilite l'ajout de loggings sans avoir à déclarer manuellement une instance de `Logger`.
  - **Exemple :**
    ```java
    @Slf4j
    public class MyClass {
        public void doSomething() {
            log.info("Doing something");
        }
    }
    ```

- **`@Log`**, **`@Log4j`**, **`@Log4j2`**, **`@CommonsLog`**, **`@Flogger`**
  - **Rôle** : Fournit des loggers pour diverses bibliothèques de logging comme `java.util.logging`, `Log4j`, `Log4j2`, Apache Commons Logging, et Google Flogger.
  - **Exemple :**
    ```java
    @Log4j2
    public class MyClass {
        public void doSomething() {
            log.info("Doing something");
        }
    }
    ```

#### 7. **Annotations pour les Access Levels**

- **`@FieldDefaults`**
  - **Rôle** : Définit les niveaux d'accès par défaut (par exemple, `private`, `protected`) pour les champs dans une classe.
  - **Exemple :**
    ```java
    @FieldDefaults(level = AccessLevel.PRIVATE)
    public class Person {
        String name;
        int age;
    }
    ```

#### 8. **Annotations pour les Exceptions et les Erreurs**

- **`@NonNull`**
  - **Rôle** : Génère des vérifications pour les paramètres de méthode et les champs pour s'assurer qu'ils ne sont pas null.
  - **Exemple :**
    ```java
    public class Person {
        private final String name;

        public Person(@NonNull String name) {
            this.name = name;
        }
    }
    ```

### **Intégration et Configuration**

Pour utiliser Lombok dans un projet Maven, ajoutez la dépendance suivante à votre fichier `pom.xml` :

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.24</version> <!-- Vérifiez la version la plus récente -->
    <scope>provided</scope>
</dependency>
```

Pour Gradle, ajoutez cette ligne à votre fichier `build.gradle` :

```groovy
dependencies {
    compileOnly 'org.projectlombok:lombok:1.18.24' // Vérifiez la version la plus récente
    annotationProcessor 'org.projectlombok:lombok:1.18.24'
}
```

### **Avantages de Lombok**

- **Réduction du code boilerplate** : Lombok génère automatiquement des méthodes courantes, réduisant ainsi la quantité de code répétitif que vous devez écrire.
- **Code plus lisible** : Les annotations permettent d'améliorer la lisibilité du code en éliminant les parties répétitives.
- **Facilité d'utilisation** : Lombok simplifie les tâches courantes comme la gestion des getters, setters, et constructeurs.

### **Inconvénients de Lombok**

- **Dépendance supplémentaire** : Ajouter Lombok comme dépendance peut introduire une nouvelle dépendance dans le projet.
- **Complexité des outils** : Certains outils de développement et environnements peuvent ne pas bien supporter Lombok ou nécessiter une configuration supplémentaire.
- **Opacité** : Le code généré par Lombok peut rendre le débogage plus complexe, car il n'est pas directement visible dans le code source.

Lombok est une bibliothèque puissante pour simplifier le code Java, mais son utilisation doit être équilibrée avec une compréhension des impacts sur le projet et les outils de développement utilisés.
