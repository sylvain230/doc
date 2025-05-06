# vue.js

## Généralités

### Différence entre Vue.js et d'autres frameworks

Vue.js est un framework JavaScript progressif qui se concentre sur la construction d'interfaces utilisateur. 
Contrairement à React, qui est une bibliothèque, Vue.js est un framework complet avec des outils intégrés pour le routage et la gestion de l'état. 
Par rapport à Angular, Vue.js est plus léger et plus facile à apprendre, tout en offrant une grande flexibilité.

### Cycle de vie des composants

Le cycle de vie d'un composant Vue.js comprend plusieurs étapes, telles que created, mounted, updated, et destroyed. 
Ces hooks permettent d'exécuter du code à des moments spécifiques du cycle de vie du composant.

### Directives

#### principales

 v-bind lie des attributs ou des classes à des expressions dynamiques. v-model crée une liaison bidirectionnelle sur les éléments de formulaire. 
 v-for est utilisé pour rendre une liste d'éléments en itérant sur une collection. v-if conditionne le rendu d'un élément basé sur une expression.

#### différence entre v-if et v-show

v-if ajoute ou supprime des éléments du DOM en fonction de la condition, 
tandis que v-show utilise le style CSS display pour afficher ou masquer les éléments sans les supprimer du DOM.

### Les composants

#### Création/Réutilisabilité

Les composants Vue.js sont créés en utilisant la méthode Vue.component ou en définissant des composants locaux dans l'option components d'une instance Vue. 
Ils peuvent être réutilisés en les incluant dans les templates d'autres composants.

#### Communication entre composants

Les props permettent de passer des données des composants parents aux composants enfants. 
Les événements personnalisés ($emit) permettent aux composants enfants de communiquer avec les composants parents.

### Routage

#### Conf. du routage

Vue Router est utilisé pour configurer le routage dans une application Vue.js. Les routes sont définies dans un fichier de configuration et associées à des composants.

#### routes dynamiques vs statiques

Les routes dynamiques utilisent des paramètres pour rendre des composants en fonction de l'URL, tandis que les routes statiques sont définies avec des chemins fixes.

### Gestion de l'état avec Vuex

Vuex est une bibliothèque de gestion de l'état pour Vue.js. 
Elle utilise un store centralisé pour gérer l'état de l'application. 
Les state contiennent les données, les getters sont des fonctions pour accéder aux données, les mutations modifient l'état, et les actions sont des fonctions asynchrones qui peuvent déclencher des mutations.

### Concepts de Vuex

state pour les données, getters pour accéder aux données, mutations pour modifier l'état, et actions pour les opérations asynchrones.

#### Optimisation et performance

### Bonnes pratiques
Utiliser des composants fonctionnels pour les composants stateless, éviter les rendus inutiles avec v-once, et utiliser des techniques de lazy loading pour charger les composants à la demande.

### Slots et mixins

Les slots permettent de passer du contenu dynamique aux composants enfants, tandis que les mixins permettent de réutiliser des morceaux de logique dans plusieurs composants.

### Intégration avec des APIs

#### Intégration des APIs

Utiliser des bibliothèques comme Axios ou Fetch pour faire des appels API. Les appels API sont généralement effectués dans les méthodes ou les actions Vuex.

#### Gestion des appels synchrones

Utiliser async/await pour gérer les appels API asynchrones et gérer les erreurs avec des blocs try/catch.

### Exemple de code

```
<!-- Template du composant -->
<template>
  <div>
    <h1>Liste de tâches</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id">{{ task.text }}</li>
    </ul>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Ajouter une nouvelle tâche" />
    <button @click="addTask">Ajouter</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { id: 1, text: 'Apprendre Vue.js' },
        { id: 2, text: 'Construire une application' }
      ],
      newTask: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ id: this.tasks.length + 1, text: this.newTask });
        this.newTask = '';
      }
    }
  }
};
</script>

<style scoped>
/* Styles du composant */
h1 {
  font-size: 24px;
  margin-bottom: 10px;
}
input {
  margin-right: 10px;
}
button {
  padding: 5px 10px;
}
</style>

