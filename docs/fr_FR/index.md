# Plugin **SomfyUnified**
<img src="/docs/assets/images/SomfyUnified-Image.png" alt="" style="height: 40%; width:40%;"/>
<img src="/SomfyUnified-Doc/assets/images/SomfyUnified-Image.png" alt="SomfyUnified logo" style="height: 40%; width:40%;"/>

_Applicable version 2.1.6_<br>
_Updated 2025 0111_


## Presentation
Le plugin **SomfyUnified** est destiné à permettre une interface entre Jeedom et les équipements de l'écosystème Somfy connectés via les API OverKiz et appartenant aux familles listées ci-dessous:

>- **Somfy TaHoma Cloud**
>- **Somfy TaHoma Local**
>- **Atlantic Cozytouch**
>- **Thermor Cozytouch**
>- **Daikin**
>- ~~Brandt Smart Control~~ (Changement d'API, ce serveur n'est plus supporté)
>- **Flexom**
>- **Hexaom HexaConnect**
>- **Hitachi Hi Kumo**
>- **Nexity Eugénie**
>- ~~Rexel Energeasy Connect~~ (Changement d'API, ce serveur n'est plus supporté)
>- **Simu (LiveIn2)**
>- **Ubiwizz**


### WiFi Direct
A partir de la version 2.0 et par extension, il prend également en charge les équipements pilotables par **WiFi Direct** et qui ne nécessitent pas une Box/Gateway pour se connecter au serveur.<br>

**Notice**<br>
La connection des équipements avec connections via NaviClim, Navilink reste à être validée par de futurs utilisateurs.


## Caractéristiques
### Gestion multi-serveurs

Basé sur une gestion multi-serveurs, le plugin **SomfyUnified** remonte, crée et gère la totalité des commandes et informations disponibles auprès des serveurs enregistrés et configurés par l'utilisateur.

### Retour d'état instantané
En fonctionnement opérationnel, la prise en compte d'une commande reçue par l'équipement sera suivie par une **mise à jour instantanée** de l'état/info correspondant (1).<br>
Ce retour d'état instantané assure à l'utilisateur un réel confort d'utilisation et de programmation de ses équipements.<br>
Le retour d'état est opérationnel avec les serveurs de type cloud et local.<br>
Le retour d'état instantané n'est pas disponible sur les serveurs de type wifi.

(1) _Sauf si l'information n'était pas mise à disposition par le serveur_

### Gestion des Scénarios (App)

Si des scénarios ont été programmés au niveau de l'app  constructeur, le plugin permet de les exécuter.
Pour chaque serveur, la liste des scénarios se trouve dans l'équipement `serverScenarios_server` et sous forme d'une liste dans la commande `serverScenarioList`.
Si la commande info `serverScenarioTimestamp` est égale à 0 ou contient une date Timestamp non valide, c'est à dire, correspondant à une date passée par rapport à maintenant, le scénario sera déclanché immédiatement.
Si la commande info `serverScenarioTimestamp` contient une date valide (au format Unix Timestamp), le scénario sera alors déclanché à cette date.

La liste des scénarios est mise à jour en même temps que les données Info des équipements (synchronisé par le cron Cloud).

**Notes**<br>
TaHoma Cloud: seuls les scénarios de type **Manuel** sont remontés par l'API.<br>
TaHoma Local: la gestion des scénarios n'est pas supportée par l'API locale (serveur Local).

### Adaptabilité et évolutivité à l'écosystème

L'écosystème géré par le plugin **SomfyUnified** comprend, à ce jour, de nombreux partenaires et est susceptible de continuer à s'étoffer et évoluer.<br>
Cela signifie qu'une box des familles de l'écosystème (TaHoma, Cozytouch, ...) peut s'interfacer à de nombreux dispositifs très différents les uns des autres pour les piloter.
On trouve actuellement dans l'écosystèmes le contrôle de dispositifs tels que des systèmes de controle d'ouverture ou fermeture d'ouvrants (volets roulants, portes, stores, ...), des systèmes d'alarme, des systèmes de chauffage et climatisation, ...<br>

L'absence de documentation de la part de Somfy sur les commandes des dispositifs rend la syntaxe de ces opérations particulièrement difficile à anticiper et implémenter dans un plugin et ce, à priori.<br>

Afin de s'adapter à une telle diversité de commandes ou données potentielles, le plugin gère les différents équipements à partir de fichiers de configurations propres à chaque équipement.<br>

La liste des équipements dont le fichier de configuration est intégré au plugin est donnée en fin de ce document.

### Compatibilité

Le plugin **SomfyUnified** est compatible des systèmes fonctionnant sous Debian 11 & 12.


## Statut de validation du plugin

Compte-tenu de la grande diversité d'équipements susceptibles d'être gérés par le plugin, il est impossible, pour le développeur, d'avoir pu valider tous les types d'équipements.<br>
Les validations se feront donc au fur et à mesure de l'adoption du plugin par les utilisateurs qui accepteront de tenter son intégration.

Compte-tenu de l'état d'avancement, l'état de validation des différentes familles d'équipements est donné dans le tableau suivant:

| Equipement                 |  Type API  |  Etat de validation |
| :------------------------- | :--------: | :-----------------: |
| Somfy TaHoma Cloud (2)     | cloud      | validé              |
| Somfy TaHoma Local         | local      | validé              |
| Cozytouch (3)              | cloud      | validé              |
| Daikin (2)                 | cloud      | validé              |
| Hitachi Hi Kumo            | cloud      | validé              |
| Velux (2)                  | cloud      | validé              |
| BFt (EasyAXS)              | cloud      | à confirmer         |
| Flexom                     | cloud      | à confirmer         |
| Hexaom HexaConnect         | cloud      | à confirmer         |
| Nexity Eugénie             | cloud      | à confirmer         |
| Simu (LiveIn2)             | cloud      | à confirmer         |
| Ubiwizz                    | cloud      | à confirmer         |

(2) _Daikin, Velux (via Somfy TaHoma)_<br>
(3) _Atlantic, Sauter (Gen1), Thermor_


## Feuille de route

Dans l'état actuel du plugin, les fonctionnalités suivantes sont prévues mais non encore opérationnelles:
1. Le plugin est en langue EN, la version FR sera disponible dans une version ultérieure.
2. D'une façon générale, pas de widgets spécifiques associés aux commandes. Dans certains cas, des widgets dédiés sont appliqués sinon les widgets du core Jeedom s'appliquent.


## API locale Somfy

L'utilisation du serveur local de votre gateway Somfy nécessite que vous ayez au préalable créé un Token d'authentification à partir de la page du plugin prévue à cet effet.<br>
La gateway Somfy a la capacité d'enregistrer et de conserver plusieurs tokens.<br>
Le plugin propose les fonctionalités de gestion des token de votre gateway (création avec label utilisateur, suppression).

## API locale en mode IP

Le mode IP est à utiliser lorsqu'un système DNS dans votre configuration ne résoud pas les hostnames de type **.local**.<br>
C'est le cas en particulier lorsque vous utilisez une box Jeedom Atlas.<br>
Le mode IP peut être activé lors de la création ou mise à jour d'un serveur de type **Local**.<br>
Lorsque le Mode IP est activé, la vérification SSL est obligatoirement et automatiquement désactivée (verifySSL = No).<br>

## Rafraichissements périodiques

En complément du retour d'état instantané qui s'effectue après l'envoi d'une commande, un rafraichissement périodique de l'ensemble des données équipement s'effectue toutes les:
- 30 mn pour un serveur CLOUD
- 1 mn pour un serveur LOCAL
- 1 mn pour un serveur WIFI


## Utilisation des Logs

Attention, les Logs `Debug` et `Info` génèrent beaucoup d'informations. Ces modes ne sont à utiliser que pour entrer en analyse du plugin et pendant des courtes périodes.<br>
Lors du fonctionnement normal, positionner les Logs en mode `Defaut`.


## Crons

En fonctionnement normal, les Crons `cron` et `cron30` doivent être cochés.


## Utilisation des commandes user

...


## FAQ

1. **Mon équipement a été créé mais il n’y a aucune commande qui apparait ?**<br>
L’équipement n’est pas (encore) intégré dans la base de donnée (BdD) du plugin (voir ci-dessous).<br>
A l’aide de l’explorateur de fichier Jeedom, se rendre dans le répertoire:<br>
`plugins/SomfyUnified/userData/components/`<br>
Créer une archive .zip du répertoire **undefined** puis la renommer en y ajoutant .txt à la fin. Envoyer ce fichier créer au concepteur du plugin (en MP) afin que l’équipement puisse être inclus à la BdD du plugin SomfyUnified.

2. **Je souhaite piloter des équipements controlés par une box qui ne se trouvent pas sur le même réseau local (LAN) que celui qui gère mon Jeedom.**<br>
C'est le cas d'équipements situés dans une résidence secondaire par exemple. Oui, cela est possible en gérant vos équipements via le serveur CLOUD associé. Dans ce cas, votre box n'apparaitra pas dans le panel "Local IoT Gateways".

3. **Puis-je enregistrer et gérer plusieurs serveurs avec mon plugin SomfyUnified ?.**<br>
Oui, le plugin **SomfyUnified** assure la gestion de tous les serveurs enregistrés par l'utilisateur et choisis dans la liste du menu "Manage Servers" et correctement configurés.<br>
Une configuration classique pourrait être: Somfy TaHoma CLOUD + Somfy TaHoma LOCAL + Cozytouch CLOUD.

4. **Sur mon Jeedom, puis-je gérer des équipements Somfy TaHoma qui ne sont pas reconnus par l'API Somfy Local ?.**<br>
Comme le plugin **SomfyUnified** assure la gestion de tous les serveurs enregistrés, il est possible de gérer ses équipements Somfy TaHoma en local pour profiter de l'avantages mode Cloudless et d'avoir accès également via le serveur CLOUD aux autres équipements non reconnus par votre box TaHoma en local.<br>


## Liste des équipements en BdD du plugin (Cozytouch WiFi Direct)

A cette date, l'inclusion des équipements suivant a été effectuée:

| Type Equipement            |  Identifiant Equipement                                                 | Constructeur      |
| :------------------------- | :---------------------------------------------------------------------- | :---------------- |
| Water Heater               | Calypso Split                                                           | Atlantic          |
|                            | Calypso Split Trineo                                                    | Atlantic          |
|                            | Phazy                                                                   | Sauter            |
|                            | Duralis Connect                                                         | Thermor           |



## Liste des équipements en BdD du plugin (API Overkiz)

A cette date, l'inclusion des équipements suivant a été effectuée:

| Type Equipement            |  Identifiant Equipement                                                 | Constructeur      | Commandes | Infos     |
| :------------------------- | :---------------------------------------------------------------------- | :---------------- | :-------- | :-------- |
| Alarm                      | internal:TSKAlarmComponent                                              | Somfy             | 14        | 9         |
|				             | io:AlarmIOComponent                                                     |                   |           |           |
| Awning		             | io:AwningValanceIOComponent                                             |                   |           |           |
|				             | io:HorizontalAwningIOComponent                                          |                   |           |           |
|				             | ogp:Awning                                                              |                   |           |           |
|				             | rts:HorizontalAwningRTSComponent                                        |                   |           |           |
| CarbonDioxideSensor		 | netatmo:CO2Component                                                    | Legrand Netatmo   |           |           |
| ConfigurationComponent     | netatmo:ConfigurationComponent                                          | Legrand Netatmo   |           |           |
|				             | netatmo:HomeController                                                  | Legrand Netatmo   |           |           |
|				             | netatmo:WeatherStationConfigurationComponent                            | Legrand Netatmo   |           |           |
| ConsumptionSensor          | io:DHWRelatedFossilEnergyConsumptionSensor                              |                   |           |           |
|				             | io:HeatingRelatedFossilEnergyConsumptionSensor                          |                   |           |           |
|				             | io:TotalFossilEnergyConsumptionSensor                                   |                   |           |           |
| ContactSensor		         | io:ContactIOSystemDeviceSensor                                          |                   |           |           |
|				             | io:SomfyContactIOSystemSensor                                           |                   |           |           |
|				             | rtds:RTDSContactSensor                                                  |                   |           |           |
|				             | zigbee:DoorSensorComponent                                              |                   |           |           |
| Dock		                 | internal:TSKDockComponent                                               |                   |           |           |
| ElectricitySensor		     | io:AirConditioningElectricalEnergyConsumptionSensor                     |                   |           |           |
|				             | io:CumulatedElectricalEnergyConsumptionIOSystemDeviceSensor             |                   |           |           |
|				             | io:DHWCumulatedElectricalEnergyConsumptionIOSystemDeviceSensor          |                   |           |           |
|				             | io:DHWElectricalEnergyConsumptionSensor                                 |                   |           |           |
|				             | io:DHWRelatedElectricalEnergyConsumptionSensor                          |                   |           |           |
|				             | io:ElectricityMeterComponent                                            |                   |           |           |
|				             | io:EnergyConsumptionSensorsConfigurationComponent                       |                   |           |           |
|				             | io:EnergyConsumptionSensorsHeatPumpComponent                            |                   |           |           |
|				             | io:HeatingElectricalEnergyConsumptionSensor                             |                   |           |           |
|				             | io:HeatingRelatedElectricalEnergyConsumptionSensor                      |                   |           |           |
|				             | io:OtherElectricalEnergyConsumptionSensor                               |                   |           |           |
|				             | io:PlugsElectricalEnergyConsumptionSensor                               |                   |           |           |
|				             | io:TotalElectricalEnergyConsumptionIOSystemSensor                       |                   |           |           |
|				             | io:TotalElectricalEnergyConsumptionSensor                               |                   |           |           |
|				             | modbuslink:DHWCumulatedElectricalEnergyConsumptionMBLSystemDeviceSensor |                   |           |           |
|				             | modbus:YutakiV2SpaceHeatingElectricalEnergyConsumptionComponent         | Hitachi           |           | 8         |
| ExteriorScreen		     | io:VerticalExteriorAwningIOComponent                                    |                   |           |           |
| ExteriorVenetianBlind	     | io:ExteriorVenetianBlindIOComponent                                     |                   |           |           |
| GarageDoor		         | io:DiscreteGarageOpenerIOComponent                                      |                   |           |           |
|				             | io:GarageOpenerIOComponent                                              |                   |           |           |
|				             | ogp:GarageDoor                                                          |                   |           |           |
|				             | rts:GarageDoorWithVentilationPositionRTSComponent                       |                   | 10        |           |
| Gate		                 | io:SlidingDiscreteFullyPedestriableGateOpenerIOComponent                |                   |           |           |
|				             | io:SlidingDiscreteGateOpenerIOComponent                                 |                   |           |           |
|				             | ogp:Gate                                                                |                   | 4         | 14        |
|				             | rts:GateOpenerRTSComponent                                              |                   | 9         |           |
|				             | rts:SlidingGateOpenerRTSComponent                                       |                   |           |           |
| Generic		             | ovp:ModbusMainController                                                | Hitachi           | 3         | 8         |
| HeatingSystem		         | io:AtlanticElectricalHeaterIOComponent                                  | Atlantic          |           |           |
|				             | io:AtlanticElectricalHeaterWithAdjustableTemperatureSetpointIOComponent | Atlantic          |           |           |
|				             | io:AtlanticElectricalTowelDryerIOComponent                              | Atlantic          |           |           |
|				             | io:AtlanticElectricalTowelDryer_IC3_IOComponent                         | Atlantic          |           |           |
|				             | io:AtlanticPassAPCBoilerMainComponent                                   | Atlantic          |           |           |
|				             | io:AtlanticPassAPCHeatingAndCoolingZoneComponent                        | Atlantic          |           |           |
|				             | io:AtlanticPassAPCHeatingZoneComponent                                  | Atlantic          |           |           |
|				             | io:AtlanticPassAPCHeatPumpMainComponent                                 | Atlantic          |           |           |
|				             | io:AtlanticPassAPCZoneControlMainComponent                              | Atlantic          |           |           |
|				             | io:AtlanticPassAPCZoneControlZoneComponent                              | Atlantic          | 32        | 30        |
|				             | modbus:YutakiRoomThermostatZone1Component                               | Hitachi           |           | 7         |
|				             | modbus:YutakiRoomThermostatZone2Component                               | Hitachi           |           | 7         |
|				             | netatmo:NetatmoRoomController                                           | Legrand Netatmo   | 6         | 20        |
|				             | ogp:HvacZone                                                            | Daikin            |           |           |
| HitachiHeatingSystem       | modbus:YutakiMainComponent                                              | Hitachi           | 41        | 73        |
|                            | modbus:YutakiV2Zone1Component                                           | Hitachi           | 26        | 25        |
|                            | modbus:YutakiV2Zone2Component                                           | Hitachi           | 26        | 25        |
| HumiditySensor             | io:RelativeHumidityIOSystemDeviceSensor                                 |                   |           |           |
|                            | netatmo:HumidityComponent                                               | Legrand Netatmo   |           |           |
|                            | zigbee:RelativeHumidityComponent                                        |                   |           |           |
| Light                      | hue:ColorTemperatureLightBulbHUEComponent                               | Philps Hue        |           |           |
|				             | hue:ExtendedColorLightCandleHUEComponent                                | Philps Hue        |           |           |
|				             | hue:GenericColorTemperatureLightHUEComponent                            | Philps Hue        |           |           |
|				             | hue:GenericDimmableLightHUEComponent                                    | Philps Hue        |           |           |
|				             | hue:GenericExtendedColorLightHUEComponent                               | Philps Hue        |           |           |
|				             | io:AtlanticDimmableLightIOComponent                                     | Atlantic          | 19        | 8         |
|				             | io:DimmableLightIOComponent                                             |                   |           |           |
|				             | io:DimmableLightIOComponent                                             |                   |           |           |
|				             | io:DimmableRGBLightIOComponent                                          |                   |           |           |
|				             | io:LightMicroModuleSomfyIOComponent                                     |                   |           |           |
|				             | ogp:Light                                                               |                   |           |           |
|				             | rts:LightRTSComponent                                                   |                   |           |           |
| LightSensor                | io:LightIOSystemDeviceSensor                                            |                   |           |           |
|                            | io:LightIOSystemSensor                                                  |                   |           |           |
| MusicPlayer         	     | ogp:AudioPlayer                                                         |                   |           |           |
| NoiseSensor         	     | netatmo:NoiseComponent                                                  | Legrand Netatmo   |           |           |
| OccupancySensor       	 | io:OccupancyIOSystemDeviceSensor                                        |                   |           |           |
| OnOff       	             | io:OnOffIOComponent                                                     |                   |           |           |
| Pergola      	             | io:SimpleBioclimaticPergolaIOComponent                                  |                   |           |           |
|				             | ogp:Pergola                                                             |                   |           |           |
| Pod       	             | internal:PodMiniComponent                                               |                   |           |           |
|				             | internal:PodV2Component                                                 |                   |           |           |
|				             | internal:PodV3Component                                                 |                   |           |           |
|				             | internal:UPodComponent                                                  |                   |           |           |
|				             | internal:UPodNetWorkComponent                                           |                   |           |           |
| ProtocolGateway       	 | enocean:TransceiverEnoceanComponent                                     |                   |           |           |
|				             | homekit:StackComponent                                                  |                   |           |           |
|				             | hue:BridgeHUEV2Component                                                | Philps Hue        |           |           |
|				             | io:StackComponent                                                       |                   |           |           |
|				             | ogp:Bridge                                                              |                   |           |           |
|				             | ogp:Gateway                                                             |                   |           |           |
|				             | zigbee:StackV3Component                                                 |                   |           |           |
|				             | zigbee:TransceiverV3_0Component                                         |                   |           |           |
| RemoteController       	 | io:IzymoController                                                      |                   |           |           |
|                       	 | io:KeygoController                                                      |                   |           |           |
|				             | rtds:RTDSRemoteControllerComponent                                      |                   |           |           |
| RollerShutter       	     | io:RollerShutterGenericIOComponent                                      |                   |           |           |
|				             | io:RollerShutterVeluxIOComponent                                        |                   |           |           |
|				             | io:RollerShutterWithBatterySomfyIOComponent                             |                   |           |           |
|				             | io:RollerShutterWithLowSpeedManagementIOComponent                       | Somfy             |           |           |
|				             | rts:RollerShutterRTSComponent                                           | Somfy             |           |           |
|				             | zigbee:ProfaluxGenericComponent                                         | Profalux          | 14        | 17        |
|				             | zigbee:RollerShutterGenericComponent                                    | Profalux          | 15        | 27        |
| Screen          	         | io:VerticalInteriorBlindVeluxIOComponent                                |                   |           |           |
| Shutter          	         | ogp:Shutter                                                             |                   |           |           |
| SmokeSensor       	     | io:SomfySmokeIOSystemSensor                                             | Somfy             |           |           |
| SwingingShutter       	 | rts:SwingingShutterRTSComponent                                         |                   |           |           |
| TemperatureSensor      	 | netatmo:TemperatureComponent                                            | Legrand Netatmo   |           |           |
|				             | io:AtlanticPassAPCOutsideTemperatureSensor                              | Atlantic          |           |           |
|				             | io:AtlanticPassAPCZoneTemperatureSensor                                 | Atlantic          |           |           |
|				             | io:TemperatureInCelciusIOSystemDeviceSensor                             |                   |           |           |
|				             | io:TemperatureIOSystemSensor                                            |                   |           |           |
|				             | netatmo:NetatmoThermostatTemperatureSensor                              | Legrand Netatmo   | 0         | 8         |
|				             | ogp:TemperatureSensor                                                   | Daikin            |           |           |
|				             | zigbee:TemperatureSensorComponent                                       |                   |           |           |
| WaterHeatingSystem      	 | io:AtlanticDomesticHotWaterProductionV2_AEX_IOComponent                 | Atlantic          |           |           |
|                        	 | io:AtlanticDomesticHotWaterProductionV2_CETHI_V4_IOComponent            | Atlantic          |           |           |
|				             | io:AtlanticPassAPCDHWComponent                                          | Atlantic          |           |           |
|				             | io:DomesticHotWaterTankComponent                                        |                   |           |           |
|				             | modbuslink:AtlanticDomesticHotWaterProductionMBLComponent               |                   |           |           |
| WeatherSensor              | core:WeatherSystemSensor                                                |                   |           |           |
| Wifi       	             | internal:WifiComponent                                                  |                   |           |           |
| Window       	             | io:WindowOpenerVeluxIOComponent                                         | Velux             |           |           |
