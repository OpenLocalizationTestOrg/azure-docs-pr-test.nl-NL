---
title: aaaInstall Symantec Endpoint Protection op een Windows-virtuele machine in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en Hallo Symantec Endpoint Protection security-uitbreiding configureren op een nieuwe of bestaande virtuele machine in Azure gemaakt met de Hallo klassieke implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Hoe tooinstall en Symantec Endpoint Protection configureren op een virtuele machine van Windows
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Dit artikel ziet u hoe tooinstall en Hallo Symantec Endpoint Protection-client configureren op een bestaande virtuele machine (VM) met Windows Server. Deze volledige client omvat services zoals virussen en bescherming tegen spyware, firewall en inbraakdetectie te voorkomen. Hallo-client is geïnstalleerd als een uitbreiding van de beveiliging met behulp van Hallo VM-Agent.

Als u een bestaand abonnement van Symantec voor een on-premises oplossing hebt, kunt u deze tooprotect uw virtuele machines in Azure. Als u niet een klant nog, kunt u zich aanmelden voor een proefabonnement. Zie voor meer informatie over deze oplossing [Symantec Endpoint Protection op van Microsoft Azure-platform][Symantec]. Deze pagina bevat ook koppelingen toolicensing informatie en instructies voor het installeren van Hallo client als u al een Symantec-klant bent.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Symantec Endpoint Protection installeren op een bestaande virtuele machine
Voordat u begint, moet u de volgende Hallo:

* Hello Azure PowerShell-module, versie 0.8.2 of hoger op de computer. U kunt controleren Hallo-versie van Azure PowerShell die u hebt geïnstalleerd met Hallo **Get-Module azure | tabel opmaken versie** opdracht. Zie voor instructies en een koppeling toohello meest recente versie [hoe tooInstall en configureer Azure PowerShell][PS]. Meld u aan tooyour Azure-abonnement met `Add-AzureAccount`.
* Hallo VM-Agent uitgevoerd op Hallo Azure virtuele Machine.

Controleer eerst of deze VM-Agent is al geïnstalleerd op de virtuele machine van Hallo Hallo. Vult Hallo cloudservicenaam en de naam van de virtuele machine en voer de volgende opdrachten bij een beheerdersniveau Azure PowerShell-opdrachtprompt Hallo. Vervang alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens.

> [!TIP]
> Als u niet Hallo-cloudservice en de namen van de virtuele machine weet, voert u **Get-AzureVM** toolist Hallo namen voor alle virtuele machines in uw huidige abonnement.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Als hello **write-host** opdracht geeft **True**, Hallo VM-Agent is geïnstalleerd. Als deze wordt weergegeven in **False**, Zie Hallo-instructies en een koppeling toohello downloaden in hello Azure blogbericht [VM-Agent en -extensies: Part 2][Agent].

Als Hallo VM-Agent is geïnstalleerd, voert u deze opdrachten tooinstall Hallo Symantec Endpoint Protection-agent.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify die Hallo Symantec security-uitbreiding is geïnstalleerd en is bijgewerkt:

1. Meld u aan toohello virtuele machine. Zie voor instructies [hoe tooLog op virtuele Machine Running Windows Server tooa][Logon].
2. Voor Windows Server 2008 R2, klikt u op **Start > Symantec Endpoint Protection**. Typ voor Windows Server 2012 of Windows Server 2012 R2, vanuit het startscherm hello, **Symantec**, en klik vervolgens op **Symantec Endpoint Protection**.
3. Van Hallo **Status** tabblad Hallo **Status Symantec Endpoint Protection** venster updates toepassen of opnieuw opstarten indien nodig.

## <a name="additional-resources"></a>Aanvullende bronnen
[Hoe tooLog op tooa Virtual Machine Running Windows Server][Logon]

[Azure VM-extensies en functies][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
