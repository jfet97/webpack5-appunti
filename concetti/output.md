# Output

La configurazione del field **output** ci permette specificare come e dove i file compilati devono essere salvati. È possibile impostare solo una configurazione.

La configurazione consiste nel provvedere un valore per il subfiled **filename**, il quale specifica il nome da usare per il file generato:

__webpack.config.js__
```javascript
module.exports = {
  output: {
    filename: 'bundle.js',
  }
};
```

Il file creato sarà: `./dist/bundle.js`.

Se webpack è stato impostato per creare più bundle è necessario provvedere un nome unico per ognuno di essi. Un modo per farlo è il seguente:

__webpack.config.js__
```javascript
module.exports = {
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist' // imposta anche il path
  }
};
```

I file creati saranno: `./dist/app.js` e `./dist/search.js`.
