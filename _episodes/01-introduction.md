---
title: Introduzione
teaching: 0
exercises: 0
questions:
- What is static web content?
- Why should I use GitHub or GitLab Pages to create my website?
objectives:
- Explain what a static site generator does.
- Choose the appropriate tool for your website/project.
keypoints:
- A static site generator combines page-specific content with layout elements and
  styling information to construct individual webpages.
- GitHub/GitLab Pages is a good choice for people who are already familiar with Git
  and GitHub/GitLab.
- This approach can be used to create a relatively small website/blog on a limited
  budget.
---


## Come funzionano i siti web

Quando usiamo un browser web per visitare una pagina del World-Wide Web, il browser
chiede informazioni a un server - un computer che memorizza i dati rilevanti per il sito
e che è configurato per ricevere e rispondere alle richieste di tali dati. Supponendo
che non ci siano stati problemi in questa fase (ad esempio, la richiesta di una pagina
che non esiste o l'impossibilità di raggiungere il server), il nostro browser riceve e
interpreta queste informazioni per renderizzare e visualizzare la pagina web sul nostro
schermo.

Uno sviluppatore web probabilmente rimarrebbe inorridito nel leggere una così grossolana
semplificazione, e questo è solo uno dei motivi per cui gli sviluppatori web non sono il
target di questo tutorial.

La pagina visualizzata dal browser web è il risultato della combinazione di **HTML** -
un formato gerarchico che descrive gli elementi strutturali della pagina e il loro
contenuto grezzo - con **CSS** - un insieme ordinato di istruzioni di stile che indicano
al browser come il contenuto deve essere organizzato e formattato - ed eventuali
**immagini** che devono essere incorporate nella pagina. Altre informazioni ricevute dal
server, ma non visualizzate dal browser, includono **metadati**, **cookies** e altri
elementi non visibili nell'HTML - informazioni sul sito che potrebbero essere rilevanti
per un computer ma che probabilmente non sono interessanti per un essere umano (ci sono
[eccezioni][qwantz-easter-egg-ext] a questo) - e script che il browser può eseguire per
fare qualcosa in risposta a vari trigger.

## Hello World in HTML

Quando si impara un nuovo linguaggio di programmazione, spesso si trova un riferimento
al famoso esempio `Hello world`. Questi esempi sono in genere il codice più semplice in
grado di produrre e visualizzare il testo "Hello, World!" sullo schermo.

Poiché l'HTML richiede la presenza di alcuni tag e quasi sempre in coppie corrispondenti
(apertura `<tag>` e chiusura `</tag>`), i documenti HTML tendono a diventare verbosi
piuttosto rapidamente.

Il più semplice HTML valido `Hello world` è:

~~~
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <p>Hello, World!</p>
  </body>
</html>
~~~
> 
{: .language-html }

Come potete immaginare, scrivere a mano lunghi documenti HTML è piuttosto doloroso.
Notate che non abbiamo specificato nulla su come e dove il testo debba essere
visualizzato.

Per ottenere questo risultato è necessario includere tag stilizzati o istruzioni CSS
(Cascading Style Sheets). Se non si forniscono istruzioni CSS (all'interno del documento
HTML o in un file separato), un browser web farà un'ipotesi sulla disposizione degli
elementi HTML nella pagina in base alle sue impostazioni predefinite.

> ## I molti tag dell'HTML
> 
> Nell'esempio `Hello world` di cui sopra vengono usati 5 tag diversi (`html`, `head`,
> `title`, `body` e `p`) nella loro forma aperta `<>` e chiusa `</>`. Vediamo anche il
> tag speciale `doctype` che indica il formato e la versione del documento, in questo
> caso, [HTML(5)][html5-wikipedia].
> 
> Esistono molti altri tag per definire:
> - *elementi strutturali*, come `table`, `div`, `span`, `nav`, `section`;
> - *elenchi*, come `ul` (per gli elenchi non ordinati) e `or` (per gli elenchi
>   ordinati);
> - *elementi stilizzati*, come `i`/`em` (per i *corsivi/enfasi*), `b`/`strong` (per il
>   **grosso**) e `u` (per il <u>testo sottolineato</u>);
> - *intestazioni*, numerate da `h1` a `h6` per i titoli e i sottotitoli
>   progressivamente più piccoli;
> - *elementi multimediali*, come `img`, `video`, `audio` per incorporare contenuti
>   multimediali ricchi; e
> - *collegamenti*, utilizzando l'importante tag `a` (ancora) per collegarsi a sezioni
>   della stessa pagina o ad altre pagine dello stesso sito web o di siti esterni.
> 
> L'[elenco dei tag HTML validi][html5-tags] è piuttosto esteso e copre una ricca gamma
> di funzionalità che alimentano il world wide web di oggi.
> 
{: .callout }

> ## Esercizio: Scrivere HTML di base
> 
> Dato il testo stilizzato:
> 
> <h1><em>Hello</em>, World!</h1>
> 
> scrivere l'HTML che produrrà lo stesso risultato. **Il carattere grande è ottenuto
> grazie all'uso di un'intestazione.
> 
> > ## Soluzione
> > 
> > ~~~
> > <h1><em>Hello</em>, World!</h1>
> > ~~~
> > {: .language-html }
> > 
> {: .solution }
> 
{: .challenge }

Scriviamo un esempio HTML più complesso, utilizzando una tabella che mostri il testo
"Hello, World!" in diverse lingue e che si visualizzi come segue: ![Esempio di tabella
HTML](../fig/html-table.png){: .image-with-shadow width="600px" }

L'HTML per produrre una tabella di questo tipo ha questo aspetto (potete copiare e
incollare lo snippet nel file HTML creato nell'esempio precedente):
~~~
<table>
    <tr><th>Language</th><th>Text</th></tr>
    <tr><td>English</td><td>Hello, World!</td></tr>
    <tr><td>French</td><td>Bonjour, le monde!</td></tr>
    <tr><td>Portuguese</td><td>Olá, Mundo!</td></tr>
    <tr><td>Serbian</td><td>Zdravo, svete!</td></tr>
</table>
~~~
> 
{: .language-html }

Ogni riga è racchiusa tra i tag **t**able **r**ow `<tr>` e `</tr>`. All'interno di una
riga, i tag `<th>` e `</th>` sono usati per contenere **t**able **h**eadings (speciali
celle di tabella visualizzate in grassetto), mentre le normali celle **t**able **d**ata
sono contenute nei tag `<td>` e `</td>`.

Un esempio simile scritto usando le liste HTML avrebbe il seguente aspetto: ![Esempio di
lista HTML](../fig/html-list.png){: .image-with-shadow width="600px" }

~~~
<ul>
    <li>English: Hello, World!</li>
    <li>French: Bonjour, le monde!</li>
    <li>Portuguese: Olá, Mundo!</li>
    <li>Serbian: Zdravo, svete!</li>
</ul>
~~~
> 
{: .language-html }

Qui abbiamo usato i tag **u**nordered **l**ist `<ul>` e `</ul>` per definire una lista
con 4 elementi, ciascuno a sua volta avvolto in singoli tag **l**ist **i**tem (`<li>` e
`</li>`).

## Siti statici vs siti dinamici

Le pagine statiche sono quelle il cui contenuto è memorizzato su un server in uno stato
pronto per essere inviato a qualsiasi utente che faccia una richiesta per quella pagina
web. Quando viene effettuata una richiesta, il server deve inviare solo le informazioni
che compongono la pagina web (come HTML e CSS). I siti che non cambiano spesso, come ad
esempio un sito web contenente il proprio CV, sono spesso memorizzati come siti statici.

Al contrario, i siti _dinamici_ sono quelli che hanno le loro pagine generate quando un
utente fa una richiesta per una pagina web. A seconda del momento in cui viene fatta la
richiesta, il contenuto può cambiare; ad esempio, cliccando su aggiorna quando si
visualizza una discussione in un forum web, potrebbero apparire nuovi commenti. La
differenza fondamentale è che le pagine statiche devono essere generate una sola volta,
dopodiché rimangono invariate sul server, rispetto alle pagine dinamiche che vengono
rigenerate da un server ogni volta che riceve una richiesta.

> ## Esempi nel campo delle scienze della vita
> 
> Un tipico esempio di sito web _statico_ nel campo delle scienze della vita è la
> documentazione di uno strumento o di un formato di file, come questa pagina di
> [wwpdb.org](https://www.wwpdb.org/documentation/file-format).
> 
> Le pagine di ingresso del [database PDB](https://www.rcsb.org/), invece, caricano
> diversamente i contenuti sulla base degli strumenti di visualizzazione e delle opzioni
> scelte dall'utente. Un database o un webserver è di solito un sito web _dinamico_.
> 
{: .callout}

Questa lezione si concentra sui siti statici e sugli strumenti che possono essere usati
per crearli, noti come **Generatori di siti statici**.

Uno dei vantaggi dell'uso dei generatori di siti statici è che eliminano la necessità di
produrre manualmente molto HTML, permettendoci di concentrarci sul contenuto leggibile
che vogliamo che le nostre pagine contengano. Tuttavia, abbiamo bisogno di un modo per
dire al generatore come vogliamo che il nostro contenuto appaia quando viene
visualizzato nel browser. A tale scopo, utilizzeremo uno strumento chiamato Markdown,
che impareremo a conoscere in una puntata successiva.

![Le pagine possono essere create in diversi modi: generazione statica lato server (in
cui l'HTML viene generato una volta sul server e non cambia in seguito), generazione
dinamica lato server (in cui il server può aggiornare e inviare nuovo HTML in base alle
richieste del browser dell'utente) e generazione lato client (in cui parti delle pagine
HTML vengono generate dal browser utilizzando codice
Javascript)](../fig/page-generation-js4ds.svg)

_Figura 1.1: Alternative per la generazione di pagine. Questa figura è una versione
modificata dell'originale pubblicato in [JavaScript for Data Science][js4ds], ed è
riprodotta qui con il permesso dell'autore._

I siti generati staticamente sono un'ottima scelta quando le informazioni che si
desidera visualizzare su un sito web sono le stesse indipendentemente da chi visita il
sito e quando, e se è improbabile che il contenuto delle pagine debba cambiare molto
spesso. Ciò rende i generatori di siti statici una buona scelta per i siti che
forniscono documentazione o contenuti didattici, come questa pagina: lo scopo della
pagina è fornire le stesse informazioni a ogni visitatore. Il visitatore può arrivare,
(si spera) trovare e leggere ciò di cui ha bisogno e andarsene contento e soddisfatto.

I siti dinamici offrono molte più possibilità di fornire interattività e contenuti
personalizzati o di attualità. Tuttavia, la loro creazione è un po' più complicata e
comporta un notevole onere aggiuntivo per il server, non da ultimo in termini di
requisiti computazionali e di sicurezza. Tra l'altro, questo significa che, a differenza
delle pagine statiche (si veda il resto di questa lezione), è improbabile trovare
piattaforme a costo zero che vi aiutino a fornire contenuti dinamici.

> ## Esercizio: Lo strumento perfetto per il lavoro
> 
> Dati i seguenti tipi di siti web, chiedete se un generatore di siti statici è una
> soluzione appropriata per implementarli.
> 
> - (1) Un sito web personale con le sezioni *Chi siamo* e *Progetti*
> - (2) Un forum o una piattaforma di discussione
> - (3) Un blog o un sito di notizie della comunità
> - (4) Un motore di ricerca (come google.com)
> - (5) Un wiki (come wikipedia.com)
> - (6) Un libro online
> 
> > ## Soluzione
> > 
> > - (1) **sito web personale**: Nella maggior parte dei casi, **Sì**. Questo tipo di
> >   contenuto è tipicamente scritto/modificato da una sola persona e destinato ad
> >   avere un accesso di sola lettura per i visitatori.
> > - (2) **forum o discussione**: Molto probabilmente **No**. Un sito web di questo
> >   tipo richiede interattività e modi per identificare chi ha scritto quale
> >   contenuto.
> > 
> > Per le domande 3 e 5 la risposta è sia **Sì** che **No** a seconda dei requisiti e
> > delle funzionalità necessarie.
> > 
> > - (3) **blog/news**: Un semplice blog o un sito di notizie, gestito da un piccolo
> >   gruppo di utenti, è perfettamente realizzabile utilizzando un generatore statico.
> >   Per gruppi molto numerosi di creatori di contenuti o se l'accesso agli articoli
> >   deve essere controllato individualmente, l'uso di un generatore statico porterà a
> >   difficili sfide tecniche.
> > - (4) **motore di ricerca**: Il più delle volte **No**. Implementare qualcosa di
> >   sofisticato come la ricerca di Google sarebbe quasi impossibile con un generatore
> >   statico. Esistono modi per avere un semplice motore che cerca in tutte le pagine
> >   prodotte da un generatore statico utilizzando l'indicizzazione e facendo un uso
> >   intelligente delle caratteristiche del browser, ma questo approccio ha molte
> >   limitazioni.
> > - (5) **wiki**: Un semplice wiki è perfettamente fattibile con un generatore statico
> >   (ad esempio [GitHub Wiki Pages](https://guides.github.com/features/wikis/)), ma
> >   diventa limitante non appena il suo contenuto deve essere modificato o discusso da
> >   molti utenti, come nel caso di Wikipedia.
> > - (6) **libro online**: Sicuramente **Sì**. I generatori statici sono perfetti per
> >   questo tipo di siti web. In genere forniscono modi per evitare la ripetizione dei
> >   contenuti (variabili e modelli), la creazione automatica di una *Tabella dei
> >   contenuti*, e altre chicche.
> > 
> {: .solution }
> 
{: .challenge }

## Pagine GitLab

Se il sito che si vuole creare si adatta bene ai punti di forza di un generatore di siti
statici - è relativamente __piccolo__, sarà __aggiornato di rado__, e il __contenuto non
ha bisogno di essere personalizzato per il visitatore__ - allora crearlo con GitLab
Pages è una buona opzione. GitLab Pages è un sistema che permette agli utenti di creare
e servire siti web direttamente dai loro repository GitLab. Il servizio è gratuito per i
repository pubblici e le pagine semplici possono essere create e servite con pochissima
configurazione.

Esamineremo un elenco di modelli, di complessità crescente. Mentre i primi saranno
basati su semplice Markdown, quelli più avanzati si baseranno su più tecnologie (un
esempio è mostrato nel diagramma sottostante). All'inizio può sembrare opprimente, ma in
questa lezione spiegheremo la maggior parte di queste tecnologie; non tratteremo in
dettaglio solo CSS/Sass (linguaggio di styling che viene compilato in CSS) e
JavaScript/CoffeeScript (linguaggio di scripting che viene compilato in JavaScript).

![Siti web statici nel diagramma della panoramica tecnologica di GitHub
Pages](../fig/jekyll-gh-pages-website-overview.svg){: width="700px" }

Per prima cosa, creeremo un progetto per archiviare i nostri file e impareremo a
scrivere e formattare il contenuto delle nostre pagine usando HTML e Markdown, prima di
configurare GitLab per visualizzare questo contenuto come sito web usando GitLab Pages.

## Impostazione di un progetto

Prima di iniziare a lavorare, dobbiamo creare un progetto in cui lavorare. Questo
progetto è simile a una cartella sul computer, con le differenze principali che la
cartella vive sul web in GitLab/GitHub (anche se è possibile mantenerne una copia sul
computer, se necessario) e che la cartella utilizza un software di controllo di versione
chiamato [`git`](https://git-scm.com/) per tenere traccia delle modifiche ai file. Per i
nostri scopi ignoreremo il software di controllo di versione, anche se può essere utile
se si ha bisogno di tornare a vecchie versioni (si veda [Software Carpentry - Version
Control with Git](https://swcarpentry.github.io/git-novice/) per un'introduzione). In
questa lezione lavoreremo con questa cartella sul web per controllare il sito che
creeremo.

> ## Accedere al proprio account GitLab
> Prima di poter creare un repo, è necessario effettuare il login nel [EMBL
> GitLab](https://git.embl.de/)
> 
{: .callout}

Ci sono due modi per creare un nuovo progetto:

Fare clic sul pulsante "+" nella barra di navigazione in alto e scegliere "nuovo
progetto"

![Plus button](../fig/gitlab-new-navbar.png){: .image-with-shadow width="600px" }

**o**, se siete nella pagina dei progetti, fate clic sul pulsante "Nuovo progetto"

![Pulsante nuovo progetto](../fig/gitlab-nuovo-progetto.png){: .image-with-shadow
width="600px" }

Verrete reindirizzati a una pagina che fornisce tre opzioni:
1. Creare un progetto vuoto
1. Creare da un modello
1. Importazione del progetto Prendete il tempo necessario per leggere le descrizioni dei
   diversi casi. Selezionate "Crea progetto vuoto".

Successivamente dovrete inserire alcune informazioni sul vostro progetto.

![Pagina vuota del nuovo repository](../fig/gitlab_blank_new_repo.png){:
.image-with-shadow width="600px" }

In questa lezione lavoreremo su un sito web generale di gruppo. Potete immaginare che
questo sito sia per il vostro gruppo di laboratorio, per un gruppo di progetto specifico
o per un altro gruppo con cui lavorate. Nel campo "Nome del progetto", digitate
`group-website`.

Il campo `Project slug` determinerà l'URL di accesso al progetto e al sito web; viene
generato automaticamente quando si riempie il campo `Project name`. Lasciarlo così
com'è.

Osservate il menu a tendina accanto al campo `Project URL`. L'opzione predefinita è il
proprio utente, che si riferisce al proprio spazio dei nomi. Potrebbero essere
disponibili altri spazi dei nomi, a seconda dei gruppi a cui si appartiene. Ad esempio,
se questo è il sito web del vostro gruppo, potrebbe essere una buona scelta selezionare
lo spazio dei nomi del vostro gruppo per ospitarlo. Questo sia per fornire un facile
accesso al progetto agli altri membri del gruppo, sia per avere il nome del gruppo (e
non quello dell'utente) nell'URL del sito. Tuttavia, inizializzeremo questo progetto di
prova nel nostro spazio dei nomi.

Possiamo anche aggiungere una descrizione (ad esempio "Progetto per imparare a creare
siti web con le pagine di GitLab") in modo da sapere di che progetto si tratta quando lo
ritroveremo dopo il workshop.

Controlleremo anche l'opzione `Initialize repository with a README`. È buona norma avere
un file README che fornisca ulteriori informazioni sul proprio repo.

> ## GitLab vs GitHub
> 
> La maggior parte dei passaggi qui descritti sono molto simili in GitHub. Ciò che
> GitLab chiama "Progetto", in GitHub è un "Repository", quindi se il vostro istruttore
> confonde i due termini ecco perché. Inoltre, i "Gruppi" sono in GitLab
> "organizzazioni".
> 
> Le differenze più rilevanti riguardano il livello di visibilità e le opzioni di
> configurazione. In GitHub, sono disponibili solo due opzioni per un repository:
> "Pubblico" o "Privato". GitLab dell'EMBL consente una regolazione più specifica dei
> permessi attraverso l'opzione "Interno", cioè accessibile solo all'utente loggato.
> Infine, mentre GitLab permette di inizializzare il repository solo con un README,
> GitHub include l'opzione di inizializzarlo anche con un file .gitignore e di licenza.
> 
{: .callout}

Una volta terminati questi passaggi, si può fare clic sul pulsante `Create Project`.
GitLab imposterà il repo e dovrebbe creare un repo chiamato `group-website` con un file
`README.md` al suo interno. Quello che l'interfaccia grafica ci ha appena aiutato a fare
è fondamentalmente la seguente procedura:

~~~
mkdir group-website
cd group-website
git init
cat > README.md
git add README.md
git commit -m "Initial commit"
~~~
> 
{: .language-bash }

Su un server remoto. Il ramo predefinito è `main`.

![repository Github per il sito web del
gruppo](../fig/gitlab_group_website_project.png){: .image-with-shadow width="800px" }

Prima di passare al capitolo successivo, date un'occhiata ai pulsanti in alto, come `Add
LICENSE`, `Add CHANGELOG` ecc. che vi suggeriscono i possibili passi successivi. Per
citarne uno, la Licenza è sicuramente qualcosa che si potrebbe voler includere nel
proprio progetto. Non ci occuperemo di questo aspetto in dettaglio, ma considerate che
la licenza è una buona pratica (se non addirittura necessaria) per qualsiasi progetto
che includa dati o software. Il vostro sito web, anche se molto semplice e statico,
includerà una sorta di *dati*, anche solo i nomi delle persone. Le tecnologie e i
modelli che userete per generarlo sono *software*. Una parola di saggezza.

[qwantz-easter-egg-ext]:
https://chrome.google.com/webstore/detail/dinosaur-comics-easter-eg/bojkkeeefjmeogpgnlomodfkkfkfhabj
[js4ds]: http://js4ds.org
[html5-tags]: https://www.w3schools.com/TAGS/default.asp

{% include links.md %}

