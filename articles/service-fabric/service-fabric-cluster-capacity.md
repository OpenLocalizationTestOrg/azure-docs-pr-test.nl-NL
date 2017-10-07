---
title: aaaPlanning hello capaciteit voor Service Fabric-cluster | Microsoft Docs
description: Service Fabric-cluster overwegingen bij capaciteitsplanning. Nodetypes, duurzaamheid en betrouwbaarheid lagen
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Service Fabric-cluster overwegingen bij capaciteitsplanning
Voor productie-implementatie is capaciteitsplanning een belangrijke stap. Hier volgen enkele Hallo items u tooconsider hebt als onderdeel van dit proces.

* Hallo aantal knooppunt typen uw behoeften toostart cluster met uit
* Hallo-eigenschappen van elk knooppunttype (grootte, primair, internetgericht, aantal virtuele machines, enz.)
* Hallo betrouwbaarheid en duurzaamheid kenmerken van Hallo-cluster

Laat het ons kort Bekijk elk van deze items.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>Hallo aantal knooppunt typen uw behoeften toostart cluster met uit
U moet eerst toofigure uit welke Hallo-cluster dat u maakt is gebruikt voor toobe gaan en welke soorten toepassingen u van plan bent toodeploy in dit cluster. Als u niet wissen op Hallo doel van de cluster hello, u waarschijnlijk nog niet klaar tooenter Hallo capaciteitsplanning proces.

Tot stand brengen Hallo aantal knooppunttypen toostart uit met uw cluster moet.  Elk knooppunttype is toegewezen tooa virtuele-Machineschaalset. Elk knooppunttype kan vervolgens worden uitgebreid of omlaag onafhankelijk, hebben verschillende sets van poorten openen en andere capaciteitsmetrieken kan hebben. Dus Hallo besluit van het aantal knooppunttypen Hallo in wezen wordt geleverd omlaag toohello overwegingen te volgen:

* Uw toepassing beschikt over meerdere services en een van deze hoeven toobe openbare of internetverbinding? Standaard-toepassingen bevatten een front-gatewayservice die invoer ontvangt van een client en een of meer back-end-services die communiceren met Hallo front-end-services. Dus in dit geval u uiteindelijk eindigen met typen voor ten minste twee knooppunten.
* Beschikt over uw services (die gezamenlijk uw toepassing) andere infrastructuur behoeften zoals meer RAM-geheugen of hoger CPU-cycli? Bijvoorbeeld, laat het ons wordt ervan uitgegaan dat u wilt dat toodeploy bevat een front-end-service en een back-endservice toepassing hello. Hallo front-end-service kan worden uitgevoerd op kleinere virtuele machines (VM-grootten zoals D2) die poorten geopend toohello internet.  Hallo back-endservice, echter is berekening intensieve en behoeften toorun op grotere virtuele machines (met VM-grootten zoals D4 D6, D15) die geen internet gericht.
  
  In dit voorbeeld, hoewel u tooput kunt bepalen alle services op één knooppunttype Hallo, is het raadzaam dat u deze plaatsen in een cluster met twee typen van de knooppunten.  Hiermee kunt u elk type toohave distinct knooppunteigenschappen zoals verbinding met internet of VM-grootte. Hallo aantal virtuele machines kan worden geschaald onafhankelijk, evenals.  
* Omdat u niet kunt Hallo toekomstige voorspellen, gaat u met feiten die u precies weet en bepaal van Hallo aantal knooppunttypen die uw toepassingen toostart met moeten. U kunt altijd toevoegen of knooppunttypen later verwijderen. Een Service Fabric-cluster moet ten minste één knooppunttype hebben.

## <a name="hello-properties-of-each-node-type"></a>Hallo-eigenschappen van elk knooppunttype
Hallo **knooppunttype** kunnen worden beschouwd als gelijkwaardig tooroles in Cloudservices. Knooppunttypen definiëren Hallo VM-grootten, Hallo aantal virtuele machines en hun eigenschappen. Elk knooppunttype dat is gedefinieerd in een Service Fabric-cluster is ingesteld als een afzonderlijke virtuele-machineschaalset. Virtuele-machineschaalset is een Azure compute-bron kunt u toodeploy gebruiken en beheren van een verzameling van virtuele machines als een set. Wordt gedefinieerd als afzonderlijke virtuele-machineschaalset, elk knooppunttype kan vervolgens worden uitgebreid of omlaag onafhankelijk, hebben verschillende sets van poorten openen en andere capaciteitsmetrieken kan hebben.

Lees [dit document](service-fabric-cluster-nodetypes.md) voor meer informatie over Hallo relatie van Nodetypes toovirtual machineschaalset hoe tooRDP in één Hallo-exemplaren van nieuwe poorten openen enzovoort.

Uw cluster kan er meer dan één knooppunttype, maar het primaire knooppunttype hello (eerste is die u op Hallo portal definieert Hallo) moet ten minste vijf VM's voor clusters die worden gebruikt voor productieworkloads (of ten minste drie virtuele machines voor testclusters) hebben. Als u Hallo-cluster met een Resource Manager-sjabloon maakt, zoek naar **primaire** kenmerk onder Hallo knooppunt typedefinitie. het primaire knooppunttype Hallo is Hallo knooppunttype waar de Service Fabric-systeemservices worden geplaatst.  

### <a name="primary-node-type"></a>Primaire knooppunttype
Voor een cluster met typen met meerdere knooppunten moet u toochoose één van beide toobe primaire. Hier volgen Hallo kenmerken van een primaire knooppunttype:

* Hallo **minimale grootte van virtuele machines** voor het primaire knooppunttype hello wordt bepaald door Hallo **duurzaamheid laag** u kiest. Hallo standaard voor Hallo duurzaamheid laag is Brons. Schuif omlaag voor meer informatie over welke Hallo duurzaamheid laag is en het Hallo-waarden kan duren.  
* Hallo **minimum aantal virtuele machines** voor het primaire knooppunttype hello wordt bepaald door Hallo **betrouwbaarheidslaag** u kiest. Hallo standaardwaarde voor de betrouwbaarheidslaag Hallo is Zilver. Schuif omlaag voor meer informatie over welke betrouwbaarheidslaag Hallo is en het Hallo-waarden kan duren. 


* Hallo Service Fabric systeemservices (bijvoorbeeld Hallo Cluster Manager-service of Image Store-service) worden geplaatst op het primaire knooppunttype hello en in dat geval Hallo betrouwbaarheid en duurzaamheid van Hallo cluster wordt bepaald door Hallo laag waarde en duurzaamheid betrouwbaarheidslaag u hebt geselecteerd voor het primaire knooppunttype Hallo-waarde.

![Schermopname van een cluster met twee knooppunttypen ][SystemServices]

### <a name="non-primary-node-type"></a>Niet-primaire knooppunttype
Er is een primaire knooppunttype en Hallo rest van deze zijn niet-primaire voor een cluster met typen met meerdere knooppunten. Hier volgen Hallo kenmerken van een niet-primaire knooppunttype:

* Hallo minimale grootte van virtuele machines voor dit knooppunttype wordt bepaald door Hallo duurzaamheid laag die u kiest. Hallo standaard voor Hallo duurzaamheid laag is Brons. Schuif omlaag voor meer informatie over welke Hallo duurzaamheid laag is en het Hallo-waarden kan duren.  
* Hallo minimum aantal virtuele machines voor dit knooppunttype zijn. U moet echter dit nummer op basis van het aantal replica's van Hallo toepassingsservices/dat u toorun in dit knooppunttype wilt Hallo kiezen. Hallo aantal virtuele machines in een knooppunttype kan worden verhoogd, nadat u Hallo cluster hebt geïmplementeerd.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>Hallo duurzaamheid kenmerken van Hallo-cluster
Hallo duurzaamheid laag is gebruikte tooindicate toohello system Hallo rechten van uw virtuele machines met Hallo onderliggende Azure-infrastructuur. In het primaire knooppunttype hello kan deze bevoegdheid Service Fabric toopause VM niveau infrastructuur verzoeken (zoals een VM opnieuw wordt opgestart, VM terugzetten van de installatiekopie of VM-migratie) die van invloed zijn Hallo quorum vereisten voor het Hallo-systeemservices en uw stateful services. In typen van de niet-primaire knooppunten Hallo kan deze bevoegdheid VM niveau infrastructuur verzoeken zoals VM opnieuw wordt opgestart, VM terugzetten van de installatiekopie, VM-migratie enz., die van invloed zijn Hallo quorum vereisten voor uw stateful services die worden uitgevoerd in het Service Fabric-toopause.

Deze bevoegdheid wordt uitgedrukt in Hallo volgende waarden:

* Goud - Hallo infrastructuur taken gedurende een periode van twee uur per UD kunnen worden onderbroken. Goud duurzaamheid kan alleen op volledige knooppunt VM-SKU's zoals D15_V2, G5 enzovoort worden ingeschakeld.
* Zilver - hello infrastructuur taken gedurende een periode van tien minuten per UD kan worden onderbroken en is beschikbaar op alle standard VM's van één kern en hoger.
* Brons - geen bevoegdheden. Dit is de standaardinstelling Hallo. Dit niveau duurzaamheid alleen gebruiken voor knooppunttypen met _alleen_ staatloze werkbelastingen. 

> [!WARNING]
> NodeTypes uitgevoerd met Brons duurzaamheid verkrijgen _geen bevoegdheden_. Dit betekent dat infrastructuur taken die invloed zijn op uw staatloze werkbelastingen niet worden gestopt of vertraagd. Het is mogelijk dat dergelijke taken nog steeds invloed op uw werkbelastingen hebben kunnen, uitvaltijd of andere problemen veroorzaken. Voor een of andere vorm van productie werkbelasting uitgevoerd met ten minste zilver wordt aanbevolen. 
> 

U krijgt toochoose duurzaamheid niveau voor elk van de typen van de knooppunten. U kunt één type knooppunt toohave een niveau duurzaamheid goud of zilver en andere Hallo Brons in Hallo hetzelfde cluster. **Moet u het minimale aantal 5 knooppunten voor elk knooppunttype met een duurzaamheid van goud of zilver onderhouden**. 

**Voordelen van het gebruik van zilver of goud duurzaamheid niveaus**
 
1. Vermindert het aantal vereiste stappen in een bewerking voor schaal hello (dat wil zeggen, deactivering van het knooppunt en verwijder ServiceFabricNodeState heet automatisch)
2. Vermindert Hallo risico van gegevensverlies vanwege tooa klant geïnitieerde in-place VM SKU wijzigingsbewerking of bewerkingen van de Azure-infrastructuur.
     
**Nadelen van het gebruik van zilver of goud duurzaamheid niveaus**
 
1. Implementaties tooyour virtuele-Machineschaalset en andere gerelateerde Azure-resources) kunnen worden uitgesteld, kunnen een time-out of volledig door problemen in het cluster of op het niveau van de infrastructuur Hallo kunnen worden geblokkeerd. 
2. Toeneemt Hallo aantal [replica lifecycle gebeurtenissen](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (bijvoorbeeld primaire worden verwisseld) vanwege tooautomated knooppunt deactivations tijdens de bewerkingen van de Azure-infrastructuur.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Aanbevelingen voor wanneer toouse zilver of goud duurzaamheid niveaus

Gebruik zilver of goud duurzaamheid voor alle die host stateful knooppunttypen services die u verwacht dat tooscale in (VM-exemplaren verminderen) vaak, en u liever dat implementatiebewerkingen voor het vereenvoudigen van deze schaal in bewerkingen worden uitgesteld. Hallo scale-out scenario's (toe te voegen exemplaren van virtuele machines) in uw keuze van Hallo duurzaamheid laag niet worden afgespeeld, heeft alleen schaal in.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Operationele aanbevelingen voor het Hallo-knooppunt typt u dat u hebt ingesteld toosilver of goud duurzaamheid niveau.

1. Uw cluster en de toepassingen gezond te houden te allen tijde en zorg ervoor dat toepassingen tooall reageren [replica lifecycle gebeurtenissen Service](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (zoals het maken van replica is vastgelopen) op tijdige wijze.
2. Vast veiliger manieren toomake een wijziging in de VM SKU (schaal omhoog/omlaag): het wijzigen van de VM-SKU van een virtuele-Machineschaalset inherent is Hallo een onveilige bewerking en kan dus moeten worden vermeden indien mogelijk. Hier volgt Hallo proces kunt u veelvoorkomende problemen tooavoid volgen.
    - **Voor niet-primaire nodetypes:** het is raadzaam dat u nieuwe virtuele-Machineschaalset maken, Hallo service plaatsing tooinclude Hallo nieuwe virtuele-Machineschaalset/knooppunt beperkingstype wijzigen en verlaagt u Hallo oude virtuele-Machineschaalset exemplaar aantal too0, één knooppunt tegelijk (dit is toomake of verwijdering van Hallo knooppunten hebben geen invloed Hallo betrouwbaarheid van Hallo cluster).
    - **Voor de primaire nodetype Hallo:** onze aanbeveling is VM SKU van het primaire knooppunttype Hallo niet te wijzigen. Als Hallo reden voor hello nieuwe SKU capaciteit is, we raden aan toe te voegen meer exemplaren of, indien mogelijk, maak een nieuw cluster. Als u geen keuze hebt, brengt u wijzigingen toohello virtuele Machine Scale ingesteld Model definition tooreflect Hallo nieuwe SKU. Als uw cluster slechts één nodetype heeft, zorgt u ervoor dat alle stateful toepassingen tooall reageren [replica lifecycle gebeurtenissen Service](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (zoals het maken van replica is vastgelopen) in een tijdige wijze en dat de replica van de service opnieuw samenstellen duur is minder dan vijf minuten (voor zilver duurzaamheid niveau). 


> [!WARNING]
> Veranderende Hallo VM SKU-grootte voor VM-Schaalsets niet ten minste zilver duurzaamheid wordt uitgevoerd, is niet aanbevolen. VM-SKU-grootte wijzigen is een gegevens-destructieve in-place infrastructuur-bewerking. Zonder enige mogelijkheid toodelay of de monitor deze wijziging is het mogelijk dat Hallo-bewerking kan ertoe leiden dataloss voor stateful services dat of ertoe leiden andere onvoorziene gebruiksproblemen, zelfs voor staatloze werkbelastingen dat. 
> 
    
3. Het minimale aantal vijf knooppunten voor alle virtuele-Machineschaalset met MR ingeschakeld onderhouden
4. Willekeurige VM-instanties verwijderen, gebruik altijd de virtuele-Machineschaalset scale omlaag functie niet. Hallo verwijdering van VM-instanties van willekeurige heeft een potentieel evenwicht maken in Hallo verdeeld over UD en FD VM-instantie. Deze onbalans kan Hallo systemen mogelijkheid tooproperly taakverdeling voor de replica's Hallo service-exemplaren/Service nadelig beïnvloeden.
6. Als u automatisch schalen, stelt u Hallo regels zodat schaal (Bezig met verwijderen van de VM-instanties) slechts één knooppunt tegelijk worden uitgevoerd. Het verkleinen van meer dan één exemplaar tegelijk is niet veilig.
7. Als het verkleinen van een primaire knooppunttype, moet u deze nooit omlaag meer dan welke betrouwbaarheidslaag Hallo kunt schalen.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>Hallo betrouwbaarheidskenmerken van Hallo-cluster
Hallo betrouwbaarheidslaag wordt gebruikt tooset Hallo aantal replica's van systeemservices Hallo dat u wilt dat toorun in dit cluster op het primaire knooppunttype Hallo. Hallo meer Hallo aantal replica's, hello betrouwbaarder Hallo systeemservices zijn in uw cluster.  

Hallo betrouwbaarheidslaag kan duren voordat Hallo volgende waarden:

* Platina - Run Hallo systeemservices met een doelreplica aantal 9 instellen
* Goud - Run Hallo systeemservices met een doelreplica aantal 7 instellen
* Silver - Hallo systeemservices uitvoeren met een telling doel replica set van 5 
* Brons - Run Hallo systeemservices met een doel replica set telling van 3

> [!NOTE]
> Hallo betrouwbaarheidslaag u bepaalt Hallo kunt u het minimum aantal knooppunten dat het primaire knooppunttype moet hebben. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Aanbevelingen voor de betrouwbaarheidslaag Hallo.

 Wanneer u vergroten of Hallo grootte van uw cluster (Hallo som van de VM-exemplaren in typen van alle knooppunten verkleinen), moet u de betrouwbaarheid van uw cluster in één laag tooanother Hallo bijwerken. Dit activeert Hallo upgrades nodig toochange Hallo system services replica set aantal clusters. Hallo-upgrade in voortgang toocomplete wacht voordat u een andere wijzigingen toohello cluster, zoals het toevoegen van knooppunten.  U kunt Hallo voortgang van Hallo upgrade in Service Fabric Explorer of door te voeren [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Hier volgt Hallo aanbeveling op Hallo betrouwbaarheidslaag kiezen.

| **De clustergrootte van het** | **Betrouwbaarheidslaag** |
| --- | --- |
| 1 |Geef geen parameter Betrouwbaarheidslaag Hallo, Hallo systeem berekend |
| 3 |Brons |
| 5 of 6|Zilver |
| 7 of 8 |Goud |
| 9 en hoger |Platina |




## <a name="primary-node-type---capacity-guidance"></a>Primaire knooppunttype - capaciteit richtlijnen

Hier vindt u richtlijnen voor het plannen van capaciteit voor Hallo primaire knooppunt type Hallo

1. **Aantal VM-exemplaren toorun elke werkbelasting productie in Azure:** moet u een minimale primaire knooppunt puntgrootte van 5 opgeven. 
2. **Aantal VM-exemplaren toorun testwerkbelastingen in Azure** kunt u een primaire knooppunt dat de minimale grootte van 1 of 3. cluster met één knooppunt, wordt uitgevoerd met een speciale configuratie en kan dus Hallo, schaal buiten het cluster wordt niet ondersteund. Hallo cluster met één knooppunt, heeft geen betrouwbaarheid en in de Resource Manager-sjabloon hebt u dus tooremove/niet opgeven dat de configuratie (geen instelling Hallo configuratiewaarde is niet voldoende). Als u instelt cluster met één knooppunt Hallo instellen via de portal en vervolgens Hallo-configuratie is automatisch afgehandeld. clusters met knooppunten 1 en 3 worden niet ondersteund voor het uitvoeren van de productie-workloads. 
3. **VM SKU:** primaire knooppunttype is waar Hallo systeemservices worden uitgevoerd, zodat Hallo VM SKU u kiest, moet nemen bij account Hallo algemene piekuren laden u tooplace plannen in Hallo-cluster. Hier volgt een vergelijking tooillustrate wat heb hier - van het primaire knooppunttype Hallo als uw 'longen' zien, is wat zuurstof tooyour brain bieden en dus als Hallo brain geen voldoende zuurstof krijgt, uw instantie te lijden heeft onder. 

Aangezien de capaciteitsbehoeften Hallo van een cluster wordt bepaald door de werkbelasting u van plan bent toorun in Hallo-cluster, kunnen we met kwalitatieve richtlijnen voor uw specifieke werkbelasting, maar hier is Hallo brede richtlijnen toohelp die u aan de slag

Voor productieworkloads 


- Hallo aanbevolen dat VM SKU is standaard D3 of standaard D3_V2 of een vergelijkbare met minimaal 14 GB van de lokale SSD.
- Hallo minimale ondersteund gebruik VM SKU is standaard D1 of standaard D1_V2 of een vergelijkbare met minimaal 14 GB van de lokale SSD. 
- Gedeeltelijke core zoals standaard A0 VM-SKU's worden niet ondersteund voor productieworkloads.
- Standaard A1 SKU wordt niet ondersteund voor productieworkloads voor betere prestaties.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>Niet-primaire knooppunttype - capaciteit richtlijnen voor stateful werkbelastingen

In deze richtlijnen voor stateful werkbelastingen met behulp van Service fabric is [betrouwbare verzamelingen of reliable Actors](service-fabric-choose-framework.md) die u in Hallo niet-primaire knooppunttype worden uitgevoerd.


**Aantal VM-instanties:** voor productieworkloads stateful zijn wordt aanbevolen dat u deze met een minimum- en aantal replica's van 5 uitvoeren. Dit betekent dat in de actieve status u uiteindelijk met een replica (van een replicaset) in elk domein met fouten en upgradedomein eindigen. Hallo hele betrouwbaarheid laag concept voor Hallo primaire knooppunttype een toospecify manier is deze instelling voor systeemservices. Hallo dus dezelfde tooyour stateful services ook is van toepassing.

Voor productieworkloads dus Hallo minimale aanbevolen niet - primaire knooppunt puntgrootte 5, als u stateful werkbelastingen worden uitgevoerd in het.


**VM SKU:** . Dit is het knooppunttype Hallo waar uw toepassingsservices worden uitgevoerd, dus Hallo VM SKU u kiest, moet rekening account Hallo piekbelasting u van plan bent tooplace in elk knooppunt. Hallo capaciteitsbehoeften van Hallo nodetype, wordt bepaald door de werkbelasting dat u van plan bent toorun in Hallo-cluster, zodat we u niet met kwalitatieve richtlijnen voor uw specifieke werkbelasting opgeven, maar hier wordt Hallo brede richtlijnen toohelp die u aan de slag

Voor productieworkloads 

- Hallo aanbevolen dat VM SKU is standaard D3 of standaard D3_V2 of een vergelijkbare met minimaal 14 GB van de lokale SSD.
- Hallo minimale ondersteund gebruik VM SKU is standaard D1 of standaard D1_V2 of een vergelijkbare met minimaal 14 GB van de lokale SSD. 
- Gedeeltelijke core zoals standaard A0 VM-SKU's worden niet ondersteund voor productieworkloads.
- Standaard A1 SKU wordt specifiek niet ondersteund voor productieworkloads voor betere prestaties.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>Niet-primaire knooppunttype - capaciteit richtlijnen voor staatloze werkbelastingen

In deze richtlijnen staatloze werkbelastingen die u op Hallo niet-primaire nodetype uitvoert.

**Aantal VM-instanties:** voor productieworkloads staatloze zijn Hallo minimale ondersteund niet - primaire knooppunt type grootte is 2. Hiermee kunt u toorun u twee staatloze exemplaren van uw toepassing en zodat uw service toosurvive Hallo verlies van een VM-instantie. 

> [!NOTE]
> Als uw cluster wordt uitgevoerd op een service fabric-versie lager dan 5.6, vanwege tooa defect in Hallo runtime (dit probleem is opgelost als 5.6), het verkleinen van een niet-primaire knooppunt type tooless dan 5, resulteert in het cluster health schakelen slechte, totdat u aanroepen [ Verwijder ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) met de naam van het juiste knooppunt Hallo. Lees [Service Fabric-cluster uitvoeren in- of](service-fabric-cluster-scale-up-down.md) voor meer informatie
> 
>

**VM SKU:** . Dit is het knooppunttype Hallo waar uw toepassingsservices worden uitgevoerd, dus Hallo VM SKU u kiest, moet rekening account Hallo piekbelasting u van plan bent tooplace in elk knooppunt. Hallo capaciteitsbehoeften van Hallo nodetype, wordt bepaald door de werkbelasting dat u van plan bent toorun in Hallo-cluster, zodat we u niet met kwalitatieve richtlijnen voor uw specifieke werkbelasting opgeven, maar hier wordt Hallo brede richtlijnen toohelp die u aan de slag

Voor productieworkloads 


- Hallo aanbevolen dat VM SKU is standaard D3 of standaard D3_V2 of gelijkwaardig. 
- Hallo minimale ondersteund gebruik VM SKU is standaard D1 of standaard D1_V2 of gelijkwaardig. 
- Gedeeltelijke core zoals standaard A0 VM-SKU's worden niet ondersteund voor productieworkloads.
- Standaard A1 SKU wordt niet ondersteund voor productieworkloads voor betere prestaties.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Volgende stappen
Zodra u klaar bent met het plannen van capaciteit en een cluster instellen, lezen Hallo volgende:

* [Beveiliging voor service Fabric-cluster](service-fabric-cluster-security.md)
* [Service Fabric health model Inleiding](service-fabric-health-introduction.md)
* [Relatie van Nodetypes tooVirtual machine schaal ingesteld](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
