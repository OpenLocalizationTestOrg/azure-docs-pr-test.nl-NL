---
title: 'Beveiliging voor service Fabric-cluster: client rollen | Microsoft Docs'
description: In dit artikel beschrijft Hallo twee client rollen en Hallo machtigingen toohello rollen opgegeven.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Toegangsbeheer op basis van rollen voor Service Fabric-clients
Azure Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn: beheerder en gebruiker. Toegangsbeheer kunt Hallo beheerder toolimit toegang toocertain cluster clusterbewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken.  

**Beheerders** hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Standaard **gebruikers** hebben alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.

U opgeven Hallo twee client rollen (administrator en client) gelijktijdig Hallo met maken van het cluster door afzonderlijke certificaten voor elk. Zie [Service Fabric-clusterbeveiliging](service-fabric-cluster-security.md) voor meer informatie over het instellen van een beveiligde Service Fabric-cluster.

## <a name="default-access-control-settings"></a>Instellingen voor toegangsbeheer standaard
Hallo beheerder toegang besturingselementtype heeft volledige toegang tooall hello FabricClient APIs. Het kunt lees- en schrijfbewerkingen op Hallo Service Fabric-cluster, inclusief Hallo volgende bewerkingen uitvoeren:

### <a name="application-and-service-operations"></a>Toepassing en service-activiteiten
* **CreateService**: service maken                             
* **CreateServiceFromTemplate**: service gemaakt op basis van sjabloon                             
* **UpdateService**: service-updates                             
* **DeleteService**: verwijderen van een service                             
* **ProvisionApplicationType**: toepassing type inrichting                             
* **SubmitMetadata**: maken van de toepassing                               
* **DeleteApplication**: toepassing verwijderen                             
* **UpgradeApplication**: starten of toepassingsupgrades onderbreken                             
* **UnprovisionApplicationType**: toepassing type hierbij                             
* **MoveNextUpgradeDomain**: toepassingsupgrades met een expliciete updatedomein hervatten                             
* **ReportUpgradeHealth**: toepassingsupgrades met de huidige upgradevoortgang Hallo hervatten                             
* **ReportHealth**: reporting health                             
* **PredeployPackageToNode**: voorafgaand aan implementatie API                            
* **CodePackageControl**: code pakketten opnieuw te starten                             
* **RecoverPartition**: herstellen van een partitie                             
* **RecoverPartitions**: partities herstellen                             
* **RecoverServicePartitions**: servicepartities herstellen                             
* **RecoverSystemPartitions**: service systeempartities herstellen                             

### <a name="cluster-operations"></a>Bewerkingen voor een cluster
* **ProvisionFabric**: MSI en de clusternaambron manifest inrichten                             
* **UpgradeFabric**: beginnen cluster                             
* **UnprovisionFabric**: MSI en de clusternaambron manifest hierbij                         
* **MoveNextFabricUpgradeDomain**: upgrades van de cluster met een expliciete updatedomein hervatten                             
* **ReportFabricUpgradeHealth**: cluster-upgrades met de huidige upgradevoortgang Hallo hervatten                             
* **StartInfrastructureTask**: infrastructuurtaken starten                             
* **FinishInfrastructureTask**: infrastructuurtaken is voltooid                             
* **InvokeInfrastructureCommand**: infrastructuur-opdrachten voor het beheer van taak                              
* **ActivateNode**: activeren van een knooppunt                             
* **DeactivateNode**: deactiveren van een knooppunt                             
* **DeactivateNodesBatch**: meerdere knooppunten deactiveren                             
* **RemoveNodeDeactivations**: omzetten deactivering op meerdere knooppunten                             
* **GetNodeDeactivationStatus**: deactivering van de status controleren                             
* **NodeStateRemoved**: status van knooppunt reporting verwijderd                             
* **ReportFault**: fout met betrekking tot rapportage                             
* **FileContent**: image store client bestandsoverdracht (externe toocluster)                             
* **FileDownload**: image store client bestand downloaden Inleiding (externe toocluster)                             
* **InternalList**: image store bestand lijst clientbewerking (intern)                             
* **Verwijderen**: image store client delete-bewerking                              
* **Uploaden**: image store-clientbewerking uploaden                             
* **NodeControl**: starten, stoppen en opnieuw starten van de knooppunten                             
* **MoveReplicaControl**: het verplaatsen van replica's van één knooppunt tooanother                             

### <a name="miscellaneous-operations"></a>Verschillende bewerkingen
* **Ping**: client-pings                             
* **Query**: alle query's zijn toegestaan
* **NameExists**: naming URI bestaan controles                             

Hallo gebruiker toegang besturingselementtype is standaard beperkt toohello volgende bewerkingen: 

* **EnumerateSubnames**: naming URI opsomming                             
* **EnumerateProperties**: eigenschap opsomming naming                             
* **PropertyReadBatch**: eigenschap naming leesbewerkingen                             
* **GetServiceDescription**: long poll servicemeldingen en lezen service beschrijvingen                             
* **ResolveService**: compatibele gebaseerde service resolutie                             
* **ResolveNameOwner**: het omzetten van namen URI eigenaar                             
* **ResolvePartition**: het omzetten van systeemservices                             
* **ServiceNotifications**: servicemeldingen op basis van gebeurtenissen                             
* **GetUpgradeStatus**: polling upgradestatus van toepassing                             
* **GetFabricUpgradeStatus**: polling upgradestatus van cluster                             
* **InvokeInfrastructureQuery**: infrastructuurtaken opvragen                             
* **Lijst**: image store client bestandsbewerking lijst                             
* **ResetPartitionLoad**: opnieuw instellen van belasting van een failover-eenheid                             
* **ToggleVerboseServicePlacementHealthReporting**: schakelen uitgebreide plaatsing health servicerapportages                             

Hallo beheerder toegangsbeheer heeft ook toegang toohello voorafgaand aan activiteiten.

## <a name="changing-default-settings-for-client-roles"></a>Standaardinstellingen wijzigen voor client-functies
U kunt in Hallo cluster manifestbestand Beheerclient mogelijkheden toohello opgeven indien nodig. U kunt Hallo standaardinstellingen wijzigen door te gaan toohello **Fabric instellingen** optie tijdens [cluster maken](service-fabric-cluster-creation-via-portal.md), en het geven van de voorgaande instellingen in Hallo Hallo **naam**, **admin**, **gebruiker**, en **waarde** velden.

## <a name="next-steps"></a>Volgende stappen
[Beveiliging voor service Fabric-cluster](service-fabric-cluster-security.md)

[Service Fabric-cluster maken](service-fabric-cluster-creation-via-portal.md)

