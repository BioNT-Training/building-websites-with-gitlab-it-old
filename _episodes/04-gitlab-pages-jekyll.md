---
title: Pagine GitLab con Jekyll
teaching: 0
exercises: 0
questions:
- How do I publish web pages through GitLab and Jekyll?
objectives:
- Publish Markdown files as HTML on the web with GitHub Pages
keypoints:
- Through Jekyll, GitLab serves pages are generated from `.md` files
---


[Jekyll](https://jekyllrb.com/) è un potente generatore di siti statici che può stare
dietro a GitLab Pages. Crea contenuti statici di siti web in HTML a partire da vari file
presenti nel repository (file Markdown, fogli di stile CSS, modelli/layout di pagina,
ecc.) Questo contenuto "compilato" viene poi servito come sito web.

Jekyll facilita la gestione del sito web perché dipende dai modelli. I modelli (o layout
nella notazione di Jekyll) sono progetti che possono essere riutilizzati da più pagine.
Per esempio, noi (i vostri istruttori) non abbiamo creato uno stile per ogni singolo
esercizio di questa lezione separatamente: abbiamo creato un modello che specifica come
gli esercizi devono essere mostrati (il riquadro arancione, il riquadro delle soluzioni
a discesa, ecc.) e ogni volta che tagghiamo un blocco di testo come "Esercizio" viene
mostrato in questo modo.

Tra poco parleremo dei layout di Jekyll; per ora iniziamo a imparare Jekyll e il suo
linguaggio di scripting chiamato
[Liquid](https://shopify.github.io/liquid/basics/introduction/).

## Parametri globali

Anche in questo caso, attiveremo e personalizzeremo il nostro deployment dal file
`.gitlab-ci.yml`. Si può decidere di modificare la versione precedente del repository
`group-website`, ma noi suggeriamo di crearne uno nuovo. Seguire i passi di
"Impostazione di un progetto"
nell'[introduzione](https://grp-bio-it-workshops.embl-community.io/building-websites-with-gitlab/01-introduction/index.html),
se si desidera farlo. Creare/modificare il contenuto del file `.gitlab-ci.yml` con:

~~~
image: ruby:latest

pages:
  script:
    - gem install bundler
    - bundle install
    - bundle exec jekyll build -d public
  artifacts:
    paths:
      - public
  only:
    - main
~~~
> 
{: .language-yaml }

Questo codice richiede che lo script venga eseguito nell'ambiente dell'ultima versione
di Ruby, installa la gemma Jekyll e costruisce il sito nel percorso pubblico (creando la
cartella in remoto, non ci si deve preoccupare a questo punto). Il risultato riguarda
solo il ramo principale.

L'esecuzione di questa pipeline richiede anche un `Gemfile`. Crearlo nella cartella
principale con il seguente contenuto:
~~~
source "https://rubygems.org"

gem "jekyll"
~~~
> 
{: .language-shell }

In breve, ma lo vedremo più in dettaglio, Jekyll cerca i file di testo che iniziano con
un'intestazione formattata in questo modo:

~~~
---
variable: value
other_variable: other_value
---

...stuff in the page...
~~~
> 
{: .source}

e inserisce i valori di queste variabili nella pagina quando la formatta. I tre trattini
che iniziano l'intestazione *devono* essere i primi tre caratteri del file: anche un
solo spazio prima di essi farà sì che Jekyll ignori il file.

Il contenuto dell'intestazione deve essere formattato come YAML e può contenere
booleani, numeri, stringhe di caratteri, elenchi e dizionari di coppie nome/valore. I
valori dell'intestazione sono indicati nella pagina come `page.variable`. Ad esempio,
questa pagina:

~~~
---
name: Science
---
{% raw %}Today we are going to study {{page.name}}.{% endraw %}
~~~
> 
{: .source}

è tradotto in:

~~~
<html>
  <body>
    <p>Today we are going to study Science.</p>
  </body>
</html>
~~~
> 
{: .html}

> ## Esercizio: La sintassi di Jekyll
> Verificate la vostra comprensione della sintassi di Jekyll. In cosa verrebbe tradotto
> questo template?
> ~~~
> ---
> name: Tom
> location: Heidelberg
> ---
> {% raw %}{{page.name}} is in {{page.location}}. I believe {{page.location}} is a very nice city.{% endraw %}
> ~~~
> {: .source}
> 
> > ## Soluzione
> > ~~~
> > <html>
> >   <body>
> >     <p>Tom is in Heidelberg. I believe Heidelberg us a very nice city.</p>
> >   </body>
> > </html>
> > ~~~
> > {: .html}
> > 
> > 
> > 
> {: .solution }
> 
{: .challenge }

Le principali opzioni di configurazione di Jekyll sono specificate in un altro file,
chiamato `_config.yml`. Creiamo alcuni parametri di configurazione per il nostro sito
web.

1. Creare un file `_config.yml` nella directory principale del sito.
2. Aggiungere i parametri `description` e `email` come:

~~~
description: This project develops training materials for reseachers wanting to learn to build project
websites in GitLab Pages.
email: team@carpentries.org
~~~
> 
{: .language-yaml}

le impostazioni di configurazione globale di `_config.yml` sono rese disponibili come
variabile `site.PARAMETER_NAME` in ogni pagina del sito. Quindi, il parametro globale
`email` che abbiamo definito sopra sarà accessibile come `site.email`. Si noti che si
tratta di parametri globali, quindi diversi dai parametri locali specifici della pagina
negli esempi precedenti.

Per accedere al valore del parametro all'interno di una pagina, si utilizza la notazione
di Liquid per l'output del contenuto, circondando una variabile tra parentesi graffe
come `{% raw %}{{ variable }}{% endraw %}`.

> ## Parametri globali predefiniti
> Oltre ai parametri globali definiti dall'utente, Jekyll mette a disposizione un certo
> numero di [utili variabili predefinite a livello di
> sito](https://jekyllrb.com/docs/variables#site-variables) all'interno del sito web:
> per esempio `{% raw %}{{ site.time }}{% endraw %}` (l'ora corrente) o `{% raw %}{{
> site.pages }}{% endraw %}` (un elenco di tutte le pagine).
> 
{: .callout}

Creare un file `index.md` nella cartella principale, con il seguente contenuto:

~~~
{% raw %}---
title: My first Jekyll page
---{% endraw %}

# Building Websites with Jekyll and GitLab

## Description
{% raw %}{{ site.description }}{% endraw %}
Welcome to {% raw %}{{ page.title }}{% endraw %}

Have any questions about what we do? [We'd love to hear from you!]({% raw %}mailto:{{ site.email }}{% endraw %})
~~~
> 
{: .language-markdown }

Il progetto deve includere i seguenti file:

![Basic Jekyll](../fig/basic_files_jekyll.png){: .image-with-shadow width="600px" }

Impegnare e spingere le modifiche, quindi monitorare l'esecuzione della pipeline e
controllare il risultato finale all'URL `https://<your user
name>.embl-community.io/group-website`.

> ## Esercizio: Creare un parametro globale di Twitter
> In `about.md` abbiamo un URL di Twitter sotto la sezione "Contatti". Questa è
> un'informazione che potrebbe essere inserita nei parametri globali di `_config.yml`,
> perché si potrebbe voler ripetere in calce a ogni pagina. Apportare le modifiche al
> sito web per estrarre l'URL di Twitter come parametro globale.
> > ## Soluzione
> > 1. Aggiungere il parametro twitter a `_config.yml`:
> >    ~~~
> >    description: "This research project develops training materials for reseachers wanting to learn to build project
> >    websites in GitHub with GitHub Pages."
> >    email: "team@carpentries.org"
> >    twitter: "https://twitter.com/thecarpentries"
> >    ~~~
> >    {: .language-yaml}
> > 
> > 
> > 2. Utilizzare il parametro twitter in `about.md`:
> > 
> >    ~~~
> >    # About
> > 
> >    ## Project
> > 
> >    {% raw %}{{ site.description }}{% endraw %}
> > 
> >    ## Funders
> > 
> >    We gratefully acknowledge funding from the XYZ Founding Council, under grant number 'abc'.
> > 
> >    ## Cite us
> > 
> >    You can cite the project as:
> > 
> >    > *The Carpentries 2019 Annual Report. Zenodo. https://doi.org/10.5281/zenodo.3840372*
> > 
> >    ## Contact us
> > 
> >    - Email: [{% raw %}{{ site.email }}{% endraw %}](mailto:{% raw %}{{ site.email }}{% endraw %})
> >    - Twitter: [{% raw %}{{ site.twitter }}{% endraw %}]({% raw %}{{ site.twitter }}{% endraw %})
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 3. Si noti che non si dovrebbe vedere alcun cambiamento nel proprio sito web.
> >    Tuttavia, ora è possibile accedere all'URL di Twitter da qualsiasi pagina del
> >    sito, se necessario.
> > 
> {: .solution}
> 
{: .challenge}

## Parametri locali

Oltre ai parametri globali (a livello di sito) disponibili tramite la variabile globale
`site`, Jekyll mette a disposizione informazioni _locali_ (specifiche della pagina)
tramite la variabile `page`. Alcune di queste sono predefinite, come `page.title`, che
fornisce il titolo della pagina attualmente attiva/visitata. Altri possono essere
definiti autonomamente. Si veda questo [elenco dei parametri predefiniti della pagina]
(https://jekyllrb.com/docs/variables#page-variables).

È possibile definire parametri locali utilizzando la notazione YAML all'interno di una
pagina Markdown, includendola in un'intestazione di pagina e delimitando l'intestazione
con linee triple tratteggiate `---`. Queste intestazioni sono chiamate *front matter* e
sono usate per impostare variabili e metadati sulle singole pagine del sito Jekyll.

> ## Materia prima
> Da [sito web di Jekyll](https://jekyllrb.com/docs/front-matter/):
> 
> > Qualsiasi file che contenga un blocco YAML front matter verrà elaborato da Jekyll
> > come un file speciale. Il front matter deve essere la prima cosa nel file e deve
> > avere la forma di un blocco YAML valido, compreso tra linee triple tratteggiate.
> 
{: .callout}

> ## I parametri globali e locali sono sensibili alle maiuscole e minuscole
> È importante notare che i parametri usati nei siti sono sensibili alle maiuscole. Per
> convenzione, di solito sono tutti caratteri minuscoli.
> 
{: .callout}

Ecco un esempio:

~~~
---
layout: post
title: "My first blog post"
author: "Danger Mouse"
---
~~~
> 
{: .language-yaml }

Tra queste linee triple tratteggiate, è possibile sovrascrivere le variabili predefinite
(come `page.layout` o `page.title`) o crearne di personalizzate di cui si ha bisogno
localmente nella pagina (come `page.author`). Queste variabili saranno poi disponibili
per l'accesso tramite i tag di Liquid (ad esempio, `{% raw %}{{{% endraw %} page.title
{% raw %}}}{% endraw %}` ) più avanti nel file e anche in tutti i file che lo includono.
Si noti che queste variabili sono accessibili solo in quella pagina. Si otterrà un
errore se si cerca di fare riferimento a una `page.variable` definita in una pagina
diversa.

> ## Esercizio: Pratica con le variabili locali
> 
> Esercitiamoci a creare e usare le variabili locali. Pensate a una variabile locale che
> potreste voler usare solo nella vostra pagina `about.md` o `index.md`. Se non vi viene
> in mente nessuna, create una variabile locale chiamata "lezione-esempio" con il valore
> di "https://carpentries.github.io/lesson-example/" e fatele riferimento nel vostro
> `index.md`.
> 
> Cosa avete aggiunto al vostro `index.md` per creare questa variabile? Dove è stata
> aggiunta la materia prima nel file `index.md`? Come si fa riferimento a questa
> variabile?
> 
> > ## Soluzione
> > 
> > Creare un'intestazione YAML all'inizio di `index.md` e aggiungere la variabile
> > `lesson-example` tra i delimitatori a triplo trattino. Si può quindi fare
> > riferimento al valore nella pagina `index.md` come `{% raw %}{{{% endraw %}
> > page.lesson-example {% raw %}}}{% endraw %}`. Il file dovrebbe ora apparire come:
> > 
> > ~~~
> > ---
> > lesson-example: "https://carpentries.github.io/lesson-example/"
> > ---
> > 
> > # Building Websites in GitHub
> > 
> > ## Description
> > {% raw %}{{ site.description }}{% endraw %}
> > 
> > More details about the project are available from the [About page](about).
> > 
> > See some [examples of our work]({% raw %}{{{% endraw %} page.lesson-example {% raw %}}}{% endraw %}).
> > 
> > Have any questions about what we do? [We'd love to hear from you!]({% raw %}mailto:{{ site.email }}{% endraw %})
> > ~~~
> > {: .language-markdown }
> > 
> > 
> > Si noti che questa variabile non è accessibile dalla pagina `about.md` ed è locale a
> > `index.md`.
> > 
> {: .solution}
> 
{: .challenge}

## Aggiunta di nuove pagine

Il prossimo passo sarà creare un'altra pagina di questo sito web. Idealmente, il nostro
sito avrà più pagine e quindi, per mantenere l'ordine, creeremo la cartella `pages` per
memorizzarle. In questa cartella, creare un file `about.md` con il seguente contenuto:

~~~
{% raw %}---
title: About
permalink: /about/
---{% endraw %}

# About

## Project

{% raw %}{{ site.description }}{% endraw %}

## Funders

We gratefully acknowledge funding from the XYZ Founding Council, under grant number 'abc'.

## Cite us

You can cite the project as:

>    *The Carpentries 2019 Annual Report. Zenodo. https://doi.org/10.5281/zenodo.3840372*

## Contact us

- Email: [{% raw %}{{ site.email }}{% endraw %}](mailto:{% raw %}{{ site.email }}{% endraw %})
- Twitter: [@thecarpentries](https://twitter.com/thecarpentries)
~~~
> 
{: .language-markdown }

Si noti che la posizione dell'URL di questa pagina è specificata nell'intestazione,
attraverso l'attributo `permalink`.

Questo è l'aspetto attuale delle vostre cartelle:

![Informazioni su Jekyll](../fig/about-jekyll-pages.png){: .image-with-shadow
width="600px" }

Ora si deve modificare il file `index.md` per includere un link alla nuova pagina about,
in modo da poterla raggiungere dalla pagina principale. Aggiungere una riga al file
`index.md` per includere:

~~~
More details about the project are available from the [About page](about).
~~~
> 
{: .language-markdown }

Il link in questa riga reindirizzerà a `https://<your user
name>.embl-community.io/group-website/about`, che è l'URL della nostra nuova pagina
about.

Impegnarsi, fare il push e andare sul proprio sito web per vedere le modifiche. Si noti
che i parametri del sito non saranno resi bene quando si visualizzano i file in GitHub
(saranno visualizzati come testo `{% raw %}{{ site.PARAMETER_NAME }}{% endraw %}`
piuttosto che come valore reso del parametro), ma lo saranno nel sito web.

> ## Riutilizzare e ridurre
> I parametri globali di Jekyll sono un modo utile per mantenere tutta la configurazione
> del sito in un unico posto (anche se li si usa solo una volta). In combinazione con i
> layout/template di Jekyll (di cui parleremo nel prossimo episodio), sono un ottimo
> modo per creare snippet di markup riutilizzabili che possono essere ripetuti su più
> pagine o addirittura su ogni pagina del sito. Il riutilizzo aiuta a ridurre la
> quantità di codice da scrivere.
> 
{: .callout}

## Link utili

Questo voleva essere solo un tutorial di base. Le possibilità di personalizzazione dei
siti con Jekyll vanno ben oltre quanto mostrato qui, si potrebbe ad esempio:

- progettazione di layout di pagina (come gli esercizi/soluzioni di questa lezione),
- lavorare con i loop per elaborare iterativamente variabili contenenti più valori,
- utilizzare i filtri per controllare il formato delle variabili quando vengono inserite
  in una pagina,

e altro. [Questa lezione](https://carpentries-incubator.github.io/jekyll-pages-novice/)
di The Carpentries, anche se pensata per GitHub, è una risorsa preziosa per saperne di
più su come farlo.

Se si sta cercando la documentazione ufficiale di GitLab sulle pagine GitLab con Jekyll,
seguire [questo
link](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html).

Infine, [questo progetto](https://gitlab.com/pages/jekyll) contiene un modello più
elaborato di sito web basato su GitLab e Jekyll.


{% include links.md %}

