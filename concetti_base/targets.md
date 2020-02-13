# Targets

Poiché il JavaScript può essere scritto sia per i server che per i browser, webpack offre la possibilità di impostare più target di  deployment tramite il campo `target` nel file di configurazione.

## Utilizzo

__webpack.config.js__

```js
module.exports = {
  target: 'node'
};
```

È sufficiente impostare il __target__ desiderato tramite l'apposito field dell'oggetto configurazione. Nell'esempio è stato scelto `node` come target, perciò webpack produrrà del codice che fa uso della direttica `require()` propria del runtime Node.js, oltre a lasciare invariati gli import di moduli standard come `fs` e `path`.

Il target di default è `web`.

## Target multipli

Per impostare target multipli è necessario creare due differenti configurazioni ed esportarle entrambe:

__webpack.config.js__

```js
const path = require('path');
const serverConfig = {
  target: 'node',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.node.js'
  }
};

const clientConfig = {
  target: 'web',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.js'
  }
};

module.exports = [ serverConfig, clientConfig ];
```

Questa configurazione farà si che webpack crei due diversi file nella cartella `dist`: `lib.js` e `lib.node.js`.
