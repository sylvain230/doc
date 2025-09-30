
# ReactJS

Librairie JavaScript basée sur JS et créée par Facebook. L'objectif de cette biblio. est de fournir aux dév une interface utilisateur réutilisable complète.

## Généralités

### Dernière version de React

React est une librairie OpenSource Javascript

JSX signifie JavaScript XML et il s'agit d'une extension de syntaxe de type XML pour ECMAScript. Fondamentalement, il fournit simplement le sucre syntaxique pour la fonction React.createElement(type, props, ...children), nous donnant l'expressivité de JavaScript ainsi qu'une syntaxe de modèle de type HTML.

Les principales fonctionnalités de React sont :

- Utilise la syntaxe JSX, une extension de syntaxe de JS qui permet aux développeurs d'écrire du HTML dans leur code JS.
- Il utilise Virtual DOM au lieu de Real DOM étant donné que les manipulations Real DOM sont coûteuses.
- Prend en charge le rendu côté serveur, utile pour les optimisations des moteurs de recherche (SEO).
- Suit le flux de données unidirectionnel ou unidirectionnel ou la liaison de données.
- Utilise des composants d'interface utilisateur réutilisables/composables pour développer la vue.

## Composants

Les composants vous permettent de découper l'interface utilisateur en éléments indépendants et réutilisables, vous permettant ainsi de considérer chaque élément de manière isolée.
Ce sont des fonctions Javascript.

## Cycle de vie d'un composant

Trois étapes Initialisation => Mise à jour des états => Destructions

## Etat

L'état d'un composant est un objet qui contient des informations qui peuvent changer au cours de la durée de vie du composant. Le point important est que chaque fois que l'objet d'état change, le composant est restitué. Il est toujours recommandé de rendre notre état aussi simple que possible et de minimiser le nombre de composants avec état.

## Différence entre ReactJS et React Native

ReactJS est une bibliothèque Javascript alors que React Native est une plate-forme complète dotées de nombreuses fonctionnalités pour créer une app. du début à la fin.

## State

state est géré dans un composant comme le sont les variables. Il correspond à l'état local d'un composant. Il est lié au composant.
setState() planifie la mise à jour de l'objet state du composant. Quand l'état local change, le composant répond en se rafraîchissant.

## Props

props est une propriété passé au composant comme les arguments d'une fonction. C'est une information qui vient de l'extérieur du composant, généralement un parent direct (pas toujours).

## Redux

Redux est une bibliothèque de gestion d'état qui fournit un moyen prévisible de stocket et de mettre à jour l'état global d'une appliation.
En utilisant Redux, on va stocker toutes les données dont on a besoin dans un seul « store », qui peut être partagé entre tous les composants de l’application.

Avantages :
  - Séparation des concepts : Les composants deviennent "Stateless" car ils ne gèrent plus que l'affichage
  - État immuable : Store Redux est immuable. Il ne peut pas être modifié directement. On doit passer par des "actions" pour modifier les données.
  - Facilite la gestion des mises à jour d’état : Utilisation du mécanisme de "reducers" pour gérer les mises à jour de l'état
  - Facilite le débogage
  - Facilité de partage de l’état : En stockant l’état global de l’application dans le store Redux, il devient facile de partager l’état entre différents composants de l’application.
  - Gestion d’état centralisée : On stocke l’état global de l’application dans un seul endroit, appelé “le store”, ce qui nous permet de maintenir une vue d’ensemble de l’état de l’application. C’est plus simple à maintenir, mais aussi à faire évoluer, et le “state” est également plus facilement accessible à tous les composants.

## Les hooks

Les Hooks permettent d'utiliser l'état local (state) et les fonctionnalités du cycle de vie d'un composant de classe à l'intérieur d'un composant fonctionnel (une simple fonction JavaScript).
	- 1. Appelés uniquement au niveau racine du composant fonctionnel. 
  - 2. Appelés uniquement depuis des composants fonctionnels (ou d'autres Hooks personnalisés).

### Les Hooks de Base : L'État et les Effets Secondaires

#### useState

Rôle : Permet d'ajouter une variable d'état à un composant fonctionnel.

Syntaxe : const [valeur, setValeur] = useState(valeurInitiale);

Mécanisme : Contrairement à la modification directe d'un champ dans une classe, setValeur déclenche un re-rendu du composant et met à jour la valeur. C'est le point de départ de la réactivité de React.

Parallèle Senior : C'est la façon la plus simple de gérer l'état transitoire (l'équivalent d'une variable de portée locale pour un service Spring, mais au niveau de l'UI).

#### useEffect

Rôle : Gère tout ce qui est considéré comme un effet secondaire après le rendu (appels API, manipulation du DOM, abonnements, timers). Il remplace les trois méthodes principales du cycle de vie des classes (componentDidMount, componentDidUpdate, componentWillUnmount).

Syntaxe : useEffect(() => { /* code à exécuter */ }, [dépendances]);

### Les hooks pour l'architecture globale

#### useContext (Gestion de l'État Simple Global)

Rôle : Permet à un composant de s'abonner à un Contexte (un "canal" de données global) sans avoir à passer les props à chaque niveau de l'arbre (le fameux Prop Drilling).

Impact : Souvent suffisant pour remplacer Redux sur des applications de taille moyenne, ou pour gérer des thèmes, des préférences utilisateur, ou des données d'authentification.

🥶 Le Piège de la Valeur Périmée (Stale Closure)
Si vous oubliez d'inclure une variable d'état (par exemple, count) dans le tableau de dépendances, la fonction useCallback capture la valeur de count qui existait au moment du premier rendu.

Rendu Initial : count vaut 0. La fonction est créée et mémorise que count vaut 0.

Rendu 2 : L'utilisateur clique. count passe à 1. Le composant parent se rend.

useCallback : Le tableau de dépendances n'a pas changé, donc la fonction n'est pas recréée.

Le Bug : Lorsque la fonction mémorisée est appelée, elle utilise la valeur capturée (count: 0), et non la nouvelle valeur (count: 1). Le calcul est faux.

#### useReducer (Gestion d'État Local Complexe)

Rôle : Alternative à useState pour la gestion d'un état local dont les mises à jour dépendent d'un état ou d'une logique complexe (ex: un panier d'achat).

Mécanisme : Il utilise le pattern Action/Reducer de Redux, mais de manière locale au composant.

### Les Hooks d'Optimisation

#### useMemo

Mémorise une valeur calculée (le résultat d'une fonction) pour ne la recalculer que si ses dépendances changent.
il vérifie si les props du composant enfant ont changé pour décider s'il doit refaire le rendu ou non.

#### useCallback

Mémorise une fonction elle-même pour qu'elle ne soit pas recréée à chaque rendu.

#### useRef

Permet de conserver une valeur mutable qui ne déclenche pas de re-rendu lorsque vous la modifiez (pour accéder directement à un élément du DOM ou stocker une référence persistante).
