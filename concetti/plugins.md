# Plugins

I plugin sono la linfa vitale di webpack: permettono di fare tutto ciò che i loaders non possono.

## Anatomia

I plugin di webpack sono semplici oggetti JS aventi un metodo `apply`. Questo metodo sarà invocato da webpack, dandoci accesso all'intero ciclo di vita della compilazione:

__ConsoleLogOnBuildWebpackPlugin.js__

```javascript
const pluginName = 'ConsoleLogOnBuildWebpackPlugin';

class ConsoleLogOnBuildWebpackPlugin {
  apply(compiler) {
    // la callback verrà invocata poco prima dell'avvio del processo di building
    compiler.hooks.run.tap(pluginName, compilation => {
      console.log('The webpack build process is starting!!!');
    });
  }
}

module.exports = ConsoleLogOnBuildWebpackPlugin;
```

Il primo parametro del metodo `tap` dell'hook del compiler deve essere una versione, in stile _CamelCase_, del nome del plugin. È cosnigliato fare uso di una costante come nell'esempio, in modo che il nome possa facilmente essere riutilizzato per più hook.

## Utilizzo

Poiché i plugin potrebbero dover essere configurati, bisogna utilizzare una nuova istanza del plugin nella configurazione di webpack:

__webpack.config.js__

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin'); // installato via npm
const webpack = require('webpack'); // per accedere ai plugin di default
const path = require('path');

module.exports = {
  plugins: [
    // notare l'utilizzo della keyword 'new'
    new webpack.ProgressPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```
