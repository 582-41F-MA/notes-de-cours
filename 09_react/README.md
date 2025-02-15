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

### Cours 13

-   [Reacting to Input with State](https://react.dev/learn/reacting-to-input-with-state)
-   [Choosing the State Structure](https://react.dev/learn/choosing-the-state-structure)
-   [Sharing State Between Components](https://react.dev/learn/sharing-state-between-components)
-   [Preserving and Resetting State](https://react.dev/learn/preserving-and-resetting-state)

### Cours 12

-   [State: A Component's Memory](https://react.dev/learn/state-a-components-memory)
-   [Render and Commit](https://react.dev/learn/render-and-commit)
-   [State as Snapshot](https://react.dev/learn/state-as-a-snapshot)
-   [Queueing a Series of State Updates](https://react.dev/learn/queueing-a-series-of-state-updates)
-   [Updating Objects in State](https://react.dev/learn/updating-objects-in-state)
-   [Updating Arrays in State](https://react.dev/learn/updating-arrays-in-state)

### Cours 11

-   [Responding to Events](https://react.dev/learn/responding-to-events)

### Cours 10

-   [Keeping Components Pure](https://react.dev/learn/keeping-components-pure)
-   [Understanding Your UI as a Tree](https://react.dev/learn/understanding-your-ui-as-a-tree)

### Cours 9

-   [Writing Markup with JSX](https://react.dev/learn/writing-markup-with-jsx)
-   [JavaScript in JSX with Curly Braces](https://react.dev/learn/javascript-in-jsx-with-curly-braces)
-   [Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component)
-   [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
-   [Using TypeScript](https://react.dev/learn/typescript)
-   [Conditional Rendering](https://react.dev/learn/conditional-rendering)
-   [Rendering Lists](https://react.dev/learn/rendering-lists)

### Cours 8

-   [Your First Component](https://react.dev/learn/your-first-component)
-   [Importing and Exporting Components](https://react.dev/learn/importing-and-exporting-components)
