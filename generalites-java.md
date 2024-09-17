# JAVA

## Généralités

### Java 8

- Lambdas expressions
- streams (map, reduce)
- Référence de méthode => Faire référence à une méthode d'une interface fonctionnelle
- Interface optinnelle => Interface qui ne contient qu'une seule méthode abstraite
- Optional => Utilisé pour traiter les NPE, fournit des méthodes pour vérifier la présence d'une valeur

### Java 9

- Jigsaw pour rendre modulaire l'application et réduire la taille sur les env.
- Méthodes privées dans les interfaces
- try-with-resources
- API Flow

### Java 10

- Inférence de type => Utilisation de var afin de gagner en lisiblité

### Java 11

- Inférence de type pour les paramètres e lambdas => utilisation de var dans les lambdas
- Nouveau client HTTP compatible avec la version 2 de HTTP

## Dernière version de Java

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

Ce sont 2 méthodes de classe d'objet. Tous les objets sont des Object.
Deux objets égaux doivent présenter le même hashcode
Si 2 objets identique avec un hashcode différent alors on aura des "doublons" dans un Set
Si equals n'est pas défini, on compare les adresses avec ==

## Final/Static

- static signifie qu'il n'y a qu'une seule copie de la variable en mémoire et celle ci est partagée par toutes les instance sde la classe.
- final signifie simplement que la valeur ne peut pas être modifiée. Sans final, tout objet peut modifier la valeur de la variable.
