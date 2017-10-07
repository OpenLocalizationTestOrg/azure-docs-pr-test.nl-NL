---
title: aaaVirtual machine extensies en functies voor Linux | Microsoft Docs
description: Meer informatie over welke extensies beschikbaar zijn voor virtuele machines in Azure, gegroepeerd op wat ze bieden of verbeteren.
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Uitbreidingen van de virtuele machine en functies voor Linux

Virtuele machine van Azure-extensies zijn kleine toepassingen waarmee de configuratie en automatisering taken na de implementatie op virtuele machines in Azure. Als een virtuele machine vereist een software-installatie, beveiliging tegen virussen of Docker-configuratie, een VM-extensie kan bijvoorbeeld worden gebruikt toocomplete deze taken. Azure VM-extensies kunnen worden uitgevoerd met hello Azure CLI, Azure Resource Manager-sjablonen, PowerShell en hello Azure-portal. Extensies worden gebundeld met een nieuwe implementatie van de virtuele machine of eventuele bestaande systeem uitgevoerd.

Dit document bevat een overzicht van de VM-extensies voor vereisten voor het gebruik van Azure VM-extensies en richtlijnen over hoe toodetect, beheren en verwijderen van de VM-extensies. Dit document vindt u algemene informatie omdat veel VM-extensies beschikbaar zijn, elk met een potentieel unieke configuratie. Extensie-specifieke informatie vindt u in elke afzonderlijke document specifieke toohello-extensie.

## <a name="use-cases-and-samples"></a>Gebruiksvoorbeelden en voorbeelden

Enkele andere Azure VM-extensies beschikbaar zijn, elk met een specifieke gebruiksvoorbeeld. Een aantal voorbeelden:

- Status van PowerShell gewenste configuraties tooa virtuele machine met behulp van Hallo DSC-extensie voor Linux toepassen. Zie voor meer informatie [Azure gewenst State configuration-uitbreiding](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Bewaking van een virtuele machine met Microsoft Monitoring Agent VM-extensie Hallo configureren. Zie voor meer informatie [hoe toomonitor een Linux-VM](tutorial-monitoring.md).
- Bewaking van uw Azure-infrastructuur met Hallo Datadog-uitbreiding configureren. Zie voor meer informatie, Hallo [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configureer een Docker-host op een virtuele machine van Azure met behulp van Hallo Docker VM-extensie. Zie voor meer informatie [Docker VM-extensie](dockerextension.md).

Bovendien tooprocess-specifieke uitbreidingen, een extensie voor aangepaste scripts is beschikbaar voor Windows- en Linux virtuele machines. Hallo-extensie voor aangepaste scripts voor Linux kunt eventuele Bash script toobe uitvoeren op een virtuele machine. Aangepaste scripts zijn handig voor het ontwerpen van Azure-implementaties die moeten worden geconfigureerd afgezien van wat systeemeigen Azure tooling kan bieden. Zie voor meer informatie [Linux VM aangepaste scriptextensie](extensions-customscript.md).


## <a name="prerequisites"></a>Vereisten

De extensie van elke virtuele machine mogelijk een eigen set vereisten. Hallo Docker VM-extensie heeft bijvoorbeeld een vereiste van een ondersteunde Linux-distributie. Vereisten van afzonderlijke uitbreidingen zijn aangegeven in het Hallo-extensie-specifieke documentatie.

### <a name="azure-vm-agent"></a>Azure VM-agent

Hello Azure VM-agent beheert interactie tussen een virtuele machine van Azure en hello Azure-infrastructuurcontroller. Hallo VM-agent is verantwoordelijk voor veel functionele aspecten van het implementeren en beheren van virtuele machines in Azure, waaronder het uitvoeren van de VM-extensies. Hello Azure VM-agent is geïnstalleerd op Azure Marketplace-installatiekopieën en kan handmatig worden geïnstalleerd op ondersteunde besturingssystemen.

Zie voor informatie over ondersteunde besturingssystemen en installatie-instructies, [virtuele machine van Azure-agent](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>VM-extensies detecteren

Veel andere VM-extensies zijn beschikbaar voor gebruik met virtuele machines in Azure. toosee een volledige lijst Hallo de volgende opdracht met hello Azure CLI, Hallo Voorbeeldlocatie vervangen door een Hallo-locatie van uw keuze uitvoeren.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>VM-extensies worden uitgevoerd

Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op de bestaande virtuele machines, die handig zijn als u de verbinding op een reeds geïmplementeerde virtuele machine herstellen of toomake configuratiewijzigingen nodig. VM-extensies kunnen ook worden gebundeld met implementaties van Azure Resource Manager-sjabloon. Via uitbreidingen met Resource Manager-sjablonen kunnen virtuele machines in Azure worden geïmplementeerd en geconfigureerd zonder tussenkomst van de na de implementatie.

Hallo volgende methoden kan worden gebruikt toorun een uitbreiding op basis van een bestaande virtuele machine.

### <a name="azure-cli"></a>Azure CLI

Uitbreidingen van de virtuele machine van Azure kunnen worden uitgevoerd op basis van een bestaande virtuele machine met behulp van Hallo `az vm extension set` opdracht. In dit voorbeeld voert Hallo-extensie voor aangepaste scripts op basis van een virtuele machine.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Hallo script produceert uitvoer vergelijkbare toohello volgende tekst:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Azure Portal

VM-extensies mag toegepaste tooan bestaande virtuele machine via hello Azure-portal. toodo hello virtuele machine, dus selecteer kiezen **extensies**, en klik op **toevoegen**. Hallo-extensie gewenste uit Hallo lijst met beschikbare uitbreidingen en Hallo-instructies in de wizard Hallo selecteren.

Hallo toont volgende afbeelding Hallo-installatie van Hallo Linux aangepaste scriptextensie van hello Azure-portal.

![Extensie voor aangepaste scripts installeren](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Azure Resource Manager-sjablonen

VM-extensies kunnen toegevoegde tooan Azure Resource Manager-sjabloon en uitgevoerd met de implementatie van de sjabloon Hallo Hallo. Wanneer u een uitbreiding met een sjabloon implementeert, kunt u volledig geconfigureerde Azure-implementaties. Bijvoorbeeld: hello die volgende JSON is genomen van de Resource Manager-sjabloon. Hallo sjabloon implementeert een set van netwerktaakverdeling virtuele machines en een Azure SQL database, en installeert een toepassing .NET Core op elke virtuele machine. Hallo VM-extensie zorgt voor Hallo software-installatie.

Zie voor meer informatie, Hallo volledige [Resource Manager-sjabloon](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Zie voor meer informatie [Azure Resource Manager-sjablonen samenstellen](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Beveiligde gegevens van de VM-extensie

Wanneer u een VM-extensie uitvoert, kan het benodigde tooinclude gevoelige informatie zoals referenties, namen van opslagaccounts en toegang tot de opslagaccountsleutels zijn. Veel VM-extensies bevatten een beveiligde configuratie die gegevens versleutelt en ontsleutelt deze alleen in de virtuele doelmachine Hallo. Elke uitbreiding heeft een specifieke beveiligde configuratieschema en elk wordt beschreven in de uitbreiding specifieke documentatie bij.

Hallo volgende voorbeeld ziet u een exemplaar van de aangepaste scriptextensie Hallo voor Linux. U ziet dat tooexecute Hallo-opdracht bevat een set referenties. In dit voorbeeld Hallo opdracht tooexecute niet versleuteld.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Zwevend Hallo **opdracht tooexecute** eigenschap toohello **beveiligd** configuratie beveiligt Hallo uitvoering tekenreeks.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>VM-extensies oplossen

Elk VM-extensie wellicht stappen specifieke toohello extensie probleemoplossing. Bijvoorbeeld, wanneer u Hallo aangepaste scriptextensie, script uitvoering details zijn te vinden lokaal op Hallo virtuele machine waarop Hallo-extensie is uitgevoerd. Probleemoplossing-extensie-specifieke worden beschreven in de documentatie van de extensie-specifieke.

Hallo volgende stappen voor probleemoplossing toepassing tooall-extensies voor virtuele machine.

### <a name="view-extension-status"></a>Status van de extensie weergeven

Nadat u de extensie van een virtuele machine is uitgevoerd voor een virtuele machine, gebruik Hallo status van de Azure CLI opdracht tooreturn-extensie te volgen. Parameternamen voorbeeld vervangen door uw eigen waarden.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Hallo-uitvoer ziet er Hallo volgende tekst:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Status van extensie-uitvoering kan worden gevonden in hello Azure-portal. tooview hello status van een extensie, selecteer Hallo virtuele machine kiezen **extensies**, en selecteer de gewenste extensie Hallo.

### <a name="rerun-a-vm-extension"></a>Voer een VM-extensie

Mogelijk zijn er gevallen waarin de extensie van een virtuele machine toobe moet opnieuw uit. U kunt een uitbreiding opnieuw uitvoeren te verwijderen en vervolgens opnieuw uit te voeren Hallo-extensie met een methode van de uitvoering van uw keuze. tooremove een uitbreiding Hallo volgende opdracht met hello Azure CLI uitvoeren. Parameternamen voorbeeld vervangen door uw eigen waarden.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

U kunt een uitbreiding verwijderen met behulp van Hallo stappen te volgen in hello Azure-portal:

1. Selecteer een virtuele machine.
2. Kies **extensies**.
3. Selecteer Hallo gewenste extensie.
4. Kies **verwijderen**.

## <a name="common-vm-extension-reference"></a>Algemene referentie voor VM-extensie
| Naam van de uitbreiding | Beschrijving | Meer informatie |
| --- | --- | --- |
| Extensie voor aangepaste scripts voor Linux |Scripts uitvoeren op een virtuele machine van Azure |[Extensie voor aangepaste scripts voor Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Docker-uitbreiding |Hallo Docker-daemon toosupport externe Docker opdrachten installeren. |[Docker-VM-extensie](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| VM-extensie voor toegang |Toegang tooan Azure virtuele machine herstellen |[VM-extensie voor toegang](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Azure extensie voor diagnostische gegevens |Azure Diagnostics beheren |[Azure extensie voor diagnostische gegevens](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| De extensie Azure VM-toegang |Gebruikers en referenties beheren |[Uitbreiding van de VM-toegang voor Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
