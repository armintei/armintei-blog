---
title: Bloggen als IT-Nerds
date: 2025-05-26
tags:
  - blog
  - guide
---

Ein Blog ist ein geniales Medium um seine Ideen festzuhalten und mit anderen zu teilen. Daher habe ich beschlossen, einen eigenen Blog ins Leben zu rufen.

Natürlich könnte ich mir jetzt eine generische WordPress-Seite basteln...aber das wäre langweilig. Um etwas Würze in das ganze zu bringen, wird dieser Blog technisch unnötig anspruchsvoll aufgebaut.

Dazu benötigen wir folgende Tools:

- Obsidian
- Hugo
- GitHub

### Installation
*Disclaimer! Ich arbeite auf einem Linux System. Daher richtet sich diese Anleitung eher an Linux User. Ich werde die Schritte für Windows ergänzen.* 
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

Innerhalb von eurem Zielverzeichnis, wird ein neuer Ordner mit eurem Website Namen erstellt. Wir wechseln in diesen hinein und erstellen hier ein leeres git Repository.

Führt diesen Code-Block aus, um git einzurichten, das Theme herunterzuladen und anschließend die hugo Website zu starten. 
```
git init
git config --global user.name "USERNAME"
git config --global user.email "your@mail.com"
git submodule add -f https://github.com/panr/hugo-theme-terminal.git themes/terminal
hugo server -t terminal
```

Filesync
```
sudo rsync -av --delete "Obsidian Vault/Punk Records/Blog" "Documents/armintei/content/posts/"
```

Unser Blog ist jetzt mit Inhalt gefüllt allerdings gibt es noch ein Problem mit den Bildern. Diese werden nicht dargestellt weil unsere Seite die Quelle nicht kennt.
Das lösen wir mit einem Python Script.

```
# Linux 

import os
import re
import shutil

# Paths
posts_dir = "/home/min/Documents/armintei/content/posts/"
attachments_dir = "/home/min/Obsidian Vault/Punk Records/ImageSource/"
static_images_dir = "/home/min/Documents/armintei/static/images/"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
if filename.endswith(".md"):
filepath = os.path.join(posts_dir, filename)
with open(filepath, "r") as file:
content = file.read()

# Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
images = re.findall(r'\[\[([^]]*\.png)\]\]', content)

# Step 3: Replace image links and ensure URLs are correctly formatted
for image in images:

# Prepare the Markdown-compatible link with %20 replacing spaces
markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
content = content.replace(f"[[{image}]]", markdown_image)

# Step 4: Copy the image to the Hugo static/images directory if it exists
image_source = os.path.join(attachments_dir, image)
if os.path.exists(image_source):
shutil.copy(image_source, static_images_dir)

# Step 5: Write the updated content back to the markdown file
with open(filepath, "w") as file:
file.write(content)
 
print("Markdown files processed and images copied successfully.")
```


### Upload to GitHub

In GitHub ein neues Repository erstellen
![[Pasted image 20250526180623.png]]

```
## Generiert einen SSH Key (Mac/Linux/Windows)
cd ~/.ssh
ssh-keygen -t rsa -b 4096 -C "your@mail.com"
```

Lest die .pub Datei aus die erzeugt wurde und speichert den enthaltenen SSH-Key in eurem GitHub-Account.

Um die Verbindung zu testen:
```
ssh -T git@github.com
```
 
Ihr solltet eine Nachricht mit eurem Benutzernamen erhalten.

git remote add origin git@github.com:USERNAME/REPONAME
git add .
git commit -m "Your message"
git push -u origin master




