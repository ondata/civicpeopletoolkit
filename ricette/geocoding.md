
<!-- TOC -->

- [Introduzione](#introduzione)
- [Perché è utile](#perché-è-utile)
- [Come fare](#come-fare)
    - [Con OpenRefine e le API di Nominatim](#con-openrefine-e-le-api-di-nominatim)
        - [Note e riferimenti](#note-e-riferimenti)

<!-- /TOC -->
# Introduzione

Il _geocoding_ è la trasformazione di una stringa (`Via Libertà 92, Palermo`) in una coppia di coordinate (`38.140157, 13.345594`).

# Perché è utile

Molto spesso si hanno a disposizione elenchi di indirizzi. Sono dati quindi riferibili a dei luoghi, ma che non si possono usare per creare subito una mappa.

Come ad esempio i dati sottostanti, relativi ad alcuni beni immobili sequestrati alle mafie in Sardegna.

| m_bene      | regione  | provincia | comune            | indirizzo              | 
|-------------|----------|-----------|-------------------|------------------------| 
| I-SS-111490 | Sardegna | Sassari   | Alghero           | VIA EUROPA N. 85       | 
| I-SS-111484 | Sardegna | Sassari   | Sassari           | VIALE UMBERTO I, N. 68 | 
| I-SS-122176 | Sardegna | Sassari   | Sassari           | VIA DALMAZIA N. 21     | 
| I-SS-122189 | Sardegna | Sassari   | Sassari           | VIALE UMBERTO I N. 68  | 
| I-CA-178778 | Sardegna | Cagliari  | Quartu Sant'Elena | VIA IRLANDA 58         | 

# Come fare

## Con OpenRefine e le API di Nominatim

[**OpenRefine**](../tools/openrefine.md) è uno strumento classico per "fare cose" con i dati e le [**API di Nominatim**](http://wiki.openstreetmap.org/wiki/Nominatim) sono uno dei servizi con cui è possibile fare il _geocoding_ di un indirizzo.

Nel video sottostante è illustrata la procedura:

- si crea un progetto in OpenRefine importando la tabella che contiene gli indirizzi ([qui](./data/immobiliOpenRegioSardegna.csv) il file usato nel video);
- si aggiunge una colonna che verrà usata per fare il _geocoding_, in modo che il dato di input contenga sia l'indirizzo, che il comune di riferimento (altrimenti il _geocoding_ sarebbe impossibile), con la formula `value + ', ' + cells["comune"].value + ', Italia'`
- si lancia la procedura di _geocoding_ usando delle [istruzioni](https://github.com/aborruso/geocode_openrefine/blob/master/Nominatim/open_refine_nominatim.json) scritte da [**Andrea Zedda**](https://twitter.com/andria_tzedda);
- si esporta l'output come foglio elettronico

[![](./imgs/videoGeocodingOpenrefine.png)](https://www.youtube.com/watch?v=GpD87pKYQgo&feature=youtu.be&hd=1)

### Note e riferimenti

- il _geocoding_ di Nominatim è basato sul database di [**OpenStreetMap**](https://www.openstreetmap.org/#map=19/38.12672/13.29924), quindi i risultati non saranno soddisfacenti in quei luoghi per cui in OSM ci sono pochi dati o di scarsa qualità;
- [qui](https://operations.osmfoundation.org/policies/nominatim/) le linee di condotta sull'utilizzo delle API;
- ai dati di output si applica la licenza di [OpenStreetMap](http://www.openstreetmap.org/copyright).