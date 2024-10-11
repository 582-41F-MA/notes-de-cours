# Types génériques

Un type générique représente un type indéterminé. Au contraire de `any`
qui désactive le vérificateur de type pour une valeur, un type générique
permet de conserver le type original, même si celui-ci est inconnu au
moment d'écrire le code.

Considérons une fonction nommée `echo` qui retourne simplement
l'argument sur lequel elle est appliquée. Précédemment, nous avons
utilisé `any` pour définir la signature d'une telle fonction.

```ts
function echo(arg: any): any { return arg; }
```

Quoique la fonction `echo` telle que définie ci-dessus retourne bel et
bien l'argument donné, elle a aussi comme effet d'*effacer* le type de
celui-ci. Toute valeur retournée par `echo` aura le type `any`. Nous
perdrons donc la validation de type pour celle-ci.

```ts
let foo = 1;         // type de foo : number
let bar = echo(foo); // type de bar : any
bar.toUppperCase();  // aucune erreur TypeScript
```

Si le vérificateur de type savait le type de `bar`, il pourrait nous
avertir que `toUpperCase` n'est pas une propriété accessible sur un
nombre. Mais comme son type est `any`, l'erreur apparaîtra seulement au
moment d'exécuter le code.

Réécrivons la fonction `echo` de sorte à utiliser un type générique.

```ts
function echo<T>(arg: T): T { return arg; }
```

L'annotation `<T>` représente ci-dessus une *variable de type*. Une
variable de type est similaire à un paramètre, mais pour un type : elle
permet d'abstraire le type de `arg` au sein de la fonction. De la même
façon qu'on ne connaît pas la valeur de `arg` au moment de concevoir la
fonction, on ne connaît pas le type de `T`. De la même façon qu'on
donnera une valeur à `arg` au moment d'appeler la fonction, on donnera
le type de `T`.

```ts
let foo = 1;                 // type de foo : number
let bar = echo<number>(foo); // type de bar : number
bar.toUpperCase();           // error: Property 'toUpperCase' does not exist on type 'number'
```

## Interfaces génériques

Il est également possible d'utiliser les types génériques avec les
objets. Ceci est particulièrement utile avec les types qui se comportent
comme des *conteneurs*.

Considérons par exemple un objet qui représente une paire de valeur de
même type. Puisque nous ne savons pas le type des valeurs au moment de
concevoir l'objet, on devra utiliser une variable de type.

```ts
type pair<T> = { first: T, second: T };
```

Ce type générique nous permettra notamment d'écrire une fonction qui
pourra être appliquée sur une paire de chaînes.

```ts
function printPair(p: pair<string>): string {
    return `First: ${p.first}, Second: ${p.second}`;
}
```

Ou encore sur une paire de valeurs de type indéterminé.

```ts
function echoPair<T>(p: pair<T>): pair<T> {
    return p;
}
```

Notez que ce genre de gymnastique de types n'est généralement pas
nécessaire. Il souvent préférable d'utiliser la simple composition pour
la majorité des problèmes. Cela dit, certains types d'objets natifs sont
génériques. C'est la cas des promesses, lesquelles sont une sorte de
conteneur pour une valeur dont nous ne connaissons par le type à
l'avance.

```ts
function newFakePromise(): Promise<string> {
    return new Promise((resolve) => {
        resolve("Tada!");
    });
}

const p = newFakePromise(); // type de p : Promise<string>
```

Pareillement, le type de retour de la fonction native `fetch` est
`Promise<Response>` puisque `fetch` retourne une promesse qui se résout
en un objet de type `Response`.
