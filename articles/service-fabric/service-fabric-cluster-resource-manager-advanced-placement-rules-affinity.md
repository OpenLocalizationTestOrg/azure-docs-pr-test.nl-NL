---
title: aaaService Fabric Cluster Resource Manager - affiniteit | Microsoft Docs
description: Overzicht van de affiniteit voor Service Fabric-Services configureren
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Configureren en gebruiken van serviceaffiniteit in Service Fabric
Affiniteit is een besturingselement die hoofdzakelijk toohelp eenvoudig hello overgang van grotere monolithische toepassingen in de cloud en microservices wereld Hallo is opgegeven. Dit wordt ook gebruikt als optimalisatie voor verbeterde prestaties Hallo van services, hoewel dit bijwerkingen kan hebben.

Stel dat u u brengt een grotere app of een die zojuist is niet ontworpen met microservices in gedachten, tooService Fabric (of een gedistribueerde omgeving). Dit type overgang is gebruikelijk. Begint u met de Hallo hele app naar Hallo-omgeving op te heffen, het verpakken en ervoor te zorgen dat deze goed blijft werken wordt uitgevoerd. U start splitsen in verschillende kleinere services dat alle tooeach andere praten.

Uiteindelijk merkt u dat de toepassing hello enkele problemen ondervindt. Hallo problemen vallen gewoonlijk in een van deze categorieën:

1. Sommige onderdeel X in Hallo monolithische app had een niet-gedocumenteerde afhankelijkheid voor Y-onderdeel en u deze onderdelen alleen omgezet in afzonderlijke services. Aangezien deze services zijn nu wordt uitgevoerd op andere knooppunten in cluster hello, zijn ze verbroken.
2. Deze onderdelen communiceren (lokale named-pipes | gedeeld geheugen | bestanden op schijf) en ze hoeven toobe kunnen toowrite tooa gedeeld lokale resource Prestatieoverwegingen nu. Deze harde afhankelijkheid opgehaald later verwijderd, mogelijk.
3. Alles werkt prima, maar het blijkt dat deze twee componenten daadwerkelijk chatty/prestatiegebeurtenissen gevoelige zijn. Wanneer ze deze naar de afzonderlijke services verplaatst algemene toepassingsprestaties tanked of latentie verhoogd. Als gevolg hiervan voldoet hello algemene toepassing niet aan de verwachtingen.

In dergelijke gevallen we toolose onze refactoring work niet wilt en niet wilt dat toogo back toohello monoliet. de laatste voorwaarde Hallo wenselijk zelfs als een gewone optimalisatie. Echter, totdat we Hallo onderdelen toowork natuurlijk als services ontwerpen kunt (of Hallo prestatieverwachtingen een andere manier kunnen worden opgelost) gaan we tooneed sommige beeld krijgt van plaats.

Welke toodo? U kan ook proberen affiniteit inschakelen.

## <a name="how-tooconfigure-affinity"></a>Hoe tooconfigure affiniteit
tooset up affiniteit u een affiniteitsrelatie tussen twee verschillende services definiëren. U kunt zien affiniteit als 'wijst' een service op een andere en spreken "deze service kan alleen uitgevoerd wanneer dat service wordt uitgevoerd." Soms verwezen tooaffinity als een bovenliggende/onderliggende relatie (waar u aanwijst Hallo onderliggende hello bovenliggende). Affiniteit zorgt ervoor dat Hallo replica's of exemplaren van een service zijn geplaatst op Hallo dezelfde knooppunten als die van een andere service.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Een onderliggende service alleen deel uitmaken van een relatie met één-relatie. Indien u wenste de Hallo onderliggende toobe wachtrijen tootwo bovenliggende services in één keer hebt u een aantal opties:
> - Hallo relaties reverse (hebben parentService1 en parentService2 wijst op Hallo huidige onderliggende service), of
> - Wijs een Hallo bovenliggende als een hub met conventie en alle services, wijst u op of de service hebben. 
>
> Hallo resulterende plaatsingsgedrag in Hallo cluster moet dezelfde Hallo.
>

## <a name="different-affinity-options"></a>Affiniteit van verschillende opties
Affiniteit wordt voorgesteld via een van de verschillende schema's voor correlatie en heeft twee verschillende modi. de meest voorkomende modus Hallo van affiniteit is zogeheten nonalignedaffinity zijn. Hallo in nonalignedaffinity zijn, replica's of exemplaren van andere services Hallo worden geplaatst op Hallo dezelfde knooppunten. Hallo is andere modus AlignedAffinity. Uitgelijnde affiniteit is nuttig alleen met stateful services. Configureren van twee stateful services toohave uitgelijnd affiniteit zorgt ervoor dat de primaire Hallo van deze services zijn geplaatst op Hallo dezelfde knooppunten als elke andere. Het ook ervoor zorgt dat elk paar secundaire replica's voor deze services toobe op Hallo dezelfde geplaatst knooppunten. Het is ook mogelijk (Hoewel in minder frequente) tooconfigure nonalignedaffinity zijn voor stateful services. Hallo verschillende replica's van twee stateful services zou worden uitgevoerd op Hallo Hallo dezelfde knooppunten voor nonalignedaffinity zijn, maar hun primaire kunnen terechtkomen op verschillende knooppunten.

<center>
![Affiniteit tussen modi en de gevolgen ervan][Image1]
</center>

### <a name="best-effort-desired-state"></a>Beste toestand van de moeite gewenst
Een affiniteitsrelatie is zo goed mogelijke poging. Biedt geen Hallo dezelfde garanties van onderbrengen of betrouwbaarheid waarop in Hallo dezelfde uitvoerbaar proces komt. Hallo-services in een affiniteitsrelatie zijn fundamenteel verschillende entiteiten die mislukken en onafhankelijk van elkaar worden verplaatst. Een affiniteitsrelatie kan ook afbreken, hoewel deze einden tijdelijk zijn. Beperkingen van de capaciteit kunnen bijvoorbeeld betekenen dat slechts een deel van het Hallo-objecten in Hallo affiniteitsrelatie op een bepaald knooppunt past. In dergelijke gevallen zelfs als er een affiniteitsrelatie aanwezig is, deze kan niet worden geforceerd vanwege toohello andere beperkingen. Als het dus mogelijk toodo, wordt later Hallo schending automatisch gecorrigeerd.

### <a name="chains-vs-stars"></a>Ketens versus sterren
Hallo Cluster Resource Manager is vandaag de dag niet kunnen toomodel ketens van affiniteit relaties. Dit betekent dat een service die een onderliggend element in een affiniteitsrelatie is niet een bovenliggend item in een andere affiniteitsrelatie. Als u dit type relatie toomodel wilt, hebt u effectief toomodel als een ster, in plaats van een keten. toomove van een keten tooa ster, Hallo onderste onderliggende zou in plaats daarvan bovenliggende items toohello eerste onderliggende bovenliggende zijn. Afhankelijk van Hallo rangschikking van uw services wellicht toodo dit meermalen. Als er geen service natuurlijke bovenliggende, wellicht toocreate die als een tijdelijke aanduiding fungeert. Afhankelijk van uw vereisten, u kunt ook toolook in [toepassingsgroepen](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Vs ketens. Sterren in de Context van affiniteit relaties Hallo][Image2]
</center>

Een andere ding toonote over affiniteit relaties is vandaag de dag dat ze gericht zijn. Dit betekent dat die Hallo affiniteit regel alleen geplaatst met bovenliggende Hallo Hallo kind worden afgedwongen. Niet kan worden gegarandeerd dat bovenliggende Hallo bevindt Hallo onderliggende. Het is ook belangrijk toonote die Hallo affiniteitsrelatie kan niet worden perfecte of direct afgedwongen omdat verschillende services met verschillende levenscycli hebt en kunnen mislukken en afzonderlijk verplaatsen. Stel dat plotseling over tooanother knooppunt Hallo bovenliggende mislukt omdat deze is vastgelopen. Hallo Cluster Resource Manager en Failover Manager ingang Hallo failover eerst omdat Hallo prioriteit Hallo services houden, consistente en beschikbaar is. Zodra Hallo failover is voltooid, Hallo affiniteitsrelatie is verbroken, maar Hallo Cluster Resource Manager denkt dat alles is voldoende dat totdat deze Hallo kind meldingen niet is opgeslagen met Hallo bovenliggende. Dit soort controles worden regelmatig uitgevoerd. Meer informatie over hoe Hallo Cluster Resource Manager beperkingen evalueert is beschikbaar in [in dit artikel](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), en [deze](service-fabric-cluster-resource-manager-balancing.md) wordt gesproken meer informatie over hoe tooconfigure Hallo waarop deze beperkingen zijn uitgebracht geëvalueerd.   


### <a name="partitioning-support"></a>Ondersteuning voor partitioneren
Hallo laatste toonotice over de affiniteit is affiniteit relaties worden niet ondersteund wanneer Hallo bovenliggende is gepartitioneerd. Gepartitioneerde bovenliggende services mogelijk uiteindelijk wordt ondersteund, maar tegenwoordig het is niet toegestaan.

## <a name="next-steps"></a>Volgende stappen
- Voor meer informatie over het configureren van services, [meer informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)
- toolimit services tooa klein aantal machines of verzamelen Hallo laden van services, gebruik [toepassingsgroepen](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png