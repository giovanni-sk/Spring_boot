## Liste des annotations les plus couramment utilisées dans Spring Boot, classées par ordre d'importance du plus utile au moins utile, avec leur rôle et des exemples d'utilisation.

### 1. `@RestController`
**Rôle :** Combinaison de `@Controller` et `@ResponseBody`. Indique qu'une classe est un contrôleur REST, et que les méthodes de cette classe renvoient des données JSON ou XML directement dans la réponse HTTP.

**Exemple :**
```java
@RestController
@RequestMapping("/api/books")
public class BookController {

    @GetMapping
    public List<Book> getAllBooks() {
        // Logique pour récupérer tous les livres
    }
}
```

### 2. `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`
**Rôle :** Spécifie le type de requête HTTP (GET, POST, PUT, DELETE) et l'URL à laquelle la méthode est mappée.

**Exemple :**
```java
@GetMapping("/books")
public List<Book> getAllBooks() {
    // Récupérer tous les livres
}
```

### 3. `@RequestMapping`
**Rôle :** Mappe les requêtes HTTP sur des méthodes ou classes spécifiques, de manière plus générale que les annotations comme `@GetMapping`.

**Exemple :**
```java
@RequestMapping(value = "/books", method = RequestMethod.GET)
public List<Book> getAllBooks() {
    // Récupérer tous les livres
}
```

### 4. `@Service`
**Rôle :** Indique qu'une classe est un service (couche métier) dans l'application Spring. Elle est automatiquement détectée par Spring lors du scan des composants.

**Exemple :**
```java
@Service
public class BookService {
    // Logique métier pour gérer les livres
}
```

### 5. `@Repository`
**Rôle :** Indique que la classe est un composant DAO (Data Access Object) qui interagit avec la base de données. Elle est utilisée pour encapsuler la logique d'accès aux données.
Non obligatoire du moment on extends deja la classe du JpaRepository
**Exemple :**
```java
@Repository
public interface BookRepository extends JpaRepository<Book, Long> {
    // Méthodes pour interagir avec la base de données
}
```

### 6. `@Entity`
**Rôle :** Marque une classe comme une entité JPA, c'est-à-dire qu'elle correspond à une table dans la base de données.

**Exemple :**
```java
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String title;
    private String author;
    // Autres attributs, getters et setters
}
```

### 7. `@Autowired`
**Rôle :** Injecte automatiquement les dépendances dans les composants Spring (comme les services, repositories, etc.).

**Exemple :**
```java
@Service
public class BookService {

    @Autowired
    private BookRepository bookRepository;
}
```

### 8. `@Component`
**Rôle :** Marque une classe comme un composant Spring générique. Les annotations spécialisées comme `@Service`, `@Repository`, et `@Controller` en héritent.

**Exemple :**
```java
@Component
public class MyComponent {
    // Logique ici
}
```

### 9. `@Configuration`
**Rôle :** Indique qu'une classe contient des méthodes de configuration et des beans qui doivent être gérés par le conteneur Spring.

**Exemple :**
```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

### 10. `@Bean`
**Rôle :** Indique qu'une méthode produit un bean qui doit être géré par Spring.

**Exemple :**
```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

### 11. `@PathVariable`
**Rôle :** Lie une variable de l'URL à un paramètre de méthode.

**Exemple :**
```java
@GetMapping("/books/{id}")
public Book getBookById(@PathVariable Long id) {
    // Logique pour récupérer un livre par ID
}
```

### 12. `@RequestParam`
**Rôle :** Extrait les paramètres de requête (query parameters) d'une URL.

**Exemple :**
```java
@GetMapping("/books")
public List<Book> getBooksByAuthor(@RequestParam String author) {
    // Logique pour récupérer les livres par auteur
}
```

### 13. `@RequestBody`
**Rôle :** Lie le corps d'une requête HTTP (format JSON ou XML) à un objet Java.

**Exemple :**
```java
@PostMapping("/books")
public Book createBook(@RequestBody Book book) {
    // Logique pour créer un nouveau livre
}
```

### 14. `@ResponseBody`
**Rôle :** Indique que le résultat d'une méthode de contrôleur doit être écrit directement dans la réponse HTTP, généralement sous forme de JSON ou XML.

**Exemple :**
```java
@ResponseBody
@GetMapping("/books")
public List<Book> getAllBooks() {
    // Récupérer tous les livres
}
```

### 15. `@RequestHeader`
**Rôle :** Lie une valeur d'en-tête HTTP à un paramètre de méthode.

**Exemple :**
```java
@GetMapping("/books")
public List<Book> getBooksByHeader(@RequestHeader("Authorization") String token) {
    // Logique pour récupérer des livres en utilisant un jeton d'autorisation
}
```

### 16. `@ExceptionHandler`
**Rôle :** Définit une méthode comme étant responsable du traitement d'une exception spécifique dans un contrôleur.

**Exemple :**
```java
@ExceptionHandler(BookNotFoundException.class)
public ResponseEntity<String> handleNotFound(BookNotFoundException ex) {
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
}
```

### 17. `@ControllerAdvice`
**Rôle :** Permet de définir des gestionnaires d'exceptions globaux pour plusieurs contrôleurs.

**Exemple :**
```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleAllExceptions(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(ex.getMessage());
    }
}
```

### 18. `@Transactional`
**Rôle :** Indique que la méthode ou la classe doit être exécutée dans une transaction, ce qui permet de gérer les transactions dans Spring.

**Exemple :**
```java
@Service
public class BookService {

    @Transactional
    public void saveBook(Book book) {
        // Logique pour sauvegarder un livre
    }
}
```

### 19. `@Primary`
**Rôle :** Indique qu'un bean doit être préféré lors de l'injection lorsque plusieurs beans de même type sont disponibles.

**Exemple :**
```java
@Bean
@Primary
public MyService primaryService() {
    return new MyServiceImpl1();
}
```

### 20. `@Scope`
**Rôle :** Définit le cycle de vie d'un bean, comme `singleton` ou `prototype`.

**Exemple :**
```java
@Bean
@Scope("prototype")
public MyService prototypeService() {
    return new MyService();
}
```

### 21. `@EnableAutoConfiguration`
**Rôle :** Permet à Spring Boot de configurer automatiquement l'application en fonction des dépendances trouvées sur le classpath.

**Exemple :**
```java
@SpringBootApplication
@EnableAutoConfiguration
public class LibraryApplication {
    // ...
}
```

### 22. `@EnableJpaRepositories`
**Rôle :** Active la détection automatique des repositories JPA dans le package spécifié.

**Exemple :**
```java
@EnableJpaRepositories(basePackages = "com.example.library.repository")
public class JpaConfig {
    // ...
}
```
Voici une liste complète des annotations importantes dans Spring Boot, en ajoutant celles qui ne figurent pas encore dans votre liste et en expliquant leur rôle et leur utilisation :

### 23. `@SpringBootApplication`
**Rôle :** C'est une annotation composite qui englobe `@Configuration`, `@EnableAutoConfiguration`, et `@ComponentScan`. Elle est utilisée pour démarrer une application Spring Boot.

**Exemple :**
```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

### 24. `@Value`
**Rôle :** Injecte des valeurs dans les champs d'un bean depuis le fichier de configuration (`application.properties` ou `application.yml`).

**Exemple :**
```java
@Component
public class MyComponent {

    @Value("${my.property}")
    private String myProperty;

    // Utiliser myProperty ici
}
```

### 25. `@Profile`
**Rôle :** Spécifie que la configuration ou le bean ne doit être actif que dans un certain profil (par exemple, développement, production).

**Exemple :**
```java
@Configuration
@Profile("dev")
public class DevConfig {
    // Beans pour le profil de développement
}
```

### 26. `@ConditionalOnProperty`
**Rôle :** Conditionne l'enregistrement d'un bean à la présence d'une propriété spécifique dans la configuration.

**Exemple :**
```java
@Configuration
@ConditionalOnProperty(name = "feature.enabled", havingValue = "true")
public class FeatureConfig {
    // Configuration conditionnelle basée sur une propriété
}
```

### 27. `@ConditionalOnClass`
**Rôle :** Conditionne l'enregistrement d'un bean à la présence d'une classe spécifique sur le classpath.

**Exemple :**
```java
@Configuration
@ConditionalOnClass(SomeClass.class)
public class SomeClassConfig {
    // Configuration conditionnelle basée sur la présence d'une classe
}
```

### 28. `@ConditionalOnMissingBean`
**Rôle :** Conditionne l'enregistrement d'un bean si un autre bean de même type n'existe pas déjà.

**Exemple :**
```java
@Configuration
public class MyConfig {

    @Bean
    @ConditionalOnMissingBean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

### 29. `@Cacheable`
**Rôle :** Indique que le résultat d'une méthode doit être mis en cache.

**Exemple :**
```java
@Cacheable("books")
public Book getBook(Long id) {
    // Logique pour récupérer un livre
}
```

### 30. `@CacheEvict`
**Rôle :** Indique que le cache doit être invalidé pour une méthode spécifique.

**Exemple :**
```java
@CacheEvict("books")
public void updateBook(Book book) {
    // Logique pour mettre à jour un livre
}
```

### 31. `@CachePut`
**Rôle :** Met à jour le cache avec le résultat de la méthode.

**Exemple :**
```java
@CachePut("books")
public Book updateBook(Long id, Book book) {
    // Logique pour mettre à jour un livre et mettre à jour le cache
}
```

### 32. `@Async`
**Rôle :** Indique qu'une méthode doit être exécutée de manière asynchrone dans un thread séparé.

**Exemple :**
```java
@Async
public CompletableFuture<String> asyncMethod() {
    // Traitement asynchrone
}
```

### 33. `@EventListener`
**Rôle :** Permet d'écouter des événements Spring ApplicationContext.

**Exemple :**
```java
@Component
public class MyEventListener {

    @EventListener
    public void handleCustomEvent(CustomEvent event) {
        // Traitement de l'événement
    }
}
```

### 34. `@Scheduled`
**Rôle :** Permet de planifier des tâches à exécuter périodiquement.

**Exemple :**
```java
@Component
public class ScheduledTasks {

    @Scheduled(fixedRate = 5000)
    public void performTask() {
        // Tâche à exécuter toutes les 5 secondes
    }
}
```

### 35. `@Import`
**Rôle :** Permet d'importer des configurations supplémentaires dans la configuration principale.

**Exemple :**
```java
@Configuration
@Import(AdditionalConfig.class)
public class MainConfig {
    // Configuration principale
}
```

### 36. `@PropertySource`
**Rôle :** Spécifie des fichiers de propriétés supplémentaires à charger dans le contexte Spring.

**Exemple :**
```java
@Configuration
@PropertySource("classpath:additional.properties")
public class AppConfig {
    // Configuration
}
```

### 37. `@Transactional(readOnly = true)`
**Rôle :** Indique que la méthode ou la classe est en lecture seule, ce qui peut optimiser les performances pour les opérations de lecture.

**Exemple :**
```java
@Service
@Transactional(readOnly = true)
public class BookService {

    public List<Book> getAllBooks() {
        // Lecture uniquement
    }
}
```

### 38. `@Data`
**Rôle :** Fournit des annotations Lombok pour générer automatiquement getters, setters, `equals()`, `hashCode()`, et `toString()`. 

**Exemple :**
```java
@Data
public class Book {
    private Long id;
    private String title;
    private String author;
}
```

### 39. `@Setter`, `@Getter`, `@ToString`, `@EqualsAndHashCode`
**Rôle :** Fournit des annotations Lombok pour générer des getters, setters, méthodes `toString()`, et méthodes `equals()`/`hashCode()` individuellement.

**Exemple :**
```java
@Getter
@Setter
@ToString
@EqualsAndHashCode
public class Book {
    private Long id;
    private String title;
    private String author;
}
```

### 40. `@FieldDefaults`
**Rôle :** Définit les niveaux d'accès par défaut pour les champs dans une classe.

**Exemple :**
```java
@FieldDefaults(level = AccessLevel.PRIVATE)
public class Book {
    Long id;
    String title;
    String author;
}
```

Ces annotations couvrent une large gamme de fonctionnalités offertes par Spring et Spring Boot pour développer des applications robustes et bien structurées. Utiliser ces annotations de manière appropriée vous aidera à tirer parti des capacités du framework et à maintenir un code propre et maintenable.
---

Ces annotations couvrent la majorité des fonctionnalités nécessaires pour développer une application Spring Boot. Celles listées au début sont les plus couramment utilisées et essentielles, tandis que celles vers la fin sont plus spécifiques à certains cas d'utilisation.
