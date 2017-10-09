---
title: aaaConfigure hello upgrade van een Service Fabric-toepassing | Microsoft Docs
description: Meer informatie over hoe tooconfigure instellingen Hallo voor het upgraden van een Service Fabric-toepassing met behulp van Microsoft Visual Studio.
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Hallo-upgrade van een Service Fabric-toepassing in Visual Studio configureren
Visual Studio tools voor Azure Service Fabric bieden upgrade ondersteuning voor het publiceren van toolocal of externe clusters. Er zijn drie scenario's waarin u tooupgrade uw toepassing tooa nieuwere versie in plaats van de vervangen toepassing hello wilt tijdens het testen en foutopsporing:

* Toepassingsgegevens niet verloren gaan tijdens het Hallo-upgrade.
* Beschikbaarheid blijft hoge zodat er niet serviceonderbreking tijdens de upgrade hello, als er dat voldoende service-exemplaren verspreid over upgradedomeinen.
* Tests kunnen worden uitgevoerd op basis van een toepassing, terwijl deze wordt bijgewerkt.

## <a name="parameters-needed-tooupgrade"></a>Parameters nodig tooupgrade
U kunt kiezen uit twee soorten implementatie: reguliere of de upgrade. Een gewone implementatie worden gewist alle vorige implementatie-informatie en gegevens op het Hallo-cluster, terwijl een upgrade-implementatie behouden deze blijft. Wanneer u een Service Fabric-toepassing in Visual Studio bijwerkt, moet u de upgrade toepassingsparameters tooprovide en statusbeleid voor controle. Upgrade van de toepassing parameters te regelen Hallo upgrade terwijl controle statusbeleid bepalen of Hallo-upgrade is geslaagd. Zie [upgrade van de Service Fabric-toepassing: upgrade parameters](service-fabric-application-upgrade-parameters.md) voor meer informatie.

Er zijn drie upgrade modi: *bewaakte*, *UnmonitoredAuto*, en *UnmonitoredManual*.

* De upgrade van een bewaakte automatiseert het Hallo-upgrade en toepassing statuscontrole.
* Een upgrade UnmonitoredAuto automatiseert het Hallo-upgrade, maar slaat het Hallo statuscontrole van de toepassing.
* Wanneer u een upgrade UnmonitoredManual doet, moet u toomanually elk upgradedomein upgraden.

Elke upgrademodus vereist verschillende sets van parameters. Zie [parameters voor het bijwerken van toepassing](service-fabric-application-upgrade-parameters.md) toolearn meer informatie over de beschikbare upgradeopties Hallo.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Upgrade van een Service Fabric-toepassing in Visual Studio
Als u Hallo Visual Studio Service Fabric extra tooupgrade Service Fabric-toepassing, kunt u een proces publiceren toobe opgeven van een upgrade in plaats van een normale implementatie door te controleren Hallo **upgrade uitvoert voor de toepassing hello** controleren vak.

### <a name="tooconfigure-hello-upgrade-parameters"></a>upgrade tooconfigure Hallo-parameters
1. Klik op Hallo **instellingen** knop volgende toohello selectievakje. Hallo **Upgrade Parameters bewerken** dialoogvenster wordt weergegeven. Hallo **Upgrade Parameters bewerken** in het dialoogvenster ondersteunt Hallo bewaakte UnmonitoredAuto en UnmonitoredManual upgrade modi.
2. Selecteer de upgrademodus Hallo dat u toouse wilt en vult u Hallo parameter raster.

    Elke parameter heeft standaardwaarden. optionele parameter Hallo *DefaultServiceTypeHealthPolicy* een hash-tabel invoer. Hier volgt een voorbeeld van Hallo hash-tabel invoerindeling voor *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *Servicetypehealthpolicymap; deze* is een andere optionele parameter waarmee een hash-Tabelinvoer in Hallo de volgende indeling:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Hier volgt een voorbeeld van de praktijk:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. Als u de upgrademodus UnmonitoredManual selecteert, moet u handmatig starten van een PowerShell-console toocontinue en klaar bent met het upgradeproces Hallo. Raadpleeg te[upgrade van de Service Fabric-toepassing: geavanceerde onderwerpen](service-fabric-application-upgrade-advanced.md) toolearn hoe handmatige upgrade werkt.

## <a name="upgrade-an-application-by-using-powershell"></a>Upgrade van een toepassing met behulp van PowerShell
U kunt de PowerShell-cmdlets tooupgrade Service Fabric-toepassing. Zie [upgrade zelfstudie over Service Fabric](service-fabric-application-upgrade-tutorial.md) en [Start ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) voor gedetailleerde informatie.

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Geef een selectievakje statusbeleid in het manifestbestand van de toepassing hello
Elke service in een Service Fabric-toepassing kan een eigen parameters voor het beleid van health dat voorrang boven de standaardwaarden Hallo hebben. U kunt deze parameterwaarden in het manifestbestand van de toepassing hello opgeven.

Hallo volgende voorbeeld ziet u hoe een unieke health tooapply beleid voor elke service in het toepassingsmanifest Hallo controleren.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het implementeren van een toepassing [implementeren van een bestaande toepassing in Azure Service Fabric](service-fabric-deploy-existing-app.md).