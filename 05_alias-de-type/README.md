# Alias de type

Un *alias* est un nom alternatif donné à un type. Un alias ne crée pas
un nouveau type de valeur comme le fait une classe ; il permet seulement
de référer à un type sous un autre nom. En ce sens, c'est surtout un
outil de documentation.

Considérons une fonction qui permet de déposer un montant d'argent dans
un compte en banque. Un montant est une information qui peut être
représentée de différentes façons : en dollar canadien, en euros, en
yen, en cents, etc. Techniquement, toutes ces valeurs seront de type
`number`. Un alias permettrait de documenter avec laquelle de ces
représentations notre fonction travaille.

Pour définir un nouvel alias, on utilise le mot-clé `type` suivi du nom
de l'alias puis du type.

```ts
type cents = number;
```

Une fois défini, l'alias peut être utilisé à la place des types natifs.

```ts
function deposit(amount: cents): void { ... }
```

Bien sûr, TypeScript ne sait pas faire la différence entre des cents et
des dollars. Rien ne vous empêchera donc d'appliquer la fonction sur un
nombre qui représente des dollars. Mais l'annotation permet ici
d'informer ceux et celles qui utiliseront la fonction.

## Types d'objet

Les alias peuvent être autant utilisés avec les primitifs (chaînes,
booléens, etc.) que les objets. Ceci permet d'alléger quelque peu la
signature des fonctions lorsque celles-ci manipulent des objets
complexes.

Un alias pour un objet est défini de la même manière que pour un
primitif. La structure de l'objet sera décrite en utilisant la syntaxe
pour les objets littéraux, à la différence que les propriétés peuvent
être séparées soit par des virgules soit par des points-vigules.

```ts
type account = { 
    name: string, 
    balance: number,
    deposit: (amount: cents) => cents,
    withdraw: (amount: cents) => cents,
};
```

TypeScript est un système de typage *structurel* ; c'est-à-dire que le
vérificateur de type s'attarde à la structure des objets, et non à au
nom de l'alias. N'importe quel objet ayant les mêmes propriétés que
`account` satisfera l'interface de `account`, et pourra donc être
utilisé comme tel.
