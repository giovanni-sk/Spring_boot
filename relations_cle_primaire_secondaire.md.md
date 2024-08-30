## Les Relations de table 
### 1. Relation `One-to-Many` entre `User` et `Order`

- **Description** : Un `User` peut passer plusieurs `Order` (commandes).
- **Implémentation** : 
  - Dans l'entité `User`, vous avez une relation `@OneToMany` avec `Order`.
  - `Order` possède une clé étrangère `user_id` qui référence le `User`.
  
  ```java
  @Entity
  public class User {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      
      @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
      private List<Order> orders;
  }
  
  @Entity
  public class Order {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      
      @ManyToOne
      @JoinColumn(name = "user_id", nullable = false)
      private User user;
  }
  ```

### 2. Relation `One-to-Many` entre `Order` et `OrderItem`

- **Description** : Une `Order` peut contenir plusieurs `OrderItem` (articles de commande).
- **Implémentation** :
  - Dans l'entité `Order`, il y a une relation `@OneToMany` avec `OrderItem`.
  - `OrderItem` possède une clé étrangère `order_id` qui référence `Order`.

  ```java
  @Entity
  public class Order {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;

      @OneToMany(mappedBy = "order", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
      private List<OrderItem> orderItems;
  }
  
  @Entity
  public class OrderItem {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      
      @ManyToOne
      @JoinColumn(name = "order_id", nullable = false)
      private Order order;
  }
  ```

### 3. Relation `Many-to-One` entre `OrderItem` et `Product`

- **Description** : Un `OrderItem` correspond à un `Product` spécifique, mais un produit peut apparaître dans plusieurs `OrderItem`.
- **Implémentation** :
  - Dans l'entité `OrderItem`, vous avez une relation `@ManyToOne` avec `Product`.
  - `OrderItem` possède une clé étrangère `product_id` qui référence `Product`.

  ```java
  @Entity
  public class OrderItem {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;

      @ManyToOne
      @JoinColumn(name = "product_id", nullable = false)
      private Product product;
  }
  
  @Entity
  public class Product {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;

      @OneToMany(mappedBy = "product", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
      private List<OrderItem> orderItems;
  }
  ```

### Résumé des Relations

1. **`User` ↔ `Order`** : 
   - Un `User` peut avoir plusieurs `Order` (`One-to-Many`).
   - Une `Order` est associée à un seul `User` (`Many-to-One`).

2. **`Order` ↔ `OrderItem`** :
   - Une `Order` peut contenir plusieurs `OrderItem` (`One-to-Many`).
   - Un `OrderItem` appartient à une seule `Order` (`Many-to-One`).

3. **`OrderItem` ↔ `Product`** :
   - Un `OrderItem` correspond à un seul `Product` (`Many-to-One`).
   - Un `Product` peut être référencé dans plusieurs `OrderItem` (`One-to-Many`).

Ces relations permettent de structurer la base de données pour représenter les interactions réelles entre les utilisateurs, les commandes, et les produits dans un système de gestion de commandes.
