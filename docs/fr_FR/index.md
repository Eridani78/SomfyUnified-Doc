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
| Atlantic Cozytouch (1)     | cloud      | validé              |
| BFt (EasyAXS)              | cloud      | à confirmer         |
| Brandt Smart Control       | cloud      | à confirmer         |
| Flexom                     | cloud      | à confirmer         |
| Hexaom HexaConnect         | cloud      | à confirmer         |
| Hitachi Hi Kumo            | cloud      | à confirmer         |
| Nexity Eugénie             | cloud      | à confirmer         |
| Rexel Energeasy Connect    | cloud      | à confirmer         |
| Simu (LiveIn2)             | cloud      | à confirmer         |
| Ubiwizz                    | cloud      | à confirmer         |

(1) _Atlantic, Sauter (Gen1), Thermor_


## Feuille de route

Dans l'état actuel du plugin, les fonctionnalités suivantes sont prévues mais non encore opérationnelles:
1. La mise à jour "instantée" des commandes Info est en cours d'intégration. Les mises à jour sont toutes les 1 mn pour un serveur LOCAl et 30 mn pour un serveur CLOUD.
2. Le plugin est en langue EN, la version FR sera bientôt disponible
3. Pas de widgets spécifiques associés aux commandes. Les widgets du core Jeedom s'appliquent.


## Ecosystème Somfy/TaHoma

L'écosystème Somfy TaHoma comprend, à ce jour, de nombreux partenaires et est susceptible de continuer à s'étoffer et évoluer.
Cela signifie qu'une box des familles de l'écosystème (TaHoma, Cozytouch, ...) peut s'interfacer à de nombreux dispositifs très différents les uns des autres pour les piloter.
On trouve actuellement dans l'écosystèmes Somfy le contrôle de dispositifs tels que des systèmes de controle d'ouverture ou fermeture d'ouvrants (volets roulants, portes, stores, ...), des systèmes d'alarme, des systèmes de chauffage et climatisation, ...

L'absence de documentation de la part de Somfy sur les commandes des dispositifs rend la syntaxe de ces opérations particulièrement difficile à anticiper et implémenter dans un plugin et ce, à priori.

Afin de s'adapter au mieux à une telle diversité de commandes ou données potentielles, deux modes de fonctionnement du plugin ont du être implémenté.


## API locale Somfy

A suivre ...


## Gestion des Scénarios (App)

Si des scénarios ont été programmés au niveau de l'app  constructeur, le plugin permet de les exécuter.
Pour chaque serveur, la liste des scénarios se trouve dans l'équipement `serverScenarios_server` et sous forme d'une liste dans la commande `serverScenarioList`.
Si la commande info `serverScenarioTimestamp` est égale à 0 ou contient une date Timestamp non valide, c'est à dire, correspondant à une date passée par rapport à maintenant, le scénario sera déclanché immédiatement.
Si la commande info `serverScenarioTimestamp` contient une date valide (au format Unix Timestamp), le scénario sera alors déclanché à cette date (fonctionnalité non validée).

La liste des scénarios est mise à jour en même temps que les données Info des équipements (synchronisé par le cron Cloud).

Notes<br>
TaHoma Cloud: seuls les scénarios de type **Manuel** sont remontés par l'API.<br>
TaHoma Local: la gestion des scénarios n'est pas supportée par l'API locale (serveur Local).


## FAQ

1. **Mon équipement a été créé mais il n’y a aucune commande qui apparait ?**<br>
L’équipement n’est pas (encore) intégré dans la base de donnée (BdD) du plugin (voir ci-dessous).<br>
A l’aide de l’explorateur de fichier Jeedom, se rendre dans le répertoire:<br>
`plugins/SomfyUnified/userData/components/`<br>
Créer une archive .zip du répertoire **undefined** puis la renommer en y ajoutant .txt à la fin. Envoyer ce fichier créer au concepteur du plugin (en MP) afin que l’équipement puisse être inclus à la BdD du plugin SomfyUnified.

2. **Je souhaite piloter des équipements controlés par une box qui ne se trouvent pas sur le même réseau local (LAN) que celui qui gère mon Jeedom.**<br>
C'est le cas d'équipements situés dans une résidence secondaire par exemple. Oui, cela est possible en gérant vos équipements via le serveur CLOUD associé. Dans ce cas, votre box n'apparaitra pas dans le panel "Local IoT Gateways".

3. **Puis-je enregistrer et gérer plusieurs serveurs avec mon plugin SomfyUnified ?.**<br>
Oui, le plugin **SomfyUnified** assure la gestion de tous les serveurs enregistrés par l'utilisateur et choisis dans la liste du menu "Manage Servers".<br>
Une configuration classique pourrait être: Somfy TaHoma CLOUD + Somfy TaHoma LOCAL + Cozytouch CLOUD.

4. **Sur mon Jeedom, puis-je gérer des équipements Somfy TaHoma qui ne sont pas reconnus par l'API Somfy Local ?.**<br>
Comme le plugin **SomfyUnified** assure la gestion de tous les serveurs enregistrés, il est possible de gérer ses équipements Somfy TaHoma en local pour profiter des avantages retours d'état immédiats et mode Cloudless et d'avoir accès également via le serveur CLOUD aux autres équipements non reconnus par votre box TaHoma en local.<br>


## Liste des équipements en BdD du plugin

A cette date, l'inclusion des équipements suivant a été effectuée:

| Type Equipement            |  Identifiant Equipement                                                 |
| :------------------------- | :---------------------------------------------------------------------- |
| Alarm                      | internal:TSKAlarmComponent                                              |
|				             | io:AlarmIOComponent                                                     |
| Awning		             | io:AwningValanceIOComponent                                             |
|				             | io:HorizontalAwningIOComponent                                          |
|				             | rts:HorizontalAwningRTSComponent                                        |
| CarbonDioxideSensor		 | netatmo:CO2Component                                                    |
| ConfigurationComponent     | netatmo:ConfigurationComponent                                          |
|				             | netatmo:HomeController                                                  |
|				             | netatmo:WeatherStationConfigurationComponent                            |
| ConsumptionSensor          | io:DHWRelatedFossilEnergyConsumptionSensor                              |
|				             | io:HeatingRelatedFossilEnergyConsumptionSensor                          |
|				             | io:TotalFossilEnergyConsumptionSensor                                   |
| ContactSensor		         | io:ContactIOSystemDeviceSensor                                          |
|				             | io:SomfyContactIOSystemSensor                                           |
|				             | rtds:RTDSContactSensor                                                  |
|				             | zigbee:DoorSensorComponent                                              |
| Dock		                 | internal:TSKDockComponent                                               |
| ElectricitySensor		     | io:AirConditioningElectricalEnergyConsumptionSensor                     |
|				             | io:CumulatedElectricalEnergyConsumptionIOSystemDeviceSensor             |
|				             | io:DHWCumulatedElectricalEnergyConsumptionIOSystemDeviceSensor          |
|				             | io:DHWElectricalEnergyConsumptionSensor                                 |
|				             | io:ElectricityMeterComponent                                            |
|				             | io:EnergyConsumptionSensorsConfigurationComponent                       |
|				             | io:EnergyConsumptionSensorsHeatPumpComponent                            |
|				             | io:HeatingElectricalEnergyConsumptionSensor                             |
|				             | io:OtherElectricalEnergyConsumptionSensor                               |
|				             | io:PlugsElectricalEnergyConsumptionSensor                               |
|				             | io:TotalElectricalEnergyConsumptionIOSystemSensor                       |
| ExteriorScreen		     | io:VerticalExteriorAwningIOComponent                                    |
| GarageDoor		         | io:DiscreteGarageOpenerIOComponent                                      |
| Gate		                 | io:SlidingDiscreteFullyPedestriableGateOpenerIOComponent                |
| HeatingSystem		         | io:AtlanticElectricalHeaterIOComponent                                  |
|				             | io:AtlanticElectricalHeaterWithAdjustableTemperatureSetpointIOComponent |
|				             | io:AtlanticPassAPCBoilerMainComponent                                   |
|				             | io:AtlanticPassAPCHeatingZoneComponent                                  |
|				             | io:AtlanticPassAPCZoneControlMainComponent                              |
|				             | io:AtlanticPassAPCZoneControlZoneComponent                              |
| HumiditySensor		     | netatmo:HumidityComponent                                               |
| Light         		     | hue:ColorTemperatureLightBulbHUEComponent                               |
|				             | hue:ExtendedColorLightCandleHUEComponent                                |
|				             | hue:GenericColorTemperatureLightHUEComponent                            |
|				             | hue:GenericDimmableLightHUEComponent                                    |
|				             | hue:GenericExtendedColorLightHUEComponent                               |
|				             | io:DimmableLightIOComponent                                             |
|				             | io:OnOffLightIOComponent                                                |
| LightSensor         	     | io:LightIOSystemSensor                                                  |
| MusicPlayer         	     | ogp:AudioPlayer                                                         |
| NoiseSensor         	     | netatmo:NoiseComponent                                                  |
| OccupancySensor       	 | io:OccupancyIOSystemDeviceSensor                                        |
| OnOff       	             | io:OnOffIOComponent                                                     |
| Pod       	             | internal:PodMiniComponent                                               |
|				             | internal:PodV2Component                                                 |
|				             | internal:PodV3Component                                                 |
| ProtocolGateway       	 | enocean:TransceiverEnoceanComponent                                     |
|				             | homekit:StackComponent                                                  |
|				             | hue:BridgeHUEV2Component                                                |
|				             | io:StackComponent                                                       |
|				             | ogp:Bridge                                                              |
|				             | zigbee:StackV3Component                                                 |
|				             | zigbee:TransceiverV3_0Component                                         |
| RemoteController       	 | io:KeygoController                                                      |
| RollerShutter       	     | io:RollerShutterGenericIOComponent                                      |
|				             | io:RollerShutterWithBatterySomfyIOComponent                             |
|				             | io:RollerShutterWithLowSpeedManagementIOComponent                       |
| SmokeSensor       	     | io:SomfySmokeIOSystemSensor                                             |
| TemperatureSensor      	 | netatmo:TemperatureComponent                                            |
|				             | io:AtlanticPassAPCOutsideTemperatureSensor                              |
|				             | io:AtlanticPassAPCZoneTemperatureSensor                                 |
|				             | io:TemperatureInCelciusIOSystemDeviceSensor                             |
|				             | io:TemperatureIOSystemSensor                                            |
| WaterHeatingSystem      	 | io:AtlanticDomesticHotWaterProductionV2_CETHI_V4_IOComponent            |
|				             | io:AtlanticPassAPCDHWComponent                                          |
|				             | io:DomesticHotWaterTankComponent                                        |
| Wifi       	             | internal:WifiComponent                                                  |
