---
title: MSDeploy met hostnaam en ssl-certificaat met een web-app implementeren
description: Een Azure Resource Manager-sjabloon gebruiken voor het implementeren van een web-app met behulp van MSDeploy en aangepaste hostnaam en een SSL-certificaat instellen
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Een web-app met MSDeploy, aangepaste hostnaam en SSL-certificaat implementeren
Deze handleiding helpt bij het maken van de implementatie van een end-to-end voor een Azure-Web-App, gebruik van MSDeploy, evenals een aangepaste hostnaam en een SSL-certificaat toevoegen aan de ARM-sjabloon.

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Voorbeeld van een toepassing maken
U implementeert een ASP.NET-webtoepassing. De eerste stap is om een eenvoudige webtoepassing te maken (of kunt u het gebruik van een bestaande - in dat geval kunt u deze stap overslaan).

Open Visual Studio 2015 en kies Bestand > Nieuw Project. Kies in het dialoogvenster dat verschijnt Web > ASP.NET-webtoepassing. Kies Web onder sjablonen en kies de MVC-sjabloon. Selecteer *verificatietype wijzigen* naar *geen verificatie*. Dit dient alleen voor de voorbeeldtoepassing zo eenvoudig mogelijk te maken.

Op dit moment hebt u een eenvoudige ASP.Net web-app gereed om te gebruiken als onderdeel van uw implementatie.

### <a name="create-msdeploy-package"></a>MSDeploy-pakket maken
Volgende stap is het maken van het pakket voor het implementeren van de web-app in Azure. Om dit te doen, sla het project en voer de volgende vanaf de opdrachtregel:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Hiermee wordt een gecomprimeerde pakket onder de map PackageLocation gemaakt. De toepassing is nu gereed om te worden geïmplementeerd, die u kunt nu opbouwen uit een Azure Resource Manager-sjabloon dat doet.

### <a name="create-arm-template"></a>ARM-sjabloon maken
Eerst laten we beginnen met een eenvoudige ARM-sjabloon die u maakt een webtoepassing en een hosting plan (opmerking die parameters en variabelen niet als beknopt alternatief bevat weergegeven worden).

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

Vervolgens moet u de resource voor de web-app om een geneste MSDeploy-resource te wijzigen. Hierdoor kunt u om te verwijzen naar het pakket eerder hebt gemaakt en Azure Resource Manager het pakket naar de Azure-Web-App implementeren met MSDeploy zien. Hieronder ziet u de bron Microsoft.Web/sites met de geneste MSDeploy-resource:

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

Nu u ziet dat de resource MSDeploy duurt voordat een **packageUri** eigenschap die is gedefinieerd als volgt:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Dit **packageUri** neemt de storage-account-uri die verwijst naar het opslagaccount waar u zult uploaden uw postcode pakket op. De Azure Resource Manager worden benut [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor het ophalen van het pakket naar beneden lokaal vanuit het opslagaccount wanneer u de sjabloon implementeert. Dit proces wordt uitgevoerd via een PowerShell-script die uploaden van het pakket en roept u de Azure Management-API voor het maken van de vereiste sleutels en geef die naar de sjabloon als parameters (*_artifactsLocation* en *_ artifactsLocationSasToken*). U moet de parameters definiëren voor de map en bestandsnaam van het pakket is geüpload naar onder de storage-container.

Vervolgens moet u in een andere geneste resource voor het instellen van de hostnaambindings wilt gebruiken voor een aangepast domein toevoegen. Moet u eerst om ervoor te zorgen dat u de hostnaam en het kan worden gecontroleerd door Azure dat jij de eigenaar ervan - Zie eigenaar [een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md). Wanneer dat is gebeurd, kunt u het volgende kunt toevoegen aan de sjabloon onder de sectie Microsoft.Web/sites resource:

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

Tot slot moet u een andere bovenste niveau resource, Microsoft.Web/certificates toevoegen. Deze bron uw SSL-certificaat bevat en wordt aangelegd op hetzelfde niveau als uw web-app en hosting plannen.

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

U moet een geldig SSL-certificaat hebben om het instellen van deze resource. Zodra u die geldig certificaat hebt moet u het pfx-bytes extraheren als een base64-tekenreeks. Een optie om op te halen dit is het gebruik van de volgende PowerShell-opdracht:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

U kan vervolgens dit als een parameter doorgeven aan de ARM-sjabloon voor implementatie.

De ARM-sjabloon is nu gereed.

### <a name="deploy-template"></a>Sjabloon implementeren
De laatste stappen zijn om dit alles samenvoegen in een volledige end-to-end-implementatie. Om ervoor te implementatie gemakkelijker u gebruikmaken van kunt de **implementeren AzureResourceGroup.ps1** PowerShell-script dat wordt toegevoegd wanneer u een Azure-resourcegroepproject in Visual Studio om u te helpen maken bij het uploaden van alle artefacten die zijn vereist in de de sjabloon. Deze moet u een opslagaccount dat u wilt gebruiken tevoren hebt gemaakt. In dit voorbeeld gemaakt ik een account met gedeelde opslag voor de pakket.zip worden geüpload. Het script wordt gebruikmaken van AzCopy om het uploaden van het pakket naar het opslagaccount. U doorgeeft bij de locatie van de artefacten en het script worden alle bestanden in die map automatisch uploaden naar de benoemde storage-container. U hebt na het aanroepen van implementeren AzureResourceGroup.ps1 en werk vervolgens de SSL-bindingen als u wilt toewijzen van de aangepaste hostnaam vervolgens met de SSL-certificaat.

De volledige implementatie aanroepen van de implementeren ziet u de volgende PowerShell-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

Op dit moment uw toepassing moet zijn geïmplementeerd en moet u kunnen te bladeren via https://www.yourcustomdomain.com

