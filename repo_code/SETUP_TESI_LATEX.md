# Configurazione locale della tesi in LaTeX

Questa guida riassume la configurazione utilizzata per scrivere e compilare la tesi Sapienza con VS Code, GitHub e LaTeX su Ubuntu.

## Repository

La repository principale della tesi è:

```text
https://github.com/jacopotdsc/tesi
```

Per clonarla e aprirla in VS Code:

```bash
cd ~/Desktop
git clone https://github.com/jacopotdsc/tesi.git
cd tesi
code .
```

Il file `AGENTS.md` è già presente e non deve essere ricreato dallo script di installazione.

## Repository di codice come riferimenti

Le repository usate come sorgenti tecniche della tesi devono essere aggiunte come Git submodule, non come normali cartelle. In questo modo la repository della tesi registra esattamente il commit del codice utilizzato senza incorporare un'altra repository Git.

Se `mpx/` è già stato aggiunto e Git mostra `adding embedded git repository`, dalla root di `tesi` eseguire:

```bash
git rm --cached -r mpx
git submodule add -f https://github.com/jacopotdsc/mpx.git mpx
git add .gitmodules mpx
git commit -m "Add MPX as thesis reference submodule"
git push
```

Per aggiungere un'altra repository come riferimento si usa lo stesso schema:

```bash
git submodule add URL_REPOSITORY NOME_CARTELLA
git add .gitmodules NOME_CARTELLA
git commit -m "Add code reference submodule"
git push
```

Chi clona la tesi per la prima volta deve usare:

```bash
git clone --recurse-submodules https://github.com/jacopotdsc/tesi.git
```

Se la tesi è già stata clonata:

```bash
git submodule update --init --recursive
```

Per aggiornare successivamente il riferimento di `mpx`:

```bash
git -C mpx pull
git add mpx
git commit -m "Update MPX reference"
git push
```

## Estensione VS Code

Installare l'estensione **LaTeX Workshop** da VS Code oppure da terminale:

```bash
code --install-extension James-Yu.latex-workshop
```

Le scorciatoie principali sono:

- `Ctrl+Alt+B`: compilazione del documento;
- `Ctrl+Alt+V`: visualizzazione del PDF;
- `Ctrl+click` nel PDF: ritorno al punto corrispondente nel sorgente.

## Pacchetti LaTeX

La classe `sapthesis` e i pacchetti usati dal documento sono forniti principalmente da:

```text
texlive-latex-base
texlive-latex-recommended
texlive-latex-extra
texlive-science
texlive-publishers
texlive-fonts-recommended
texlive-lang-english
latexmk
```

Prima dell'installazione è opportuno verificare lo spazio disponibile:

```bash
df -h /
```

Una distribuzione LaTeX può occupare diversi gigabyte. `sudo apt clean` elimina soltanto i pacchetti scaricati conservati nella cache di APT.

## Configurazione di VS Code

Il file `.vscode/settings.json` utilizzato è:

```json
{
  "latex-workshop.latex.autoBuild.run": "onSave",
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.latex.outDir": "%DIR%/build"
}
```

Il PDF e i file temporanei vengono quindi prodotti nella directory `build/`.

## Compilazione

Il comando completo è:

```bash
latexmk -pdf -outdir=build main.tex
```

È stato definito l'alias:

```bash
alias compile_tesi='latexmk -pdf -outdir=build main.tex'
```

Per controllare se esiste:

```bash
type compile_tesi
```

Per compilare e aprire il risultato:

```bash
compile_tesi
xdg-open build/main.pdf
```

Per eliminare i soli file generati da LaTeX:

```bash
latexmk -c -outdir=build main.tex
```

## Controllo dei pacchetti

I file principali possono essere verificati con:

```bash
for package in sapthesis algorithm2e algorithm algpseudocode subcaption subfigure subfloat listings; do
    kpsewhich "$package.sty"
done
```

Se `kpsewhich` non stampa alcun percorso, il relativo pacchetto non è installato.

Quando LaTeX mostra:

```text
Enter file name:
```

non bisogna inserire `main.tex`: significa che manca il file `.cls` o `.sty` indicato subito prima. Inserire `main.tex` caricherebbe nuovamente il documento e causerebbe l'errore `Two \documentclass or \documentstyle commands`. Interrompere invece con `Ctrl+C` e installare il pacchetto mancante.

## Preambolo consigliato

Per evitare definizioni duplicate e pacchetti obsoleti, è preferibile non caricare simultaneamente `algorithm2e` e `algorithm`, né combinare `subcaption` con `subfigure` e `subfloat`.

Una configurazione pulita è:

```latex
\documentclass{sapthesis}

\usepackage[english]{babel}
\usepackage[utf8]{inputenc}
\usepackage{graphicx}
\usepackage{float}
\usepackage{hyperref}
\usepackage{algorithm}
\usepackage{algpseudocode}
\usepackage{subcaption}
\usepackage{amssymb}
\usepackage{comment}
\usepackage{caption}
\usepackage{listings}
\usepackage{xcolor}
```

## Errori incontrati e soluzioni

### `sapthesis.cls not found`

La classe Sapienza è fornita da `texlive-publishers`. Per verificarla:

```bash
kpsewhich sapthesis.cls
```

Se non viene mostrato alcun percorso:

```bash
sudo apt update
sudo apt install texlive-publishers
```

### `Two \documentclass or \documentstyle commands`

Questo errore è comparso perché, davanti al prompt `Enter file name:`, è stato inserito `main.tex`. In questo modo LaTeX ha caricato una seconda volta l'intero documento. Quando compare quel prompt bisogna digitare `x` e premere Invio, quindi installare il file `.sty` o `.cls` mancante.

### `Command \listofalgorithms already defined`

È causato dall'uso contemporaneo di `algorithm2e` e `algorithm`. È stato scelto `algorithm` insieme ad `algpseudocode`:

```latex
\usepackage{algorithm}
\usepackage{algpseudocode}
```

Per rimuovere la configurazione incompatibile:

```bash
sed -i '/algorithm2e/d; /RestyleAlgo/d' main.tex
```

### `Command \c@subfigure already defined`

È causato dall'uso contemporaneo di `subcaption` e `subfigure`. È stato mantenuto soltanto `subcaption`:

```bash
sed -i '/\\usepackage{subfigure}/d; /\\usepackage{subfloat}/d' main.tex
```

### `final exam date but no examiner`

La classe `sapthesis` richiede un esaminatore quando viene specificata `\examdate`. Finché gli esaminatori non sono noti, la data può essere rimossa:

```bash
sed -i '/\\examdate{/d' main.tex
```

Successivamente dovranno essere aggiunti entrambi i campi:

```latex
\examiner{Prof. Nome Cognome}
\examdate{October 2026}
```

### Processi LaTeX sospesi

`Ctrl+Z` sospende la compilazione senza terminarla. I processi sospesi si vedono con:

```bash
jobs
```

Per terminare, ad esempio, i job 1 e 2:

```bash
kill %1 %2
```

Al prompt interattivo di LaTeX è preferibile digitare `x` e premere Invio. Dopo aver corretto il sorgente, pulire e ricompilare:

```bash
latexmk -C -outdir=build main.tex
compile_tesi
```

## Script completo di reinstallazione

Aprire un terminale nella root della repository `tesi` e copiare tutto il blocco seguente. Lo script non modifica `main.tex` e non tocca `AGENTS.md`.

```bash
set -e

echo "Available disk space:"
df -h /

sudo apt clean
sudo apt update
sudo apt install --no-install-recommends \
  latexmk \
  texlive-latex-base \
  texlive-latex-recommended \
  texlive-latex-extra \
  texlive-science \
  texlive-publishers \
  texlive-fonts-recommended \
  texlive-lang-english

if command -v code >/dev/null 2>&1; then
  code --install-extension James-Yu.latex-workshop
else
  echo "Warning: the 'code' command is unavailable; install LaTeX Workshop manually in VS Code."
fi

mkdir -p build chapters figures tables .vscode

if [ ! -f .vscode/settings.json ]; then
  cat > .vscode/settings.json <<'VSCODE_SETTINGS'
{
  "latex-workshop.latex.autoBuild.run": "onSave",
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.latex.outDir": "%DIR%/build"
}
VSCODE_SETTINGS
fi

touch citations.bib

if [ ! -f .gitignore ]; then
  cat > .gitignore <<'GITIGNORE'
build/
*.aux
*.bbl
*.bcf
*.blg
*.fdb_latexmk
*.fls
*.log
*.out
*.run.xml
*.synctex.gz
*.toc
*.lof
*.lot
GITIGNORE
fi

if ! grep -q '^alias compile_tesi=' "$HOME/.bashrc" 2>/dev/null; then
  printf '%s\n' "alias compile_tesi='latexmk -pdf -outdir=build main.tex'" >> "$HOME/.bashrc"
fi

alias compile_tesi='latexmk -pdf -outdir=build main.tex'

echo "Checking the LaTeX installation..."
for package in sapthesis algorithm2e algorithm algpseudocode subcaption listings; do
  package_path="$(kpsewhich "$package.sty" || true)"
  if [ -n "$package_path" ]; then
    echo "FOUND: $package_path"
  else
    echo "MISSING: $package.sty"
  fi
done

if [ ! -f main.tex ]; then
  echo "ERROR: main.tex was not found. Run this script from the thesis repository root."
  exit 1
fi

echo "Compiling main.tex..."
compile_tesi

echo "Setup completed. PDF: $(pwd)/build/main.pdf"
echo "In new terminals, use: compile_tesi"
```
