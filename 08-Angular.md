# La base d'Angular

* Qu'est-ce qu'un Composant ?

C'est le bloc de construction fondamental d'une application Angular, gérant une partie de l'interface utilisateur. Il est composé d'une classe TypeScript, d'un template HTML et d'un style CSS.

* Quel est le rôle d'un NgModule ?

Il définit comment les parties d'une application (composants, services, directives, pipes) sont groupées et partagées. Il s'agit du mécanisme de modularité d'Angular.

* Qu'est-ce que l'Injection de Dépendances (DI) ?

Un design pattern où une classe reçoit ses dépendances (services) de sources externes plutôt que de les créer elle-même, facilitant la réutilisation et les tests unitaires.

* Expliquez le Data Binding.

C'est le mécanisme qui synchronise les données entre la classe du composant (modèle) et le template HTML (vue). Il peut être unidirectionnel (one-way) ou bidirectionnel (two-way - [(ngModel)]).

Citez les principaux Directives Structurelles.

# Intermédiaire (Composants, Services et Cycle de Vie)

* Quels sont les Hooks de cycle de vie clés ?

ngOnInit (initialisation après construction et injection des inputs), 
ngOnChanges (appelé lorsqu'une propriété @Input change) et 
ngOnDestroy (nettoyage avant la destruction du composant).

* Comment communiquer Parent ➡️ Enfant ?

Via le décorateur @Input() sur une propriété de l'enfant. Le parent lui passe une valeur dans le template.

* Comment communiquer Enfant ➡️ Parent ?

Via le décorateur @Output() et l'EventEmitter. L'enfant émet un événement que le parent écoute et gère.

* Quel est le rôle d'un Service ?

Fournir une logique et/ou des données aux composants qui en ont besoin. Ils sont généralement des singletons et sont utilisés pour les appels HTTP et la gestion d'état global.

* Différence constructor vs ngOnInit ?

Le constructor est utilisé pour l'Injection de Dépendances. ngOnInit est l'endroit privilégié pour la logique d'initialisation (appels de données, souscriptions), car les @Input sont garantis d'être disponibles à ce moment.

# Avancé (Performance, Réactivité et Architecture)

* Qu'est-ce que la détection de changement OnPush ?

C'est une stratégie de performance qui indique à Angular de ne vérifier les changements dans le composant que si ses références d'@Input changent ou si un événement est déclenché à l'intérieur de lui.

* Expliquez le Lazy Loading.

C'est une technique de routage qui consiste à charger des modules (et donc leurs composants) uniquement lorsque l'utilisateur navigue vers leur route. Cela réduit le temps de chargement initial.

* Différence Promises vs Observables (RxJS) ?

Une Promise gère une seule valeur future (mono-valeur) et n'est pas annulable. Un Observable gère un flux de valeurs multiples dans le temps, est lazy (ne s'exécute qu'à la souscription) et est annulable.

* Quelle est la différence entre les Formulaires Réactifs et Basés sur les Modèles ?

Les Formulaires Réactifs sont créés explicitement dans le code TypeScript (approche model-driven) et sont plus faciles à tester. Les Formulaires Basés sur les Modèles reposent principalement sur les directives dans le template HTML.

* Qu'est-ce que la compilation AOT ?

AOT (Ahead-Of-Time) compile le code Angular (HTML/TypeScript) en JavaScript avant que le navigateur ne le télécharge. Cela améliore les performances de rendu et la sécurité, et réduit la taille de l'application (meilleur Tree Shaking).
