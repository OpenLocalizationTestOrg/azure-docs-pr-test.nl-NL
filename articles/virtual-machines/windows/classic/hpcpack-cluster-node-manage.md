---
title: rekenknooppunten aaaManage HPC Pack cluster | Microsoft Docs
description: Meer informatie over PowerShell-script extra tooadd, verwijderen, starten en stoppen van HPC Pack 2012 R2-cluster-rekenknooppunten in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Hallo aantal en de beschikbaarheid van rekenknooppunten in een cluster HPC Pack in Azure beheren
Als u een HPC Pack 2012 R2-cluster in Azure VM's hebt gemaakt, kunt u manieren tooeasily toevoegen, verwijderen, (ingericht) starten of stoppen (deprovision) sommige compute knooppunt VM's in het cluster. toodo deze taken uitvoeren Azure PowerShell-scripts die zijn geïnstalleerd op Hallo hoofdknooppunt VM. Deze scripts met help u Hallo aantal en de beschikbaarheid van uw cluster HPC Pack resources beheren zodat u de kosten kunt bepalen.

> [!IMPORTANT] 
> Dit artikel geldt alleen tooHPC Pack 2012 R2 clusters in Azure gemaakt met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.
> Hallo PowerShell-scripts die worden beschreven in dit artikel zijn niet beschikbaar in HPC Pack 2016.

## <a name="prerequisites"></a>Vereisten
* **HPC Pack 2012 R2-cluster in Azure VM's**: een HPC Pack 2012 R2-cluster maken in het klassieke implementatiemodel Hallo. U kunt bijvoorbeeld Hallo-implementatie automatiseren met behulp van Hallo HPC Pack 2012 R2 VM-installatiekopie in Azure Marketplace Hallo en een Azure PowerShell-script. Zie voor informatie en vereisten [een HPC-Cluster maken met Hallo HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md).
  
    Na de implementatie Hallo zoeken knooppunt management scripts in Hallo % CCP\_HOME % bin-map op Hallo hoofdknooppunt. Elk Hallo scripts worden uitgevoerd als een beheerder.
* **Azure publish certificaat voor het bestand of het beheer van instellingen**: U moet toodo een van de volgende Hallo Hallo hoofdknooppunt van:
  
  * **Importeren hello Azure bestand publicatie-instellingen**. toodo deze, voer hello Azure PowerShell-cmdlets volgen op Hallo hoofdknooppunt:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Hello Azure-beheercertificaat configureren op het hoofdknooppunt Hallo**. Als u Hallo cer-bestand hebt, importeer het in het certificaatarchief van Hallo CurrentUser\My en voer vervolgens hello Azure PowerShell-cmdlet voor uw Azure-omgeving (AzureCloud of AzureChinaCloud) te volgen:
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Rekenknooppunt virtuele machines toevoegen
Toevoegen van rekenknooppunten Hello **toevoegen HpcIaaSNode.ps1** script.

### <a name="syntax"></a>Syntaxis
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>Parameters
* **ServiceName**: naam van de cloudservice Hallo die nieuwe berekening knooppunt virtuele machines worden toegevoegd aan.
* **ImageName**: Azure VM-installatiekopienaam, die kan worden verkregen via de klassieke Azure-portal Hallo of Azure PowerShell-cmdlet **Get-AzureVMImage**. Hallo installatiekopie moet voldoen aan Hallo volgens de vereisten:
  
  1. Een Windows-besturingssysteem moet worden geïnstalleerd.
  2. HPC Pack moet worden geïnstalleerd in de berekeningsfunctie knooppunt Hallo.
  3. Hallo afbeelding moet een persoonlijke installatiekopie in gebruikerscategorie hello, niet een openbare Azure VM-installatiekopie.
* **Aantal**: aantal compute knooppunt VMs toobe toegevoegd.
* **InstanceSize**: grootte van Hallo compute knooppunt virtuele machines.
* **DomainUserName**: domeingebruikersnaam, dat wil gebruikte toojoin Hallo nieuwe virtuele machines toohello domein zeggen.
* **DomainUserPassword**: wachtwoord van de domeingebruiker Hallo.
* **NodeNameSeries** (optioneel): patroon naamgeving voor Hallo rekenknooppunten. Hallo-indeling moet &lt; *hoofdmap\_naam*&gt;&lt;*Start\_getal*&gt;%. Bijvoorbeeld, compute MyCN % 10%: een reeks Hallo knooppuntnamen vanaf MyCN11. Als niet wordt opgegeven, Hallo script gebruikt Hallo knooppunt naming reeks geconfigureerd in Hallo HPC-cluster.

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld wordt 20 grootte grote rekenknooppunt virtuele machines in de cloudservice hello *hpcservice1*, op basis van de VM-installatiekopie Hallo *hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Rekenknooppunt virtuele machines verwijderen
Verwijderen van rekenknooppunten Hello **verwijderen HpcIaaSNode.ps1** script.

### <a name="syntax"></a>Syntaxis
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>Parameters
* **Naam**: namen van de cluster knooppunten toobe verwijderd. Jokertekens worden ondersteund. Hallo-parameternaam set is. U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.
* **Knooppunt**: Hallo HpcNode object voor Hallo knooppunten toobe verwijderd, die kan worden verkregen via Hallo HPC PowerShell-cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). naam van de parameter Hallo is knooppunt. U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.
* **DeleteVHD** (optioneel): instelling toodelete Hallo gekoppeld schijven voor Hallo virtuele machines die zijn verwijderd.
* **Force** (optioneel): tooforce offline HPC-knooppunten instellen voordat u ze verwijdert.
* **Bevestig** (optioneel): vragen om bevestiging voordat het Hallo-opdracht wordt uitgevoerd.
* **WhatIf**: toodescribe instellen wat er zou gebeuren als u Hallo-opdracht uitvoert, zonder het Hallo-opdracht daadwerkelijk wordt uitgevoerd.

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld zorgt ervoor dat offline Hallo knooppunten met namen die beginnen *HPCNode-CN -* en ze Hallo knooppunten en hun bijbehorende schijven worden verwijderd.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Rekenknooppunt virtuele machines starten
Start de rekenknooppunten Hello **Start HpcIaaSNode.ps1** script.

### <a name="syntax"></a>Syntaxis
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>Parameters
* **Naam**: namen van Hallo cluster knooppunten toobe gestart. Jokertekens worden ondersteund. Hallo-parameternaam set is. U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.
* **Knooppunt**-Hallo HpcNode object voor Hallo knooppunten toobe gestart, die kan worden verkregen via Hallo HPC PowerShell-cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). naam van de parameter Hallo is knooppunt. U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld begint knooppunten met namen die beginnen *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Rekenknooppunt virtuele machines stoppen
Stoppen van rekenknooppunten Hello **Stop HpcIaaSNode.ps1** script.

### <a name="syntax"></a>Syntaxis
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>Parameters
* **Naam**-namen van Hallo cluster knooppunten toobe gestopt. Jokertekens worden ondersteund. Hallo-parameternaam set is. U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.
* **Knooppunt**: Hallo HpcNode object voor Hallo knooppunten toobe is gestopt, die kan worden verkregen via Hallo HPC PowerShell-cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). naam van de parameter Hallo is knooppunt. U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.
* **Force** (optioneel): tooforce offline HPC-knooppunten instellen voordat u ze stopt.

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld zorgt ervoor dat offline knooppunten met namen die beginnen *HPCNode-CN -* en vervolgens stopt Hallo knooppunten.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Volgende stappen
* tooautomatically vergroten of verkleinen van de clusterknooppunten Hallo volgens de huidige werkbelasting Hallo van jobs en taken op Hallo cluster, Zie [automatisch vergroten of verkleinen Hallo HPC Pack clusterbronnen in Azure volgens toohello clusterbelasting](hpcpack-cluster-node-autogrowshrink.md).

