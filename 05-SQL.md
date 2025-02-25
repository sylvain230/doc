
### Généralités

## SQL

C'est un langage de programmation pour effectuer des tâches sur des données.

## SGBD

- Il s'agit d'un système de gestion de base de données, un logiciel utilisé pour effectuer diverses opérations sur les données stockées dans une base de données, telles que l'accès, la mise à jour, la manipulation, l'insertion et la suppression de données. Il existe différents types de SGBD, tels que les SGBD relationnels.
- Ces types sont basés sur la manière dont les données sont organisées, structurées et stockées dans le système.

## SGBDR

C'est un système de gestion de base de données relationnelles
C'est utilisé pour stocker les données dans une ou des tables relationnelles avec des lignes et des colonnes.

## Principaux SGBDR

- Oracle
- mySQL
- Microsoft SQL
- postgreSQL

## Quels sont les types de requêtes ACTION les plus importants ?

- UPDATE permet de modifier les valeurs des champs d’une table
- DELETE permet de supprimer des enregistrements dans une table
- CREATE TABLE permet de créer une nouvelle table
- INSERT INTO permet d’ajouter des enregistrements dans une table

## Qu’est-ce qu’une clause JOIN ?

La clause JOIN combine les colonnes d’au moins deux tables avec des valeurs associées pour créer une nouvelle table.

##  À quoi servent les index ?

Un index SQL stocke des sections importantes d’une table de base de données pour permettre une recherche rapide et efficace. 
Plutôt que d’effectuer une recherche dans toute la base de data, les utilisateurs n’ont qu’à consulter l’index lors de la récupération des data. 
Les index contribuent donc à améliorer les performances d’un SGBDR.

##  Comment créer un index avec SQL ?

La syntaxe de création d’un index peut varier en fonction du SGBDR. 
Dans la plupart des systèmes, l’instruction CREATE INDEX est utilisée pour lancer le processus. 
L’utilisateur est ensuite invité à attribuer un nom à l’index et à sélectionner les colonnes qui le constitueront.

## Qu'est-ce qu'une contrainte et pourquoi l'utiliser ?

Ensemble de conditions définissant le type de données pouvant être introduites dans chaque colonne d'un tableau.
Les contraintes garantissent l'intégrité des données dans un tableau et bloquent les actions indésirables.

## Quelles contraintes SQL connaissez-vous ?

- DEFAULT - fournit une valeur par défaut pour une colonne.
- UNIQUE - n'autorise que des valeurs uniques.
- NOT NULL - n'autorise que les valeurs non nulles.
- PRIMARY KEY - n'autorise que des valeurs uniques et strictement non nulles (NOT NULL et UNIQUE).
- FOREIGN KEY - fournit des clés partagées entre deux tableaux ou plus.

## Comment supprimer un enregistrement d'un tableau ?

DELETE FROM table_name
WHERE condition;

## Comment ajouter une colonne à un tableau ?

ALTER TABLE table_name
ADD column_name datatype;

## Comment renommer une colonne d'un tableau ?

ALTER TABLE table_name
RENAME COLUMN old_column_name TO new_column_name;

## Comment supprimer une colonne d'un tableau ?

ALTER TABLE table_name
DROP COLUMN column_name;
