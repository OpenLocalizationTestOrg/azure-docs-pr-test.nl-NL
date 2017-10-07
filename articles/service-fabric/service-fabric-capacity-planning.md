---
title: planning voor Service Fabric-apps aaaCapacity | Microsoft Docs
description: Hierin wordt beschreven hoe tooidentify aantal rekenknooppunten die zijn vereist voor een Service Fabric-toepassing hello
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Capaciteitsplanning voor Service Fabric-toepassingen
Dit document leert u hoe tooestimate bedrag Hallo van resources (CPU, RAM-geheugen, schijf-opslag) moet u toorun uw Azure Service Fabric-toepassingen. Het is gebruikelijk voor uw resource vereisten toochange gedurende een bepaalde periode. U moet enkele bronnen normaal als u uw service ontwikkelen en testen en vervolgens meer resources nodig als u gaat u naar de productie en uw toepassing populariteit groeit. Bij het ontwerpen van uw toepassing analyseren op lange termijn Hallo-vereisten en keuzes waarmee uw service tooscale toomeet hoge vraag maken.

 Wanneer u een Service Fabric-cluster maakt, kunt u bepalen welke typen virtuele machines (VM's) aanbrengen Hallo-cluster. Elke virtuele machine wordt geleverd met een beperkte hoeveelheid resources in Hallo vorm van CPU (kernen en snelheid), netwerkbandbreedte, RAM-geheugen en schijfruimte. Als uw service gedurende een bepaalde periode groeit, kunt u tooVMs bieden grotere bronnen en/of Voeg meer virtuele machines tooyour cluster bijwerken. toodo Hallo laatstgenoemde, u moet bouwen uw service in eerste instantie zodat deze kan profiteren van nieuwe virtuele machines die toohello cluster dynamisch zijn toegevoegd.

Sommige services beheren weinig toono gegevens op Hallo VM's zelf. Capaciteitsplanning voor deze services moeten zich voornamelijk op de prestaties, wat betekent dat selecteren Hallo richten passende daarom CPU (kernen en snelheid) van Hallo virtuele machines. Bovendien moet u netwerkbandbreedte, met inbegrip van hoe vaak u netwerk overdrachten zijn optreedt en hoeveel gegevens worden overgebracht. Als uw service tooperform goed als de service usage toeneemt moet, kunt u meer virtuele machines toohello cluster toevoegen en laden van aanvragen verdelen over Hallo netwerk over alle Hallo VM's.

Voor services die grote hoeveelheden gegevens op Hallo van virtuele machines beheren, plannen van capaciteit moet zich richten voornamelijk op grootte. U moet dus zorgvuldig rekening houden Hallo-capaciteit van het RAM-geheugen en schijfruimte opslag Hallo van de virtuele machine. Hallo virtueel geheugenbeheersysteem in Windows maakt schijfruimte eruit RAM tooapplication code. Hallo Service Fabric-runtime biedt bovendien slim wisselgeheugengebruik behouden alleen hot gegevens in het geheugen en zwevend Hallo koude gegevens toodisk. Toepassingen kunnen meer geheugen hebben dan fysiek beschikbaar is op Hallo VM dus gebruiken. Prestaties, met meer RAM-geheugen gewoon worden verhoogd omdat Hallo VM meer schijfopslag in RAM-geheugen houden kunt. Hallo VM die u selecteert, moet een schijf groot genoeg toostore Hallo gegevens die u op Hallo VM wilt hebben. Op deze manier hebt Hallo VM voldoende RAM-geheugen tooprovide u met de Hallo prestaties die u wenst. Als de gegevens van uw service gedurende een bepaalde periode groeit, kunt u meer virtuele machines toohello cluster en partitie Hallo gegevens over alle Hallo VM's kunt toevoegen.

## <a name="determine-how-many-nodes-you-need"></a>Het aantal knooppunten, u moet bepalen
Partitioneren van uw service kunt u tooscale gegevens van uw service. Zie voor meer informatie over het partitioneren [partitioneren Service Fabric](service-fabric-concepts-partitioning.md). Elke partitie moet passen binnen één VM, maar meerdere (klein) partities kunnen worden geplaatst op een enkele virtuele machine. Dus hebt met meer kleine partities u meer flexibiliteit dan een paar grotere partities. Hallo afweging is dat u veel partities verhoogt de overhead van de Service Fabric en u transactiebewerkingen meerdere partities niet uitvoeren. Er is ook meer potentiële netwerkverkeer als uw servicecode moet vaak tooaccess gegevensitems die bevinden zich in verschillende partities. Bij het ontwerpen van uw service, moet u zorgvuldig overwegen deze tooarrive voor- en nadelen op een effectieve partitionering strategie.

Stel dat uw toepassing heeft een stateful service waarmee u verwacht dat de toogrow tooDB_Size GB in een jaar store grootte heeft. U bent bereid tooadd meer toepassingen (en partities) als er groei afgezien van dat jaar.  Hallo replicatie factor (RF), waarmee wordt bepaald Hallo aantal replica's voor uw service-effecten Hallo totale DB_Size. Hallo is totale DB_Size over alle replica's Hallo replicatie Factor vermenigvuldigd met DB_Size.  Node_Size vertegenwoordigt Hallo schijf ruimte/RAM-geheugen per knooppunt gewenste toouse voor uw service. Hallo DB_Size moet in het geheugen voor de beste prestaties passen tussen Hallo-cluster en een Node_Size die rond Hallo RAM Hallo die VM moet worden gekozen. Door het toewijzen van een Node_Size die groter is dan Hallo RAM capaciteit zijn u vertrouwen op Hallo paginering geleverd door Hallo Service Fabric-runtime. Prestaties van uw kan dus niet worden optimaal als uw volledige gegevens wordt beschouwd als toobe hot (sinds het vervolgens Hallo gegevens is wisselbare in/out). Voor veel services waarbij slechts een fractie van Hallo gegevens hot is, is het echter kosteneffectiever zijn.

het aantal knooppunten vereist voor maximale prestaties Hallo worden als volgt berekend:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Account voor groei
U kunt toocompute Hallo aantal knooppunten op basis van Hallo DB_Size die u van plan uw service toogrow, Daarnaast bent toohello DB_Size waarmee u bent begonnen. Aantal knooppunten Hallo vervolgens groeien wanneer uw service groeit, zodat u het aantal knooppunten Hallo niet te veel inricht. Maar Hallo aantal partities moet zijn gebaseerd op Hallo aantal knooppunten die nodig zijn wanneer u uw service op maximale groei uitvoert.

Het is goed toohave zodat u eventuele onverwachte pieken of fout verwerken kan (bijvoorbeeld als een paar virtuele machines uitvallen) een aantal extra machines beschikbaar zijn op elk gewenst moment.  Hoewel Hallo extra capaciteit moet worden bepaald met behulp van de verwachte pieken, een beginpunt tooreserve is een paar extra virtuele machines (5 tot 10 procent extra).

Hallo voorgaande wordt ervan uitgegaan dat een stateful service. Als u meer dan één stateful service hebt, hebt u tooadd hello DB_Size die zijn gekoppeld aan andere services in vergelijking met Hallo Hallo. U kunt ook het aantal knooppunten afzonderlijk voor elke stateful service Hallo berekenen.  Uw service heeft replica's of partities die niet zijn verdeeld. Houd er rekening mee dat partities ook meer gegevens dan andere hebben. Zie voor meer informatie over het partitioneren [artikel over aanbevolen procedures partitioneren](service-fabric-concepts-partitioning.md). Hallo voorgaande vergelijking is echter partitie en replica agnostisch, omdat de Service Fabric zorgt ervoor dat Hallo replica's zijn verdeeld tussen de Hallo knooppunten op een geoptimaliseerde manier.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Gebruik van een werkblad voor kostenberekening
Nu we enkele real-nummers in Hallo formule. Een [voorbeeld werkblad](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) ziet u hoe tooplan Hallo capaciteit voor een toepassing met drie typen van gegevensobjecten. Voor elk object geschatte we de grootte en hoeveel objecten dat naar verwachting krijgt toohave. We ook selecteren het aantal replica's we van elk objecttype willen. Hallo werkblad berekent de totale hoeveelheid geheugen toobe opgeslagen in de cluster Hallo Hallo.

We Voer vervolgens een VM-grootte en de maandelijkse kosten. Op basis van VM-grootte hello, vertelt Hallo werkblad dat u Hallo minimum aantal partities die moet u uw gegevens toophysically past toosplit op Hallo knooppunten. U kunt een groter aantal partities tooaccommodate die specifiek berekening en netwerk-verkeer van uw toepassing moet mogelijk wenst. Hallo werkblad toont Hallo aantal partities die u Hallo profiel gebruikersobjecten beheert is toegenomen van één toosix.

Op basis van deze informatie, Hallo werkblad wordt nu dat u alle Hallo-gegevens met Hallo gewenst partities en replica's op een 26-node cluster fysiek kan ophalen. Echter, dit cluster zou worden veel verpakt, zodat u een aantal extra knooppunten tooaccommodate knooppuntfouten en upgrades kunt. Hallo werkblad wordt ook weergegeven dat meer dan 57 knooppunten te hoeven geen extra waarde biedt omdat u leeg knooppunten zou hebben. Nogmaals, kunt u toogo hierboven 57 knooppunten toch tooaccommodate knooppuntfouten en upgrades. U kunt Hallo werkblad toomatch specifieke behoeften van uw toepassing aanpassen.   

![Werkblad voor kostenberekening][Image1]

## <a name="next-steps"></a>Volgende stappen
Bekijk [partitioneren Service Fabric-services] [ 10] toolearn meer over het partitioneren van uw service.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
