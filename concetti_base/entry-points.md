# Entry Points

Vi sono più modi per definire il field **entry** in modo da impostare uno o più punti di ingresso della nostra applicazione.

## Singola entry

Le due seguenti sintassi sono equivalenti:

__webpack.config.js__
```javascript
module.exports = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};
```

e la sua shorthand:

__webpack.config.js__
```javascript
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```

Vi è anche la possibilità di iniettare una o più dipendenze di terze parti assieme all'entry principale:

__webpack.config.js__
```javascript
module.exports = {
  entry: {
    main: [
      ['@babel-polyfill', './src/js/main.js']
    ]
  },
};
```

Il grafo globale delle dipendenze sarà sempre uno solo perché le dipendenze dei vari file iniettati verranno unite a quelle del main file.

## Multiple entry

Nel caso in cui abbiamo più punti di ingresso tra loro indipendenti è utile avere la possibilità di impostarli:

__webpack.config.js__
```javascript
module.exports = {
  entry: {
    app: './src/app.js',
    adminApp: './src/adminApp.js'
  }
};
```

Ogni entry point avrà un proprio grafo delle dipendenze associato ed un proprio bundle finale.
