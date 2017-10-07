---
title: aaaScale een Service Fabric-cluster in- of | Microsoft Docs
description: Service Fabric-cluster in- of toomatch demand schalen door het instellen van regels voor automatisch schalen voor elk knooppunt type/virtuele-machineschaalset. Toevoegen of verwijderen van knooppunten tooa Service Fabric-cluster
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Schalen van een Service Fabric-cluster in- of met regels voor automatisch schalen
Virtuele-machineschaalsets zijn een Azure compute-resource toodeploy gebruiken en beheren van een verzameling van virtuele machines als een set. Elk knooppunttype dat is gedefinieerd in een Service Fabric-cluster is ingesteld als een afzonderlijke virtuele-machineschaalset. Elk knooppunttype kan vervolgens worden uitgebreid of uit onafhankelijk, hebben verschillende sets van poorten openen en andere capaciteitsmetrieken kan hebben. Lees meer over in Hallo [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) document. Aangezien Hallo Service Fabric-typen voor knooppunten in het cluster zijn gemaakt van de virtuele-machineschaalsets op Hallo back-end, moet u tooset van regels voor automatisch schalen voor elk knooppunt type/virtuele-machineschaalset.

> [!NOTE]
> Uw abonnement moet voldoende kernen tooadd Hallo van nieuwe virtuele machines die gezamenlijk dit cluster hebben. Er is geen modelvalidatie, er dus een tijd implementatie mislukt als een van de quotalimieten voor Hallo zijn bereikt.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Kies Hallo knooppunt type/virtuele-machineschaalset tooscale instellen
Op dit moment niet kunnen toospecify Hallo automatisch schalen regels voor virtuele-machineschaalsets met de portal hello, dus laat ons gebruik van Azure PowerShell (1.0 +) toolist Hallo knooppunttypen en voeg vervolgens automatisch schalen regels toothem.

tooget hello lijst van de VM-die schaalset gezamenlijk van uw cluster, Hallo volgende cmdlets worden uitgevoerd:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Instellen van regels voor automatisch schalen voor Hallo knooppunt type/virtuele-machineschaalset
Als uw cluster typen met meerdere knooppunten heeft, Herhaal dat dit voor elk knooppunt typen/virtuele-machineschaalset ingesteld dat het gewenste tooscale (inkomend of uitgaand). Account Hallo aantal knooppunten rekening die u hebt nodig voordat u een automatische schaling instellen. minimum aantal knooppunten die u voor het primaire knooppunttype Hallo hebt nodig Hallo wordt aangedreven door Hallo betrouwbaarheid niveau die u hebt gekozen. Lees meer over [betrouwbaarheid niveaus](service-fabric-cluster-capacity.md).

> [!NOTE]
> Het verkleinen van Hallo primaire knooppunt type tooless dan het minimumaantal Hallo Hallo cluster instabiel maken of brengt u het naar beneden. Dit kan leiden tot verlies van gegevens voor uw toepassingen en Hallo systeemservices.
> 
> 

Hallo-functie voor automatisch schalen wordt momenteel niet aangedreven door Hallo belasting dat uw toepassingen tooService Fabric kunnen melden. Dus op dit moment Hallo wordt u automatisch geschaald uitsluitend aangedreven door Hallo-prestatiemeteritems die worden gegenereerd door elk Hallo exemplaren van virtuele machines scale set.  

Volg deze instructies [tooset up automatisch geschaald voor elke virtuele-machineschaalset](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> In een schaal omlaag scenario, tenzij uw knooppunttype duurzaamheid niveau van de goud, Zilver heeft moet u toocall hello [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) met de naam van het juiste knooppunt Hallo.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Virtuele machines tooa knooppunt type/virtuele-machineschaalset handmatig toevoegen
Volg Hallo voorbeeld/instructies in Hallo [snel starten-sjablonengalerie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Hallo aantal virtuele machines in elke Nodetype. 

> [!NOTE]
> Toevoegen van virtuele machines kost tijd, dus niet van plan bent Hallo toevoegingen toobe onmiddellijk. Dus tooadd capaciteit plannen goed in tijd, tooallow gedurende meer dan tien minuten voordat Hallo VM-capaciteit beschikbaar voor replica's Hallo is-service-exemplaren tooget geplaatst.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Virtuele machines handmatig uit Hallo primaire knooppunt type/virtuele-machineschaalset verwijderen
> [!NOTE]
> Hallo system service fabric-services worden uitgevoerd in Hallo primaire knooppunttype in uw cluster. Zo moet nooit afgesloten of Hallo aantal exemplaren in dat knooppunt types terugschroeven die kleiner zijn dan wat betrouwbaarheidslaag Hallo garandeert. Raadpleeg te[Hallo gegevens over de betrouwbaarheid tiers hier](service-fabric-cluster-capacity.md). 
> 
> 

U moet tooexecute Hallo volgende stappen één VM-instantie op een tijdstip. Hiermee kunt u systeemservices hello (en uw stateful services) toobe afsluiten op VM-instantie Hallo u wilt verwijderen en de nieuwe replica's die zijn gemaakt op andere knooppunten.

1. Voer [uitschakelen ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) met opzet 'RemoveNode' toodisable Hallo knooppunt gaat u tooremove (Hallo hoogste exemplaar in het desbetreffende knooppunttype).
2. Voer [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake ervoor dat knooppunt Hallo is inderdaad toodisabled overgegaan. Als dat niet het geval is, wacht totdat het Hallo-knooppunten is uitgeschakeld. U kunt geen wacht niet langer in deze stap.
3. Volg Hallo voorbeeld/instructies in Hallo [snel starten-sjablonengalerie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Hallo aantal virtuele machines met één die Nodetype. Hallo-instantie verwijderd is de hoogste VM-instantie Hallo. 
4. Herhaal stap 1 tot en met 3 indien nodig, maar nooit terugschroeven Hallo aantal exemplaren in Hallo primaire knooppunttypen kleiner is dan wat betrouwbaarheidslaag Hallo garandeert. Raadpleeg te[Hallo gegevens over de betrouwbaarheid tiers hier](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Virtuele machines handmatig uit Hallo niet-primaire knooppunt type/virtuele-machineschaalset verwijderen
> [!NOTE]
> Voor een stateful service moet u een bepaald aantal knooppunten toobe altijd up toomaintain beschikbaarheid en preserve status van uw service. Aan Hallo zeer minimale moet u het aantal knooppunten gelijk toohello doel replica set telling van de partitie-/ service Hallo Hallo. 
> 
> 

U moet Hallo Hallo één VM-instantie stappen te volgen op een tijdstip worden uitgevoerd. Hiermee kunt u systeemservices hello (en uw stateful services) toobe afsluiten op Hallo VM-instantie die u wilt verwijderen en nieuwe replica's gemaakt waar u anders.

1. Voer [uitschakelen ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) met opzet 'RemoveNode' toodisable Hallo knooppunt gaat u tooremove (Hallo hoogste exemplaar in het desbetreffende knooppunttype).
2. Voer [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake ervoor dat knooppunt Hallo is inderdaad toodisabled overgegaan. Als dat niet, wacht u tot Hallo van knooppunten is uitgeschakeld. U kunt geen wacht niet langer in deze stap.
3. Volg Hallo voorbeeld/instructies in Hallo [snel starten-sjablonengalerie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Hallo aantal virtuele machines met één die Nodetype. Hiermee wordt de hoogste VM-instantie Hallo nu verwijderd. 
4. Herhaal stap 1 tot en met 3 indien nodig, maar nooit terugschroeven Hallo aantal exemplaren in Hallo primaire knooppunttypen kleiner is dan wat betrouwbaarheidslaag Hallo garandeert. Raadpleeg te[Hallo gegevens over de betrouwbaarheid tiers hier](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Gedrag kunnen zich in Service Fabric Explorer
Wanneer u een cluster Hallo opschalen nieuwe Service Fabric Explorer Hallo aantal knooppunten (virtuele-machineschaalset exemplaren) die deel van Hallo-cluster uitmaken.  Wanneer u schaalt een cluster omlaag u wordt echter wel Hallo verwijderd knooppunt/VM-instantie in een slechte status weergegeven, tenzij u aanroepen [verwijderen ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) met de naam van het juiste knooppunt Hallo.   

Hier is Hallo uitleg van dit probleem.

Hallo knooppunten die worden vermeld in Service Fabric Explorer zijn afspiegeling van welke Hallo Service Fabric-systeemservices (FM specifiek) op de hoogte van het aantal knooppunten Hallo cluster had/heeft Hallo. Wanneer u Hallo virtuele-machineschaalset vastgestelde schaalt, Hallo VM is verwijderd maar FM system-service nog steeds denkt dat Hallo-knooppunt (die is toegewezen toohello VM die is verwijderd) wordt keert u terug. Dus blijft Service Fabric Explorer toodisplay dat knooppunt (Hoewel Hallo-status is mogelijk fout of een onbekend).

In de volgorde toomake ervoor dat een knooppunt wordt verwijderd wanneer een virtuele machine wordt verwijderd, hebt u twee opties:

1) Kies een duurzaamheid van goud of zilver (beschikbaar snel) voor knooppunttypen Hallo in uw cluster, waardoor u Hallo infrastructuur integratie. Die vervolgens wordt automatisch verwijderd Hallo knooppunten van de status van onze services (FM) wanneer u omlaag schalen.
Raadpleeg te[Hallo meer informatie over duurzaamheid niveaus hier](service-fabric-cluster-capacity.md)

2) Hallo VM-instantie is verkleind, hoeft u toocall hello [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Service Fabric-clusters tijd in beslag nemen een bepaald aantal knooppunten toobe up op alle Hallo volgorde toomaintain beschikbaarheid en preserve status - waarnaar wordt verwezen tooas 'onderhoud quorum'. Het wordt dus doorgaans onveilige tooshut omlaag alle Hallo-machines in de cluster Hallo tenzij u eerst hebt uitgevoerd een [volledige back-up van de staat](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Volgende stappen
Lezen Hallo tooalso na meer over het plannen van capaciteit van de cluster, upgraden van een cluster en partitioneren services:

* [De capaciteit van de cluster plannen](service-fabric-cluster-capacity.md)
* [Cluster-upgrades](service-fabric-cluster-upgrade.md)
* [Stateful services van de partitie voor maximale schaal](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
