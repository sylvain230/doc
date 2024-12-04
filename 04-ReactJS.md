
# ReactJS

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

Composants

Les composants vous permettent de découper l'interface utilisateur en éléments indépendants et réutilisables, vous permettant ainsi de considérer chaque élément de manière isolée.

Etat

L'état d'un composant est un objet qui contient des informations qui peuvent changer au cours de la durée de vie du composant. Le point important est que chaque fois que l'objet d'état change, le composant est restitué. Il est toujours recommandé de rendre notre état aussi simple que possible et de minimiser le nombre de composants avec état.
