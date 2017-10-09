## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Betekenis van de migratie van IaaS-middelen van Hallo classic deployment model tooResource Manager
Voordat we op Hallo details inzoomen, bekijken we Hallo verschil tussen gegevens vlak- en management vlak bewerkingen op Hallo IaaS-middelen.

* *Controle van beheer/vlak* beschrijft Hallo-aanroepen die binnenkomen Hallo Beheercontrole/vlak of Hallo-API voor het wijzigen van resources. Bijvoorbeeld beheren bewerkingen zoals het maken van een VM, opnieuw starten van een virtuele machine en het bijwerken van een virtueel netwerk met een nieuw subnet Hallo met resources. Ze niet rechtstreeks van invloed op de verbindende toohello exemplaren.
* *Gegevens vlak* (toepassing) beschrijft Hallo runtime van Hallo toepassing zelf en interactie met exemplaren die niet door hello Azure API omvat. Toegang verkrijgen tot uw website of het binnenhalen van gegevens vanaf een actief SQL Server-exemplaar of een MongoDB-server kan worden gezien als interactie op het gegevensvlak of toepassingsinteractie. Ook worden vlak gegevens kopiëren van een blob in een opslagaccount en toegang hebben tot een openbare IP-adres tooRDP of SSH naar Hallo virtuele machine. Deze bewerkingen Houd Hallo toepassing uitvoert via compute, netwerk en opslag.

Achter de schermen hello, is Hallo gegevens vlak Hallo dezelfde tussen Hallo klassieke implementatiemodel en de Resource Manager-stack. Tijdens het migratieproces vertalen we Hallo representatie van Hallo resources uit Hallo Classic deployment model toothat in Hallo Resource Manager-stack. Als gevolg hiervan moet u toouse nieuwe hulpprogramma's, API's, SDK's toomanage uw resources in Hallo Resource Manager-stack.

![Schermopname die het verschil tussen het beheer-/controlevlak en het gegevensvlak weergeeft](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> In sommige gevallen migratie hello Azure-platform stopt deallocates en uw virtuele machines opnieuw wordt opgestart. Dit leidt tot een korte uitvaltijd voor het gegevensvlak.
>

## <a name="hello-migration-experience"></a>Hallo migratie-ervaring
Voordat u de migratie-ervaring Hallo, wordt de volgende Hallo aanbevolen:

* Zorg dat de Hallo-resources die u wilt dat toomigrate niet een niet-ondersteunde functies of -configuraties gebruikt. Meestal Hallo platform detecteert deze problemen en genereert een fout.
* Als u virtuele machines die zich niet in een virtueel netwerk hebt, wordt deze gestopt en toewijzing ongedaan gemaakt als onderdeel van Hallo bewerking voorbereiden. Als u niet wilt dat toolose Hallo openbaar IP-adres, voorbereiden uiterlijk in Hallo IP-adres reserveren voordat Hallo bewerking. Als Hallo virtuele machines zich in een virtueel netwerk, zijn ze echter niet gestopt en de toewijzing ongedaan gemaakt.
* Plan de migratie tijdens buiten kantooruren tooaccommodate onverwachte fouten die kunnen ontstaan tijdens de migratie.
* Hallo huidige configuratie van uw virtuele machines downloaden met behulp van PowerShell, opdrachtregelinterface (CLI)-opdrachten of REST-API's toomake is het eenvoudiger voor validatie nadat Hallo stap voorbereiden is voltooid.
* Werk uw automation/uitoefening scripts toohandle Hallo Resource Manager-implementatiemodel voordat u Hallo-migratie begint. Desgewenst kunt u doen GET-bewerkingen wanneer Hallo resources beschikbaar in Hallo status voorbereid zijn.
* Evalueer Hallo RBAC beleidsregels die zijn geconfigureerd op het Hallo-classic IaaS-middelen en plannen voor nadat Hallo migratie voltooid is.

Hallo Migratiewerkstroom is als volgt

![Schermafbeelding van Hallo Migratiewerkstroom](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Alle Hallo bewerkingen die worden beschreven in de volgende secties Hallo zijn idempotent. Als er een probleem dan een niet-ondersteunde functie of een Configuratiefoutbericht wordt weergegeven, is het aanbevolen dat u opnieuw Hallo proberen voorbereiden, afgebroken of doorgevoerd, bewerking. Hello Azure-platform probeert Hallo actie opnieuw.
>
>

### <a name="validate"></a>Valideren
Hallo bewerking valideren is de eerste stap Hallo Hallo-migratieproces. Hallo-doel van deze stap is tooanalyze Hallo status van resources Hallo u toomigrate in het klassieke implementatiemodel Hallo wensen en geslaagde/mislukte retourneren als Hallo bronnen geschikt voor migratie zijn.

U selecteert Hallo virtueel netwerk of een cloudservice (indien dit niet in een virtueel netwerk is) wilt u toovalidate voor migratie.

* Als het Hallo-bron is niet geschikt is voor migratie, bevat hello Azure-platform alle Hallo redenen waarom niet ondersteund voor migratie.

#### <a name="checks-not-done-in-validate"></a>Controleert niet uitgevoerd in valideren

Valideren alleen analyseert Hallo status van resources in het klassieke implementatiemodel Hallo Hallo bewerking. Om alle fouten en niet-ondersteunde scenario's vanwege toovarious configuraties in het klassieke implementatiemodel Hallo u kunt controleren. Het is niet mogelijk toocheck voor alle problemen die hello Azure Resource Manager-stack aan Hallo resources tijdens de migratie opleggen kan. Deze problemen zijn alleen gecontroleerd wanneer Hallo resources ondergaan transformatie in de volgende stap Hallo van migratie, dat wil zeggen voorbereiden. Hallo in de volgende tabel geeft een lijst van alle Hallo problemen ingecheckt niet valideren.


|Netwerken incheckt niet valideren|
|-|
|Een virtueel netwerk dat ER- en VPN-gateways|
|Virtuele netwerkverbinding van het type gateway in staat verbinding verbreken|
|Alle ER circuits zijn vooraf gemigreerde tooAzure Resource Manager-stack|
|Azure Resource Manager-quotum controleert op netwerkbronnen, dat wil zeggen, statische openbare IP-adres, dynamische openbare IP-adressen, Load Balancer, Netwerkbeveiligingsgroepen, routetabellen, netwerkinterfaces |
| Controleer of alle regels van de load balancer geldig voor implementatie/VNET zijn |
| Controleer voor conflicterende persoonlijke IP-adressen tussen virtuele machines stoppen ongedaan in Hallo dezelfde VNET |

### <a name="prepare"></a>Voorbereiden
Hallo voorbereiden bewerking is de tweede stap Hallo Hallo-migratieproces. Hallo-doel van deze stap toosimulate Hallo transformatie van Hallo IaaS resources van klassieke implementatie model tooResource Manager-resources is en dit naast elkaar voor u toovisualize.

> [!NOTE] 
> Klassieke resources zijn niet gewijzigd tijdens deze stap. Het is daarom een toorun veilige stap als u om de migratie probeert. 

U selecteert Hallo virtuele netwerk of Hallo cloudservice (indien dit niet een virtueel netwerk is) wilt u tooprepare voor migratie.

* Hallo-bron is niet geschikt is voor migratie, hello Azure-platform Hiermee stopt u het migratieproces Hallo als Hallo reden waarom de bewerking is mislukt voor het voorbereiden van Hallo bevat.
* Als het Hallo-bron is geschikt voor migratie, hello Azure-platform eerst wordt vergrendeld Hallo management vlak bewerkingen voor Hallo resources onder de migratie. Bijvoorbeeld, bent u niet kunnen tooadd een gegevens schijf tooa VM onder de migratie.

Hello Azure-platform vervolgens Hallo migratie start van metagegevens van klassieke implementatie model tooResource Manager voor Hallo resources migreert.

Nadat Hallo voorbereiden is voltooid, hebt u de optie Hallo visualiseren Hallo bronnen zowel klassieke implementatiemodel en het Resource Manager. Voor elke cloudservice in het klassieke implementatiemodel Hallo hello Azure-platform maakt een Resourcegroepnaam met Hallo patroon `cloud-service-name>-Migrated`.

> [!NOTE]
> Het is niet mogelijk tooselect Hallo naam van resourcegroep gemaakt voor de gemigreerde bronnen (dat wil zeggen '-gemigreerd '), maar nadat de migratie is voltooid, kunt u Azure Resource Manager verplaatsen functie toomove resources tooany resourcegroep die u wilt gebruiken. meer informatie over deze Zie tooread [verplaatsen van resources toonew resourcegroep of abonnement](../articles/resource-group-move-resources.md)

Hier vindt u twee schermen die Hallo resultaat na een geslaagd Prepare-bewerking weergegeven. Eerste scherm ziet u een resourcegroep die de oorspronkelijke cloudservice Hallo bevat. Tweede scherm toont Hallo nieuwe '-gemigreerd ' bronnengroep die Hallo gelijkwaardige Azure Resource Manager-resources bevat.

![Schermafbeelding van portal met klassieke cloudservice](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Schermafbeelding van Azure Resource Manager-resources in voorbereiding](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Hier volgt achter de schermen kijken uw resources na voltooiing van de Hallo van fase voorbereiden. Let erop dat de resource Hallo Hallo gegevens vlak is, is dezelfde Hallo. Deze wordt weergegeven in zowel Hallo management vlak (klassieke implementatiemodel) en het Hallo besturingselement vlak (Resource Manager).

![Achter de schermen Hallo in de fase voorbereiden](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Virtuele Machines die zich niet in een klassiek virtueel netwerk zijn gestopt-de toewijzing ongedaan gemaakt in deze fase van de migratie.
>

### <a name="check-manual-or-scripted"></a>Controleren (handmatig of gepland)
In stap Hallo controle, kunt u eventueel Hallo configuratie dat u hebt gedownload eerdere toovalidate dat Hallo migratie er goed uitziet gebruiken. U kunt ook toohello portal en controle Hallo eigenschappen en resources toovalidate metagegevens migratie mooi aanmelden.

Als u een virtueel netwerk migreert, wordt de configuratie van virtuele machines meestal niet opnieuw opgestart. U kunt valideren dat Hallo toepassing nog steeds actief en werkend is voor toepassingen op deze virtuele machines.

U kunt uw bewaking/automation en operationele scripts toosee testen als Hallo VMs werkt zoals verwacht en als uw bijgewerkte scripts goed werkt. Alleen GET-bewerkingen worden ondersteund wanneer Hallo bronnen bevinden zich in Hallo status voorbereid.

Er is geen set-tijdvenster voordat u dit u toocommit Hallo migratie moet. U kunt zoveel tijd nemen als u wilt in deze fase. Hallo management vlak is echter voor deze bronnen vergrendeld totdat u afgebroken of doorgevoerd.

Als er problemen zijn, kunt u altijd afbreken Hallo migratie en het klassieke implementatiemodel toohello terug. Nadat u teruggaan wordt hello Azure-platform Hallo management vlak bewerkingen op Hallo resources geopend zodat u kunt de normale bewerkingen op deze virtuele machines in het klassieke implementatiemodel Hallo hervatten.

### <a name="abort"></a>Afbreken
Afbreken is een optionele stap toorevert uw model wijzigingen toohello klassieke implementatie gebruiken en Hallo migratie stoppen. Deze bewerking worden Hallo Resource Manager-metagegevens voor uw resources die is gemaakt in de vorige voorbereidingsstap Hallo verwijderd. 

![Achter de schermen Hallo in de fase afbreken](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Deze bewerking kan niet worden uitgevoerd nadat u de opslagbewerking Hallo hebt geactiveerd.     
>

### <a name="commit"></a>Doorvoeren
Nadat u Hallo validatie, kunt u Hallo migratie kunt doorvoeren. Resources worden niet meer weergegeven in het klassieke implementatiemodel en zijn alleen beschikbaar in Hallo Resource Manager-implementatiemodel. Hallo kunnen gemigreerde bronnen worden beheerd alleen in de nieuwe portal Hallo.

> [!NOTE]
> Dit is een idempotente bewerking. Als dit mislukt, wordt het aanbevolen dat u Hallo Voer bewerking opnieuw uit. Als dit toofail blijft, maak een ondersteuningsticket of maak een forum post met een label ClassicIaaSMigration op onze [VM forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Achter de schermen Hallo in de fase doorvoeren](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>Waar toobegin migratie?

Hier volgt een stroomdiagram dat toont hoe tooproceed met migratie

![Schermafbeelding van de migratiestappen Hallo](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>De vertaling van Resource Manager-resources van klassieke implementatie model tooAzure
U vindt het klassieke implementatiemodel Hallo en Resource Manager-weergaven van Hallo resources in de volgende tabel Hallo. Andere functies en resources worden momenteel niet ondersteund.

| Klassieke weergave | Weergave van de Resource Manager | Gedetailleerde opmerkingen |
| --- | --- | --- |
| Naam cloudservice |DNS-naam |Tijdens de migratie een nieuwe resourcegroep wordt gemaakt voor elke cloudservice met Hallo naamgevingspatroon `<cloudservicename>-migrated`. Deze resourcegroep bevat al uw resources. cloudservicenaam Hello wordt een DNS-naam die is gekoppeld aan Hallo openbaar IP-adres. |
| Virtuele machine |Virtuele machine |VM-specifieke eigenschappen worden ongewijzigd gemigreerd. Bepaalde osProfile gegevens, zoals de naam van de computer, worden niet opgeslagen in het klassieke implementatiemodel Hallo en leeg blijft na de migratie. |
| Schijfbronnen tooVM gekoppeld |TooVM impliciete schijven die zijn gekoppeld |Schijven worden niet gemodelleerd als op het hoogste niveau bronnen in Hallo Resource Manager-implementatiemodel. Ze worden gemigreerd als impliciete schijven onder Hallo VM. Alleen de schijven die zijn gekoppeld tooa VM worden momenteel ondersteund. Resource Manager virtuele machines kunnen nu gebruikmaken klassieke opslagaccounts waarmee Hallo schijven toobe eenvoudig gemigreerd zonder de updates. |
| VM-extensies |VM-extensies |Alle Hallo resource-uitbreidingen, met uitzondering van XML-extensies worden gemigreerd vanuit het klassieke implementatiemodel Hallo. |
| Certificaten van virtuele machine |Certificaten in Azure Key Vault |Als een cloudservice servicecertificaten, een nieuwe Azure sleutelkluis per cloudservice bevat en Hallo certificaten is verplaatst naar de sleutelkluis Hallo. Hallo VM's zijn bijgewerkt tooreference Hallo certificaten van de sleutelkluis Hallo. <br><br> **Opmerking:** Neem niet verwijderen Hallo keyvault zoals dit leiden Hallo VM toogo in een mislukte status tot kan. We proberen op het verbeteren van dingen in Hallo back-end zodat kluizen sleutel kan worden veilig verwijderd of samen met de Hallo VM tooa nieuw abonnement verplaatst. |
| WinRM-configuratie |WinRM-configuratie in osProfile |Windows Remote Management-configuratie wordt verplaatst ongewijzigd als onderdeel van Hallo-migratie. |
| Eigenschap van beschikbaarheidsset |Resource van beschikbaarheidsset | Beschikbaarheidsset specificatie is een eigenschap op Hallo VM in het klassieke implementatiemodel Hallo. Beschikbaarheidssets worden een resource op het hoogste niveau als onderdeel van Hallo-migratie. Hallo volgende configuraties worden niet ondersteund: meerdere beschikbaarheidssets per cloudservice of een of meer beschikbaarheidssets samen met de virtuele machines die zich niet in een beschikbaarheidsset in een cloudservice. |
| Netwerkconfiguratie op een virtuele machine |Primaire netwerkinterface |De netwerkconfiguratie op een virtuele machine wordt weergegeven als primaire netwerkbron interface Hallo na de migratie. Voor virtuele machines die zich niet in een virtueel netwerk, Hallo interne IP-adres wijzigt tijdens de migratie. |
| Meerdere netwerkinterfaces in een VM |Netwerkinterfaces |Als een virtuele machine meerdere netwerkinterfaces die zijn gekoppeld heeft, wordt elke netwerkinterface een bron op het hoogste niveau als onderdeel van de migratie Hallo in Hallo Resource Manager-implementatiemodel, samen met alle Hallo-eigenschappen. |
| Eindpuntset met gelijke taakverdeling |Load balancer |In het klassieke implementatiemodel hello toegewezen Hallo platform een impliciete load balancer voor elke cloudservice. Een nieuwe load balancer-resource is gemaakt tijdens de migratie en Hallo-taakverdeling eindpuntset wordt load balancer-regels. |
| Inkomende NAT-regels |Inkomende NAT-regels |Invoereindpunten gedefinieerd op Hallo VM zijn geconverteerde tooinbound netwerk adres vertaling regels onder Hallo load balancer tijdens de migratie Hallo. |
| VIP-adres |Openbaar IP-adres met DNS-naam |Hallo virtueel IP-adres verandert in een openbaar IP-adres en is gekoppeld aan Hallo load balancer. Een virtueel IP-adres kan alleen worden gemigreerd als er een invoereindpunt tooit toegewezen. |
| Virtueel netwerk |Virtueel netwerk |Hallo virtueel netwerk wordt gemigreerd, met alle eigenschappen, toohello Resource Manager-implementatiemodel. Een nieuwe resourcegroep wordt gemaakt met de naam Hallo `-migrated`. |
| Gereserveerde IP-adressen |Openbaar IP-adres met een statische toewijzingsmethode |Gereserveerd IP-adressen die zijn gekoppeld aan Hallo load balancer worden gemigreerd, samen met de Hallo migratie van de cloudservice Hallo of Hallo virtuele machine. Niet-gekoppelde gereserveerde IP-migratie wordt momenteel niet ondersteund. |
| Openbaar IP-adres per VM |Openbaar IP-adres met een dynamische toewijzingsmethode |openbaar IP-adres die zijn gekoppeld aan VM is geconverteerd naar een openbare IP-adresbron, met Hallo toewijzing methode set toostatic Hallo Hallo. |
| NSG's |NSG's |Netwerkbeveiligingsgroepen die zijn gekoppeld aan een subnet worden als onderdeel van Hallo migratie toohello Resource Manager-implementatiemodel gekloond. Hallo NSG in het klassieke implementatiemodel Hallo wordt niet verwijderd tijdens de migratie Hallo. Hallo management vlak bewerkingen voor Hallo NSG worden echter geblokkeerd wanneer Hallo migratie uitgevoerd wordt. |
| DNS-servers |DNS-servers |DNS-servers die zijn gekoppeld aan een virtueel netwerk of Hallo VM worden gemigreerd als onderdeel van Hallo bijbehorende Resourcemigratie, samen met alle Hallo-eigenschappen. |
| UDR's |UDR's |Gebruiker gedefinieerde routes die zijn gekoppeld aan een subnet worden als onderdeel van Hallo migratie toohello Resource Manager-implementatiemodel gekloond. Hallo UDR in het klassieke implementatiemodel Hallo wordt niet verwijderd tijdens de migratie Hallo. Hallo management vlak bewerkingen voor Hallo UDR worden geblokkeerd wanneer Hallo migratie uitgevoerd wordt. |
| De eigenschap Doorsturen via IP op de netwerkconfiguratie van een virtuele machine |De eigenschap op Hallo NIC doorsturen via IP |Hallo doorsturen via IP-eigenschap op een virtuele machine is geconverteerde tooa-eigenschap op Hallo netwerkinterface tijdens de migratie Hallo. |
| Load balancer met meerdere IP-adressen |Load balancer met meerdere openbare IP-resources |Elke openbare IP-adres die zijn gekoppeld aan Hallo load balancer geconverteerde tooa openbare IP-resource is en die zijn gekoppeld aan Hallo load balancer na de migratie. |
| Interne DNS-namen op Hallo VM |Interne DNS-namen op Hallo NIC |Tijdens de migratie zijn Hallo interne DNS-achtervoegsels voor virtuele machines Hallo gemigreerde tooa alleen-lezen eigenschap met de naam 'InternalDomainNameSuffix' op Hallo NIC. Hallo achtervoegsel ongewijzigd blijft na de migratie en VM-resolutie moet blijven toowork als voorheen. |
| Gateway voor een virtueel netwerk |Gateway voor een virtueel netwerk |Eigenschappen van de gateway voor virtuele netwerken worden ongewijzigd gemigreerd. Hallo VIP die zijn gekoppeld aan Hallo gateway verandert niet beide. |
| Lokale netwerksite |Lokale netwerkgateway |LAN site-eigenschappen zijn de nieuwe resource gemigreerde ongewijzigd tooa Local Network Gateway genoemd. Deze bevat on-premises adresvoorvoegsels en een externe gateway-IP. |
| Verwijzingen naar verbindingen |Verbinding |Na de migratie worden de verwijzingen naar verbindingen tussen de gateway en de lokale netwerksite in de netwerkconfiguratie in Resource Manager vertegenwoordigd door een nieuwe resource met de naam Verbinding. Alle eigenschappen van connectiviteit verwijzing in de configuratie van netwerkbestanden zijn verbindingsbron gekopieerde ongewijzigd toohello nieuw gemaakt. VNet-connectiviteit tooVNet in de klassieke wordt bereikt door het maken van twee IPsec-tunnels toolocal netwerksites Hallo VNets die vertegenwoordigt. Dit is de verbinding getransformeerde tooVnet2Vnet type in het resource manager-model zonder lokale netwerkgateways. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Wijzigingen tooyour automation en tooling na migratie
Als onderdeel van de migratie van uw resources van Hallo Classic deployment model toohello Resource Manager-implementatiemodel hebben tooupdate uw bestaande automatisering of tooling tooensure dat het toowork na de migratie Hallo blijft.
