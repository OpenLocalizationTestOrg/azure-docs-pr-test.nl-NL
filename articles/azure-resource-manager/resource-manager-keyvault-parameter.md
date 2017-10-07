---
title: aaaKey kluis geheim met Resource Manager-sjabloon | Microsoft Docs
description: Toont hoe een geheim van een sleutel toopass vault als parameter tijdens de implementatie.
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Sleutelkluis toopass beveiligde parameterwaarde gebruiken tijdens de implementatie

Wanneer u een beveiligde waarde (zoals een wachtwoord) toopass als parameter tijdens de implementatie moet, kunt u ophalen Hallo-waarde van een [Azure Key Vault](../key-vault/key-vault-whatis.md). U Hallo waarde wordt opgehaald door te verwijzen naar Hallo sleutelkluis en geheim in de parameterbestand. Hallo-waarde is nooit beschikbaar gemaakt, omdat u alleen verwijzen naar de sleutelkluis-ID. U hoeft geen toomanually Voer Hallo-waarde voor Hallo geheim telkens wanneer u Hallo resources implementeren. Hallo sleutelkluis kan bestaan in een ander abonnement dan Hallo-resourcegroep die u implementeert. Wanneer u verwijst naar de sleutelkluis hello, opnemen u Hallo abonnements-ID.

Bij het maken van de sleutelkluis Hallo Hallo ingesteld *enabledForTemplateDeployment* eigenschap te*true*. Deze waarde tootrue instelt, toestaan u toegang van Resource Manager-sjablonen tijdens de implementatie.  

## <a name="deploy-a-key-vault-and-secret"></a>Een sleutelkluis en geheim implementeren

een sleutelkluis toocreate en geheim gebruiken van Azure CLI of PowerShell. U ziet dat sleutelkluis Hallo voor sjabloonimplementatie is ingeschakeld. 

Gebruik voor Azure CLI:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Gebruik voor PowerShell:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Toegang toohello geheim inschakelen

Of u van een nieuwe sleutelkluis of een bestaande gebruikmaakt, zorg ervoor dat Hallo-gebruiker Hallo-sjabloon implementeren Hallo geheim toegang. Hallo gebruiker implementeren van een sjabloon die verwijst naar een geheim hebben Hallo `Microsoft.KeyVault/vaults/deploy/action` machtiging voor Hallo sleutelkluis. Hallo [eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) en [Inzender](../active-directory/role-based-access-built-in-roles.md#contributor) beide rollen deze toegang verlenen. U kunt ook maken een [aangepaste rol](../active-directory/role-based-access-control-custom-roles.md) die deze machtiging verleent en Hallo toothat gebruikersrol toevoegen. Zie voor meer informatie over het toevoegen van een gebruikersrol tooa [tooadministrator rollen in Azure Active Directory voor een gebruiker toewijzen](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Verwijst naar een geheim met statische-ID

Hallo-sjabloon die u een geheim sleutelkluis ontvangt is vergelijkbaar met een andere sjabloon. Dat komt doordat **u verwijzen naar de sleutelkluis Hallo Hallo parameterbestand, niet Hallo sjabloon.** Bijvoorbeeld, implementeert Hallo na sjabloon een SQL-database met een administrator-wachtwoord. De wachtwoordparameter Hallo is tooa veilige tekenreeks ingesteld. Maar Hallo sjabloon geeft geen waar die waarde worden opgehaald.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

Maak nu een parameterbestand voor Hallo voorafgaand aan de sjabloon. In het parameterbestand hello, moet u een parameter die overeenkomt met de naam van Hallo-parameter in de sjabloon Hallo Hallo opgeven. Hallo-parameterwaarde, verwijst naar Hallo geheim Hallo sleutelkluis. U verwijzen naar Hallo geheim door Hallo resource-id van de sleutelkluis hello en Hallo-naam van Hallo geheim. Hallo sleutelkluis geheim moet al bestaan in Hallo voorbeeld te volgen, en u een statische waarde opgeven voor de bron-ID.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Verwijst naar een geheim met dynamische ID

Hallo vorige sectie hebt u geleerd hoe toopass een statische resource-ID voor de sleutel Hallo geheim kluis. In sommige gevallen moet u echter tooreference een sleutelkluis geheim dat varieert op basis van de huidige implementatie Hallo. U kunt in dat geval niet vastleggen Hallo resource-ID in het parameterbestand Hallo. Helaas kan niet u dynamisch genereren Hallo resource-ID in het parameterbestand Hallo Sjabloonexpressies zijn niet toegestaan in het parameterbestand Hallo.

toodynamically hello resource-ID voor een geheim sleutelkluis genereren, moet u Hallo resource die Hallo geheim in een geneste sjabloon moet verplaatsen. In de sjabloon master u Hallo geneste sjabloon toevoegen en geeft u in een parameter met de Hallo dynamisch gegenereerd bron-ID.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Volgende stappen
* Raadpleeg voor algemene informatie over sleutelkluizen [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).
* Zie voor volledige voorbeelden voor het verwijzen naar de sleutel geheimen [Sleutelkluis voorbeelden](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

