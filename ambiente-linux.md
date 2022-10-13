# Preparación de Ambiente Desarrollo Linux

Creado por Álvaro Araya O.

## Ubuntu Linux

Nota: Debe sustituir xyz por el usuario actual en los paths

### configurar sudoers

```bash
sudo nano /etc/sudoers.d/xyz
xyz ALL=(ALL) NOPASSWD:ALL
```

### Generar la llave RSA para autenticación por SSH

```bash
ssh-keygen -b 4096
cat .ssh/id_rsa.pub
```

### Configuración nano

```console
sudo nano /etc/nanorc

set brackets ""')>]}"
set constantshow
set linenumbers
set matchbrackets "(<[{)>]}"
set nonewlines
set tabsize 2
set tabstospaces
set trimblanks

set titlecolor bold,lightwhite,blue
set promptcolor lightwhite,lightblack
set statuscolor bold,lightwhite,green
set errorcolor bold,lightwhite,red
set spotlightcolor black,lime
set selectedcolor lightwhite,magenta
set stripecolor ,yellow
set scrollercolor cyan
set numbercolor cyan
set keycolor cyan
set functioncolor green
```

### Instalación GIT

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update; sudo apt install git

git config --global user.name "nombre-usuario-en-github"
git config --global user.email "correo-en-git-hub"
git config --global init.defaultBranch main
git config --global color.ui true
git config --global core.autocrlf input
git config --global core.eol lf
git config --global core.editor "nano"
git config --global pull.rebase false
git config --global push.default simple
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
git config --global alias.rescue '!git fsck --full --no-reflogs --unreachable --lost-found | grep commit | cut -d\  -f3 | xargs -n 1 git log -n 1 --pretty=oneline > .git/lost-found.txt'
```

### Configuración ZSH

```bash
sudo apt install curl wget zsh -y
sudo usermod -s $(which zsh) $USER
sudo usermod -s $(which zsh) root
```

Instalar la aplicación Terminator

```bash
sudo apt-get install terminator -y
```

Instalar las fuentes recomendadas en:

https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k

Establecer la fuente 'MesloLGS NF' como fuente monospace predeterminada

```bash
sudo add-apt-repository universe
sudo apt install gnome-tweak-tool
```

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Opciones de oh-my-zsh
# (1) (1) (0) (2) (1) (4) (1) (s) (0) (0)

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

mkdir ~/.bin
nano ~/.bin/xyz-env.zsh

# agregar el siguiente texto al archivo

# variables de entorno para zsh
# source "/home/xyz/.bin/xyz-env.zsh"
export JAVA_HOME="/opt/jdk-11"
export GRADLE_HOME="/opt/gradle"
export MAVEN_HOME="/opt/maven"
export NODE_HOME="/opt/node"
export MTR_OPTIONS="-4noLSRDBAWVJMX"
export NMON="cmndl"
export PATH=$JAVA_HOME/bin:$PATH
export PATH=$GRADLE_HOME/bin:$PATH
export PATH=$MAVEN_HOME/bin:$PATH
export PATH=$NODE_HOME/bin:$PATH
export PATH=/home/xyz/.bin:$PATH
export PAGER="/usr/bin/most -s"
HIST_STAMPS="yyyy-mm-dd"
alias l="ls -latrh"

# copiar el source del archivo xyz.env después del export ZSH, por ejemplo:
nano ~/.zshrc
source "/home/xyz/.bin/xyz-env.zsh"
ZSH_THEME="powerlevel10k/powerlevel10k"
ZSH_DISABLE_COMPFIX=true

Agregar los plugins en:

plugins=(git node docker docker-compose)

# ### CERRAR LA TERMINAL Y VOLVER A ABRIR ###
# Opciones de PowerLevel recomendadas
# (y) (y) (y) (y) (1) (1) (1) (2) (2) (1) (2) (4) (1) (2) (2) (y) (2) (y)

```

Para habilitar el mismo ambiente como root:

```bash
sudo -i
ln -s /home/xyz/.zshrc;
ln -s /home/xyz/.oh-my-zsh;
ln -s /home/xyz/.p10k.zsh;
```

### Instalación de Chrome en Ubuntu

```bash
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt update
sudo apt install google-chrome-stable
```

### Dependencias

```bash
sudo -i
cd /opt
wget https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.4.1%2B1/OpenJDK17U-jdk_x64_linux_hotspot_17.0.4.1_1.tar.gz
tar -xvf OpenJDK17U-jdk_x64_linux_hotspot_17.0.4.1_1.tar.gz; rm OpenJDK17U-jdk_x64_linux_hotspot_17.0.4.1_1.tar.gz
wget https://mirrors.ucr.ac.cr/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
tar -xvf apache-maven-3.6.3-bin.tar.gz; rm apache-maven-3.6.3-bin.tar.gz
wget https://services.gradle.org/distributions/gradle-6.8.3-bin.zip
unzip gradle-6.8.3-bin.zip; rm gradle-6.8.3-bin.zip
wget https://nodejs.org/dist/v14.16.0/node-v14.16.0-linux-x64.tar.xz
tar -xvf node-v14.16.0-linux-x64.tar.xz; rm node-v14.16.0-linux-x64.tar.xz

# Las rutas deben quedar de la siguiente manera:
# /opt/
# ├── gradle
# ├── jdk-17
# ├── maven
# └── node

# Para probar las versiones:

mvn --version
java --version
gradle --version
npm --version
node --version
```

### Instalación Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker xyz
sudo systemctl enable docker
sudo apt install docker-compose -y
```

Cerrar sesión y volver a ingresar


### Instalación de MySQL Workbench

```bash
sudo snap install mysql-workbench-community
snap connect mysql-workbench-community:password-manager-service
snap connect mysql-workbench-community:ssh-keys
snap connect mysql-workbench-community:cups-control
```

### Instalación de Visual Studio Code

Descargar el archivo de:
https://code.visualstudio.com/download

```bash
# Descargar el archivo de https://code.visualstudio.com/download según la plataforma
# Ubuntu:
wget https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64
sudo dpkg -i code_1.55.2-1618307277_amd64.deb
```

**Extensiones:**

- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
- [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [Colored console log](https://marketplace.visualstudio.com/items?itemName=rehfres.colored-console-log)
- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- [Prettier - Code Formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [JS & CSS Minifier](https://marketplace.visualstudio.com/items?itemName=olback.es6-css-minify)
- [JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)
- [Reactjs code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.ReactSnippets)
- [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)
- [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer)

Opcionales:

- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
- [One Dark Pro](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme)

**Configuración:**

```json
{
  "editor.formatOnPaste": true,
  "editor.formatOnType": true,
  "prettier.printWidth": 160,
  "prettier.quoteProps": "consistent",
  "prettier.trailingComma": "all",
  "git.enableSmartCommit": true,
  "editor.fontSize": 13,
  "editor.fontFamily": "'MesloLGS NF'",
  "liveServer.settings.donotShowInfoMsg": true,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "workbench.iconTheme": "material-icon-theme",
  "workbench.colorTheme": "One Dark Pro",
  "vsicons.dontShowNewVersionMessage": true,
  "liveServer.settings.donotVerifyTags": true,
  "workbench.startupEditor": "newUntitledFile",
  "terminal.integrated.fontSize": 11,
  "files.eol": "\n",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "prettier.singleQuote": false,
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "files.trimTrailingWhitespace": true,
  "files.trimFinalNewlines": true,
  "editor.fontLigatures": true,
  "editor.tabSize": 2,
  "editor.wordWrapColumn": 160,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.smoothScrolling": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": true,
    "source.organizeImports": true
  },
  "explorer.confirmDragAndDrop": false,
  "editor.detectIndentation": false,
  "editor.useTabStops": false,
  "editor.formatOnSave": true,
  "editor.multiCursorModifier": "ctrlCmd",
  "http.proxyAuthorization": null
}
```

### Instalación de ngrok

Ingresar a:

https://dashboard.ngrok.com/get-started/setup

```bash
unzip /path/to/ngrok.zip
```

Generar el token:

https://dashboard.ngrok.com/get-started/your-authtoken

```bash
nano ~/.ngrok2/ngrok.yml
authtoken: [token]
```
