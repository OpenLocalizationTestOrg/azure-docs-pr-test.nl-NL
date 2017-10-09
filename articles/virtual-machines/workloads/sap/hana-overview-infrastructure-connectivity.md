---
title: aaaInfrastructure en connectiviteit tooSAP HANA in Azure (grote exemplaren) | Microsoft Docs
description: Een verbinding is vereist infrastructuur toouse SAP HANA configureren in Azure (grote exemplaren).
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Infrastructuur voor SAP HANA (grote exemplaren) en de verbindingen van Azure 

Sommige definities tevoren voordat u deze handleiding leest. In [SAP HANA (grote exemplaren) overzicht en architectuur op Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) er zijn twee verschillende soorten HANA grote exemplaar eenheden met geïntroduceerd:

- S72, S72m S144, S144m, S192 en S192m die we tooas Hallo 'Type ik klasse' verwijzen van SKU's.
- S384, S384m S384xm, S576, S768 en S960 die we verwijzen tooas Hallo Type II klasse van SKU's.

Hallo klasse specificaties zijn gaat toobe in Hallo HANA grote exemplaar documentatie tooeventually verwijzen toodifferent mogelijkheden en vereisten op basis van HANA grote exemplaar SKU's gebruikt.

Er zijn andere definities die wordt vaak gebruikt:
- **Grote exemplaar stempel:** een hardware-infrastructuur stack die SAP HANA TDI gecertificeerd en specifiek toorun SAP HANA-exemplaren in Azure.
- **SAP HANA in Azure (grote exemplaren):** officiële taal voor de aanbieding Hallo in Azure toorun HANA-exemplaren in op SAP HANA TDI gecertificeerde hardware die wordt geïmplementeerd in grote exemplaar stempels in verschillende Azure-regio's. Hallo gerelateerde term **HANA grote exemplaar** kort voor SAP HANA in Azure (grote exemplaren) is en veel deze technische handleiding gebruikt.
 

Nadat de Hallo aankoop van SAP HANA in Azure (grote exemplaren) tussen u en Microsoft enterprise-accountteam Hallo is voltooid, is hello volgende informatie vereist door Microsoft toodeploy HANA grote exemplaar eenheden:

- Naam van de klant
- Zakelijke contactgegevens (inclusief e-mailadres en telefoonnummer)
- Technische contactgegevens (inclusief e-mailadres en telefoonnummer nummer)
- Technische contactpersoon netwerkgegevens (inclusief e-mailadres en telefoonnummer nummer)
- Azure-implementatie regio (VS-West, VS-Oost, Australië-Oost, Australië-Zuidoost, West-Europa en Noord-Europa vanaf juli 
- 2017)
- Bevestig SAP HANA op Azure (grote exemplaren) SKU (configuratie)
- Als al gedetailleerde in Hallo overzicht en document architectuur voor grote HANA-exemplaren voor elke Azure-regio die wordt geïmplementeerd op:
    - Een/29 IP-adresbereik voor ER P2P-verbindingen die verbinding maken met Azure VNets tooHANA grote exemplaren
    - Een/24 CIDR-blok gebruikt voor Hallo HANA grote exemplaren Server IP-adresgroep
- Hallo IP-adres bereikwaarden in Hallo VNet-adresruimte-kenmerk van elke Azure-VNet die verbinding toohello HANA grote exemplaren maakt gebruikt
- Gegevens voor elk systeem HANA grote exemplaren:
  - Gewenste hostnaam - in het ideale geval met de volledig gekwalificeerde domeinnaam.
  - Gewenste IP-adres voor Hallo HANA grote exemplaar eenheid buiten Hallo Server IP-adresgroepbereik - Houd er rekening mee dat Hallo eerste 30 IP-adressen in de servergroep van IP-adresbereik zijn gereserveerd voor intern gebruik binnen grote exemplaren HANA Hallo
  - De naam van de SAP HANA SID voor Hallo SAP HANA-exemplaar (vereist toocreate Hallo nodig SAP HANA-gerelateerde schijfvolumes). Hallo HANA SID is vereist voor het maken van machtigingen voor Hallo <sidadm> op Hallo NFS-volumes, die gekoppelde toohello HANA grote exemplaar eenheid krijgen. Dit wordt ook gebruikt als een Hallo naam onderdelen van Hallo schijfvolumes gekoppelde ophalen. Als u meer dan één HANA-exemplaar op Hallo eenheid toorun wilt, moet u toolist meerdere HANA SID's. Elke Hiermee haalt u een afzonderlijke set van volumes die zijn toegewezen.
  - Hallo groupid Hallo hana sidadm gebruiker heeft in Hallo Linux-besturingssysteem vereist toocreate Hallo nodig SAP HANA-gerelateerde schijfvolumes is. Hallo sapsys groep Hallo SAP HANA-installatie meestal gemaakt met een groeps-id 1001. Hallo hana sidadm gebruiker maakt deel uit van de groep
  - Hallo userid Hallo hana sidadm gebruiker heeft in Hallo Linux-besturingssysteem vereist toocreate Hallo nodig SAP HANA-gerelateerde schijfvolumes is. Als u meerdere exemplaren van HANA op Hallo eenheid uitvoert, moet u alle Hallo toolist <sid>adm-gebruikers 
- Azure-abonnement-ID voor hello Azure-abonnement toowhich SAP HANA op Azure HANA grote exemplaren gaat toobe rechtstreeks verbonden zijn. Dit abonnement-ID verwijst naar hello Azure-abonnement, die wordt toobe in rekening gebracht bij Hallo HANA grote exemplaar eenheid.

Nadat u Hallo informatie Microsoft bepalingen SAP HANA in Azure (grote exemplaren) en retourneert Hallo informatie nodig toolink uw Azure VNets tooHANA grote exemplaren en tooaccess Hallo HANA grote exemplaar eenheden opgeven.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Verbinding maken met virtuele Azure-machines tooHANA grote exemplaren

Zoals vermeld [SAP HANA (grote exemplaren) overzicht en architectuur op Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) Hallo minimale implementatie van grote exemplaren HANA met Hallo SAP toepassingslaag in Azure lijkt, zoals:

![Azure VNet verbonden tooSAP HANA op Azure (grote exemplaren) en on-premises](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Zoek dichter op Hallo Azure VNet aan clientzijde, we Hallo nodig voor de volgende voordelen:

- Hallo-definitie van een Azure-VNet is momenteel toobe gebruikt toodeploy Hallo virtuele machines van Hallo SAP toepassingslaag in.
- Dit automatisch betekent dat als een subnet standaard hello Azure Vnet is gedefinieerd die echt Hallo één gebruikte toodeploy Hallo VM's in.
- Hello Azure VNet dat gemaakt toohave moet ten minste één VM-subnet en één ExpressRoute-Gateway-subnet. Deze subnetten moeten Hallo IP-adresbereiken als opgegeven en die worden beschreven in de volgende secties Hallo worden toegewezen.

Ja, bekijken we iets dichter bij hello Azure VNet maken voor grote HANA-exemplaren

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Hello Azure VNet maken voor HANA grote exemplaren

>[!Note]
>Hello Azure VNet voor grote HANA-exemplaar moet worden gemaakt met behulp van hello Azure Resource Manager-implementatiemodel. Hallo oudere Azure-implementatiemodel, bekend als het klassieke implementatiemodel wordt niet ondersteund met Hallo HANA grote exemplaar oplossing.

Hallo VNet kan worden gemaakt met hello Azure-portal, PowerShell, Azure-sjabloon of Azure CLI (Zie [een virtueel netwerk maken met Azure-portal Hallo](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hallo voorbeeld te volgen, bekijken we in een VNet via hello Azure-portal is gemaakt.

Als we kijken naar Hallo definities van een Azure VNet via hello Azure-portal, bekijken we in bepaalde Hallo definities en hoe die betrekking hebben toowhat we lijst met verschillende IP-adresbereiken. Als we Hallo bedoelen **adresruimte**, bedoelen we Hallo-adresruimte die hello Azure VNet toouse is toegestaan. Deze adresruimte is ook Hallo-adresbereik dat Hallo VNet gebruikt voor het doorgeven van de BGP-route. Dit **adresruimte** kunnen hier worden weergegeven:

![Address Space van Azure VNet weergegeven in hello Azure-portal](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

In geval van Hallo voorgaande met 10.16.0.0/16, hello Azure VNet een in plaats daarvan grote en wide IP-adresbereik toouse opgegeven. Betekent dat alle Hallo IP-adresbereiken van de volgende subnetten binnen dit VNet hun bereiken binnen die adresruimte kunnen hebben. Meestal bevelen we dergelijke grote adresbereik niet voor één VNet in Azure. Maar we in Hallo-subnetten die zijn gedefinieerd in hello Azure VNet ophalen van een stapje verder kunt bekijken:

![Azure VNet-subnetten en hun IP-adresbereiken](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Zoals u ziet, bekijken we een VNet met een eerste VM-subnet (hier 'default' genoemd) en een subnet met de naam 'GatewaySubnet'.
In Hallo volgende sectie, verwijzen we toohello IP-adresbereik van Hallo subnet, waardoor 'default' hello Graphics als is aangeroepen **Azure VM-subnet IP-adresbereik**. In Hallo uit te voeren, verwijzen we toohello IP-adresbereik van Gatewaysubnet Hallo als **VNet Gateway-Subnet IP-adresbereik**. 

In geval Hallo gedemonstreerd door Hallo twee afbeeldingen hierboven ziet u dat Hallo **VNet-adresruimte** behandelt, hello **Azure VM-subnet IP-adresbereik** en Hallo **VNet Gateway-Subnet IP-adres bereik**. 

In andere gevallen waarbij tooconserve of u specifieke worden met de IP-adresbereiken, kunt u Hallo beperken **VNet-adresruimte** van een VNet-toohello specifieke bereiken door elk subnet wordt gebruikt. In dit geval kunt u Hallo **VNet-adresruimte** van een VNet als meerdere specifieke bereiken als volgt te werk:

![Azure VNet-adresruimte met twee spaties](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

In dit geval Hallo **VNet-adresruimte** heeft twee spaties gedefinieerd. Deze twee spaties zijn identiek toohello IP-adresbereiken gedefinieerd voor **Azure VM-subnet IP-adresbereik** en Hallo **VNet Gateway-Subnet IP-adresbereik.**

U kunt naamgevingsnorm die u wilt gebruiken voor deze tenant subnetten (VM-subnetten). Echter, **altijd moet er één en slechts één gateway-subnet voor elk VNet** die toohello SAP HANA op Azure (grote exemplaren) ExpressRoute-circuit is verbonden. En **deze gatewaysubnet moet altijd de naam 'GatewaySubnet'** tooensure juiste plaatsing van Hallo ExpressRoute-gateway.

> [!WARNING] 
> Het is essentieel dat Hallo gateway-subnet altijd met de naam 'GatewaySubnet'.

Meerdere VM-subnetten kunnen worden gebruikt, zelfs met behulp van niet-aaneengesloten-adresbereiken. Maar zoals eerder vermeld, deze adresbereiken moeten worden behandeld door Hallo **VNet-adresruimte** Hallo VNet in geaggregeerde vorm of in een lijst met Hallo exacte bereiken van Hallo VM-subnetten en Hallo gatewaysubnet.

Samenvatting van belangrijke feit Hallo over een Azure-VNet die verbinding tooHANA grote exemplaren maakt:

- U moet toosubmit tooMicrosoft hello **VNet-adresruimte** bij het uitvoeren van een aanvankelijke implementatie van grote HANA-exemplaren. 
- Hallo **VNet-adresruimte** mag een groter bereik die betrekking heeft op Hallo bereik voor de Azure VM-subnet IP-adresbereiken en Hallo VNet Gateway-Subnet IP-adresbereik.
- Of u kunt indienen als **VNet-adresruimte** meerdere bereiken die betrekking hebben op Hallo verschillende IP-adresbereiken van VM-subnet IP-adresbereiken en Hallo VNet Gateway-Subnet IP-adresbereik.
- Hallo gedefinieerd **VNet-adresruimte** gebruikte doorgifte van de BGP-routering is.
- Hallo-naam van het gatewaysubnet Hallo moet: **'GatewaySubnet'.**
- Hallo **VNet-adresruimte** wordt gebruikt als een filter op Hallo HANA grote exemplaar aan clientzijde tooallow of niet toestaan van verkeer toohello HANA grote exemplaar eenheden van Azure. Als Hallo BGP routinggegevens Hallo Azure VNet en Hallo IP-adresbereiken is geconfigureerd voor het filteren op Hallo HANA grote exemplaar aan clientzijde niet overeenkomen, kunnen problemen in de verbinding veroorzaakt.
- Er zijn een aantal details van het gatewaysubnet Hallo die zijn beschreven verderop in de sectie 'Verbinding te maken van een VNet tooHANA grote exemplaar ExpressRoute'



### <a name="different-ip-address-ranges-toobe-defined"></a>Verschillende IP-adresbereiken toobe gedefinieerd 

We al enkele Hallo IP-adresbereiken nodig toodeploy HANA grote exemplaren in vorige gedeelten geïntroduceerd. Maar er zijn een aantal meer IP-adresbereiken, die belangrijk zijn. We doorlopen een meer gedetailleerde informatie. Hallo verzonden volgende IP-adressen waarvan niet toobe hoeven tooMicrosoft moet toobe gedefinieerd vóór het verzenden van een aanvraag voor de initiële implementatie:

- **VNet-adresruimte:** al eerder geïntroduceerd, of zijn Hallo IP-adres range(s) u hebt toegewezen (of tooassign plannen) tooyour ruimte Adresparameter in hello Azure virtuele netwerken (VNet) verbinding maken met toohello grote SAP HANA-exemplaar -omgeving. Het is raadzaam dat deze parameter adresruimte waarde met meerdere regels bestaat uit hello Azure VM-Subnet meerdere bereiken en hello Azure Gateway subnetbereik zoals Hallo Graphics eerder is. Dit bereik mogen elkaar niet overlappen met uw on-premises of Server IP-groep of ER P2P-adresbereiken. Hoe tooget dit of deze IP-adresbereiken? Uw bedrijfsnetwerk team of service provider moet een of meerdere IP-adresbereiken, maar is of niet worden gebruikt in uw netwerk bieden. Voorbeeld: Als uw Azure VM-Subnet (Zie eerder) 10.0.1.0/24 is en uw Azure-Gateway-Subnet (Zie de volgende) 10.0.2.0/28, klikt u vervolgens de adresruimte van uw Azure-VNet is het raadzaam toobe twee regels; 10.0.1.0/24 en 10.0.2.0/28. Hoewel het Hallo-adresruimte waarden kunnen worden samengevoegd, die overeenkomt met deze toohello subnet bereiken wordt u aangeraden tooavoid onbedoeld hergebruik van niet-gebruikte IP-adresbereiken in grotere-adresruimten in toekomstige Hallo elders in uw netwerk. **Hallo VNET-adresruimte is een IP-adresbereik, die behoeften toobe tooMicrosoft verzonden tijdens het aanvragen van een aanvankelijke implementatie**

- **Azure VM-subnet IP-adresbereik:** dit IP-adresbereik, zoals eerder al besproken is Hallo een u hebt toegewezen (of tooassign plannen) toohello Azure VNet subnet parameter in uw Azure-VNET verbinding toohello grote exemplaar voor SAP HANA-omgeving . Dit IP-adresbereik is gebruikte tooassign IP-adressen tooyour virtuele Azure-machines. Hallo IP-adressen buiten dit bereik mogen tooconnect tooyour grote SAP HANA-exemplaar (s). Indien nodig, kunnen meerdere Azure VM-subnetten kunnen worden gebruikt. Een/24 CIDR-blok door Microsoft wordt aanbevolen voor elke Azure VM-Subnet. Dit adresbereik moet een deel van het Hallo-waarden die worden gebruikt in hello Azure VNet-adresruimte. Hoe tooget dit IP-adresbereik? Uw bedrijfsnetwerk team of service provider moet een IP-adresbereik op dat momenteel niet wordt gebruikt in uw netwerk bieden.

- **VNet-Gateway-Subnet IP-adresbereik:** , afhankelijk van Hallo functies die u van plan bent toouse, hello aanbevolen grootte:
   - Ultra-performance ExpressRoute-gateway: / 26-Adresblok - vereist voor de klasse Type II van SKU's
   - Integratie met VPN- en ExpressRoute met behulp van een High-performance ExpressRoute-Gateway (of kleinere): / 27-Adresblok
   - Alle andere situaties: / 28-Adresblok. Dit adresbereik moet een deel van het Hallo-waarden die in Hallo 'VNet-adresruimte' waarden gebruikt. Dit adresbereik moet een deel van het Hallo-waarden die in hello Azure VNet-adresruimte waarden moet u toosubmit tooMicrosoft gebruikt. Hoe tooget dit IP-adresbereik? Uw bedrijfsnetwerk team of service provider moet een IP-adresbereik op dat momenteel niet wordt gebruikt in uw netwerk bieden. 

- **-Adresbereik voor ER P2P-connectiviteit:** is deze Hallo IP-bereik voor de verbinding met SAP HANA grote exemplaar ExpressRoute (ER) P2P. Dit bereik van IP-adressen moet een/29 CIDR IP-adresbereik. Dit bereik mogen elkaar niet overlappen met uw on-premises of andere Azure-IP-adresbereiken. Dit IP-adresbereik is gebruikte tooset Hallo ER connectiviteit van uw Azure VNet ExpressRoute-Gateway toohello grote exemplaar voor SAP HANA-servers. Hoe tooget dit IP-adresbereik? Uw bedrijfsnetwerk team of service provider moet een IP-adresbereik op dat momenteel niet wordt gebruikt in uw netwerk bieden. **Dit bereik is een IP-adresbereik, die behoeften toobe tooMicrosoft verzonden tijdens het aanvragen van een aanvankelijke implementatie**
  
- **Server IP-Adresgroepbereik:** deze IP-adresbereik is gebruikte tooassign Hallo afzonderlijke IP-adres tooHANA grote exemplaar servers. Hallo aanbevolen subnetgrootte van het is een/24 CIDR blokkeren - maar indien nodig kan zijn kleinere tooa minimaal 64 IP-adressen te bieden. In dit bereik zijn hello eerste 30 IP-adressen gereserveerd voor gebruik door Microsoft. Zorg ervoor dat dit feit wordt verwerkt bij het kiezen van Hallo formaat van Hallo bereik. Dit bereik mogen elkaar niet overlappen met uw on-premises of andere Azure-IP-adressen. Hoe tooget dit IP-adresbereik? Uw bedrijfsnetwerk team of service provider moet een IP-adresbereik dat momenteel niet in uw netwerk gebruikt wordt bieden. Een/24 (aanbevolen) unieke CIDR toobe gebruikt voor het toewijzen van Hallo specifieke IP-adressen die nodig zijn voor SAP HANA in Azure (grote exemplaren) blokkeren. **Dit bereik is een IP-adresbereik, die behoeften toobe tooMicrosoft verzonden tijdens het aanvragen van een aanvankelijke implementatie**
 
Hoewel u toodefine nodig hebt en IP-adresbereiken Hallo bovenstaande plannen, moeten ze niet alle tooMicrosoft toobe verzonden. toosummarize hello bovenstaande Hallo IP-adresbereiken zijn van vereiste tooname tooMicrosoft zijn:

- Azure VNet adres Space(s)
- Adresbereik voor ER P2P-connectiviteit
- Server IP-adresbereik van adresgroep

Aanvullende VNets die tooconnect tooHANA grote exemplaren moet toevoegen, moet u toosubmit Hallo nieuwe Azure VNet-adresruimte u tooMicrosoft toevoegt. 

Hieronder volgt een voorbeeld van andere bereiken Hallo en enkele voorbeeld-bereiken als u nodig hebt tooconfigure en uiteindelijk tooMicrosoft bieden. Zoals u ziet, Hallo-waarde voor hello Azure VNet-adresruimte wordt niet geaggregeerd in het eerste voorbeeld hello, maar uit Hallo adresbereiken Hallo eerste Azure VM-subnet IP-adresbereik en Hallo VNet Gateway-Subnet IP-adresbereik is gedefinieerd. Met behulp van meerdere VM-subnetten binnen hello Azure VNet zou werk dienovereenkomstig door te configureren en het verzenden van Hallo extra IP Hallo-adresbereiken van aanvullende VM-subnetten als onderdeel van hello Azure VNet-adresruimte.

![IP-adresbereiken in SAP HANA vereist op minimale implementatie van Azure (grote exemplaren)](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

U hebt bovendien de mogelijkheid Hallo aggregeren van hello gegevens verzenden van tooMicrosoft. In dat geval zou Hallo adresruimte van hello Azure VNet alleen bevatten één spatie. Met behulp van Hallo IP-adresbereiken eerder in Hallo-voorbeeld gebruikt. Deze cumulatieve VNet-adresruimte kan eruitzien als:

![Tweede mogelijkheid van IP-adresbereiken in SAP HANA vereist op minimale implementatie van Azure (grote exemplaren)](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Zoals u ziet, in plaats van twee kleinere bereiken die gedefinieerd Hallo-adresruimte van hello Azure VNet hebben we een groter bereik die betrekking heeft op 4096 IP-adressen. Een grote definitie Hallo adresruimte laat de ongebruikte sommige in plaats daarvan grote gegevensreeksen. Omdat Hallo VNet-adresruimte waarde(n) worden gebruikt voor het doorgeven van de BGP-route, wordt informatie over het gebruik van ongebruikte bereiken lokale Hallo of elders in uw netwerk kunnen Routering problemen veroorzaken. Het is daarom aanbevolen tookeep Hallo die adresruimte nauw uitgelijnd met de adresruimte voor Hallo werkelijke subnet gebruikt. Indien nodig, zonder uitvaltijd op Hallo VNet, kunt u nieuwe waarden van de adresruimte altijd later toevoegen.
 
> [!IMPORTANT] 
> Elk IP-adres bereik van ER-P2P, IP-servergroep, Azure VNet-adresruimte moet **niet** met elkaar overlappen of elk andere bereik ergens anders in uw netwerk gebruikt; elk moet discreet zijn en als Hallo twee afbeeldingen eerdere weergeven niet mogelijk een subnet van een ander bereik. Als er worden overlappingen tussen bereiken optreden, hello Azure VNet kan geen verbinding maken toohello ExpressRoute-circuit.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Vervolgstappen na de adresbereiken zijn gedefinieerd
Na de Hallo IP-adresbereiken zijn gedefinieerd, moeten hello volgende activiteiten toohappen:

1. Hallo IP-adresbereiken voor Azure VNet-adresruimte, Hallo ER P2P connectiviteit en Server IP-Adresgroepbereik, samen met andere gegevens die is aangeboden aan begin van document Hallo Hallo indienen. Op dit moment, zou kunnen u ook beginnen toocreate hello VNet en Hallo VM-subnetten. 
2. Een Express Route-circuit is gemaakt door Microsoft tussen uw Azure-abonnement en Hallo HANA grote exemplaar stempel.
3. Een tenantnetwerk wordt gemaakt op Hallo grote exemplaar stempel door Microsoft.
4. Microsoft configureert netwerken in Hallo SAP HANA op Azure (grote exemplaren) infrastructuur tooaccept IP-adressen van uw Azure VNet-adresruimte die communiceert met grote HANA-exemplaren.
5. Afhankelijk van de Hallo die specifieke SAP HANA op Azure (grote exemplaren) SKU hebt aangeschaft, Microsoft wijst een compute-eenheid in een tenantnetwerk toewijzen en opslag koppelen en Hallo besturingssysteem (SUSE of Red Hat Linux) installeren. IP-adressen voor deze eenheden worden genomen buiten Hallo servergroep IP-adresbereik u tooMicrosoft verzonden.

Microsoft levert aan Hallo einde van het implementatieproces hello, Hallo tooyou gegevens te volgen:
- Informatie nodig tooconnect uw Azure-VNet(s) toohello ExpressRoute-circuit dat verbinding Azure VNets tooHANA grote exemplaren maakt:
     - Autorisatie sleutel (s)
     - ExpressRoute PeerID
- Gegevens tooaccess HANA grote exemplaren na het tot stand gebracht ExpressRoute-circuit en Azure VNet.

U vindt ook Hallo reeks HANA grote exemplaren verbinden in Hallo document [tooEnd Setup voor SAP HANA grote exemplaren eindigen](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Veel van de volgende stappen uit Hallo worden weergegeven in een voorbeeldimplementatie in dat document. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>Verbinding maken met een VNet tooHANA grote exemplaar ExpressRoute

Als u alle Hallo IP-adresbereiken gedefinieerd en zijn nu klaar Hallo gegevens terug van Microsoft, kunt u beginnen Hallo VNet die u hebt gemaakt voordat tooHANA grote exemplaren verbinding te maken. Eenmaal hello die Azure VNet wordt gemaakt, een ExpressRoute-gateway moet worden gemaakt op Hallo VNet toolink hello VNet toohello ExpressRoute-circuit dat verbinding toohello klant tenant op Hallo grote exemplaar stempel maakt.

> [!NOTE] 
> Deze stap kan too30 minuten toocomplete, duren als de nieuwe gateway Hallo in Hallo aangewezen Azure-abonnement is gemaakt en vervolgens toohello verbonden Azure VNet opgegeven.

Als er al een gateway bestaat, controleert u of het een ExpressRoute-gateway of niet is. Zo niet, Hallo gateway moet worden verwijderd en opnieuw gemaakt als een ExpressRoute-gateway. Als een ExpressRoute-gateway al gemaakt is, omdat hello die Azure VNet al is verbonden toohello ExpressRoute-circuit voor lokale connectiviteit, gaat u verder toohello VNets koppelen hieronder.

- Gebruik van beide hello (nieuwe) [Azure-portal](https://portal.azure.com/), of tooyour VNet PowerShell toocreate een ExpressRoute VPN-gateway is verbonden.
  - Als u hello Azure-portal gebruikt, voegt u een nieuwe **virtuele netwerkgateway** en selecteer vervolgens **ExpressRoute** als type Hallo-gateway.
  - Als u PowerShell in plaats daarvan hebt gekozen, downloadt u eerst en Hallo laatste gebruik [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) tooensure een optimale ervaring. Hallo opdrachten na maken een ExpressRoute-gateway. Hallo teksten voorafgegaan door een  _$_  zijn door de gebruiker gedefinieerde variabelen die behoefte toobe bijgewerkt met de specifieke informatie.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

In dit voorbeeld is Hallo HighPerformance gateway-SKU gebruikt. Uw opties zijn HighPerformance of UltraPerformance zoals Hallo alleen gateway-SKU's die worden ondersteund voor SAP HANA in Azure (grote exemplaren).

> [!IMPORTANT]
> Voor grote exemplaren HANA Hallo SKU van het type S384, S384m S384xm, S576, S768 en S960 (Type II klasse SKU's), Hallo Hallo UltraPerformance Gateway-SKU verplicht is.

### <a name="linking-vnets"></a>Vnet's koppelen

Nu dat hello Azure VNet een ExpressRoute-gateway heeft, kunt u Hallo autorisatie-informatie is geleverd door Microsoft tooconnect hello ExpressRoute-gateway toohello SAP HANA op Azure (grote exemplaren) ExpressRoute-circuit is gemaakt voor deze verbinding gebruiken. Deze stap kan worden uitgevoerd met hello Azure-portal of PowerShell. Hallo-portal wordt aanbevolen, PowerShell-instructies zijn echter als volgt. 

- U uitvoeren Hallo-opdrachten voor elk VNet-gateway met behulp van een andere AuthGUID voor elke verbinding na. Hallo eerste twee items in Hallo script volgende afkomstig zijn uit Hallo informatie geleverd door Microsoft. Hallo AuthGUID is ook een specifieke voor elk VNet en de gateway. Betekent dat als u wilt een andere Azure-VNet tooadd, moet u tooget een andere AuthID voor uw ExpressRoute-circuit dat verbinding HANA grote exemplaren in Azure maakt. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Als u tooconnect Hallo gateway toomultiple ExpressRoute-circuits die gekoppeld aan uw abonnement wilt zijn, moet u mogelijk tooexecute deze stap meer dan één keer. Bijvoorbeeld, u waarschijnlijk gaat tooconnect Hallo hetzelfde VNet Gateway toohello ExpressRoute-circuit dat Hallo VNet tooyour on-premises netwerk verbindt.

## <a name="adding-more-ip-addresses-or-subnets"></a>Meer IP-adressen of subnetten toe te voegen

Gebruik de hello Azure-portal, PowerShell of CLI wanneer meer IP-adressen of subnetten toe te voegen.

In dit geval wordt aangeraden Hallo tooadd Hallo nieuwe IP-adresbereik als nieuw bereik toohello VNet-adresruimte in plaats van een nieuw bereik geaggregeerde genereren. In beide gevallen moet u toosubmit deze wijziging tooMicrosoft tooallow connectiviteit buiten die nieuwe IP-adresbereik toohello HANA grote exemplaar eenheden in de client. U kunt een Azure-ondersteuning aanvraag tooget Hallo nieuwe VNet-adresruimte toegevoegd openen. Nadat u een bevestiging ontvangen, moet u Hallo volgende stappen uitvoeren.

toocreate een extra subnet uit hello Azure-portal, Zie het artikel Hallo [een virtueel netwerk maken met Azure-portal Hallo](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), en toocreate vanuit PowerShell, Zie [maken van een virtueel netwerk met behulp van PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Vnet's toe te voegen

U kunt na het in eerste instantie verbinding maakt met een of meer Azure VNets, tooadd extra velden die toegang SAP HANA in Azure (grote exemplaren tot). Eerst een ondersteuning van Azure-aanvraag verzendt, bevatten in die aanvraag Hallo specifieke informatie identificerende Hallo bepaald Azure-implementatie en Hallo IP-adresruimte adresbereiken Hallo Azure VNet-adresruimte. SAP HANA op Azure Service Management geeft vervolgens de benodigde informatie Hallo moet u tooconnect Hallo extra vnet's en ExpressRoute. Voor elk VNet moet u een unieke Autorisatiesleutel tooconnect toohello ExpressRoute-Circuit tooHANA grote exemplaren.

Een nieuwe Azure VNet tooadd stappen:

1. Hallo eerste stap bij het Hallo-voorbereidingsproces is voltooid, Zie Hallo _maken van Azure VNet_ sectie.
2. Hallo tweede stap van het voorbereidingsproces Hallo is voltooid, Zie Hallo _gatewaysubnet maken_ sectie.
3. tooconnect uw extra VNets toohello HANA grote exemplaar ExpressRoute-circuit, open een Azure-ondersteuningsaanvraag met informatie op Hallo van nieuwe VNet en vraagt u een nieuwe autorisatie-sleutel.
4. Nadat een melding dat Hallo autorisatie is voltooid, Hallo Microsoft geleverde autorisatiegegevens toocomplete Hallo derde stap in het voorbereidingsproces hello gebruiken, gaat u naar Hallo _VNets koppelen_ sectie.

## <a name="increasing-expressroute-circuit-bandwidth"></a>ExpressRoute-circuit bandbreedte vergroten

Neem contact op met de SAP HANA op Azure Service Management. Als u op de hoogte tooincrease Hallo bandbreedte van Hallo SAP HANA op Azure (grote exemplaren) ExpressRoute-circuit, maakt u een aanvraag voor de ondersteuning van Azure. (U kunt een verhoging van het voor een enkel circuit bandbreedte up tooa maximaal 10 Gbps aanvragen.) U ontvangt vervolgens een melding als Hallo-bewerking voltooid is; Er is geen verdere actie nodig tooenable deze hogere snelheid in Azure.

## <a name="adding-an-additional-expressroute-circuit"></a>Toevoegen van een extra ExpressRoute-circuit

Neem contact op met de SAP HANA op Azure Service Management als u wordt aangeraden dat een extra ExpressRoute-circuit is vereist, wordt een aanvraag voor de ondersteuning van Azure toocreate Maak een nieuwe ExpressRoute-circuit (en de tooget autorisatie informatie tooconnect tooit). Hallo-adresruimte die gaat worden gebruikt op Hallo die vnets moet worden gedefinieerd alvorens Hallo aanvraag, in volgorde voor SAP HANA op Azure Service Management tooprovide autorisatie.

Zodra nieuwe Hallo-circuit is gemaakt en Hallo SAP HANA van Azure Service Management-configuratie voltooid is, gaat u tooreceive melding met de gewenste tooproceed Hallo-informatie. Hallo stappen hierboven beschreven voor het maken en te verbinden Hallo nieuwe VNet toothis extra circuit. U bent niet kunnen tooconnect Azure VNets toothis extra circuit als ze al tooanother SAP HANA op Azure (grote exemplaar) ExpressRoute-circuit in Hallo verbonden hetzelfde Azure-gebied.

## <a name="deleting-a-subnet"></a>Verwijderen van een subnet

tooremove een VNet subnet, ofwel hello Azure-portal, PowerShell of CLI kan worden gebruikt. Als uw Azure VNet IP-adres bereik/Azure VNet-adresruimte een cumulatieve bereik is, is er geen volgen voor u met Microsoft. Behalve dat Hallo doorgeven VNet is nog steeds adresruimte van het BGP-route met subnet Hallo verwijderd. Als u hello Azure VNet IP-adres-bereik/Azure VNet-adresruimte gedefinieerd als meerdere IP-adresbereiken waarvan één is toegewezen tooyour verwijderd subnet, moet u die buiten uw VNet-adresruimte te verwijderen en vervolgens informeren SAP HANA op Azure-servicebeheer tooremove op Hallo bereiken die SAP HANA in Azure (grote exemplaren) is toocommunicate met toegestaan.

Hoewel er geen nog specifieke, toegewezen Azure.com instructies over het verwijderen van subnetten Hallo-proces voor het verwijderen van subnetten is omkeren Hallo van Hallo-proces voor deze toe te voegen. Zie het artikel Hallo [een virtueel netwerk maken met Azure-portal Hallo](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over het maken van subnetten.

## <a name="deleting-a-vnet"></a>Verwijderen van een VNet

Beide hello Azure-portal, PowerShell of CLI gebruiken bij het verwijderen van een VNet. SAP HANA op Azure Service Management verwijdert bestaande goedkeuringen Hallo op Hallo SAP HANA op Azure (grote exemplaren) ExpressRoute-circuit en hello Azure VNet IP-adres-bereik/Azure VNet-adresruimte voor Hallo communicatie met HANA grote exemplaren te verwijderen.

Zodra het Hallo VNet is verwijderd, opent u een Azure-ondersteuning aanvraag tooprovide Hallo IP-adresruimte range(s) toobe verwijderd.

Hoewel er geen nog specifieke, toegewezen Azure.com instructies over het verwijderen van VNets Hallo-proces voor het verwijderen van VNets is omkeren Hallo van Hallo-proces voor deze toe te voegen, die hierboven is beschreven. Zie Hallo artikelen [een virtueel netwerk maken met Azure-portal Hallo](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en [maken van een virtueel netwerk met behulp van PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over het maken van VNets.

Alles wordt verwijderd, tooensure verwijderen Hallo volgende items:

- ExpressRoute-verbinding VNet-Gateway, Hallo VNet Gateway openbare IP- en VNet

## <a name="deleting-an-expressroute-circuit"></a>Verwijderen van een ExpressRoute-circuit

een extra SAP HANA in Azure (grote exemplaren) ExpressRoute-circuit tooremove een aanvraag voor de ondersteuning van Azure met SAP HANA op Azure Service Management openen en vraag dat Hallo circuit moet worden verwijderd. U kunt binnen hello Azure-abonnement, verwijderen of behouden Hallo VNet indien nodig. Echter u Hallo verbinding tussen Hallo HANA grote exemplaren ExpressRoute-circuit moet verwijderen en Hallo VNet gateway gekoppeld.

Als u ook tooremove een VNet wilt, volgt u Hallo instructies over het verwijderen van een VNet in bovenstaande Hallo-sectie.


