

- Q1 :  Qu'est-ce qu'une base de données relationnelle ?
- R : C'est une base de données qui organise les informations dans une ou plusieurs tables.

- Q2 : Qu'est-ce qu'une table ?
- R : C'est une collection des données organisés dans des lignes et colonnes

-  Q3  : Qu'est-ce qu'un 'statement' ?
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

-  Q4 : Dans le `SELECT * FROM table_x` le _*_ correspond à quoi ?
-  R : L'astérisque * représente un `wildcard` qui signifie _je veux toutes les colonnes de table_x_ .

-  Q5 : et si on veut pas utiliser * ?
-  R :  On peut préciser les colonnes qu'on veut récupérer par ex:
```sql
SELECT id, nom
FROM table_x;
```


| id  | nom   |
| --- | ----- |
| 2   | Curie |

**Ici on a récupérer les deux colonnes id et nom, et on a ignorer le colonnes prenom** 


- Q6 : Que signifie le mot-clé `AS` ?
-  R : Le mot-clé `AS` permet de créer un alias pour une colonne ou une table dans une requête SQL

>[!caution]
>Cet alias est temporaire et n'affecte que le résultat de la requête. Il ne modifie pas la structure de la table, contrairement aux commandes `ALTER` ou `UPDATE`, qui apportent des changements permanents à la base de données

Ex :
```sql
SELECT nom AS 'last name'
FROM table_x;
```

**On aura ce retour :**

| id  | prenom | last name |
| --- | ------ | --------- |
| 2   | Marie  | Curie     |

**On pourra bien faire une deuxième requête à la suite : **

```sql
SELECT nom
FROM table_x;
```



| id  | prenom | nom   |
| --- | ------ | ----- |
| 2   | Marie  | Curie |
|     |        |       |
|     |        |       |

Donc, ici, on voit bien que le 'changement' est vraiment temporaire et lié à la requête. Le mot-clé `AS` ne modifie pas l'état de la table ni des lignes.

- Q7 :  Que signifie le mot-clé `Distinct` ?
- R : Il renvoie les valeurs uniques dans une colonne donnée.

Prenons un exemple pour bien illustré :

```sql
SELECT tools 
FROM inventory;
```

cette requête renvoie :

| tools  |
| ------ |
| Hammer |
| Nails  |
| Nails  |
| Nails  |

En ajoutant le mot-clé `DISTANCT` :

| tools  |
| ------ |
| Hammer |
| Nails  |

-  Q 8 : Que signifie le mot-clé `LIKE` ?
-  R : Il permet de faire du 'pattern matching'.

Example :

| id  | name           | genre  | year | imdb_rating |
| --- | -------------- | ------ | ---- | ----------- |
| 1   | Avatar         | action | 2009 | 7.9         |
| 2   | Jurassic World | action | 2015 | 7.3         |
| 3   | Se7en          | drama  | 1995 | 8.6         |
| 4   | The Avengers   | action | 2012 | 8.1         |
| 5   | Seven          | drama  | 1979 | 6.1         |


Ici, nous avons deux films : `Seven` de Andy Sidaris  et `Se7en` de David Fincher. On remarque qu'il n'y a qu'un seul caractère de différence entre les deux noms. Peut-on trouver les films qui commencent par `Se` et se terminent par `en`, avec un seul caractère entre les deux ?



```sql
SELECT * 
FROM movies
WHERE name LIKE 'Se_en';
```



Dans cette requête, le caractère _ est utilisé comme un `wildcard`. En français, on peut dire : "Trouve-moi le film dont le nom correspond à ces critères :

1- Commence par `Se`
2- Se termine par `en`
3- Entre les deux, il peut y avoir n'importe quel caractère, chiffre ou symbole, etc."

- Q10 : C'est très intéressant d'utiliser `LIKE`, mais que faire si l'on veut chercher un pattern ? Par exemple, comment trouver un film dont le nom commence par la lettre A, sans savoir combien de lettres suivent ? on va pas faire `WHERE name LIKE 'A___________'` non ?
- R : Pour cela, on peut utiliser le caractère `%` comme un `wildcard` qui représente zéro ou plusieurs caractères. Voici comment formuler la requête :


```sql
SELECT *
FROM movies
WHERE name LIKE 'A%';
```

Dans cette requête, le `%` indique que, après la lettre _A_, il peut y avoir n'importe quel nombre de caractères (y compris aucun). Cela permet de trouver tous les films dont le nom commence par _A_, quelle que soit la longueur du titre.

```sql
// Qui termine par 'a'
SELECT *
FROM movies
WHERE name LIKE '%a';
```

```sql
// Qui ont les trois caractères 'man' dans le centre de mot 
SELECT * 
FROM movies 
WHERE name LIKE '%man%';
```



> [!TIP]
> `LIKE` n'est pas sensible à la casse, on aura `Batman` et `Man of Steel` les deux sont valides




> [!question] Combien de wildcards avons-nous vus jusqu'à présent ?
> > [!todo] Jusqu'à présent, nous avons vu deux* types de `wildcards` dans SQL.
> > > [!wildcards]  
> > > 1. Le caractère `_`, qui représente un seul caractère. 
> > > 2. Le caractère `%`, qui représente zéro ou plusieurs caractères.
> > > 3. _Le caractère `*` n'est pas utilisé dans SQL pour le `pattern matching`, mais il est souvent utilisé dans d'autres contextes pour représenter zéro ou plusieurs caractères_







 
