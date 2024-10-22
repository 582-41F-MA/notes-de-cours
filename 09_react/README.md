# React

React est une bibliothèque de code externe pour créer des interfaces
utilisateurs. La bibliothèque est libre d'accès, et maintenue
principalement par Meta (anciennement Facebook).

## Installation

Techniquement, React nécessite aucune installation. On peut importer son
interface à partir d'un module JavaScript comme n'importe quel autre
module. Il est toutefois coutume d'utiliser React avec JSX (ou dans
notre cas TSX), un sur-ensemble syntaxique de JavaScript (ou TypeScript)
qui permet d'écrire du HTML directement dans nos scripts. Et comme tout
sur-ensemble syntaxique, celui-ci doit être transcompiler en JavaScript
afin que le navigateur puisse l'exécuter.

### Vite

Il existe plusieurs façon d'installer les outils nécessaires pour créer
une application React. Dans ce cours, nous utiliserons [Vite][] pour sa
simplicité et sa comptabilité avec Deno.

[Vite]: https://vite.dev

Pour créer un nouveau projet avec Vite et Deno, il suffit d'exécuter la
commande suivante dans votre terminal :

```sh
deno run -A npm:create-vite@latest --template react-ts
```

Une fois le téléchargement terminé, veuillez ignorer les instructions
qui s'affichent à l'écran, et exécuter plutôt le commande `deno
install`. Au contraire de NPM, Deno enregistre globalement les paquets
nécessaires au bon fonctionnement de React. Vous n'aurez donc pas à
télécharger ceux-ci de nouveau pour chaque projet (mais il faudra tout
de même exécuter de nouveau les commandes ci-dessus).

Pour lancer votre application, exécutez la commande `deno task dev`.

## Ressources d'apprentissage

La meilleure façon d'apprendre une bibliothèque ou un cadre
d'applications est de lire sa documentation. React ne fait pas exception
à la règle. Pour cette raison, dans les semaines à venir, nous suivrons
le tutoriel offert sur le site officiel de React. Vous trouverez
ci-dessous les chapitres à lire pour chaque cours.

### Cours 9

-   [Your First Component](https://react.dev/learn/your-first-component)
-   [Importing and Exporting Components](https://react.dev/learn/importing-and-exporting-components)
