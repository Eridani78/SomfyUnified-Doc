# Plugin **SomfyUnified**
<img src="/docs/assets/images/SomfyUnified-Image.png" alt="" style="height: 40%; width:40%;"/>
<img src="/SomfyUnified-Doc/assets/images/SomfyUnified-Image.png" alt="SomfyUnified logo" style="height: 40%; width:40%;"/>


## Presentation
Le plugin **SomfyUnified** est destiné à permettre une interface entre Jeedom et les équipements connectés via les API OverKiz:
- Somfy TaHoma Cloud (cloud)
- Somfy TaHoma Local (local)
- Atlantic Cozytouch (cloud)
- Brandt Smart Control (cloud)
- Flexom (cloud)
- Hexaom HexaConnect (cloud)
- Hitachi Hi Kumo (cloud)
- Nexity Eugénie (cloud)
- Rexel Energeasy Connect (cloud)
- Ubiwizz (cloud)

| Equipement              | Type API | Validé     |
| :---------------------- | :------: | :--------: |
| Somfy TaHoma Cloud      | cloud    | oui        |
| Somfy TaHoma Local      | local    | oui        |
| Atlantic Cozytouch      | cloud    | en attente |
| Brandt Smart Control    | cloud    | en attente |
| Flexom                  | cloud    | en attente |
| Hexaom HexaConnect      | cloud    | en attente |
| Hitachi Hi Kumo         | cloud    | en attente |
| Nexity Eugénie          | cloud    | en attente |
| Rexel Energeasy Connect | cloud    | en attente |
| Ubiwizz                 | cloud    | en attente |


## Ecosystème Somfy/TaHoma
L'écosystème Somfy TaHoma comprend, à ce jour, de nombreux partenaires et est susceptible de continuer à s'étoffer et évoluer.
Cela signifie qu'une box TaHoma peut s'interfacer à de nombreux dispositifs très différents les uns des autres pour les piloter.
On trouve actuellement dans l'écosystèmes Somfy le contrôle de dispositifs tels que des systèmes de controle d'ouverture ou fermeture d'ouvrants (volets roulants, portes, stores, ...), des systèmes d'alarme, des systèmes de chauffage et climatisation, ...

L'absence de documentation de la part de Somfy sur les commandes des dispositifs rend la syntaxe de ces opérations particulièrement difficile à anticiper et implémenter dans un plugin et ce, à priori.

Afin de s'adapter au mieux à une telle diversité de commandes ou données potentielles, deux modes de fonctionnement du plugin ont du être implémenté.


## API locale Somfy
...

