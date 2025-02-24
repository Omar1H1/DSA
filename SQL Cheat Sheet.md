

- Q :  Qu'est-ce qu'une base de données relationnelle ?
- R : C'est une base de données qui organise les informations dans une ou plusieurs tables.

- Q : Qu'est-ce qu'une table ?
- R : C'est une collection des données organisés dans des lignes et colonnes

- Q : Qu'est-ce qu'un 'statement' ?
-  R : c'est des mots clés que la base de données reconnaît comme des instructions valides, par exemple :
- `CREATE TABLE` c'est pour créé une nouvelle table
- `INSERT INTO` c'est pour ajouter une ligne dans table
> [!note]
>Pour que `INSERT INTO X_NAME` fonctionne, il faut que la table soit déjà créée par `CREATE TABLE X_NAME`. 

- `SELECT` c'est pour demander des données spécifique à partir de notre table
- `ALTER TABLE` changer `mettre à jour la forme` de table
- `UPDATE` mettre à jour une ligne dans la table

> [!important]
>`ALTER TABLE` et `UPDATE` se ressemblent, mais ils accomplissent deux tâches distinctes.
> `ALTER TABLE` en SQL est principalement utilisé pour modifier, éditer ou mettre à jour les caractéristiques d'une **table**. 
> `UPDATE`, en revanche, est utilisé pour mettre à jour les données des lignes dans une table. Conclusion : `ALTER` opère au niveau de la table, tandis que `UPDATE` opère au niveau des lignes dans la table.

- `DELETE FROM` c'est pour supprimer des lignes dans le table

>[!note]
> `DELETE FROM` doit être associé à une **clause** comme `WHERE` qui précise quel information à  supprimer.
> ex : `DELETE FROM table_x WHERE id = 1`

**Avant le** `DELETE FROM` 

| id  | prenom | nom    |     |
| --- | ------ | ------ | --- |
| 1   | Max    | Planck |     |
| 2   | Marie  | Curie  |     |

**Apres le** `DELETE FROM`


| id  | prenom | nom   |
| --- | ------ | ----- |
| 2   | Marie  | Curie |
