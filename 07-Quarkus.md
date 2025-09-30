- Quarkus

| Aspect | Description de Quarkus | Lien avec Spring |
| :--- | :---: | :---: |
| But principal | Framework Java "Supersonique Subatomique" conçu pour le cloud natif, les microservices et les architectures sans serveur (serverless) | Spring Boot est aussi très utilisé pour les microservices. La philosophie : Faciliter la création et le déploiement d'applications. |
| Performance | Temps de démarrage extrêment rapide, empreinte mémoire très faible (surtout complié en natif avec GraalVM) | Spring est souvent plus lourd et plus lent au démarrage |
| Technologie clé | Se base sur les standards Java bien établis (JAX-RS, CDI, JPA) et les optimise. | Spring et Quarkus s'appuient sur les standards Java Entreprise (Gestion des dépendances, annotations) |
| Argument | Comment-est ce que je peux apprendre rapidement Quarkus avec mon expérience ? | Bien que je n'aie pas encore eu l'occasion de travailler sur Quarkus, mon expertise de Senior en JAVA et en particulier avec Spring et Spring Boot me donne une excellente compréhension des enjeux d'un framework back-end. Je suis familier avec les problématiques de microservices, d'API REST et de conteneurisation, qui sont au cœur de Quarkus. Je suis confiant(e) dans ma capacité à monter en compétence très rapidement sur Quarkus, d'autant plus que je vois l'avantage qu'il apporte en matière de performance et de légèreté pour les applications cloud-native|


- L'Optimisation au Temps de Compilation (Build Time)

# "Compile Time Boot"
 Au lieu de faire tout le travail d'initialisation (scan des classes, configuration de la Dependency Injection, etc.) au démarrage de l'application (comme Spring Boot), Quarkus le fait pendant la compilation (Build Time).

# GraalVM
C'est un JDK de haute performance qui a 2 fonctions principales :
## Un Compilateur JIT Amélioré (Just-In-Time)
Compilateur JIT plus performant. Utilisation de moins de ressoures. Démarre plus rapidement pour atteindre les performances maximales plus tôt.
## Le "Native Image" : Compilation AOT (Ahead-Of-Time)
Principe AOT : Au lieu de compiler le code Java pendant l'exécution (JIT), GraalVM permet de le compiler en avance sur le temps (Ahead-Of-Time ou AOT) directement en un exécutable natif (un fichier binaire) pour un système d'exploitation et une architecture spécifiques (par exemple, un .exe pour Windows ou un binaire pour Linux).

Quarkus est optimisé pour être compilé en exécutable natif avec l'outil GraalVM. Le code Java est transformé en un binaire machine, sans avoir besoin d'une JVM pour s'exécuter.

# Le Modèle de Développement "Kubernetes-Native"

## Container First
Le framework est conçu pour fonctionner de manière optimale dans un conteneur Linux/Kubernetes. Il utilise les ressources de la manière la plus efficace possible (mémoire RSS, CPU).

## Développeur (Developer Joy)
Quarkus maintient les standards Java (CDI, JAX-RS/RestEasy, JPA/Hibernate) pour que les développeurs Java se sentent à l'aise, tout en offrant le Live Coding.

# Les Standards et la Compatibilité (Le Pont avec Spring)

## Java Standards
Quarkus utilise Jakarta EE standards (comme CDI pour l'injection de dépendances et JAX-RS pour les API REST), mais avec sa propre implémentation optimisée (ArC pour l'injection).

## Impératif & Réactif
Quarkus prend en charge les deux styles : le code impératif classique (comme vous le faites dans la plupart des applications Spring) et le code réactif non-bloquant (comme Spring WebFlux).
