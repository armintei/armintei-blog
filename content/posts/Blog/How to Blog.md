---
title: Bloggen für IT-Nerds
date: 2025-05-26
tags:
  - blog
  - guide
---

Ein Blog ist ein schönes Medium, um seine eigenen Gedanken und Ideen mit der Welt zu teilen. Außerdem ist es ein praktisches Journal, auf das man quasi von überall aus Zugriff hat.

Natürlich könnte ich mir jetzt eine generische WordPress-Seite zusammenschustern...aber das wäre ja langweilig. Um etwas Würze in das ganze zu bringen, wird dieser Blog technisch anspruchsvoll aufgesetzt.

Dazu benötigen wir folgende Tools:

- Obsidian
- Hugo
- GitHub

### Installation
*Disclaimer! Ich arbeite auf einem Linux System. Daher richtet sich diese Anleitung eher an Linux User.* 
1. Obsidian
Installiere als erstes [Obsidian](https://obsidian.md/download) falls du es noch nicht hast.
Unter Linux solltest du es mit den gängigen Paketmanagern installieren können.
In meinem Fall(Arch) sieht das wie folgt aus:
`pacman -S obsidian`

2. Hugo
Anschließend geht es weiter mit Hugo. 
Hierfür benötigen wir vorab noch [git](https://git-scm.com/downloads) & [go](https://go.dev/)
Beide sollten standardmäßig unter Linux installiert sein. 
So kannst man das überprüfen:
`git version`
`go version`

Wenn Beides installiert ist, können wir nun Hugo installieren. Dazu gehen wir vor wie bei Obsidian.
`pacman -S hugo`

### Setup
Um eine Seite zu erstellen wechseln wir mit `cd` erstmal in ein Verzeichnis in unserem System in dem wir die Daten speichern wollen. Ich habe habe das ganze in `Documents`erstellt.
`hugo new site $website-name`

![[hugo.png]]

Innerhalb von eurem Zielverzeichnis, wird ein neuer Ordner mit eurem Website Namen erstellt. Wir wechseln in diesen hinein und erstellen hier ein leeres git Repository.
`git init`
`git config --global user.name "USER"`
`git config --global user.email "user@mail.com"`
`git submodule add -f https://github.com/panr/hugo-theme-terminal.git themes/terminal`
`hugo server`

Filesync
`sudo rsync -av --delete "Obsidian Vault/Punk Records/Blog" "Documents/armintei/content/posts/"`



 



