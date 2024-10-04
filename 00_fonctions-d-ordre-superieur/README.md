# Les fonctions d'ordre supérieur

Les fonctions d'ordre supérieur sont des fonctions qui opèrent sur
d'autres fonctions, soit en prenant celles-ci comme argument, soit en
retournant celles-ci comme valeur de retour. 

## Définition versus application

Pour comprendre les fonctions d'ordre supérieur, il faut d'abord
comprendre la différence entre *définir* une fonction, et *appeler* ou
*appliquer* celle-ci. Dans les langages de programmation ayant des
fonctions de première classe, la définition d'une fonction est une
*expression*.

Considérons l'exemple suivant (à moins d'avis contraire, tout le code
ci-dessous est en JavaScript) :

```js
const add = function (n, m) { return n + m; };
```

L'expression `function(n, m) { return n + m; }` a une valeur qui
correspond à la définition de la fonction. Puisque cette définition est
une expression, on peut l'affecter à une variable, de la même façon que
l'on affecte `true` ou `"bar"`.

L'exemple ci-dessus est d'ailleurs équivalent au code suivant :

```js
function add(n, m) { return n + m; }
```

Dans les deux cas, la fonction est affectée à l'identifiant `add`. On
peut donc appliquer la fonction à des arguments en plaçant ceux-ci entre
parenthèses.

```js
add(1, 2);
```

Mais on peut aussi faire référence à la fonction elle-même, par exemple,
en l'affichant dans la console.

```js
console.log(add); // => [Function: add]
```

Vous remarquerez que la valeur de l'expression `add(1, 2)` est le nombre
`3`, alors que celle de l'expression `add` est une *référence* à la
fonction.

## Les fonctions de rappel

Puisque, dans les langages de programmation ayant des fonctions de
première classe, les fonctions sont des expressions, on peut traiter
celles-ci comme n'importe quelle autre valeur. Ainsi, en plus de pouvoir
être affectée à un identifiant, une fonction peut être utilisée comme
argument. On appelle parfois ce genre de fonction des « fonctions de
rappel » (ou *callback fonction* en anglais).

Considérons la fonction JavaScript suivante, laquelle répète un nombre
de fois donné une action donnée :

```js
function repeat(times, action) { 
    for (; times > 0; times--) action();
}
```

Comme vous voyez, le paramètre `times` est un nombre, alors que `action`
correspond à une fonction. De cette façon, on peut appeler la fonction
`action` à chaque boucle, sans connaître d'avance à quelle procédure
elle correspond. 

```js
repeat(3, function () { console.log("foo"); }); // => foo foo foo
```

Une fonction de rappel peut également définir un ou plusieurs
paramètres, la valeur desquels sera passée à la fonction de rappel
lorsque celle-ci sera appelée par la fonction d'ordre supérieur.

```js
function greet_french(name) { return `Bonjour ${name} !`; }
function greet_english(name) { return `Hi ${name}!`; }

function processInput(callback) {
    const name = "Ye";
    const greeting = callback(name);
    console.log(greeting);
}

processInput(greet_french);  // => Bonjour Ye !
processInput(greet_english); // => Hi Ye!
```

## Les fermetures

Une fermeture (*closure*, en anglais) est la paire formée d'une fonction
et des références à son état environnant. En JavaScript, toutes les
fonctions forment des fermetures puisque toutes les fonctions ont accès,
au moment de leur définition, à la portée environnante.

```js
let balance = 100;

function deposit(amount) { balance = balance + amount; }

deposit(50);
console.log(balance); // => 150;
```

Considérons l'exemple ci-dessus. Comme vous pouvez voir, la variable
`balance` est accessible dans le corps de la fonction `deposit` . Au
moment d'appeler `deposit`, l'interpréteur JavaScript doit donc non
seulement avoir en mémoire le corps de la fonction, mais également les
affectations définies dans son environnement.

### Les variables d'état locales

Ce phénomène est particulièrement intéressant lorsqu'une fonction est
définie à l'intérieur d'une autre fonction.

```js
function newDeposit(balance) {
    return function (amount) { return balance += amount; };
}
```

La fonction `newDeposit`, par exemple, retourne comme valeur une
fonction anonyme. Comme cette dernière est définie à l'intérieur de la
fonction `newDeposit`, elle forme une fermeture avec la portée
environnante, laquelle inclus `balance`. C'est pourquoi on peut accéder
à `balance` à l'intérieur de la fonction anonyme.

Plus intéressant encore, puisque la fonction anonyme forme une
fermeture, l'interpréteur doit garder en mémoire la valeur de `balance`.
Et donc, chaque fois que la fonction `deposit` est appelée, la valeur de
`balance` est mise à jour.

```js
const deposit = newDeposit(100);
console.log(deposit(25)); // => 125
console.log(deposit(50)); // => 175
```

Ci-dessus, la fermeture permet d'établir un environnement privé où la
variable locale `balance` est gardée en mémoire entre chaque appel de
`deposit`.

De plus, puisque la variable est locale à `newDeposit`, chaque appel de
`newDeposit` permet de créer des balances parallèles et indépendantes
les unes des autres.

```js
const deposit1 = newDeposit(0);
const deposit2 = newDeposit(100);
console.log(deposit1(50)); // => 50
console.log(deposit2(50))  // => 150
```

### L'injection de dépendances

Outre permettre de créer des variables d'état locales, les fermetures
permettent aussi de passer des arguments à des fonctions de rappel. On
nomme se mécanisme « injection de dépendances » car il permet
d'abstraire les ressources ou les valeurs sur lesquelles dépendent une
fonction. L'écouteur d'évènements donné à la méthode `addEventListener`,
par exemple, accepte seulement un argument: un object de type `Event`.

```js
function handleClick(event) { alert("Allô"); }
document.addEventListener("click", handleClick);
```

Pour passer d'autres arguments à la fonction `handleClick`, on peut
toutefois définir l'écouteur d'évènements à l'intérieur d'une autre
fonction, laquelle recevra lesdits arguments.

```js
function handleClick(name) { 
    return function (event) { alert(`Allô ${name}`); };
}
document.addEventListener("click", handleClick("Gollum"));
```

