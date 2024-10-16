# Structures de données persistante

En JavaScript, comme dans la majorité des langages de programmation, les
types primitifs sont tous *immuables*. C'est-à-dire qu'une valeur de
type `number`, `string` ou `boolean` ne peut pas éprouver de changement.
Le nombre `1`, par exemple, ne peut pas être transformé en le nombre
`2`. Ces deux nombres sont des nombres différents, et aucune opération
ne peut transformer un en l'autre. Pareillement, il est impossible de
changer la chaîne de caractères `"abc"` en `"abcdef"`. Certes, on peut
concaténer `"abc"` et `"def"`, mais le résultat sera une troisième
chaîne, et non une version mise à jour des chaînes initiales.

Il en est autrement des objets (et des tableaux, qui sont un type
spécial d'objet). Un objet est, par défaut, *muable*. C'est-à-dire que
JavaScript permet de changer les propriétés d'un objet après qu'il aille
été créé. On peut ainsi transformer sans problème `{ n: 1 }` en `{ n: 2
}`. La valeur de `n` aura changée, mais l'interpréteur considéra tout de
même ces deux « versions » comme étant un seul et même objet.

Jumelé au fait que les objets soient affectés par *référence* (et non
par *copie*, comme pour les valeurs primitives), cette mutabilité peut
rendre un programme complexe difficile à comprendre. Si n'importe quelle
partie du code source ayant accès à un objet peut modifier celui-ci,
alors il devient ardu de retracer l'état du programme.

Pour cette raison, certains langages de programmation (majoritairement
ceux appartenant à la famille dite « fonctionnelle ») ne possèdent
aucune structure de données muable. C'est le cas de Haskell, par
exemple, ou Elixir. Ces langages utilisent des *structures de données
persistantes* qui, lorsque « modifiées », préservent leurs versions
antérieures. Autrement dit, une opération sur une structure de données
persistantes ne modifie pas celle-ci *en place* (comme c'est le cas par
défaut pour les objets en JavaScript), mais renvoie plutôt une nouvelle
structure. 

Le système de gestion de version Git est un bon exemple d'un programme
basé sur les structures de données persistantes. Dans le modèle de
données de Git, un fichier est représenté par une structure nommée 
« blob ». Un blob est immuable. À chaque fois qu'un fichier est
modifié, un nouveau blob est créé, ce qui permet de sauvegarder les
différentes versions du fichier. Il en va de même pour les répertoires
(ou « arbres ») ainsi que les *commits*, qui représente un instantané de
l'état du dépôt à un moment donné.

## Implémentation simple

Implémenter une structure de données persistante en JavaScript est assez
simple. Par exemple, un type d'objet peut être conçu de sorte à ce qu'il
soit immuable. Il suffit de s'assurer que ses propriétés soient privées,
et que ses méthodes retournent toujours une nouvelle version de l'objet.

Considérons l'exemple d'un compte en banque :

```ts
class Account {
    private balance: number;

    constructor(balance = 0) {
        this.balance = balance;
    }

    deposit(amount: number): Account {
        return new Account(this.balance + amount);
    }
}
```

Comme vous pouvez voir, la méthode `deposit` ne modifie pas la balance
de l'instance. Plutôt, une nouvelle « copie » est créée avec la nouvelle
valeur de `balance`.
