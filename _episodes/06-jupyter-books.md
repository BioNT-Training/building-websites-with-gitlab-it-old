---
title: Pagine GitLab con libri Jupyter
teaching: 0
exercises: 0
questions:
- How do I publish web pages through GitLab and Jupyter books?
objectives:
- Publish Jupyter notebooks as HTML on the web with GitHub Pages
keypoints:
- Through Jupyter books, you'll be able to integrate interactive components and code
  in your web pages
---


Facciamo qualcosa di diverso, che vi suonerà un po' più familiare se siete abituati ai
progetti [Jupyter](https://jupyter.org/). Dal loro sito web:
> Il progetto Jupyter esiste per sviluppare software open-source, standard aperti e
> servizi per il calcolo interattivo in decine di linguaggi di programmazione.

**I taccuini Jupyter** consentono di creare e condividere documenti contenenti codice
attivo e testo narrativo. *i *Jupyter Lab** ampliano le loro funzionalità creando un
ambiente di sviluppo interattivo (che consente di navigare nel file system e di definire
l'ambiente di codifica). **Jupyter Hub** è una versione multiutente di Jupyer Lab che le
istituzioni possono implementare localmente (come abbiamo fatto noi dell'EMBL)
(https://jupyterhub.embl.de/).

E **libro Jupyer**?
> Jupyter Book è un progetto open source per la creazione di libri e documenti di
> qualità a partire da materiale computazionale.

Il [tutorial completo](https://jupyterbook.org/start/your-first-book.html) vi guiderà
attraverso le fasi di installazione e la personalizzazione dettagliata disponibile, nel
contesto di questa lezione ci occuperemo solo delle basi. Prima di tutto, installiamo
Jupyter Book. Nel vostro terminale:

~~~
pip install -U jupyter-book
~~~
> 
{: .language-bash }

Attenzione: è necessario avere installato anche **pip**. Ora, creiamo il nostro primo
progetto di libro. Il comando `jupyter-book --help` ci aiuterà a controllare le opzioni,
ma in questa lezione vi spoilereremo qualcosa: il comando

~~~
jupyter-book create jupyter-book-demo
~~~
> 
{: .language-bash }

il comando creerà un libro Jupyter di base in una cartella `jupyter-book-demo`. Questa
cartella include già i tre elementi necessari per la creazione di un libro: un file
`_config.yml`, una tabella di contenuto `_toc.yml` e il contenuto del libro in una
raccolta di file MarkDown, reStructuredText o Jupyter Notebook.

Dal momento che ci stiamo stancando di tutto questo sviluppo e distribuzione, non
vogliamo modificare nulla nel contenuto, ma diamo priorità al fatto che sia pronto e
funzionante in GitLab. Provate a indovinare, cosa dobbiamo aggiungere? Un file
`.gitlab-ci.yml`.

~~~
pages:
  stage: deploy
  image: python:slim
  script:
    - pip install -U jupyter-book
    - jupyter-book clean .
    - jupyter-book build .
    - mv _build/html public
  artifacts:
    paths:
      - public
~~~
> 
{: .language-yaml }

Questo pezzo di codice:
1. Installa jupyter-book (o controlla che sia correttamente installato in remoto).
2. Pulisce la cartella dai file risultanti da (eventuali) build precedenti.
3. esegue il comando `jupyter-book build .`, che costruisce il libro nella cartella in
   una sottocartella `_build`. Si può controllare l'output eseguendo lo stesso comando
   nel terminale e ci si renderà conto che i file HTML effettivi sono nella
   sottocartella `_build/html`.
4. sposta quindi il contenuto HTML nella nostra solita cartella `public`, dove sono
   memorizzati gli artefatti.

> ## Il tuo tempo per sperimentare con un modello
> Questo modello è volutamente minimale per dare la possibilità di mettere alla prova le
> proprie capacità di lettura della documentazione. Consultate le guide agli argomenti
> su [jupyterbook.org](https://jupyterbook.org/intro.html) e trovate un modo per:
> 1. Aggiungere un'altra pagina chiamata "Informazioni" e collegata all'indice.
> 2. Giocate con il formato dei file di questa nuova pagina, aggiungete lo stesso tipo
>    di contenuto nei formati MarkDown, reStructuredTex e Notebook.
> 3. Aggiungere una figura e una didascalia.
> 4. Inserire una cella di codice. Se conoscete un qualsiasi linguaggio di
>    programmazione, aggiungete un semplice grafico e visualizzate l'output di tale
>    grafico nella vostra pagina.
> 5. Per funzioni di codice più avanzate, controllare [come rendere il codice
>    eseguibile](https://jupyterbook.org/interactive/thebe.html)
> 6. Controllare la [galleria di libri
>    Jupyter](https://executablebooks.org/en/latest/gallery.html) per trarre
>    ispirazione!
> 
{: .challenge}



