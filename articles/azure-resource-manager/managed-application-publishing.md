---
title: aaaCreate en publiceer de toepassing van een Azure-service catalogus beheerd | Microsoft Docs
description: Toont hoe toocreate een Azure-toepassing die is bedoeld voor leden van uw organisatie beheerd.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="f39c0-103">Een beheerde toepassing voor intern verbruik publiceren</span><span class="sxs-lookup"><span data-stu-id="f39c0-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="f39c0-104">U kunt maken en publiceren van Azure [beheerde toepassingen](managed-application-overview.md) die bestemd zijn voor leden van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="f39c0-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="f39c0-105">Een IT-afdeling kan bijvoorbeeld beheerde toepassingen die ervoor zorgen aan de organisatie-standaarden dat publiceren.</span><span class="sxs-lookup"><span data-stu-id="f39c0-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="f39c0-106">Deze beheerde toepassingen zijn beschikbaar via de Servicecatalogus hello, niet hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f39c0-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="f39c0-107">een beheerde toepassingsservices voor de Servicecatalogus hello toopublish, moet u:</span><span class="sxs-lookup"><span data-stu-id="f39c0-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="f39c0-108">Maak een ZIP-pakket dat Hallo drie vereiste sjabloonbestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="f39c0-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="f39c0-109">Bepaal welke gebruiker, groep of toepassing toegang toohello resourcegroep in van de gebruiker van het Hallo-abonnement tot moet.</span><span class="sxs-lookup"><span data-stu-id="f39c0-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="f39c0-110">Hallo beheerde toepassingsdefinitie waarmee verwijst toohello ZIP-pakket en aanvragen van toegang voor Hallo identiteit maken.</span><span class="sxs-lookup"><span data-stu-id="f39c0-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="f39c0-111">Een beheerde toepassingspakket maken</span><span class="sxs-lookup"><span data-stu-id="f39c0-111">Create a managed application package</span></span>

<span data-ttu-id="f39c0-112">de eerste stap Hallo is toocreate Hallo drie vereiste bestanden voor sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f39c0-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="f39c0-113">Alle drie bestanden in een ZIP-bestand van het pakket en upload het tooan toegankelijke locatie, zoals een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f39c0-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="f39c0-114">U doorgeven een koppeling toothis ZIP-bestand wanneer maken Hallo definitie van toepassingen wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="f39c0-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="f39c0-115">**applianceMainTemplate.json**: dit bestand definieert hello Azure resources die zijn ingericht als onderdeel van Hallo beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="f39c0-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="f39c0-116">Hallo sjabloon gaat niet anders dan reguliere Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f39c0-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="f39c0-117">Bijvoorbeeld, een opslagaccount door middel van een beheerde toepassing toocreate, applianceMainTemplate.json bevat:</span><span class="sxs-lookup"><span data-stu-id="f39c0-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="f39c0-118">**mainTemplate.json**: gebruikers kunnen deze sjabloon implementeren wanneer Hallo maken voor toepassing beheerde.</span><span class="sxs-lookup"><span data-stu-id="f39c0-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="f39c0-119">Hiermee definieert u de bron Hallo beheerde toepassing die een resourcetype Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="f39c0-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="f39c0-120">Dit bestand bevat alle Hallo-parameters die u nodig hebt voor Hallo bronnen in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="f39c0-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="f39c0-121">U kunt twee belangrijke eigenschappen instellen in deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f39c0-121">You set two important properties in this template.</span></span> <span data-ttu-id="f39c0-122">Eerst Hallo **applianceDefinitionId** eigenschap is Hallo-ID van de definitie van de toepassing hello beheerd.</span><span class="sxs-lookup"><span data-stu-id="f39c0-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="f39c0-123">U maken Hallo-definitie verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f39c0-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="f39c0-124">Wanneer u deze waarde instelt, moet u bepalen welke abonnement en de resource groep toouse voor het opslaan van beheerde toepassingsservices definities Hallo.</span><span class="sxs-lookup"><span data-stu-id="f39c0-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="f39c0-125">En u moet bepalen van een naam voor de definitie van Hallo.</span><span class="sxs-lookup"><span data-stu-id="f39c0-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="f39c0-126">Hallo-ID is Hallo indeling:</span><span class="sxs-lookup"><span data-stu-id="f39c0-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="f39c0-127">Ten tweede Hallo **managedResourceGroupId** eigenschap is Hallo-ID van de resourcegroep Hallo waar hello Azure-resources worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f39c0-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="f39c0-128">U kunt een waarde op voor de naam van deze resourcegroep toewijzen of zodat de gebruiker van Hallo Geef een naam op.</span><span class="sxs-lookup"><span data-stu-id="f39c0-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="f39c0-129">Hallo-indeling van het Hallo-ID is:</span><span class="sxs-lookup"><span data-stu-id="f39c0-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="f39c0-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="f39c0-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="f39c0-131">Hallo volgende voorbeeld ziet u een bestand mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="f39c0-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="f39c0-132">Hiermee wordt een resourcegroep voor bronnen Hallo geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f39c0-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="f39c0-133">Hallo roldefinitie-ID is een definitie van een benoemde set-toouse **storageApp** in een resourcegroep met de naam **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="f39c0-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="f39c0-134">U kunt deze waarden toouse verschillende namen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f39c0-134">You can change these values toouse different names.</span></span> <span data-ttu-id="f39c0-135">Geef uw eigen abonnement-ID in Hallo definitie-ID.</span><span class="sxs-lookup"><span data-stu-id="f39c0-135">Provide your own subscription ID in hello definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="f39c0-136">**applianceCreateUiDefinition.json**: hello Azure portal maakt gebruik van dit bestand toogenerate Hallo-gebruikersinterface voor gebruikers die maken Hallo beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="f39c0-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="f39c0-137">U definiëren hoe gebruikers de gegevens voor elke parameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="f39c0-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="f39c0-138">U kunt opties kunt gebruiken, zoals een vervolgkeuzelijst, in het tekstvak, wachtwoord en andere hulpprogramma's voor invoer.</span><span class="sxs-lookup"><span data-stu-id="f39c0-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="f39c0-139">hoe een UI-definitiebestand voor een beheerde toepassing toocreate zien toolearn [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="f39c0-140">Hallo volgende voorbeeld ziet u een bestand applianceCreateUiDefinition.json waarmee gebruikers toospecify Hallo storage account voorvoegsel via een tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f39c0-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="f39c0-141">Nadat alle Hallo nodig bestanden klaar bent, kunt u ze als ZIP-bestand pakket.</span><span class="sxs-lookup"><span data-stu-id="f39c0-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="f39c0-142">Hallo drie bestanden moeten zich op het hoofdniveau Hallo van Hallo ZIP-bestand.</span><span class="sxs-lookup"><span data-stu-id="f39c0-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="f39c0-143">Als u deze in een map, foutbericht er een wanneer maken Hallo definitie van de toepassing hello vereiste bestanden zijn niet aanwezig is gemeld dat wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="f39c0-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="f39c0-144">Upload Hallo pakket tooan toegankelijke locatie vanaf waar deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f39c0-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="f39c0-145">Hallo rest van dit artikel wordt ervan uitgegaan Hallo ZIP-bestand aanwezig is op een openbaar toegankelijke opslag-blob-container.</span><span class="sxs-lookup"><span data-stu-id="f39c0-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="f39c0-146">Een groep voor Azure Active Directory-gebruiker of toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f39c0-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="f39c0-147">de tweede stap Hallo is tooselect een gebruikersgroep of toepassing voor het beheren van Hallo bronnen namens de klant Hallo.</span><span class="sxs-lookup"><span data-stu-id="f39c0-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="f39c0-148">Deze, gebruikersgroep of toepassing kunt u de juiste machtigingen heeft op Hallo beheerde bron groep volgens toohello rol die is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f39c0-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="f39c0-149">Hallo-rol kan ingebouwde rollen gebaseerd toegangsbeheer (RBAC)-functie zoals eigenaar of bijdrager zijn.</span><span class="sxs-lookup"><span data-stu-id="f39c0-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="f39c0-150">U kunt geeft ook een afzonderlijke gebruiker machtiging toomanage Hallo resources, maar doorgaans het toewijzen van deze machtiging tooa-gebruikersgroep.</span><span class="sxs-lookup"><span data-stu-id="f39c0-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="f39c0-151">een nieuwe Active Directory-gebruikersgroep toocreate Zie [een groep maken en leden toevoegen in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="f39c0-152">Hallo-object-ID van Hallo gebruiker groep toouse moet u voor het beheren van Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="f39c0-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="f39c0-153">Hallo volgende voorbeeld ziet u hoe tooget object-ID van de weergavenaam van de groep Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="f39c0-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="f39c0-154">Hallo opdracht retourneert Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f39c0-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="f39c0-155">tooretrieve alleen Hallo object-ID, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f39c0-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="f39c0-156">Hallo roldefinitie-ID ophalen</span><span class="sxs-lookup"><span data-stu-id="f39c0-156">Get hello role definition ID</span></span>

<span data-ttu-id="f39c0-157">Vervolgens moet u Hallo roldefinitie-ID van Hallo RBAC ingebouwde rol die u wilt dat toogrant toegang toohello gebruiker, groep of toepassing.</span><span class="sxs-lookup"><span data-stu-id="f39c0-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="f39c0-158">Meestal gebruikt u Hallo eigenaar of bijdrager of lezer rol.</span><span class="sxs-lookup"><span data-stu-id="f39c0-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="f39c0-159">Hallo na de opdracht ziet u hoe tooget roldefinitie-ID voor de rol van eigenaar Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="f39c0-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="f39c0-160">Deze opdracht retourneert Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f39c0-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="f39c0-161">U moet Hallo-waarde van Hallo 'name'-eigenschap van het voorgaande voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="f39c0-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="f39c0-162">U kunt alleen voor die eigenschap met ophalen:</span><span class="sxs-lookup"><span data-stu-id="f39c0-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="f39c0-163">Definitie van de toepassing hello beheerd maken</span><span class="sxs-lookup"><span data-stu-id="f39c0-163">Create hello managed application definition</span></span>

<span data-ttu-id="f39c0-164">Als u nog geen een resourcegroep voor het opslaan van de definitie van de beheerde toepassing, maakt u een nu:</span><span class="sxs-lookup"><span data-stu-id="f39c0-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="f39c0-165">Maak nu Hallo beheerde toepassing definitie resource.</span><span class="sxs-lookup"><span data-stu-id="f39c0-165">Now, create hello managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="f39c0-166">Hallo-parameters gebruikt in het voorgaande voorbeeld Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="f39c0-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="f39c0-167">**resourcegroep**: Hallo-naam van resourcegroep Hallo waar Hallo beheerd voor de toepassingsdefinitie van de wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f39c0-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="f39c0-168">**niveau van de vergrendeling**: Hallo type vergrendeling op Hallo beheerde resourcegroep geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f39c0-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="f39c0-169">Dit voorkomt dat Hallo klant ongewenste bewerkingen uitvoert op deze resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f39c0-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="f39c0-170">Alleen-lezen is momenteel alleen ondersteund vergrendelingsniveau Hallo.</span><span class="sxs-lookup"><span data-stu-id="f39c0-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="f39c0-171">Als alleen-lezen is opgegeven, kan Hallo klant Hallo adresbronnen in Hallo beheerde resourcegroep alleen lezen.</span><span class="sxs-lookup"><span data-stu-id="f39c0-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="f39c0-172">**autorisaties**: beschrijft Hallo principal-ID en Hallo roldefinitie-ID of de gebruikte toogrant machtiging toohello beheerde resourcegroep zijn.</span><span class="sxs-lookup"><span data-stu-id="f39c0-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="f39c0-173">Dit opgegeven in de indeling van Hallo `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="f39c0-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="f39c0-174">Meerdere waarden kunnen ook worden opgegeven voor deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f39c0-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="f39c0-175">Als er meerdere waarden nodig zijn, moeten ze worden opgegeven in Hallo formulier `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="f39c0-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="f39c0-176">Meerdere waarden worden gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="f39c0-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="f39c0-177">**bestands-pakket-uri**: Hallo locatie van Hallo beheerde toepassingspakket met de sjabloonbestanden hello, wat kunnen een Azure Storage-blob.</span><span class="sxs-lookup"><span data-stu-id="f39c0-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f39c0-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f39c0-178">Next steps</span></span>

* <span data-ttu-id="f39c0-179">Zie voor een inleiding toomanaged toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f39c0-180">Zie voor voorbeelden van Hallo bestanden [beheerde toepassing voorbeelden](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="f39c0-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="f39c0-181">Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="f39c0-182">Zie voor meer informatie over publiceren beheerde toepassingen toohello Azure Marketplace [Azure beheerde toepassingen in Hallo Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="f39c0-183">Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="f39c0-184">hoe een UI-definitiebestand voor een beheerde toepassing toocreate zien toolearn [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f39c0-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
