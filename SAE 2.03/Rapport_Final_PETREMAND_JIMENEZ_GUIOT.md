# Rapport Final SAE R2.03

:bust_in_silhouette: Equipe: Quentin GUIOT, Shems PETREMAND, Hugo JIMENEZ
 Moodle: https://moodle.univ-lille.fr/course/view.php?id=30827&sectionid=266881
 Référent: Jean Carle - jean.carle@univ-lille.fr

# Table des matières

0.  [**Introduction**](#introduction)
1. [**Préparation de l'environnement virtuel**](#préparation-de-lenvironnement-virtuel)
1.1 - [Préparation d'une machine virtuel Debian](#préparation-d’une-machine-virtuel-debian)
1.2 - [Installation de l'OS](#installation-de-los)
1.3 - [Accès sudo pour user](#accès-sudo-pour-user)
2. [**Installation de Git**](#installation-de-git)
2.1 - [Configuration globale de Git](#configuration-globale-de-git)
3. [**Installation de Gitea**](#installation-de-gitea)
3.1 - [Installation du binaire](#installation-du-binaire)
3.2 - [Préparation de l'environnement Git](#préparation-de-l’environnement-git)
3.3 - [Lancement de Gitea](#lancement-de-gitea)
3.4 - [Paramétrage de Gitea](#paramétrage-de-gitea)
3.5 - [Utilisation de Gitea](#utilisation-de-gitea)
4. [**Conclusion**](#conclusion)
	

# Introduction
Dans le cadre de la SAé-203 Réseau, notre équipe s'est exercée à l'installation et configuration d'un poste de travail type, incluant les outils de bases nécessaire ou favorable au confort d'utilisation, ainsi qu'à la préparation d'un environnement de versionning, ici Gitea. 
Au sein de ce rapport, nous reviendrons sur les différentes étapes de cette mise en oeuvre, en appuyant sur des aspects et questions techniques ainsi que sur les éventuelles difficultées rencontrées. 
Le rapport est appuyé d'images, majoritairement des screenshot issus des diverses installations afin de démontrer le bon déroulé du processus.

## 1. Préparation de l'environnement virtuel

### 1.1 - Préparation d’une machine virtuel Debian

- ***Question(s) 1.* Configuration matérielle dans VirtualBox**
    
    > Que signifie “64-bit” dans “Debian 64-bit” ?
    
    Dans “Debian 64-bit”, le “64-bit” correspond à la taille des registres du processeur.
    
    Un processeur 64 bits est favorisé par rapport un processeur 32 bits car il permet de traiter de grandes quantités de mémoire plus efficacement avec une mémoire de 4 Go, 8 Go, 16 Go ou plus contrairement au processeur 32 bits qui lui a une mémoire vive de 2 Go et un espace disque de 20 Go maximum.
    
    > Quelle est la configuration réseau utilisée par défaut ?
    
    Par défaut, lors de l’installation de la machine virtuel nous avons configurer le mirroir Debian de ‘polytech-lille’ et le proxy associé.
    
     
    
    > Quel est le nom du fichier XML contenant la configuration de votre machine ?
    
    Le fichier contenant la configuration de la machine se nomme `SAE203.vbox`.
    
    > Sauriez-vous le modifier directement ce fichier pour mettre 2 processeurs à votre machine ?
        
    Il est possible de modifier ce fichier en ajoutant `count='2'` dans `<Hardware>` à la suite de CPU → `<CPU count='2'>` 
    

---
### 1.2 - Installation de l'OS

- ***Question(s) 2.* Installation OS de base**
    
    > Qu’est-ce qu’un fichier iso bootable ?
    
    Un fichier ISO bootable est un fichier image qui peut être utilisé pour créer un disque de démarrage ou une clé USB de démarrage,  qui est souvent utilisée pour installer un système d'exploitation, tels que Windows, Linux ou MacOS, sur un ordinateur ou pour exécuter des programmes de récupération système.
    
    > Qu’est-ce que MATE ? GNOME ?
    
    GNOME est un environnement de bureau open-source pour les systèmes d'exploitation de type Unix, qui fournit une interface utilisateur graphique conviviale et des fonctionnalités utiles pour les utilisateurs de ces systèmes.
    
    MATE est également un environnement de bureau open-source, basé sur GNOME. Il fournit une gamme complète de fonctionnalités, applications et options de personnalisation pour les utilisateurs de ces systèmes.
    
    > Qu’est-ce qu’un serveur web ?
    
    Un serveur web est un logiciel qui stocke et distribue des fichiers sur Internet, comme des pages web, des images, des vidéos, etc. Il répond aux demandes des navigateurs web pour afficher ces fichiers en utilisant le protocole HTTP.
    
    > Qu’est-ce qu’un serveur ssh ?
    
    Un serveur SSH est différent d’un serveur car le serveur web est conçu pour stocker et diffuser des fichiers sur Internet, tandis que le serveur SSH permet d’établir une connexion sécurisée à distance à un ordinateur ou un serveur.
    
    > Qu’est-ce qu’un serveur mandataire ?
    
    Un serveur mandataire est un serveur informatique qui a pour fonction de relayer des requêtes entre un poste client et un serveur. Il agit comme un tampon en améliorant les performances, la sécurité et la confidentialité des connexions réseau.
    

---

### 1.3 - Accès `sudo` pour user
- ***Question(s) 3.* sudo**
    
    > Comment peux-ton savoir à quels groupes appartient l’utilisateur user ? 
   
    Pour savoir à quel groupe appartient l’utilisateur user, on peut utiliser la commande `sudo groups user` .
    
    > Quel est la version du noyau Linux utilisé par votre VM ? N’oubliez pas, comme pour toutes les questions, de justifier votre réponse.
    
    La version de notre noyau Linux utilisé est **Debian 11.6.0-amd64** comme indiquer dans les consignes lors de la mise en place de la VM. On peut connaître la version de notre noyau (aussi appelé Kernel) en utilisant la commande `uname -v` dans un terminal.
    
    > À quoi servent les suppléments invités ? Donner 2 principales raisons de les installer.
    
    Les suppléments invités permettent d'améliorer l'expérience utilisateur et les performances de la machine virtuelle en lui fournissant des fonctionnalités supplémentaires et une meilleure intégration avec l'hôte. Les principales raisons de les installer sont : 
    
    1. *Meilleure résolution d'écran :* sans les suppléments invités, la machine virtuelle peut être limitée à une résolution d'écran basse, ce qui peut rendre l'utilisation de certains logiciels difficile. Les suppléments invités permettent de définir une résolution d'écran plus élevée, ce qui améliore l'affichage.
    2. *Partage de fichiers et copier-coller entre la machine hôte et la machine virtuelle :* les suppléments invités permettent de partager des fichiers entre la machine hôte et la machine virtuelle, ce qui facilite le transfert de données. Mais il est également possible de copier-coller du texte et des fichiers entre la machine hôte et la machine virtuelle, ce qui facilite le travail entre les deux environnements.
    
    > À quoi sert la commande `mount` (dans notre cas de figure et dans le cas général) ?
    
    La commande mount premet de demander au système d’exploitation de rendre un système de fichiers accesibles, à un emplacement spécifié (le point de montage).
    
    Dans notre cas de figure, `mount` nous a servit pour installer “VirtualBox Guest Additions” qui est un ensemble de pilotes et de logiciels supplémentaires qui améliorent les performances et les fonctionnalités des systèmes d'exploitation invités dans VirtualBox.
    

## 2. Installation de Git

Dans cette section, nous verrons comment installer et configure l'outil **Git**.

### 2.1 - Configuration globale de git

Installation de git :

`sudo apt install git-gui`

- ***Questions 1.* Préliminaire**

> Qu’est-ce que le logiciel *git-gui* ? Comment se lance-t-il ?

Le logiciel *git-gui* est est l’interface graphique de ***Git*** qui est en ligne de commande.
Git-gui fournit une interface utilisateur graphique pour effectuer des opérations Git courantes telles que la création de commits, la fusion de branches et la gestion des conflits. mais toutes les possibilités offertes par Git ne sont pas disponibles dans Git Gui.

Pour le lancer il suffit simplement de faire la commande `git gui` dans un terminal.

- *Source :* [https://www.codeur-pro.fr/](https://www.atlassian.com/)

> Qu’est-ce que le logiciel *gitk* ? Comment se lance-t-il ?

Gitk est un logiciel graphique de visualisation d'historique Git. Il permet de visualiser l'historique des commits et des branches, ainsi que les différences entre les versions d'un fichier.

Pour le lancer il suffit simplement de faire la commande `gitk` dans un terminal.

- *Source :* [https://www.atlassian.com/](https://www.atlassian.com/)

> Quelle sera la ligne de commande *git* pour utiliser par défaut le proxy de l’université sur tous vos projets git ?

```bash
export http_proxy=http://cache.univ-lille.fr:3128
export https_proxy=http://cache.univ-lille.fr:3128
```


## 3. Installation de Gitea

- ***Question(s) 2.* À propos de Gitea**

> Qu’est ce que Gitea ?

Gitea est une plateforme d'hébergement de code open source et légère pour Git, permettant de gérer des dépôts de code source et des collaborations de manière simplifiée.

> À quels logiciels bien connus dans ce domaine peut-on le comparer (en citer au moins 2) ?

On peut le comparer à **GitLab** et **GitHub**.

### 3.1 - Installation du binaire

Téléchargement du binaire :

```bash
wget -O gitea https://dl.gitea.com/gitea/1.18.5/gitea-1.18.5-linux-amd64
chmod +x gitea
```

Vérification de la signature avec la clé GPG (pour éviter toutes modifications du binaire) :

```bash
gpg --keyserver keys.openpgp.org --recv 7C9E68152594688862D62AF62D9AE806EC1592E2
gpg --verify gitea-1.18.5-linux-amd64.asc gitea-1.18.5-linux-amd64
```

---

### 3.2 - Préparation de l’environnement Git

Vérification de la version de Git (doit être ≥ 2.0 pour fonctionner) : 
`git --version`

Création de l’utilisateur pour démarrer Git :

```bash
adduser \
   --system \
   --shell /bin/bash \
   --gecos 'Git Version Control' \
   --group \
   --disabled-password \
   --home /home/git \
   git
```

Création de la structure du répertoire nécessaire :

```bash
mkdir -p /var/lib/gitea/{custom,data,log}
chown -R git:git /var/lib/gitea/
chmod -R 750 /var/lib/gitea/
mkdir /etc/gitea
chown root:git /etc/gitea
chmod 770 /etc/gitea
```

Configuration du répertoire :

```bash
export GITEA_WORK_DIR=/var/lib/gitea/

#Copie du binaire Gitea dans un emplacement global
cp gitea /usr/local/bin/gitea
```

---

### 3.3 - Lancement de Gitea

Démarrage automatique de Gitea au lancement de la machine :

- Créer le fichier `/etc/systemd/system/gitea.service` et enregistrer le contenu suivant à l’intérieur :
    
    ```bash
    [Unit]
    Description=Gitea (Git with a cup of tea)
    After=syslog.target
    After=network.target
    ###
    # Don't forget to add the database service dependencies
    ###
    #
    #Wants=mysql.service
    #After=mysql.service
    #
    #Wants=mariadb.service
    #After=mariadb.service
    #
    #Wants=postgresql.service
    #After=postgresql.service
    #
    #Wants=memcached.service
    #After=memcached.service
    #
    #Wants=redis.service
    #After=redis.service
    #
    ###
    # If using socket activation for main http/s
    ###
    #
    #After=gitea.main.socket
    #Requires=gitea.main.socket
    #
    ###
    # (You can also provide gitea an http fallback and/or ssh socket too)
    #
    # An example of /etc/systemd/system/gitea.main.socket
    ###
    ##
    ## [Unit]
    ## Description=Gitea Web Socket
    ## PartOf=gitea.service
    ##
    ## [Socket]
    ## Service=gitea.service
    ## ListenStream=<some_port>
    ## NoDelay=true
    ##
    ## [Install]
    ## WantedBy=sockets.target
    ##
    ###
    
    [Service]
    # Uncomment the next line if you have repos with lots of files and get a HTTP 500 error because of that
    # LimitNOFILE=524288:524288
    RestartSec=2s
    Type=simple
    User=git
    Group=git
    WorkingDirectory=/var/lib/gitea/
    # If using Unix socket: tells systemd to create the /run/gitea folder, which will contain the gitea.sock file
    # (manually creating /run/gitea doesn't work, because it would not persist across reboots)
    #RuntimeDirectory=gitea
    ExecStart=/usr/local/bin/gitea web --config /etc/gitea/app.ini
    Restart=always
    Environment=USER=git HOME=/home/git GITEA_WORK_DIR=/var/lib/gitea
    # If you install Git to directory prefix other than default PATH (which happens
    # for example if you install other versions of Git side-to-side with
    # distribution version), uncomment below line and add that prefix to PATH
    # Don't forget to place git-lfs binary on the PATH below if you want to enable
    # Git LFS support
    #Environment=PATH=/path/to/git/bin:/bin:/sbin:/usr/bin:/usr/sbin
    # If you want to bind Gitea to a port below 1024, uncomment
    # the two values below, or use socket activation to pass Gitea its ports as above
    ###
    #CapabilityBoundingSet=CAP_NET_BIND_SERVICE
    #AmbientCapabilities=CAP_NET_BIND_SERVICE
    ###
    # In some cases, when using CapabilityBoundingSet and AmbientCapabilities option, you may want to
    # set the following value to false to allow capabilities to be applied on gitea process. The following
    # value if set to true sandboxes gitea service and prevent any processes from running with privileges
    # in the host user namespace.
    ###
    #PrivateUsers=false
    ###
    
    [Install]
    WantedBy=multi-user.target
    ```
    

Effectuer ces successions de commande dans le terminal, afin d’activer et démarrer Gitea à chaque démarrage de la machine :

```bash
# Enable and start Gitea at boot
sudo systemctl enable gitea
sudo systemctl start gitea

# If you have systemd version 220 or later, you can enable and immediately start Gitea at once by:
sudo systemctl enable gitea --now
```

---
-> **ETAPE OPTIONNELLE**
*Réaliser cette étape si le démarrage de Gitea échoue.*

Installation de ***supervisor*** :

```bash
# Install supervisor by running below command in terminal
sudo apt install supervisor

# Create a log dir for the supervisor logs
# /!\ En supposant que Gitea est installé dans "/home/git/gitea/"
mkdir /home/git/gitea/log/supervisor
```

Création du fichier configuration de ***supervisor*** :

- Créer le fichier `/etc/supervisor/supervisord.conf` et enregister le contenu suivant à l’intérieur :
    
    M*odifiez les paramètres d'utilisateur (`git`) et d'accueil (`/home/git`) pour qu'ils correspondent à l'environnement de déploiement. Modifiez le PORT ou supprimez l'indicateur -p si le port par défaut est utilisé.*
    
    ```bash
    [program:gitea]
    directory=/home/git/go/src/github.com/go-gitea/gitea/
    command=/home/git/go/src/github.com/go-gitea/gitea/gitea web
    autostart=true
    autorestart=true
    startsecs=10
    stdout_logfile=/var/log/gitea/stdout.log
    stdout_logfile_maxbytes=1MB
    stdout_logfile_backups=10
    stdout_capture_maxbytes=1MB
    stderr_logfile=/var/log/gitea/stderr.log
    stderr_logfile_maxbytes=1MB
    stderr_logfile_backups=10
    stderr_capture_maxbytes=1MB
    user = git
    environment = HOME="/home/git", USER="git"
    ```
    
    Activation et démarrage automatique de ***supervisor :***
    
    ```bash
    sudo systemctl enable supervisor
    sudo systemctl start supervisor
    ```
    
    *Si vous avez systemd version 220+, vous pouvez activer et démarrer immédiatement le superviseur avec :*
    
    ```bash
    sudo systemctl enable supervisor --now
    ```
    
---
Démarrage via le terminal :

```bash
GITEA_WORK_DIR=/var/lib/gitea/ /usr/local/bin/gitea web -c /etc/gitea/app.ini
```

Redémarrage de Gitea avec **systemd** (recommandé) : `systemctl restart gitea`

*Si le démarrage échoue, réaliser l'étape optionnelle précédant celle-ci.*

---

### 3.4 - Paramétrage de Gitea

Vérifier que le service est bien démarré avec : `systemctl status gitea.service`

Utiliser le navigateur physique de la machine et se rendre sur l’url suivant : [http://localhost:3000](http://localhost:3000)

Arrivée sur l’interface de Gitea

![Illustration configuration Gitea](https://i.imgur.com/dFUS2sV.png)

Début du paramètrage avec les informations nécessaires :

- La base de données sera `SQLite3` ;
- Le compte administrateur web sera :
    - Nom : gitea
    - Password : gitea
    - Email : git@localhost

![Illustration création utilisateur Gitea](https://i.imgur.com/ZK3nbNx.png)

→ A la fin de l’installation, ne pas oublier de protéger `/etc/gitea` et `/etc/gitea/app.ini` :

```bash
chmod 750 /etc/gitea
chmod 640 /etc/gitea/app.ini
```

- ***Question(s) 3.* Mise à jour**

> Comment faire pour la mettre à jour sans devoir tout reconfigurer ? Essayez en mettant à jour vers la version 1.19.

Pour mettre à jour Gitea tout en conservant la configuration existante, vous pouvez suivre les étapes suivantes :

1.  Sauvegardez vos données : **Avant toute mise à jour, il est recommandé de sauvegarder vos données Gitea, y compris la base de données et les fichiers de configuration.**
    
2.  Téléchargez la nouvelle version de Gitea : Rendez-vous sur le [site officiel de Gitea](https://gitea.io/en-us/) pour télécharger la dernière version stable de Gitea.
    
3.  Arrêtez le service Gitea : Arrêtez le service Gitea sudo avec la commande suivante : `sudo systemctl stop gitea`
    
4.  Faites une copie des fichiers de configuration : Faites une copie des fichiers de configuration de Gitea (généralement situés dans le répertoire `/etc/gitea`) *(et des fichiers de log s'ils existent)*.
    
5.  Installez la nouvelle version de Gitea : Installez la nouvelle version de Gitea en [suivant les instructions](https://docs.gitea.io/en-us/upgrade-from-gitea/).
    
6.  Copiez les fichiers de configuration : Copiez les fichiers de configuration de l'étape 4 dans le répertoire de configuration de la nouvelle installation. Assurez-vous de remplacer les fichiers de configuration de la nouvelle installation par ceux que vous avez sauvegardés.
    
7.  Redémarrez le service Gitea : Redémarrez le service Gitea en utilisant la commande suivante : `sudo systemctl start gitea`
    
8.  Vérifiez que tout fonctionne correctement : Ouvrez votre navigateur et accédez à votre instance Gitea pour vérifier que tout fonctionne correctement.
---

### 3.5 - Utilisation de Gitea

Création d’un projet depuis l’interface Gitea :
![Illustration création projet Gitea](https://i.imgur.com/mQ4Nt1p.png)

![Illustration création projet Gitea 2](https://i.imgur.com/8c93KCn.png){ width=800px, height=600px }

![Illustration création projet Gitea 3](https://i.imgur.com/MNsOPum.png){ width=800px, height=600px }

- ***Question(s) 4.* Projets existans**

> Que se passe-t-il ? Qu’elle semble en être la cause ? Corrigez ce problème.

Nous avons remarquer aucun problème lors de la réalisation des étapes finales.

# Conclusion

Au cours de cette SAé l'ensemble de notre équipe a pu bénéficier d'un apprentissage théorique, au travers de diverses questions techniques, mais surtout pratiques, en s'exerçant directement, en manipulant les premiers outils et technologies, le tout en apprenant à faire face aux difficultées et à les surmonter, ce en respectant des deadlines mais aussi une méthode de travail encadrée, via notamment la rédaction du rapport précédent ainsi que de celui-ci. Ce savoir-faire nous est par ailleurs directement utile pour la gestion de nos projets et travaux au sein de l'IUT, et ceux à venir.
