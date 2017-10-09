---
title: virtuele machine van Azure-extensie voor Linux aaaOMS | Microsoft Docs
description: Hallo OMS-agent op Linux virtuele machine met de extensie van een virtuele machine implementeren.
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Extensie van de virtuele machine OMS voor Linux

## <a name="overview"></a>Overzicht

Operations Management Suite (OMS) biedt mogelijkheden voor bewaking, waarschuwingen en waarschuwing herstel tussen cloud en on-premises activa. Hallo OMS-Agent de extensie van de virtuele machine voor Linux is gepubliceerd en ondersteund door Microsoft. Hallo-extensie Hallo OMS-agent is geïnstalleerd op virtuele machines in Azure en virtuele machines in een bestaande OMS-werkruimte inschrijft. Dit document details Hallo ondersteund platforms, configuraties en implementatie-opties voor de extensie van de virtuele machine OMS Hallo voor Linux.

## <a name="prerequisites"></a>Vereisten

### <a name="operating-system"></a>Besturingssysteem

Hallo-extensie OMS-Agent kan worden uitgevoerd op basis van deze Linux-distributies.

| Distributie | Versie |
|---|---|
| CentOS Linux | 5, 6 en 7 |
| Oracle Linux | 5, 6 en 7 |
| Red Hat Enterprise Linux Server | 5, 6 en 7 |
| Debian GNU/Linux | 6, 7 en 8 |
| Ubuntu | 12.04 TNS, 14.04 TNS, 15.04, 15.10, 16.04 TNS |
| SUSE Linux Enterprise Server | 11 en 12 |

### <a name="internet-connectivity"></a>Internetconnectiviteit

Hallo-extensie OMS-Agent voor Linux is vereist dat Hallo doel-virtuele machine is verbonden toohello internet. 

## <a name="extension-schema"></a>Uitbreidingsschema

Hallo toont volgende JSON Hallo-schema voor Hallo OMS-Agent-extensie. Hallo-uitbreiding vereist Hallo werkruimte-ID en werkruimte sleutel uit Hallo doel OMS-werkruimte. Deze waarden kunnen worden gevonden in Hallo OMS-portal. Omdat Hallo werkruimtesleutel moet worden behandeld als gevoelige gegevens, moet deze worden opgeslagen in de configuratie van een beveiligde instelling. Azure VM-extensie beveiligde instellingsgegevens versleuteld en alleen op de virtuele doelmachine Hallo ontsleuteld. Houd er rekening mee dat **workspaceId** en **workspaceKey** zijn hoofdlettergevoelig.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Eigenschapswaarden

| Naam | Waarde / voorbeeld |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Uitgever | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (bijvoorbeeld) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (bijvoorbeeld) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ == |


## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager-sjablonen. Sjablonen zijn ideaal bij het implementeren van een of meer virtuele machines die na implementatieconfiguratie zoals onboarding tooOMS vereisen. Een voorbeeldsjabloon voor Resource Manager met OMS-Agent VM-extensie voor Hallo vindt u op Hallo [galerie van Azure Quick Start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

Hallo JSON-configuratie voor de extensie van een virtuele machine worden genest in de bron van de virtuele machine Hallo of geplaatst op Hallo bovenste niveau van een Resource Manager JSON-sjabloon. Hallo plaatsing van Hallo JSON-configuratie is van invloed op Hallo-waarde van Hallo resourcenaam en het type. Zie voor meer informatie [naam en type voor de onderliggende resources instellen](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Hallo volgende voorbeeld wordt ervan uitgegaan Hallo OMS-extensie is genest binnen de bron van de virtuele machine Hallo. Wanneer het nesten van Hallo extensie resource Hallo JSON wordt geplaatst in Hallo `"resources": []` object van het Hallo virtuele machine.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Bij het plaatsen van Hallo extensie JSON aan Hallo basis van sjabloon hello, Hallo Resourcenaam bevat een verwijzing toohello bovenliggende virtuele machine en Hallo type reflecteert Hallo geneste configuratie.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Azure CLI-implementatie

Hello Azure CLI mag gebruikte toodeploy Hallo OMS-Agent VM-extensie tooan bestaande virtuele machine. Vervangen door Hallo OMS-sleutel en OMS-ID die uit de OMS-werkruimte. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Oplossen van problemen en ondersteunen

### <a name="troubleshoot"></a>Problemen oplossen

Gegevens over Hallo status van extensie-implementaties kunnen worden opgehaald uit hello Azure-portal en met behulp van hello Azure CLI. Implementatiestatus van toosee Hallo van uitbreidingen voor een bepaalde virtuele machine Hallo volgende opdracht uitvoeren hello Azure CLI.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Uitvoering van de extensie uitvoer volgt geregistreerde toohello bestand:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Foutcodes en hun betekenis

| Foutcode | Betekenis | Mogelijke actie |
| :---: | --- | --- |
| 10 | Virtuele machine is al verbonden tooan OMS-werkruimte | tooconnect hello VM toohello werkruimte die is opgegeven in het Uitbreidingsschema hello, stopOnMultipleConnections toofalse instellen in instellingen voor openbare of verwijdert u deze eigenschap. Deze virtuele machine opgehaald in rekening gebracht zodra voor elke werkruimte is verbonden met. |
| 11 | Ongeldige configuratie opgegeven toohello extensie | Ga als volgt Hallo voorgaande voorbeelden tooset alle eigenschapswaarden die nodig zijn voor implementatie. |
| 12 | Hallo dpkg Pakketbeheer is vergrendeld | Zorg ervoor dat alle dpkg update-bewerkingen op Hallo machine hebt opgegeven en probeer het opnieuw. |
| 20 | Voortijdig aangeroepen inschakelen | [Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello meest recente versie. |
| 51 | Deze extensie wordt niet ondersteund op Hallo van de virtuele machine als besturingssysteem | |
| 55 | Kan geen verbinding maken toohello Microsoft Operations Management Suite-service | Controleer of Hallo systeem toegang heeft toegang tot Internet of een geldige HTTP-proxy is opgegeven. Controleer daarnaast Hallo juistheid van Hallo werkruimte-ID. |

Extra informatie over probleemoplossing vindt u op Hallo [OMS-Agent voor Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Ondersteuning

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op Hallo [MSDN Azure en Stack Overflow-forums](https://azure.microsoft.com/en-us/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/en-us/support/options/) en selecteer de Get-ondersteuning. Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](https://azure.microsoft.com/en-us/support/faq/).
