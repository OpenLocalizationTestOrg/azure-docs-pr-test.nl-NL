---
title: Azure-resourcegroepen die VM-extensies bevatten aaaExporting | Microsoft Docs
description: Resource Manager-sjablonen met uitbreidingen van de virtuele machine exporteren.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Exporteren van resourcegroepen met VM-extensies

Azure-resourcegroepen kunnen worden geëxporteerd naar een nieuwe Resource Manager-sjabloon die vervolgens kan worden geïmplementeerd. Hallo exportproces interpreteert bestaande resources en Resource Manager-sjabloon maakt die bij de implementatie resulteert in een vergelijkbare resourcegroep. Wanneer u Hallo resourcegroep exportoptie tegen een bronnengroep met uitbreidingen van de virtuele Machine, worden de verschillende items moeten toobe beschouwd als zoals extensie compatibiliteit en beveiligde instellingen.

De Documentdetails van dit hoe Hallo resourcegroep exportproces werkt met betrekking tot de virtuele machine extensies, met inbegrip van een lijst met ondersteunde extensies en meer informatie over de verwerking van beveiligde gegevens.

## <a name="supported-virtual-machine-extensions"></a>Ondersteunde virtuele machines-extensies

Er zijn veel uitbreidingen van de virtuele Machine beschikbaar. Niet alle uitbreidingen kunnen worden geëxporteerd naar een Resource Manager-sjabloon Hallo 'Automatiseringsscript' gebruiken. Als de extensie van een virtuele machine niet wordt ondersteund, moet deze toobe handmatig terug in de geëxporteerde sjabloon Hallo geplaatst.

Hallo kunnen volgende extensies worden geëxporteerd met Hallo automation script functie.

| Toestelnummer ||||
|---|---|---|---|
| Acronis back-up | Datadog Windows-Agent | Patches voor Linux OS | VM-momentopname Linux
| Back-up Acronis Linux | Docker-uitbreiding | Puppet-Agent |
| BG Info | DSC-extensie | Site 24 x 7 Apm inzicht |
| BMC CTM Agent Linux | Dynatrace Linux | 24 x 7 Linux siteserver |
| BMC CTM Agent Windows | Dynatrace Windows | 24 x 7 Windows siteserver |
| Chef-Client | HPE beveiliging toepassing Defender | Trend Micro DSA |
| Aangepast Script | IaaS Antimalware | Trend Micro DSA Linux |
| Aangepaste scriptextensie | IaaS diagnostische gegevens | Toegang voor Linux VM |
| Aangepast Script voor Linux | Linux Chef-Client | Toegang voor Linux VM |
| Datadog Linux-Agent | Diagnose van Linux | VM-momentopname |

## <a name="export-hello-resource-group"></a>Hallo resourcegroep exporteren

tooexport een resourcegroep in een sjabloon voor herbruikbare voltooid Hallo stappen te volgen:

1. Meld u aan toohello Azure-portal
2. Klik op Hallo Hub-Menu, resourcegroepen
3. Hallo doelresourcegroep in de lijst Hallo selecteren
4. Klik op Hallo resourcegroep blade Automation-Script

![Sjabloon exporteren](./media/extensions-export-templates/template-export.png)

Hello Azure Resource Manager-script voor automatische produceert een Resource Manager-sjabloon, een parameterbestand en implementatie van verschillende voorbeeldscripts zoals PowerShell en Azure CLI. Op dit moment Hallo geëxporteerde sjabloon kan worden gedownload met Hallo downloadknop toegevoegd als een nieuwe sjabloon toohello sjabloonbibliotheek of gedistribueerd met behulp van Hallo implementatieknop.

## <a name="configure-protected-settings"></a>Beveiligde instellingen configureren

Veel virtuele machine van Azure-extensies bevatten een beveiligde instellingen configuratie, waarbij gevoelige gegevens zoals referenties en configuratie tekenreeksen worden gecodeerd. Beveiligde instellingen worden niet geëxporteerd met Hallo automatiseringsscript. Als nodig is, beveiligde instellingen toobe opnieuw in Hallo ingevoegd moeten geëxporteerd sjablonen.

### <a name="step-1---remove-template-parameter"></a>Stap 1 - sjabloonparameter verwijderen

Wanneer Hallo die resourcegroep wordt geëxporteerd, een parameter één sjabloon wordt gemaakt tooprovide geëxporteerd een toohello waarde beveiligde instellingen. Deze parameter kan worden verwijderd. tooremove hello parameter bekijkt hello parameterlijst en Hallo-parameter die er ongeveer vergelijkbaar toothis JSON-voorbeeld uitziet verwijderen.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Stap 2: Get beveiligde eigenschappen

Omdat elk beveiligd instellen van een reeks vereiste eigenschappen heeft, moet een lijst van deze eigenschappen toobe verzameld. Alle parameters van de configuratie van beveiligde Hallo vindt u in Hallo [Azure Resource Manager-schema op GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Dit schema bevat alleen de parametersets Hallo voor Hallo-uitbreidingen die worden vermeld in Hallo overzicht sectie van dit document. 

Uit binnen Hallo schema-opslagplaats, zoeken naar Hallo desired-extensie voor dit voorbeeld `IaaSDiagnostics`. Eenmaal Hallo extensies `protectedSettings` object is gevonden, dient u elke parameter. In voorbeeld Hallo Hallo `IaasDiagnostic` uitbreiding, Hallo vereisen parameters zijn `storageAccountName`, `storageAccountKey`, en `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Stap 3 - Hallo beveiligd configuratie opnieuw maken

Op Hallo van de geëxporteerde sjabloon, zoekt u `protectedSettings` en Hallo geëxporteerde beveiligde instellingsobject vervangen door een nieuwe met extensieparameters Hallo vereist en een waarde voor elk criterium.

In voorbeeld Hallo Hallo `IaasDiagnostic` uitbreiding, Hallo nieuwe beveiligde instelling configuratie eruit zou Hallo voorbeeld te volgen:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

Hallo eindextensie resource lijkt vergelijkbare toohello JSON-voorbeeld te volgen:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Als u de sjabloon parameters tooprovide eigenschapswaarden, moeten deze toobe gemaakt. Als u Sjabloonparameters voor beveiligd waarden in te stellen maakt, ervoor toouse hello `SecureString` parametertype zodat gevoelige waarden zijn beveiligd. Zie voor meer informatie over het gebruik van parameters [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).

In voorbeeld Hallo Hallo `IaasDiagnostic` uitbreiding, Hallo volgende parameters zouden worden gemaakt in Hallo parameters sectie van Hallo Resource Manager-sjabloon.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

Hallo-sjabloon kan op dit moment worden geïmplementeerd met behulp van de implementatiemethode van een sjabloon.
