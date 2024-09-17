
# Spring

- Dernière version de Spring Boot : 3.3.3
- Dernière version de Java : 22
- Pour traiter des données : Spring Data ou JPA
- Différence entre tests unitaires et d'intégrations

## Créer un projet Spring rapidement

- Pour initialiser un projet [rapidement](https://start.spring.io/ )

## Framework Spring

- Repose sur un conteneur IoC (Inversion of control) qui assure la gestion du cycle de vie des beans et l'injection de dépendance
- Utilisation de l'AOP (Aspect Oriented Programming), mise à œuvre de la séparation des préoccupations.  

## Types d'injection de dépendance

- Mécanisme qui permet d'implémenter le principe d'inversion of control.
- Il consiste à créer dynamiquement (injecter) les dépendances entre les différentes classes en s’appuyant sur une description (fichier de configuration ou métadonnées) ou de manière programmatique.
- Ainsi les dépendances entre composants logiciels ne sont plus exprimées dans le code de manière statique mais déterminées dynamiquement à l’exécution.
- Elle consiste à injecter dynamiquement les dépendances pour différentes classes en s’appuyant sur un ou plusieurs modules. Ainsi, les dépendances entre des classes d’implémentation et une interface ne sont plus exprimées dans le code de manière statique mais déterminées dynamiquement.

## Asynchronisme en Spring

- Code propre, lisible, faiblement couplés.
- Il est plus réutilisable et peut être utilisé dans un contexte différent.

## Hibernate vs JPA vs Spring Data

- Hibernate est un framework. C'est une implémentation de JPA
- Java Persistence API est une norme
- Spring Data est une abstraction d'accès aux données JPA
- Il existe aussi Spring JDBC. On peut faire des preparedStatement pour empêcher les injections SQL. (faille de sécurité très connue)

## Scope

@Singleton est le scope par défaut dans Spring. Une seule instance de l'objet est créée et réutilisée.
@Prototype => Différentes instances sont créées à chaque appel du bean.
@Request
@Session

## Spring boot

- C'est un framework de dév. Java, une déclinaison du framework Spring classique qui permet essentiellement de faire des micro services.
- Dans Spring boot, tout est @Bean et à base de conf.
- Avantages => Optimisation de la gestion des dépendances, auto-configuration avec @SpringBootApplication, gestion des properties et déploiement facile
- Le serveur est fourni
- Annotations pour faire des controllers : @RestController, @RequestMapping, @GetMapping
- @Repository
- @Service
- Facilité pour séparer en 3 couches : Controller -> Service -> Repository

## Annotation pour injecter une dépendance
Il existe 4 types d’injections de dépendances :
- injection par constructeur ;

  ```
      @Autowired
    public Car(Engine engine, Transmission transmission) {
        this.engine = engine;
        this.transmission = transmission;
    }
  ```
  
- injection par interface ;
```
  public class ProductService {

   @Autowired
   private ProductRepository productRepository;

}
```
- injection par mutateur ;
```
public class ProductService {
   private ProductRepository productRepository;
  
   @Autowired
   public void setProductRepository(ProductRepository productRepository) {
      this.productRepository = productRepository;
   }
}
```
- injection par champs.

## Asynchronisme en Spring @Sync pour gérer l'asynchronysme.

Il faut faire attention aux proxy lors de l'utilisation de @Sync
Hibernate vs JPA vs Spring data    Hibernate est un framework. C'est une implémentation JPA.
Java Persistence API est une norme.
Spring data est une abstraction d'accès aux données JPA.

## Singleton
```
public class Singleton{

   private static final INSTANCE = new Singleton();

   /** private constructor pour être sûr que personne ne pourra créer une instance **/
   private Singleton(){
      // ... init code
   }

   public Singleton getInstance(){
      if(instance == null){
         instance = new Singleton();
      }
      return instance;
   }
   // autres methodes de la classe ...
}
```
## Spring MVC

- Spring MVC (Model View Controller) pour développer des applis Web.

## Statefull vs stateless

###  Stateless
Un processus ou une application stateless est indépendant. Il ne stocke pas de données et ne fait référence à aucune transaction passée. Chaque transaction est effectuée à partir de rien, comme si c'était la première fois. Les applications stateless fournissent un service ou une fonction et utilisent un réseau de diffusion de contenu, le web ou des serveurs d'impression pour traiter ces requêtes à court terme.
Par exemple, une recherche en ligne pour répondre à une question quelconque est une transaction stateless. Vous tapez votre question dans le moteur de recherche et appuyez sur Entrée. Si votre transaction est accidentellement interrompue ou fermée, vous devez en démarrer une nouvelle. Les transactions stateless sont comparables à des distributeurs automatiques : une seule requête et une seule réponse.

### Stateful

Les applications et processus stateful, quant à eux, peuvent être réutilisés indéfiniment. Les plateformes bancaires en ligne et les messageries en sont deux exemples. Les transactions précédentes sont prises en compte et peuvent affecter la transaction actuelle. C'est pour cela que les applications stateful utilisent les mêmes serveurs chaque fois qu'elles traitent une requête d'un utilisateur.
Si une transaction statefulest interrompue, le contexte et l'historique sont stockés et vous pouvez ainsi reprendre là où vous en étiez. Les applications stateful gardent une trace de divers éléments, comme l'URL de la page, les paramètres de préférence et l'activité récente. Les transactions stateful sont comparables à une conversation continue et périodique avec la même personne.

"Stateful" et "Stateless" sont des attributs pour les beans de session.

Un bean session (en bref) fournit un moyen d'appeler des méthodes sur un serveur d'applications. Le bean est une instance d'une classe Java. Habituellement, un bean est détruit après la fin de la méthode distante (et renvoie un résultat). Ces beans sont "stateless".

Il est possible (mais plutôt inhabituel) d'ajouter des champs et des attributs au bean afin qu'un client puisse "créer" cette instance sur le serveur et l'utiliser pour plus d'une opération. Ces beans sont "statefull" (et doivent être évités).
