---
title: "Création d'un CV via HUGO"
date: 2020-10-07T00:00:00+01:00
slug: "resume-github-hugo"
tags: [Github Actions, Hugo]
categories: [how-to]
---  

# Création d'un CV via Hugo


Dans l'ensemble des outils de gestion de code source décentralisé, [Git](https://Git-scm.com/) est celui qui domine. Je passe sur l'intérêt d'un gestionnaire de source décentralisé pour aller directement à l'hébergement.

Il y a plusieurs services en ligne proposant Git :
  - [Bitbucket](https://bitbucket.org/) qui a une très belle intégration avec [Jira](https://www.atlassian.com/fr/software/jira)
  - [GitLab](https://about.gitlab.com/) qui autorise une installation on-premise. D'ailleurs [Gnome](https://www.gnome.org/news/2018/05/gnome-moves-to-gitlab-2/) l'utilise ainsi que [freedesktop](https://about.gitlab.com/blog/2018/08/20/freedesktop-org-migrates-to-GitLab/)
  - [GitHub](https://github.com) le player historique qui depuis son [achat par Microsoft](https://news.microsoft.com/announcement/microsoft-acquires-github/) s'intègre de plus en plus dans un éco-système microsoft extrêmement puissant.

Alors pourquoi GitHub... parce que ! Plus sérieusement, 
  - le mécanisme [GitHub actions](https://github.com/features/actions) permet d'avoir un système de déploiement par étage plus simple à mettre en place que Bitbucket.
  - entre GitLab et GitHub, j'ai une légère préférence pour GitHub


## Création d'un dépôt

Une fois votre compte [GitHub](https://github.com/join) activé, il faut se créer un dépôt pour stocker les sources de votre site, blog ou CV.


![Création du dépôt](https://res.cloudinary.com/dswia5bj3/image/upload/s--5R8JPpEP--/f_auto,fl_force_strip.immutable_cache/v1602238713/CV_Hugo_GitHub/nz8mj5_wejc5k.jpg)


Plusieurs éléments important sur cette page :
  1. Vu que c'est un site public, le dépôt doit être public
  2. Nous ajouterons plus tard le **.gitignore**
  3. Concernant la licence, c'est comme vous le souhaitez

Il est intéressant de voir qu'en initialisant le dépôt avec un fichier, GitHub va créer une branche par défaut nommée **main** plutôt que l'ancien terme **master**. C'est suite aux [différents](https://www.zdnet.com/article/mysql-drops-master-slave-and-blacklist-whitelist-terminology/) [mouvements](https://twitter.com/TwitterEng/status/1278733305190342656) pour [l'égalité raciale](https://github.com/rust-lang/rust/pull/74127) et [l'inclusion](https://www.foxbusiness.com/technology/twitter-jpmorgan-replace-racial-coding-terms).

## Configuration du dépôt
Maintenant que le dépôt est créé, nous allons le configurer pour simplifier les prochaines actions.

La première étape est de créer une branche nommée **gh-pages**, pour cela nous allons utiliser le navigateur plutôt qu'une ligne de commande. Le nom gh-pages est "réservé" par GitHub pour les sites web statique (c'est-à-dire sans base de données ou langage de programmation côté serveur). 
 
![Branch Create](https://res.cloudinary.com/dswia5bj3/image/upload/s--SrH-l1rv--/f_auto,fl_force_strip.immutable_cache/v1602238112/CV_Hugo_GitHub/yh8tjg.jpg)


Maintenant que vous avez créé la branche qui contiendra votre CV, vérifier qu'elle est disponible / accessible en allant dans la configuration du dépôt.

![Configure repository](https://res.cloudinary.com/dswia5bj3/image/upload/s--2X2YWrRH--/f_auto,fl_force_strip.immutable_cache/v1602238112/CV_Hugo_GitHub/yhbvgb.jpg)
Nous verrons plus tard comment utiliser un domaine personnalisé.

## Outils en local
Pour éditer votre site web en local, il vous faut :
  - un éditeur de texte, j'utilise [Visual Studio Code](https://code.visualstudio.com) mais [Notepad++](https://notepad-plus-plus.org) fait l'affaire aussi
  - un client Git afin d'interagir avec votre dépôt hébergé chez GitHub

Si vous utilisez Notepad++, je vous conseille d'installer le client officiel [GitHub Desktop](https://desktop.github.com) qui vous donnera une interface graphique simple mais suffisante pour votre dépôt. Si vous utilisez Visual Studio Code, installez un [client en ligne de commande](https://Git-scm.com/downloads). Bien sur, si vous utilisez un linux, utilisez le paquet Git de votre distribution.

Pour ma part, j'utilise <abbr title="Visual Studio Code">VS Code</abbr> qui fournit une interface et [des extensions sympas](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) pour interagir avec Git et me permet de coder dans d'autres langage.
 
Je passe sur l'installation de ces outils car ça ne pose pas de difficulté majeure.

## Récupérer le code

On commence le site en tant que tel en clonant en local le dépôt distant. 

![Menu Git](https://res.cloudinary.com/dswia5bj3/image/upload/s--sCKrMcw_--/f_auto,fl_force_strip.immutable_cache/v1602357609/CV_Hugo_GitHub/nddkmq.jpg)

![clone du dépôt](https://res.cloudinary.com/dswia5bj3/image/upload/s--N9Ci6ecc--/f_auto,fl_force_strip.immutable_cache/v1602357609/CV_Hugo_GitHub/np43lk.jpg)

Ou bien sinon, récupérer l'URL de votre dépôt dans GitHub directement

![Repo URL](https://res.cloudinary.com/dswia5bj3/image/upload/s--PrYXEcXw--/f_auto,fl_force_strip.immutable_cache/v1602358216/CV_Hugo_GitHub/lcoycj.jpg)
Puis en ligne de commande pour avoir en local votre dépôt

```
claudio@mac Projects % git clone https://github.com/obsidienne/cv.git
Cloning into 'cv'...
warning: templates not found in /Users/claudio/.git-templates
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
claudio@mac Projects % 
```

Pour éviter de stocker n'importe quoi dans le dépôt distant, on va rajouter un **.gitignore**. Ne connaissant pas Hugo, je vais aller sur le site [gitignore.io](https://gitignore.io) pour récupérer les fichiers et répertoires à exclure du gestionnaire de source Git 
  - MacOS
  - Visual Studio Code
  - Hugo

![Add .gitignore](https://res.cloudinary.com/dswia5bj3/image/upload/s--9oJ5kcrj--/f_auto,fl_force_strip.immutable_cache/v1602359267/CV_Hugo_GitHub/cxjrjx.jpg)

On ajoute le fichier dans la liste des fichiers à versionner et on commit puis on push.

![stage change](https://res.cloudinary.com/dswia5bj3/image/upload/s--N36P2arN--/f_auto,fl_force_strip.immutable_cache/v1602360089/CV_Hugo_GitHub/u03eor.jpg)

![push change](https://res.cloudinary.com/dswia5bj3/image/upload/s--Awjet3mC--/f_auto,fl_force_strip.immutable_cache/v1602360401/CV_Hugo_GitHub/nrf2av.jpg)

ou en ligne de commande
```
claudio@mac cv % git add .
claudio@mac cv % git commit -m "Add .gitignore"
[main eb34c9a] Add .gitignore
 1 file changed, 57 insertions(+)
 create mode 100644 .gitignore
claudio@mac cv % git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 832 bytes | 118.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/obsidienne/cv.git
   3d85332..eb34c9a  main -> main
claudio@mac cv % 
```

## Hugo

Installons Hugo en téléchargeant la version extended, je le télécharge [directement depuis GitHub](https://github.com/gohugoio/hugo/releases). Une fois que vous l'avez installé.

On initialise le site Hugo

```
claudio@mac cv % ./hugo.darwin new site . --force
Congratulations! Your new Hugo site is created in /Users/claudio/Public/Projects/cv.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
claudio@mac cv % 
```

Choisissez un [thème Hugo](https://themes.gohugo.io/), pour mon CV j'ai pris celui de [almeida](https://themes.gohugo.io/almeida-cv/). Puis on va l'installer.

```
claudio@mac cv % git submodule add https://github.com/ineesalmeida/almeida-cv themes/almeida-cv
Cloning into '/Users/claudio/Public/Projects/cv/themes/almeida-cv'...
warning: templates not found in /Users/claudio/.git-templates
remote: Enumerating objects: 176, done.
remote: Counting objects: 100% (176/176), done.
remote: Compressing objects: 100% (96/96), done.
remote: Total 176 (delta 69), reused 162 (delta 58), pack-reused 0
Receiving objects: 100% (176/176), 3.47 MiB | 6.96 MiB/s, done.
Resolving deltas: 100% (69/69), done.
claudio@mac cv % 
```

On ajoute dans le fichier config.toml, à la racine du site, le thème à utiliser

```
theme = "almeida-cv"
```

On initialise le site avec des données, on le lance

```sh
claudio@mac cv % cp themes/almeida-cv/exampleSite/data/content.yaml data 
claudio@mac cv % cp -r themes/almeida-cv/exampleSite/static/ static   
claudio@mac cv % 
claudio@mac obsidienne.github.io % ../hugo_extended/hugo serve
Start building sites … 

                   | EN  
-------------------+-----
  Pages            |  6  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  8  
  Processed images |  0  
  Aliases          |  1  
  Sitemaps         |  1  
  Cleaned          |  0  

Built in 16 ms
Watching for changes in /Users/claudio/Public/Projects/obsidienne.github.io/{archetypes,content,static,themes}
Watching for config changes in /Users/claudio/Public/Projects/obsidienne.github.io/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Vous pouvez maintenant y accéder via votre navigateur.

## GitHub Action

Qu'est-ce que GitHub Actions, pour simplifier, c'est un automate de déploiement. C'est à dire qu'à chaque fois qu'une condition est remplie, une succession d'actions s'enclenche pour automatiser des tâches répétitives de contrôle qualité et de mise à disposition.

Vous trouverez le fichier à l'adresse [build.yml](https://github.com/obsidienne/obsidienne.github.io/blob/main/.github/workflows/build.yml)

Tout d'abord on spécifie l'évènement qui va déclencher un build. Ici, c'est un **push** sur la branche **main**

```
name: build

on:
  push:
    branches: [main]
```


On défini le job créant le site avec un **name** et l'**runs-on** dans lequel va s'executer le build ainsi que les différentes **steps**

```
jobs:
  build:
    name: Build Hugo Site
    runs-on: ubuntu-latest
    steps:
      - name: Install Hugo
      - name: Checkout main branch
      - name: Checkout gh-pages branch
      - name: Hugo Build
      - name: Copy files
      - name: Commit changes
```

Première étape, créé un environnement Hugo dans l'environnement ubuntu-latest. GitHub Action crée un environnement temporaire, ici [ubuntu-latest](https://docs.github.com/en/free-pro-team@latest/actions/reference/specifications-for-github-hosted-runners) qui correspond au moment où j'ecris à Ubuntu 18.04

Dans cette environnement temporaire, on télécharge une [release d'Hugo](https://github.com/gohugoio/hugo/releases) via curl. 

```
      - name: Install Hugo
        env:
          HUGO_VERSION: 0.75.1
        run: |
          mkdir ~/hugo
          cd ~/hugo
          curl -L "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz" --output hugo.tar.gz
          tar -xvzf hugo.tar.gz
          sudo mv hugo /usr/local/bin
```

Maintenant, on va récupérer dans l'environnement temporaire le code du CV qui se trouve dans la branche **main** mais aussi le site web généré se trouvant dans la branche **gh-pages**.
Pour cela, on utilise l'action [actions/checkout@v2](https://github.com/actions/checkout). Nous avons donc 2 répertoires
  - un contenant le code devant être interprété par Hugo pour générer le site
  - un contenant contenant le site web précedemment généré

```
      - name: Checkout main branch
        uses: actions/checkout@v2
        with:
          ref: main
          path: blog
          submodules: true
      - name: Checkout gh-pages branch
        uses: actions/checkout@v2
        with:
          ref: gh-pages
          path: gh-pages
```


Tout simple, on construit le site et on déplace le site généré dans le répertoire gh-pages.

```
      - name: Hugo Build
        run: cd blog && hugo
      - name: Copy files
        run: cp -rf blog/public/* gh-pages/
```

Un peu plus lourd, mais pas tant que ça. L'idée est de pousser vers la branche gh-pages les modifications apportées lors de la génération du site à l'étape précédente.

N'oubliez pas de changer le nom et le courriel !

```
      - name: Commit changes
        run: |
          cd gh-pages
          Git config --local user.email "bernardes.claudio@gmail.com"
          Git config --local user.name "Claudio Bernardes"
          Git add -A .
          if Git diff-index --quiet HEAD --; then
            echo "No changes..."
          else
            Git commit -m "[CI] build hugo static site"
            Git push
          fi
```



## URL personnalisé
Afin d'avoir une URL personnalisé, il vous faut acheter un domaine. Et donc, 
  1. trouver un super nom de domaine
  2. utiliser un registar, par exemple godaddy, ovh ou encore [bookmyname.com](https://www.bookmyname.com)
  3. prier pour que votre super nom de domaine ne soit pas déjà acheté 


Ensuite, une fois votre domaine acheté, il faut le configurer pour qu'il pointe vers GitHub. Les URL pour les GitHub pages se trouvent dans la doc GitHub

``` 
www                      3600  CNAME obsidienne.github.io.
resume                   3600  CNAME  obsidienne.github.io.
@                        3600  A      185.199.108.153
@                        3600  A      185.199.109.153
@                        3600  A      185.199.110.153
@                        3600  A      185.199.111.153
```


Et pour finir il faut ajouter un fichier CNAME dans la branche gh-pages de votre dépôt. Ce fichier contient le nom de domaine.

![Configure CNAME](https://res.cloudinary.com/dswia5bj3/image/upload/s--A5HdwH0L--/f_auto,fl_force_strip.immutable_cache/v1602252792/CV_Hugo_GitHub/f08ihp.png)

## Faire votre CV
Voilà, vous avez maintenant un site web statique totalement automatisé et accessible depuis une URL personnalisé.
Modifié le fichier data finaliser votre CV, le mien se trouve là https://resume.bernardes.eu

Dans cet exemple, c'est un CV. Mais vous pouvez le faire aussi pour un site de photo (et dans ce cas je vous conseil [cloudinary.com](https://cloudinary.com)) ou un blog.

