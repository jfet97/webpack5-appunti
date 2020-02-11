# Configuration

Il file di configurazione di webpack non è altro che un file JavaScript che esporta un oggetto configurazione. Poichè è un normale modulo CommonJs, è possibile:

* importare altri file usando `require(...)`
* usare utility scaricate con __npm__ sempre via `require(...)`
* sfruttare il linguaggio per generare le varie parti della configurazione

## Esempio di semplice configurazione

__webpack.config.js__

```javascript
var path = require('path');

module.exports = {
  mode: 'development',
  entry: './foo.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'foo.bundle.js'
  }
};
```
