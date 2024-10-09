# Annotations de type

À première vue, la plus grande différence entre un programme JavaScript
et son équivalent TypeScript est l'annotation de type. En TypeScript, la
signature d'une fonction doit inclure le type de ses paramètres ainsi
que le type de sa valeur de retour.

```ts
function greet(name: string): string {
    return `Bonjour ${name}`;
}
```

La fonction ci-dessus, par exemple, peut être appliquée seulement sur un
argument de type `string`, et elle retournera toujours une valeur de
type `string`.

En TypeScript, ces annotations de type forment un contrat : le programme
ne s'exécutera pas si une fonction est appliquée sur un argument dont le
type ne correspond pas au type du paramètre, ou si la fonction ne
retourne pas une valeur dont le type correspond à l'annotation.

De plus, au sein de la fonction, `name` sera considéré par TypeScript
comme étant toujours une valeur de type `string`. Le vérificateur de
type s'assurera que l'argument n'est pas utilisé dans un contexte où une
valeur d'un autre type est attendu.

```ts
function greet(name: string): string {
    name.forEach(n => console.log("...")); // Property 'forEach' does not exist on type 'string'.
}
```

En JavaScript, ce genre d'erreurs apparaîtra au moment de l'exécution
(si la fonction est appliquée sur un argument du mauvais type), tandis
que TypeScript vérifiera que le type des variables est correct *avant*
l'exécution du programme.

## Variables

Quoi qu'il est possible d'ajouter des annotations de type sur les
variables, cela n'est pas nécessaire dans la majorité des cas. Si une
variable est déclarée et immédiatement affectée à une valeur, TypeScript
est capable de déduire son type à partir du type de la valeur
d'initialisation.

Ci-dessous, le type de `n` est `number` puisque `1` est de type
`number`.

```ts
const n = 1;
```

Or, si on déclare une variable sans lui affectée une valeur
immédiatement, il est impossible pour TypeScript de déduire son type. On
devra donc obligatoirement inclure une annotation de type.

```ts
let i: number;
```

## Tableaux

Outre les types de valeur atomique (`string`, `number`, `boolean`),
certains types méritent quelques précisions. C'est le cas des tableaux,
la notation pour lesquels doit inclure le type des éléments qu'il
contient.

```ts
function arraySum(a: number[]): number {
    let sum = 0;
    for (let e of a) sum += e;
    return sum;
}
```

Ainsi, la fonction ci-dessus peut être appliquée seulement sur un
tableau dont tous les éléments sont des nombres. La fonction retournera
toujours un nombre ; la somme des éléments du tableau donné.

## Objets

De la même manière, la notation pour un objet doit inclure le type de
ses propriétés.

```ts
function isAdult(person: { name: string, age: number }): boolean {
    return person.age >= 18;
}
```

La fonction ci-dessus peut être appliquée seulement sur un objet ayant
une propriété `name` dont le type est `string` et une propriété `age`
dont le type est `number`. La fonction retournera toujours un booléen.

Alternativement, si possible, on utilisera le nom de la classe à partir
de laquelle l'objet a été instancié. Étant donné une classe `Person`, la
signature de la fonction ci-dessus pourrait donc être réécrite de la
façon suivante :

```ts
function isAdult(p: Person): boolean {
    return p.age >= 18;
}
```

### Éléments HTML

Il en va de même pour les éléments HTML (lesquels sont représentés comme
des objets en JavaScript), et tout autres types d'objet natif (`Date`,
`Error`, `RegExp`, etc.).

```ts
function createList(people: Person[]): HTMLUListElement {
    const ul = document.createElement("ul");
    for (let p of people) {
        const li = document.createElement("li");
        li.textContent(`${p.name} is ${p.age} years old`);
        ul.append(li);
    }
    return ul;
}
```

La fonction ci-dessus peut être appliquée seulement sur un tableau dont
tous les éléments sont de type `Person`. La fonction retournera toujours
un nœud de type `HTMLUListElement`.

Vous trouverez sur [MDN][HTML element interfaces] une liste des types
représentant les divers éléments HTML. Quoique techniquement tous les
éléments HTML sont de type `HTMLElement`, il est important que vos
annotations soient aussi précises que possible.

[HTML element interfaces]:
    https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API#html_element_interfaces_2

## Fonctions

En JavaScript, les fonctions sont des valeurs comme les autres. Elles
peuvent être affectées à une variable, ou utilisées comme argument. Une
fonction peut même retourner une autre fonction comme valeur de retour.

Considérons une fonction `newCounter` qui doit être appliquée sur un
nombre (le compte initial), et qui retourne une fonction anonyme
permettant d'incrémenter le compteur.

```ts
function newCounter(start: number): (incr: number) => number {
    let count = start;
    return (incr) => count += incr;
}
```

Vous remarquerez que l'annotation de type pour la valeur de retour est
similaire à la syntaxe utilisée pour les fonctions fléchées. La fonction
`newCounter` retourne une fonction qui doit être appliquée sur un nombre
(`incr`), et qui retournera toujours un nombre. Les annotations de types
de la fonction anonyme sont omises dans l'instruction de retour puisque
sa signature est déjà donnée dans la signature de `newCounter`.

## Classes

TypeScript inclut quelques mots clés supplémentaires qui peuvent être
utilisés dans le contexte d'une classe. Au moment de déclarer une
propriété, par exemple, les mots clés `public`, `protected` et `private`
peuvent être utilisés pour définir la visibilité de celle-ci.

```ts
class Account {
    public name: string;

    private validate(): boolean {
        /* ... */
    }
}
```

## Assertions de type

Certaines fonctions retourne une valeur dont il est impossible pour
TypeScript de vérifier le type. C'est le cas, notamment, de
`querySelector`.

Considérons par exemple le code ci-dessous.

```ts
const node = document.querySelector("#name");
```

La valeur de la constante `node` est soit de type `Element`, soit de
type `null` (si aucun élément ne possède l'identifiant `name`). Il est
impossible de savoir lequel de ces deux type ce sera *avant* d'exécuter
le programme. Par conséquent, lorsque on utilisera `node`, notre code
devra absolument prendre en considération ces deux possibilités. Sinon,
le vérificateur de type émettra une erreur.

```ts
node.textContent = "Test"; // node is possibly null.
```

Puisque `node` est possiblement `null`, on ne peut pas accéder à la
propriété `textContent` car celle-ci n'existe pas sur les valeurs de
type `null`.

Dans cette situation, si on connait avec certitude le type de la valeur
de retour de `querySelector`, on utilisera le mot clé `as` afin
d'assurer au vérificateur que la valeur de retour est bel et bien d'un
type en particulier.

```ts
const node = document.querySelector("#name") as HTMLParagraphElement;
```

## Unions de type

Certains opérateurs propres à TypeScript permettent de créer de nouveaux
types à partir de types existant. C'est le cas de l'opérateur d'union
`|` qui permet de représenter des valeurs qui sont soit d'un type, soit
d'un autre.

Considérons par exemple la signature ci-dessous.

```ts
function printID(id: number | string): void { ... }
```

La fonction `printID` peut être appliquée sur un argument de type soit
`number` soit `string`. 

Quoique les unions de type peuvent créer des abstractions utiles, on
fera attention de ne pas en abuser. Une fonction qui s'applique sur un
seul type d'argument ou retourne un seul type de valeur est plus facile
à utiliser et à tester qu'une fonction fonction qui travaille avec des
unions de type.

## Types littéraux

En plus des types généraux `string` et `number`, on peut définir un type
comme étant une chaîne ou un nombre précis. C'est d'ailleurs ainsi que
TypeScript définit le type d'une constante.

```ts
const n = 1;
```

Ci-dessus, le type de `n` n'est techniquement pas `number`, mais plutôt
`1`. On se rappelle que le type d'une valeur représente l'ensemble des
valeurs possibles pour celle-ci. Or, puisqu'on ne peut pas réaffecter la
valeur d'une constante, `n` ne pourra jamais valoir `2` ou `3` ou
n'importe quel autre nombre. L'ensemble des valeurs possible de `n`
inclut uniquement `1`.

Par eux-mêmes, les types littéraux ne sont pas très utiles. On peut
toutefois les combiner avec l'opérateur d'union pour exprimer certaines
contraintes.

La signature suivante, par exemple, appartient à une fonction qui peut
être appliquée seulement sur les arguments `"left"`, `"right"`, et
`"center"`. Aucune autre valeur ne sera admise par le vérificateur de
type.


```ts
function printText(s: string, align: "left" | "right" | "center"): string { 
    ...
}
```

