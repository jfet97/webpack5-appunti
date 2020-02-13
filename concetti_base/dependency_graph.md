# Dependency Graph

Ogni volta che un file dipende da un'altro, webpack tratta quest'ultimo come una __dipendenza__. Ciò permette a webpack di considerare anche file che non contengono del codice, come le immagini o i web fonts, delle dipendenze della nostra applicazione.

Quando webpack processsa la nostra applicazione, inizia da una lista di moduli specificati come entry point nel file di configurazione e costruisce, ricorsivamente, un grafo delle dipendenze che include ogni file di cui la nostra applicazione necessita. Dopodiché compatterà il tutto in un bundle che potrà essere caricato direttamente dal browser.
