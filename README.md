# Docker compose advanced media
Guide d'installation d'outils d'automatisation et de gestion de téléchargements touts médias, stable et safe, pour Plex (ou autre).

<h2>Caractéristiques</h2>
Stack utilisé sur un Synology DS918+, DSM 7.1.1-42962 Update 6 mais cela devrait fonctionner avec n'importe quel serveur sur lequel on peut installer Docker.

<i>Toutes les app sensibles passent à travers un client VPN, donc avoir un compte chez un fournisseur VPN est requis pour utiliser tout cela.</i>

<ol>
    <li>Créer un dossier partagé "docker", puis, dedans, le dossier "portainer"</li>
    <li>Installer Docker (ou Container Manager dans DSM 7.2) : https://linuxhint.com/run-docker-containers-synology-nas/</li>
    <li>Installer "portainer-ce" dans Docker : https://mariushosting.com/how-to-install-portainer-on-your-synology-nas/</li>
    <li>Créer les dossiers suivant* dans le dossier partagé "docker" :
    bazarr
    flaresolverr
    gluetun 
    jackett
    overseerr
    qbittorrent
    radarr
    slskd
    sonarr
    watchtower</li>
    <li>Créer une stack sur Portainer du nom que vous voulez, avec le Web editor : https://docs.portainer.io/user/docker/stacks/add#option-1-web-editor</li>
    <li>Copier/coller le code docker-compose que j'ai rédigé ici pour installer l'ensemble des containers que j'ai sélectionné* : https://github.com/Pandaarr/docker-compose-advanced-media/blob/main/stack-portainer-ce
    <li>Editer les 'XXXX' ainsi que les PUID, PGID et volumes pour que cela fonctionne avec votre systeme</li>
    PS : Pour connaitre le PUID et PGID d'un utilisateur que vous avez cree via l'interface de votre Synology : https://mariushosting.com/synology-how-to-find-uid-userid-and-gid-groupid/
    <li>Cliquer sur "Deploy the stack" tout en bas (vous inquiétez pas, c'est éditable à volonté si jamais vous zappé un truc !)</li>
    <li>Configurer l'ensemble des images installées avec leurs doc officielles (lien en commentaire dans le code du github)</li>
</ol>



*Liste des containers présents dans la stack suggérée et leurs fonctionnalités :

<ul>
    <li>Radarr
    Automatisation et gestion de téléchargement de films : https://radarr.video/</li>
    <li>Sonarr
    Automatisation et gestion de téléchargement de séries : https://sonarr.tv/</li>
    <li>Bazarr
    Automatisation et gestion de téléchargement de sous-titres pour films et séries : https://www.bazarr.media/</li>
    <li>Overseerr
    Outil de gestion des requêtes (les vôtres et celles des utilisateurs de votre Plex) et de découverte de médias conçu pour fonctionner avec Plex, Radarr et Sonarr : https://overseerr.dev/</li>
    <li>Gluetun
    Client VPN pour plusieurs fournisseurs VPN, écrit en Go et utilisant OpenVPN ou Wireguard, DNS sur TLS, avec quelques serveurs proxy intégrés : https://github.com/qdm12/gluetun#features</li>
    <li>Flaresolverr (passe par gluetun)
    Serveur proxy pour contourner la protection Cloudflare et DDoS-GUARD, à renseigner dans Jackett : https://github.com/FlareSolverr/FlareSolverr</li>
    <li>Jackett (passe par gluetun)
    Passerelle entre vos trackers torrent et Radarr, Sonarr... : https://github.com/Jackett/Jackett</li>
    <li>qBittorrent (passe par gluetun)
    Client torrent de qualité : https://www.qbittorrent.org/</li>
    <li>Soulseek (slskd) (passe par gluetun)
    Aaaah, enfin Soulseek version serveur ! Pour moi, c'est le meilleur réseau de partage de musique, on trouve tout (bon, je cherche quasi que du metal hein !).
    L'interface mobile est fonctionnelle, idéal pour ajouter des albums sur Plex quand on vous recommande un groupe entre deux bières : https://github.com/slskd/slskd</li>
    Watchtower
    <li>MAJ automatique de toutes les images de vos containers ne contenant pas le label 'com.centurylinklabs.watchtower.enable: "false"'</li>
</ul>
