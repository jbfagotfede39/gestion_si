<!--- Description ----
-- Auteur : Jean-Baptiste Fagot
-- Objectif : Script maintenance logiciels clients
-- Problèmes : 
-- À faire : 
-- Notes : 
 -->

- Application d'aide à la maintenance informatique : [http://data.eaux-jura.com:3838/outils_informatiques/](http://data.eaux-jura.com:3838/outils_informatiques/)

# ssh
- Générer une clé ssh :
```shell
ssh-keygen -b 4096
```
- Afficher une clé ssh :
```shell
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_ed25519.pub
```

# Chocolatey
En ouvrant le PowerShell en mode administrateur

## Installation
```shell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
## Fonctionnement général
- Recherche d'un paquet (ou bien recherche [en ligne](https://community.chocolatey.org/packages)) : 
```shell
choco search --by-id-only firefox
```

- Désinstallation d'un paquet
```shell
choco uninstall firefox
choco uninstall firefox virtualbox vlc
```

- Lister les paquets installés
```shell
choco list -l
```

## Liste générale de paquets
```shell
choco install firefox chrome -y
choco install libreoffice -y
choco install notepadplusplus.install -y
```

## Mises à jour
- Lister les mises à jour
```shell
choco outdated
```

- MAJ d'un unique paquet
```shell
choco upgrade f.lux -y
```

- MAJ de tous les paquets
```shell
choco upgrade all -y
```

# Homebrew
- Installation :
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- Nettoyage :
```shell
brew cleanup
```
- Désinstallation (si nécessaire) :
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall.sh)"
```

## Cask
- [Liste](https://formulae.brew.sh/cask/) des casks
- Recherche d'un cask : 
```shell
brew search rstudio
```

- Informations sur un paquet : 
```shell
brew info zotero
```

- Liste des casks installés :
```shell
brew list --cask --versions
```

- Liste de casks à installer :
```shell
brew install --cask $(cat liste_a_installer.txt)
```

- Export des casks installés avec leurs versions :
```shell
export poste=129
brew list --cask --versions > ${poste}_$(date +%Y-%m-%d_%H-%M-%S)_brew_versions.txt
```

- Mise à jour générale des casks :
```shell
brew update && brew outdated --cask --greedy # --greedy permet d'afficher également les applications qui ont un auto-update d'inclus
brew upgrade --cask --greedy
brew upgrade --cask quarto # Upgrade d'une seule application
brew upgrade --cask quarto,rstudio # Upgrade de plusieurs applications
# brew pin postgresql # Pour figer les MAJ des brew simples, pas des cask
```

- Mise à jour d'une liste spécifique de casks
 ```shell
formulas=("quarto" "rstudio")
for formula in "${formulas[@]}"; do
    brew upgrade "$formula"
done
```

- Travail en cours sur automatisation des MAJ dans 4 terminaux :
 * Lister les MAJ à jour
 * Diviser en 4 paquets : https://stackoverflow.com/questions/31968664/upgrade-all-the-casks-installed-via-homebrew-cask : combiner `brew cask outdated | xargs brew cask reinstall` et `brew upgrade --cask $(brew list --cask)` avec
```
# Exemple de liste
list=(item1 item2 item3 item4 item5 item6 item7 item8 item9 item10 item11 item12 item13 item14)

# Extraire les éléments de l'index 8 à 12
# Notez que les indices commencent à 0, donc l'index 8 est le 9ème élément
extracted_elements=("${list[@]:8:5}")

# Afficher les éléments extraits
echo "Éléments 8 à 12 : ${extracted_elements[@]}"
```

- Requête postgreSQL de nettoyage des changements de version copiés-collés depuis `Homebrew` :
```sql
UPDATE fd_production.informatique_suivimaintenance
SET infutil_description = REPLACE(infutil_description, ') != ', ' -> ')
WHERE infutil_date = '2023-11-04' AND infutil_machine_id = 897;
```

### Liste de formules `brew` générales utiles
```shell
brew install broot
brew install nano
brew install php
brew install tesseract
brew install tesseract-lang
```

### Liste des cask
```shell
# brew install --cask angry-ip-scanner
brew install --cask avast-security
# brew install --cask balenaetcher
# brew install --cask brave-browser
# brew install --cask coteditor
brew install --cask dbeaver-community
brew install --cask deskpad
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
# brew install --cask postman # Formulation de requêtes d'API REST
brew install --cask qgis
# brew install --cask quarto
# brew install --cask r
# brew install --cask raspberry-pi-imager
# brew install --cask raycast
# brew install --cask rstudio
# brew install --cask scribus
brew install --cask skype
# brew install --cask telegram
brew install --cask the-unarchiver
brew install --cask todoist
brew install --cask vlc
# brew install --cask veracrypt
# brew install --cask vnc-viewer
# brew install --cask vscodium
# brew install --cask macfuse # Dans cet ordre 1/3
# brew install borgbackup/tap/borgbackup-fuse # Dans cet ordre 2/3
# brew install --cask vorta # Dans cet ordre 3/3
# brew install --cask wireshark
# brew install --cask wireshark-chmodbpf
brew install --cask xquartz
brew install --cask zoom
# brew install --cask zotero
```

# OSX
- Accès distant : `Réglages système` → `Général` → `Partage` → `Gestion à distance`
- Accès distant : `Réglages système` → `Général` → `Partage` → `Session à distance`
  
- Récupération l'accès aux commandes système :
```shell
export PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
```

- [Aide générale](https://www.cyberciti.biz/faq/apple-mac-os-x-update-softwareupdate-bash-shell-command/)

- Lister les mises à jour :
```shell
softwareupdate -l
```

- Installer une mise à jour (le ` -v` permet d'avoir des détails au fil de l'avancement) :
```shell
softwareupdate  -v --install 'macOS High Sierra 10.13.3 Supplemental Update-'
```

- Installer toutes les mises à jour disponibles :
```shell
sudo softwareupdate -v -i -a
```

- Télécharger une mise à jour sans l'installer
```shell
softwareupdate -d NAME
```

- Outils de développement/Command Line Tools
```shell
sudo xcode-select --install
```

## Dock
- Gestion des applications visibles via [dockutil](https://github.com/kcrawford/dockutil)
```shell
brew install dockutil
dockutil --add /Applications/RStudio.app --after 'Calendrier' --allhomes
dockutil --add /Applications/DBeaver.app --after 'RStudio' --allhomes
dockutil --add /Applications/QGIS.app --after 'DBeaver' --allhomes
dockutil --add /Applications/Zotero.app --after 'QGIS' --allhomes
dockutil --add /Applications/Multifish.app --after 'QGIS' --allhomes
dockutil --remove 'Launchpad'
dockutil --remove 'Messages'
dockutil --remove 'Mail'
dockutil --remove 'Plans'
dockutil --remove 'Photos'
dockutil --remove 'FaceTime'
dockutil --remove 'Calendrier'
dockutil --remove 'Contacts'
dockutil --remove 'Rappels'
dockutil --remove 'Notes'
dockutil --remove 'Freeform'
dockutil --remove 'TV'
dockutil --remove 'Musique'
dockutil --remove 'Keynote'
dockutil --remove 'Numbers'
dockutil --remove 'Pages'
dockutil --remove 'App Store'
```
- Désactiver les applications récemment ouvertes
```shell
defaults write com.apple.dock show-recents -bool FALSE
killall Dock
```

# R
## Installation des packages
```r
install.packages("pak")
pak::pak("jbfagotfede39/afd39")
pak::pak("strboul/caseconverter")
# install.packages('devtools')
# devtools::install_github("jbfagotfede39/afd39")
# devtools::install_github("jbfagotfede39/afd39", upgrade = "never")
# devtools::install_github("jbfagotfede39/aquatools")
# devtools::install_github("jbfagotfede39/aquatools", upgrade = "never")
# devtools::install_github("strboul/caseconverter")
install.packages(c('ade4', 'akima', 'archive', 'attachment', 'basemaps', 'bib2df', 'bookdown', 'checkmate', 'clisymbols', 'colourpicker', 'corrr', 'cronR', 'DT', 'dygraphs', 'elevatr', 'emayili', 'esquisse', 'flextable', 'ggmap', 'ggplotify', 'ggrepel', 'ggsn', 'ggthemes', 'gitcreds', 'gt', 'gtExtras', 'gtsummary', 'hexView', 'hms', 'hrbrthemes', 'htmlTable', 'janitor', 'kableExtra', 'leaflet', 'logr', 'magick', 'magick', 'mapview', 'marquee', 'metR', 'OpenStreetMap', 'osmdata', 'ows4R', 'paletteer', 'palmerpenguins', 'pander', 'pdftools', 'pgirmess', 'qrcode', 'readODS', 'recipes', 'RCurl', 'RefManageR', 'renv', 'reticulate', 'rosm', 'roxygen2md', 'rsconnect', 'RSQLite', 'sassy', 'shiny', 'shinyauthr', 'shinydashboard', 'shinyFiles', 'shinyjs', 'shinyTime', 'styler', 'svglite', 'tidygeocoder', 'tidylog', 'tidyxl', 'usethis', 'vegan', 'viridis'))
```

## Configuration connexion base de données
- Éventuelles mise à jour de la fonction `BDD.ouverture`
```R
keyring::key_set("multifish", "user")
keyring::key_set("eaux-jura-sig-data", "user")
```

## Test de fonctionnement
```R
library(afd39);library(aquatools);library(DBI);library(dbplyr);library(sf);library(tidyverse)
dbD <- BDD.ouverture("Data")
Stations <- sf::st_read(dbD, query = "select * from fd_production.chroniques_stations;")
```

# Python
- Installation de PIP
```shell
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
```

- Installation de packages
```shell
pip3 install pandas
```

# Outils génériques
- [No Sleep](https://nosleep.page/) : le site qui empêche votre ordinateur ou smartphone de passer en veille
