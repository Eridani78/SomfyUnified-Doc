# Plugin **SomfyUnified**
<img src="/docs/assets/images/SomfyUnified-Image.png" alt="" style="height: 40%; width:40%;"/>
<img src="/SomfyUnified-Doc/assets/images/SomfyUnified-Image.png" alt="SomfyUnified logo" style="height: 40%; width:40%;"/>


## Presentation
Le plugin **SomfyUnified** est destiné à permettre une interface entre Jeedom et les équipements de l'écosystème Somfy connectés via les API OverKiz et appartenant aux familles listées ci-dessous:
- Somfy TaHoma Cloud
- Somfy TaHoma Local
- Atlantic Cozytouch
- Brandt Smart Control
- Flexom
- Hexaom HexaConnect
- Hitachi Hi Kumo
- Nexity Eugénie
- Rexel Energeasy Connect
- Simu (LiveIn2)
- Ubiwizz


## Compatibilité
Le plugin **SomfyUnified** est compatible des systèmes fonctionnant sous Debian 10, 11 & 12.


## Statut de validation du plugin

Compte-tenu de la grande diversité d'équipements susceptibles d'être gérés par le plugin, il est impossible, pour le développeur, d'avoir pu valider tous les types d'équipements.<br>
Les validations se feront donc au fur et à mesure de l'adoption du plugin par les utilisateurs qui accepteront de tenter son intégration.

Compte-tenu de l'état d'avancement, l'état de validation des différentes familles d'équipements est donné dans le tableau suivant:

| Equipement                 |  Type API  |  Etat de validation |
| :------------------------- | :--------: | :-----------------: |
| Somfy TaHoma Cloud         | cloud      | validé              |
| Somfy TaHoma Local         | local      | validé              |
| Atlantic Cozytouch         | cloud      | en attente          |
| Brandt Smart Control       | cloud      | en attente          |
| Flexom                     | cloud      | en attente          |
| Hexaom HexaConnect         | cloud      | en attente          |
| Hitachi Hi Kumo            | cloud      | en attente          |
| Nexity Eugénie             | cloud      | en attente          |
| Rexel Energeasy Connect    | cloud      | en attente          |
| Simu (LiveIn2)             | cloud      | en attente          |
| Ubiwizz                    | cloud      | en attente          |


## Ecosystème Somfy/TaHoma
L'écosystème Somfy TaHoma comprend, à ce jour, de nombreux partenaires et est susceptible de continuer à s'étoffer et évoluer.
Cela signifie qu'une box des familles de l'écosystème (TaHoma, Cozytouch, ...) peut s'interfacer à de nombreux dispositifs très différents les uns des autres pour les piloter.
On trouve actuellement dans l'écosystèmes Somfy le contrôle de dispositifs tels que des systèmes de controle d'ouverture ou fermeture d'ouvrants (volets roulants, portes, stores, ...), des systèmes d'alarme, des systèmes de chauffage et climatisation, ...

L'absence de documentation de la part de Somfy sur les commandes des dispositifs rend la syntaxe de ces opérations particulièrement difficile à anticiper et implémenter dans un plugin et ce, à priori.

Afin de s'adapter au mieux à une telle diversité de commandes ou données potentielles, deux modes de fonctionnement du plugin ont du être implémenté.


## API locale Somfy
A suivre ...

## FAQ
| 01  | Mon équipement a été créé mais il n’y a aucune commande qui n’apparait ?  |
| :-: | :------------------------------------------------------------------------ |
|     | L’équipement n’est pas (encore) intégré dans la base de donnée (BdD) du plugin. A l’aide de l’explorateur de fichier Jeedom, se rendre dans le répertoire: userData/components. Créer une archive .zip du répertoire **undefined** puis la renommer en y ajoutant .txt à la fin. Envoyer ce fichier créer au concepteur du plugin (en MP) afin que l’équipement puisse être inclus à la BdD du plugin SomfyUnified. |

