# Getting Started

## Basic Setup

Innanzitutto creiamo una cartella, inizializziamo npm e installiamo sia webpack che la webpack CLI localmente:

```sh
mkdir webpack-demo
cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```

Adesso creiamo la seguente struttura di cartelle, file e il loro contenuto:

__project__

```default
  webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js
```

__src/index.js__

```js
function component() {
  const element = document.createElement('div');

  // Attenzione: è necessaria la presenza di lodash inclusa tramite script
  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());
```

__index.html__

```html
<!doctype html>
<html>
  <head>
    <title>Getting Started</title>
    <script src="https://unpkg.com/lodash@4.16.6"></script>
  </head>
  <body>
    <script src="./src/index.js"></script>
  </body>
</html>
```

Per evitare di pubblicare inavvertitamente il progetto su npm, eliminiamo l'entry `main` ed impostiamo il package come `private`:

__package.json__

```json
  {
    "name": "webpack-demo",
    "version": "1.0.0",
    "description": "",
    "private": true, // <-- da aggiungere
    "main": "index.js", // <-- da rimuovere
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "webpack": "^4.20.2",
      "webpack-cli": "^3.1.2"
    },
    "dependencies": {}
  }
```

In questo esempio, vi è una dipendenza implicita tra i tag `<script>`: il nostro file `index.js` __dipende__ da `lodash`, poiché fa utilizzo della variabile `_`. Ciò significa che `index.js` assume che `lodash` venga scaricata prima della sua esecuzione, senza però dichiarare esplicitamente la dipendenza.

Vi sono dei problemi nell'agire in questo modo:

* non è immediatamente evidente che il nostro script dipende da una libreria esterna
* se una dipendenza manca, o è inclusa nell'ordine sbagliato, l'applicazione non funzionerà in modo corretto
* se una dipendenza viene inclusa ma non utilizzata, il browser scaricherà inutilmente del codice

Vediamo come utilizzare webpack per gestire, e migliorare, la situazione.

## Creating a Bundle

Innanzitutto modificheremo leggermente la struttura del nostro progetto: separiamo il codice sorgente (`/src`) che noi stessi scriviamo dal codice risultante dal processo di bundling di webpack (`/dist`):

__project__

```default
  webpack-demo
  |- package.json
+ |- /dist
+   |- index.html
- |- index.html
  |- /src
    |- index.js
```

Per inserire `lodash` in quanto dipendenza, dobbiamo installare la libreria localmente:

```sh
npm install --save lodash
```

Adesso importiamola nel nostro script:

__src/index.js__

```js
import _ from 'lodash'; // <--

function component() {
  const element = document.createElement('div');

  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());
```

In utlimo dobbiamo aggiornare l'`index.html` in modo tale che faccia uso __solo__ del bundle prodotto da webpack:

__index.html__

```html
  <!doctype html>
  <html>
   <head>
     <title>Getting Started</title>
   </head>
   <body>
     <script src="main.js"></script> <!-- -->
   </body>
  </html
```

Con questo setup il nostro script `index.js` richiede esplicitamente la presenza di lodash, eseguendo il binding della libreria all'underscore (`_`). Perciò lo scope globale non viene sporcato. Inoltre, webpack sfrutta questa dipendenza, adesso esplicita, nella creazione del grafo delle dipendenze, per poi generare un bundle ottimizzato dove gli script verranno eseguiti nell'ordine corretto.

Ora possiamo eseguire webpack con `npx webpack`, il quale prenderà automaticamente in carico il nostro script `src/index.js` come entry point, e genererà `dist/main.js` come output. Se apriamo `index.html` nel browser dovremmo trovare la stringa 'Hello webpack'.

## Using a Configuration

Dalla versione 4, webpack non necessità più di una configurazione. D'altra parte, tutti i progetti non banali necessitano di una configurazione, ed è per questo che webpack supporta un file di configurazione:

__project__

```
  webpack-demo
  |- package.json
+ |- webpack.config.js
  |- /dist
    |- index.html
  |- /src
    |- index.js
```

__webpack.config.js__

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

__shell__

```
npx webpack --config webpack.config.js
```

Se è presente un `webpack.config.js`, webpack prenderà quello di default, senza la necessità di utilizzare l'opzione `--config`. Ad ogni modo, ciò mostra che possiamo passare a webpack una configurazione con un nome qualsiasi.

##  NPM Scripts

È buona norma aggiungere uno script nel `package.json` per eseguire il build del progetto:

__package.json__
```json
  {
    "name": "webpack-demo",
    "version": "1.0.0",
    "description": "",
    "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
      "build": "webpack" // <-- da aggiungere>
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "devDependencies": {
      "webpack": "^4.20.2",
      "webpack-cli": "^3.1.2"
    },
    "dependencies": {
      "lodash": "^4.17.5"
    }
  }
```
