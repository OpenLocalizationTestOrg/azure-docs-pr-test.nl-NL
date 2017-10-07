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
# <a name="publish-a-managed-application-for-internal-consumption"></a>Een beheerde toepassing voor intern verbruik publiceren

U kunt maken en publiceren van Azure [beheerde toepassingen](managed-application-overview.md) die bestemd zijn voor leden van uw organisatie. Een IT-afdeling kan bijvoorbeeld beheerde toepassingen die ervoor zorgen aan de organisatie-standaarden dat publiceren. Deze beheerde toepassingen zijn beschikbaar via de Servicecatalogus hello, niet hello Azure Marketplace.

een beheerde toepassingsservices voor de Servicecatalogus hello toopublish, moet u:

* Maak een ZIP-pakket dat Hallo drie vereiste sjabloonbestanden bevat.
* Bepaal welke gebruiker, groep of toepassing toegang toohello resourcegroep in van de gebruiker van het Hallo-abonnement tot moet.
* Hallo beheerde toepassingsdefinitie waarmee verwijst toohello ZIP-pakket en aanvragen van toegang voor Hallo identiteit maken.

## <a name="create-a-managed-application-package"></a>Een beheerde toepassingspakket maken

de eerste stap Hallo is toocreate Hallo drie vereiste bestanden voor sjablonen. Alle drie bestanden in een ZIP-bestand van het pakket en upload het tooan toegankelijke locatie, zoals een opslagaccount. U doorgeven een koppeling toothis ZIP-bestand wanneer maken Hallo definitie van toepassingen wordt beheerd.

* **applianceMainTemplate.json**: dit bestand definieert hello Azure resources die zijn ingericht als onderdeel van Hallo beheerde toepassing. Hallo sjabloon gaat niet anders dan reguliere Resource Manager-sjabloon. Bijvoorbeeld, een opslagaccount door middel van een beheerde toepassing toocreate, applianceMainTemplate.json bevat:

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

* **mainTemplate.json**: gebruikers kunnen deze sjabloon implementeren wanneer Hallo maken voor toepassing beheerde. Hiermee definieert u de bron Hallo beheerde toepassing die een resourcetype Microsoft.Solutions/appliances. Dit bestand bevat alle Hallo-parameters die u nodig hebt voor Hallo bronnen in applianceMainTemplate.json.

  U kunt twee belangrijke eigenschappen instellen in deze sjabloon. Eerst Hallo **applianceDefinitionId** eigenschap is Hallo-ID van de definitie van de toepassing hello beheerd. U maken Hallo-definitie verderop in dit onderwerp. Wanneer u deze waarde instelt, moet u bepalen welke abonnement en de resource groep toouse voor het opslaan van beheerde toepassingsservices definities Hallo. En u moet bepalen van een naam voor de definitie van Hallo. Hallo-ID is Hallo indeling:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  Ten tweede Hallo **managedResourceGroupId** eigenschap is Hallo-ID van de resourcegroep Hallo waar hello Azure-resources worden gemaakt. U kunt een waarde op voor de naam van deze resourcegroep toewijzen of zodat de gebruiker van Hallo Geef een naam op. Hallo-indeling van het Hallo-ID is:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Hallo volgende voorbeeld ziet u een bestand mainTemplate.json. Hiermee wordt een resourcegroep voor bronnen Hallo geïmplementeerd. Hallo roldefinitie-ID is een definitie van een benoemde set-toouse **storageApp** in een resourcegroep met de naam **managedApplicationGroup**. U kunt deze waarden toouse verschillende namen wijzigen. Geef uw eigen abonnement-ID in Hallo definitie-ID.

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

* **applianceCreateUiDefinition.json**: hello Azure portal maakt gebruik van dit bestand toogenerate Hallo-gebruikersinterface voor gebruikers die maken Hallo beheerde toepassing. U definiëren hoe gebruikers de gegevens voor elke parameter opgeven. U kunt opties kunt gebruiken, zoals een vervolgkeuzelijst, in het tekstvak, wachtwoord en andere hulpprogramma's voor invoer. hoe een UI-definitiebestand voor een beheerde toepassing toocreate zien toolearn [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Hallo volgende voorbeeld ziet u een bestand applianceCreateUiDefinition.json waarmee gebruikers toospecify Hallo storage account voorvoegsel via een tekstvak.

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

Nadat alle Hallo nodig bestanden klaar bent, kunt u ze als ZIP-bestand pakket. Hallo drie bestanden moeten zich op het hoofdniveau Hallo van Hallo ZIP-bestand. Als u deze in een map, foutbericht er een wanneer maken Hallo definitie van de toepassing hello vereiste bestanden zijn niet aanwezig is gemeld dat wordt beheerd. Upload Hallo pakket tooan toegankelijke locatie vanaf waar deze kan worden gebruikt. Hallo rest van dit artikel wordt ervan uitgegaan Hallo ZIP-bestand aanwezig is op een openbaar toegankelijke opslag-blob-container.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Een groep voor Azure Active Directory-gebruiker of toepassing maken

de tweede stap Hallo is tooselect een gebruikersgroep of toepassing voor het beheren van Hallo bronnen namens de klant Hallo. Deze, gebruikersgroep of toepassing kunt u de juiste machtigingen heeft op Hallo beheerde bron groep volgens toohello rol die is toegewezen. Hallo-rol kan ingebouwde rollen gebaseerd toegangsbeheer (RBAC)-functie zoals eigenaar of bijdrager zijn. U kunt geeft ook een afzonderlijke gebruiker machtiging toomanage Hallo resources, maar doorgaans het toewijzen van deze machtiging tooa-gebruikersgroep. een nieuwe Active Directory-gebruikersgroep toocreate Zie [een groep maken en leden toevoegen in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

Hallo-object-ID van Hallo gebruiker groep toouse moet u voor het beheren van Hallo resources. Hallo volgende voorbeeld ziet u hoe tooget object-ID van de weergavenaam van de groep Hallo Hallo:

```azurecli-interactive
az ad group show --group exampleGroupName
```

Hallo opdracht retourneert Hallo volgende uitvoer:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

tooretrieve alleen Hallo object-ID, gebruiken:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Hallo roldefinitie-ID ophalen

Vervolgens moet u Hallo roldefinitie-ID van Hallo RBAC ingebouwde rol die u wilt dat toogrant toegang toohello gebruiker, groep of toepassing. Meestal gebruikt u Hallo eigenaar of bijdrager of lezer rol. Hallo na de opdracht ziet u hoe tooget roldefinitie-ID voor de rol van eigenaar Hallo Hallo:


```azurecli-interactive
az role definition list --name owner
```

Deze opdracht retourneert Hallo volgende uitvoer:

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

U moet Hallo-waarde van Hallo 'name'-eigenschap van het voorgaande voorbeeld Hallo. U kunt alleen voor die eigenschap met ophalen:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Definitie van de toepassing hello beheerd maken

Als u nog geen een resourcegroep voor het opslaan van de definitie van de beheerde toepassing, maakt u een nu:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Maak nu Hallo beheerde toepassing definitie resource.

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

Hallo-parameters gebruikt in het voorgaande voorbeeld Hallo zijn:

* **resourcegroep**: Hallo-naam van resourcegroep Hallo waar Hallo beheerd voor de toepassingsdefinitie van de wordt gemaakt.
* **niveau van de vergrendeling**: Hallo type vergrendeling op Hallo beheerde resourcegroep geplaatst. Dit voorkomt dat Hallo klant ongewenste bewerkingen uitvoert op deze resourcegroep. Alleen-lezen is momenteel alleen ondersteund vergrendelingsniveau Hallo. Als alleen-lezen is opgegeven, kan Hallo klant Hallo adresbronnen in Hallo beheerde resourcegroep alleen lezen.
* **autorisaties**: beschrijft Hallo principal-ID en Hallo roldefinitie-ID of de gebruikte toogrant machtiging toohello beheerde resourcegroep zijn. Dit opgegeven in de indeling van Hallo `<principalId>:<roleDefinitionId>`. Meerdere waarden kunnen ook worden opgegeven voor deze eigenschap. Als er meerdere waarden nodig zijn, moeten ze worden opgegeven in Hallo formulier `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Meerdere waarden worden gescheiden door een spatie.
* **bestands-pakket-uri**: Hallo locatie van Hallo beheerde toepassingspakket met de sjabloonbestanden hello, wat kunnen een Azure Storage-blob.

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding toomanaged toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).
* Zie voor voorbeelden van Hallo bestanden [beheerde toepassing voorbeelden](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).
* Zie voor meer informatie over publiceren beheerde toepassingen toohello Azure Marketplace [Azure beheerde toepassingen in Hallo Marketplace](managed-application-author-marketplace.md).
* Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).
* hoe een UI-definitiebestand voor een beheerde toepassing toocreate zien toolearn [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
