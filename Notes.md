# WS2526-MLP Notes

## Datensätze

* https://www.kaggle.com/datasets/andrewmvd/ocular-disease-recognition-odir5k
* https://www.kaggle.com/datasets/tanjemahamed/odir5k-classification
* https://www.kaggle.com/datasets/efiyearcan/odir-5k-preprocessed-with-clahe


## Fragen & Notizen
### 28.11.25

* ODIR5K Originalbilder sind sehr groß (z.B. 2300 x 1700) -> Preprocessed Bilder nehmen (512 x 512) oder selbst eine Preprocessing Pipeline implementieren?
    * Dürfen gepreprocesseste benutzen
* XAI (Grad-CAM)? -> Kann man am Ende einfügen wenn schon was vorliegt
* Möglichkeit: Hierarchisches Labeling (1. Krank oder Gesund, 2. Welche Krankheit usw.)
    * Krankheiten getrennt trainieren und dann zusammenfügen
    * dann würde man zB bei Hypertension (128 Bilder) zufällig 128 aus den Anderen nehmen
* Max Pooling?
* Trainingsdaten aggregieren

### 12.12.25

* DataLoader zur Verwaltung (Umgang mit großen Datenmengen, aber eben ohne alle im Speicher zu halten)
* Daten nach Transformation prüfen (z.B. Rotation um 15°)
    * Durch die Transformationen können wir die seltenen Klassen hochsetzen, indem sie häufiger gesampled werden
* Pooling bei den 512x512 Bildern: eher gleichmäßig reduzieren als mehr anfangs oder mehr am Ende
* Gute Resolution ist die die so klein ist dass es noch genau genug erkannt wird (vllt bisschen plus für Puffer)
* Als nächstes ein vortrainiertes Netz (z.B. resnet) voranstellen und dann (mit eigenem Netz?) finetunen; Peer: “den Head mit eigenen Schichten austauschen”