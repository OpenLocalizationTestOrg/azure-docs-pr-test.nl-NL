---
title: Sleutelkluis geheim met Resource Manager-sjabloon | Microsoft Docs
description: Laat zien hoe een geheim van een sleutelkluis als parameter doorgeven tijdens de implementatie.
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
ms.openlocfilehash: 1ca72599e67e79d42a3d430dbb13e89ea7265334
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-key-vault-to-pass-secure-parameter-value-during-deployment"></a><span data-ttu-id="93f50-103">De Sleutelkluis gebruiken voor veilige parameterwaarde worden doorgegeven tijdens de implementatie</span><span class="sxs-lookup"><span data-stu-id="93f50-103">Use Key Vault to pass secure parameter value during deployment</span></span>

<span data-ttu-id="93f50-104">Wanneer u een beveiligde waarde (zoals een wachtwoord) als een parameter doorgeven tijdens de implementatie moet, kunt u de waarde van de ophalen een [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93f50-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="93f50-105">De waarde wordt opgehaald door te verwijzen naar de sleutelkluis en geheim in de parameter-bestand.</span><span class="sxs-lookup"><span data-stu-id="93f50-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span></span> <span data-ttu-id="93f50-106">De waarde is nooit beschikbaar gemaakt, omdat u alleen verwijzen naar de sleutelkluis-ID.</span><span class="sxs-lookup"><span data-stu-id="93f50-106">The value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="93f50-107">U hoeft niet de waarde handmatig invoeren voor het geheim telkens wanneer die u de resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="93f50-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="93f50-108">De sleutelkluis kan bestaan in een ander abonnement dan de resourcegroep die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="93f50-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span></span> <span data-ttu-id="93f50-109">Wanneer u verwijst naar de sleutelkluis, omvatten u de abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="93f50-109">When referencing the key vault, you include the subscription ID.</span></span>

<span data-ttu-id="93f50-110">Wanneer u de sleutelkluis maakt, stelt de *enabledForTemplateDeployment* eigenschap *true*.</span><span class="sxs-lookup"><span data-stu-id="93f50-110">When creating the key vault, set the *enabledForTemplateDeployment* property to *true*.</span></span> <span data-ttu-id="93f50-111">Deze waarde instelt op true, toestaan u toegang van Resource Manager-sjablonen tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="93f50-111">By setting this value to true, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="93f50-112">Een sleutelkluis en geheim implementeren</span><span class="sxs-lookup"><span data-stu-id="93f50-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="93f50-113">Maakt een sleutelkluis en een geheim, gebruikmaken van Azure CLI of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93f50-113">To create a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="93f50-114">U ziet dat de sleutelkluis is ingeschakeld voor de sjabloonimplementatie van de.</span><span class="sxs-lookup"><span data-stu-id="93f50-114">Notice that the key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="93f50-115">Gebruik voor Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="93f50-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="93f50-116">Gebruik voor PowerShell:</span><span class="sxs-lookup"><span data-stu-id="93f50-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-to-the-secret"></a><span data-ttu-id="93f50-117">Toegang tot het geheim inschakelen</span><span class="sxs-lookup"><span data-stu-id="93f50-117">Enable access to the secret</span></span>

<span data-ttu-id="93f50-118">Of u een nieuwe sleutelkluis of een bestaande gebruikt, zorg ervoor dat de implementatie van de sjabloon gebruiker toegang het geheim tot.</span><span class="sxs-lookup"><span data-stu-id="93f50-118">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span></span> <span data-ttu-id="93f50-119">Het implementeren van een sjabloon die verwijst naar een geheim gebruiker moet beschikken over de `Microsoft.KeyVault/vaults/deploy/action` machtiging voor de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="93f50-119">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span></span> <span data-ttu-id="93f50-120">De [eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) en [Inzender](../active-directory/role-based-access-built-in-roles.md#contributor) beide rollen deze toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="93f50-120">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="93f50-121">U kunt ook maken een [aangepaste rol](../active-directory/role-based-access-control-custom-roles.md) die deze machtiging verleent en de gebruiker toevoegen aan die rol.</span><span class="sxs-lookup"><span data-stu-id="93f50-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span></span> <span data-ttu-id="93f50-122">Zie voor meer informatie over het toevoegen van een gebruiker aan een rol [een gebruiker toewijzen aan beheerdersrollen in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="93f50-122">For information about adding a user to a role, see [Assign a user to administrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="93f50-123">Verwijst naar een geheim met statische-ID</span><span class="sxs-lookup"><span data-stu-id="93f50-123">Reference a secret with static ID</span></span>

<span data-ttu-id="93f50-124">De sjabloon die u een geheim sleutelkluis ontvangt is vergelijkbaar met een andere sjabloon.</span><span class="sxs-lookup"><span data-stu-id="93f50-124">The template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="93f50-125">Dat komt doordat **u verwijzen naar de sleutelkluis in de parameter-bestand niet in de sjabloon.**</span><span class="sxs-lookup"><span data-stu-id="93f50-125">That's because **you reference the key vault in the parameter file, not the template.**</span></span> <span data-ttu-id="93f50-126">Bijvoorbeeld, implementeert u de volgende sjabloon een SQL-database met een administrator-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="93f50-126">For example, the following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="93f50-127">De wachtwoordparameter is ingesteld op een veilige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="93f50-127">The password parameter is set to a secure string.</span></span> <span data-ttu-id="93f50-128">Maar de sjabloon geeft geen waar die waarde worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93f50-128">But, the template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="93f50-129">Maak nu een parameterbestand voor de voorgaande sjabloon.</span><span class="sxs-lookup"><span data-stu-id="93f50-129">Now, create a parameter file for the preceding template.</span></span> <span data-ttu-id="93f50-130">Geef in het parameterbestand een parameter die overeenkomt met de naam van de parameter in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="93f50-130">In the parameter file, specify a parameter that matches the name of the parameter in the template.</span></span> <span data-ttu-id="93f50-131">De waarde van parameter verwijst naar het geheim van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="93f50-131">For the parameter value, reference the secret from the key vault.</span></span> <span data-ttu-id="93f50-132">U verwijzen naar het geheim door het doorgeven van de resource-id van de sleutelkluis en de naam van het geheim.</span><span class="sxs-lookup"><span data-stu-id="93f50-132">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="93f50-133">In het volgende voorbeeld wordt het geheim sleutelkluis moet al bestaan en u een statische waarde opgeven voor de bron-ID.</span><span class="sxs-lookup"><span data-stu-id="93f50-133">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="93f50-134">Verwijst naar een geheim met dynamische ID</span><span class="sxs-lookup"><span data-stu-id="93f50-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="93f50-135">De vorige sectie hebt u geleerd hoe u een statisch resource-ID voor de sleutelkluis-geheim doorgeven.</span><span class="sxs-lookup"><span data-stu-id="93f50-135">The previous section showed how to pass a static resource ID for the key vault secret.</span></span> <span data-ttu-id="93f50-136">In sommige gevallen moet u echter verwijzen naar een sleutelkluis geheim dat varieert op basis van de huidige implementatie.</span><span class="sxs-lookup"><span data-stu-id="93f50-136">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span></span> <span data-ttu-id="93f50-137">In dat geval kunt u niet vastleggen de bron-ID in het parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="93f50-137">In that case, you cannot hard-code the resource ID in the parameters file.</span></span> <span data-ttu-id="93f50-138">Helaas kan niet u dynamisch genereren de resource-ID in het parameterbestand Sjabloonexpressies zijn niet toegestaan in het parameterbestand.</span><span class="sxs-lookup"><span data-stu-id="93f50-138">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span></span>

<span data-ttu-id="93f50-139">Als de resource-ID voor een geheim sleutelkluis dynamisch worden gegenereerd, moet u de resource die het geheim in een geneste sjabloon moet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="93f50-139">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span></span> <span data-ttu-id="93f50-140">In de sjabloon master u de geneste sjabloon toevoegen en geeft u in een parameter die de dynamisch gegenereerde resource-id bevat.</span><span class="sxs-lookup"><span data-stu-id="93f50-140">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93f50-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93f50-141">Next steps</span></span>
* <span data-ttu-id="93f50-142">Raadpleeg voor algemene informatie over sleutelkluizen [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="93f50-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="93f50-143">Zie voor volledige voorbeelden voor het verwijzen naar de sleutel geheimen [Sleutelkluis voorbeelden](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="93f50-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

