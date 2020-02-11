# Module Resolution

Un __resolver__ è una libreria che aiuta a trovare un modulo tramite il suo path assoluto. Un modulo può essere richiesto come dipendenza da un altro modulo ad esempio con:

```js
import foo from 'path/to/module';
// or
require('path/to/module');
```

Ed esso potrebbe fare parte dell'applicazione oppure essere una dipendenza esterna.\
Il resolver che webpack utilizza è [enhanced-resolve](https://github.com/webpack/enhanced-resolve).

## Regole di risoluzione dei moduli

Webpack è in grado di risolvere tre tipi di file path.

### Path assoluti

```js
import '/home/me/file';

import 'C:\\Users\\me\\file';
```

Poiché il path assoluto è già noto, non sono necessarie ulteriori operazioni per trovare il file.

### Path relativi

```js
import '../src/file1';

import './file2';
```

In questo caso, il path della cartella del file che fa uso delle dipendenze viene unita ai path relativi specificati nei vari `import`/`require` in modo da ottenere il path assoluto del modulo importato.

### Module paths

```js
import 'module';

import 'module/lib/file';
```

I moduli vengono cercati all'interno di tutte le cartelle specificate in `resolve.modules`. È anche possibile modificare il path originale del modulo creando un alias tramite l'opzione di configurazione `resolve.alias`.
&nbsp;

Una volta che il path viene risolto, esso può rivelarsi essere il path di un file o di una cartella.

Nel primo caso:

* Se il path contiene l'estensione del file, allora il file viene direttamente inserito nel bundle.
* Altrimenti, l'estensione viene risolta attraverso l'opzione `resolve.extensions`, la quale specifica quali sono le estensioni accettate.

Nel secondo caso, per trovare il giusto file con la giusta estensione:

* Se la cartella contiene un file `package.json`, allora i field specificati in `resolve.mainFields` vengono controllati in ordine, e il primo field corrispondente al path determinerà il path del file.

* Se non vi è alcun `package.json` o se non è stato possibile ricavare un path valido da `resolve.mainFields`, allora i file name specificati in `resolve.mainFiles` vengono controllati in ordine, per vedere se vi è un file con il medesimo nome all'intenro della cartella importata.

* Dopodiché l'estensione del file verrà risolta in modo simile tramite l'opzione `resolve.extensions`.

Webpack fornisce delle impostazioni predefinite per queste opzioni.

## Caching

Ogni accesso al filesystem viene cachato, in modo che accessi multipli al medesimo file vengano eseguiti con maggiori performance.\
In modalità __watch__, solo i file realmente modificati vengono eliminati dalla cache. Se questa modalità non è attiva, la cache viene pulita prima di ogni compilazione.
