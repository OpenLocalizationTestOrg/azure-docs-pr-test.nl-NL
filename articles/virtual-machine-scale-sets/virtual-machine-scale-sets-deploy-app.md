---
title: Implementeren van een app op de virtuele-machineschaalsets
description: Uitbreidingen voor depoy een app op Azure Virtual Machine-Schaalsets gebruiken.
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Implementeren van uw toepassing op virtuele-machineschaalsets

In dit artikel beschrijft de verschillende manieren voor het installeren van software op het moment dat de schaalaanpassingsset is ingericht.

U wilt controleren de [Scale ingesteld ontwerp overzicht](virtual-machine-scale-sets-design-overview.md) artikel worden enkele van de grenzen die zijn opgelegd door de virtuele-machineschaalsets beschreven.

## <a name="capture-and-reuse-an-image"></a>Vastleggen en een installatiekopie van het opnieuw gebruiken

U kunt een virtuele machine die in Azure om de installatiekopie van een base voorbereiden voor de schaal is ingesteld. Dit proces maakt een beheerde schijf in uw opslagaccount die u kunt verwijzen naar als de basisinstallatiekopie voor uw scale set. 

Voer de volgende stappen uit:

1. Een virtuele Machine van Azure maken
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. Afstand verbinding met de virtuele machine en het systeem naar wens aanpassen.

   Als u wilt, kunt u nu uw toepassing kunt installeren. Weet dat wel door uw toepassing nu te installeren, mag u uw toepassing meer gecompliceerde upgraden omdat u wellicht eerst verwijderen. In plaats daarvan kunt u deze stap voor het installeren van alle vereisten die uw toepassing mogelijk nodig hebt, zoals een bepaalde functie van de runtime- of -besturingssysteem.

3. Volg de zelfstudie 'machine vastleggen' voor [Linux] [ linux-vm-capture] of [Windows][windows-vm-capture].

4. Maak een [virtuele-Machineschaalset] [ vmss-create] met de installatiekopie van URI die u hebt vastgelegd in de vorige stap.

Zie voor meer informatie over schijven [schijven overzicht beheerde](../virtual-machines/windows/managed-disks-overview.md) en [gegevensschijven gekoppeld gebruik](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-the-scale-set-is-provisioned"></a>Wanneer de schaalaanpassingsset is ingericht installeren

Uitbreidingen van de virtuele machine kunnen worden toegepast op een virtuele-machineschaalset. U kunt de virtuele machines in een schaal ingesteld als een hele groep aanpassen met de extensie van virtuele machine. Zie voor meer informatie over uitbreidingen [uitbreidingen van de virtuele Machine](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Er zijn drie belangrijkste uitbreidingen die kunt u, als afhankelijk van het besturingssysteem is op basis van Linux of op basis van Windows.

### <a name="windows"></a>Windows

Voor een besturingssysteem op basis van Windows, gebruiken de **aangepast Script v1.8** extensie, of de **PowerShell DSC** extensie.

#### <a name="custom-script"></a>Aangepast Script

De aangepaste scriptextensie wordt een script uitgevoerd op elk exemplaar van de virtuele machine in de schaalset. Een configuratiebestand of variabele geeft aan welke bestanden zijn gedownload naar de virtuele machine en vervolgens welke opdracht wordt uitgevoerd. U kunt dit bijvoorbeeld een installatieprogramma, een script, een batch-bestand, uitvoerbare bestanden uitvoeren.

Een hashtabel PowerShell gebruikt om de instellingen. In dit voorbeeld configureert u de extensie voor aangepaste scripts voor het uitvoeren van een PowerShell-script waarop IIS wordt geïnstalleerd.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Gebruik de `-ProtectedSetting` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

---------


Azure CLI maakt gebruik van een json-bestand voor de instellingen. In dit voorbeeld configureert u de extensie voor aangepaste scripts voor het uitvoeren van een PowerShell-script waarop IIS wordt geïnstalleerd. Sla het volgende json-bestand als _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Voer deze opdracht Azure CLI.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Gebruik de `--protected-settings` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

### <a name="powershell-dsc"></a>PowerShell DSC

U kunt de PowerShell DSC gebruiken om aan te passen scale set vm-exemplaren. De **DSC** extensie gepubliceerd door **Microsoft.Powershell** implementeert en de opgegeven DSC-configuratie op elk exemplaar van de virtuele machine wordt uitgevoerd. Een configuratiebestand of variabele vertelt u de extensie waar *.zip* pakket is, en welke _script functie_ combinatie om uit te voeren.

Een hashtabel PowerShell gebruikt om de instellingen. In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Gebruik de `-ProtectedSetting` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

-----------

Azure CLI maakt gebruik van een json voor de instellingen. In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd. Sla het volgende json-bestand als _settings.json_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

Voer deze opdracht Azure CLI.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Gebruik de `--protected-settings` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

### <a name="linux"></a>Linux

Linux kunt beide gebruiken de **aangepast Script v2.0** -extensie of gebruik **cloud init** tijdens het maken van.

Aangepast script is een eenvoudige uitbreiding die u downloadt bestanden naar de virtuele machine-exemplaren en een opdracht wordt uitgevoerd.

#### <a name="custom-script"></a>Aangepast Script

Sla het volgende json-bestand als _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

De Azure CLI gebruiken deze extensie toevoegen aan een bestaande virtuele-machineschaalset. Elke virtuele machine in de schaal automatisch ingesteld wordt uitgevoerd voor de uitbreiding.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Gebruik de `--protected-settings` overschakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

#### <a name="cloud-init"></a>Cloud-Init

Cloud-Init wordt gebruikt wanneer de schaalset gemaakt. Maak eerst een lokaal bestand met de naam _cloud init.txt_ en voeg uw configuratie toe. Zie bijvoorbeeld [deze basisvertalingen](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

De Azure CLI gebruiken voor het maken van een schaalset. De `--custom-data` veld accepteert de bestandsnaam van een cloud-init-script.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Hoe beheer ik toepassingsupdates?

Als u uw toepassing via een uitbreiding hebt geïmplementeerd, wijzigt u de definitie van de extensie in een bepaalde manier. Deze wijziging zorgt ervoor dat de extensie moet worden geïmplementeerd op alle exemplaren van de virtuele machine. Iets **moet** Azure biedt niet kunnen zien dat de extensie is gewijzigd over de extensie in, zoals de naam van een bestand waarnaar wordt verwezen, anders worden gewijzigd.

Als u standaard de toepassing in uw eigen installatiekopie uitbreidbaar, gebruikt u een pijplijn geautomatiseerde implementatie updates van toepassingen. Ontwerp uw architectuur ter bevordering van de snelle wisselen van een gefaseerde schaal instelt in productie. Een goed voorbeeld van deze benadering is de [Azure Spinnaker stuurprogramma werk](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Verpakker](https://www.packer.io/) en [Terraform](https://www.terraform.io/) ondersteuning voor Azure Resource Manager, zodat u kunt ook uw installatiekopieën 'als de code' definiëren en ze te ontwikkelen in Azure, gebruik vervolgens de VHD in de schaalset. Hierdoor zou dus worden echter problematisch voor installatiekopieën van marketplace, waarbij extensies/aangepaste scripts belangrijker omdat u geen bits van marketplace rechtstreeks bewerken.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Wat gebeurt er wanneer een kan worden geschaald schaalset uit?
Wanneer u een of meer virtuele machines aan een schaalset toevoegt, wordt de toepassing wordt automatisch geïnstalleerd. Voor het voorbeeld als de schaal ingesteld uitbreidingen die zijn gedefinieerd, ze worden uitgevoerd op een nieuwe virtuele machine telkens wanneer die deze is gemaakt. Als de scale-set is gebaseerd op een aangepaste installatiekopie, is een nieuwe virtuele machine een kopie van de aangepaste installatiekopie van de bron. Als de scale set virtuele machines container hosts zijn, hebt u mogelijk starten van de code voor het laden van de containers in een extensie voor aangepaste scripts. Of een uitbreiding van een agent die wordt geregistreerd bij de orchestrator van een cluster, zoals Azure Container Service kunt installeren.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Hoe implementatie een OS-update in update domeinen?
Stel dat u wilt uw installatiekopie van het besturingssysteem bijwerken terwijl de virtuele-machineschaalset ingesteld uitgevoerd. PowerShell en Azure CLI kunt installatiekopieën van virtuele machines, één virtuele machine tegelijk bijwerken. De [upgraden van een virtuele-Machineschaalset](./virtual-machine-scale-sets-upgrade-scale-set.md) artikel bevat ook verdere informatie over welke opties beschikbaar zijn voor een upgrade uitvoert op een virtuele-machineschaalset.

## <a name="next-steps"></a>Volgende stappen

* [Gebruik PowerShell voor het beheren van uw scale ingesteld.](virtual-machine-scale-sets-windows-manage.md)
* [Maak een sjabloon van de set schaal.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

