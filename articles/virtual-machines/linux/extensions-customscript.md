---
title: aangepaste scripts aaaRun op Linux VM's in Azure | Microsoft Docs
description: Configuratietaken voor Linux-VM automatiseren met behulp van aangepaste Scriptextensie Hallo
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Hello Azure-extensie voor aangepaste scripts gebruiken met Linux virtuele Machines
Hallo aangepaste Scriptextensie worden gedownload en scripts uitgevoerd op virtuele machines in Azure. Deze uitbreiding is nuttig voor post-implementatieconfiguratie, software-installatie of een andere configuratie / beheertaak. Scripts kunnen worden gedownload van Azure storage of andere toegankelijke internetlocatie, of toohello extensie uitvoeringstijd. Hallo-extensie voor aangepaste scripts worden geïntegreerd met Azure Resource Manager-sjablonen en kan ook worden uitgevoerd met hello Azure CLI, PowerShell, Azure-portal of hello Azure virtuele Machine REST-API.

De Documentdetails van dit hoe toouse aangepaste Scriptextensie van Hallo hello Azure CLI en een Azure Resource Manager-sjabloon en details stappen voor probleemoplossing in Linux-systemen.

## <a name="extension-configuration"></a>Configuratie voor uitbreiding
configuratie van de aangepaste Scriptextensie Hallo geeft bijvoorbeeld de locatie van script en Hallo opdracht toobe uitvoeren. Deze configuratie kan worden opgeslagen in de configuratiebestanden, op Hallo vanaf de opdrachtregel of in een Azure Resource Manager-sjabloon opgegeven. Gevoelige gegevens kunnen worden opgeslagen in een beveiligde configuratie die is versleuteld en worden alleen ontsleuteld in Hallo virtuele machine. Hallo is beveiligde handig wanneer Hallo uitvoering opdracht geheimen zoals een wachtwoord bevat.

### <a name="public-configuration"></a>De openbare configuratie
Schema:

**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig. Hallo-namen gebruiken, zoals hieronder tooavoid implementatieproblemen wordt weergegeven.

* **commandToExecute**: (vereist, string) vermelding punt script tooexecute Hallo
* **fileUris**: (optioneel, string array) Hallo-URL's voor bestanden toobe gedownload.
* **tijdstempel** (optioneel, geheel getal) dit veld alleen tootrigger een opnieuw uitvoeren van script hello gebruiken door de waarde van dit veld te wijzigen.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Beveiligde configuratie
Schema:

**Opmerking** -de namen van deze eigenschappen zijn hoofdlettergevoelig. Hallo-namen gebruiken, zoals hieronder tooavoid implementatieproblemen wordt weergegeven.

* **commandToExecute**: (optioneel, string) vermelding punt script tooexecute Hallo. Dit veld in plaats daarvan gebruiken als uw opdracht geheimen zoals wachtwoorden bevat.
* **storageAccountName**: (optioneel, string) Hallo-naam van de storage-account. Als u de storage-referenties opgeeft, moet alle fileUris URL's voor Azure Blobs.
* **storageAccountKey**: (optioneel, string) Hallo toegangssleutel van het opslagaccount.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Azure CLI
Wanneer u hello Azure CLI toorun Hallo extensie voor aangepaste scripts, een configuratiebestand of bestanden met minimale Hallo bestands-uri en Hallo uitvoering scriptopdracht maken.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

Hallo-instellingen kunnen eventueel worden opgegeven in Hallo opdracht als een tekenreeks JSON-indeling. Hierdoor Hallo configuratie toobe tijdens de uitvoering en zonder een afzonderlijk configuratiebestand opgegeven.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Voorbeelden van Azure CLI

**Voorbeeld 1** -openbare configuratie met een scriptbestand.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Azure CLI-opdracht:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Voorbeeld 2** -openbare configuratie zonder script een bestand.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Azure CLI-opdracht:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Voorbeeld 3** - een openbare-configuratiebestand is gebruikte toospecify Hallo-scriptbestand URI en een beveiligde configuratiebestand is gebruikte toospecify Hallo opdracht toobe uitgevoerd.

De openbare configuratie voor bestand:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Beveiligde configuratiebestand:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Azure CLI-opdracht:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Resource Manager-sjabloon
Hello Azure-extensie voor aangepaste scripts kan worden uitgevoerd tijdens de virtuele Machine implementatie met een Resource Manager-sjabloon. toodo toevoegen dus juist opgemaakte JSON toohello-implementatiesjabloon.

### <a name="resource-manager-examples"></a>Voorbeelden van Resource Manager
**Voorbeeld 1** -openbare configuratie.

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**Voorbeeld 2** -opdracht kan worden uitgevoerd in beveiligde configuratie.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
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
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Zie Hallo .net Core muziek Store Demo voor een compleet voorbeeld - [muziek Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Problemen oplossen
Wanneer Hallo aangepaste Scriptextensie wordt uitgevoerd, wordt de Hallo script gemaakt of gedownload naar een map vergelijkbare toohello voorbeeld te volgen. Hallo-opdrachtuitvoer wordt ook opgeslagen in deze map in `stdout` en `stderr` bestand.

```bash
/var/lib/waagent/custom-script/download/0/
```

Hello Azure Scriptextensie produceert een logboek u hier vindt.

```bash
/var/log/azure/custom-script/handler.log
```

de uitvoeringsstatus Hallo Hallo aangepaste Scriptextensie kan ook worden opgehaald met hello Azure CLI.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

Hallo-uitvoer ziet er Hallo volgende tekst:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over andere VM-extensies voor Script [overzicht van de uitbreiding van de Azure-Script voor Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

