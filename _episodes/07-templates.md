---
title: Modelli di GitLab
teaching: 0
exercises: 0
questions:
- Where can I find pre-built projects/themes for my site?
objectives:
- Find and fork pre-existing templates to determine the technologies behind a project
  and the styles of the deriving website
keypoints:
- You can find many pre-existing templates for sites on the Internet
- You can find the presented themes for sites in our local GitLab
- You can avoid duplicated effort by basing new layouts on previous ones
---


## Modelli di Bio-IT

I modelli che abbiamo sviluppato insieme sono disponibili nella nostra piattaforma
GitLab:
- [Modello HTML semplice](https://git.embl.de/grp-bio-it/template_pages_html)
- [template Jekyll](https://git.embl.de/grp-bio-it/template-pages-jekyll)
- [template Sphinx](https://git.embl.de/grp-bio-it/template-pages-sphinx)
- [Libro Jupyter](https://git.embl.de/grp-bio-it/template-jupyter-book)

Potrebbero essere leggermente arricchiti rispetto a quanto abbiamo visto in questa
lezione, per esempio il modello HTML semplice presenta anche un file `.css`, ma sono
tenuti al minimo di proposito. Se volete usarli come base per un vostro progetto,
dovreste **fornirli**. Se lo si fa per sviluppare un proprio progetto e non per
contribuire al template stesso, si deve poi **rimuovere la relazione di fork**.
Esaminiamo insieme il processo.

![fork di un repository tramite il pulsante Fork](../fig/template-pages-fork.png)

Fare il fork di un progetto facendo clic sul pulsante "Fork" a destra del titolo del
progetto. Si aprirà un menu (mostrato di seguito) molto simile a quello che appare
quando si apre un nuovo progetto. Si può decidere di mantenere il progetto privato e di
modificarne il titolo e la descrizione. È anche possibile inserirlo nel gruppo/spazio
dei nomi pertinente.

![il menu del progetto fork](../fig/fork-project-menu.png)

Una volta terminato, rimuovere la relazione di fork. È possibile modificare le
impostazioni del progetto nel menu a sinistra della pagina del progetto, seguendo:
`Settings > General > Advanced` e poi scorrere fino alla scheda "Rimuovi relazione di
fork".

![rimuovere la relazione fork](../fig/advanced-settings.png)

Una volta fatto questo, si può clonare il repository in locale e iniziare a modificare
il template. Se avete bisogno di un riassunto su clonazione, biforcazione, push e pull
in Git, date un'occhiata a [questa lezione](https://swcarpentry.github.io/git-novice/)
di The Carpentries.

## Altri modelli

Vi chiedete dove potete trovare altri esempi di progetti di pagine GitLab? Controllate
[questo link](https://gitlab.com/pages). Include più di 40 esempi, basati su diverse
tecnologie. Anche in questi casi, è buona norma rimuovere la relazione di fork se lo
scopo è quello di utilizzare il template per lo sviluppo del proprio sito web e non di
contribuire al template stesso. Alcuni esempi di template presenti in questo repository
sono:
- [**courseware-template**](https://gitlab.com/pages/courseware-template), un template
  basato su Jekyll per il sito web di un corso. Lo si può vedere in azione
  [qui](https://courseware-as-code.gitlab.io/courseware-tutorial/). Include stili per
  formattare i contenuti delle lezioni, i quiz e le diapositive.
- [**hugo blog template**](https://gitlab.com/pages/hugo), il template per [costruire
  blog](https://pages.gitlab.io/hugo/) basato su [Hugo](https://gohugo.io/).
- [**jupyterbook**](https://gitlab.com/pages/jupyterbook), un modello per generare libri
  e documenti che integrano codice Python. Vedetelo reso
  [qui](https://pages.gitlab.io/jupyterbook/intro.html).

Ora avete tutte le competenze necessarie per iniziare a giocare con le pagine di GitLab.
Sentitevi liberi di [contattarci](mailto:bio-it@embl.de) se avete domande o di aprire un
problema nei progetti modello per richiedere funzionalità o sollevare problemi. Siete
anche invitati a contribuire allo sviluppo dei modelli di pagine, sia quelli esistenti
che quelli nuovi che potrebbero adattarsi ai vostri casi d'uso. Infine, consultate il
prossimo capitolo (bonus) per sapere come gestire gli errori nell'esecuzione della
pipeline, per poter risolvere eventuali errori di CI/CD!

{% include links.md %}

