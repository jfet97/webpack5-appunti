# Modules

La programmazione modulare consiste nel suddividere un programma in parti di dimensioni ridotte, chiamate __moduli__, ciascuna delle quali, se ben formata, provvede il giusto grado di astrazione e incapsulamento, in modo che ogni modulo abbia un design coerente e uno scopo chiaro all'interno dell'applicazione complessiva.

Node.js ha quasi subito supportato questo tipo di programmazione. Nel web, invece, il supporto per i moduli è stato lento ad arrivare.\
Esistono numerosi tools per ovviare a questo problema, e webpack ha riunito i numerosi pregi di tutti essi apllicando il concetto di modulo a qualsiasi file del nostro progetto.

## Che cosa è un modulo webpack

A differenza dei moduli di Node.js, i moduli weback possono palesare le loro dipendenze in un elevato numero di modi:

* tramite l'`import` statement di ES2015
* tramite il `require` statement del CommonJS
* tramite gli statement `define` e `require` del AMD
* tramite l'`@import` statement all'interno di un file css/sass/less
* richiamando una immagine via url nel CSS `url(...)` o nell'HTML `<img src=...>`

## Tipi di modulo supportati

Webpack supporta moduli scritti in una larga varietà di linguaggi e preprocessori grazie ai __loaders__. Essi infatti specificano a webpack come processare moduli non scritti in JavaScript in modo da includerli come dipendenze nel bundle generato.\
Esistono, ad esempio,  loaders per moduli scritti in:

* CoffeeScript
* TypeScript
* Sass
* Less
* Stylus
* Elm
