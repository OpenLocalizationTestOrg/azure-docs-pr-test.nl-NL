---
title: Overzicht van virtuele machines Agent aaaAzure | Microsoft Docs
description: Overzicht van de virtuele Machine van Azure-Agent
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Overzicht van Azure VM-Agent

Hallo Microsoft Azure-Agent voor virtuele Machine (VM-Agent) is een beveiligde, lichtgewicht proces die VM interactie met hello Azure-Infrastructuurcontroller beheert. Hallo VM-Agent heeft een primaire rol als inschakelen en het uitvoeren van de virtuele machine van Azure-extensies. VM-extensies inschakelen na de implementatieconfiguratie van virtuele machines, zoals het installeren en configureren van software. Uitbreidingen van de virtuele machine ook inschakelen herstelfuncties zoals het opnieuw instellen van Hallo beheerderswachtwoord van een virtuele machine. Zonder hello Azure VM-Agent, de uitbreidingen van de virtuele machine kunnen niet worden uitgevoerd.

In dit document worden de installatie, detectie en verwijdering van hello Azure VM-Agent.

## <a name="install-hello-vm-agent"></a>Hallo VM-Agent installeren

### <a name="azure-gallery-image"></a>Afbeelding van de Azure-galerie

Hello Azure VM-Agent wordt standaard geïnstalleerd op een Windows-virtuele machine op basis van een installatiekopie van een Azure-galerie geïmplementeerd. Bij het implementeren van een installatiekopie van een Azure-galerie van Hallo Portal, PowerShell, opdrachtregelinterface of een Azure Resource Manager-sjabloon worden hello die Azure VM-Agent ook is geïnstalleerd. 

### <a name="manual-installation"></a>Handmatige installatie

Hallo Windows VM-agent kan handmatig worden geïnstalleerd met behulp van een Windows installer-pakket. Handmatige installatie kan nodig zijn bij het maken van de installatiekopie van een aangepaste virtuele machine die wordt geïmplementeerd in Azure. toomanually installatie Hallo Windows VM-Agent, Hallo VM-Agent-installatieprogramma downloaden vanaf deze locatie [Windows Azure VM-Agent downloaden](http://go.microsoft.com/fwlink/?LinkID=394789). 

Hallo VM-Agent kan worden geïnstalleerd door te dubbelklikken op Hallo windows installer-bestand. Voor een automatisch of zonder toezicht-installatie van de VM-agent Hallo Hallo volgende opdracht worden uitgevoerd.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Hallo VM-Agent detecteren

### <a name="powershell"></a>PowerShell

Hello Azure Resource Manager PowerShell-module kan worden gebruikt tooretrieve informatie over Azure Virtual Machines. Met `Get-AzureRmVM` retourneert behoorlijk een stukje informatie, met inbegrip van Hallo Inrichtingsstatus voor hello Azure VM-Agent.

```PowerShell
Get-AzureRmVM
```

Hallo volgende is slechts een subset van Hallo `Get-AzureRmVM` uitvoer. Kennisgeving Hallo `ProvisionVMAgent` eigenschap genest in `OSProfile`, is deze eigenschap de gebruikte toodetermine als Hallo VM-agent toohello geïmplementeerde virtuele machine is.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Hallo na script kan worden gebruikt tooreturn een beknopte lijst met namen van de virtuele machine en status Hallo Hallo VM-Agent.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Handmatige detectie

Als Windows Azure VM tooa aangemeld, worden Taakbeheer gebruikte tooexamine actieve processen. toocheck voor hello Azure VM-Agent, opent u Taakbeheer > Hallo tabblad met details op en zoek naar een procesnaam `WindowsAzureGuestAgent.exe`. Hallo aanwezigheid van dit proces geeft dat die Hallo VM-agent is geïnstalleerd.

## <a name="upgrade-hello-vm-agent"></a>Hallo VM-Agent bijwerken

Hello Azure VM-Agent voor Windows, wordt automatisch bijgewerkt. Als u nieuwe virtuele machines zijn geïmplementeerd tooAzure, krijgen ze Hallo nieuwste VM-agent. Aangepaste installatiekopieën voor virtuele machine moet de handmatig bijgewerkte tooinclude Hallo nieuwe VM-agent.
