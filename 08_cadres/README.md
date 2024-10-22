# Cadres d'applications et cadriciels

Dans le contexte du web, il n'y a pas de définition universellement
acceptée des termes « cadre » ou « cadriciel » (*framework*, en
anglais).

Selon l'Office québécois de la langue française, le mot « cadre
d'applications » désigne une « infrastructure logicielle permettant la
conception de programmes ». La définition note également que les cadres
sont fondés sur la réutilisation des étapes de conception. On mettra
l'emphase ici sur le terme « infrastructure » qui désigne un support ou
une base indispensable à l'édification, au maintien ou au fonctionnement
d'une structure.

De la même manière, un cadriciel web est un ensemble de code externe
dont l'interface dicte la structure globale d'un projet. Il offre une
approche standardisée (un genre de squelette) pour construire et
déployer les applications web, et automatise certaines tâches courantes
telles que la gestion de bases de données, l'interprétation des
gabarits, l'authentification, etc. Les cadriciels populaires incluent
Django, Laravel, Ruby on Rails, Next, etc.

En théorie, un cadre d'applications diffère d'une bibliothèque de code
externe en ce que cette dernière ne dicte pas de manière significative
la structure globale d'un projet. Les bibliothèques sont des modules
utilisés ici et là, facilement remplaçables sans avoir à changer le
reste du code source. Pour citer [Alexander Petros][] : 

> A library is a cog that you add to your machine, a framework is a
> pre-built machine that you control by customizing its cogs. 

[Alexander Petros]:
https://htmx.org/essays/is-htmx-another-javascript-framework/

En pratique, la distinction entre les deux est plus ambiguë. Il n'existe
pas de règle stricte qui détermine à quel moment une bibliothèque
devient un cadre d'applications, et vice versa. De nombreuses
bibliothèques au sens défini ci-dessus (React, Flask ou HTMX), se
qualifient souvent elles-mêmes de cadriciel.

## Un mot de précaution

Utiliser une bibliothèque ou un cadre d'application implique une
certaine abstraction. En utilisant des interfaces tierces, et non les
interfaces natives de votre langage ou de votre plateforme, vous
programmez inévitablement à un niveau d'abstraction supérieur. Vous
travaillerez plus vite, certes, mais au dépend de code que vous n'avez
pas écris vous-même, et que vous ne comprenez pas complètement.

Ce compromis est un choix à faire avec soins. Un cadriciel utilisera des
conventions et des concepts que vous devrez apprendre, mais que vous ne
pourrez pas appliquer ailleurs. Il vous libérera de l'obligation de
prendre nombreuses décisions, mais il limitera aussi votre flexibilité.
Si le cadre choisi est populaire, il aura une communauté d'experts
prêt·es a vous aider, mais il rendra aussi plus complexe le déboguage.

Être un ou une bonne programmeuse web implique de savoir quand ce
compromis vaut le peine, et quand il n'en vaut pas.
