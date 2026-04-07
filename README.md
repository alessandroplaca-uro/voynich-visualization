# Voynich Visualization

Visualizzatore interattivo del sistema morfemico del Voynich Manuscript (MS 408),
con focus sul **Currier language split** (Hand A vs Hand B) emerso dall'analisi
PCA dei vettori morfemici dei singoli folii.

→ **[Apri il visualizzatore](https://alessandroplaca-uro.github.io/voynich-visualization/)**

## Cosa stai guardando

Ogni punto nel grafico 3D è un **folio** del manoscritto, proiettato in uno spazio
PCA costruito sulle frequenze di 27 morfemi atomici (solventi, gallows, bench
characters, suffissi verbali). Il colore codifica la **sezione tematica**
(Herbal, Balneo, Pharma, Stars), mentre la **forma del marker** codifica il
registro grammaticale di **Currier** (`$L=A` cerchio, `$L=B` rombo).

Tre spazi PCA selezionabili dal menu a tendina:

1. **Spazio congiunto** — PCA su tutti i 174 folii insieme. PC1 (39.2% della
   varianza) separa Hand A da Hand B con Cohen's d = 2.94 ("huge effect"). Il
   primo asse del corpus al livello morfemico è la lingua di Currier, non il
   tema.
2. **Spazio Hand A** — PCA fatta solo sui folii Currier-A. L'asse principale
   (23.7% var) è termico: `ch/chy/t` vs `l`.
3. **Spazio Hand B** — PCA fatta solo sui folii Currier-B. L'asse principale
   (37.3% var, struttura unidimensionale fortissima) è "intensità di
   macerazione": `d/y/dy/edy` collineari.

Sotto il grafico 3D:

- **Profilo verbale per (sezione × mano)**: barre raggruppate dei verbi
  `edy/chy/shy/ey/eey/dy/ody/lky` per ogni gruppo. Si vede a colpo d'occhio
  che Pharma-A è dominato da `ody` e Balneo-B è una muraglia di `edy`.
- **Asse Currier (boxplot di PC1 congiunto)**: distribuzione di PC1 per
  ciascun gruppo (sec × hand), con la media. La separazione fra le due
  popolazioni è massiva.

Controlli in alto:

- **Spazio**: dropdown per scegliere uno dei tre PCA.
- **Tema**: switch chiaro / scuro.
- **Spaziatura**: switch compatta / espansa (cambia i range degli assi).

## Risultato chiave

Le sezioni tematiche del Voynich (Herbal, Balneo, Pharma, Stars) sono in larga
parte **mono-lingua**:

| Sezione | Currier-A | Currier-B |
|---|---|---|
| Herbal | 7 433 token | 3 070 token |
| Balneo | 0 | 6 602 |
| Pharma | 1 631 | 168 |
| Stars | 0 | 10 631 |

Quando si separa il corpus per `$L`, emergono **due grammatiche complementari**
con assi principali quasi ortogonali (cos PC1<sub>A</sub>, PC1<sub>B</sub> = 0.49):

- **Traccia A** (Hand A, formularista): Herbal-A → Pharma-A. Estrazione termica
  con `ch/chy/t`, ricombinazione composita con `ody`, sintassi verbale con
  memoria di 2° ordine forte (CMI = 0.49).
- **Traccia B** (Hand B, schedarista): Herbal-B → Balneo-B → Stars-B. Macerazione
  monotona con `edy` (run di 10+ in fila), grammatica markoviana di 1° ordine
  (CMI ≈ 0.07), distillazione iterata con `lk` in Stars.

Le due tracce condividono i 4 solventi (k/t/l/s), i morfemi atomici, l'architettura
del cifrario — ma li compongono con regole grammaticali strutturalmente diverse.

## Dati e metodo

Corpus: trascrizione Takahashi/Stolfi del Voynich Manuscript (file `LSI_ivtff_0d.txt`,
solo righe `;H>`, separatore punto, encoding latin-1).

Currier language: campo `$L` codificato dai page-header
`<fNNN> <! $I=i $Q=q $P=p $L=l $H=h $X=x>`. Cf. la documentazione del file
Stolfi: *"l is the language in Currier's sense, A or B"*.

Vettori folio: per ogni folio si calcola la frequenza relativa di 27 morfemi
(`k/t/l/s/ch/sh/ckh/cth`, suffissi verbali `lky/eeey/eey/edy/ody/chy/shy/ey/dy`,
aspettuali `al/am`, esiti `ar/or`, sistema AIN `aiiin/aiin/ain`, atomi
`q/d/y`). Folii con < 30 token esclusi. Analizzati 174 folii (102 Hand A,
72 Hand B) sulle ~226 pagine totali.

PCA manuale via decomposizione spettrale di numpy (`np.linalg.eigh` sulla
matrice di covarianza centrata).

## Provenienza e contesto di ricerca

Questo visualizzatore è il risultato di una sessione di analisi (sessione 106,
7 aprile 2026) all'interno di un programma di ricerca più ampio sul Voynich
Manuscript come **cifrario di un farmacista** medievale. Il programma di ricerca
è documentato altrove (Paper III, "The Pharmacists' Cipher", in preparazione).

Il dataset PCA, gli script di estrazione e i ~100 test statistici di supporto
alle 88+ ipotesi del programma vivono in un repository di lavoro privato. Solo
il visualizzatore è pubblicato qui.

## Tecnologie

- **Plotly.js 2.32** per il rendering 3D e i pannelli secondari.
- HTML/CSS/JS vanilla, nessun framework.
- Singolo file HTML self-contained (~280 KB), nessuna richiesta di rete dopo
  il caricamento iniziale di Plotly da CDN.

## Licenza

CC BY 4.0 (Attribution). Se usi il visualizzatore o i dati derivati per
pubblicazioni o presentazioni, cita "Placa A., Voynich Visualization,
sessione 106 — 2026".

## Riproducibilità

L'HTML è generato da uno script Python che parsa il corpus Takahashi e
calcola la PCA. Lo script vive nel repo di lavoro privato. I dati grezzi
(Takahashi LSI_ivtff_0d.txt) sono pubblici e disponibili sul sito di
Stolfi/Reeds: <http://www.ic.unicamp.br/~stolfi/voynich/>.
