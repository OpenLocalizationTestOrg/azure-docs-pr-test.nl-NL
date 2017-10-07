---
title: aaaBest procedures voor het maken van Resource Manager-sjablonen | Microsoft Docs
description: Richtlijnen voor het vereenvoudigen van uw Azure Resource Manager-sjablonen.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen
Deze richtlijnen kunt u Azure Resource Manager-sjablonen die betrouwbare en eenvoudige toouse zijn maken. Hallo richtlijnen zijn alleen suggesties. Ze zijn geen vereisten, tenzij anders wordt vermeld. Uw scenario mogelijk een variant van een van de Hallo wijze van aanpak of voorbeelden te volgen.

## <a name="resource-names"></a>Resourcenamen
In het algemeen werken u met drie soorten resourcenamen in Resource Manager:

* Resourcenamen moeten uniek zijn.
* Resourcenamen die geen unieke toobe vereist, maar u een naam waarmee u kunt een resource op basis van de context waarin tooprovide kiezen.
* Resourcenamen kunnen niet algemeen zijn.

 Zie voor meer informatie over de beperkingen voor resource [aanbevolen naamgevingsregels voor Azure-resources](../guidance/guidance-naming-conventions.md).

### <a name="unique-resource-names"></a>Unieke resourcenamen
U moet een unieke bronnaam voor resourcetype dat een data access-eindpunt opgeven. Sommige algemene brontypen waarvoor een unieke naam zijn onder andere:

* Azure Storage<sup>1</sup> 
* Web Apps-functie van Azure App Service
* SQL Server
* Azure Key Vault
* Azure Redis-cache
* Azure Batch
* Azure Traffic Manager
* Azure Search
* Azure HDInsight

<sup>1</sup> opslagaccountnamen ook moet een kleine letter, 24 tekens of korter is, en geen eventuele verbindingsstreepjes.

Als u een parameter voor een resourcenaam opgeeft, moet u een unieke naam opgeven bij het implementeren van Hallo resource. Desgewenst kunt u een variabele die gebruikmaakt van Hallo [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate naam van een functie. 

Ook kunt of wilt u een voorvoegsel tooadd achtervoegsel toohello **uniqueString** resultaat. Wijzigen Hallo unieke naam kunt u gemakkelijk herkennen Hallo brontype van Hallo-naam. U kunt bijvoorbeeld een unieke naam voor een opslagaccount genereren met behulp van de volgende variabele Hallo:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Resourcenamen voor identificatie
Sommige brontypen kunt u tooname, maar hun namen hebben geen unieke toobe. U kunt een naam waarmee zowel Hallo resource context en het resourcetype Hallo opgeven voor deze resourcetypen. Geef een beschrijvende naam die helpt u identificeren Hallo-bron in een lijst met bronnen. Als u de naam van een andere bron voor verschillende implementaties toouse moet, kunt u een parameter voor de naam van de Hallo:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Als u niet toopass in een naam tijdens de implementatie hoeft, kunt u een variabele gebruiken: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

U kunt ook een waarde vastgelegde gebruiken:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Algemene resourcenamen
Voor brontypen die u voornamelijk via een andere resource benaderen, kunt u een algemene naam die is vastgelegd in Hallo-sjabloon. U kunt bijvoorbeeld een algemene naam op voor firewallregels instellen op een SQL server:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>Parameters
Hallo kan volgende informatie nuttig zijn wanneer u met parameters werkt:

* Beperk het gebruik van parameters. Gebruik indien mogelijk een variabele of een letterlijke waarde. Parameters gebruiken om alleen voor deze scenario's:
   
   * De instellingen die u wilt dat toouse variaties volgens tooenvironment (SKU, grootte, capaciteit).
   * Resourcenamen wilt u toospecify voor eenvoudige identificatie.
   * De waarden die u vaak toocomplete andere taken (zoals een beheerdersgebruikersnaam gebruikt).
   * Geheimen (zoals wachtwoorden).
   * Hallo getal of matrix met waarden toouse wanneer u meerdere exemplaren van een resourcetype maakt.
* Gebruik kamelen voor namen van parameters.
* Geef een beschrijving van elke parameter in metagegevens Hallo:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Definieer de standaardwaarden voor parameters (met uitzondering van wachtwoorden en SSH-sleutels):
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Gebruik **SecureString** voor alle wachtwoorden en geheimen: 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Indien mogelijk niet gebruiken voor een parameter toospecify locatie. Gebruik in plaats daarvan Hallo **locatie** eigenschap van het Hallo-resourcegroep. Met behulp van Hallo **resourceGroup () .location** -expressie voor al uw resources, resources in de sjabloon Hallo zijn geïmplementeerd in dezelfde locatie als de resourcegroep Hallo Hallo:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Als een resourcetype wordt ondersteund in een beperkt aantal locaties, kunt u een geldige locatie is direct in de sjabloon Hallo toospecify. Als u moet een **locatie** parameter, die zo veel mogelijk parameterwaarde delen met bronnen die zich waarschijnlijk toobe in Hallo dezelfde locatie. Hierdoor minimaliseert Hallo aantal keren dat gebruikers worden gevraagd tooprovide locatie-informatie.
* Vermijd het gebruik van een parameter of variabele voor Hallo API-versie voor een resourcetype. Resource-eigenschappen en waarden kunnen variëren door versienummer. IntelliSense in een code-editor kan niet het juiste schema Hallo bepalen wanneer Hallo API-versie tooa parameter of variabele is ingesteld. In plaats daarvan Hallo harde code in Hallo sjabloon API-versie.

## <a name="variables"></a>Variabelen
Hallo kan volgende informatie nuttig zijn wanneer u met variabelen werkt:

* Variabelen voor waarden die u nodig hebt toouse meer dan één keer in een sjabloon gebruiken. Als een waarde slechts één keer gebruikt wordt, kunt u een waarde vastgelegde uw sjabloon eenvoudiger tooread.
* U kunt geen hello gebruiken [verwijzing](resource-group-template-functions-resource.md#reference) functie in Hallo **variabelen** gedeelte van de sjabloon Hallo. Hallo **verwijzing** functie is afgeleid van de waarde van de runtimestatus van Hallo resource. Variabelen worden echter omgezet tijdens de eerste parseren van de sjabloon Hallo Hallo. Waarden die Hallo moet samenstellen **verwijzing** functie rechtstreeks in Hallo **resources** of **levert** gedeelte van Hallo-sjabloon.
* Variabelen voor de resourcenamen die uniek zijn, zoals beschreven in [Resourcenamen](#resource-names).
* U kunt variabelen groeperen in complexe objecten. Gebruik Hallo **variable.subentry** tooreference een waarde van een complex object opmaken. Variabelen groeperen, kunt u gerelateerde variabelen volgen. Dit verbetert de leesbaarheid van Hallo-sjabloon. Hier volgt een voorbeeld:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Een complex object kan niet een expressie die verwijst naar een waarde van een complex object bevatten. Definieer een afzonderlijke variabele voor dit doel.
   > 
   > 
   
     Zie voor geavanceerde voorbeelden van het gebruik van complexe objecten als variabelen [delen status in Azure Resource Manager-sjablonen](best-practices-resource-manager-state.md).

## <a name="resources"></a>Resources
Hallo kan volgende informatie nuttig zijn wanneer u met resources werkt:

* toohelp andere medewerkers Hallo doel van Hallo resource begrijpen, geef **opmerkingen** voor elke resource in Hallo sjabloon:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* U kunt tags tooadd metagegevens tooresources gebruiken. Gebruik metagegevens tooadd informatie over uw resources. U kunt bijvoorbeeld metagegevens toorecord Factureringsdetails voor een resource toevoegen. Zie voor meer informatie [Using tags tooorganize uw Azure-resources](resource-group-using-tags.md).
* Als u een *openbaar eindpunt* in uw sjabloon (zoals een Azure Blob storage openbaar eindpunt), *komen niet vastleggen* Hallo naamruimte. Gebruik Hallo **verwijzing** functie toodynamically Hallo-naamruimte ophalen. U kunt deze benadering toodeploy Hallo sjabloon toodifferent naamruimte public omgevingen gebruiken zonder Hallo eindpunt in Hallo sjabloon handmatig wijzigen. Hallo API-versie toohello ingesteld dezelfde versie die u in de sjabloon voor Hallo storage-account gebruikt:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Als Hallo storage-account is geïmplementeerd in Hallo dezelfde sjabloon die u maakt, hoeft u niet de naamruimte van de provider Hallo toospecify wanneer u verwijst naar Hallo resource. Dit is Hallo vereenvoudigde syntaxis:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Als u andere waarden in de sjabloon die geconfigureerde toouse een openbare naamruimte hebt, kunt u deze waarden wijzigen tooreflect Hallo dezelfde **verwijzing** functie. U kunt bijvoorbeeld Hallo instellen **storageUri** eigenschap van Hallo virtuele machine diagnostische profiel:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Ook kunt u verwijzen naar een bestaand opslagaccount die zich in een andere resourcegroep:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Wijs openbare IP-adressen tooa virtuele machine alleen wanneer dit vereist is voor een toepassing. tooconnect tooa virtuele machine (VM) voor foutopsporing of voor beheer of administratieve doeleinden inkomende NAT-regels, een virtuele netwerkgateway of een jumpbox gebruiken.
   
     Zie voor meer informatie over het aansluiten van toovirtual machines:
   
   * [Virtuele machines worden uitgevoerd voor een architectuur N-aantal lagen in Azure](../guidance/guidance-compute-n-tier-vm.md)
   * [WinRM toegang instellen voor virtuele machines in Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Toestaan van externe toegang tooyour VM via hello Azure-portal](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Toestaan van externe toegang tooyour virtuele machine met behulp van PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Toestaan van externe toegang tooyour Linux-VM met Azure CLI](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Hallo **domainNameLabel** eigenschap voor openbare IP-adressen moet uniek zijn. Hallo **domainNameLabel** waarde moet tussen 3 en 63 tekens lang en volg Hallo regels die door deze reguliere expressie opgegeven: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Omdat Hallo **uniqueString** functie genereert een tekenreeks die is 13 tekens lang zijn, hello **dnsPrefixString** parameter is beperkt too50 tekens:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Wanneer u een extensie voor aangepaste scripts tooa wachtwoord toevoegt, gebruikt u Hallo **commandToExecute** eigenschap in Hallo **protectedSettings** eigenschap:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure die geheimen zijn versleuteld wanneer ze worden doorgegeven als parameters tooVMs en -extensies, gebruikt u Hallo **protectedSettings** eigenschap van de relevante Hallo-extensies.
   > 
   > 

## <a name="outputs"></a>uitvoer
Als u een sjabloon toocreate openbare IP-adressen gebruikt, voegt u een **levert** sectie gegevens van Hallo IP-adres en Hallo volledig gekwalificeerde domeinnaam (FQDN retourneert). U kunt uitvoer waarden tooeasily ophalen informatie over de openbare IP-adressen en FQDN's gebruiken na de implementatie. Wanneer u verwijst naar resource hello, Hallo API-versie die u hebt gebruikt toocreate gebruiken het: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Één sjabloon versus geneste sjablonen
toodeploy uw oplossing kunt u één sjabloon of een sjabloon van de belangrijkste met meerdere geneste sjablonen. Geneste sjablonen gelden voor meer geavanceerde scenario's. Met behulp van een geneste sjabloon biedt u Hallo volgende voordelen:

* U kunt een oplossing in de betreffende onderdelen uitgesplitst.
* U kunt geneste sjablonen met verschillende belangrijke sjablonen hergebruiken.

Als u toouse geneste sjablonen kiest, kunt Hallo richtlijnen u uw sjabloonontwerp standaardiseren. Deze richtlijnen zijn gebaseerd op [patronen voor Azure Resource Manager-sjablonen ontwerpen](best-practices-resource-manager-design-templates.md). U wordt aangeraden een ontwerp dat het Hallo-sjablonen te volgen:

* **Belangrijkste sjabloon** (azuredeploy.json). Gebruik dit voor de invoerparameters Hallo.
* **Gedeelde bronnen sjabloon**. Gebruik toodeploy gedeelde resources die gebruikmaken van alle andere bronnen (bijvoorbeeld virtuele-netwerk en beschikbaarheid sets). Gebruik Hallo **dependsOn** expressie tooensure dat deze sjabloon wordt geïmplementeerd voordat andere sjablonen.
* **Optionele resources sjabloon**. Gebruik tooconditionally resources op basis van een parameter (bijvoorbeeld een jumpbox) implementeren.
* **Lid resources sjabloon**. Elk exemplaartype binnen een toepassingslaag heeft een eigen configuratie. Binnen een laag, kunt u een ander exemplaar typen definiëren. (Bijvoorbeeld Hallo eerste instantie wordt gemaakt van een cluster en extra exemplaren toohello bestaand cluster worden toegevoegd.) Elk exemplaartype heeft een eigen sjabloon voor de implementatie.
* **Scripts**. Algemeen herbruikbare scripts zijn van toepassing voor elk van exemplaartype (bijvoorbeeld, initialiseren en formatteren extra schijven). Aangepaste scripts die u voor een specifieke aanpassing doel maakt zijn verschillend, op basis van het Hallo-instanceType.

![Geneste sjabloon](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Zie voor meer informatie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Voorwaardelijk toonested sjablonen koppelen
U kunt een parameter tooconditionally koppeling toonested sjablonen gebruiken. Hallo parameter maakt deel uit van Hallo URI voor Hallo sjabloon:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Sjabloon
Het is een goede gewoonte toopass uw sjabloon via een JSON-validator. Een validatiefunctie kunt u Verwijder overbodige komma's, haakjes en haakjes ertoe leiden een fout opgetreden tijdens de implementatie dat kunnen. Probeer [JSONLint](http://jsonlint.com/) of een pakket linter voor uw favoriete omgeving (Visual Studio Code, Atom, Sublime tekst, Visual Studio) bewerken.

Het is ook een goed idee tooformat uw JSON voor een betere leesbaarheid. Voor uw lokale editor kunt u een pakket van JSON-indeling. Druk in Visual Studio, tooformat Hallo-document op **Ctrl + K, Ctrl + D**. Druk in Visual Studio Code op **Alt + Shift + F**. Als uw lokale editor niet Hallo document opmaken, kunt u een [online formatter](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Volgende stappen
* Zie voor instructies over het aanpassen van uw oplossing voor virtuele machines, [een virtuele machine van Windows worden uitgevoerd in Azure](../guidance/guidance-compute-single-vm.md) en [een Linux-VM in Azure uitvoeren](../guidance/guidance-compute-single-vm-linux.md).
* Zie voor instructies over het instellen van een opslagaccount [controlelijst voor prestaties en schaalbaarheid van Azure Storage](../storage/common/storage-performance-checklist.md).
* toolearn over hoe een onderneming met Resource Manager tooeffectively abonnementen beheren, Zie [Azure enterprise scaffold: Prescriptieve abonnement governance](resource-manager-subscription-governance.md).

