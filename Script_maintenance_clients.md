<!--- Description ----
-- Auteur : Jean-Baptiste Fagot
-- Objectif : Script maintenance logiciels clients
-- Problèmes : 
-- À faire : 
-- Notes : 
 -->

# ssh
- Générer une clé ssh :
``` bash
ssh-keygen -b 4096
```
- Afficher une clé ssh :
``` bash
cat ~/.ssh/id_rsa.pub
```

# Homebrew
- Installation :
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- Désinstallation (si nécessaire) :
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall.sh)"
```

## Cask
- [Liste](https://formulae.brew.sh/cask/) des casks
- Recherche d'un cask : 
``` bash
brew search rstudio
```

- Informations sur un paquet : 
``` bash
brew info zotero
```

- Liste des casks installés :
``` bash
brew list --cask --versions
```

- Export des casks installés avec leurs versions :
``` bash
export poste=129
brew list --cask --versions > ${poste}_$(date +%Y-%m-%d_%H-%M-%S)_brew_versions.txt
```

- Mise à jour des casks :
``` bash
brew update && brew outdated --cask
brew upgrade --cask
# brew pin postgresql # Pour figer les MAJ des brew simples, pas des cask
```

### List de formules générales utiles
```bash
brew install nano
brew install php
```

### Liste des cask
``` bash
# brew install --cask alfred
# brew install --cask angry-ip-scanner
# brew install --cask anydesk
brew install --cask avast-security
# brew install --cask balenaetcher
# brew install --cask brave-browser
# brew install --cask coteditor
brew install --cask dbeaver-community
# brew install --cask docker
brew install --cask firefox
brew install --cask gimp
# brew install --cask github
brew install --cask google-chrome
brew install --cask google-earth-pro
brew install --cask inkscape
# brew install --cask jdownloader
# brew install --cask joplin
brew install --cask libreoffice
brew install --cask libreoffice-language-pack
brew install --cask lifesize
# brew install --cask lulu
# brew install --cask mactex
brew install --cask microsoft-auto-update
brew install --cask microsoft-teams
# brew install --cask middleclick
# brew install --cask multi
brew install --cask nextcloud
# brew install --cask onyx
# brew install --cask openvpn-connect
# brew install --cask oracle-jdk
brew install --cask qgis
# brew install --cask quarto
# brew install --cask r
# brew install --cask rstudio
# brew install --cask scribus
brew install --cask skype
brew install --cask teamviewer
# brew install --cask telegram
brew install --cask the-unarchiver
brew install --cask vlc
# brew install --cask vnc-viewer
# brew install --cask vscodium
# brew install --cask macfuse # Dans cet ordre 1/3
# brew install borgbackup/tap/borgbackup-fuse # Dans cet ordre 2/3
# brew install --cask vorta # Dans cet ordre 3/3
brew install --cask xquartz
brew install --cask zoom
# brew install --cask zotero
```

# OSX
- [Aide générale](https://www.cyberciti.biz/faq/apple-mac-os-x-update-softwareupdate-bash-shell-command/)
- Lister les mises à jour :
``` bash
softwareupdate -l
```

- Installer une mise à jour (le ` -v` permet d'avoir des détails au fil de l'avancement) :
``` bash
softwareupdate  -v --install 'macOS High Sierra 10.13.3 Supplemental Update-'
```

- Installer toutes les mises à jour disponibles :
``` bash
sudo softwareupdate -v -i -a
```

- Télécharger une mise à jour sans l'installer
``` bash
softwareupdate -d NAME
```

# R
## Installation des packages
``` R
install.packages('devtools')
devtools::install_github("jbfagotfede39/aquatools")
devtools::install_github("jbfagotfede39/aquatools", upgrade = "never")
devtools::install_github("jbfagotfede39/afd39")
devtools::install_github("jbfagotfede39/afd39", upgrade = "never")
install.packages(c('ade4', 'akima', 'archive', 'attachment', 'bib2df', 'clisymbols', 'colourpicker', 'corrr', 'cronR', 'DT', 'dygraphs', 'flextable', 'ggmap', 'ggplotify', 'ggrepel', 'gitcreds', 'gt', 'gtExtras', 'gtsummary', 'hrbrthemes', 'janitor', 'kableExtra', 'logr', 'markdown', 'osmdata', 'palmerpenguins', 'pander', 'qrcode', 'RCurl', 'recipes', 'renv', 'RSQLite', 'sassy', 'shiny', 'shinyauthr', 'shinydashboard', 'shinyFiles', 'styler', 'svglite', 'tidygeocoder', 'tidylog', 'tidyxl', 'vegan', 'viridis'))
```

## Test de fonctionnement
``` R
library(afd39);library(aquatools);library(DBI);library(dbplyr);library(ggrepel);library(glue);library(lubridate);library(readxl);library(sf);library(stringr);library(tidyverse)
dbD <- BDD.ouverture("Data")
Stations <- sf::st_read(dbD, query = "select * from fd_production.chroniques_stations;")
```
