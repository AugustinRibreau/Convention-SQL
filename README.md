# Convention SQL
:wave: Bienvenue sur la convention SQL. <br />
### Contexte
<b>SQL</b>, Structured Query Language est un langage informatique normalisé servant à exploiter des bases de données relationnelles. La partie langage permet de rechercher, d'ajouter, de modifier ou de supprimer des données dans les bases de données.<br />

### Bonne pratique
Voici une liste de bonnes pratiques qui s’appliquent à la fois pour le nommage des tables et des colonnes: <br />

- <b>Ne pas utiliser les mots réservés.</b><br />
  - Documentation MySQL 5.6 : <a href="http://www.htmlite.com/mysql002a.php">mots réservés</a><br />
  - Documentation PostgreSQL 9.2 : <a href="https://www.postgresql.org/docs/9.2/sql-keywords-appendix.html">mots réservés</a><br />
  - Documentation SQL Server 2000 : <a href="https://docs.microsoft.com/fr-fr/sql/t-sql/language-elements/reserved-keywords-transact-sql?view=sql-server-2017">mots réservés</a><br />
- <b>Ne pas utiliser de caractères spéciaux</b><br />
- <b>Eviter les majuscules.</b> Pour écrire 2 mots il faut privilégier l’utilisation d’un underscore. Par exemple il faut plutôt utiliser “date_inscription” que “DateInscription”<br />
- <b>Eviter l’utilisation d’abréviation.</b> A première vu c’est pratique pour faire noms de tables pas très long, mais dans la pratique un développeur ne comprendra pas facilement à quoi ça correspond et il devrait visualiser le contenu pour comprendre ce qui se cache derrière
<br />

### Noms de tables
Voici une liste de bonnes pratiques : <br />

- Utiliser un <b>nom représentatif du contenu</b>
- Utiliser <b>un seul mot</b> lorsque c’est possible
- <b>Privilégier le singulier</b> (mais c’est parfois un grand débat …)
- Penser à des <b>noms génériques</b> et envisager les futurs évolutions. Par exemple une table “client” qui pourrait aussi contenir les prospects et commerciaux devrait plutôt s’intitulé “utilisateur”
- <b>Préfixer</b> les noms des tables
    - Permet d’éviter d’utiliser accidentellement des mots réservés.
    - Permet d’éviter les conflits lorsqu’il y a plusieurs logiciels similaires sur une même base de données (par exemple, si 2 logiciels utilisent chacun une table intitulée “utilisateur”).
    - Utile pour séparer facilement les tables associée à un système ou à un autre. Par exemple si un blog WordPress et une boutique e-commerce Prestashop sont placé sur une même base de données, le blog aura des tables commençant par “wp_” tandis que la boutique aura des tables commançant par “ps_”.
    - C’est plus simple pour ré-installer un backup. Par exemple, pour réinstaller une sauvegarde du blog, il est possible d’ajouter des tables commençant par “wp2013_” puis de modifier le code de l’application pour tout migrer d’un coup.
    - Sur des gros projets ça peut être pratique pour que toutes les tables associées aux utilisateurs commence par exemple par “user_”, toutes celles concernant les produits par “product_” et ainsi de suite.
    
### Noms de colonnes
Voici la liste de bonnes pratiques :<br />

- <b>Préfixer toutes les colonnes</b> de la même façon pour chaque table. C’est beaucoup plus pratique lorsqu’il convient d’effectuer des jointures.
- Dans le cas d’un site à vocation multilingue : <b>indiquer la langue et la zone géographie</b> pour les champs alphanumériques (fr_fr pour le français de France, fr_ca pour le français du Canada, fr_be pour le français de Belgique …). C’est extrêmement pratique si un jour une application doit devenir multilingue. Si la base de données doit s’internationaliser il suffira d’ajouter une colonne supplémentaire avec les traductions.
- Lorsqu’une clé étrangère est utilisée (traduction anglaise : “Foreign Key”), il est pratique de l’indiquer dans le nom de la colonne. La colonne peut contenir le préfixe, puis “fk” pour Foreign Key, puis le nom de la table et enfin se terminer par “id”. Ainsi, une colonne pourrait s’intituler “wp_fk_user_id” (cf. préfixe “wp”, foreign key sur la table utilisateur de la colonne “id”).
- Toujours intitulé de façon similaire certains champs tels que les DATE ou DATETIME. Cela permet d’aider un développeur à savoir ce que va contenir un champ sans nécessairement regarder le contenu.

### Exemple

Imaginons les tables d’un forum. Il peut y avoir 3 tables : une pour les forums, une autre pour les questions et une dernière pour les messages. Ces tables sont liées entres elles grâce à des clé étrangères.

### Schéma
Ci-dessous il est présenté 2 façon distinctes de nommer les tables d’une telle application:<br />

<img src="https://github.com/AugustinRibreau/Convention-SQL/blob/master/sql-base-donnees-merise-forum.png" height="500vh"/><br />
Clic sur l'image pour l'agrandir.<br />
L’exemple que je recommande est l’exemple de droite. Cet exemple utilise des préfixe et respecte une bonne convention de nommage pour savoir ce que peux contenir les colonnes.<br />

### Requêtes
Voici l’exemple d’une requête avec le <b>mauvais nommage</b> :<br />
```SQL
SELECT `post`.`id` AS post_id, `post`.`contenu` AS post_contenu, `topic`.`id` AS topic_id, `topic`.`nom` AS topic_nom
FROM `post`
INNER JOIN `topic` ON `topic`.`topic_id` = `post`.`id`
```
Cette requête est un peu longue et compliquée. Il faut par exemple utiliser le nom de la table pour éviter des erreurs où SQL ne sais pas différencier quel colonne est appelée. C’est indispensable pour éviter l’erreur : “nom de colonne ambigu”.
<br /> <br />
Cette requête SQL peut être simplifiée en utilisant <b>des règles de nommages</b>:<br />
```SQL
SELECT `p_id`, `p_description_fr_fr`, `t_id`, `t_nom_fr_fr`
FROM `f_post`
INNER JOIN `f_topic` ON `t_id` = `p_fk_topic_id`
```

## Auteur
- Augustin Ribreau - <i>Developpeur</i> - <a href="https://augustin.ribreau.co/" target="_blank">augustin.ribreau.co</a>

Voir aussi la liste des <a href="https://github.com/AugustinRibreau/Convention-SQL/blob/master/source.txt" target="_blank">sources</a> ayant été utilisé.



