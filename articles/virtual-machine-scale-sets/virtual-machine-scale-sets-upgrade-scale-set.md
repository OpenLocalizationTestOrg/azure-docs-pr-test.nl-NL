---
title: aaaUpgrade een virtuele machine van Azure-schaalset | Microsoft Docs
description: Een Azure virtuele-machineschaalset bijwerken
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Een virtuele-machineschaalset bijwerken
Dit artikel wordt beschreven hoe u een besturingssysteem update tooan Azure virtuele-machineschaalset instellen zonder uitvaltijd kunt implementeren. In deze context omvat een update OS Hallo versie of SKU Hallo OS wijzigen en het wijzigen van Hallo-URI van een aangepaste installatiekopie. Zonder uitvaltijd bijwerken van virtuele machines één op een tijdstip of in groepen (zoals een foutdomein op een tijdstip) in plaats van in één keer wordt bijgewerkt. Op deze manier kunnen alle virtuele machines die niet wordt bijgewerkt blijven uitvoeren.

tooavoid dubbelzinnigheid, gaan we onderscheid OS-update kunt u vier typen tooperform:

* Het wijzigen van Hallo versie of SKU van een platforminstallatiekopie. Bijvoorbeeld, het wijzigen van Ubuntu 14.04.2-LTS-versie uit 14.04.201506100 too14.04.201507060 of Hallo Ubuntu 15.10/laatste SKU too16.04.0-LTS/latest wijzigen. Dit scenario wordt beschreven in dit artikel.
* Het wijzigen van URI die nieuwe versie van een aangepaste installatiekopie die u hebt ontwikkeld tooa verwijst Hallo (**eigenschappen** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **installatiekopie** > **uri**). Dit scenario wordt beschreven in dit artikel.
* Verwijzing naar afbeelding van een scale-set die is gemaakt met Azure beheerd schijven Hallo wijzigen.
* Besturingssysteem van patchen Hallo binnen een virtuele machine (voorbeelden hiervan zijn een beveiligingspatch installeren en uitvoeren van Windows Update). Dit scenario wordt ondersteund, maar niet behandeld in dit artikel.

Virtuele-machineschaalsets die zijn geïmplementeerd als onderdeel van een [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster niet hier worden besproken. Zie [Patch Windows-besturingssysteem in uw Service Fabric-cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) voor meer informatie over Service Fabric-patching.

Hallo basic volgorde voor het wijzigen van Hallo OS-versie/SKU van een platforminstallatiekopie of Hallo-URI van een aangepaste installatiekopie ziet er als volgt:

1. Hallo virtuele machine scale set model worden opgehaald.
2. Hallo-versie, SKU, verwijzing naar afbeelding of de URI-waarde in Hallo model wijzigen.
3. Hallo model bijwerken.
4. Voer een *manualUpgrade* op Hallo virtuele machines in de schaalset Hallo aanroepen. Deze stap is alleen relevant als *upgradePolicy* te is ingesteld,**handmatige** in uw scale ingesteld. Als er te**automatische**, alle Hallo virtuele machines kunnen worden bijgewerkt in één keer dus uitvaltijd.

Met deze informatie in gedachten, gaan we kijken hoe u Hallo-versie van een schaal instellen in PowerShell en via Hallo REST-API kan bijwerken. Deze voorbeelden verrekend Hallo geval van een besturingssysteemkopie, maar in dit artikel biedt voldoende informatie voor u tooadapt dit proces tooa aangepaste installatiekopie.

## <a name="powershell"></a>PowerShell
In dit voorbeeld bijgewerkt in een Windows virtuele-machineschaalset (maken toohello nieuwe versie 4.0.20160229. Na het bijwerken van Hallo model, wordt een update-exemplaar voor een virtuele machine op een tijdstip.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Als u Hallo URI voor een aangepaste installatiekopie in plaats van een platform-versie van de afbeelding wijzigen bijwerkt, vervangt u 'set Hallo nieuwe versie' hello regel met een opdracht die wordt bijgewerkt Hallo broninstallatiekopie URI. Bijvoorbeeld, als Hallo scale set is gemaakt zonder gebruik van beheerde Azure-schijven, eruit Hallo update als volgt:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Als een aangepaste installatiekopie gebaseerd schaalset is gemaakt met Azure beheerd schijven, en vervolgens de verwijzing naar afbeelding van Hallo zou worden bijgewerkt. Bijvoorbeeld:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Hallo REST-API
Hier volgen enkele voorbeelden van Python die hello Azure REST-API tooroll uit een update OS-versie gebruiken. Hallo lightweight maken beide gebruik [azurerm](https://pypi.python.org/pypi/azurerm) bibliotheek met REST API van Azure wrapper functies toodo GET op Hallo schaal model, gevolgd door een PUT met een bijgewerkte model instelt. Ze ook zoeken op de virtuele machine-exemplaren weergaven tooidentify Hallo virtuele machines per updatedomein.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) is een pythonscript dat is gebruikt tooroll uit een OS upgrade tooa met virtuele-machineschaalset één updatedomein tegelijk worden ingesteld.

![Vmssupgrade script voor het kiezen van virtuele machines of een updatedomein](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Dit script kunt u specifieke virtuele machines tooupdate kiezen of geef een updatedomein. Het ondersteunt wijzigen van een platform-versie van de installatiekopie en het Hallo-URI van een aangepaste installatiekopie wijzigen.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is een algemene editor voor de virtuele-machineschaalsets waarin de virtuele machine de status als een heatmap waarbij één rij één updatedomein vertegenwoordigt. U kunt onder andere Hallo-model voor een schaalset bijwerken met een nieuwe versie, SKU of aangepaste installatiekopie URI en selecteer vervolgens een fout met betrekking tot domeinen tooupgrade. Wanneer u doet dit, worden alle Hallo virtuele machines in dat updatedomein bijgewerkte toohello nieuw model. U kunt ook een uitrollende upgrade op basis van de batchgrootte Hallo van uw keuze doen.  

Hallo volgende schermafbeelding ziet u een model van een schaal voor Ubuntu 14.04-2LTS versie 14.04.201507060 instelt. Veel meer opties zijn toegevoegd toothis hulpprogramma sinds deze schermafbeelding is gemaakt.

![Model van een schaal ingesteld voor Ubuntu 14.04-2LTS Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Nadat u op **Upgrade** en vervolgens **Details ophalen**, virtuele machines in UD 0 tooupdate gestart.

![Vmsseditor tonen worden bijgewerkt](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

