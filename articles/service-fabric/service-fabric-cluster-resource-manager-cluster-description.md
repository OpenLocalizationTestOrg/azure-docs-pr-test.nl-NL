---
title: aaaCluster beschrijving van de Cluster Resource Manager | Microsoft Docs
description: Met een beschrijving van een Service Fabric-cluster door te geven voor domeinen met fouten, domeinen upgraden, eigenschappen van het knooppunt en knooppunt capaciteitswaarden voor Hallo Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Met een beschrijving van een service fabric-cluster
Hallo Service Fabric-Cluster Resource Manager biedt verschillende mechanismen voor het beschrijven van een cluster. Tijdens runtime, wordt Hallo Cluster Resource Manager gebruikt deze informatie tooensure hoge beschikbaarheid van Hallo-services in Hallo cluster wordt uitgevoerd. Bij het afdwingen van deze belangrijke regels, ook wordt geprobeerd toooptimize Hallo brongebruik binnen Hallo-cluster.

## <a name="key-concepts"></a>Belangrijkste concepten
Hallo Cluster Resource Manager biedt ondersteuning voor verschillende functies die worden beschreven van een cluster:

* Domeinen met fouten
* Upgradedomeinen
* Knooppunteigenschappen
* Capaciteit van knooppunt

## <a name="fault-domains"></a>Foutdomeinen
Een domein met fouten is een gebied van gecoördineerde is mislukt. Een enkele computer is een Foutdomein (omdat deze niet kan op een eigen voor verschillende oorzaken hebben, vanuit power supply fouten toodrive fouten toobad NIC firmware). Machines verbonden toohello dezelfde Ethernet-switch bevinden zich in hetzelfde Foutdomein als Hallo zijn machines delen één bron stroomstoring of op één locatie. Aangezien het natuurlijke voor de hardware fouten toooverlap, worden de domeinen met fouten zijn inherent hiërarchische en worden weergegeven als URI's in Service Fabric.

Het is belangrijk dat Foutdomeinen correct zijn ingesteld sinds de Service Fabric gebruikt deze informatie toosafely plaats services. Service Fabric wil niet tooplace services zodanig dat Hallo verlies van een domein met fouten (dit wordt veroorzaakt door Hallo storing van een onderdeel) een toogo service niet actief veroorzaakt. In hello Azure Service Fabric Hallo Foutdomein informatie verstrekt door Hallo omgeving toocorrectly gebruikt-omgeving configureert u Hallo knooppunten in cluster Hallo namens jou. Voor Service Fabric zelfstandige, domeinen met fouten worden gedefinieerd op moment Hallo is dat Hallo-cluster ingesteld 

> [!WARNING]
> Het is belangrijk dat Hallo Foutdomein informatie opgegeven tooService Fabric nauwkeurig is. Stel dat dat uw Service Fabric-cluster knooppunten binnen 10 virtuele machines, op vijf fysieke hosts worden uitgevoerd. In dit geval wordt er 10 virtuele machines, maar er is slechts 5 verschillende (hoogste niveau) fault-domeinen. Delen dezelfde fysieke host zorgt ervoor dat Hallo VMs tooshare Hallo foutdomein dezelfde hoofdmap, aangezien Hallo VMs ervaring fout gecoördineerd als hun fysieke host is mislukt.  
>
> Omdat Service Fabric Hallo Foutdomein van een knooppunt niet toochange verwacht. Andere mechanismen zoals hoge beschikbaarheid van virtuele machines, Hallo gezorgd [HA virtuele machines](https://technet.microsoft.com/en-us/library/cc967323.aspx), transparante migratie van virtuele machines van één host tooanother gebruiken. Deze mechanismen geen opnieuw configureren of melding Hallo code binnen Hallo VM wordt uitgevoerd. Als zodanig zijn **niet ondersteund** als omgevingen voor het uitvoeren van Service Fabric-clusters. Service Fabric moet de gebruikte beveiligingstechnologieën Hallo alleen hoge beschikbaarheid. Mechanismen zoals VM livemigratie, SAN's, of andere gebruikers zijn niet nodig. Als u gebruikt in combinatie met Service Fabric, deze mechanismen _verminderen_ toepassing beschikbaarheid en betrouwbaarheid omdat ze extra complexiteit veroorzaken gecentraliseerde bronnen van de fout toevoegen en gebruiken van betrouwbaarheid en beschikbaarheidsstrategieën die met die in Service Fabric conflicteren. 
>
>

In onderstaande afbeelding voor Hallo kleur we alle Hallo entiteiten tooFault domeinen en lijst met die alle verschillende domeinen met fouten die het resultaat Hallo bijdragen. In dit voorbeeld hebben we datacenters ('DC'), rekken ('R') en blades ("B"). Stelen, als elke blade meer dan één virtuele machine bevat, kan er een andere laag in Hallo Foutdomein hiërarchie.

<center>
![Knooppunten ingedeeld via domeinen met fouten][Image1]
</center>

Tijdens runtime, hello Service Fabric-Cluster Resource Manager-domeinen met fouten in de cluster Hallo Hallo beschouwt en indelingen plannen. Hallo stateful replica's of stateless exemplaren voor een bepaalde service worden gedistribueerd, zodat ze in afzonderlijke domeinen met fouten. Hallo service over domeinen met fouten worden verdeeld, zorgt u ervoor Hallo beschikbaarheid van Hallo-service niet is geknoeid als een Foutdomein op elk niveau van Hallo hiërarchie is mislukt.

Van service Fabric-Cluster Resource Manager niet van belang hoeveel lagen in Hallo Foutdomein hiërarchie. Echter, wordt geprobeerd tooensure die Hallo verlies van elk een deel van de hiërarchie Hallo heeft geen invloed op services die erin worden uitgevoerd. 

Het is raadzaam als er Hallo hetzelfde aantal knooppunten op elk niveau van diepte in Hallo Foutdomein hiërarchie. Als Hallo 'boomstructuur' van de domeinen met fouten in het cluster niet in balans is, maakt het moeilijker voor Hallo Cluster Resource Manager toofigure uit Hallo best toewijzing van services. Imbalanced Foutdomeinen indelingen betekenen dat Hallo verlies van bepaalde domeinen impact Hallo beschikbaarheid van services die meer dan andere domeinen. Als gevolg hiervan Hallo Cluster Resource Manager is verwijderd tussen twee doelen: deze toouse Hallo-machines in het domein 'dikke' wil dat door het plaatsen van services op deze, en deze services in andere domeinen tooplace wil zodat Hallo verlies van een domein geen problemen veroorzaken. 

Wat imbalanced domeinen eruit? In onderstaande Hallo diagram, laten we zien twee verschillende cluster indelingen. Hallo knooppunten zijn in de eerste voorbeeld Hallo gelijkmatig verdeeld over Hallo domeinen met fouten. In het tweede voorbeeld hello heeft een Foutdomein veel meer knooppunten dan Hallo andere domeinen met fouten. 

<center>
![Twee verschillende cluster indelingen][Image2]
</center>

Hallo keuze waarvan Foutdomein een knooppunt bevat wordt in Azure, voor u beheerd. Echter, afhankelijk van het aantal knooppunten die u inricht Hallo kunt u nog steeds uiteindelijk domeinen met fouten met meer knooppunten bevat dan andere. Stel dat u hebt vijf domeinen met fouten in het Hallo-cluster, maar zeven knooppunten inrichten voor een gegeven NodeType. In dit geval eindigen hello eerst twee domeinen met fouten met meer knooppunten. Als u toodeploy meer NodeTypes met alleen een aantal exemplaren doorgaat, haalt Hallo probleem slechter. Daarom die verdient het aanbeveling dat Hallo is het aantal knooppunten in elk knooppunttype een veelvoud van Hallo aantal Foutdomeinen.

## <a name="upgrade-domains"></a>Upgradedomeinen
Upgradedomeinen zijn een andere functie waarmee een Service Fabric-Cluster Resource Manager Hallo Hallo lay-out van de cluster Hallo begrijpen. Upgradedomeinen sets met knooppunten die zijn bijgewerkt op Hallo definiëren hetzelfde moment. Upgradedomeinen help Hallo Cluster Resource Manager begrijpen en te organiseren beheerbewerkingen zoals upgrades.

Upgradedomeinen zijn veel zoals domeinen met fouten, maar met enkele belangrijke verschillen. Eerst definiëren gebieden van gecoördineerde hardwarefouten domeinen met fouten. Upgrade uitvoeren van domeinen, op Hallo daarentegen, zijn gedefinieerd door het beleid. U toodecide hoeveel u wilt dat, in plaats van dit wordt bepaald door het Hallo-omgeving. U kunt zoveel Upgrade-domeinen als knooppunten hebben. Een ander verschil tussen domeinen met fouten en -domeinen upgraden is dat er geen Upgrade domeinen hiërarchische. In plaats daarvan lijken ze meer op een eenvoudige label. 

Hallo volgende diagram ziet u drie dat domeinen upgraden worden striped verdeeld over drie domeinen met fouten. U ziet ook een mogelijke plaatsing voor drie verschillende replica's van een stateful service, waar elke in verschillende domeinen met fouten en domeinen upgraden eindigt. Deze plaatsing kunt Hallo verlies van een domein met fouten in de Hallo midden van een service-upgrade en nog steeds een kopie van het Hallo-code en gegevens.  

<center>
![Plaatsing met fouten en Upgradedomeinen][Image3]
</center>

Er zijn voor- en nadelen toohaving grote aantallen domeinen upgraden. Meer domeinen upgraden betekent elke stap van het Hallo-upgrade is een meer gedetailleerd en daarom is van invloed op een kleiner aantal knooppunten of services. Als gevolg hiervan minder services hebben toomove tegelijk minder verloop Inleiding in Hallo-systeem. Dit heeft vaak tooimprove betrouwbaarheid, omdat minder Hallo-service wordt beïnvloed door een probleem tijdens de upgrade Hallo geïntroduceerd. Meer domeinen upgraden betekent ook dat u minder beschikbare buffer op andere knooppunten toohandle Hallo gevolgen Hallo upgrade nodig. Bijvoorbeeld, als u vijf upgraden domeinen hebt, afhandelt Hallo knooppunten in elk ongeveer 20% van uw verkeer. Als u tootake omlaag dat domein bijwerken voor een upgrade nodig, moet die load gewoonlijk toogo ergens. Aangezien u vier resterende upgraden domeinen hebt, moet elk voldoende ruimte voor ongeveer 5% van totale Hallo-verkeer. Meer domeinen upgraden betekent dat u minder buffer op Hallo knooppunten in Hallo cluster nodig. Denk bijvoorbeeld als er 10 domeinen upgraden in plaats daarvan. In dat geval zouden elke UD alleen worden verwerkt ongeveer 10% van totale Hallo-verkeer. Wanneer een Upgradestappen via Hallo-cluster, moet elk domein alleen toohave ruimte voor ongeveer 1.1% van de totale Hallo-verkeer. Meer domeinen upgraden kunt u in het algemeen toorun uw knooppunten op een hoger gebruik, omdat u minder gereserveerde capaciteit nodig. Hallo geldt ook voor domeinen met fouten.  

Hallo nadeel dat veel domeinen upgraden is dat upgrades tootake langer vaak. Service Fabric wacht een korte periode na een Upgrade-domein is voltooid en controleert voordat u begint tooupgrade Hallo volgende. Deze vertragingen inschakelen detecteren problemen die zijn geïntroduceerd door Hallo upgrade voordat Hallo upgrade wordt uitgevoerd. Hallo afweging is acceptabel omdat deze onjuiste wijzigingen voorkomt dat van invloed zijn op te veel van de service Hallo tegelijk.

Te weinig upgraden domeinen heeft veel negatieve neveneffecten – terwijl elke afzonderlijke upgraden domein niet actief is en een groot deel van een upgrade wordt uitgevoerd de algehele capaciteit is niet beschikbaar. Bijvoorbeeld, als u slechts drie domeinen upgraden hebt duurt u omlaag ongeveer 1/3 van uw algehele service of het cluster capaciteit tegelijk. Met zoveel van uw service niet actief in één keer niet gewenst omdat u toohave voldoende capaciteit in de rest van de werkbelasting van uw cluster toohandle Hallo Hallo hebt. Onderhoud van deze buffer houdt in dat tijdens de normale werking die knooppunten kleiner dan ze anders zou zijn geladen. Dit verhoogt de Hallo kosten van het uitvoeren van uw service.

Er is geen echte limiet toohello totale aantal fouten of domeinen upgraden in een omgeving, of de beperkingen van hoe ze elkaar overlappen. Die gezegd, er zijn enkele algemene patronen zijn:

- Domeinen met fouten en -domeinen upgraden toegewezen 1:1
- Een Upgrade Domain per knooppunt (fysieke of virtuele OS exemplaar)
- Een 'striped' of 'matrix' model waar Hallo domeinen met fouten en -domeinen upgraden vormen een matrix met computers waarop een meestal omlaag Hallo diagonaal

<center>
![Probleem- en Upgradedomein indelingen][Image4]
</center>

Er is dat geen best beantwoordt welke indeling toochoose, elk heeft een aantal voordelen en nadelen. Hallo 1FD:1UD model is bijvoorbeeld eenvoudige tooset maximaal is. Hallo is 1 Upgradedomein per knooppunt model zoals welke mensen worden gebruikt om de meeste. Elk knooppunt is tijdens upgrades onafhankelijk bijgewerkt. Dit is vergelijkbaar toohow kleine sets machines handmatig in de afgelopen Hallo zijn bijgewerkt. 

meest voorkomende Hallo-model is Hallo FD/UD matrix waar hello FDs en UDs een tabel vormen en knooppunten worden geplaatst langs Hallo diagonaal wordt gestart. Dit is standaard gebruikt in Service Fabric-clusters in Azure Hallo-model. Voor clusters met knooppunten die veel belandt alles wat u ziet eruit als Hallo compacte matrix patroon hierboven.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Beperkingen voor fouttolerantie en het upgraden van domein en het resulterende gedrag
Hallo Cluster Resource Manager beschouwt Hallo desire tookeep een service verdeeld zijn over de fout en -domeinen upgraden als een beperking. U vindt meer informatie over de beperkingen in [in dit artikel](service-fabric-cluster-resource-manager-management-integration.md). status van probleem- en Upgrade Domain beperkingen Hallo: ' voor een bepaalde service partitie moet nooit er een verschil *meer dan één* in Hallo aantal serviceobjecten (stateless service-exemplaren of stateful service replica's) tussen twee domeinen." Dit voorkomt dat bepaalde verplaatst of regelingen die strijdig zijn met deze beperking.

Bekijk een voorbeeld. Stel dat we een cluster met zes knooppunten zijn geconfigureerd met vijf domeinen met fouten en vijf domeinen upgraden hebben.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Nu gaan we spreken maken we een service met een TargetReplicaSetSize (of voor een stateless service een InstanceCount) van vijf. Hallo replica's land op N1 N5. In feite is nooit N6 gebruikt ongeacht hoeveel services zoals deze die u maakt. Maar waarom? Bekijk Hallo verschil tussen de huidige indeling Hallo en wat er gebeurt als N6 is gekozen.

Hier volgt Hallo indeling we is en Hallo aantal replica's per fouttolerantie en het upgraden van domein:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Deze indeling wordt verdeeld in termen van knooppunten per domein met fouten en het upgraden van domein. Het is ook taakverdeling in termen van Hallo aantal replica's per probleem- en Upgrade-domein. Elk domein heeft hetzelfde aantal knooppunten Hallo en Hallo hetzelfde aantal replica's.

Nu gaan we kijken wat gebeurt er als er N6 in plaats van N2 gebruikt waren. Hoe zou replica's Hallo gedistribueerd vervolgens?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Deze lay-out is in strijd met onze definitie voor Hallo Foutdomein beperking. FD0 heeft twee replica's, terwijl FD1 nul, aanbrengen Hallo verschil tussen FD0 en FD1 een totaal van twee heeft. Hallo Cluster Resource Manager is niet toegestaan voor deze benadering. Op dezelfde manier als we N2 en N6 (in plaats van N1 en N2 gekozen) dat we zouden krijgen:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Deze indeling wordt verdeeld in termen van domeinen met fouten. Echter, nu deze wordt schenden Hallo upgraden domein beperking. Dit is omdat UD0 nul replica's heeft terwijl UD1 twee heeft. Daarom wordt deze lay-out ook is ongeldig en won't worden verzameld door Hallo Cluster Resource Manager. 

## <a name="configuring-fault-and-upgrade-domains"></a>Configureren van de fout en domeinen upgraden
Domeinen met fouten en -domeinen upgraden definiëren gebeurt automatisch in Azure gehoste Service Fabric-implementaties. Service Fabric opgehaald en gebruikt Hallo omgeving gegevens uit Azure.

Als u uw eigen-cluster maakt (of een bepaalde topologie in ontwikkeling toorun wilt), kunt u Hallo Foutdomein en het upgraden van domein informatie zelf opgeven. In dit voorbeeld definiëren we een lokaal ontwikkelcluster van negen knooppunt die drie 'datacenters' (elk met drie rekken omvat). Dit cluster heeft ook drie upgraden domeinen striped verdeeld over de drie datacenters. Een voorbeeld van Hallo configuratie lager is dan: 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

via ClusterConfig.json voor zelfstandige implementaties

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Bij het definiëren van clusters via Azure Resource Manager, worden Foutdomeinen en -domeinen upgraden door Azure worden toegewezen. Hallo-definitie van uw knooppunttypen en virtuele-Machineschaalsets in uw Azure Resource Manager-sjabloon bevat daarom geen Foutdomein of domeingegevens upgraden.
>

## <a name="node-properties-and-placement-constraints"></a>Eigenschappen van het knooppunt en plaatsingsbeperkingen
U gaat soms (in feite meestal Hallo) toowant tooensure die bepaalde werkbelastingen alleen op bepaalde soorten knooppunten in cluster Hallo worden uitgevoerd. Voor kan sommige werkbelasting bijvoorbeeld vereisen GPU's of SSD's en andere niet. Een goed voorbeeld van doelen hardware tooparticular werkbelastingen is er bijna alle lagen-architectuur. Bepaalde computers fungeren als front-end- of -API voor de kant van de toepassing hello Hallo en blootgestelde toohello clients of Hallo internet. Andere machines, vaak met verschillende hardware-bronnen, verwerken Hallo werk van Hallo compute of opslag lagen. Dit zijn meestal _niet_ rechtstreeks blootgesteld tooclients of Hallo internet. Service Fabric verwacht dat er gevallen waarin bepaalde werkbelastingen toorun op specifieke hardwareconfiguraties moeten zijn. Bijvoorbeeld:

* een bestaande n-tier-toepassing is 'opgeheven en verplaatst' in een Service Fabric-omgeving
* een werklast wil toorun op specifieke hardware voor prestaties of schaal veiligheidsredenen isolatie
* Een werklast worden geïsoleerd van andere werkbelastingen omwille van beleid of de resource-verbruik

toosupport dit soort configuraties, Service Fabric is een eerste-klas begrip van de labels die toegepast toonodes worden kunnen. Deze tags worden genoemd **knooppunteigenschappen**. **Plaatsingsbeperkingen** Hallo instructies gekoppeld tooindividual-services die voor een of meer eigenschappen van het knooppunt selecteert zijn. Plaatsingsbeperkingen definiëren waar services moeten worden uitgevoerd. Hallo reeks beperkingen is extensible - een sleutel-waardepaar kunt werken. 

<center>
![Cluster-indeling verschillende werkbelastingen][Image5]
</center>

### <a name="built-in-node-properties"></a>Ingebouwd in de eigenschappen van knooppunt
Service Fabric definieert een aantal standaardeigenschappen knooppunt die automatisch kunnen worden gebruikt zonder Hallo gebruiker toodefine ze. Hallo standaardeigenschappen gedefinieerd op elk knooppunt zijn Hallo **NodeType** en Hallo **NodeName**. U kunt dus bijvoorbeeld een beperking voor plaatsing als schrijven `"(NodeType == NodeType03)"`. We hebben vindt meestal NodeType toobe een van de meest gebruikte Hallo-eigenschappen. Het is nuttig omdat deze 1:1 met een type van een machine overeenkomt. Elk type van de machine overeenkomt met tooa type werkbelasting in een traditionele n-tier-toepassing.

<center>
![Plaatsingsbeperkingen en eigenschappen van knooppunt][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Plaatsing van de beperkingen en de syntaxis van de eigenschap knooppunt 
Hallo-waarde opgegeven in de eigenschap knooppunt Hallo kan string, bool, of lang ondertekend. Hallo-instructie op Hallo service heet een plaatsing *beperking* omdat beperkt waar Hallo-service kan worden uitgevoerd in Hallo-cluster. Hallo-beperking kan elke Boole-instructie die wordt toegepast op Hallo ander knooppunteigenschappen in Hallo cluster zijn. Hallo geldig selectoren in deze instructies Boolean-waarde zijn:

1) voorwaardelijke controles voor het maken van bepaalde instructies

| Instructie | Syntaxis |
| --- |:---:|
| 'gelijk zijn aan' | "==" |
| 'is niet gelijk aan' | "!=" |
| 'die groter is dan' | ">" |
| 'groter dan of gelijk zijn aan' | ">=" |
| 'kleiner dan' | "<" |
| 'kleiner dan of gelijk aan' | "<=" |

2) Boole-instructies voor groepering en logische bewerkingen

| Instructie | Syntaxis |
| --- |:---:|
| 'en' | "&&" |
| "of" | "&#124;&#124;" |
| "niet" | "!" |
| 'als één instructie een groep' | "()" |

Hier volgen enkele voorbeelden van basisbeperking instructies.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Alleen knooppunten waar hello algemene plaatsing beperking instructie evalueert te 'True' kunnen geplaatst op het Hallo-service hebben. Knooppunten waarvoor geen een eigenschap worden gedefinieerd, komen niet overeen met de plaatsing beperkingen met die eigenschap.

Stel deze eigenschappen zijn gedefinieerd voor een bepaald knooppunt-type op het knooppunt volgt Hallo:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure. 

> [!NOTE]
> Type in uw Azure Resource Manager-sjabloon Hallo knooppunt meestal parameters wordt gebruikt. Deze eruit als '[parameters('vmNodeType1Name')]' in plaats van 'NodeType01'.
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

U kunt de plaatsing van de service maken *beperkingen* voor een service, zoals als volgt:

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Als alle knooppunten van NodeType01 geldig zijn, kunt u ook dat knooppunttype met Hallo beperking selecteren "(NodeType == NodeType01) '.

Hallo cool bewerkingen over een service plaatsingsbeperkingen is dat ze kunnen dynamisch worden bijgewerkt tijdens runtime. Dus als u wilt, kunt u een service navigeren in de cluster hello, toevoegen en verwijderen vereisten, enzovoort. Service Fabric zorgt om ervoor te zorgen dat service Hallo blijft en beschikbaar is zelfs wanneer deze typen wijzigingen worden aangebracht.

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

Plaatsingsbeperkingen zijn opgegeven voor elke andere benoemde service-exemplaar. Updates altijd uitgevoerd Hallo van (overschrijven) wat eerder is opgegeven.

Hallo cluster definitie definieert Hallo-eigenschappen op een knooppunt. Kan de eigenschappen van een knooppunt is de upgrade van een cluster configuratie vereist. Een upgrade van een knooppunt eigenschappen nodig elk knooppunt in kwestie toorestart tooreport nieuwe eigenschappen. Deze rolling upgrades worden beheerd door Service Fabric.

## <a name="describing-and-managing-cluster-resources"></a>Beschrijven en de clusterbronnen beheren
Een van de belangrijkste taken van een orchestrator is toohelp Hallo brongebruik in Hallo cluster beheren. Het beheren van clusterbronnen kan leiden tot een aantal verschillende dingen. Eerst, er ervoor zorgen dat machines zijn niet overbelast. Dit betekent om ervoor te zorgen dat machines meer services die deze kunnen verwerken worden niet uitgevoerd. Er is ten tweede Netwerktaakverdeling en optimalisatie van die kritieke toorunning services efficiënt is. Kosten effectieve of prestaties-serviceaanbiedingen gevoelige mag geen enkele toobe knooppunten hot terwijl andere koude. Hot knooppunten leiden tooresource conflicten en slechte prestaties en koude knooppunten vertegenwoordigen verspild bronnen en hogere kosten. 

Service Fabric vertegenwoordigt resources als `Metrics`. Metrische gegevens zijn logische of fysieke resource die u wilt dat toodescribe tooService Fabric. Voorbeelden van metrische gegevens zijn bijvoorbeeld 'WorkQueueDepth' of 'MemoryInMb'. Zie voor meer informatie over Hallo fysieke resources die Service Fabric kunnen van toepassing op knooppunten [resource governance](service-fabric-resource-governance.md). Zie voor meer informatie over het configureren van aangepaste metrische gegevens en het gebruik [in dit artikel](service-fabric-cluster-resource-manager-metrics.md)

Metrische gegevens zijn anders dan plaatsingen beperkingen en eigenschappen van het knooppunt. Eigenschappen van het knooppunt zijn statisch descriptors van Hallo knooppunten zelf. Metrische gegevens worden de resources die knooppunten hebben en dat services gebruiken wanneer ze worden uitgevoerd op een knooppunt beschreven. De eigenschap van een knooppunt kan 'HasSSD' en tootrue of ONWAAR kan worden ingesteld. Hallo hoeveelheid beschikbare ruimte op die SSD en hoeveel is verbruikt door services zou een metriek zoals 'DriveSpaceInMb' zijn. 

Het is belangrijk toonote die op dezelfde manier als voor plaatsingsbeperkingen en eigenschappen van het knooppunt Hallo Service Fabric-Cluster Resource Manager biedt geen begrijpen welke Hallo-namen van Hallo metrische gegevens gemiddelde. De namen van de metrische gegevens zijn alleen tekenreeksen. Het is een goede gewoonte toodeclare eenheden als onderdeel van de metrische Hallo-namen die u maakt tijdens kan dubbelzinnig zijn.

## <a name="capacity"></a>Capaciteit
Als u alle resource uitgeschakeld *balancing*, Service-Fabric-Cluster Resource Manager zou nog ervoor te zorgen dat geen knooppunt uiteindelijk via de capaciteit. Capaciteit overschrijdingen beheren is mogelijk, tenzij het Hallo-cluster is vol of Hallo werkbelasting is groter dan een willekeurig knooppunt. Capaciteit is een andere *beperking* die Hallo Cluster Resource Manager gebruikt toounderstand hoeveel van een bron op een knooppunt is. Resterende capaciteit is ook getraceerd voor Hallo cluster als geheel. Zowel Hallo capaciteit en het verbruik van Hallo op Hallo serviceniveau worden uitgedrukt in termen van metrische gegevens. Dus bijvoorbeeld Hallo metriek mogelijk 'ClientConnections' en een bepaald knooppunt heeft misschien een capaciteit voor 'ClientConnections' van 32768. Andere knooppunten kunnen andere limieten deel van de service uitgevoerd op knooppunt kunnen zeggen het momenteel verbruikt 32256 van Hallo metriek 'ClientConnections' hebben.

Tijdens runtime houdt Hallo Cluster Resource Manager resterende capaciteit in de cluster Hallo en op knooppunten. In de volgorde tootrack aftrekken capaciteit Hallo Cluster Resource Manager elke service informatie over het gebruik van capaciteit van van het knooppunt waarop Hallo-service wordt uitgevoerd. Met deze informatie kunt Hallo Service Fabric-Cluster Resource Manager kunt te achterhalen waar tooplace of verplaatsen van replica's zodat de knooppunten niet Bespreek de capaciteit.

<center>
![Clusterknooppunten en capaciteit][Image7]
</center>

C#:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Hier ziet u capaciteit die zijn gedefinieerd in het clustermanifest Hallo:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

Meestal laden een service wijzigingen dynamisch. Stel dat de belasting van een replica van 'ClientConnections' gewijzigd van 1024 too2048, maar Hallo knooppunt werd uitgevoerd op vervolgens alleen had 512 resterende voor deze metriek capaciteit. Nu die replica of de plaatsing van het exemplaar is ongeldig, omdat er niet genoeg ruimte op het knooppunt. Hallo Cluster Resource Manager heeft tookick in en Hallo knooppunt terug hieronder capaciteit ophalen. Belasting op het Hallo-knooppunt dat door een of meer van de replica's Hallo of exemplaren van dat knooppunt tooother knooppunten verplaatsen via capaciteit vermindert. Bij het verplaatsen van replica's, probeert Hallo Cluster Resource Manager toominimize Hallo kosten van deze stromen. Verplaatsingkosten wordt besproken in [in dit artikel](service-fabric-cluster-resource-manager-movement-cost.md) meer over Hallo Cluster Resource Manager strategieën de herverdeling en regels beschreven [hier](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Cluster-capaciteit
Hoe hello Service Fabric-Cluster Resource Manager behouden Hallo algehele-cluster van een te volle? Ook met de dynamische belasting bij er veel niet is kunt het doen. Services kunnen hun piek load onafhankelijk van de acties die door Hallo Cluster Resource Manager hebben. Uw cluster met genoeg ruimte vandaag is mogelijk als gevolg hiervan underpowered als u morgen opnieuw stelen. Die gezegd, er zijn een aantal besturingselementen die zijn standaard uitbreidbaar tooprevent problemen zijn. Hallo eerst doen we is voorkomt het maken van nieuwe werkbelastingen waardoor Hallo cluster toobecome volledige Hallo.

Stel dat u een stateless service maakt en of hieraan sommige load gekoppeld. Stel dat Hallo service Hallo 'DiskSpaceInMb' metriek hecht. Stel nu dat het gaat tooconsume vijf eenheden van 'DiskSpaceInMb' voor elk exemplaar van Hallo-service is. Wilt u toocreate drie exemplaren van Hallo-service. Goed gedaan. Dat betekent dat we 15 eenheden van toobe 'DiskSpaceInMb' moet aanwezig zijn op Hallo cluster zodat we tooeven worden kunnen toocreate deze service-exemplaren. Hallo Cluster Resource Manager berekent voortdurend Hallo capaciteit en het verbruik van elke metriek zodat deze kan Hallo resterende capaciteit in Hallo cluster bepalen. Als er niet voldoende ruimte, Hallo Cluster Resource Manager weigert Hallo service aanroepen van maken.

Omdat de vereiste Hallo alleen die er 15 eenheden beschikbaar zijn, kan deze ruimte veel verschillende manieren worden toegewezen. Bijvoorbeeld, kan er één resterende eenheid van de capaciteit op 15 verschillende knooppunten of drie resterende eenheden van de capaciteit van vijf verschillende knooppunten. Als Hallo Cluster Resource Manager dingen rangschikken kunt zodat er vijf eenheden beschikbaar is op drie knooppunten, wordt het Hallo-service. Opnieuw ordenen Hallo-cluster is meestal mogelijk tenzij Hallo-cluster bijna vol is of Hallo bestaande services kunnen niet worden gecombineerd om een bepaalde reden.

## <a name="buffered-capacity"></a>Buffer capaciteit
De capaciteit van de buffer is een andere functie Hallo Cluster Resource Manager. Reservering van een gedeelte van Hallo kunt algehele capaciteit van het knooppunt. Deze buffer capaciteit is alleen gebruikte tooplace services tijdens upgrades en knooppuntfouten. De capaciteit van de buffer is globaal opgegeven per metrische gegevens voor alle knooppunten. Hallo-waarde die u voor Hallo gereserveerde capaciteit kiest is een functie van Hallo aantal probleem- en Upgrade domeinen hebt u in het Hallo-cluster. Meer fouttolerantie en -domeinen upgraden betekent dat u een lager getal kunt kiezen voor de capaciteit van de buffer. Als u meer domeinen hebt, kunt u uw cluster toobe kleinere hoeveelheden niet beschikbaar verwachten tijdens upgrades en fouten. Capaciteit gebufferd geven alleen zinvol als u opgegeven Hallo knooppunt capaciteit voor een metriek hebt.

Hier volgt een voorbeeld van hoe toospecify capaciteit gebufferd:

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

gehoste clusters via ClusterConfig.json voor zelfstandige implementaties of Template.json voor Azure:

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

Hallo maken van nieuwe services mislukt wanneer het Hallo-cluster valt buiten het gebufferde capaciteit voor een metriek. Hallo maken van nieuwe services toopreserve Hallo buffer voorkomen, zorgt u ervoor dat upgrades en fouten geen knooppunten toogo overbelast veroorzaken. De capaciteit van de buffer is optioneel, maar wordt aanbevolen in een cluster dat een capaciteit voor een metriek definieert.

Hallo Cluster Resource Manager, wordt deze informatie laden. Voor elke metriek omvat deze informatie: 
  - Hallo gebufferd capaciteitsinstellingen
  - Hallo totale capaciteit
  - Hallo huidige verbruik
  - Hiermee wordt aangegeven of elke metriek wordt beschouwd als met gelijke taakverdeling of niet
  - statistieken over Hallo standaarddeviatie
  - Hallo-knooppunten die Hallo belasting voor de meeste en minimaal hebben  
  
Hieronder ziet u een voorbeeld van deze uitvoer:

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Volgende stappen
* Bekijk voor informatie over het Hallo-architectuur en de informatiestroom binnen Hallo Cluster Resource Manager, [in dit artikel](service-fabric-cluster-resource-manager-architecture.md)
* Defragmentatie metrische gegevens definiëren is eenrichtingssessie tooconsolidate belasting van de knooppunten in plaats van af te spreiden. toolearn hoe tooconfigure defragmentatie, raadpleeg dan te[in dit artikel](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Vanaf Hallo begin starten en [ophalen van een inleiding toohello Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)
* toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
