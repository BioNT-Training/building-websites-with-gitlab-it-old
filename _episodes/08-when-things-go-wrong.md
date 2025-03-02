---
title: Quando le cose vanno male
teaching: 0
exercises: 0
questions: How do I troubleshoot errors in the GitLab pipelines?
objectives:
- Get feedback from GitLab about why a pipeline failed
keypoints:
- If a pipeline fails, GitLab will provide you useful feedback on why
---



## Quando le cose vanno male

Finora abbiamo visto come utilizzare con successo varie tecnologie per produrre un sito
web. Ci sono però alcune situazioni in cui possono fallire a causa di un errore di
battitura o di informazioni mancanti. Esamineremo uno di questi casi con un esempio di
Jekyll.

> ## Esercizio: Risoluzione dei problemi di Jekyll
> 
> Questo esercizio vi aiuterà a riconoscere gli errori più comuni quando lavorate con
> questi elementi di un sito web Jekyll.
> 
> modificate il vostro file `_config.yml` e sostituite un carattere `:` con uno `=` in
> una delle variabili.
> 
> > ## Soluzione
> > 
> > Per esempio, `mail=team@carpentries.org` invece di `mail:team@carpentries.org`.
> > ~~~
> > description: "This research project develops training materials for reseachers wanting to learn to build project
> > websites in GitHub with GitHub Pages."
> > email: "team@carpentries.org"
> > twitter: "https://twitter.com/thecarpentries
> > ~~~
> > {: .language-yaml}
> > 
> > 
> > Se si naviga nel repository GitHub, si può vedere che qualcosa si rompe in
> > `about.md`, dove si usa `{% raw %}{{ site.twitter }}{% endraw %}`, ma,
> > contrariamente a quanto si è visto prima con il Markdown non valido, Jekyll
> > rifiuterà di costruire il sito e produrrà un messaggio di errore.
> > 
> > Vedremo in seguito dove trovare i messaggi di errore e identificarne la causa.
> > 
> {: .solution }
> 
{: .challenge }

Se avete tenuto d'occhio la pagina di esecuzione della pipeline di GitLab fino ad ora
(`CI/CD > Pipelines`), potreste aver notato che una volta che si spinge il risultato
della pipeline "in attesa", poi inizia a "correre" e alla fine "passa". Alla fine. Se
non lo fa, lo stato è "failed", si può ricevere un'email al riguardo (a seconda delle
impostazioni del proprio account GitLab) e non bisogna farsi prendere dal panico. Come
possiamo invece capire cosa ha causato l'errore e risolverlo? Lo stato "failed" è un
pulsante, clicchiamolo.

![cliccare sul pulsante fallito per accedere al log della
pipeline](../fig/gitlab-error.png)

Ancora una volta, si può fare clic sul pulsante ❌ <span style="color:red">pages</span>
per accedere a maggiori dettagli, cioè al registro completo dell'esecuzione della
pipeline. Scorrendo la finestra simile a un terminale, si può vedere come si è avviata,
ha preparato gli ambienti, ha installato le dipendenze e ha eseguito correttamente fino
al comando `bundle exec jekyll build - public`. Lo ricordate? È il comando che lancia
Jekyll, incluso nel file `.gitlab-ci.yml`.

In base a ciò, abbiamo motivo di sospettare che l'errore sia legato all'incapacità di
Jekyll di costruire la pagina. Leggendo più attentamente per ottenere maggiori dettagli,
troviamo:

~~~
$ bundle exec jekyll build -d public
                    ------------------------------------------------
      Jekyll 4.2.1   Please append `--trace` to the `build` command
                     for any additional information or backtrace.
                    ------------------------------------------------
/usr/local/bundle/gems/safe_yaml-1.0.5/lib/safe_yaml/load.rb:143:in `parse': (/builds/hpg_ToyM/0/grp-bio-it/template-pages-jekyll/_config.yml): could not find expected ':' while scanning a simple key at line 3 column 1 (Psych::SyntaxError)
~~~
> 
{: .language-bash }

Questo significa due cose: in primo luogo, il log suggerisce un modo per ottenere
maggiori dettagli, cioè modificare il file `.gitlab-ci.yml` aggiungendo `--trace` al
comando `bundle exec jekyll build -d public`, che diventa così `bundle exec jekyll build
-d public --trace`. Tuttavia, non ne abbiamo bisogno: la frase successiva è abbastanza
chiara. Dice che si è verificato un errore nell'analisi del file `_config.yml` perché
Jekyll non ha trovato il carattere previsto `:`. Poiché questo errore impedisce a Jekyll
di costruire la pagina, il processo non può continuare.

> ## Il fallimento non rimuoverà il vostro sito web
> 
> Dato il fallimento, vi starete chiedendo che fine abbia fatto il sito web Se visitate
> l'indirizzo troverete che il sito è ancora disponibile.
> 
> GitLab manterrà online la versione precedente fino a quando l'errore non sarà risolto
> e una nuova compilazione sarà completata con successo.
> 
{: .callout }

Dovremmo tornare al nostro file `_config.yml` e correggere l'errore `=` che abbiamo
fatto (di proposito, questa volta). Poi si può spingere di nuovo il progetto e il
problema è risolto!

> ## Esercizio: Pratica con la risoluzione dei problemi di Jekyll
> 
> A volte gli errori di battitura possono cambiare il vostro sito web in modo
> sorprendente. Sperimentiamo alcuni possibili problemi e vediamo cosa succede.
> 
> Provare le modifiche elencate di seguito sul file `index.md` e vedere cosa succede
> quando la pagina viene visualizzata. Ogni volta si dovrà correggere l'errore
> precedente.
> 1. Usate una variabile globale o locale che non avete definito prima.
> 2. Lasciare il trattino alla fine dell'intestazione YAML.
> 3. Non mettere uno spazio tra l'intestazione YAML e il resto della pagina
> 4. Mettere l'intestazione YAML in una posizione diversa della pagina.
> 
> > ## Soluzione
> > 
> > 1. Il punto in cui è stata usata la variabile undefined è vuoto, ma per il resto non
> >    ci sono errori. Esempio:
> > 
> >    ~~~
> >    Hi! {% raw %}{{ site.greeting }}{% endraw %}. What have you been up to?
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 2. L'intestazione viene visualizzata in qualche modo nel file e la variabile
> >    definita va alla pagina indice invece che al link impostato.
> > 
> >    ~~~
> >    ---
> >    lesson-example: "https://carpentries.github.io/lesson-example/"
> > 
> >    Examples of our work can be found at: {% raw %}{{ page.lesson-example }}{% endraw %}
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 3. Questo non sembra influire sulla nostra pagina, ma spesso può causare la rottura
> >    di pagine più complesse.
> > 
> >    ~~~
> >    ---
> >    lesson-example: "https://carpentries.github.io/lesson-example/"
> >    ---
> >    Examples of our work can be found at: {% raw %}{{ page.lesson-example }}{% endraw %}
> >    ~~~
> >    {: .language-markdown }
> > 
> > 
> > 4. Questo fa sì che l'intestazione venga visualizzata nella pagina e interrompe il
> >    collegamento variabile creato.
> > 
> >    ~~~
> >    Examples of our work can be found at: {% raw %}{{ page.lesson-example }}{% endraw %}
> >    ---
> >    lesson-example: "https://carpentries.github.io/lesson-example/"
> >    ---
> >    ~~~
> >    {: .language-markdown }
> > 
> {: .solution}
> 
> Nota: assicurarsi di correggere eventuali errori introdotti intenzionalmente nella
> pagina prima di andare avanti.
> 
{: .challenge}


