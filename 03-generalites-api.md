# API

## Verbes HTTP

- GET pour consulter des données
- POST pour créer des données
- PUT pour mettre à jour des données
- PATCH pour mettre à jour partiellement des données
- DELETE pour supprimer des données
- HEAD, CONNECT, OPTION, TRACE, PATCH

## Codes retours

- 200 Ok. Le serveur a traité la requête avec succès.
- 201 Created. Une nouvelle ressource a été créée.
- 204 No Content. Peut être utilisée en réponse à une reqête DELETE effectuée avec succès
- 206 Partial Content. En réponse à une requête demandant une réponse trop lourde pour être envoyée en une seule fois. De la pagination va être nécessaire pour récupérer l'ensemble des informations.
- 304 Not Modified. Le client peut utiliser les données en cache car elles n'ont pas été modifiées depuis la date spécifiée.
- 400 Bad Request. La requête est invalide et ne peut pas être traitée par le serveur.
- 401 Unauthorized. L'utilisateur doit s'authentifier.
- 403 Forbidden. L'utilisateur n'est pas autorisé à accéder à cette ressource.
- 404 Not found. La ressource demandée n'existe pas.
- 500 Internal Server Error. Erreur non gérée

## 400 vs 500

- Les erreurs 4XX ont lieu lorsque l'appel à un serveur a échoué.
- Les erreurs 5XX ont lieu lorsqu'il y a une erreur interne au serveur.
