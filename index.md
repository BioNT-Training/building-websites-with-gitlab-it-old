---
layout: lesson
root: .
permalink: index.html
---


> ## Prerequisiti
> Prima di seguire questa lezione, gli studenti dovrebbero idealmente essere in grado
> di:
> 
> 1. creare un progetto su [GitLab][gitlab] / [EMBL GitLab][embl-gitlab].
> 1. clonare una copia locale di un progetto con Git, aggiungere e fare il commit dei
>    file modificati e fare il push/pull delle modifiche tra i repository locali e
>    remoti.
> 1. eseguire comandi nella shell.
> 
> Nessuno dei prerequisiti sopra elencati è assolutamente necessario per seguire la
> lezione. Tuttavia, saranno necessari per gestire in modo efficiente lo sviluppo del
> sito web dal proprio portatile e per testarne l'aspetto prima di creare versioni
> ufficiali.
> 
> Se volete imparare una qualsiasi delle abilità elencate sopra, le lezioni di [Software
> Carpentry][swc] su [the Shell][swc-shell] e [Git][swc-git] sono un buon punto di
> partenza.
> 
{: .prereq }

Per coloro che hanno già familiarità con i modi in cui Git e una piattaforma online come
GitLab o GitHub possono aiutare a tracciare e confrontare le modifiche ai file di testo
e a collaborare con altri progetti, __GitLab__ (e GitHub) __Pages__ forniscono un modo
gratuito per costruire e ospitare pagine web. Questo approccio è comunemente usato per
fornire documentazione sui progetti software e per creare blog e siti web per individui
e organizzazioni già abituati a lavorare con gli strumenti Git per i loro altri
progetti. Tuttavia, per coloro che muovono i primi passi verso la creazione di siti di
questo tipo, il processo può risultare confuso e intimidatorio. Questo tutorial si
propone di risolvere questo problema
1. fornisce una guida passo-passo alla creazione di una raccolta di pagine,
1. mostra esempi multipli di come strutturarli in un sito coerente,
1. dimostrazione di come usare diversi framework per lo sviluppo di pagine web, dal
   semplice _HTML_ a _Jekyll_ e _Sphinx_.

Verrà anche discussa brevemente la differenza tra lo sviluppo di pagine GitLab e GitHub.

> ## Schermate non aggiornate
> 
> In questa lezione utilizzeremo e mostreremo contenuti e schermate di
> [git.embl.de](https://git.embl.de/). Essendo una piattaforma in continua evoluzione,
> GitLab aggiunge sempre nuove funzionalità e nuovi elementi visivi al suo sito web.
> **Le schermate** della lezione potrebbero quindi risultare non sincronizzate, fare
> riferimento o mostrare contenuti che non esistono più.
> 
> Se durante la lezione si trovano **screenshot** che non corrispondono più a ciò che si
> vede nel browser, si prega di [aprire un
> problema](https://git.embl.de/grp-bio-it-workshops/building-websites-with-gitlab/-/issues)
> descrivendo ciò che si vede e come differisce dal contenuto della lezione. Sentitevi
> liberi di aggiungere tutte le schermate necessarie per chiarire la discrepanza.
> 
{: .callout }

> ## Obiettivi di apprendimento
> 
> Dopo aver seguito questa lezione, gli studenti saranno in grado di:
> 
> - __creare__ contenuti di pagina formattati con _HTML_ o _Markdown_
> - __configurare__ il proprio progetto per costruire e servire pagine su GitLab
> - __costruire__ un semplice sito per ospitare contenuti in semplice _HTML_
> - __costruire__ un sito coerente con più pagine usando il framework _Jekyll_ o
>   _Sphinx_
> - __personalizzare il layout e lo stile delle pagine del loro sito
> 
{: .objectives }

[gitlab]: https://gitlab.com/
[embl-gitlab]: https://git.embl.de/

{% include links.md %}

