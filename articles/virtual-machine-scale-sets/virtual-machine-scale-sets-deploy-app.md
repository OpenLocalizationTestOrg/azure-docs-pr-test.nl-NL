---
title: Hiermee stelt u een app op de virtuele-machineschaalset aaaDeploy
description: Extensies toodepoy een app op Azure Virtual Machine-Schaalsets gebruiken.
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Implementeren van uw toepassing op virtuele-machineschaalsets

In dit artikel wordt beschreven hoe u zien hoe van tooinstall software op Hallo Hallo tijdschaal ingesteld is ingericht.

Gewenste tooreview hello [Scale ingesteld ontwerp overzicht](virtual-machine-scale-sets-design-overview.md) artikel worden enkele Hallo-limieten opgelegd door de virtuele-machineschaalsets beschreven.

## <a name="capture-and-reuse-an-image"></a>Vastleggen en een installatiekopie van het opnieuw gebruiken

U kunt een virtuele machine die in Azure tooprepare de installatiekopie van een basis voor de schaal is ingesteld. Dit proces maakt een beheerde schijf in uw opslagaccount die u kunt verwijzen naar als basisinstallatiekopie Hallo voor uw scale set. 

Hallo volgende stappen:

1. Een virtuele Machine van Azure maken
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. Afstand verbinding met virtuele machine Hallo en Hallo system tooyour eigen smaak aanpassen.

   Als u wilt, kunt u nu uw toepassing kunt installeren. Echter weet dat u nu uw toepassing installeert, mag u uw toepassing meer gecompliceerde upgraden omdat u tooremove wellicht het eerste. In plaats daarvan kunt u deze stap tooinstall alle vereisten die uw toepassing mogelijk nodig hebt, zoals een bepaalde functie van de runtime- of -besturingssysteem.

3. Volg 'machine vastleggen' Hallo-zelfstudie voor [Linux] [ linux-vm-capture] of [Windows][windows-vm-capture].

4. Maak een [virtuele-Machineschaalset] [ vmss-create] Hello installatiekopie URI die u in de vorige stap Hallo vastgelegd.

Zie voor meer informatie over schijven [schijven overzicht beheerde](../virtual-machines/windows/managed-disks-overview.md) en [gegevensschijven gekoppeld gebruik](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Installeren wanneer Hallo scale set is ingericht.

Uitbreidingen van de virtuele machine kunnen worden toegepast tooa virtuele-machineschaalset. U kunt Hallo virtuele machines in een instellen als een hele groep schaal aanpassen met de extensie van virtuele machine. Zie voor meer informatie over uitbreidingen [uitbreidingen van de virtuele Machine](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Er zijn drie belangrijkste uitbreidingen die kunt u, als afhankelijk van het besturingssysteem is op basis van Linux of op basis van Windows.

### <a name="windows"></a>Windows

Voor een besturingssysteem op basis van Windows gebruiken beide Hallo **aangepast Script v1.8** -extensie of Hallo **PowerShell DSC** extensie.

#### <a name="custom-script"></a>Aangepast Script

een script wordt uitgevoerd op elk exemplaar van de virtuele machine in de schaalset Hallo van Hallo extensie voor aangepaste scripts. Een configuratiebestand of variabele geeft aan welke bestanden zijn gedownload toohello virtuele machine en vervolgens welke opdracht wordt uitgevoerd. U kunt deze toorun een installatieprogramma, een script, een batchbestand en uitvoerbare bestanden bijvoorbeeld gebruiken.

PowerShell maakt gebruik van een hashtabel voor Hallo-instellingen. In dit voorbeeld configureert Hallo aangepast script extensie toorun een PowerShell-script dat door IIS wordt geïnstalleerd.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Gebruik Hallo `-ProtectedSetting` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

---------


Azure CLI maakt gebruik van een json-bestand voor Hallo-instellingen. In dit voorbeeld configureert Hallo aangepast script extensie toorun een PowerShell-script dat door IIS wordt geïnstalleerd. Opslaan van de volgende json-bestand als Hallo _settings.json_.

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
>Gebruik Hallo `--protected-settings` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

### <a name="powershell-dsc"></a>PowerShell DSC

U kunt de PowerShell DSC toocustomize Hallo scale set vm-exemplaren. Hallo **DSC** extensie gepubliceerd door **Microsoft.Powershell** implementeert en Hallo opgegeven DSC-configuratie op elk exemplaar van de virtuele machine wordt uitgevoerd. Een configuratiebestand of variabele vertelt Hallo-uitbreiding waarin *.zip* pakket is, en welke _script functie_ combinatie toorun.

PowerShell maakt gebruik van een hashtabel voor Hallo-instellingen. In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd.

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Gebruik Hallo `-ProtectedSetting` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

-----------

Azure CLI maakt gebruik van een json voor Hallo-instellingen. In dit voorbeeld implementeert een DSC-pakket dat IIS is geïnstalleerd. Opslaan van de volgende json-bestand als Hallo _settings.json_.

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
>Gebruik Hallo `--protected-settings` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

### <a name="linux"></a>Linux

Linux kunt beide Hallo **aangepast Script v2.0** -extensie of gebruik **cloud init** tijdens het maken van.

Aangepast script is een eenvoudige uitbreiding die u downloadt bestanden toohello virtuele machine-exemplaren en een opdracht wordt uitgevoerd.

#### <a name="custom-script"></a>Aangepast Script

Opslaan van de volgende json-bestand als Hallo _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Gebruik hello Azure CLI tooadd deze extensie tooan bestaande virtuele-machineschaalset. Elke virtuele machine in Hallo schaal instellen automatisch wordt uitgevoerd Hallo extensie.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Gebruik Hallo `--protected-settings` schakelen voor alle instellingen die mogelijk gevoelige gegevens bevatten.

#### <a name="cloud-init"></a>Cloud-Init

Cloud-Init wordt gebruikt wanneer Hallo scale set wordt gemaakt. Maak eerst een lokaal bestand met de naam _cloud init.txt_ en uw tooit configuratie toe te voegen. Zie bijvoorbeeld [deze basisvertalingen](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Gebruik hello Azure CLI toocreate een schaal ingesteld. Hallo `--custom-data` veld accepteert Hallo-bestandsnaam van een cloud-init-script.

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

Als u uw toepassing via een uitbreiding hebt geïmplementeerd, alter Hallo uitbreidingsdefinitie op een bepaalde manier. Deze wijziging wordt Hallo extensie toobe geïmplementeerd tooall virtuele machine-exemplaren. Iets **moet** Azure biedt niet kunnen zien die Hallo extensie is gewijzigd over Hallo-extensie, zoals de naam van een bestand waarnaar wordt verwezen, anders worden gewijzigd.

Als u standaard uitbreidbaar Hallo-toepassing in uw eigen installatiekopie, gebruikt u een pijplijn geautomatiseerde implementatie updates van toepassingen. Ontwerp uw architectuur toofacilitate snel wisselen van een gefaseerde schaal instelt in productie. Een goed voorbeeld van deze benadering is Hallo [Azure Spinnaker stuurprogramma werk](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Verpakker](https://www.packer.io/) en [Terraform](https://www.terraform.io/) ondersteuning voor Azure Resource Manager, zodat u kunt ook uw installatiekopieën 'als de code' definiëren en ze te ontwikkelen in Azure, gebruik vervolgens Hallo VHD in de schaalset. Hierdoor zou dus worden echter problematisch voor installatiekopieën van marketplace, waarbij extensies/aangepaste scripts belangrijker omdat u geen bits van marketplace rechtstreeks bewerken.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Wat gebeurt er wanneer een kan worden geschaald schaalset uit?
Wanneer u een of meer virtuele machines tooa scale set toevoegt, wordt de toepassing hello automatisch geïnstalleerd. Voor het voorbeeld als Hallo schaalset uitbreidingen die zijn gedefinieerd, ze worden uitgevoerd op een nieuwe virtuele machine telkens wanneer die deze is gemaakt. Als Hallo scale set is gebaseerd op een aangepaste installatiekopie, is een nieuwe virtuele machine een kopie van de aangepaste broninstallatiekopie Hallo. Als Hallo scale set virtuele machines container hosts zijn, mogelijk hebt u starten van de code tooload Hallo containers in een extensie voor aangepaste scripts. Of een uitbreiding van een agent die wordt geregistreerd bij de orchestrator van een cluster, zoals Azure Container Service kunt installeren.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Hoe implementatie een OS-update in update domeinen?
Stel dat u wilt dat tooupdate ingesteld terwijl de virtuele-machineschaalset Hallo uw installatiekopie van het besturingssysteem uitgevoerd. PowerShell en hello Azure CLI kunnen Hallo installatiekopieën van virtuele machines, één virtuele machine tegelijk bijwerken. Hallo [upgraden van een virtuele-Machineschaalset](./virtual-machine-scale-sets-upgrade-scale-set.md) artikel bevat ook verdere informatie over welke opties zijn beschikbaar tooperform een besturingssysteem bij het upgraden naar een virtuele-machineschaalset.

## <a name="next-steps"></a>Volgende stappen

* [Gebruik PowerShell toomanage uw schaalset.](virtual-machine-scale-sets-windows-manage.md)
* [Maak een sjabloon van de set schaal.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

