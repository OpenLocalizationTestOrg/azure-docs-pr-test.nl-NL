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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="d459c-103">Sleutelkluis toopass beveiligde parameterwaarde gebruiken tijdens de implementatie</span><span class="sxs-lookup"><span data-stu-id="d459c-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="d459c-104">Wanneer u een beveiligde waarde (zoals een wachtwoord) toopass als parameter tijdens de implementatie moet, kunt u ophalen Hallo-waarde van een [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d459c-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="d459c-105">U Hallo waarde wordt opgehaald door te verwijzen naar Hallo sleutelkluis en geheim in de parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="d459c-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="d459c-106">Hallo-waarde is nooit beschikbaar gemaakt, omdat u alleen verwijzen naar de sleutelkluis-ID.</span><span class="sxs-lookup"><span data-stu-id="d459c-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="d459c-107">U hoeft geen toomanually Voer Hallo-waarde voor Hallo geheim telkens wanneer u Hallo resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="d459c-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="d459c-108">Hallo sleutelkluis kan bestaan in een ander abonnement dan Hallo-resourcegroep die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="d459c-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="d459c-109">Wanneer u verwijst naar de sleutelkluis hello, opnemen u Hallo abonnements-ID.</span><span class="sxs-lookup"><span data-stu-id="d459c-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="d459c-110">Bij het maken van de sleutelkluis Hallo Hallo ingesteld *enabledForTemplateDeployment* eigenschap te*true*.</span><span class="sxs-lookup"><span data-stu-id="d459c-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="d459c-111">Deze waarde tootrue instelt, toestaan u toegang van Resource Manager-sjablonen tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="d459c-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="d459c-112">Een sleutelkluis en geheim implementeren</span><span class="sxs-lookup"><span data-stu-id="d459c-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="d459c-113">een sleutelkluis toocreate en geheim gebruiken van Azure CLI of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d459c-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="d459c-114">U ziet dat sleutelkluis Hallo voor sjabloonimplementatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d459c-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="d459c-115">Gebruik voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="d459c-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="d459c-116">Gebruik voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d459c-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="d459c-117">Toegang toohello geheim inschakelen</span><span class="sxs-lookup"><span data-stu-id="d459c-117">Enable access toohello secret</span></span>

<span data-ttu-id="d459c-118">Of u van een nieuwe sleutelkluis of een bestaande gebruikmaakt, zorg ervoor dat Hallo-gebruiker Hallo-sjabloon implementeren Hallo geheim toegang.</span><span class="sxs-lookup"><span data-stu-id="d459c-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="d459c-119">Hallo gebruiker implementeren van een sjabloon die verwijst naar een geheim hebben Hallo `Microsoft.KeyVault/vaults/deploy/action` machtiging voor Hallo sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="d459c-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="d459c-120">Hallo [eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) en [Inzender](../active-directory/role-based-access-built-in-roles.md#contributor) beide rollen deze toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="d459c-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="d459c-121">U kunt ook maken een [aangepaste rol](../active-directory/role-based-access-control-custom-roles.md) die deze machtiging verleent en Hallo toothat gebruikersrol toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d459c-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="d459c-122">Zie voor meer informatie over het toevoegen van een gebruikersrol tooa [tooadministrator rollen in Azure Active Directory voor een gebruiker toewijzen](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d459c-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="d459c-123">Verwijst naar een geheim met statische-ID</span><span class="sxs-lookup"><span data-stu-id="d459c-123">Reference a secret with static ID</span></span>

<span data-ttu-id="d459c-124">Hallo-sjabloon die u een geheim sleutelkluis ontvangt is vergelijkbaar met een andere sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d459c-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="d459c-125">Dat komt doordat **u verwijzen naar de sleutelkluis Hallo Hallo parameterbestand, niet Hallo sjabloon.**</span><span class="sxs-lookup"><span data-stu-id="d459c-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="d459c-126">Bijvoorbeeld, implementeert Hallo na sjabloon een SQL-database met een administrator-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d459c-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="d459c-127">De wachtwoordparameter Hallo is tooa veilige tekenreeks ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d459c-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="d459c-128">Maar Hallo sjabloon geeft geen waar die waarde worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d459c-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="d459c-129">Maak nu een parameterbestand voor Hallo voorafgaand aan de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d459c-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="d459c-130">In het parameterbestand hello, moet u een parameter die overeenkomt met de naam van Hallo-parameter in de sjabloon Hallo Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="d459c-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="d459c-131">Hallo-parameterwaarde, verwijst naar Hallo geheim Hallo sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="d459c-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="d459c-132">U verwijzen naar Hallo geheim door Hallo resource-id van de sleutelkluis hello en Hallo-naam van Hallo geheim.</span><span class="sxs-lookup"><span data-stu-id="d459c-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="d459c-133">Hallo sleutelkluis geheim moet al bestaan in Hallo voorbeeld te volgen, en u een statische waarde opgeven voor de bron-ID.</span><span class="sxs-lookup"><span data-stu-id="d459c-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="d459c-134">Verwijst naar een geheim met dynamische ID</span><span class="sxs-lookup"><span data-stu-id="d459c-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="d459c-135">Hallo vorige sectie hebt u geleerd hoe toopass een statische resource-ID voor de sleutel Hallo geheim kluis.</span><span class="sxs-lookup"><span data-stu-id="d459c-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="d459c-136">In sommige gevallen moet u echter tooreference een sleutelkluis geheim dat varieert op basis van de huidige implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d459c-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="d459c-137">U kunt in dat geval niet vastleggen Hallo resource-ID in het parameterbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="d459c-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="d459c-138">Helaas kan niet u dynamisch genereren Hallo resource-ID in het parameterbestand Hallo Sjabloonexpressies zijn niet toegestaan in het parameterbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="d459c-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="d459c-139">toodynamically hello resource-ID voor een geheim sleutelkluis genereren, moet u Hallo resource die Hallo geheim in een geneste sjabloon moet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="d459c-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="d459c-140">In de sjabloon master u Hallo geneste sjabloon toevoegen en geeft u in een parameter met de Hallo dynamisch gegenereerd bron-ID.</span><span class="sxs-lookup"><span data-stu-id="d459c-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d459c-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d459c-141">Next steps</span></span>
* <span data-ttu-id="d459c-142">Raadpleeg voor algemene informatie over sleutelkluizen [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d459c-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="d459c-143">Zie voor volledige voorbeelden voor het verwijzen naar de sleutel geheimen [Sleutelkluis voorbeelden](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="d459c-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

