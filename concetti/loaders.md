# Loaders

I loaders sono delle trasformazioni che vengono applicate al codice sorgente di un modulo Ci permettono di pre-processare i file mentre li importiamo, dandoci la possibilità di integrare direttamente codici sorgenti scritti in TypeScript, CSS, ma anche immagini e molto altro!

## Usare i Loader

Innanzitutto è necessario installare il loader necessario:

```sh
npm install --save-dev css-loader
```

Dopodiché bisogna far sapere a webpack che desideriamo usare questo loader per importare i file `.css`:

```javascript
module.exports = {
  module: {
    rules: [
        {
          test: /\.css$/,
          use: 'css-loader'
        }
    ]
  }
};
```

&nbsp;

È possibile impostare più di un loader per un specifico tipo di file. I loader verranno eseguiti in cascata, a partire dall'ultimo, ed ognuno agirà sul prodotto del precedente:

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
            {
              loader: 'style-loader'
            },
            {
                loader: 'css-loader',
                options: {
                    modules: true
                }
            },
            {
                loader: 'sass-loader'
            }
        ]
      }
    ]
  }
};
```

In questo esempio l'ordine sarà: `sass-loader` -> `css-loader` -> `style-loader`.\
Alla fine della catena, webpack si aspetta sempre del JavaScript.
