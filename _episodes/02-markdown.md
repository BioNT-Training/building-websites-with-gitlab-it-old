---
title: Scrivere con Markdown
teaching: 0
exercises: 0
questions:
- How can I write content for my webpages?
- How do I link to other pages?
objectives:
- create simple pages of formatted text
keypoints:
- Markdown is an relatively easy way to write formatted text
- Markdown and HTML tags can be used together in a single page
- I recommend writing Markdown links 'reference-style'
- The landing page for a website is conventionally named `index.md`
---


# Markdown
Markdown è un linguaggio di markup leggero, cioè una convenzione per aggiungere
informazioni di stile al contenuto testuale. Come indica il nome Markdown, gli elementi
sintattici di questo linguaggio sono ridotti al minimo. Avendo una sintassi piuttosto
minimalista, il testo formattato in Markdown è relativamente leggibile. Questo potrebbe
essere uno dei motivi per cui Markdown è diventato il linguaggio preferito per la
formattazione degli input dell'utente su siti web come, ad esempio:
- [Stack Exchange](https://stackexchange.com/)
- [GitLab](https://about.gitlab.com/)
- [GitHub](https://github.com/).

# Dove iniziare a scrivere Markdown?
Esistono molti strumenti per il rendering del codice sorgente Markdown. Il rendering è
il processo di generazione di una visione gradevole del contenuto utilizzando le
informazioni di stile incluse nel testo sorgente. È molto probabile che il vostro editor
sia in grado di farlo. Poiché stiamo lavorando per creare siti web utilizzando le pagine
di GitLab, utilizzeremo subito GitLab per imparare le basi di Markdown. Il progetto
GitLab creato nell'ultimo episodio contiene un file `README.md`. Cliccare sul nome del
file per accedervi.

L'immagine sottostante mostra la vista predefinita. Questa vista include una vista
renderizzata del contenuto all'interno del file `README.md`, come quella della homepage
del nostro progetto.

![anteprima README](../fig/gitlab_readme.png){: .image-with-shadow width="900px" }

I pulsanti sulla destra permettono di interagire con il file e la visualizzazione. I
primi due pulsanti, quelli con le icone, permettono di passare da `Display source` a
`Display rendered file`. Passando il mouse su di essi, si visualizzano i due messaggi in
un tooltip. Il sorgente è la vista non renderizzata del nostro file. Possiamo
modificarla attraverso il pulsante blu `Edit`. Fare clic su di esso.

![Interfaccia di modifica del file README dei siti web del
gruppo](../fig/gitlab_edit_readme.png){: .image-with-shadow width="900px" }

Possiamo cambiare il contenuto e dare un'occhiata alla vista renderizzata facendo clic
sulla scheda `Preview` in alto.

![Anteprima del contenuto renderizzato del file README dei siti web del
gruppo](../fig/gitlab_edit_readme_preview.png){: .image-with-shadow width="900px" }

Aggiungiamo `Some **bold** font` e vediamo cosa succede quando lo visualizziamo in
anteprima usando la scheda anteprima. Cosa è successo al mondo in grassetto?

Per salvare il contenuto nel file `README.md`, si deve cliccare sul pulsante `Commit
changes` in fondo alla pagina. Si noti che non si tratta di un semplice pulsante
"Salva", ma di un vero e proprio commit. Questa versione del progetto sarà memorizzata
in git con il nome `Commit message` che si specificherà nel menu di commit qui e nel
ramo impostato come `Target branch`. Per il momento abbiamo solo il ramo principale -
quindi la scelta è ovvia - e il messaggio di commit è precompilato con il nome del file
appena modificato. Si potrebbe voler essere più precisi nel messaggio di commit, ma per
il momento si può scegliere l'opzione predefinita. Impegnare questa modifica.

> ## Scrittura di un messaggio di commit
> 
> Un messaggio di commit è un commento breve, descrittivo e specifico che ci aiuterà a
> ricordare in seguito cosa abbiamo fatto e perché. Per saperne di più sulla scrittura
> di un messaggio di commit si veda [questa
> sezione](https://swcarpentry.github.io/git-novice/04-changes/index.html) della lezione
> di Git-novice.
> 
{: .callout}

![Dopo il commit delle modifiche al README](../fig/gitlab_readme_committed.png){:
.image-with-shadow width="900px" }

L'interfaccia reindirizza alla pagina principale del progetto. In alto, un messaggio
dice "Le tue modifiche sono state impegnate con successo" Le nostre modifiche sono state
incluse nel file README, che ora mostra la seconda riga con il carattere in grassetto.

# Scrittura di Markdown

Ora che conosciamo l'interfaccia di modifica e la scheda di anteprima dei nostri
progetti `README.md`, possiamo usarlo come editor di testo e studiare alcune
caratteristiche di Markdown.

Il nostro `README.md` contiene già del testo e due funzioni di formattazione:
- Intestazione `# group-website`
- Enfasi usando `**bold**`.

Impariamo un altro po' di Markdown aggiungendo un po' di formattazione e vediamo cosa
succede quando lo visualizziamo in anteprima usando la scheda anteprima. Aggiungete
quanto segue al vostro file `README.md`.

~~~
# group-website
Repo for learning how to make websites with GitLab pages

## Learning Markdown

Vanilla text may contain *italics* and **bold words**.

This paragraph is separated from the previous one by a blank line.
Line breaks
are caused by two trailing spaces at the end of a line.

[Carpentries Webpage](https://carpentries.org/)

### Carpentries Lesson Programs:
- Software Carpentry
- Data Carpentry
- Library Carpentry
~~~
> 
{: .language-markdown }

Si può quindi fare di nuovo clic sulla scheda di anteprima per vedere come viene resa la
formattazione.

![Anteprima della formattazione aggiunta al
README](../fig/gitlab_learning_markdown.png){: .image-with-shadow width="900px" }

> ## Gli spazi intermedi di Markdown sono significativi
> 
> Nell'esempio precedente ci sono due spazi alla fine di `Line breaks `. Questi
> introducono la cosiddetta **interruzione di riga dura**, facendo sì che il paragrafo
> continui nella riga successiva, aggiungendo un `<br/>` all'HTML generato.
> 
> Se si interrompe la riga in un file markdown ma non si includono i due spazi finali,
> l'HTML generato continuerà nella stessa riga **senza** introdurre un `<br/>`. Questo
> si chiama **interruzione di riga morbida**.
> 
> In alcuni casi è possibile che le **interruzioni di riga morbide** introducano un
> `<br/>`. Questo può accadere quando si usano diversi [sapori di
> markdown](#markdown-flavours). {: .language-markdown }
> 
{: .callout}

Si può fare il commit di queste modifiche per salvarle. Ma prima, facciamo un esercizio
per provare a scrivere altro markdown.

> ## Esercizio: Prova il Markdown
> Usate [questo cheatsheet][gitlab-flavored-markdown] per aggiungere quanto segue al
> vostro `README.md`:
> 
> - Un'altra intestazione di secondo livello
> - Un po' di testo sotto il titolo di secondo livello che include un link e un testo
>   ~~strikethrough~~.
> - un titolo di terzo livello
> - un elenco numerato
> - Bonus: Aggiungi questa immagine
>   <https://github.com/carpentries/carpentries.org/blob/main/images/TheCarpentries-opengraph.png>
> 
> > ## Soluzione di esempio
> > Per esempio, il markdown potrebbe essere simile al seguente:
> > ~~~
> > ## More info on the lesson
> > You can find this lesson [here](https://grp-bio-it-workshops.embl-community.io/building-websites-with-gitlab/).
> > 
> > ### Four reasons you should learn Markdown:
> > 
> > 1. Less formatting than HTML
> > 2. Easy to read even with formatting
> > 3. Commonly used for websites and software development
> > 4. We ~~don't~~ use it in The Carpentries
> > 
> > ![Carpentries Logo](https://github.com/carpentries/carpentries.org/raw/main/images/TheCarpentries-opengraph.png)
> > ~~~
> > {: .language-markdown }
> > 
> > 
> > 
> {: .solution }
> 
{: .challenge }


> ## Collegamenti di tipo referenziale
> 
> Finora abbiamo usato link in stile _inline_ che hanno l'URL in linea con il testo
> della descrizione, per esempio:
> 
> ~~~
> [Carpentries Webpage](https://carpentries.org/)
> ~~~
> {: .language-markdown }
> 
> Se si usa un link più di una volta, si consideri di usare invece i cosiddetti link in
> stile riferimento. I collegamenti in stile riferimento fanno riferimento all'URL
> tramite un'etichetta. L'etichetta va tra parentesi quadre `[ ]` subito dopo il testo
> descrittivo del collegamento e poi più avanti, di solito in fondo alla pagina, si può
> collegare l'etichetta all'URL a cui fa riferimento per completare il collegamento. In
> questo modo si ottiene quanto segue:
> ~~~
> [Carpentries Webpage][carpentries]
> 
> [carpentries]: https://carpentries.org/
> ~~~
> {: .language-markdown }
> 
{: .callout}

Continueremo a usare Markdown e a saperne di più nel resto della lezione. Sia che
decidiate di strutturare il vostro sito web con tecnologie basate su Markdown o su HTML,
dovrete comunque conoscere alcune nozioni di base di Markdown per modificare il vostro
file README. Il file README fornirà una guida essenziale - mostrata nella pagina di
destinazione del vostro progetto - ai vostri collaboratori e anche a voi per capire di
cosa tratta il progetto e come contribuire.

> ## Sapori di Markdown
> La descrizione iniziale di Markdown era informale e conteneva alcune ambiguità, per
> cui nel corso degli anni sono apparse [diverse implementazioni di Markdown e
> variazioni della
> sintassi](https://github.com/commonmark/commonmark-spec/wiki/markdown-flavors) (spesso
> indicate come "gusti") per supportare varie caratteristiche ed estensioni della
> sintassi. Di conseguenza, la sintassi di una variante può non essere interpretata come
> ci si aspetta in un'altra: bisogna essere consapevoli di quale sia quella utilizzata
> da una particolare piattaforma. Ecco alcune varianti note:
>   - [GitLab-flavored Markdown][gitlab-flavored-markdown] (usato in questa lezione e da
>     GitLab)
>   - [GitHub-flavored Markdown][github-flavored-markdown] (usato da GitHub)
>   - [Kramdown][kramdown] (un'implementazione veloce, Ruby, open source rilasciata
>     sotto licenza MIT)
> 
> Mardown è anche il linguaggio della piattaforma di note collaborative disponibile
> all'EMBL. È possibile accedervi [qui] (https://pad.bio-it.embl.de/). La piattaforma è
> basata su [CodiMD](https://github.com/hackmdio/codimd).
> 
{: .callout}

> ## Esercizio: Aggiungere i dettagli del proprio repository a CodiMD
> 
> Usare la sintassi Markdown per aggiungere un link nel documento di appunti
> collaborativi che si sta usando per seguire questa lezione. Il testo del link deve
> essere il proprio nome utente GitLab e la destinazione il proprio repository.
> 
{: .challenge }

[kramdown]: https://kramdown.gettalong.org/
[gitlab-flavored-markdown]: https://docs.gitlab.com/ee/user/markdown.html
[github-flavored-markdown]:
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

{% include links.md %}

