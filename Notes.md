# WiSe 25/26 Machine Learning Praktikum - Notizen & Fragen

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

### 19.12.25
* GANs oder Diffusion Netze einsetzen?
    * Ja, erstmal GAN
    * Vllt danach Diffusion
* Linke und rechte Augen separat trainieren?
    * Ja: z.B. nur auf linke Augen trainieren und die rechten spiegeln
    * One Hot Encoded: (binär) 10 und 01
    * Achtung: kann zu Overfitting führen
* Benchmarks anschauen

### 09.01.26
* Hypertension 0 erkannt: zusätzlich zu den Class Weights die seltenen Krankheiten vorher duplizieren (leichte Verschiebung und/oder Rotation um 5°; bei Verschiebung aber gucken wie sinnvoll das ist, wenn die preproccesden eig alle mittig sein sollten) -> auf Größe 100 bringen
* Hierarchisches Labeling
    * z.B. Glaucoma und Normal zusammenbringen und dann im 2. Schritt das nochmal unterscheiden (in Kiwan_TestModel_v03 wurde Glaucoma z.B. 17 mal richtig und 20 mal normal zugewiesen)
* Wie ist das nochmal mit den Patienten?? in csv 2 Einträge pro Patient aber 1 Patient kann auch auf beiden Augen eine jeweils andere Krankheit haben UND einzelne Augen die selbst mehrere Krankheiten haben
    * dann statt 1-of-n eine m-of-n-Klassifikation
        * dann z.B. 7 statt 8 Ausgänge (ohne Normal, nur die Krankheiten) -> Normal kriegt dann Label 0 und die Krankheiten irgendwo eine 1 (+ weiteres für spezifische Krankheit??) und die können dann auch beinhalten, dass ein Auge mehrere Krankheiten hat??

Vorschläge zum Umgang mit der Ungleichheit (auch mögliche Themen für die Hausarbeit):
* Class Weights
* Data Augmentation
* Oversampling (seltene duplizieren)
* Andere Loss Funktionen, die die Häufigkeit besser abdecken (z.B. Focal Loss)
* Partial Labeling, hierarchische Segmentierung
* Die häufigsten (Normal und Diabetic) rausnehmen und schauen wie gut der Rest dann funktioniert?
* Kombination/Vergleich der Ansätze

### 16.01.26
* Ergänzend (wieder erinnert): Andere preprocessede Bilder zu ODIR5K probieren (siehe Links oben)