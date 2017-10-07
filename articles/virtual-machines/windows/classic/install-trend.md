---
title: aaaInstall Trend Micro grondige Security op een virtuele machine | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooinstall en Trend Micro beveiliging configureren op een virtuele machine gemaakt met de Hallo klassieke implementatiemodel in Azure.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Hoe tooinstall en Trend Micro grondige Security configureren als een Service op een virtuele machine van Windows
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Dit artikel ziet u hoe tooinstall en Trend Micro grondige Security configureren als een Service op een nieuwe of bestaande virtuele machine (VM) met Windows Server. Uitgebreide beveiliging als een Service omvat anti-malwarebeveiliging, een firewall, een inbraakdetectie preventie van systeem en integriteit bewaken.

Hallo-client is geïnstalleerd als een uitbreiding van beveiliging via Hallo VM-Agent. Installeer op een nieuwe virtuele machine Hallo grondige beveiligingsagent, als Hallo die VM-Agent automatisch door hello Azure-portal gemaakt wordt.

Een bestaande virtuele machine gemaakt met de klassieke portal hello, hello Azure CLI of PowerShell hebben mogelijk niet een VM-agent. Voor een bestaande virtuele machine die geen Hallo VM-Agent moet toodownload en eerst installeren. In dit artikel komen beide situaties.

Als u een abonnement van de Trend Micro voor een on-premises oplossing hebt, kunt u deze toohelp beveiligen van uw virtuele machines in Azure. Als u niet een klant nog, kunt u zich aanmelden voor een proefabonnement. Zie voor meer informatie over deze oplossing Hallo Trend Micro blogbericht [Microsoft Azure VM-Agent-extensie voor grondige Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Hallo grondige beveiligingsagent installeren op een nieuwe virtuele machine

Hallo [Azure-portal](http://portal.azure.com) kunt u Hallo Trend Micro beveiliging uitbreiding installeren wanneer u een installatiekopie van Hallo **Marketplace** toocreate Hallo virtuele machine. Als u één virtuele machine maakt, is met behulp van Hallo portal een eenvoudige manier tooadd bescherming van Trend Micro.

Met behulp van een item in Hallo **Marketplace** een wizard waarmee u kunt Hallo virtuele machine instellen wordt geopend. Gebruik van Hallo **instellingen** blade, Hallo derde venster van Hallo wizard tooinstall Hallo Trend Micro beveiliging extensie.  Raadpleeg voor algemene instructies [maken van een virtuele machine met Windows in hello Azure-portal](tutorial.md).

Als u krijgt toohello **instellingen** blade van de wizard Hallo Hallo volgende stappen:

1. Klik op **extensies**, klikt u vervolgens op **-extensie toevoegen** in Hallo Volgend deelvenster.

   ![Beginnen met het Hallo-extensie toevoegen][1]

2. Selecteer **grondige beveiligingsagent** in Hallo **nieuwe resource** deelvenster. Klik in deelvenster grondige beveiligingsagent Hallo op **maken**.

   ![Grondige beveiligingsagent identificeren][2]

3. Voer Hallo **Tenant-id** en **Tenant activering wachtwoord** voor Hallo-extensie. Desgewenst kunt u een **beveiliging beleids-id**. Klik vervolgens op **OK** tooadd Hallo-client.

   ![Geef details op extensie][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Hallo grondige beveiligingsagent installeren op een bestaande virtuele machine
tooinstall Hallo-agent op een bestaande virtuele machine, moet u Hallo volgende items:

* Hello Azure PowerShell-module, versie 0.8.2 of nieuwer, is geïnstalleerd op uw lokale computer. U kunt controleren Hallo-versie van Azure PowerShell die u hebt geïnstalleerd met behulp van Hallo **Get-Module azure | tabel opmaken versie** opdracht. Zie voor instructies en een koppeling toohello meest recente versie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Meld u aan tooyour Azure-abonnement met `Add-AzureAccount`.
* VM-Agent is geïnstalleerd op de virtuele doelmachine Hallo Hallo.

Controleer eerst of deze Hallo die VM-Agent is al geïnstalleerd. Vult Hallo cloudservicenaam en de naam van de virtuele machine en voer de volgende opdrachten bij een beheerdersniveau Azure PowerShell-opdrachtprompt Hallo. Vervang alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Als u niet Hallo-cloudservice en de naam van virtuele machine weet, voert u **Get-AzureVM** toodisplay dat gegevens voor alle virtuele machines in uw huidige abonnement Hallo.

Als hello **write-host** opdracht retourneert **True**, Hallo VM-Agent is geïnstalleerd. Als het resultaat **False**, Zie Hallo-instructies en een koppeling toohello downloaden in hello Azure blogbericht [VM-Agent en -extensies: Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Als Hallo VM-Agent is geïnstalleerd, moet u deze opdrachten uitvoeren.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Volgende stappen
Het duurt enkele minuten duren voordat Hallo agent toostart uitgevoerd wanneer deze is geïnstalleerd. Daarna moet u tooactivate grondige beveiliging op Hallo virtuele machine zodat deze kan worden beheerd door een grondige Security Manager. Zie Hallo artikelen voor aanvullende instructies te volgen:

* Trend van artikel over deze oplossing [Instant-On Cloud Security voor Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* Een [Windows PowerShell-voorbeeldscript](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure Hallo virtuele machine
* [Instructies](http://go.microsoft.com/fwlink/?LinkId=404099) voor Hallo-voorbeeld

## <a name="additional-resources"></a>Aanvullende bronnen
[Hoe toolog op tooa virtuele machine met Windows Server]

[Azure VM-extensies en functies]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Hoe toolog op tooa virtuele machine met Windows Server]:connect-logon.md
[Azure VM-extensies en functies]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
