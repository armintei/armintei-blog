
### Installation

```
curl -s https://ohmyposh.dev/install.sh | bash -s
nano ~/.bashrc 
```

An erster Stelle im Skript hinzufügen, um oh-my-posh beim starten des Terminals automatisch zu initialisieren:
```
# oh-my-posh
export PATH=$PATH:/home/min/.local/bin
```
Außerdem deklarieren wir eine Variable `POSH_THEME="theme.name"` 

Alle themes sind in master repository enthalten. Wir klonen es in einen neuen Ordner `posh-themes`.
```
git clone https://github.com/JanDeDobbeleer/oh-my-posh.git posh-themes
```

Um das festlegen des Themes etwas einfacher zu gestalten, fügen wir noch etwas in der Datei `.bashrc` hinzu.

```
POSH_THEME="theme.name"

eval "$(oh-my-posh init bash --config /home/min/posh-themes/themes/$POSH_THEME.omp.json)"
```
Wir deklarieren eine Variable `POSH_THEME="theme-name"` und brauchen bloß den Namen des gewünschten Themes einfügen.