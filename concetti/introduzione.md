# Introduzione

## Concetti chiave

Webpack è un **static module bundler** che, nel processare la nostra applicazione, crea un grafo delle dipendenze tra i vari moduli del nostro progetto e genera uno o più _bundles_.

Dalla versione 4 non richiede più un file di configurazione, anche se rimane aperta la possibilità di configurarlo all'estremo.

### Entry

È necessario \(almeno\) un punto iniziale dal quale iniziare a costruire il grafo delle dipendenze. Webpack determinerà in automatico tutte le sue dipendenze, dirette o indirette che siano, finché non avrà esaminato l'intero progetto.

Di default l'entry point è `./src/index.js`, ma è possibile specificarne uno diverso, o anche impostarne più di uno, tramite il field **entry** del nile di configurazione:

```javascript
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

### Output

Di default webpack andrà ad inserire il _bundle_ generato nella cartella `/dist`, nominando il file principale `main.js`.

È possibile modificare questo comportamento agendo sul field **output**:

```javascript
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'lib'), // percorso dove salvare il bundle
    filename: 'my-first-webpack.bundle.js' // nome del bundle generato
  }
};
```

### Loaders

Di default webpack è in grado di comprendere solo file `.js` e `.json`, ma vi è la possibilità, tramite quelli che sono chiamati **loaders**, di processare altri tipi di file per convertirli in moduli che possono essere utilizzati nel nostro progetto. Anche questi moduli verranno quindi inseriti nel grafo delle dipendenze.

Il field **module.rules** può essere modificato per questo scopo:

```javascript
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
        {
          test: /\.txt$/, // regex per il match con file aventi estensione .txt
          use: 'raw-loader' // nome del loader da utilizzare
        }
    ]
  }
};
```

### Plugins

I plugin ci permettono di eseguire tutta una serie di operazioni utili come: ottimizzazione del _bundle_, gestione degli asset, iniezione delle variabili d'ambiente e così via. Per poter far uso di un plugin è necessario importarlo, instanziarlo ed inserirlo nell'array **plugins**:

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin'); // installato via npm
const webpack = require('webpack'); // per accedere ai plugin di default

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

### Mode

È possibile importare il field `mode` su tre valori diversi, corrispondenti a tre diversi livelli di ottimizzazione: `development`, `production` e `none`. Il valore di default è `production`:

```javascript
module.exports = {
  mode: 'production'
};
```

